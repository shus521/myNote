## 用途
sed 是一个用来筛选与转换文本内容的工具。一般用来批量替换，删除某行文件。
每个 sed 命令，基本可以由选项，匹配与对应的操作来完成
## 选项
* `-n` 打印匹配内容行
* `-i` 直接替换文本内容
* `-f`指定 sed 脚本文件，包含一系列 sed 命令
## 匹配
*   `/reg/`: 匹配正则
*   `3`: 数字代表第几行
*   `$`: 最后一行
*   `1,3`: 第一行到第三行
*   `1,+3`: 第一行，并再往下打印三行 (打印第一行到第四行)
*   `1, /reg/`第一行，并到匹配字符串行
## 操作
*   `a`: append, 下一行插入内容
*   `i`: insert, 上一行插入内容
*   `p`: print，打印，通常用来打印文件某几行，通常与`-n`一起用
*   `s`: replace，替换，与 vim 一致
## 示例
```
# 打印第1-5行
ps -ef | sed -n 1,5p
# 打印最后一行
ps -ef | sed -n '$p'
# 删除第三行内容
sed '3d' hello.txt
# 管道操作，过滤包含ssh的内容，和grep类似
ps -ef | sed -n /ssh/p
# 删除匹配字符串的行
sed /one/d hello.txt
# 替换字符串
echo hello | sed s/hello/world/
# 把 hello 替换成 world
sed -i s/hello/world/g hello.txt
```