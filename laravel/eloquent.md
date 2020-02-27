## 缓存eloquent
1. 使用composer装配缓存包`composer require rennokki/laravel-eloquent-query-cache`
2. 在model中引入`use Rennokki\QueryCache\Traits\QueryCacheable;`
3. `use QueryCacheable;`
```
    use Rennokki\QueryCache\Traits\QueryCacheable;
    
    class Podcast extends Model
    {
        use QueryCacheable;
    
        ...
    }
```
## 查看数据库查询出来的模型是否有修改过数据
```
$user->isDirty();  //若$user被修改过，返回true，没有修改过返回false
$user->isDirty('name');  //若email被修改过，返回true，没有修改过返回false
$user->getDirty(); //返回修改过的属性
$user->getOriginal('name');  //查看修改前的值
```

1. 将查询结果中的某字段作为key`keyBy`