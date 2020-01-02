
|   参数  | 说明    |
| --- | --- |
|service docker start|启动docker服务|
|  -i |  允许你对容器内的标准输入 (STDIN) 进行交互    |
|  -t |  在新容器内指定一个伪终端或终端    |
| -d| 后台模式|
| docker ps| 查看运行着的docker容器|
| docker logs 容器id | 查看容器内的输出|
| docker stop 容器id | 停止运行着的docker容器 | 
| -P | 容器端口映射到主机端口 |
| docker search php| 搜索镜像|
| docker pull nginx | 拉取镜像|
|docker rm mynginx| 删除容器|
|docker inspect 容器ID或容器名 |grep '"IPAddress"'|查看容器ip|
|docker system prune|可以用于清理磁盘，删除关闭的容器、无用的数据卷和网络|
|docker exec -it mynginx /bin/bash|进入正在运行的容器内部|
## [docker-compose](./docker-compose.md)
## nginx
```
docker run --name mynginx -p 80:80 -v $PWD/www:/var/www -v $PWD/conf/conf.d:/etc/nginx/conf.d -v $PWD/logs:/var/log/nginx -d nginx
```
注：
1. 若无目录，该命令生成的nginx.conf为文件夹，需手动生成
2. nginx.conf需拷贝一份别处的
## php
```
docker pull phpdockerio/php7-fpm
docker run -p 9000:9000 --name  myphp-fpm -v ~/nginx/www:/www -v $PWD/php/conf:/usr/local/etc/php -v $PWD/php/logs:/phplogs   -d phpdockerio/php7-fpm
```

