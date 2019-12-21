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
### lumen路由配置nginx
```
        set   $root_path   '项目路径/public';
        root   $root_path;
        location / {
                try_files $uri $uri/ /index.php?$query_string;
        }
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
## jwt封装类
~~~
<?php


namespace App\Utility;


class JwtBase {
    //头部
    private static $header=array(
        'alg'=>'HS256', //生成signature的算法
        'typ'=>'JWT'  //类型
    );
    //使用HMAC生成信息摘要时所使用的密钥
    private static $key='KEY';

    /**
     * 获取jwt token
     * @param array $payload jwt载荷  格式如下非必须
     * [
     * 'iss'=>'jwt_admin', //该JWT的签发者
     * 'iat'=>time(), //签发时间
     * 'exp'=>time()+7200, //过期时间
     * 'nbf'=>time()+60, //该时间之前不接收处理该Token
     * 'sub'=>'www.admin.com', //面向的用户
     * 'jti'=>md5(uniqid('JWT').time()) //该Token唯一标识
     * ]
     * @return bool|string
     */
    public static function getToken(array $payload)
    {
        $arr = [
            'iss'=>'tianyuan', //该JWT的签发者
            'iat'=>time(), //签发时间
            'exp'=>time()+3600*24*15, //过期时间
            'nbf'=>time(), //该时间之前不接收处理该Token
            'sub'=>'', //面向的用户
            'jti'=>md5(uniqid('JWT').time()) //该Token唯一标识
        ];
        $payload = array_merge($arr,$payload);
        if(is_array($payload))
        {
            $base64header=self::base64UrlEncode(json_encode(self::$header,JSON_UNESCAPED_UNICODE));
            $base64payload=self::base64UrlEncode(json_encode($payload,JSON_UNESCAPED_UNICODE));
            $token=$base64header.'.'.$base64payload.'.'.self::signature($base64header.'.'.$base64payload,self::$key,self::$header['alg']);
            return $token;
        }else{
            return false;
        }
    }

    /**
     * 验证token是否有效,默认验证exp,nbf,iat时间
     * @param string $Token 需要验证的token
     * @return bool|string
     */
    public static function verifyToken(string $Token)
    {
        $tokens = explode('.', $Token);
        if (count($tokens) != 3)
            return false;

        list($base64header, $base64payload, $sign) = $tokens;

        //获取jwt算法
        $base64decodeheader = json_decode(self::base64UrlDecode($base64header), JSON_OBJECT_AS_ARRAY);
        if (empty($base64decodeheader['alg']))
            return false;

        //签名验证
        if (self::signature($base64header . '.' . $base64payload, self::$key, $base64decodeheader['alg']) !== $sign)
            return false;

        $payload = json_decode(self::base64UrlDecode($base64payload), JSON_OBJECT_AS_ARRAY);

        //签发时间大于当前服务器时间验证失败
        if (isset($payload['iat']) && $payload['iat'] > time())
            return false;

        //过期时间小宇当前服务器时间验证失败
        if (isset($payload['exp']) && $payload['exp'] < time())
            return false;

        //该nbf时间之前不接收处理该Token
        if (isset($payload['nbf']) && $payload['nbf'] > time())
            return false;

        return $payload;
    }

    /**
     * base64UrlEncode  https://jwt.io/ 中base64UrlEncode编码实现
     * @param string $input 需要编码的字符串
     * @return string
     */
    private static function base64UrlEncode(string $input)
    {
        return str_replace('=', '', strtr(base64_encode($input), '+/', '-_'));
    }

    /**
     * base64UrlEncode https://jwt.io/ 中base64UrlEncode解码实现
     * @param string $input 需要解码的字符串
     * @return bool|string
     */
    private static function base64UrlDecode(string $input)
    {
        $remainder = strlen($input) % 4;
        if ($remainder) {
            $addlen = 4 - $remainder;
            $input .= str_repeat('=', $addlen);
        }
        return base64_decode(strtr($input, '-_', '+/'));
    }

    /**
     * HMACSHA256签名  https://jwt.io/ 中HMACSHA256签名实现
     * @param string $input 为base64UrlEncode(header).".".base64UrlEncode(payload)
     * @param string $key
     * @param string $alg  算法方式
     * @return mixed
     */
    private static function signature(string $input, string $key, string $alg = 'HS256')
    {
        $alg_config=array(
            'HS256'=>'sha256'
        );
        return self::base64UrlEncode(hash_hmac($alg_config[$alg], $input, $key,true));
    }
}

~~~