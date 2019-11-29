[TOC]
## 国内镜像
1. `go get -u github.com/gpmgo/gopm`安装gopm
2. `gopm get -g golang.org/x/net` 带g参数下载到GOPATH，不带g下载到vendor
## import
1. 加下划线如`import _ blog`表示只为了执行init()函数，不能调用包的其他方法
2. 加点如`import . blog`导入之后调用这个包方法的时候可以直接调用，省略包名
3. 别名`import f fmt`将fmt别名为f，调用时通过f调用
## 技巧
1. go使用包package作为基本单位管理代码(php命名空间)
2. import其他包来导入依赖包(php use)
3. ***不得导入无用包***
4. 预定义常量`true`、`false`、`iota`;`iota`可被编辑器修改，在每一个`const`关键字出现时被重置为 0，然后在下一个`const`出现之前，每出现一次`iota`，其所代表的数字会自动增 1
```
package main

const (    // iota 被重置为 0
    c0 = iota   // c0 = 0
    c1 = iota   // c1 = 1
    c2 = iota   // c2 = 2
)

const (
    u = iota * 2;  // u = 0
    v = iota * 2;  // v = 2
    w = iota * 2;  // w = 4
)

const x = iota;  // x = 0
const y = iota;  // y = 0
```
还可以省略后一个赋值表达式
```
const ( 
    c0 = iota 
    c1 
    c2 
)

const ( 
    u = iota * 2 
    v 
    w 
)
```