[toc]
## 创建项目
```
composer create-project laravel/laravel blog --prefer-dist
npm install
```
## 测试
### 运行
#### windows
1. 项目根目录运行
```
"vendor/bin/phpunit.bat"   //需要加bat和引号
```
2. composer运行
    在composer.json的script中追加如下代码后运行`composer test`
```
    "test": [
        "\"vendor/bin/phpunit.bat\""
    ]
```
#### linux
1. 项目根目录运行`vendor/bin/phpunit`
2. composer运行同windows，把命令改掉即可
### 配置
1. 在根目录下的`phpunit.xml`中
2. 测试文件放置于tests目录下
3. Unit单元测试；Feature功能测试
4. 单元测试和功能测试类都继承自`Tests\TestCase`基类
## [配置](./配置.md)
## [路由](./路由.md)
## 创建表和模型
1. `php artisan make:model -m Models/Post`
命令完成了两件事
1. 在app/Models下创建模型类Post
2. 在`database/migrations`下创建post表的迁移文件
## 数据库迁移
1. 生成一个新的迁移`php artisan make:migration create_users_table`
2. `--table`和`--create`选项可以用于指定表名以及该迁移是否要创建一个新的数据表
3. 运行所有未执行的迁移`php artisan migrate`
### 回滚
1. 回滚最后一次迁移操作`php artisan migrate:rollback`
2. 回滚任意步数迁移`php artisan migrate:rollback --step=5`
3. 回滚所有迁移`php artisan migrate:reset`
#### 重建数据库
~~~
php artisan migrate:refresh
// 重建数据库并填充数据...
php artisan migrate:refresh --seed
php artisan migrate:refresh --step=5
~~~
#### 删除所有表后进行迁移
~~~
php artisan migrate:fresh
php artisan migrate:fresh --seed
~~~
## 模型工厂
1. 快速创建模型工厂`php artisan make:factory PostFactory`
2. `--model` 选项可用于指定当模型工厂被创建时生成模型的名称。这个选项将用给定的模型预填充生成的模型工厂文件
3. 生成新的填充文件`php artisan make:seeder PostsTableSeeder`
4. 运行数据库填充命令`php artisan db:seed`
## 控制器
1. 生成空的控制器`php artisan make:controller BlogController`
## [eloquent](./laravel/eloquent)
4. 可以设置`protected  $cacheFor  =  180;`在该model的所有查询中使用缓存
5. 可以设置指定查询缓存`->cacheFor()`
6. 避免命中缓存`->dontCache()`
7. 在[github](https://github.com/rennokki/laravel-eloquent-query-cache)上查看该项目
## 111
1. 重定向`redirect()`
