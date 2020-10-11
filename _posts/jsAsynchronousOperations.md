---
title: js之异步操作入门
excerpt: 关于js异步的简单理解
categories:
- 技术文章
tags:
- js
---

## ajax
```javascript
ajax('http://aaa.com/a/1.txt',function(){});
```
异步操作：同时进行多个操作，用户体验好，代码混乱
同步操作：一次只能执行一个操作，用户体验不好，但清晰

```javascript
//异步——麻烦
ajax('http://aaa.com/api/uesr',function(data1){
    ajax('http://aaa.com/api/item',function(data2){
        ajax('http://aaa.com/api/test',function(data3){


        },function(){
            alert('error');
        });
    },function(){
        alert('error');
    });
},function(){
    alert('error');
});
```
```javascript
//同步——容易
let data1=ajax('http://aaa.com/api/uesr');
let data2=ajax('http://aaa.com/api/item');
let data3=ajax('http://aaa.com/api/test');
```

## Promise
融合异步同步
封装的例子：
```javascript
//需要jQuery
let p=new Promise(function(resolve,reject){
    //异步
    //resolve   解决
    //reject    拒绝
    $.ajax({
        url:'data/1.txt',
        dataType:'json',
        success(arr){
            resolve(arr);
        },
        error(res){
            reject(res);
        }
    })
})
p.then(function(arr){
    alert('成功');
    console.log(arr);
},function(res){
    alert('失败');
    console.log(res);
});
```

