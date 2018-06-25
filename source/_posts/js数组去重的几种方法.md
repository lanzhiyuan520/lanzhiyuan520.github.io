---
layout: 兰志远
title: js数组去重的几种方法
date: 2018-06-25 10:27:35
tags: javascript
type: "tags"
---
### 数组去重的几种方式
#### 方式1：利用indexOf 遍历数组去重的数组，根据indexOf去判断新数组有没有这个值,有的话就返回索引下标，没有的话就返回-1，如果没有就push到这个新数组中，最后将这个新数组返回实现去重
```javascript
    var arr = [1,2,3,1,2,3,4,5,6,6,5,4]
    function delre(arr){
        var ret = []
        for (var i = 0; i < arr.length; i++) {
            if (ret.indexOf(arr[i]) === -1){
                ret.push(arr[i])
            }
        }
        return ret
    }
    console.log(delre(arr))
    输出:[1,2,3,4,5,6]
```
#### 方式2：遍历数组，利用object对象保存数组值，判断数组值是否已经保存在object中，未保存则push到新数组并用object[arrayItem]=1的方式记录保存
```javascript
    function delre(arr){
        var obj = {}
        var ret = []
        for (var i = 0; i < arr.length; i++) {
            if (!obj[arr[i]]){
                obj[arr[i]] = 1
                ret.push(arr[i])
            }
        }
        return ret
    }
    console.log(delre(arr))
    输出:[1,2,3,4,5,6]
```
#### 方式3：数组下标判断法, 遍历数组，利用indexOf判断元素的值是否与当前索引相等，如相等则加入
```javascript
    function delre(arr){
        var ret = []
        arr.forEach((e,i)=>{
            if (arr.indexOf(e)===i){
                ret.push(e)
            }
        })
        return ret
    }
    console.log(delre(arr))
    输出:[1,2,3,4,5,6]
```
#### 方式4：Es6的set方法
```javascript
    function delre(arr){
        var ret = new Set(arr)
        return Array.from(ret)
    }
    console.log(delre(arr))
    输出:[1,2,3,4,5,6]
```
#### 方式5：嵌套循环依次比较
```javascript
    function delre(arr){
        for (let i = 0; i < arr.length; i++) {
            for (let j = i+1; j < arr.length; j++) {
                if (arr[i] === arr[j]){
                    arr.splice(j,1)
                    j--
                }
            }
        }
        return arr
    }
    console.log(delre(arr))
    输出:[1,2,3,4,5,6]
```
