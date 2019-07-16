[TOC]
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
[xdebug]
zend_extension="E:\IM\im_webserver\php\ext\php_xdebug-2.5.5-5.6-vc11.dll"　　#指定Xdebug扩展文件的绝对路径
xdebug.auto_trace=on　　#启用代码自动跟踪
xdebug.collect_params=on　　#允许收集传递给函数的参数变量
xdebug.collect_return=on　　#允许收集函数调用的返回值
xdebug.trace_output_dir="F:\AppServ\Xdebug"　　#指定堆栈跟踪文件的存放目录
xdebug.profiler_enable=on　　#是否启用Xdebug的性能分析，并创建性能信息文件
xdebug.profiler_output_dir="F:\AppServ\Xdebug"　　#指定性能分析信息文件的输出目录
xdebug.remote_enable = on　　#是否开启远程调试
xdebug.remote_handler = dbgp　　#指定远程调试的处理协议
xdebug.remote_host= localhost　　#指定远程调试的主机名
xdebug.remote_port = 9000　　#指定远程调试的端口号
xdebug.idekey = PHPSTORM　　#指定传递给DBGp调试器处理程序的IDE Key
```
