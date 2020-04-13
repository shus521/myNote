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
## 执行存储过程
```
$sql='{ call Extend_TuiFei_WorkFlowShenHe_Tigger('.$tableId.') }';
$conn=DB::connection('sqlsrv');
$res = $conn->update($sql);
```

1. 将查询结果中的某字段作为key`keyBy`
2. `firstOrCreate`会报错，只需在`model`中添加`protected $fillable = ['openid'];`
3. 修改`create_at`为其他字段`const CREATED_AT = 'create_time';`不需自动填充`const UPDATED_AT = null;`
4. 自定义时间格式`protected $dateFormat = 'U';`