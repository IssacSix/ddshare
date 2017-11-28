[TOC]

## 你不知道的CORS

### 什么是CORS

CORS（cross origin resource sharing）: 跨域资源共享。允许浏览器向不能域的服务器发起http请求，从而为ajax提供解决跨域策略。

整个CORS通信，都是浏览器自动完成，一旦发现请求跨域，自动添加header信息，部分还会多一次请求，但用户没有感知。

服务器支持：**接口实现CORS**是关键

浏览器：除了IE10 以上的高级浏览器都能支持



### 对不同类型的CORS请求，浏览器做出的不同反应机制

![=处理流程分析](https://raw.githubusercontent.com/IssacSix/gitImags/master/20171128/cors.png)

### CORS的请求分类

1. 请求方法：
   * head
   * post
   * get
2. http headers 信息不超过一下字段
   * Accept
   * Accept-Language
   * Content-Language
   * Last-Event-ID
   * Content-Type: 仅限三种类型 
     * `application/x-www-form-urlencoded`
     * `multipart/form-data`
     * `text/plain`

