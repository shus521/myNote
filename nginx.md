## [安装](./nginx/安装.md)
## 配置二级域名
1. 在域名提供商处添加域名解析![UTOOLS1575528069976.png](https://user-gold-cdn.xitu.io/2019/12/5/16ed4ca811c5dd5f?w=662&h=487&f=png&s=22366)
2. 在`nginx.conf`中配置![UTOOLS1575528178694.png](https://user-gold-cdn.xitu.io/2019/12/5/16ed4cc273ff90e0?w=641&h=401&f=png&s=22908)
3. 在上一步配置的目录中新增文件`blog.conf`
4. ![UTOOLS1575528260523.png](https://user-gold-cdn.xitu.io/2019/12/5/16ed4cd66ae20194?w=382&h=165&f=png&s=6142)
```
server {
    listen 80;
    server_name blog.tyss.site;

    location / {
        proxy_set_header   X-Real-IP $remote_addr;
        proxy_set_header   Host      $http_host;
        proxy_pass         http://0.0.0.0:8099;
    }
}
```