## 安装
```
yum install -y https://files.freeswitch.org/repo/yum/centos-release/freeswitch-release-repo-0-1.noarch.rpm epel-release
```
## 报错及解决方案
### 问题1
执行`yum install -y https://files.freeswitch.org/repo/yum/centos-release/freeswitch-release-repo-0-1.noarch.rpm epel-release`报错`rpmdb: BDB0113 Thread/process 11221/140261771245632 failed: BDB1507 Thread d`
### 解决
重新构建rpm数据库
```
cd /var/lib/rpm
rm -rf _db*
rpm --rebuilddb
```
