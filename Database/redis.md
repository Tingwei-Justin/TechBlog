## 什么是redis?

Redis 是用来缓存的常用工具，基于C开发，支持网络，可基于内存也可持久化的日志型，key-value数据库，并提供多种语言API

像MySQL数据库瓶颈？高并发的读写，具体取决于硬件。 大概的并发是在300-700之间。远远不能满足高并发的需求，这时候我们会引入redis 缓存

1. 减轻数据库压力
2. redis是基于内存的，而数据库普遍是存在磁盘中的，通过redis可以加快访问速度

 

NoSQL的数据结构： key-value键值对

Redis 和 hashmap虽然都是存在内存中的， map实现的是本地缓存，特点是轻量以及快速，每个实例都需要各自保存一份缓存，缓存不具有一致性，生命周期伴随着jvm的销毁而结束。redis称为分布式缓存，在多实例的情况下，各实例共用一份缓存数据，缓存具有一致性。

##  Redis 特性

1. 速度快 10w/s

2. 持久化

   redis数据是写在memory中的，一旦断电就会消失。那么每次我们保存在内存的同时会同步写在磁盘中，当系统重启的时候会把数据从磁盘中同步回来

3. 支持多种数据结构

   Key - value

   Value有5种常见的数据结构 

4. 支持多种编程语言

5. 功能丰富

6. 主从复制

7. 高可用及分布式

![image-20200711232203590](../../Library/Application Support/typora-user-images/image-20200711232203590.png)



## Redis 应用场景

1. Counting
2. 展示最近，最热，点击率最高，活跃度最高等等条件的top list
3. 用户最近的访问记录 （redis list) 例如购物车
4. 通过list的lpop以及lpush接口进行队列的写入和消费
5. Redis的lua的功能扩展，例如保证原子性操作，通过编写一个脚本，要么操作全部成功，要么全部失败
6. Redis提供的主从数据同步功能。



## redis底层 resp协议

RESP协议: https://redis.io/topics/protocol

基于TCP的应用层协议RESP (Redis Serialization Protocal)

RESP底层采用的是TCP的连接方式，通过tcp 进行数据传输，然后根据解析规则解析相应信息， 完成交互

优点： 

- 实现简单
- 解析快速
- 易读性高

拿java的redis客户端jedis举例

client jedis  <--------> server  redis

```
set key name

// * + 数据长度
*3 

// $ + 字符串长度
$3
set

$3
key

$4
name
```



## Redis 集群

1. redis cluster （解决自动故障，负载均衡等）
2. 哨兵机制 （解决自动故障）
3. 主从复制 （备份，读写分离）

## Redis性能测试

 ![image-20200712000746252](../../Library/Application Support/typora-user-images/image-20200712000746252.png)

redis自带的性能测试包，用来测试当前redis机器的性能

1. `redis-benchmark -h 127.0.0.1 -p 6379 -c 100 -n 100000 `

   100个并发连接，100000个请求，监测服务器性能

2. `redis-benchmark -h 127.0.0.1 -p 6379 -q -d 100`

   测试存储大小为100字节的数据包的性能

   我们根据具体业务分析一下，value大概的字节是多大，根据平均字节以及最大字节进行测试

![image-20200712002238319](../../Library/Application Support/typora-user-images/image-20200712002238319.png)

3. `redis-benchmark -t set,get -n 100000 -q`

   选择具体数据结构进行测试。e.g. 只测试set, lpush操作的性能

4. `redis-benchmark -n 1000000 -1 script load "redis.call('set','foo', 'bar')"`

   只测试某些数值存取的性能

## 购物车业务需求

![image-20200711225312529](../../Library/Application Support/typora-user-images/image-20200711225312529.png)



签名cookie：服务器通过验证签名来判断cookie是否被改动，但是存在安全漏洞

令牌cookie：该cookie里存储一串随机字符串token作为令牌，服务器可以根据token在数据库中查找此令牌的拥有者。 



Redis设计原则

string, hash, list, set, zset

- 而为表数据相关使用hash类型

  `hset {key} {field1} {value1}`

  `hmset {key} {field1} {value1} ...` 批量插入

  `hget {key} {field}`

  `hgetall {key}`

  `hdel {key} {field}` 删除指定field 

- ZSET 有序集合

  与时间及排序有关使用ZSET类型

  `zadd  {key} {score} {member}`

  `zremrangeByRank  key 0 -26 `  保留最近25个

- 
- 

Key，Value:



## 手写一个客户端



## 手写一个分表分库插件

假如有1 TB的数据，如何将这些数据存在redis内存中？

我们回忆一下

1. 基于mycat中间插件 （代理服务器）来实现mysql的分表分库查询 
2. Java 借助tomcat 和 nginx代理

![image-20200711170237304](../../Library/Application Support/typora-user-images/image-20200711170237304.png)

那么redis 也需要一个代理（网关）

![image-20200711170516715](../../Library/Application Support/typora-user-images/image-20200711170516715.png)

假设有三个服务器

6379 0

6380 1

6381 2



redis网关 (gateway) 既作为客户端又作为服务端, 所以socket + serversocket都需要使用

更改三个服务器配置文件

```
redis-server --port 6379
```



## 读写分离插件

Assume 

6379 主服务器 master

6380 从服务器 slave

6381 从服务器 slave



判断读写操作：根据RESP协议，来判断是读还是写

主服务器从服务器同步

在 redis conf 中配置如下 `slaveof <masterip> <masterport>` 

 



![image-20200711222136792](../../Library/Application Support/typora-user-images/image-20200711222136792.png)





## 怎么样成为一个架构师

![image-20200711222257846](../../Library/Application Support/typora-user-images/image-20200711222257846.png) 