---
layout: 兰志远
title: js继承几种方式
date: 2018-08-13 17:39:26
tags: javascript
type: "tags"
---
### 1.原型链继承
```javascript
function Test(name,age){
        this.name = name || '小红'
        this.age = age || 15
        this.fun=function(){
            console.log(this.name+'今年'+this.age)
        }
    }
    function Test2(){

    }
    //Test2的原型等于Test的实例   原型链继承
    Test2.prototype = new Test('小明',20)
    var a = new Test2()
    a.fun()
    console.log(a instanceof Test)  //true
    console.log(a instanceof Test2) //true 
```
##### 缺点:
    * 1.无法实现多继承
    * 2.继承属性都是共享的
    * 3.创建子类实例时，无法向父类构造函数传参

### 2.构造函数继承
```javascript
function Fun(name,age){
        this.name = name
        this.age = age
        this.fun=function(){
            console.log(this.name+'今年'+this.age)
        }
    }
    Fun.prototype.h = function(){
        console.log('hello')
    }
    function Fun2(name,age){
        Fun.call(this)    //改变this指向 继承了Fun的属性和方法
        this.name = name
        this.age = age
    }
    var a = new Fun2('小明',20)
    var b = new Fun2('小兰',15)
    a.fun()
    console.log(a instanceof Fun)  //false
    console.log(a instanceof Fun2) //true
```
##### 缺点:
    * 1.实例并不是父类的实例，只是子类的实例
    * 2.只能继承父类的实例属性和方法，不能继承原型属性/方法
    * 3.无法实现函数复用，每个子类都有父类实例函数的副本，影响性能
    
### 3.拷贝继承
```javascript
function Fun(name,age){
        this.name = name
        this.age = age
        this.fun = function(){
            console.log(this.name+'今年'+this.age);
        }
    }
    function Fun2(name,age){
        var a = new Fun()
        //遍历实例上的属性和方法拷贝到构造函数原型上
        for (p in a){
            Fun2.prototype[p] = a[p]
        }
        Fun2.prototype.name = name
        Fun2.prototype.age = age
    }
    var b = new Fun2('小花',20)
    b.fun()
    console.log(b instanceof Fun) //false
    console.log(b instanceof Fun2) //true
```    
##### 缺点:
    * 1.效率较低，内存占用高（因为要拷贝父类的属性）
    * 2.无法获取父类不可枚举的方法（不可枚举方法，不能使用for in 访问到）
    
### 4.组合继承
```javascript
 function Fun2(name,age){
        this.name = name
        this.age = age
        this.fun = function () {
            console.log(this.name+'今年'+this.age)
        }
    }
    Fun.prototype.h = function(){
        console.log('hello world');
    }
    function Fun(name,age){
        Fun2.call(this)
        this.name = name
        this.age = age
    }
    //Fun构造函数复制给Fun2的原型上
    Fun2.prototype = new Fun()
    var a = new Fun2('小兰',30)
    a.fun()
    a.h()
    console.log(a instanceof Fun)   //true
    console.log(a instanceof Fun2)  //true
```    
##### 缺点:
    * 1.调用了两次父类构造函数，生成了两份实例
    
### 5.寄生继承
```javascript
function Fun2(name,age){
        this.name = name
        this.age = age
        this.fun = function () {
            console.log(this.name+'今年'+this.age)
        }
    }
    Fun.prototype.h = function(){
        console.log('hello world');
    }
    function Fun(name,age){
        Fun2.call(this)
        this.name = name
        this.age = age
    }
    (function(){
        //再次创建没有实例的构造函数
        var Fun3 = function(){}
        //将Fun原型复制给Fun3  Fun实例上边会有Fun原型上的属性和方法
        Fun3.prototype = Fun.prototype
        //Fun3的实例赋值给Fun2的原型  所以Fun2的实例会有Fun3原型上的属性和方法
        Fun2.prototype = new Fun3()
    })()
    var a = new Fun2('小兰',30)
    a.fun()
    a.h()
    console.log(a instanceof Fun)  //true
    console.log(a instanceof Fun2) //true
```    