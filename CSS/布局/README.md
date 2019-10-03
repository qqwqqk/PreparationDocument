# CSS 布局相关

1. [Flex 布局](#Flex-布局)
2. [经典三栏布局方案](#经典三栏布局方案)
3. [垂直居中实现方案](#垂直居中实现方案)
4. [多列等高实现方案](#多列等高实现方案)
5. [多列排版实现方案](#多列排版实现方案)
6. [块格式化上下文](#块格式化上下文)
7. [清除浮动](#清除浮动)
8. [DOM 元素隐藏](#DOM-元素隐藏)
9. [外边距折叠](#外边距折叠)
10. [Position 定位](#Position-定位)

## Flex 布局
Flex 是 Flexible Box 的缩写,意为"弹性布局",用来为盒状模型提供最大的灵活性.  
任何一个容器都可以指定为 Flex 布局.行内元素也可以使用 Flex 布局.  
Webkit 内核的浏览器,必须加上-webkit前缀.  
设为 Flex 布局以后,子元素的float、clear和vertical-align属性将失效.  

```CSS
.box { 
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  /* flex-flow: row nowrap; */
  justify-content: flex-start;
  align-items: flex-start;
  align-content: stretch;
} 
```

|属性名 |值 |描述|
|-|-|-|
|flex-direction|row,row-reverse, column, column-reverse| 子元素排列方向 |
|flex-wrap| nowrap, wrap, wrap-reverse | 换行规则 |
|flex-flow| `<flex-direction>` `<flex-wrap>` | flex-direction属性和flex-wrap属性的简写形式 |
|justify-content| flex-start, flex-end,center,space-between, space-around| 子元素横向的对齐方式|
|align-items|flex-start, flex-end, center, baseline, stretch| 子元素纵向的对齐方式|
|align-content|flex-start, flex-end, center, space-between, space-around, stretch| 多行元素的对齐方式|

```CSS
.subbox { 
  order: 0;
  flex-grow: 0;
  flex-shrink: 0;
  flex-basis: auto;
  /* flex: 0 1 auto;  auto(1 1 auto)|none(0 0 auto) */
  align-self: auto;
} 
```

|属性名 |默认值 |描述|
|-|-|-|
|order|0|元素排列顺序.数值越小,排列越靠前|
|flex-grow| 0| 元素放大比例,等分剩余空间,默认值0不参与 |
|flex-shrink|0|元素缩小比例,等分剩余空间,默认值0不参与 |
|flex-basis|auto| 定义元素占位长度(余下部分计算剩余空间), 默认值为全元素|
|flex| 0 1 auto | flex-grow, flex-shrink 和 flex-basis的简写|
|align-self| auto |允许元素存在与其他元素不一样的对齐方式,可覆盖align-items属性|

## 经典三栏布局方案
1. float布局
```HTML
<style>
  .left {
    float: left;
    width: 100px;
    height: 200px;
  }
  .right {
    float: right;
    width: 100px;
    height: 200px;
  }
  .main {
    height: 200px;
    margin-left: 120px;
    margin-right: 120px;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main"></div>
  <div class="right"></div>
</div>
```

2. BFC 规则
```HTML
<style>
  .left {
    float: left;
    width: 100px;
    height: 200px;
  }
  .right {
    float: right;
    width: 100px;
    height: 200px;
  }
  .main {
    height: 200px;
    overflow: hidden;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main"></div>
  <div class="right"></div>
</div>
```

3. 圣杯布局
```HTML
<style>
  .left {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100%;
    position: relative;
    left: -100px;
  }
  .right {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100px;
    position: relative;
    left: -100px;
  }
  .main {
    float: left;
    width: 100%;
    height: 200px;
  }
  .container{
    padding-left: 100px;
    padding-right: 100px;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main"></div>
  <div class="right"></div>
</div>
```

4. 双飞翼布局
```HTML
<style>
  .left {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100%;
  }
  .right {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100px;
  }
  .main {
    float: left;
    width: 100%;
    height: 200px;
  }
  .main::after{
    display: block;
    content: '';
    height: 0;
    font-size: 0;
    clear: both;
    zoom: 1;
  }
  .content{
    height:200px;
    margin: 0 110px;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main">
    <div class="content"></div>
  </div>
  <div class="right"></div>
</div>
```

5. Flex 布局
```HTML
<style>
  .left {
    height: 200px;
    order: -1;
    flex: 0 1 200px;
  }
  .right {
    height: 200px;
    order: 1;
    flex: 0 1 200px;
  }
  .main {
    height: 200px;
    order: 0;
    flex-grow: 1;
  }
  .container{
    display: flex;
    flex-direction: row;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main"></div>
  <div class="right"></div>
</div>
```

5. 绝对定位
```HTML
<style>
  .left {
    position: absolute;
    left: 0;
    width: 100px;
    height: 200px;
  }
  .right {
    position: absolute;
    right: 0;
    width: 100px;
    height: 200px;
  }
  .main {
    position: absolute;
    left: 100px;
    right: 100px;
    height: 200px;
  }
</style>
    
<div class="container">
  <div class="left"></div>
  <div class="main"></div>
  <div class="right"></div>
</div>
```

## 垂直居中实现方案
1. 使用 verticle-align:middle
```CSS
.centered{ 
  display: inline-block;
  vertical-align: middle;
}
```
2. 使用 Flex 布局
```CSS
.parent{
  display: flex;
}
.centered{ 
  align-self: center;
}
```
3. 使用 table-cell
```CSS
.parent{
  display: table;
}
.centered{ 
  display: table-cell;
  vertical-align: middle;
}
```
4. 使用 transform
```CSS
.parent{
  position: relative;
}
.centered{ 
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
}
```

## 多列等高实现方案
1. border-box 实现
```HTML
<style>
  #wrapper {
    display: inline-block;
    width: 400px;
    border-left: 200px solid #6ee0b6;
    background-color: #c3c3ff;
  }
  .left {
    float: left;
    width: 200px;
    margin-left: -200px;
    border-right: 10px solid #999;
    box-sizing: border-box;
    padding: 20px;
  }
  .right {
    float: left;
    margin-left: -10px;
    border-left: 10px solid #999;
    padding: 20px;
  }
</style>

<div id="wrapper">
  <div class="left">
    <p>left</p> <p>left</p> <p>left</p> <p>left</p>
  </div>
  <div class="right">
    <p>right</p> <p>right</p>
  </div>
</div>
```

2. margin 与 padding 对冲
```HTML
<style>
  #wrapper {
    overflow: hidden;
  }
  .column {
    float: left;
    width: 33%;
    margin-bottom: -99999px;
    padding-bottom: 99999px;
  }
  .left {
    background: #66CCFF;
  }
  .center {
    background: #EE0000;
  }
  .right {
    background: #39C5BB;
  }
</style>

<div id="wrapper">
    <div class="column left">
        <p>left</p>
        <p>left</p>
    </div>
    <div class="column center">
        <p>center</p>
        <p>center</p>
        <p>center</p>
        <p>center</p>
    </div>
    <div class="column right">
        <p>right</p>
        <p>right</p>
    </div>
</div>
```

3. Flex 布局实现
```HTML
<style>
  #wrapper {
  	display: flex;
    flex-direction: row;
    justify-content: center;
  }
  .item {
    flex: auto;
  	align-items: stretch;
  }
  .left {
    background: #66CCFF;
  }
  .center {
    background: #EE0000;
  }
  .right {
    background: #39C5BB;
  }
</style>

<div id="wrapper">
    <div class="item left">
        <p>left</p>
        <p>left</p>
    </div>
    <div class="item center">
        <p>center</p>
        <p>center</p>
        <p>center</p>
        <p>center</p>
    </div>
    <div class="item right">
        <p>right</p>
        <p>right</p>
    </div>
</div>
```

## 多列排版实现方案
```CSS
div {
  -moz-column-count:3; 	/* Firefox */
  -webkit-column-count:3; /* Safari 和 Chrome */
  column-count:3;
}
```

## 块格式化上下文
BFC的概念
>块格式化上下文(Block Formatting Context,BFC)是Web页面的可视化CSS渲染的一部分,是布局过程中生成块级盒子的区域,也是浮动元素与其他元素的交互限定区域.
>>BFC是一个独立的布局环境,可以理解为一个容器,在这个容器中按照一定规则进行物品摆放,并且不会影响其它环境中的物品.
>>如果一个元素符合触发BFC的条件,则BFC中的元素布局不受外部影响.
>>浮动元素会创建BFC,则浮动元素内部子元素主要受该浮动元素影响,所以两个浮动元素之间是互不影响的.

BFC触发条件
>1. float的值不为none
>2. overflow的值不为visible
>3. display的值为table-cell、tabble-caption和inline-block之一
>4. position的值不为static或则releative中的任何一个

规则
>1. 浮动的元素会被父级计算高度(父级触发了BFC)
>2. 非浮动元素不会覆盖浮动元素位置(非浮动元素触发了BFC)
>3. margin不会传递给父级(父级触发了BFC),两个相邻元素上下margin会重叠(给其中一个元素增加一个父级,然后让他的父级触发BFC)

## 清除浮动
|方法|原理|优点|缺点|建议|评分|
|-|-|-|-|-|-|
|父级div定义伪类：after和zoom|IE8以上和非IE浏览器才支持:after,原理和方法2有点类似,zoom(IE转有属性)可解决ie6,ie7浮动问题|浏览器支持好,不容易出现怪问题(目前：大型网站都有使用,如：腾迅,网易,新浪等等)|代码多,不少初学者不理解原理,要两句代码结合使用,才能让主流浏览器都支持|推荐使用,建议定义公共类,以减少CSS代码|★★★★☆|
|在结尾处添加空div标签clear:both|添加一个空div,利用css提高的clear:both清除浮动,让父级div能自动获取到高度|简单,代码少,浏览器支持好,不容易出现怪问题|不少初学者不理解原理；如果页面浮动布局多,就要增加很多空div,让人感觉很不爽|不推荐使用,但此方法是以前主要使用的一种清除浮动方法|★★★☆☆|
|父级div定义height|父级div手动定义height,就解决了父级div无法自动获取到高度的问题|简单,代码少,容易掌握|只适合高度固定的布局,要给出精确的高度,如果高度和父级div不一样时,会产生问题|不推荐使用,只建议高度固定的布局时使用|★★☆☆☆|
|父级div定义overflow:hidden|必须定义width或zoom:1,同时不能定义height,使用overflow:hidden时,浏览器会自动检查浮动区域的高度|简单,代码少,浏览器支持好|不能和position配合使用,因为超出的尺寸的会被隐藏|只推荐没有使用position或对overflow:hidden理解比较深的朋友使用|★★★☆☆|
|父级div定义overflow:auto|必须定义width或zoom:1,同时不能定义height,使用overflow:auto时,浏览器会自动检查浮动区域的高度|简单,代码少,浏览器支持好|内部宽高超过父级div时,会出现滚动条|不推荐使用,如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧|★★☆☆☆|


## DOM 元素隐藏
| |占据空间| 样式变更| 事件触发|
|-|-|-|-|
|display: none| No|Yes | No|
|visibility: hidden|Yes |No|No|
|opacity: 0 |Yes |No| Yes|

## 外边距折叠
毗邻的两个或多个外边距 (margin) 会合并成一个外边距.
>毗邻:是指没有被非空内容、padding、border 或 clear 分隔开,说明其位置关系.
>两个或多个:说明其数量必须是大于一个,又说明,折叠是元素与元素间相互的行为象.

折叠后的大小
1. 两个相同大小的正数：取某个外边距的值.即30px与30px发生折叠,折叠后的值为30px.
2. 两个不同大小的正数：取较大的外边距的值.即30px与20px发生折叠,折叠后的值为30px.
3. 一正一负：取正数与负数的和.即30px与-20px发生折叠,折叠后的值为10px.
4. 相同大小的负数：同相同大小正数.-30px与-30px折叠,折叠后为-30px.
5. 不同大小负数： 取绝对值较大的负数.-30px与-20px折叠,折叠后为-30px.

## Position 定位
|值|	描述|
|-|-|
|absolute	|生成绝对定位的元素,相对于 static 定位以外的第一个父元素进行定位.元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定.|
|fixed|	生成固定定位的元素,相对于浏览器窗口进行定位.元素的位置通过 "left", "top", "right" 以及 "bottom" 属性进行规定.|
|relative	|生成相对定位的元素,相对于其正常位置进行定位.因此,"left:20" 会向元素的 left 位置添加 20 像素.|
|static|	默认值.没有定位,元素出现在正常的流中(忽略 top, bottom, left, right 或者 z-index 声明).|
|sticky	|粘性定位,该定位基于用户滚动的位置.它的行为就像 position:relative; 而当页面滚动超出目标区域时,它的表现就像 position:fixed;,它会固定在目标位置.|
|inherit	|规定应该从父元素继承 position 属性的值.|
