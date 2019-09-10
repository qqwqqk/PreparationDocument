# 面试问题

## 宽度自适应，高度等比缩放的实现

* 使用vw实现
```CSS
.box{
  width : 70vw;
  height : 50vw;  
}
```
* 使用padding实现
```CSS
.parent{
  width: 120px;
}
.parent .child{
  width: 100%;
  height: 0;
  padding-top: 50%; // 实际为60px
}
```

## 什么时BFC，在什么情况下会被触发
* BFC的概念
  1.规范解释
    块格式化上下文（Block Formatting Context，BFC）是Web页面的可视化CSS渲染的一部分，是布局过程中生成块级盒子的区域，也是浮动元素与其他元素的交互限定区域。
  2.通俗理解
    BFC是一个独立的布局环境,可以理解为一个容器,在这个容器中按照一定规则进行物品摆放,并且不会影响其它环境中的物品。
    如果一个元素符合触发BFC的条件，则BFC中的元素布局不受外部影响。
    浮动元素会创建BFC，则浮动元素内部子元素主要受该浮动元素影响，所以两个浮动元素之间是互不影响的。
* BFC触发条件：
  1.float的值不为none
  2.overflow的值不为visible
  3.display的值为table-cell、tabble-caption和inline-block之一
  4.position的值不为static或则releative中的任何一个
* 规则：
  1.浮动的元素会被父级计算高度（父级触发了BFC）
  2.非浮动元素不会覆盖浮动元素位置（非浮动元素触发了BFC）
  3.margin不会传递给父级（父级触发了BFC），两个相邻元素上下margin会重叠（给其中一个元素增加一个父级，然后让他的父级触发BFC）

## 清除浮动
* 1.父级div定义伪类：after和zoom
  原理：IE8以上和非IE浏览器才支持:after，原理和方法2有点类似，zoom(IE转有属性)可解决ie6,ie7浮动问题
  优点：浏览器支持好，不容易出现怪问题（目前：大型网站都有使用，如：腾迅，网易，新浪等等）
  缺点：代码多，不少初学者不理解原理，要两句代码结合使用，才能让主流浏览器都支持
  建议：推荐使用，建议定义公共类，以减少CSS代码
  评分：★★★★☆
* 2.在结尾处添加空div标签clear:both
  原理：添加一个空div，利用css提高的clear:both清除浮动，让父级div能自动获取到高度
  优点：简单，代码少，浏览器支持好，不容易出现怪问题
  缺点：不少初学者不理解原理；如果页面浮动布局多，就要增加很多空div，让人感觉很不爽
  建议：不推荐使用，但此方法是以前主要使用的一种清除浮动方法
  评分：★★★☆☆
* 3.父级div定义height
  原理：父级div手动定义height，就解决了父级div无法自动获取到高度的问题
  优点：简单，代码少，容易掌握
  缺点：只适合高度固定的布局，要给出精确的高度，如果高度和父级div不一样时，会产生问题
  建议：不推荐使用，只建议高度固定的布局时使用
  评分：★★☆☆☆
* 4.父级div定义overflow:hidden
  原理：必须定义width或zoom:1，同时不能定义height，使用overflow:hidden时，浏览器会自动检查浮动区域的高度
  优点：简单，代码少，浏览器支持好
  缺点：不能和position配合使用，因为超出的尺寸的会被隐藏
  建议：只推荐没有使用position或对overflow:hidden理解比较深的朋友使用
  评分：★★★☆☆
* 5.父级div定义overflow:auto
  原理：必须定义width或zoom:1，同时不能定义height，使用overflow:auto时，浏览器会自动检查浮动区域的高度
  优点：简单，代码少，浏览器支持好
  缺点：内部宽高超过父级div时，会出现滚动条。
  建议：不推荐使用，如果你需要出现滚动条或者确保你的代码不会出现滚动条就使用吧。
  评分：★★☆☆☆

## toString与valueOf
* toString
每个对象都有一个 toString() 方法，当对象被表示为文本值时或者当以期望字符串的方式引用对象时，该方法被自动调用。对对象x，toString() 返回 “[object type]”,其中type是对象类型。如果x不是对象，toString() 返回x应有的文本值(不是单纯的加”“)
```JavaScript
var x = {};
console.log(x.toString());           //  [object Object]

//特别的用法
toString.call(new Date);             // [object Date]
toString.call(new String);           // [object String]
toString.call(Math);                 // [object Math]

//Since JavaScript 1.8.5
toString.call(undefined);            // [object Undefined]
toString.call(null);                 // [object Null]

//其他类型的toString():
var x = [1,2,3];
x.toString();                        //返回'1,2,3'
var x = function(){console.log('lalala')}
x.toString();                        // 返回'function(){console.log('lalala')}'
var x = 12345;
x.toString();                        // 返回'12345'
```
* valueOf
JavaScript 调用 valueOf() 方法用来把对象转换成原始类型的值（数值、字符串和布尔值）默认情况下, valueOf() 会被每个对象Object继承。每一个内置对象都会覆盖这个方法为了返回一个合理的值，如果对象没有原始值，valueOf() 就会返回对象自身。
```JavaScript
//一下例子均没有原始值,返回这个对象本身
var x = {};
x.valueOf(); //  返回 Object {}

var x = [1,2,3];
x.valueOf(); //返回[1, 2, 3]

var x = function(){console.log('lalala')}
x.valueOf();// 返回 function (){console.log('lalala')}

var x = 12345;
x.valueOf();// 返回 12345
```

## 事件冒泡与终止
* 事件冒泡
事件冒泡发生的条件：当为多个嵌套的元素设置了相同的事件处理程序，它们将触发事件冒泡机制。在事件冒泡中，最内部的元素将首先触发其事件，然后是栈内的下一个元素触发该事件，以此类推，直到到达最外面的元素。如果把事件处理程序指定给所有的元素，那么这些事件将依次触发。
* 冒泡终止
js冒泡和捕获是事件的两种行为，使用event.stopPropagation()起到阻止捕获和冒泡阶段中当前事件的进一步传播。使用event.preventDefault()可以取消默认事件。