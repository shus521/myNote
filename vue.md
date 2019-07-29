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
