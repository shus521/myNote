[TOC]
## 环境变量
1. 查看环境变量`env`、`printenv`
2. 查看其他进程的环境变量`cat /proc/$PID/environ | tr '\0' '\n'`
## 定时同步看云文档到github
1. 同步脚本
```
#########################################################################
# File Name: syncGit.sh
# Description: syncGit.sh
# Author: ty
# Created Time: 2019-06-29 10:15:01
# 先判断仓库文件夹是否存在
# 不存在
#     1.  克隆看云仓库
#     2.  进入目录
#     3.  添加github仓库
#     4.  推送到github
# 存在
#     1.  进入目录
#     2.  pull然后push
#########################################################################
#!/bin/bash 
cd /root/syncGit
if [ ! -d "tyss" ]; then
    git clone git@git.kancloud.cn:shus521/tyss.git
    cd tyss
    git remote add hub git@github.com:shus521/myNote.git
else
    cd tyss
    git pull origin master
fi
echo "`date +%Y-%m-%d,%H:%m:%s`"
git push hub master
```
2. 添加定时任务`/etc/crontab`每半个小时同步一次
```
*/30 * * * * root /root/syncGit/syncGit.sh >> /root/syncGit/sync.log
```
## 目录和文件操作
查找目录：`find /（查找范围） -name '查找关键字' -type d`
查找文件：`find /（查找范围） -name 查找关键字`
## gdb使用
### 定义
GDB是基于UNIX/Linux下的，基于命令行的调试工具，当程序发生coredump，可以通过GDB从core文件中复现场景，定位问题。
### 安装
1. 检查是否安装`rpm -qa | grep gdb`
2. 安装文档系统`yum install ncurses-devel`
3. 安装gdb
```
wget http://ftp.gnu.org/gnu/gdb/gdb-8.3.tar.gz
tar -zxvf gdb-8.3.tar.gz
cd gdb-8.3
./configure
make && make install
```
4. 错误1:`A compiler with support for C++11 language features is required.`
方案1:`yum install -y gcc gcc-c++`
错误2:`makeinfo: command not found`
方案2:`yum install texinfo`

## 备用
1. 在shell中不小心按`ctrl+S`后终端无反应，按`ctrl_q`可恢复
2. 方便快捷下载上传文件`yum install lrzsz`


