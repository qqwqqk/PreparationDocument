# CSS 相关

## link 与 @import 加载的区别
>link 基本语法
```HTML
  <link rel="stylesheet" href="css/index.css">
```
>@import
```CSS 基本语法
  @charse "utf-8";
  @import url(css/index.css);
```
| |link | @import |
|-|-| -|
|种类|HTML标签|CSS提供的方式|
|加载顺序|页面加载时加载|页面全部下载完后加载|
|兼容性|全兼容|CSS2.1后兼容|
|样式权重|高|低|
|DOM可控|JavaScript控制页面样式时能使用link|不可以通过DOM控制|

## CSS 预处理器
>Less
>>Less 是一门 CSS 预处理语言，它扩展了 CSS 语言，增加了变量、Mixin、函数等特性，使 CSS 更易维护和扩展。
>>Less 可以运行在 Node 或浏览器端。
>Sass
>>Sass（Syntactically Awesome Stylesheet）是一个CSS预处理器，有助于减少CSS的重复，节省时间。 它是更稳定和强大的CSS扩展语言描述文档的风格结构。

## CSS 自定义
CSS中原生的变量定义语法是：--*， 变量使用语法是var(--*),其中*表示我们的变量名称。
```CSS
:root{
  --theme-color:#39C5BB;
}
.theme1{
  background: var(--theme-color);
}
.theme2{
  background: var(--theme-color);
}
```
使用JavaScript中的setProperty() 方法用于设置一个新的 CSS 属性，或修改 CSS 声明块中已存在的属性。
```JavaScript
  document.body.style.setProperty('--theme-color',"#66CCFF");
```

## CSS 单位（尺寸）
| 单位|描述 |
|-|-|
|in|英寸|
|cm|厘米|
|mm|毫米|
|em|当前字体倍数|
|ex|当前字体半倍|
|pt|磅|
|pc|12点|
|px|像素|

## calc 属性
>calc() 函数用于动态计算长度值。
>>需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；
>>任何长度值都可以使用calc()函数进行计算；
>>calc()函数支持 "+", "-", "*", "/" 运算；
>>calc()函数使用标准的数学运算优先级规则；

## CSS 优先级
>Rule 1: 最近的祖先样式比其他祖先样式优先级高。
```HTML
<!-- 类名为 son 的 div 的 color 为 blue -->
<div style="color: red">
  <div style="color: blue">
    <div class="son"></div>
  </div>
</div>
```
>Rule 1: 最近的祖先样式比其他祖先样式优先级高。
```HTML
<!-- 类名为 son 的 div 的 color 为 blue -->
<div style="color: red">
  <div style="color: blue">
    <div class="son"></div>
  </div>
</div>
```
>Rule 2: "直接样式"比"祖先样式"优先级高。
```HTML
<!-- 类名为 son 的 div 的 color 为 blue -->
<div style="color: red">
  <div class="son" style="color: blue"></div>
</div>
```
>Rule 3: 优先级关系：内联样式 > ID 选择器 > 类选择器 = 属性选择器 = 伪类选择器 > 标签选择器 = 伪元素选择器
```HTML
<!-- div 的 color 为 black -->
<div class="content-class" id="content-id" style="color: black"></div>
<style>
  #content-id {
    color: red;
  }
  .content-class {
    color: blue;
  }
  div {
    color: grey;
  }
</style>
```
>Rule 4: 计算选择符中 ID 选择器的个数（a），计算选择符中类选择器、属性选择器以及伪类选择器的个数之和（b），计算选择符中标签选择器和伪元素选择器的个数之和（c）。按 a、b、c 的顺序依次比较大小，大的则优先级高，相等则比较下一个。若最后两个的选择符中 a、b、c 都相等，则按照"就近原则"来判断。
```HTML
<!-- div 的 color 为 red -->
<div id="con-id">
    <span class="con-span"></span>
</div>
<style>
  #con-id span {
    color: red;
  }
  div .con-span {
    color: blue;
  }
</style>
```
>Rule 5: 属性后插有 !important 的属性拥有最高优先级。若同时插有 !important，则再利用规则 3、4 判断优先级。
```HTML
<!-- div 的 color 为 red -->
<div class="father">
    <p class="son"></p>
</div>
<style>
  p {
    background: red !important;
  }
  .father .son {
    background: blue;
  }
</style>
```
>Error
>>选择器加权值的说法，即 ID 选择器权值为 100，类选择器权值为 10，标签选择器权值为 1，当一个选择器由多个 ID 选择器、类选择器或标签选择器组成时，则将所有权值相加，然后再比较权值。这种说法其实是有问题的。比如一个由 11 个类选择器组成的选择器和一个由 1 个 ID 选择器组成的选择器指向同一个标签，按理说 110 > 100，应该应用前者的样式，然而事实是应用后者的样式。错误的原因是：选择器的权值不能进位。还是拿刚刚的例子说明。11 个类选择器组成的选择器的总权值为 110，但因为 11 个均为类选择器，所以其实总权值最多不能超过 100， 你可以理解为 99.99，所以最终应用后者样式。