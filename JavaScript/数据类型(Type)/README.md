# JavaScript 数据类型
原始类型(primitive type：)<br>
undefined - 如果变量是 Undefined 类型的
boolean - 如果变量是 Boolean 类型的
number - 如果变量是 Number 类型的
string - 如果变量是 String 类型的
object - 如果变量是一种引用类型或 Null 类型的
symbol - 如果变量是 symbol 类型的

## 数字(Number)
JavaScript只有一个数字类型，以64位浮点数进行表示。
```JavaScript
console.log(1 === 1.0 )  \\true 
console.log(100 === 1e2) \\true
```

```JavaScript
var num = 1;
console.log(typeof(num)) \\number
```

## 字符串（String）
JavaScript每个字符都是16位，但没有字符类型而是用字符串进行表示。
```JavaScript
console.log('c'+'a'+'t' === 'cat') \\true
```
