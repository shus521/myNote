## 安装
```
curl -L https://github.com/docker/compose/releases/download/1.25.1-rc1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```
查看是否安装成功`docker-compose -v`
## 错误解决
### docker for windows下mysql启动提示`World-writable config file '/etc/mysql/conf.d/mysql.cnf' is ignored`
实则为权限问题，windows上把挂载的配置文件改成只读权限