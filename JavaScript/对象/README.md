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

## 数组
|方法	描述
|concat()	|连接两个或更多的数组，并返回结果。|
|join()	|把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔。|
|pop()	|删除并返回数组的最后一个元素|
|push()|	向数组的末尾添加一个或更多元素，并返回新的长度。|
|reverse()|	颠倒数组中元素的顺序。|
|shift()|	删除并返回数组的第一个元素|
|slice()|	从某个已有的数组返回选定的元素|
|sort()	|对数组的元素进行排序|
|splice()|	删除元素，并向数组添加新元素。|
|toSource()	|返回该对象的源代码。|
|toString()	|把数组转换为字符串，并返回结果。|
|toLocaleString()	|把数组转换为本地数组，并返回结果。|
|unshift()|	向数组的开头添加一个或更多元素，并返回新的长度。|
|valueOf()	|返回数组对象的原始值|

## 正则
>直接量语法
>>/pattern/attributes

>创建 RegExp 对象的语法：
>>new RegExp(pattern, attributes);

```JavaScript
var re1 = /ABC\-001/;
var re2 = new RegExp('ABC\\-001');
```


## 前端模块化
>为什么要进行前端模块化
>>避免命名冲突(减少命名空间污染)
>>降低耦合度，减少重复代码
>>更高复用性
>>高可维护性

>CommonJS
>>CommonJS定义一个文件就是一个模块，有自己的作用域。在一个文件里面定义的变量、函数、类，都是私有的，对其他文件不可见。
>>特点:所有代码都运行在模块作用域，不会污染全局作用域。模块可以多次加载，但是只会在第一次加载时运行一次，然后运行结果就被缓存了，以后再加载，就直接* * 读取缓存结果。要想让模块再次运行，必须清除缓存。模块加载的顺序，按照其在代码中出现的顺序。
>>基本语法:暴露模块：module.exports = value或exports.xxx = value;引入模块：require(xxx)，如果是第三方模块，xxx为模块名；如果是自定义模块，xxx为模块文件路径

>ES6 module
>>ES6模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。
>>export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。

## 前端打包工具
> Npm Script
>>Npm Script（https://docs.npmjs.com/misc/scripts） 是一个任务执行者。Npm是在安装Node. js时附带的包管理器，Npm Script则是Npm内置的一个功能，允许在package.json文件里面使用scripts字段定义任务.

> Grunt
>>Grunt（https://gruntjs.com） 和Npm Script类似，也是一个任务执行者。Grunt有大量现成的插件封装了常见的任务，也能管理任务之间的依赖关系，自动化地执行依赖的任务，每个任务的具体执行代码和依赖关系写在配置文件Gruntfile.js里

> Gulp
>>Gulp（http://gulpjs.com） 是一个基于流的自动化构建工具。除了可以管理和执行任务，还支持监听文件、读写文件。

> Fis3
>>Fis3（https://fex.baidu.com/fis3/） 是一个来自百度的优秀国产构建工具。相对于Grunt、Gulp这些只提供了基本功能的工具，Fis3集成了Web开发中的常用构建功能

> Webpack
>>Webpack（https://webpack.js.org） 是一个打包模块化JavaScript的工具，在Webpack里一切文件皆模块，通过Loader转换文件，通过Plugin注入钩子，最后输出由多个模块组合成的文件。Webpack专注于构建模块化项目。

> Rollup
>>Rollup（https://rollupjs.org） 是一个和Webpack很类似但专注于ES6的模块打包工具。它的亮点在于，能针对ES6源码进行Tree Shaking，以去除那些已被定义但没被使用的代码并进行Scope Hoisting，以减小输出文件的大小和提升运行性能。
