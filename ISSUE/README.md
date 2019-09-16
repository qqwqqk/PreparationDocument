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

