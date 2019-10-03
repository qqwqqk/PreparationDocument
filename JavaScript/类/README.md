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

1、原型链继承，将父类的实例作为子类的原型，他的特点是实例是子类的实例也是父类的实例，父类新增的原型方法/属性，子类都能够访问，并且原型链继承简单易于实现，缺点是来自原型对象的所有属性被所有实例共享，无法实现多继承，无法向父类构造函数传参。
2、构造继承，使用父类的构造函数来增强子类实例，即复制父类的实例属性给子类，

构造继承可以向父类传递参数，可以实现多继承，通过call多个父类对象。但是构造继承只能继承父类的实例属性和方法，不能继承原型属性和方法，无法实现函数服用，每个子类都有父类实例函数的副本，影响性能

3、实例继承，为父类实例添加新特性，作为子类实例返回，实例继承的特点是不限制调用方法，不管是new 子类（）还是子类（）返回的对象具有相同的效果，缺点是实例是父类的实例，不是子类的实例，不支持多继承

4、拷贝继承：特点：支持多继承，缺点：效率较低，内存占用高（因为要拷贝父类的属性）无法获取父类不可枚举的方法（不可枚举方法，不能使用for in 访问到）

5、组合继承：通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

6、寄生组合继承：通过寄生方式，砍掉父类的实例属性，这样，在调用两次父类的构造的时候，就不会初始化两次实例方法/属性，避免的组合继承的缺点

原型链继承
核心： 将父类的实例作为子类的原型

特点：

非常纯粹的继承关系，实例是子类的实例，也是父类的实例

父类新增原型方法/原型属性，子类都能访问到

简单，易于实现

缺点：

要想为子类新增属性和方法，不能放到构造器中

无法实现多继承

来自原型对象的所有属性被所有实例共享

创建子类实例时，无法向父类构造函数传参


构造继承

核心：使用父类的构造函数来增强子类实例，等于是复制父类的实例属性给子类（没用到原型）

特点：

解决了子类实例共享父类引用属性的问题

创建子类实例时，可以向父类传递参数

可以实现多继承（call多个父类对象）

缺点：

实例并不是父类的实例，只是子类的实例

只能继承父类的实例属性和方法，不能继承原型属性/方法

无法实现函数复用，每个子类都有父类实例函数的副本，影响性能


实例继承

核心：为父类实例添加新特性，作为子类实例返回

特点：

不限制调用方式，不管是new 子类()还是子类(),返回的对象具有相同的效果

缺点：

实例是父类的实例，不是子类的实例

不支持多继承


拷贝继承

特点：

支持多继承

缺点：

效率较低，内存占用高（因为要拷贝父类的属性）


组合继承

核心：通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用

特点：

可以继承实例属性/方法，也可以继承原型属性/方法

既是子类的实例，也是父类的实例

不存在引用属性共享问题

可传参

函数可复用


寄生组合继承

核心：通过调用父类构造，继承父类的属性并保留传参的优点，然后通过将父类实例作为子类原型，实现函数复用