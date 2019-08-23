## 配置
1. 获取某一项配置`CONFIG GET CONFIG_SETTING_NAME`
2. 获取所有配置`config get *`
3. 修改配置`CONFIG SET CONFIG_SETTING_NAME NEW_CONFIG_VALUE`
4. 参数说明
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
~~~
    sadd runoob redis
    smembers runoob
~~~