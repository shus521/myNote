## 安装
```
    curl -R -O http://www.lua.org/ftp/lua-5.3.5.tar.gz
    tar zxf lua-5.3.5.tar.gz
    cd lua-5.3.5
    make linux test
    make install
```
****
报错:`lua.c:82:31: fatal error: readline/readline.h: No such file or directory`
方案:
`yum install readline-devel`
## 语法
1. 启动lua交互命令窗口`lua`或者`lua -i`
2. 在文件开头加入`#!/usr/local/bin/lua`可以指定按照lua脚本来运行
3. 单行注释`--`
4. 多行注释
```
--[=[注释内容]=]
```
5. 仅当一个变量不等于nil时，这个变量即存在(删除变量，将其赋值为nil)
## 数据类型
1. nil：只有nil属于这个类型，表示一个无效值
    nil做比较时需要加引号
2. boolean：true/false
3. number：双精度的实浮点数
4. string：[[]]也可表示字符串
    字符串连接使用`..`
    计算字符串长度用#

5. function：c或者lua编写的函数
6. userdata：表示任意存储在变量中的C数据结构
7. thread：执行的独立线路，用于执行协同程序
    最主要的线程是协同程序（coroutine）。它跟线程（thread）差不多，拥有自己独立的栈、局部变量和指令指针，可以跟其他协同程序共享全局变量和其他大部分东西.
    线程可以同时多个运行，而协程任意时刻只能运行一个，并且处于运行状态的协程只有被挂起（suspend）时才会暂停

8. table：关联数组。数组的索引可以是数字、字符串或表类型。在 Lua 里，table 的创建是通过"构造表达式"来完成，最简单构造表达式是{}，用来创建一个空表
    索引用1开始
## 变量
全局变量、局部变量(local)、表中的域
1. 遇到赋值语句Lua会先计算右边所有的值然后再执行赋值操作，所以我们可以这样进行交换变量的值(x,y = y,x)

