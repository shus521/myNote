[TOC]
## node特性
1. Node.js 使用事件驱动模型，当web server接收到请求，就把它关闭然后进行处理，然后去服务下一个web请求。
当这个请求完成，它被放回处理队列，当到达队列开头，这个结果被返回给用户。
## 新建一个http服务器
```
// 引入http模块
var  http  =  require('http');
//创建一个http服务器，监听在8888端口
http.createServer(function(request, response) {
    //设置返回头
    response.writeHead(200, {'Content-Type' :  'text/plain'});
    response.end('Hello World');
}).listen(8888)
```
## npm包管理器
`npm install <module>`本工程内安装模块
`npm install <module> -g` 全局安装模块
`npm list`、`npm ls`查看已安装模块
`npm update <module>` 更新模块
`npm search <module>`搜索模块
`npm init`创建模块
`npm cache clear`清空本地缓存
## 事件触发器EventEmitter
```
// 引入 events 模块
var events = require('events');
// 创建 eventEmitter 对象
var eventEmitter = new events.EventEmitter();
```
注册事件
~~~
emitter.on('someEvent', function(arg1, arg2) { 
    console.log('listener1', arg1, arg2); 
}); 
~~~
触发事件
~~~
emitter.emit('someEvent', 'arg1 参数', 'arg2 参数'); 
~~~

## 模块系统
~~~
exports.world = function() {
  console.log('Hello World');
}
~~~
1. 添加项目依赖项`npm install --save <module>`
2. 删除项目依赖项`npm rm <module --save`
