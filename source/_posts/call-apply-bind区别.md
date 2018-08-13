---
layout: 兰志远
title: call apply bind区别
date: 2018-08-13 10:58:01
tags: javascript
type: "tags"
---
### 例子
```javascript
var name = '小明',age=20
var obj = {
        name : '小红',
        objage:this.age,
        myFun:function(){
            console.log(this.name+'年龄'+this.age)
        }
    }
    var obj2 = {
        age : 30,
        name : '小兰'
    }
obj.myFun.call(obj2) //将obj的this改变为obj2 所以输出小兰年龄30
obj.myFun.apply(obj2) //同样是将obj的this改变为obj2 所以输出小兰年龄30
obj.myFun.bind(obj2)()//这个稍微有点不用，后边多了一个括号，因为bind返回的是一个函数，需要再次调用，同样是将this改为obj2
```
### 在看传参方式
```javascript
var name = '小明',age=20
    var obj = {
        name : '小红',
        objage:this.age,
        myFun:function(address,play){
            console.log(this.name+'年龄'+this.age+'来自'+address+'去过'+play)
        }
    }
    var obj2 = {
        age : 30,
        name : '小兰'
    }
//传参
obj.myFun.call(obj2,'上海','成都')   //call传参方式就是以普通方式传入
obj.myFun.apply(obj2,['北京','美国']) //apply传参方式是以数组方式传入
obj.myFun.bind(obj2,'深圳','韩国')() //bind传参方式就是以普通方式传入    
```
### 区别
  * 1.call、apply、bind第一个参数都是改变this指向
  * 2.call、apply调用一次就可以，bind是需要再次调用
  * 3.call、bind传参方式都是普通传入用逗号隔开就好，apply是传入数组
