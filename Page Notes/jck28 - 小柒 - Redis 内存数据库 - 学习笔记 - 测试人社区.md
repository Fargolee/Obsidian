---
page-title: "jck28 - 小柒 - Redis 内存数据库 - 学习笔记 - 测试人社区"
url: https://ceshiren.com/t/topic/29853
date: "2024-04-23 13:40:52"
---
## [](https://ceshiren.com/t/topic/29853#redis-1)一，Redis简介

[![[附件/f715280502dfd2ccd695280d00c817f3_MD5.png]]](https://ceshiren.com/uploads/default/original/3X/8/a/8a6edc315982715752917a2af3d7617132f1b8aa.png "image")

## [](https://ceshiren.com/t/topic/29853#redis-2)二，Redis 安装

## [](https://ceshiren.com/t/topic/29853#h-21-3)2.1， 下载

参考：[redis内存数据库.pdf](https://ceshiren.com/uploads/short-url/2oQM3Jif9VmKrVDFtjwC03Wy0B5.pdf)

## [](https://ceshiren.com/t/topic/29853#h-22-4)2.2，运行

## [](https://ceshiren.com/t/topic/29853#h-23redis-5)2.3，Redis连接：

-   连接redis服务器：redis-cli -h host -p port -c --raw
    -   \-h:主机IP
    -   \-p：端口
    -   \-c：连接redis cluster（集群）时使用
    -   –raw：显示中文数据，不加的话，中文会以utf-8的形式展示

## [](https://ceshiren.com/t/topic/29853#h-6)三，基本数据结构

## [](https://ceshiren.com/t/topic/29853#h-1string-7)（1）String格式：

-   设置指定key的值：set key1 value1 （set list a)
-   获取指定key的值：get key1 (get list)

## [](https://ceshiren.com/t/topic/29853#h-2list-8)（2）list格式：（插入元素可重复）

-   将值插入到列表首位:LPUSH key value ( LPUSH list1 a ）
-   获取列表指定范围内的值：LRANGE key start stop (LRANGE list1 0 10) 获取第0到第10位的元素值

## [](https://ceshiren.com/t/topic/29853#h-3hashk-v-9)（3）Hash格式（又称散列，k-v对应的形式）：

-   将key中字段为field的值设为value：hset key filed value （hset list sex 女）
-   获取key中字段为field的值：hget key field （hget list sex)
-   获取这个key的所有字段和值：hgetall key (hgetall list)

## [](https://ceshiren.com/t/topic/29853#h-4set-10)（4）set集合：其值是无序类型的集合，集合中值唯一

-   向集合添加值：SADD （sadd setlist abc)
-   查找集合所有成员：SMEMBERS (smembers setlist)

## [](https://ceshiren.com/t/topic/29853#h-5zset-11)（5）zset有序集合：其值是有序的集合,每个值有一个分数。集合内值不能重复，但是分数可以重复

-   向有序集合添加值：ZADD myzset 1 “one” (zadd zset 1 “18”)
-   通过索引区间返回有序集合成员：ZRANGE myzset 0 -1 WITHSCORES (zrange zset 0 -1 withscores)

## [](https://ceshiren.com/t/topic/29853#h-6key-12)（6）导出数据（把某个key的所有数据导出）：

-   echo “HGETALL key” | redis-cli -h 10.177.67.186 -p 6379 -c --raw >> test.txt

## [](https://ceshiren.com/t/topic/29853#h-7-13)（7）把数据导入到缓存中：

-   cat wordlist.raw | redis-cli -h 10.177.67.186 -p 6379 -c --raw

## [](https://ceshiren.com/t/topic/29853#javaredis-14)四，Java使用Redis

## [](https://ceshiren.com/t/topic/29853#h-41-15)4.1 引入依赖

```
<!-- https://mvnrepository.com/artifact/redis.clients/jedis -->
 <dependency>
 <groupId>redis.clients</groupId>
 <artifactId>jedis</artifactId>
 <version>3.1.0</version>
 </dependency>
```

## [](https://ceshiren.com/t/topic/29853#h-42-jedis-16)4.2 创建Jedis实例

```
// 连接本地的 Redis 服务
 Jedis jedis = new Jedis("localhost");
 jedis.auth("hogwarts");// 此处为你设置的密码
 System.out.println(" 连接成功 ");
 // 查看服务是否运行
 System.out.println(" 服务正在运行 : "+jedis.ping());
```

## [](https://ceshiren.com/t/topic/29853#h-43-17)4.3 常用方法

-   set(key, value) ：给数据库中名称为 key 的 string 赋予值 value
-   get(key) ：返回数据库中名称为 key 的 string 的 value
-   lpush(key, value) ：在名称为 key 的 list 头添加一个值为 value 的元素
-   lrange(key, start, end) ：返回名称为 key 的 list 中 start 至 end 之间的  
    元素（下标从 0 开始，下同）
-   keys(pattern) ：返回满足给定 pattern 的所有 key