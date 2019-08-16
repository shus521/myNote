## 自动生成模块
1. 将build.example.php修改名称build.php放到app目录下面
2. 在根目录执行`php think build home`生成模块
3. 删除app下面的controller模块
4. 修改config目录下面的app.php中
```
~~~
    // 自动多应用模式
    'auto_multi_app'   => true,
~~~
```

 
