[TOC]
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


## 备用
1. 在shell中不小心按`ctrl+S`后终端无反应，按`ctrl_q`可恢复


