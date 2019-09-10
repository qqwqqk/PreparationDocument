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

//闭包输出： 0 1 2 3 4 
for(var i=0; i<5; i++){
  (function(i){
    setTimeout(()=>{ console.log(i) }, 0);
  })(i);
};
```