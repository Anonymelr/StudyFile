### 一、Redis-key

|      命令       |       说明        | 备注 |
| :-------------: | :---------------: | :--: |
|     keys *      |    查看所有key    |      |
|   EXISTS key    | 查看改key是否存在 |      |
| EXPIRE key TIME |  设置key存在时间  |      |
|     ttl key     |  获取key存在时间  |      |
|    type key     |   获取key的类型   |      |

### 二、基本数据类型

- 存储结构：

![img](https://img-blog.csdnimg.cn/20200110103048279.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQwMzA2MDkx,size_16,color_FFFFFF,t_70)

#### 1.String类型：

|   命令   |                          说明                          |          备注           |
| :------: | :----------------------------------------------------: | :---------------------: |
|   set    |                         设置值                         |                         |
|   get    |                         获取值                         |                         |
|  append  |                       追加字符串                       |                         |
|  strlen  |                     获取字符串长度                     |                         |
|   incr   |                         自增1                          |       浏览量应用        |
|   decr   |                         自减1                          |                         |
|  incrby  |                 可以设置步长，指定增量                 |                         |
|  decrby  |                 可以设置步长，指定减量                 |                         |
| getrange |                      获取部分字串                      | （0，-1）获取全部字符串 |
| setrange |                替换指定位置开始的字符串                |                         |
|  setex   |                      设置过期时间                      |                         |
|  setnx   |                     不存在时才设置                     |                         |
|   mset   |                       批量设置值                       |                         |
|   mget   |                       批量获取值                       |                         |
|  msetnx  |               批量设置值（不存在才成功）               |       原子性操作        |
|  getset  | 如果不存在值，则返回null；如果存在值，获取值并设置新值 |                         |

```
set user:{id}:username weihp
set user:{id}:age 22
使用json来当key
```

String类似的使用场景：value除了是我们的字符串还可以是我们的数字！

- 计数器
- 统计多单位的数量
- 粉丝数
- 对象缓存存储

#### 2.List类型

基本的数据类型，列表

在redis里面，可以把list玩成栈、队列、阻塞队列！

所有的list命令都是以l开头的

|   命令    |                      说明                       |        备注        |
| :-------: | :---------------------------------------------: | :----------------: |
|   lpush   |                 在列表头部插入                  |                    |
|   rpush   |                 在列表尾部插入                  |                    |
|  lrange   |              通过区间获取list的值               |                    |
|   lpop    |                 在列表头部取出                  |                    |
|   rpop    |                 在列表尾部取出                  |                    |
|  lindex   |                 通过下标获取值                  |                    |
|   llen    |                  获取列表长度                   |                    |
|   lrem    |     移除list集合中指定个数的value，精确匹配     |                    |
|   ltrim   |    通过下标截取指定的长度，只剩下截取的元素     |                    |
| rpoplpush |  移除列表的最后一个元素，将它移动到新的列表中   |                    |
|   lset    |  将列表中指定下标的值替换为另一个值，更新操作   | 若该值不存在会报错 |
|  linsert  | 将某一个具体的value插入到列中某个值的前面或后面 |                    |

消息排队！消息队列（lpush  rpop）、栈（lpush  lpop）

#### 3.Set类型（集合）

set中的值是不能重复的

|    命令     |                  说明                  | 备注 |
| :---------: | :------------------------------------: | :--: |
|    sadd     |                添加元素                |      |
|  smembers   |             查看set所有值              |      |
|  sismember  |        判断某一个值是否在set中         |      |
|    srem     |           移除set中指定元素            |      |
|    scard    |        获取set集合中的指定元素         |      |
| srandmember |         随机抽选指定个数的元素         |      |
|    spop     |            随机删除一个元素            |      |
|    smove    | 将一个集合中的指定元素移动到另一个集合 |      |
|    sdiff    |                  差集                  |      |
|   sinter    |                  交集                  |      |
|   sunion    |                  并集                  |      |

微博，A用户将所有的关注的人放在一个set集合中！将他的粉丝也放在一哥集合中！

共同关注，共同爱好，二度好友，推荐好友！（六度分隔理论）

#### 4.Hash类型（哈希）

Map集合，key-map！这时候这个值是一个map集合！本质和String类型没有太大区别，还是一个简单的key-value！

|  命令   |                说明                | 备注 |
| :-----: | :--------------------------------: | :--: |
|  hset   |      设置一个具体的key-value       |      |
|  hget   |           获取一个字段值           |      |
|  hmset  |         设置多个key-value          |      |
|  hmget  |           获取多个字段值           |      |
| hgetall |            获取全部数据            |      |
|  hdel   |            删除指定字段            |      |
|  hlen   |         获取hash中字段数量         |      |
| hexists |     判断hash中指定字段是否存在     |      |
|  hkeys  |           只获取所有key            |      |
| hvalues |          只获取所有value           |      |
| hincrby |              指定增量              |      |
| hsetnx  | 若不存在，则设置；若存在，则不设置 |      |

hash变更的数据 user name age，尤其是用户信息之类的，经常变动的信息！

hash更适合对象的存储，String更适合字符串的存储。

#### 5.Zset类型（有序集合）

在set的基础上，增加了一个值，set k1 v1   ——>  zset k1 score1 v1

|     命令      |            说明            | 备注 |
| :-----------: | :------------------------: | :--: |
|     zadd      |           添加值           |      |
|    zrange     | 通过区间获取值（从小到大） |      |
|   zrevrange   | 通过区间获取值（从大到小） |      |
| zrangebyscore |            排序            |      |
|     zrem      |        移除指定元素        |      |
|     zcard     |    获取zset中的元素个数    |      |
|    zcount     |   获取指定区间的元素数量   |      |

案例思路：set 排序

存储班级成绩表，工资排序

1，普通消息；2，重要消息，按权重排序

排行榜应用实现

### 三、特殊数据类型

#### 1.geospatial（地理位置）

朋友的定位，附近的人，打车距离计算？

这个功能可以推算地理位置的信息，两地之间的距离，方圆百里的人

|       命令        |                           说明                            |       备注       |
| :---------------: | :-------------------------------------------------------: | :--------------: |
|      geoadd       |      添加地理位置；参数： key  （纬度、经度、名称）       | 两极无法直接添加 |
|      geopos       |                   获取指定位置的经纬度                    |                  |
|      geodist      |                  查看两个位置的直线距离                   |                  |
|     georadius     |    获取指定位置方圆半径的所有位置（可以限制位置数量）     |                  |
| georadiusbymember |    获取指定元素方圆半径的所有位置（可以限制位置数量）     |                  |
|      geohash      | 返回一个或多个位置的经纬度（11个字符的geohash字符串表示） |                  |

geo底层的实现原理其实就是Zset！我们可以用Zset命令来操作geo

#### 2.Hyperloglog（基数）

基数--不重复的元素，可以接受误差

优点：占用的内存是固定的，2^64不同的元素的基数，只需要12KB内存！

网页的UV（一个人访问一个网站多次，但是还是算作一个人！）

0.81%错误率！统计UV任务可以忽略不计

|  命令   |     说明     | 备注 |
| :-----: | :----------: | :--: |
|  pfadd  | 创建一组元素 |      |
| pfcount | 统计元素数量 |      |
| pfmerge |     合并     |      |

如果允许容错，那么一定可以使用Hyperloglog！

如果不允许容错，就是用set或者自己的数据类型即可！

#### 3.Bitmaps

位存储

统计用户信息，活跃、不活跃！登录、未登录！打卡、365打卡！两个状态的，都可以使用Bitmaps！

|   命令   |       说明        | 备注 |
| :------: | :---------------: | :--: |
|  setbit  |     设置状态      |      |
|  getbit  |     获取状态      |      |
| bitcount | 统计状态为1的数量 |      |

统计操作，统计打卡的天数！

#### 4.Stream（流）

其实是一个消息链表，每个消息都有唯一的消息id，消息是持久化的，Redis重启后消息仍在。

支持多播的可持久化的消息队列。

|  命令  |                       说明                       |                    备注                     |
| :----: | :----------------------------------------------: | :-----------------------------------------: |
|  xadd  |                 向Strem追加消息                  | Redis生成的消息ID，由两部分组成:时间戳-序号 |
|  xdel  |          从Stream中删除消息，只是做标记          |                                             |
| xrange | 获取Stream中的消息列表，会自动过滤已经删除的消息 |                                             |
|  xlen  |               获取Stream的消息长度               |                                             |
|  del   |        删除整个Stream消息列表中的所有消息        |                                             |

### 四、事务

### 五、Jedis

1.导入对应的依赖

```java
<!--导入jedis包-->
    <dependencies>
        <dependency>
            <groupId>redis.clients</groupId>
            <artifactId>jedis</artifactId>
            <version>3.2.0</version>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>fastjson</artifactId>
            <version>1.2.62</version>
        </dependency>
    </dependencies>
```

2、编码测试

- 连接数据库

- 操作命令

- 断开连接

  ```java
  package com.weihp;
  
  import redis.clients.jedis.Jedis;
  
  /**
   * @author weihp
   * @version 1.0
   * @ClassName TestPing
   * @Description TODO
   * @Date 2020/9/16 9:50
   */
  public class TestPing {
      public static void main(String[] args) {
          //1、 new Jedis 对象
          Jedis jedis = new Jedis("127.0.0.1",6379);
  
          System.out.println(jedis.ping());
      }
  }
  
  ```

### 六、Redis持久化

#### 1、RDB

rdb保存的文件是dump.rdb，都是在我们的配置文件中快照实现的

>触发机制:
>
>1.save的规则满足的情况下，会触发rdbguize
>
>2.执行flushall命令，也会触发我们的rdb规则！
>
>3.退出redis，也会产生rdb文件

备份就自动生成一个dump.rdb

>如果恢复rdb文件：
>
>1.只需要将rdb文件放在我们redis启动目录就可以，redis启动的时候就会自动检查dump.rdb恢复其中的数据！
>
>2.查看需要存在的位置

优点：

​	1.适合大规模的数据恢复！

​	2.对数据完整行不高！

缺点：

​	1.需要一定的时间间隔进程操作！如果redis意外宕机了，这个最后一次修改数据就没有了！

​	2.frok进程的时候，会占用一定的内存空间！！！

#### 2、AOF（默认是不开启的）

aof保存的文件是appendonly.aof

将所有命令都记录下来，history，恢复的时候就把这个文件中的命令全部执行一遍！！

优点：

​	1.每一次修改都同步，文件的完整性就会更好！

​	2.每秒同步一次，可能会丢失一秒的数据

​	3.从不同步，效率最高的！

缺点：

​	1.相对于数据文件来说，aof远远大于rdb，修复的速度也比rdb慢！

​	2.aof运行效率也要比rdb慢，所以redis的持久化配置默认是rdb。

### 七、Redis缓存穿透和雪崩

