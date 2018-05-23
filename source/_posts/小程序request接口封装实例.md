---
layout: 兰志远
title: 小程序request接口封装实例
date: 2018-05-23 14:10:22
tags: 小程序
type: "tags"
---
### 使用Promise对小程序wx.request接口进行封装
#### 新建一个request.js文件，代码如下:
``` javascript
 //url 接口地址
 //method 请求方式 
 //data 要传给服务器端的数据  没有的话传个{}就可以
 //还需要别的在添加就ok
 function request(url,method,data){
    return new Promise((resolve,reject)=>{
        wx.request({
            url,
            method,
            data:{data},
            header: {
                'content-type': 'application/json'
            },
            success:function(res){
                resolve(res)
            },
            fail:function(error){
                reject(error)
            }
        })
    })
}
module.exports = {
    request
}
```
#### 在文件中使用
``` javascript
//引入封装好的request文件
var request = require('文件路径')
//这里已post为例
request.request('url','POST',data)
    .then((res)=>{
        // 请求成功函数
    })
    .error((error)=>{
        //请求失败函数
    })
```