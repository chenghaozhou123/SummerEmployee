封锁粒度：

## 封锁粒度

封锁对象的大小称为封锁粒度(Granularity)

封锁的对象：逻辑单元，物理单元

例：在关系数据库中，封锁对象：

[逻辑单元](https://baike.baidu.com/item/逻辑单元): 属性值、属性值集合、元组、关系、索引项、整个索引、整个数据库等

物理单元：页（数据页或索引页）、物理记录等

封锁粒度与系统的并发度和并发控制的开销密切相关。

封锁的粒度越大，数据库所能够封锁的数据单元就越少，并发度就越小，系统开销也越小；

封锁的粒度越小，并发度较高，但系统开销也就越大 

# 幻读（对这个有点没懂，记录下）

可重复读的时候，读会加上x锁，这样保证了读取单条数据的一致性。

而幻读这个现象针对的是多行数据。

当select条件读取时，给满足条件的行加了写锁，这些数据是其他事务无法修改，但是当其他事务插入一条符合搜索条件的数据，再执行相同的读操作就会和之前的结果不一样，这就是幻读的 现象。

解决方法:看一下是否正确

![image-20220713172658435](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20220713172658435.png)

#### 可串行化是怎样来解决幻读的呢？

select * from table where id < 3

 可串行化隔离在每次访问记录的的时候（无论读写）都会加锁。innodb串行化的读不会锁表，而是根据where锁一个范围。

https://www.zhihu.com/question/437140633/answers/updated

#### 什么时候释放锁以及两段锁协议

一般是在事务中执行完相关的语句就会释放锁了。

两段锁协议让加锁和解锁分为两个阶段执行。一个事务中一旦释放了锁就不能再申请锁。

可串行化是通过并发控制，使得并发执行的事务结果与串行执行的事务结果相同。遵循两段锁协议是保证可串行化调度的充分条件。



# 为什么走索引速度快

索引会帮助我们快速检索数据库，查询不需要通过整个表来获取数据，而是从索引中找到数据块。如果数据无序，需要查找整个数据，这带来的开销是很大的。

建立了索引的数据，就是通过事先排好序，从而在查找时可以应用二分查找来提高查询效率。这也解释了为什么索引应当尽可能的建立在主键这样的字段上，因为主键必须是唯一的，根据这样的字段生成的二叉查找树的效率无疑是最高的。



# MVCC如何解决一致性读



# 互斥锁的实现原理



# **Socket** 

Socket(套接字)可以看成是两个网络应用程序进行通信时，各自通信连接中的端点。

使用中的每一个套接字都有其类型和一个与之相连进程。通信时其中一个网络应用程序将要传输的一段信息写入它所在主机的 Socket中，该 Socket通过与[网络接口卡](https://baike.baidu.com/item/网络接口卡/9764230)(NIC)相连的传输介质将这段信息送到另外一台主机的 Socket中，使对方能够接收到这段信息。 Socket是由IP地址和端口结合的，提供向应用层进程传送数据包的机制

# zero拷贝





- 据库基础

  

  -  [事务的概念和特性？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#事务的概念和特性)
  - [会出现哪些并发一致性问题？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#会出现哪些并发一致性问题)
  - [数据库的四种隔离级别？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#数据库的四种隔离级别)
  - [什么是乐观锁和悲观锁？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是乐观锁和悲观锁)
  - [常见的封锁类型？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#常见的封锁类型)
  - [什么是三级封锁协议？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是三级封锁协议)
  - [什么是两段锁协议？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是两段锁协议)
  - [什么是 MVCC？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是-mvcc)
  - [数据库的范式？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#数据库的范式)
  - [列举几种表连接方式？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#列举几种表连接方式)
  - [什么是存储过程？有哪些优缺点？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是存储过程有哪些优缺点)
  - [Drop/Delete/Truncate的区别？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#DropDeleteTruncate的区别)
  - [什么是视图？什么是游标？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是视图什么是游标)

- MySQL

  - [数据库索引的实现原理（B+树）](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#数据库索引的实现原理b树)
  - [使用索引的优点](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#使用索引的优点)
  - [哪些情况下索引会失效？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#哪些情况下索引会失效)
  - [在哪些地方适合创建索引？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#在哪些地方适合创建索引)
  - [索引的分类？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#索引的分类)
  - [MySQL的两种存储引擎 InnoDB 和 MyISAM 的区别？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#MySQL的两种存储引擎-InnoDB-和-MyISAM-的区别)
  - [如何优化数据库？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#如何优化数据库)
  - [什么是主从复制？实现原理是什么？](https://github.com/wolverinn/Waking-Up/blob/master/Database.md#什么是主从复制实现原理是什么)

- NoSQL/Redis

  - [关系型数据库和非关系型数据库的区别？](https://github.com/wolverinn/Waking-Up/blob/master/关系型数据库和非关系型数据库的区别)

基于undo_log 版本链

持久性 redo_log 原子性undo_log

# 为什么用clickhouse而不用mysql

clickhouse不适合处理数据频繁修改和删除操作，对于删除和修改会消耗大量的性能。数据写入、修改、删除都是异步的，对于数据要及时查询不适合clickhouse，并且不支持事务，所以不用于数据一致性较高的场景。

clickhouse适用于OLAP（在线分析处理），列式存储，内部存储采用稀疏。

# 同一个事务下可以update两次相同的数据吗

隔离级别只是隔离不同事务间的数据可见性和操作性，在同一个事务中是可以做连续修改操作的。

# 在复习下kafuka 还有项目





# SQL常考语句

按数学成绩排序

xxxxxxxxxx 'Con_Forecast_Stk',Fin_Performance_Forecast Fin_Performance_Express[2022-08-29 09:49:15,556] [ERROR] Con_Forecast_Stk on 2022-08-26 00:00:00 daily_save error: 字段con_eps_hisdate 数据格式为<class 'pandas._libs.tslibs.nattype.NaTType'>，protobuf序列化无法解析,expect: int, float, bool, str,datetime​python

降序排序

SELECT * FROM STUDENT ORDER BY MATH DESC；

按数学成绩排名，若一样则按英语排名

SELECT * FROM STUDENT ORDER BY MATH ASC , ENGLISH DESC;

查询有多少人

SELECT COUNT(ENGLISH) FROM STUDENT;  聚合函数计算会忽略null值，解决方案如下

SELECT COUNT(IFNULL(ENGLISH, 0) ) FROM STUDENT;

SELECT COUNT() FROM STUDENT;

– 计算数学成绩最大值,最小值,平均值，求和

SELECT MAX(math) FROM student;

SELECT MIN(math) FROM student;

SELECT AVG(math) FROM student;

SELECT SUM(math) FROM student;

– 分别计算男同学和女同学的平均分,人数

SELECT sex,AVG(score),COUNT(name) FROM student GROUP BY sex;

分别计算男同学和女同学的平均分，人数，分数低于70的不参与分组

SELECT sex,AVG(score),COUNT(name) FROM student WHERE math > 70 GROUP BY sex;

– 分别计算男同学和女同学的平均分,人数,分数低于70不参与分组,分组之后人数要大于2的

SELECT sex,AVG(math) , COUNT(NAME) FROM student WHERE math > 70 GROUP BY sex HAVING COUNT(id) > 2;
– 每页显示3条记录

SELECT * FROM student LIMIT 0,3;

– 创建表添加非空约束

CREATE TABLE stu(

id INT;

NAME VARCHAR(20) NOT NULL;

);