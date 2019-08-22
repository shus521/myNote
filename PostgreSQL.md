[TOC]
## 库
### 新建数据库
1. 普通的sql语法`create database test`;
2. 进入到bin目录执行`createdb -h localhost -p 5432 -U postgres runoobdb`
### 删除数据库
1.
 ~~~
DROP DATABASE [ IF EXISTS ] name
~~~
DROP DATABASE 会删除数据库的系统目录项并且删除包含数据的文件目录。
DROP DATABASE 只能由超级管理员或数据库拥有者执行。
2. 进入bin目录执行`dropdb -h localhost -p 5432 -U postgres runoobdb`
*****
1. 查看数据库列表`\l`
2. 进入数据库`\c test`
## 表
### 创建表
~~~
    CREATE TABLE table_name(
       column1 datatype,
       column2 datatype,
       column3 datatype,
       .....
       columnN datatype,
       PRIMARY KEY( 一个或多个列 )
    );
~~~
### 删除表
`DROP TABLE table_name;`
*****
1. 查看表`\d`
2. 查看表信息`\d tablename`
3. 列出表中所有索引`\di`
## 模式(SCHEMA)
### 说明
可以看成是表的集合，可以包含视图、索引、据类型、函数和操作符等
**相同的对象名称可以被用于不同的模式中而不会出现冲突，例如 schema1 和 myschema 都可以包含名为 mytable 的表**
### 语法
~~~
CREATE TABLE myschema.mytable (
...
);
~~~
### 删除
删除空的模式`DROP SCHEMA myschema;`
删除一个模式以及其中包含的所有对象：`DROP SCHEMA myschema CASCADE;`
## curd
**基本sql与其他数据库类似**
### insert
1. insert可插入`DEFAULT`则插入默认值
### 从某行开始取几条
`SELECT * FROM COMPANY LIMIT 3 OFFSET 2;`
### group
在 GROUP BY 子句中，你可以对一列或者多列进行分组，但是被分组的列必须存在于列清单中(mysql对此不严格要求，但是建议按此标准)或者为聚合值(min等)
### 通用表达式WITH语句(CTE)
~~~
    WITH
       name_for_summary_data AS (
          SELECT Statement)
       SELECT columns
       FROM name_for_summary_data
       WHERE conditions <=> (
          SELECT column
          FROM name_for_summary_data)
       [ORDER BY columns]
~~~
1. name_for_summary_data可以与现有的表名相同，并且具有优先级
2. 可以在 WITH 中使用数据 INSERT, UPDATE 或 DELETE 语句，允许您在同一个查询中执行多个不同的操作
3. 在 WITH 子句中可以使用自身输出的数据
#### 递归
```
    with RECURSIVE cte as ( 
            select a.id,a.name,a.pid from tb a where id='002' 
            union all  
            select k.id,k.name,k.pid  from tb k inner join cte c on c.id = k.pid 
    )select id,name from cte;
```
#### 删除并插入
```
    WITH moved_rows AS (
       DELETE FROM COMPANY
       WHERE
          SALARY >= 30000
       RETURNING *
    )
    INSERT INTO COMPANY1 (SELECT * FROM moved_rows);
```
### HAVING
1. HAVING 子句必须放置于 GROUP BY 子句后面，ORDER BY 子句前面
## 约束
NOT NULL、UNIQUE、PRIMARY KEY、FOREIGN KEY
### CHECK约束
~~~
    CREATE TABLE COMPANY5(
       ID INT PRIMARY KEY     NOT NULL,
       NAME           TEXT    NOT NULL,
       AGE            INT     NOT NULL,
       ADDRESS        CHAR(50),
       SALARY         REAL    CHECK(SALARY > 0)
    );
~~~
### EXCLUSION 约束
EXCLUSION 约束确保如果使用指定的运算符在指定列或表达式上比较任意两行，至少其中一个运算符比较将返回 false 或 null。
## 索引
*   索引不应该使用在较小的表上。
*   索引不应该使用在有频繁的大批量的更新或插入操作的表上。
*   索引不应该使用在含有大量的 NULL 值的列上。
*   索引不应该使用在频繁操作的列上
****
1. TRUNCATE TABLE 与 DELETE 具有相同的效果，但是由于它实际上并不扫描表，所以速度更快。 此外，TRUNCATE TABLE 可以立即释放表空间，而不需要后续 VACUUM 操作，这在大型表上非常有用。
