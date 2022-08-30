创建一个数据库：

CREATE DATABASE IF NOT EXISTS helloworld

创建一个表：

每个表需要指定表引擎。

CREATE TABLE helloworld.my_first_table
(
    user_id UInt32,
    message String,
    timestamp DateTime,
    metric Float32
)
ENGINE = MergeTree()
PRIMARY KEY (user_id, timestamp)

### clickhouse中的主键（primary keys）

**不是独一无二的**

主键决定了如何对数据进行排序，上面案例中就是user_id,再timestamp。

## Insert Data

INSERT INTO helloworld.my_first_table (user_id, message, timestamp, metric) VALUES
    (101, 'Hello, ClickHouse!',                                 now(),       -1.0    ),
    (102, 'Insert a lot of rows per batch',                     yesterday(), 1.41421 ),
    (102, 'Sort your data based on your commonly-used queries', today(),     2.718   ),
    (101, 'Granules are the smallest chunks of data read',      now() + 5,   3.14159 )



## Insert a CSV file

```sql
clickhouse-client \
--query='INSERT INTO helloworld.my_first_table FORMAT CSV' < data.csv


```

