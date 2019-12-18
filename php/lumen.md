## 路由配置
* 在`routes/web.php`新增路由。
```
    $router->get('foo',  function  ()  {  
        return  'Hello World';  
    });
```
* 可以注册多种路由`get` `post` `put` `patch` `delete` `option`
### 路由参数
`{id}`必填参数
`'posts/{postId}/comments/{commentId}'`定义多个参数
`'user\[/{name}\]'`可选参数，仅在路由末尾支持
`'user/{name:\[A-Za-z\]+}'`正则表达式约束
`$router->get('/getSignRecord', 'SignController@getSignRecord');`指定路由到控制器方法
### 路由别名
```
$router->get('profile', ['as' => 'profile', function () {
    //
}]);
```
```
// 生成 URLs
$url = route('profile');

// 重定向
return redirect()->route('profile');
```
## 数据查询
* 自定义查询`->select(DB::raw('CONVERT(varchar(30),createtime,120) as createtime'))`
## 用户认证
* lumen是无状态的api，不支持session，必须使用无状态的机制来实现认证，如 API 令牌（Token）
* 在使用 Lumen 的认证功能前，取消`bootstrap/app.php`文件中的`AuthServiceProvider`调用代码的注释。
