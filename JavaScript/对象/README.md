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