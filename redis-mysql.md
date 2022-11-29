# redis mysql

**redis**

1. 1.hash表操作命令：

HSET key field valueHGET key fieldHDEL key fieldHKEYS keyHVALS keyHGETALL key

1. 1.list操作命令

​

| LPUSH key value         | 将一个或多个值插入到列表头部           |
| ----------------------- | ------------------------ |
| LRANGE key start stop   | 获取指定范围元素                 |
| RPOP key                | 移除并获取最好一个元素              |
| LLEN key                | 获取列表长度                   |
| BRPOP key1 key2 timeout | 移除并获取列表最后一个元素，或发现可弹出元素为止 |

1. 1.set常用操作命令

​

| SAND key member1 \[member2] | Text |
| --------------------------- | ---- |
| SMEMBERS key                | ​    |
| SCARD key                   | ​    |
| SINTER                      | ​    |
| SUNION key                  | ​    |

​

| Alter table `release` rename to Release; | 当表名和关键字重复时，需要在表名上加引号，tab键上方 |
| ---------------------------------------- | --------------------------- |
| service mysql stop                       | 启动停止服务                      |
| Tail -f filename                         | 动态查看日志                      |
| Scp fineName root@123.345.334.3          |                             |

### redis缓存失效问题

缓存穿透：查询一个不存在的数据，由于缓存总是不命中，将去查询数据库；

缓存雪崩：大部分key在一段时间内集中过期

缓存击穿：热点key过期

### 分布式锁

&#x20;redission：对于执行时间超时业务，通过watchdog进行锁自动续期，加锁业务完成就不会锁续期主动

解锁，锁也会自动解除；&#x20;

redission锁过期时间要大于业务执行时间，在指定了过期时间后，锁不会自动续期

### 缓存数据一致性

双写模式：写数据库同时修改redis缓存，存在数据一致性问题

失效模式：写数据库同时删除redis缓存

#### 非等于的三种实现

select device\_id,gender,age,university from user\_profile #where university != '复旦大学' #where university not like '复旦大学' # where university not in ('复旦大学')

#### 过滤空值的三种方法：

(1) Where 列名 is not null

(2) Where 列名 != 'null'

(3) Where 列名 <> 'null'

(4) where !=''

#### 如果含有索引，使用or将会失效，全表扫描

SELECT `device_id`,`gender`,`age`,`university`,`gpa` FROM `user_profile` WHERE `university` = '北京大学'

UNION SELECT `device_id`,`gender`,`age`,`university`,`gpa` FROM `user_profile` WHERE `gpa`>3.7

#### 模糊查询

\_：匹配任意一个字符；

```
SELECT * FROM 学生表 WHERE name LIKE ``'张__'``//查询姓“张”且名字是3个字的学生姓名。
```

%：匹配0个或多个字符；

```
SELECT * FROM 学生表 WHERE 姓名 LIKE ‘张%’``//查询学生表中姓‘张’的学生的详细信息。
```

\[ ]：匹配\[ ]中的任意一个字符(若要比较的字符是连续的，则可以用连字符“-”表 达 )；

```
SELECT * FROM 学生表 WHERE 姓名 LIKE '[张李刘]%’``//查询学生表中姓‘张’、姓‘李’和姓‘刘’的学生的情况。
```

\[^ ]：不匹配\[ ]中的任意一个字符。

```
SELECT * FROM 学生表 WHERE 学号 LIKE ``'%[^235]'` `//从学生表表中查询学号的最后一位不是
```

#### 求最大值

\#使用聚合函数取最大值

select max(gpa) from user\_profile where university = '复旦大学'

或者

\#通过gpa倒叙，然后取第一条

select gpa from user\_profile where university = '复旦大学' order by gpa DESC limit 1

#### 覆盖索引：

如果一个索引包含（或者说覆盖）所有需要查询的字段的值，则称之为“覆盖索引”。



#### 慢查询基础：优化数据访问 <a href="#query-optimize-data-access" id="query-optimize-data-access"></a>

查询性能低下最基本的原因是访问的数据太多。

对于低效的查询，下面两步分析总是有效的：

1. 确认应用程序是否在检索大量超过需要的数据。访问了太多的行，有时也可能访问太多的列。
2. 确认 MySQL 服务器层是否在分析大量超过需要的数据行。

查询大量不需要的数据的典型案例：

1. 查询不需要的记录
   * 最简单有效的解决方法就是在这样的查询后面加上 `LIMIT`。
2. 多表关联时返回全部列
3. 总是取出全部列
   * 每次看到 `SELECT *` 时都需要用怀疑的眼光审视，是不是真的需要返回全部的列！
4. 重复查询相同的数据

最简单的衡量查询开销的三个指标如下：

* 响应时间
* 扫描的行数
* 返回的行数

这三个指标都会记录到 MySQL 的慢日志中，所以检查慢日志记录是找出扫描行数过多的查询的好办法

```
// mysql 慢查询日志
SHOW GLOBAL VARIABLES LIKE '%slow%';


```

### 重构查询的方式

**4.3.1. 一个复杂查询还是多个简单查询**

设计查询的时候一个需要考虑的重要问题是，是否需要将一个复杂的查询分成多个简单的查询。

MySQL 从设计上让连接和断开连接都 很轻量级，在返回一个小的查询结果方面很高效。

MySQL 内部每秒能够扫描内存中上百万行数据。

在应用设计的时候，如果一个查询能够胜任时还写成多个独立查询是不明智的。

**4.3.2. 切分查询**

有时候对于一个大查询我们需要“分而治之”，将大查询切分成小查询，每个查询功能完全一样，只完成一小部分，每次只返回一小部分查询结果。例如删除旧的数据。

**4.3.3. 分解关联查询**

可以对每一个表进行一次单表查询，然后将结果在应用程序中进行关联。

用分解关联查询的方式重构查询有如下的优势：

* 让缓存的效率更高。
* 将查询分解后，执行单个查询可以减少锁的竞争。
* 在应用层做关联，可以更容易对数据库进行拆分，更容易做到高性能和可扩展。
* 查询本身效率也可能会有所提升。
* 可以减少冗余记录的查询。
* 这样做相当于在应用中实现了哈希关联，而不是使用 MySQL 的嵌套循环关联。某些场景哈希关联的效率要高很多。

### SQL执行过程

1. 客户端发送一条查询给服务器。
2. 服务器先检查查询缓存，如果命中了缓存，则立刻返回存储在缓存中的结果。否则进入下一阶段。
3. 服务器进行 SQL 解析、预处理，再由优化器生成对应的执行计划。
4. MySQL 根据优化器生成的执行计划，调用存储引擎的 API 来执行查询。
5. 将结果返回给客户端。
