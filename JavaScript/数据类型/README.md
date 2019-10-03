# JavaScript 数据类型
原始类型(primitive type：)<br>
undefined - 如果变量是 Undefined 类型的
boolean - 如果变量是 Boolean 类型的
number - 如果变量是 Number 类型的
string - 如果变量是 String 类型的
object - 如果变量是一种引用类型或 Null 类型的
symbol - 如果变量是 symbol 类型的

```JavaScript
null == undefined    //true
null === undefined   //false
"" == null           //false
1 + null             //1
1 + undefined        //NaN
```

基本数据类型：按值访问，可操作保存在变量中的实际的值。基本类型值指的是简单的数据段。基本数据类型有这六种:undefined、null、string、number、boolean、symbol。

引用类型：当复制保存着对象的某个变量时，操作的是对象的引用，但在为对象添加属性时，操作的是实际的对象。引用类型值指那些可能为多个值构成的对象。

引用类型有这几种：Object、Array、RegExp、Date、Function、特殊的基本包装类型(String、Number、Boolean)以及单体内置对象(Global、Math)。

## 数字(Number)
JavaScript只有一个数字类型，以64位浮点数进行表示。
```JavaScript
console.log(1 === 1.0 )  //true 
console.log(100 === 1e2) //true
```

```JavaScript
var num = 1;
console.log(typeof(num)) //number
```

## 字符串（String）
JavaScript每个字符都是16位，但没有字符类型而是用字符串进行表示。
```JavaScript
console.log('c'+'a'+'t' === 'cat') //true
```

## 基础类型与引用类型的区别
  1.基础类型存放于栈中，而引用类型存放于堆中；
  2.js中不允许直接访问保存在堆内存中的对象，所以在访问一个对象时，首先得到这个对象在堆内存中的地址，然后在按照这个地址去获取对象中的值，这就是按引用访问，基础类型则可以直接访问到
  3.参数传递的不同（实参复制给形参的过程），首先我们知道所有函数都是按值来传递的，传参不同也就是内存分配不同的原因，当我们把变量赋值给参数的时候，参数的改变和变量没有关系，当我们把引用类型传递给参数的时候，此时我们传递的是引用类型的地址，所有当参数在函数内部改变的时候，会出现修改了函数外面值的情况

## == 、=== 和 Object.is()

```JavaScript
var a1 = 3;
var b1 = "3";
console.log(a1 == b1);            // true
console.log(a1 === b1);           // true
console.log(Object.is(a1,b1));    // true

var a2 = -0;
var b2 = +0;
console.log(a2 == b2);            // true
console.log(a2 === b2);           // true
console.log(Object.is(a2,b2));    // false

var a3 = NaN;
var b3 = NaN;
console.log(a3 == b3);            // false
console.log(a3 === b3);           // false
console.log(Object.is(a3,b3));    // true

var a4 = undefined;
var b4 = undefined;
console.log(a4 == b4);            // true
console.log(a4 === b4);           // true
console.log(Object.is(a4,b4));    // true
```