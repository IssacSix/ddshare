## Restful API Rules

1. protocol：http / https
2. domain： https://api.example.com
3. version:    <https://api.example.com/v1>
4. Endpoint: <https://api.example.com/v1/zoos>
5. http动词：
   1. head
   2. get (select)
   3. post (create)
   4. delete (delete)
   5. put (update)
   6. parth (update)
   7. options
6. filtering: search params
7. status code: 
   1. 200	=> ok	// 服务器成功返回数据，幂等操作
   2. 201 => created  // 客户端新建或修改数据成功
   3. 202 => accept   // 请求已进入后台排队
   4. 204 => not connect  // 客户端删除数据成功
   5. 400   // 客户端请求错误
   6. 401 => unauthorized   // 客户端没有权限
   7. 403 => forbidden  // 客户端已被授权但禁止访问
   8. 404 => not found
   9. 406   // 客户端请求格式不可得
   10. 500   // 服务器错误 
8. error handing: { error: ‘xxxxx’} key-value
9. response: 
10. hypermedia: 语义化