[TOC]
## 缓存静态文件
```
<FilesMatch "\.(ico|jpg|jpeg|png|gif|css|js|woff)$">
    Header set Cache-Control "max-age=604800,public"
</FileMatch>
```
将以上内容配置在`.htaccess`文件中，如果对应扩展匹配到，Apache添加头信息，浏览器发现头信息后就会缓存。
## http持久链接
### 优点
1. cpu和内存负载减轻(同一时刻的tcp链接数变少，后续请求和响应无需打开新链接)
2. tcp链接建立以后，请求的等待事件减少
3. 网络堵塞减轻
### 不足
有并发数限制，需要设置链接超时事件
### 配置
1. 在`.htaccess`文件添加
```
<ifModule mod_headers.c>
    Header set Connection keep-alive
</ifModule>
```
2. 或者修改apache配置文件
```
    KeepAlive On
    MaxKeepAlliveRequests 100
    KeepAliveTimeout 100
```
## GZIP压缩
修改`.htaccess`文件
```
<IfModule mod_deflate.c>
SetOutputFilter DEFLATE
AddOutputFilterByType DEFLATE text/html text/plain text/xml text/css
text/javascript application/javascript
SetEnvIfNoCase Request_URI \.(?:gif|jpe?g|png)$ no-gzip dont-vary
</IfModule>
```
## 关闭不用的模块