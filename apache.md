## ab测压. 
1. 安装目录`apache\bin\ab.exe`,一般apache自带，如无自行下载
2. 参数说明

|  参数 | 说明  |
| --- | --- |
|  -n   | 指定请求数 |
| -c| 并发数，一次发送多少请求|
| -T | post发送的数据类型，也就是header中content-type的值  如-T application/json 说明发送的是json数据 |
| -p| 使用post方式发送数据|
| -H | 在header中添加信息 |
## 修改日志文件为每天生成一个
```
#ErrorLog "logs/error.log"
ErrorLog "|bin/rotatelogs.exe -l logs/error-%Y-%m-%d.log 86400"
#CustomLog "logs/access.log" common
CustomLog "|bin/rotatelogs.exe -l logs/access-%Y-%m-%d.log 86400" common
```
## 修改MPM模块配置
### 背景
客户apache内存突然升高，查看日志发现有如下报错
```
[Wed Jul 24 09:02:28.999131 2019] [mpm_winnt:notice] [pid 18948:tid 388] AH00354: Child: Starting 64 worker threads.
[Wed Jul 24 09:02:29.009139 2019] [mpm_winnt:error] [pid 18948:tid 2220] AH00326: Server ran out of threads to serve requests. Consider raising the ThreadsPerChild setting
```
### 解决方案
1. 在`httpd.conf`启用MPM模块，`Include conf/extra/httpd-mpm.conf`
2. 修改`http-mpm.conf`中
```
 <IfModule mpm_winnt_module>
    ThreadsPerChild      521
    MaxRequestsPerChild    3000
</IfModule>
```
![](https://i.vgy.me/zBfrOf.png)
## windows下apache做成服务
1. 进入apache bin目录
2. 
```
    httpd -k install -n httpd
```
3. 到系统服务中启动(设置自动启动)
## apache配置多端口多站点
1. 修改`httpd.conf`
```
1. 去掉LoadModule vhost_alias_module modules/mod_vhost_alias.so前面的#标志启用该模块
2. 去掉Include conf/extra/httpd-vhosts.conf前的#标识加载该文件配置
3. 添加Listen 81标识把81端口添加监听
```
2. 在httpd_vhosts.conf中追加配置
```
 <VirtualHost *:81>
    DocumentRoot "E:\xampp\htdocs\zentaopms\www"
    ServerName zentao.com
    <Directory "E:\xampp\htdocs\zentaopms\www">
    Options FollowSymLinks ExecCGI
    AllowOverride All
    Order allow,deny
    Allow from all
    Require all granted
    </Directory>
    </VirtualHost>
```
3. 重启apache

