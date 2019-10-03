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

* 5.全排列
```JavaScript
function permutate(str) {
  var result = [];
  if(str.length > 1) {
    var left = str[0];
    var rest = str.slice(1, str.length);
    var preResult = permutate(rest);
    for(var i=0; i<preResult.length; i++) {
      for(var j=0; j<preResult[i].length; j++) {
      var tmp = preResult[i],slice(0, j) + left + preResult[i].slice(j, preResult[i].length);
      result.push(tmp);
      }
    }
  } else if (str.length == 1) {
    return [str];
  }
  return result;
}
```