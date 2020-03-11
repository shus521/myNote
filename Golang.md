[TOC]
## 配置代理
![UTOOLS1578376078632.png](https://user-gold-cdn.xitu.io/2020/1/7/16f7e8ba8d158d30?w=1041&h=719&f=png&s=38909)
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
5. 比较浮点数是否相等不能直接比较
```
p := 0.00001
// 判断 float_vlalue_1 与 float_value_2 是否相等
if math.Dim(float64(float_value_1), float_value_2) < p {
    fmt.Println("float_value_1 和 float_value_2 相等")
}
```
## windows编译linux包
在cmd下执行
```
SET CGO_ENABLED=0
SET GOOS=linux
SET GOARCH=amd64
go build main.go
```
## *和&的用法
`&`表示取地址，例如你有一个变量`a`那么`&a`就是变量`a`在内存中的地址，对于golang，指针也是有类型的，比如如果`a`是一个`string`那么`&a`是一个`string`的指针类型，在go里面叫`&string`  
  
所以你看到`b := &a`，a，b是两个不同的变量，a是`string`类型，b是`&string`类型，你用fmt去打印b，你会发现它是一串内存地址，而非a的值  
  
所以为了拿到a的值，有个操作`*`，用来取出指针对应内存地址里存的值，所以当你fmt打印一下`*b`它会跟a一模一样
* [读取和写入json配置文件](./读取和写入json配置文件.md)
## [类](./Go/类.md)
