[TOC]
## 开启表单令牌
1. 配置行为绑定：在``tag.php``中添加
```
return array(
    'view_filter' => array('Behavior\TokenBuildBehavior'),
);
```
表示在`view_filter`标签位置执行表单令牌检测行为。
2. 在config.php中添加
~~~
'TOKEN_ON'      =>    true,  // 是否开启令牌验证 默认关闭
'TOKEN_NAME'    =>    '__hash__',    // 令牌验证的表单隐藏字段名称，默认为__hash__
'TOKEN_TYPE'    =>    'md5',  //令牌哈希验证规则 默认为MD5
'TOKEN_RESET'   =>    true,  //令牌验证出错后是否重置令牌 默认为true
~~~
3. 如果个别页面不需要令牌监测，可添加``C('TOKEN_ON',false);``
4. 如果没有调用create方法，需要手动处理
```
if (!$User->autoCheckToken($_POST)){
 // 令牌验证错误
 }
```