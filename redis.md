## 配置
1. 获取某一项配置`CONFIG GET CONFIG_SETTING_NAME`
2. 获取所有配置`config get *`
3. 修改配置`CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE`
4. 参数说明
5. 查看redis安装目录`CONFIG GET dir`
5. 
|   配置项  | 说明    |
| --- | --- |
| daemonize no | Redis 默认不是以守护进程的方式运行，可以通过该配置项修改，使用 yes 启用守护进程（Windows 不支持守护线程的配置为 no  |
| pidfile /var/run/redis.pid | 记录守护进程的pid |
| port 6379 | 指定端口 |
| bind 127.0.0.0 | 绑定主机地址 |
| timeout 300 | 当客户端闲置多长时间后关闭连接，如果指定为 0，表示关闭该功能 |
| loglevel notice | 修改日志级别(debug、verbose、notice、warning) |
| logfile stdout | 日志记录方式，默认为标准输出，如果配置 Redis 为守护进程方式运行，而这里又配置为日志记录方式为标准输出，则日志将会发送给 /dev/null |
| databases 16 | 设置数据库的数量，默认数据库为0，可以使用SELECT命令在连接上指定数据库id |
| | |
## 数据类型
1. set key value
2. get key
3. del key
4. 判断键是否存在`EXISTS key`
5. 给键设置过期时间 `EXPIRE key seconds`
### string
1. 一个键最多能存储512M
2. 二进制安全
### Hash（哈希）
键值对集合
~~~
    HMSET runoob field1 "Hello" field2 "World"
    HGET runoob field1
~~~
### List（列表）
简单的字符串列表，按照插入顺序排序
~~~
    lpush runoob redis
    lrange runoob 0 10
~~~
### Set（集合）
string类型的无序集合
集合内元素的唯一性，第二次插入的元素将被忽略
~~~
    sadd runoob redis
    smembers runoob
~~~
### zset(sorted set：有序集合)
string类型元素的集合,且不允许重复的成员
每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序成员是唯一的,但分数(score)却可以重复
~~~
    zadd runoob 0 redis
    ZRANGEBYSCORE runoob 0 1000
~~~
### HyperLogLog(基数)
去重，计数
```
    pfadd key value
    pfcount key
```
## 订阅
创建频道`SUBSCRIBE redisChat`
给频道发消息`PUBLISH redisChat "Redis is a great caching technique"`
## 备份和恢复
备份`save`、`BGSAVE`
恢复:只需将备份文件 (dump.rdb) 移动到 redis 安装目录并启动服务即可
### 缓存雪崩
过期时间相同，大批缓存同时过期产生
### 缓存穿透
数据库中没有的数据，缓存中自然也没有，导致每次都去数据库查
### 缓存击穿
热点数据，在缓存过期时突然大量请求进来，导致数据库奔溃
## 优化
### 缩短键值对的存储长度
### 使用lazy free(延迟删除)特性
### 设置键值对的过期时间
### 禁用长耗时的查询命令
### 使用slowlog优化耗时命令
### 使用Pipeline批量操作数据
### 避免大量数据同时失效
### 客户端使用优化
### 限制Redis内存大小
### 使用物理机，不用虚拟机
### 检查数据持久化策略
### 禁用THP特性
### 使用分布式架构增加读写速度
