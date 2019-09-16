# JavaScript 函数
JavaScript 函数也是对象。

## 闭包
通过函数字面量创建的函数对象包含一个连到外部上下文的连接。这被称为闭包。

```JavaScript
//原输出：5 5 5 5 5
for(var i=0; i<5; i++){
  setTimeout(()=>{console.log(i)},0);
};

//ES6输出： 0 1 2 3 4 
for(let i=0; i<5; i++){
  setTimeout(()=>{console.log(i)},0);
};

//立即执行函数输出： 0 1 2 3 4 
for(var i=0; i<5; i++){
  ((i)=>{ setTimeout(()=>{ console.log(i) }, 0); })(i);
};

////闭包输出： 0 1 2 3 4 
for(var i=0; i<5; i++){
  (()=>{ var _i=i; setTimeout(()=>{ console.log(_i) }, 0); })();
};
```

## mouseover 和 mouseenter
>mouseover：
>>当鼠标移入元素或其子元素都会触发事件，所以有一个重复触发，冒泡的过程。对应的移除事件是mouseout
>mouseenter：
>>当鼠标移除元素本身（不包含元素的子元素）会触发事件，也就是不会冒泡，对应的移除事件是mouseleave

## 防抖与节流
>防抖（debounce）
>>所谓防抖，就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。
```JavaScript
//延时版
function debounce(func, wait) {
  let timeout;
  return function () {
    let context = this;
    let args = arguments;
    if (timeout) clearTimeout(timeout);
    timeout = setTimeout(() => {
        func.apply(context, args)
    }, wait);
  }
}
//即时版
function debounce(func,wait) {
  let timeout;
  return function () {
    let context = this;
    let args = arguments;
    if (timeout) clearTimeout(timeout);
    let callNow = !timeout;
    timeout = setTimeout(() => {
        timeout = null;
    }, wait)
    if (callNow) func.apply(context, args)
  }
}
```
>节流（throttle）
>>所谓节流，就是指连续触发事件但是在 n 秒中只执行一次函数。节流会稀释函数的执行频率。
```JavaScript
//时间戳版
function throttle(func, wait) {
  let previous = 0;
  return function() {
    let now = Date.now();
    let context = this;
    let args = arguments;
    if (now - previous > wait) {
      func.apply(context, args);
      previous = now;
    }
  }
}
//定时器版
function throttle(func, wait) {
  let timeout;
  return function() {
    let context = this;
    let args = arguments;
    if (!timeout) {
      timeout = setTimeout(() => {
        timeout = null;
        func.apply(context, args)
      }, wait)
    }
  }
}
```

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

## call，apply和bind
>通过apply和call改变函数的this指向，他们两个函数的第一个参数都是一样的表示要改变指向的那个对象，第二个参数，apply是数组，而call则是arg1,arg2...这种形式。通过bind改变this作用域会返回一个新的函数，这个函数不会马上执行。

```JavaScript
var objA = {
    name: 'Tom',
  }
  var objB = {
    log: function (age) {
      return `${this.name} age: ${age}`
    }
  }
  console.log(objB.log.bind(objA, 20)())      // Tom age: 20
  console.log(objB.log.call(objA, 20))        // Tom age: 20
  console.log(objB.log.apply(objA, [ 20 ]))   // Tom age: 20
```

## eval()
>将对应的字符串解析成js并执行
>应该尽量避免使用，因为非常消耗性能（2次，一次解析成js，一次执行）
```JavaScript
eval("2+3")	        // 返回 5
var myeval = eval;	// 可能会抛出 EvalError 异常
myeval("2+3");	    // 可能会抛出 EvalError 异常
```