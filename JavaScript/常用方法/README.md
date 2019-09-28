# JavaScript 常用函数

* 1.数组扁平化
```JavaScript
function flatten(arr){
  var res = [];
  for(var i=0;i<arr.length;i++){
    if(Array.isArray(arr[i])){
        res = res.concat(flatten(arr[i]));
    }else{
        res.push(arr[i]);
    }
  }
  return res;
}
```

* 2.对象判空
```JavaScript
function isEmpty(obj){
  return Object.keys(obj).length == 0;
}
```

* 3.对象深度拷贝
```JavaScript
function deepClone(obj) {
  var _obj = JSON.stringify(obj),
  var objClone = JSON.parse(_obj);
  return objClone;
}
```

* 4.数组去重
```JavaScript
function unique (arr) {
  return Array.from(new Set(arr))
}
```