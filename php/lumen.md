[toc]
## 配置
1. Lumen 框架的所有配置项都放置在了`.env`文件，使用`$corpId = env('corpid');`获取
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
## 自定义公共函数
1. 在app目录下新建`helpers.php`，公共函数放置里面。
2. 修改`composer.json`文件，在autoload里加入files字段
```
"autoload": {
    "classmap": [
        "database/seeds",
        "database/factories"
    ],
    "files": [
        "app/helpers.php"
    ],
    "psr-4": {
        "App\\": "app/"
    }
},
```
3. 执行`composer dump-autoload`
4. 或者第二步和第三步换成在`bootstrap/app.php`中添加`require_once __DIR__.'../app/helpers.php';`

