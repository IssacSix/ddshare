[TOC]

## 搭建node中间层



调研点：

1. 【nodeAPI】 调java现有接口 request、superagent可选包
2. 【nodeAPI】 oauth2设置权限
3. 【nodeAPI】 restful jsonwebtoken 设计定义
4. 【nginx】web 框架层的 访问次数，文件大小，压缩



### Node 调用 JavaAPI: Request包







###API安全性设计：JWT

####JWT标准相关概述

**关于JWT (json web token)**

作用：安全性，防止csrf攻击

三个组成部分：

1. header: 对称加密

   * 声明加密类型

   * 申明加密算法

     ```
     {
       'typ': 'JWT',
       'alg': 'HS256'
     }
     ```

   ​

2. payload：对称加密

   * 标准中注册的声明：（标准建议但不强制使用）

   * 公共的声明：一般添加用户的相关信息或者业务相关信息

   * 私有的声明：

     ```
     {
       "sub": "1234567890",
       "name": "John Doe",
       "admin": true
     }
     ```

     ​

3. signature：签证信息

   * 加密后的header
   * 加密后的payload
   * secret: 将加密后的header跟payload以"."进行字符串拼接后使用header中type加盐，组合加密



####JWT应用场景

一般是在请求头里加入`Authorization`，并加上`Bearer`标注：

```
fetch('api/user/1', {
  headers: {
    'Authorization': 'Bearer ' + token
  }
})
```



#### 我的JWT设计

差不多搞清了JWT是怎么一回事，采用 [node-jsonwebtoken](https://github.com/auth0/node-jsonwebtoken) 模块

Example

```
// sign with default (HMAC SHA256)
var jwt = require('jsonwebtoken');
var token = jwt.sign({ foo: 'bar' }, 'shhhhh');
//backdate a jwt 30 seconds
var older_token = jwt.sign({ foo: 'bar', iat: Math.floor(Date.now() / 1000) - 30 }, 'shhhhh');

// sign with RSA SHA256
var cert = fs.readFileSync('private.key');  // get private key
var token = jwt.sign({ foo: 'bar' }, cert, { algorithm: 'RS256'});

// sign asynchronously
jwt.sign({ foo: 'bar' }, cert, { algorithm: 'RS256' }, function(err, token) {
  console.log(token);
});
```





















