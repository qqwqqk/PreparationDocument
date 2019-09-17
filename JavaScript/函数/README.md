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

## 双向绑定相关 Object.defineProperty() 与 Proxy()
>属性描述符 Object.defineProperty(obj, prop, descriptor) 的参数包含三个部分：
>>obj：必需。目标对象
>>prop：必需。需定义或修改的属性的名字
>>descriptor：必需。目标属性所拥有的特性

|属性|默认值|	说明|
|-|-|-|
|enumerable	|false|	描述属性是否可以被for...in或Object.keys枚举 |
|configurable	|false|	描述属性是否可以被删除 |
|writable	|false|	描述属性是否可以修改 |
|value	|undefined|	属性值 |
|get	|undefined	|当访问属性时触发该方法 |
|set|	undefined	|当属性被修改时触发该方法 |

>>数据描述符
```JavaScript
let obj = {}
Object.defineProperty(obj, "name", {
  enumerable: false,      //是可选值，不选的话默认值为false，
  configurable: false,    //是可选值，不选的话默认值为false，
  writable: false,
  value: "Tom"
});
```

>>存取描述符
```JavaScript
let obj = {};
let newVal;
Object.defineProperty(obj, "name", {
  enumerable: false,      //是可选值，不选的话默认值为false，
  configurable: false,    //是可选值，不选的话默认值为false，
  get: function(){
    return newVal;
  },
  set: function(newValue){
    newVal= newValue;
  },
});
```

>>双向绑定示例
```JavaScript
var person = { "name" : undefined};
var obj1 = {};
var obj2 = {};
Object.defineProperty(obj1, "name", {
  get: function(){ return person.name; },
  set: function(value){ person.name = value; },
});
Object.defineProperty(obj2, "name", {
  get: function(){ return person.name; },
  set: function(value){ person.name = value; },
});
console.log(obj1.name);       // undefined
console.log(obj2.name);       // undefined
obj1.name = "Tom";
console.log(obj1.name);       // Tom
console.log(obj2.name);       // Tom
obj1.name = "Jerry";
console.log(obj1.name);       // Jerry
console.log(obj2.name);       // Jerry
```

>Proxy 用于修改某些操作的默认行为，等同于在语言层面做出修改，属于一种“元编程”（meta programming）。
>>Proxy 可以理解成，在目标对象之前架设一层“拦截”，外界对该对象的访问，都必须先通过这层拦截，因此提供了一种机制，可以对外界的访问进行过滤和改写。
| 拦截| 描述|
|-|-|
|get(target, propKey, receiver)|拦截对象属性的读取，比如proxy.foo和proxy['foo']。|
|set(target, propKey, value, receiver)|拦截对象属性的设置，比如proxy.foo = v或proxy['foo'] = v，返回一个布尔值。|
|has(target, propKey)| 拦截propKey in proxy的操作，返回一个布尔值。|
|deleteProperty(target, propKey)| 拦截delete proxy[propKey]的操作，返回一个布尔值。|
|ownKeys(target)| 拦截Object.getOwnPropertyNames(proxy)、Object.getOwnPropertySymbols(proxy)、Object.keys(proxy)、for...in循环，返回一个数组。该方法返回目标对象所有自身的属性的属性名，而Object.keys()的返回结果仅包括目标对象自身的可遍历属性。|
|getOwnPropertyDescriptor(target, propKey)| 拦截Object.getOwnPropertyDescriptor(proxy, propKey)，返回属性的描述对象。|
|defineProperty(target, propKey, propDesc)| 拦截Object.defineProperty(proxy, propKey, propDesc）、Object.defineProperties(proxy, propDescs)，返回一个布尔值。|
|preventExtensions(target)| 拦截Object.preventExtensions(proxy)，返回一个布尔值。|
|getPrototypeOf(target)| 拦截Object.getPrototypeOf(proxy)，返回一个对象。|
|isExtensible(target)| 拦截Object.isExtensible(proxy)，返回一个布尔值。|
|setPrototypeOf(target, proto)| 拦截Object.setPrototypeOf(proxy, proto)，返回一个布尔值。如果目标对象是函数，那么还有两种额外操作可以拦截。|
a|pply(target, object, args)| 拦截 Proxy 实例作为函数调用的操作，比如proxy(...args)、proxy.call(object, ...args)、proxy.apply(...)。|
|construct(target, args)| 拦截 Proxy 实例作为构造函数调用的操作，比如new proxy(...args)。|

>>双向绑定示例
```JavaScript
let person = { "name" : undefined};
let personHandler = {
  get: function(target,propkey){
    if(propkey != "name"){ return false; }
    else { return target[propkey]; }
  },
  set: function(target,propkey,value){
    if(propkey != "name"){ return false; }
    else { target[propkey] = value; }
  }
}
let obj1 = new Proxy(person, personHandler);
let obj2 = new Proxy(person, personHandler);
console.log(obj1.name);       // undefined
console.log(obj2.name);       // undefined
obj1.name = "Tom";
console.log(obj1.name);       // Tom
console.log(obj2.name);       // Tom
obj1.name = "Jerry";
console.log(obj1.name);       // Jerry
console.log(obj2.name);       // Jerry
```

## requestAnimationFrame()
> 请求动画帧 requestAnimationFrame() 
>> 由系统来决定回调函数的执行时机。保证回调函数在屏幕每一次的刷新间隔中只被执行一次。
>>特点：
>>requestAnimationFrame会把每一帧中的所有DOM操作集中起来，在一次重绘或回流中就完成，并且重绘或回流的时间间隔紧紧跟随浏览器的刷新频率。
>>在隐藏或不可见的元素中，requestAnimationFrame将不会进行重绘或回流，这当然就意味着更少的CPU、GPU和内存使用量
>>requestAnimationFrame是由浏览器专门为动画提供的API，在运行时浏览器会自动优化方法的调用，并且如果页面不是激活状态下的话，动画会自动暂停，有效节省了CPU开销。
```JavaScript
const begin = 0;
const end = 20;
let curr = begin;
function animation(){
  requestAnimationFrame(function(){
      curr++;
      // TODO
      console.log(curr);
      if(curr < end) animation();
  })  
}
animation();
```