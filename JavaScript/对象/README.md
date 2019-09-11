# JavaScript 对象
JavaScript中的对象是可变的键控集合(keyed collections)。
```JavaScript
var arr = [1,2,3];
var fun = function(){};
var obj = {};
console.log(typeof(arr));       //Object
console.log(typeof(fun));       //Object
console.log(typeof(obj));       //Object
```

## 引用
对象通过引用来传递，它们永远不会被复制:
```JavaScript
var obj1 = { "label":"one"};
var obj2 = obj1;
obj2.label = "two";
var label = obj1.label;
console.log(label)              //two
```
## 枚举
for in 语句可以用来遍历一个对象中的所有属性名(包含原型链中的属性)。

## new 操作发生了什么
>创建一个新对象；
>将构造函数的作用域赋给新对象(因此 this 就指向了这个新对象);
>执行构造函数中的代码(为这个新对象添加属性);
>返回新对象。
```JavaScript
function New() {
  let obj = {};                                               // 创建一个新对象
  let Constructor = Array.prototype.shift.call(arguments);    // 获取构造函数
  obj.__proto__ = Constructor.prototype;                      // 连接新对象原型，新对象可以访问原型中的属性
  Constructor.apply(obj, arguments);                          // 执行构造函数，即绑定 this，并且为这个新对象添加属性
  return obj;                                                 // 返回该对象
}
```
