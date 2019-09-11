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