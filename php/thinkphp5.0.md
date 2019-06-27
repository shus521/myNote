[TOC]
## 对模型的查询和写入进行封装`scope`
~~~
namespace app\index\model;

use think\Model;

class User extends Model
{

    protected function scopeThinkphp($query)
    {
        $query->where('name','thinkphp')->field('id,name');
    }
    
    protected function scopeAge($query)
    {
        $query->where('age','>',20)->limit(10);
    }    
    
}
~~~
就可以使用一下方法查询
~~~
// 查找name为thinkphp的用户
User::scope('thinkphp')->find();
// 查找年龄大于20的10个用户
User::scope('age')->select();
// 查找name为thinkphp的用户并且年龄大于20的10个用户
User::scope('thinkphp,age')->select();
~~~
或者使用闭包查询
~~~
User::scope(function($query){
    $query->where('age','>',20)->limit(10);
})->select();
~~~
支持传入参数
支持动态调用
~~~
$user->thinkphp()->get();
~~~
