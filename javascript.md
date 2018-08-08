#### 闭包

- 闭包在形式上通常是函数包含一个函数；
- 我所认为的闭包其实就是面向对象编程中的类，通过函数来进行封装，使得外部可以访问函数内部的局部变量；例如一个类中的set和get函数，作用就是用于获取一个类的局部变量；
- 闭包还能保持函数的局部变量不会在函数执行结束的时候就被回收；

#### prototype

- prototype是创建函数时产生的一个指针，指向了一个对象，称为原型对象，可以实现继承的作用；
- 可以通过
```
function Dog(name){
  this.name = name;
  this.type = 'Dog';
}
```
来创建一个对象，然后通过```Dog.prototype.say = function(){alert("laff")}```添加方法等；

```
function Animal(){
  this.superType = 'animal';
}

Animal.prototype.superSay = function(){
  alert(this.superType);
}

Dog.prototype = new Animal(); //关键，令Dog继承自Animal
var doggie = new Dog("jj");
doggie.superSay():
```

#### 箭头函数和普通函数的区别：

- 箭头函数是匿名函数，简化了函数的定义，不能作为构造函数，也没有原型prototype，箭头函数也不绑定参数arguments，使用...来代替；

 ```
 let fun = () => {
    console.log('lalalala');
}
 ```
 
 #### 
