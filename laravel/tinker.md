## 定义
控制台驱动，tinker 允许您从交互式 shell 中的命令行与 Laravel 应用程序进行交互
## 启动
`php artisan tinker`
## 常用命令
| 命令 | 用途 |
| --- | --- |
|  `doc request`   |   查找有关函数或方法的文档  |
| `help` | 查看PsySh内置功能 |
## 用途
1. 可以执行一部分`php artisan`命令
2. 测试`Laravel`代码
```
use App\User;
factory(User::class, 5)->create();
User::limit(10)->get();
```
## REPL
### 定义
REPL 是**Read Eval Print Loop**的缩写，它是一种交互式 shell，它接受单个用户输入，运行它们，并将结果返回给用户。
### 在laravel以外使用`PsySH`
1. 全局安装`composer global require psy/psysh:@stable`
2. 启动`psysh`
3. 常用命令

| 命令     |   用途   |
| --- | --- |
|  `show In_array`   |   显示一个命令的源代码  |
| `help` | 查看PsySh内置功能 |