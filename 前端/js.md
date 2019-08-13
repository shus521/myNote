1. 变量提升：所有变量的申明语句，都会被提升到代码的头部。(先解析代码，获取所有申明的语句，再一行行执行；函数也会提升)
2. switch case语句执行的是严格相等运算`===`,不会进行类型转换。
3. 多重循环中，`break`、`continue`不带参数的话只针对最内层循环
4. 语句的前面可以加标签，相当于定位符。通常与`break`、`continue`一起使用，跳出特定的循环
~~~
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
~~~
也可用于跳出代码块{}
5. js数据类型:数值、字符串、undefined、null、布尔值、对象、(ES6中新增Symbol)
6. typeof检测值的类型`typeof 123`
7. typeof null会被检测成object
8. `null`表示一个空的对象，转为数值时为0，`undefined`表示一个此处无定义的原始值，转为数值时为NaN
9. 空数组[]和空对象{}对应的布尔值为true，而空字符串对应的布尔值为false
10. js内部数值都是通过64位的浮点数存储`1 === 1.0`,浮点数不是精确值，涉及到小数计算要谨慎。
~~~
0.3 / 0.1
// 2.9999999999999996
~~~
11. 字符串转数值`parseInt()`,一个个字符转，遇到不能转，返回转好的
   Number()遇到不能转返回NaN
    parseInt第二个参数填要转成的进制
12. 字符串转浮点数`parseFloat()`
13. 判断布尔值`isFinite()`
14.  `btoa()`：任意值转为 Base64 编码; `atob()`：Base64 编码转为原来的值
15. 查看对象属性`Obejct,keys(obj)`
    删除对象属性 `delete obj.p`
    判断属性是否在对象/数组中`p in obj`
    查看是否为自身的属性`obj.hasOwnProperty('toString')`
    遍历对象的属性
~~~
for (var i in obj) {
  console.log('键名：', i);
  console.log('键值：', obj[i]);
}
~~~
操作对象的多个属性with
16. 返回函数名`name`
返回函数参数个数`length`
17. 闭包：定义在函数内部的函数
18. `eval`命令接受一个字符串作为参数，并将这个字符串当作语句执行。
19. 清空数组的方法:length设置为0
20. addEventListener和onclick的区别？
addEventListener可以添加多个监听事件，多次触发；onclick只触发一次
