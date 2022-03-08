# 原生AJAX：

- AJAX简介：

AJAX全程为Asynchronous JavaScript And XML，就是异步的JS和XML

通过AJAX可以在浏览器中向服务器发送异步请求，最大的优势：无刷新获取数据

AJAX不是新的编程语言，而是一种将现有的标准组个在一起使用的新方式

- XML：

可扩展标记语言

XML被设计用来传输和存储数据

XML和HTML类似，不同的时HTML中都是预定义标签，而XML中没有预定义标签

```xml
name = "孙悟空";
age = 18;
gender = "男";

// 用XML表示则为：
 <student>
  <name>孙悟空</name>
  <age>18</age>
  <gender>男</gender>
 </student>
```

# AJAX优缺点：

- 优点：
  - 可以无需刷新页面与服务器端进行通信
  - 允许你根据用户事件来更新部分页面内容
- 缺点：
  - 没有浏览器历史，不能回退
  - 存在跨域问题（同源）
  - SEO不友好

# HTTP协议请求报文与响应文本结构：

- HTTP：hypertext transport protocol，超文本传输协议。协议详细规定了浏览器和万维网服务之间互相通信的规则
- 请求报文：
  - 重点是格式与参数
  - 行：GET  /s?ie=utf-8  HTTP/1.1
  - 头：
    - Host：atguigu.com
    - Cookie：name = guigu
    - Content-type：application/x-www-for-urlencoded
    - User-Agent：chrome 83
  - 空行：
  - 体：username=admin&password=admin

- 响应报文：

  - 行：HTTP/1.1  200  OK

  - 头：

    Content-Type：text/html；charset=utf-8

    Content-length：2048

    Content-encoding：gzip

  - 空行

  - 体：

    ```html
     <html>
        <head>
        </head>
        <body>
        	<h1>我是h1</h1>
        </body>
    </html>
    ```

# AJA发送GET请求：

- 1-GET.html：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    #result {
      width: 200px;
      height: 100px;
      border: solid 1px red;
    }
  </style>
</head>
<body>
  <button>点击发送请求</button>
  <div id="result"></div>
  <script>
    // 获取button元素
    const btn = document.getElementsByTagName('button')[0];
    const result = document.getElementById("result");
    // 绑定事件
    btn.onclick = function () {
      // 1、创建对象
      const xhr = new XMLHttpRequest();
      // 2、初始化，设置请求方法和url
      xhr.open('GET', 'http://127.0.0.1:8000/server');
      // 3、发送
      xhr.send();
      // 4、事件绑定 处理服务端返回的结果
      // on  when 当...的时候
      // readystate  是 xhr 对象中的属性，表示状态 0 1 2 3 4
      // change  改变
      xhr.onreadystatechange = function () {
        // 判断（服务端返回了所有的结果）
        if (xhr.readyState === 4) {
          // 判断响应状态码 200 404 403 401 500
          if (xhr.status >= 200 && xhr.status < 300) {
            // 处理结果  行 头 空行 体
            // 1、响应行
            // console.log(xhr.status);
            // console.log(xhr.statusText);
            // console.log(xhr.getAllResponseHeaders());
            // console.log(xhr.response);
            // 设置result的文本
            result.innerHTML = xhr.response;
          }
        }
      }
    }
  </script>
</body>

</html>
```

- server.js

```JavaScript
// 1、引入express
const express = require('express');

// 2、创建引用对象
const app = express();

// 3、创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
app.get('/server',(request, response)=>{
  // 设置响应头
  response.setHeader('Access-Control-Allow-Origin','*');
  // 设置响应体
  response.send('HELLO AJAX');
});

// 4、监听端口启动服务
app.listen(8000,()=>{
  console.log("服务已经启动，8000 端口监听中...");
})
```

# AJAX发送POST请求：

- 2-POST.html

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>POST</title>
  <style>
    #result {
      width: 200px;
      height: 100px;
      border: 1px solid red;
    }
  </style>
</head>
<div id="result"></div>
<script>
  // 获取元素对象
  const result = document.getElementById('result');
  // 绑定事件
  result.addEventListener("mousemove", function () {
    // 创建对象
    const xhr = new XMLHttpRequest();
    // 初始化 设置类型与url
    xhr.open('POST', 'http://127.0.0.1:8000/server');
    // 发送
    xhr.send();
    // 事件绑定
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4) {
        if (xhr.status >= 200 && xhr.status < 300) {
          result.innerHTML = xhr.response;
        }
      }
    }
  })
</script>

<body>

</body>

</html>
```

- server.js

```javascript
// 1、引入express
const express = require('express');

// 2、创建引用对象
const app = express();

// 3、创建路由规则
// request 是对请求报文的封装
// response 是对响应报文的封装
app.post('/server',(request, response)=>{
  // 设置响应头
  response.setHeader('Access-Control-Allow-Origin','*');
  // 设置响应体
  response.send('HELLO AJAX');
});

// 4、监听端口启动服务
app.listen(8000,()=>{
  console.log("服务已经启动，8000 端口监听中...");
})
```

# AJAX设置请求头信息：

xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');

- 放在xhr.open()后
- 放在xhr.send()前

# 请求超时与网络异常处理：

- 请求两秒后自动取消

```javascript
xhr.timeout = 2000;
```

- 超时回调

```javascript
xhr.ontimeout = function() {
	alert('网络异常，请稍后重试！！！');
}
```

# 取消请求：

调用abort()即可取消请求

# 重复请求问题：

定义一个变量：

let isSending = false //判断是否正在发送请求

if(isSending)  x.abort()  //如果正在发送，则取消该请求，创建一个新的请求

# jQuery发送AJAX请求：

get请求：

```javascript
$.get(url,[data],[callback],[type])
//url：请求的url地址
//data：请求携带的参数
//callback：载入成功时回调函数
//type：设置返回内容，xml，html，script，json，text，_default
```

post请求：

```javascript
$.post(url,[data],[callback],[type])
//url：请求的url地址
//data：请求携带的参数
//callback：载入成功时回调函数
//
```

通用ajax请求：

```JavaScript
$.ajax({
    url:'url地址',
    data:{放数据},
    type:'请求方式',
    dataType:'数据格式',
    //成功请求后的操作
    success:function(){
        
    },
    //失败回调
    error:function() {
    
	},
    //头信息
    headers:{
        
    }
})
```

























