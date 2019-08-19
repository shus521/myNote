`[TOC]
## 代码复用机制`trait`
旨在用细粒度和一致的方式来组合功能。 无法通过 trait 自身来实例化。它为传统继承增加了水平特性的组合；也就是说，应用的几个 Class 之间不需要继承
```
<?php  
trait ezcReflectionReturnInfo {  
    function getReturnType() { /\*1\*/ }  
    function getReturnDescription() { /\*2\*/ }  
}  
  
class ezcReflectionMethod extends ReflectionMethod {  
    use ezcReflectionReturnInfo;  
    /\* ... \*/  
}  
  
class ezcReflectionFunction extends ReflectionFunction {  
    use ezcReflectionReturnInfo;  
    /\* ... \*/  
}  
?>
```
`trait`方式引入的类库需要注意优先级，从基类继承的成员将被`trait`插入的成员所覆盖。优先顺序是来自当前类的成员覆盖了`trait`的方法，而`trait`则覆盖了被继承的方法。

`trait`类中不支持定义类的常量，在`trait`中定义的属性将不能在当前类中或者继承的类中重新定义。
为了解决多个`trait`在同一个类中的命名冲突，需要使用`insteadof`操作符来明确指定使用冲突方法中的哪一个。

以上方式仅允许排除掉其它方法，`as`操作符可以将其中一个冲突的方法以另一个名称来引入。

## xdebug
1. 点击[xdebug](https://xdebug.org/download.php)下载插件(php版本、位数、VC版本、线程安全要对应)
![](https://i.vgy.me/JHlIpD.png)
2. 修改php.ini配置文件
```
[Xdebug]
zend_extension="E:\IM\im_webserver\php\ext\php_xdebug-2.5.5-5.6-vc11.dll" 
xdebug.remote_enable=1
#与remote_connect_back不能同时开启
xdebug.remote_host="localhost" 
xdebug.remote_port=9001
 #与remote_host不能同时开启
;xdebug.remote_connect_back = 1 
xdebug.remote_handler="dbgp"
xdebug.idekey=PHPSTORM
```
![](https://i.vgy.me/BucSQO.png)
![](https://i.vgy.me/PffE4p.png)![](https://i.vgy.me/nXaMMW.png)

## 获取本机ipve地址
```
$ip = gethostbynamel($_ENV['COMPUTERNAME']);
$ip = $ip[count($ip) - 1];
```

