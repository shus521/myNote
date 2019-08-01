1. 页面跳转后返回到页面上方
~~~
router.afterEach((to,from,next) => {
  window.scrollTo(0,0);
})
~~~
2. vue部署到apache后，刷新会报错，需要修改路由重写规则，让他返回到index.html访问自己的界面
```
<IfModule mod_rewrite.c>
  RewriteEngine On
  RewriteBase /
  RewriteRule ^index\.html$ - [L]
  RewriteCond %{REQUEST_FILENAME} !-f
  RewriteCond %{REQUEST_FILENAME} !-d
  RewriteRule . /index.html [L]
</IfModule>
```
## 跨域
### 出现背景
本地vue请求后端时采用代理，打包到线上后出现跨域post请求变成了option
### 解决方案
1. 引入qs模块`yarn add qs`
2. 使用qs将对象序列化
```
import qs from "qs"
qs.stringify(formdata)
```
## 刷新后页面404
### 出现背景
采用了history模式，上线后发现刷新页面就会404
### 解决方案
将找不到资源的url(不是路径不是文件)重定向到index.html
```
<rule name="blog">
        <match url="^((?!(upload|admin|portal|api)).)*$" />
        <conditions>
            <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="true" />
            <add input="{REQUEST_FILENAME}" matchType="IsDirectory" negate="true" />
        </conditions>
        <action type="Rewrite" url="/index.html" />
    </rule>
```