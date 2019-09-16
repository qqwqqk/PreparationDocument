# Class 类 

## 类的创建

>类的创建（es5）：new一个function，在这个function的prototype里面增加属性和方法。
```JavaScript
function Animal (name) {                    // 定义一个动物类
  this.name = name || 'Animal';             // 属性
  this.sleep = function(){                  // 实例方法
    console.log(this.name + ' sleeping...');
  }
}
Animal.prototype.eat = function(food) {     // 原型方法
  console.log(this.name + ' eating ' + food);
};
```

## 类的继承

>原型链继承
>>new一个空对象,这个空对象指向Animal并且Cat.prototype指向了这个空对象
```JavaScript
function Cat(){ }
Cat.prototype = new Animal();
Cat.prototype.name = 'cat';

var cat = new Cat();
console.log(cat.name);
cat.eat('fish');                        //cat eating fish
cat.sleep();                            //cat sleeping...
console.log(cat instanceof Animal);     //true
console.log(cat instanceof Cat);        //true
```
>>特点：基于原型链，既是父类的实例，也是子类的实例
>>缺点：无法实现多继承

>构造继承
>>使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）
```JavaScript
function Cat(name){
  Animal.call(this);
  this.name = name || 'Tom';
}

var cat = new Cat();
console.log(cat.name);                // Tom
cat.sleep();                          // Tom sleeping...
console.log(cat instanceof Animal);   // false
console.log(cat instanceof Cat);      // true
```
>>特点：可以实现多继承
>>缺点：只能继承父类实例的属性和方法，不能继承原型上的属性和方法。

>组合继承：
>>相当于构造继承和原型链继承的组合体。通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用
```JavaScript
function Cat(name){
  Animal.call(this);
  this.name = name || 'Jerry';
}
Cat.prototype = new Animal();
Cat.prototype.constructor = Cat;

var cat = new Cat();
console.log(cat.name);                // Jerry
cat.sleep();                          // Jerry sleeping...
console.log(cat instanceof Animal);   // true
console.log(cat instanceof Cat);      // true
```
>>特点：可以继承实例属性/方法，也可以继承原型属性/方法
>>缺点：调用了两次父类构造函数，生成了两份实例

