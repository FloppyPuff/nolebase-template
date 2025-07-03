# 分类

| 分类  | 全称                         | 说明                           |
| --- | -------------------------- | ---------------------------- |
| DDL | Data Definition Language   | 数据定义语言，用来定义数据库对象（数据库、表、字段）。  |
| DML | Data Manipulation Language | 数据操作语言，用来对数据库表中的数据进行增删改。     |
| DQL | Data Query Language        | 数据查询语言，用来查询数据库中表的记录。         |
| DCL | Data Control Language      | 数据控制语言，用来创建数据库用户、控制数据库的访问权限。 |

---
## DDL

### DDL-数据库操作

  - **查询**
    - 查询所有数据库
      ```sql
      SHOW DATABASES;
      ```
    - 查询当前数据库
      ```sql
      SELECT DATABASE();
      ```
  - **创建**
    ```sql
    CREATE DATABASE [IF NOT EXISTS] 数据库名 [DEFAULT CHARSET 字符集] [COLLATE 排序规则];
    ```
  - **删除**
    ```sql
    DROP DATABASE [IF EXISTS] 数据库名;
    ```
  - **使用**
    ```sql
    USE 数据库名;
    ```
---

### DDL-表操作-查询
  - **查询当前数据库所有表**
    ```sql
    SHOW TABLES;
    ```
  - **查询表结构**
    ```sql
    DESC 表名;
    ```
  - **查询指定表的建表语句**
    ```sql
    SHOW CREATE TABLE 表名;
    ```
---

### DDL-表操作-创建
```sql
  CREATE TABLE 表名 (
      字段1 字段1类型 [COMMENT 字段1注释],
      字段2 字段2类型 [COMMENT 字段2注释],
      字段3 字段3类型 [COMMENT 字段3注释],
      ...
      字段n 字段n类型 [COMMENT 字段n注释]
  )[COMMENT 表注释];
```

### DDL-表操作-修改

  - **添加字段**
 ```sql
  ALTER TABLE 表名 ADD 字段名 类型(长度) [COMMENT 注释] [约束];
```
  - **修改数据类型**
   ```sql
  ALTER TABLE 表名 MODIFY 字段名 新数据类型(长度);
```
  - **修改字段名和字段类型**
   ```sql
  ALTER TABLE 表名 CHANGE 旧字段名 新字段名 类型(长度) [COMMENT 注释] [约束];
```
  - **删除字段**
```sql
  ALTER TABLE 表名 DROP 字段名;
```
  - **修改表名**
```sql
  ALTER TABLE 表名 RENAME TO 新表名;
```
  - **删除表**
   ```sql
  DROP TABLE [IF EXISTS] 表名;
```
  - **删除指定表，并重新创建该表**
   ```sql
  TRUNCATE TABLE 表名;
```

## DML

### DML-添加数据

1. 给指定字段添加数据
```sql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...);
```
 2. 给全部字段添加数据
```sql
INSERT INTO 表名 VALUES(值1,值2,...);
```
 3. 批量添加数据
```sql
INSERT INTO 表名(字段名1,字段名2,...) VALUES(值1,值2,...),(值1,值2,...),(值1,值2,...);
# 给指定字段添加数据
```

```sql
INSERT INTO 表名 VALUES(值1,值2,...),(值1,值2,...),(值1,值2,...);
# 给所有字段添加数据
```
---
### DML-修改数据

1. 修改数据
```sql
UPDATE 表名 SET 字段名1=值1,字段名2=值2,...[WHERE 条件];
```
---
### DML-删除数据

1. 删除数据
```sql
DELETE FROM 表名 [WHERE 条件];# 若不带WHERE语句，则会删除整张表
```
---

## DQL

### DQL-基本查询

1. 查询多个字段
```sql
SELECT 字段1,字段2,字段3,... FROM 表名;
```

```sql
SELECT * FROM 表名;
```

2. 设置别名
```sql
SELECT 字段1 [AS 别名1],字段2 [AS 别名2],... FROM 表名;
```

3. 去除重复记录
```sql
SELECT DISTINCT 字段列表 FROM 表名;
```

### DQL-条件查询

1. 语法
```sql
SELECT 字段列表 FROM 表名 WHERE 条件列表;
```

2. 条件

| 比较运算符                 | 功能                           |
| --------------------- | ---------------------------- |
| `>`                   | 大于                           |
| `>=`                  | 大于等于                         |
| `<`                   | 小于                           |
| `<=`                  | 小于等于                         |
| `=`                   | 等于                           |
| `<>` 或 `!=`           | 不等于                          |
| `BETWEEN ... AND ...` | 在某个范围之内（含最小值和最大值）            |
| `IN(...)`             | 在 `IN` 之后的列表中的值，多选一          |
| `LIKE`                | 模糊匹配（`_` 匹配单个字符，`%` 匹配任意个字符） |
| `IS NULL`             | 是 `NULL`                     |

| 逻辑运算符        | 功能             |     |
| ------------ | -------------- | --- |
| `AND` 或 `&&` | 并且（多个条件同时成立）   |     |
| `OR` 或  \|\| | 或者（多个条件任意一个成立） |     |
| `NOT` 或 `!`  | 非，不是           |     |

---

### DQL-聚合函数

1. 介绍：将一列数据作为一个整体，进行纵向计算
2. 常见聚合函数

| 函数   | 功能       |
|--------|------------|
| `count` | 统计数量   |
| `max`   | 最大值     |
| `min`   | 最小值     |
| `avg`   | 平均值     |
| `sum`   | 求和       |
3. 语法
```sql
SELECT 聚合函数(字段列表) FROM 表名;# NULL值不参与聚合函数运算
```

### DQL-分组查询

1. 语法
```sql
SELECT 字段列表 FROM 表名 [where 条件] GROUP BY 分组字段名 [HAVING 分组后过滤条件]
```

### DQL-排序查询

1. 语法
```sql
SELECT 字段列表 FROM 表名 ORDER BY 字段1 排序方式1,字段2 排序方式2;
# ASC为升序,DESC为降序
# 如果是多字段排序，当第一个字段值相同时，才会根据第二个字段进行排序
```

### DQL-分页查询

1. 语法
```sql
SELECT 字段列表 FROM 表名 LIMIT 起始索引，查询记录数;
```
2. 注意
   - 起始索引从1开始，起始索引=（查询页码-1）* 每页显示记录数
   - 分页查询是数据库的方言，不同数据库有不同的实现，MySQL中是LIMIT
   - 如果查询的是第一页数据，起始索引可以省略，直接简写为`limit 10`

### DQL-执行顺序

1. 编写顺序：`SELECT -> FROM -> WHERE -> GROUP BY -> HAVING -> ORDER BY -> LIMIT`
2. 执行顺序：`FROM -> WHERE -> GROUP BY -> HAVING -> SELECT -> ORDER BY -> LIMIT`

## DCL

### DCL-管理用户

1. 查询用户
```sql
USE mysql;
SELECT * FROM user;
```
2. 创建用户
```sql
CREATE USER '用户名'@'主机名' IDENTIFIED BY '密码';
```
3. 修改用户密码
```sql
ALTER USER '用户名'@'主机名' IDENTIFIED WITH mysql_native_password BY '新密码';
```
4. 删除用户
```sql
DROP USER '用户名'@'主机名';
```

### DCL-权限控制

MySQL 中定义了很多种权限，但是常用的就以下几种：

|权限|说明|
|---|---|
|`ALL`,`ALL PRIVILEGES`|所有权限|
|`SELECT`|查询数据|
|`INSERT`|插入数据|
|`UPDATE`|修改数据|
|`DELETE`|删除数据|
|`ALTER`|修改表|
|`DROP`|删除数据库/表/视图|
|`CREATE`|创建数据库/表|

1. 查询权限
```sql
SHOW GRANTS FOR '用户名'@'主机名';
```
2. 授予权限
```sql
GRANT 权限列表 ON 数据库名.表名 TO '用户名'@'主机名';
```
3. 撤销权限
```sql
REVOKE 权限列表 ON 数据库名.表名 FROM '用户名'@'主机名';
```
# 数据类型

|  分类  | 类型            | 大小               | 有符号 (SIGNED) 范围                                     | 无符号 (UNSIGNED) 范围                                      | 描述         |
| :--: | ------------- | ---------------- | --------------------------------------------------- | ------------------------------------------------------ | ---------- |
| 数值类型 | TINYINT       | 1 byte           | (-128, 127)                                         | (0, 255)                                               | 小整数值       |
|      | SMALLINT      | 2 bytes          | (-32768, 32767)                                     | (0, 65535)                                             | 大整数值       |
|      | MEDIUMINT     | 3 bytes          | (-8388608, 8388607)                                 | (0, 16777215)                                          | 大整数值       |
|      | INT 或 INTEGER | 4 bytes          | (-2147483648, 2147483647)                           | (0, 4294967295)                                        | 极大整数值      |
|      | BIGINT        | 8 bytes          | (-2^63, 2^63-1)                                     | (0, 2^64-1)                                            | 极大整数值      |
|      | FLOAT         | 4 bytes          | (-3.402823466E+38, 3.402823466351E+38)              | 0 和 (1.175494351E-38, 3.402823466E+38)                 | 单精度浮点数值    |
|      | DOUBLE        | 8 bytes          | (-1.7976931348623157E+308, 1.7976931348623157E+308) | 0 和 (2.2250738585072014E-308, 1.7976931348623157E+308) | 双精度浮点数值    |
|      | DECIMAL       | 依赖于M(精度)和D(标度)的值 | 依赖于M(精度)和D(标度)的值，M为整个数字的长度，D为小数位数                   | 依赖于M(精度)和D(标度)的值                                       | 小数值(精确定点数) |

| 分类       | 类型         | 大小               | 描述                     |
|------------|--------------|--------------------|--------------------------|
| 字符串类型 | CHAR         | 0-255 bytes        | 定长字符串               |
|            | VARCHAR      | 0-65535 bytes      | 变长字符串               |
|            | TINYBLOB     | 0-255 bytes        | 不超过255个字符的二进制数据 |
|            | TINYTEXT     | 0-255 bytes        | 短文本字符串             |
|            | BLOB         | 0-65535 bytes      | 二进制形式的长文本数据   |
|            | TEXT         | 0-65535 bytes      | 长文本数据               |
|            | MEDIUMBLOB   | 0-16777215 bytes   | 二进制形式的中等长度文本数据 |
|            | MEDIUMTEXT   | 0-16777215 bytes   | 中等长度文本数据         |
|            | LONGBLOB     | 0-4294967295 bytes | 二进制形式的极大文本数据 |
|            | LONGTEXT     | 0-4294967295 bytes | 极大文本数据             |

| 分类       | 类型      | 大小 | 范围                          | 格式                | 描述               |
|------------|-----------|------|-------------------------------|---------------------|--------------------|
| 日期类型   | DATE      | 3    | 1000-01-01 至 9999-12-31      | YYYY-MM-DD          | 日期值             |
|            | TIME      | 3    | -838:59:59 至 838:59:59        | HH:MM:SS            | 时间值或持续时间   |
|            | YEAR      | 1    | 1901 至 2155                  | YYYY                | 年份值             |
|            | DATETIME  | 8    | 1000-01-01 00:00:00 至 9999-12-31 23:59:59 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值   |
|            | TIMESTAMP | 4    | 1970-01-01 00:00:01 至 2038-01-19 03:14:07 | YYYY-MM-DD HH:MM:SS | 混合日期和时间值，时间戳 |

---

# 函数

## 字符串函数

| 函数                     | 功能                                                                 |
|--------------------------|----------------------------------------------------------------------|
| `CONCAT(S1, S2, ..., Sn)` | 字符串拼接，将 `S1`, `S2`, ... `Sn` 拼接成一个字符串                          |
| `LOWER(str)`             | 将字符串 `str` 全部转为小写                                              |
| `UPPER(str)`             | 将字符串 `str` 全部转为大写                                              |
| `LPAD(str, n, pad)`      | 左填充，用字符串 `pad` 对 `str` 的左边进行填充，达到 `n` 个字符串长度         |
| `RPAD(str, n, pad)`      | 右填充，用字符串 `pad` 对 `str` 的右边进行填充，达到 `n` 个字符串长度         |
| `TRIM(str)`              | 去掉字符串头部和尾部的空格                                                |
| `SUBSTRING(str, start, len)` | 返回从字符串 `str` 从 `start` 位置起的 `len` 个长度的子字符串               |
示例：
```sql
select concat('hello','mysql');# hellomysql  
select lower('Hello');# hello  
select upper('hello');# HELLO  
select lpad('01',5,'-');# ---01  
select rpad('01',5,'-');# 01---  
select trim(' xxx ');# xxx  
select substr("Hello MySQL",1,5);# Hello
```

## 数值函数

| 函数         | 功能                     |
|--------------|--------------------------|
| `CEIL(x)`    | 向上取整                 |
| `FLOOR(x)`   | 向下取整                 |
| `MOD(x, y)`  | 返回 `x / y` 的模         |
| `RAND()`     | 返回 0~1 内的随机数       |
| `ROUND(x, y)`| 求参数 `x` 的四舍五入的值，保留 `y` 位小数 |
示例：
```sql
select ceil(1.5); # 2  
select floor(1.5); # 1  
select mod(7,4); # 3  
select rand(); # 随机数[0-1)  
select round(2.34,2); # 2.34  
select round(2.345,2); # 2.35
```

## 日期函数

| 函数                                   | 功能                                   |
| ------------------------------------ | ------------------------------------ |
| `CURDATE()`                          | 返回当前日期                               |
| `CURTIME()`                          | 返回当前时间                               |
| `NOW()`                              | 返回当前日期和时间                            |
| `YEAR(date)`                         | 获取指定 `date` 的年份                      |
| `MONTH(date)`                        | 获取指定 `date` 的月份                      |
| `DAY(date)`                          | 获取指定 `date` 的日期                      |
| `DATE_ADD(date, INTERVAL expr_type)` | 返回一个日期/时间值加上一个时间间隔 `expr_type` 后的时间值 |
| `DATEDIFF(date1, date2)`             | 返回起始时间 `date1` 和结束时间 `date2` 之间的天数   |
示例：
```sql
select curdate(); # 2025-06-05  
select curtime(); # 17:01:18  
select now(); # 2025-06-05 17:01:38  
select year(now()); # 2025  
select month(now()); # 6  
select day(now()); # 5 
select date_add(now(),interval 70 day); # 2025-08-14 17:03:30  
select date_add(now(),interval 70 month); # 2031-04-05 17:04:22  
select date_add(now(),interval 70 year); # 2095-06-05 17:04:47  
select datediff('2021-12-01','2021-11-01');# 30  
select datediff('2021-12-01','2021-10-01'); # 61  
select datediff('2021-10-01','2021-12-01'); # -61
```

## 流程函数

| 函数                                                           | 功能                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------ |
| `IF(value, t, f)`                                            | 如果 `value` 为 `true`，则返回 `t`；否则返回 `f`                   |
| `IFNULL(value1, value2)`                                     | 如果 `value1` 不为空，则返回 `value1`；否则返回 `value2`             |
| `CASE WHEN [val1] THEN [res1] ... ELSE [default] END`        | 如果 `val1` 为 `true`，返回 `res1`；... 否则返回 `default` 默认值    |
| `CASE [expr] WHEN [val1] THEN [res1] ... ELSE [default] END` | 如果 `expr` 的值等于 `val1`，返回 `res1`；... 否则返回 `default` 默认值 |
示例：
```sql
select if (true,'ok','error'); # ok  
select ifnull('ok','default'); # ok
```

# 约束

## 概念

- 约束是作用于表中字段上的规则，用于限制存储在表中的数据

## 目的

- 保证数据库中数据的正确性、有效性和完整性

## 分类

| 约束       | 描述                                                                 | 关键字      |
|------------|----------------------------------------------------------------------|-------------|
| 非空约束   | 限制该字段的数据不能为 `NULL`                                           | `NOT NULL`  |
| 唯一约束   | 保证该字段的所有数据都是唯一、不重复的                                   | `UNIQUE`    |
| 主键约束   | 主键是一行数据的唯一标识，要求非空且唯一                                 | `PRIMARY KEY` |
| 默认约束   | 保存数据时，如果未指定该字段的值，则采用默认值                             | `DEFAULT`   |
| 检查约束（8.0.16 版本之后） | 保证字段值满足某一个条件                                         | `CHECK`     |
| 外键约束   | 用来让两张表的数据之间建立连接，保证数据的一致性和完整性                   | `FOREIGN KEY` |

示例：
```sql
create table user(  
    id int primary key auto_increment comment '主键',  #主键且自增
    name varchar(10) not null unique comment '姓名',  #非空且不能重复
    age int check ( age>=0 and age<=120 ) comment '年龄',  #年龄范围受check限制
    status char(1) default '1' comment '状态',  #默认为1
    gender char(1) comment '性别'  
) comment '用户表';
```

### 外键约束

- 语法
```sql
CREATE TABLE 表名 (
    字段名 数据类型,
    ...
    [CONSTRAINT] [外键名称] FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名)
);
```

```sql
ALTER TABLE 表名 ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段名) REFERENCES 主表 (主表列名);
```

```sql
ALTER TABLE 表名 DROP FOREIGN KEY 外键名称;
```

- 删除/更新行为

| 行为            | 说明                                                                    |
| ------------- | --------------------------------------------------------------------- |
| `NO ACTION`   | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与 `RESTRICT` 一致）         |
| `RESTRICT`    | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有则不允许删除/更新。（与 `NO ACTION` 一致）        |
| `CASCADE`     | 当在父表中删除/更新对应记录时，首先检查该记录是否有对应外键，如果有，则也删除/更新外键在子表中的记录。                  |
| `SET NULL`    | 当在父表中删除对应记录时，首先检查该记录是否有对应外键，如果有则设置子表中该外键值为 `NULL`（这就要求该外键允许取 `NULL`）。 |
| `SET DEFAULT` | 父表有变更时，子表将外键列设置成一个默认的值。（InnoDB 不支持）                                   |

示例：

```sql
ALTER TABLE 表名 
ADD CONSTRAINT 外键名称 FOREIGN KEY (外键字段) 
REFERENCES 主表名 (主表字段名) 
ON UPDATE CASCADE ON DELETE CASCADE;
```

# 多表查询

## 多表关系
1. 多对多
- 案例：学生与课程的关系
- 关系：一个学生可以选修多门课程，一门课程也可以供多个学生选择
- 实现：建立第三张中间表，中间表至少包含两个外键，分别关联两方主键

示例：
```sql
CREATE TABLE student (  
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '主键ID',  
    name VARCHAR(18) COMMENT '姓名',  
    no VARCHAR(10) COMMENT '学号'  
) COMMENT '学生表';  
  
CREATE TABLE course (  
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '主键ID',  
    name VARCHAR(18) COMMENT '课程名称'  
) COMMENT '课程表';  
  
INSERT INTO course VALUES (NULL, 'Java'), (NULL, 'PHP'), (NULL, 'MySQL'), (NULL, 'Hadoop');  
  
INSERT INTO student VALUES (NULL, '席绮丝', '2006108101'), (NULL, '谢道', '2006108102'), (NULL, '殷天正', '2006108103');  
  
CREATE TABLE Student_course (  
    id INT PRIMARY KEY AUTO_INCREMENT  comment '主键',  
    studentid INT NOT NULL COMMENT '学生ID',  
    courseid INT NOT NULL COMMENT '课程ID',  
    CONSTRAINT fk_courseid FOREIGN KEY (courseid) REFERENCES course (id),  
    CONSTRAINT fk_studentid FOREIGN KEY (studentid) REFERENCES student (id)  
) COMMENT '学生课程中间表';  
  
INSERT INTO student_course VALUES (NULL, 1, 1), (NULL, 1, 2), (NULL, 1, 3), (NULL, 2, 2), (NULL, 2, 3), (NULL, 3, 4);
```

2. 一对一
- 案例：用户与用户详情的关系
- 关系：一对一关系，多用于单表拆分，将一张表的基础字段放在一张表中，其他详情字段放在另一张表中，以提升效率
- 实现：在任意一方加入外键，关联另外一方的主键，并且设置外键为唯一的(UNIQUE)
示例：
```sql
create table tb_user(  
    id int auto_increment primary key comment '主键ID',  
    name varchar(10) comment '姓名',  
    age int comment '年龄',  
    gender char(1) comment '性别',  
    phone char(11) comment '手机号'  
) comment '用户基本信息表';  
  
CREATE TABLE tb_user_edu (  
    id INT AUTO_INCREMENT PRIMARY KEY COMMENT '主键ID',  
    degree VARCHAR(20) COMMENT '学历',  
    major VARCHAR(50) COMMENT '专业',  
    primaryschool VARCHAR(50) COMMENT '小学',  
    middleschool VARCHAR(50) COMMENT '中学',  
    university VARCHAR(50) COMMENT '大学',  
    userid INT UNIQUE COMMENT '用户ID',  
    CONSTRAINT fk_userid FOREIGN KEY (userid) REFERENCES tb_user(id)  
) COMMENT '用户教育信息表';  
  
INSERT INTO tb_user (id, name, age, gender, phone) VALUES  
(NULL, '黄渤', 45, '1', '18888881111'),  
(NULL, '冰冰', 35, '2', '18898982222'),  
(NULL, '码云', 55, '1', '18888888888'),  
(NULL, '李彦宏', 50, '1', '18888889999');  
  
INSERT INTO tb_user_edu (id, degree, major, primaryschool, middleschool, university, userid) VALUES  
(NULL, '本科', '舞蹈', '静安区第一小学', '静安区第一中学', '北京舞蹈学院', 1),  
(NULL, '硕士', '表演', '朝阳区第一小学', '朝阳区第一中学', '北京电影学院', 2),  
(NULL, '本科', '英语', '杭州市第一小学', '杭州市第一中学', '杭州师范大学', 3),  
(NULL, '本科', '应用数学', '阳泉第一小学', '阳泉市第一中学', '清华大学', 4);
```

## 多表查询

### 分类

- 连接查询
  1. 内连接：相当于查询A、B交集部分数据
  2. 外连接：
     - 左外连接：查询左表数据，以及两张表交集部分数据
     - 右外连接：查询右表数据，以及两张表交集部分数据
  3. 自连接：当前表与自身的连接查询，自连接必须使用表别名
- 子查询

#### 内连接

1. 隐式内连接：
```sql
SELECT 字段列表 FROM 表1,表2 WHERE 条件;
```
2. 显式内连接：
```sql
SELECT 字段列表 FROM 表1 [INNER] JOIN 表2 ON 连接条件;
```

#### 外连接

1. 左外连接
```sql
SELECT 字段列表 FROM 表1 LEFT [OUTER] JOIN 表2 ON 条件;
```
2. 右外连接
```sql
SELECT 字段列表 FROM 表1 RIGHT [OUTER] JOIN 表2 ON 条件：
```

#### 自连接

1. 语法
```sql
SELECT 字段列表 FROM 表A 别名A JOIN 表A 别名B ON 条件;
```

#### 联合查询

```sql
select * from emp where salary < 5000
union [all] # 使用all不会去重，不使用all会去重
select * from emp where age > 50;
```

对于联合查询的多张表的列数不需保持一致，字段类型也需保持一致

#### 子查询

- 概念：SQL语句中嵌套`select`语句，成为嵌套查询，又称子查询
- 根据子查询结果不同，分为：
  1. 标量子查询（子查询结果为单个值）
  2. 列子查询（子查询结果为一列）
  3. 行子查询（子查询结果为一行）
  4. 表子查询（子查询结果为多行多列）
- 根据子查询位置，分为：`where`之后、`from`之后、`select`之后

##### 标量子查询

- 常用操作符：`=` `<>` `>` `>=` `<` `<=`
```sql
select * from emp where dept_id = (select id from dept where name = '销售部');
```

##### 列子查询

- 常用操作符：`in` `not in` `any` `some` `all`
```sql
select  emp.salary from emp where dept_id = (select id from dept where name = '财务部');  
  
select * from emp where salary > all (select  emp.salary from emp where dept_id = (select id from dept where name = '财务部'));  # 大于所有的
  
select  emp.salary from emp where dept_id = (select id from dept where name = '研发部');  
  
select * from emp where salary > any(select  emp.salary from emp where dept_id = (select id from dept where name = '研发部')); # 大于任意一个
```

##### 行子查询

- 常用操作符：`=` `<>` `in` `not in`
```sql
select * from emp where (salary,managerid) = (select salary,emp.managerid from emp where name = '张无忌');
```

##### 表子查询

- 常用操作符：`in`
```sql
select e.*,d.* from (select * from emp where entrydate > '2006-01-01') e , dept d on e.dept_id = d.id;
```

# 事务

## 简介

事务是一组操作的集合，它是一个不可分割的工作单位，事务会把所有的操作作为一个整体一起向系统提交或撤销操作请求，即这些操作要么同时成功，要么同时失效

## 事务操作

1. 查询是否自动提交事务
```sql
select @@autocommit;
```
2. 修改是否自动提交事务
```sql
set @@autocommit = 0; # 0为手动提交，1为自动提交
```
3. 提交事务
```sql
commit;
```
4. 回滚事务
```sql
rollback;
```
5. 手动开启事务
```sql
start transaction;
```

```sql
begin;
```

## 事务四大特性

**ACID**：
- **原子性（Atomicity）**：事务是一个不可分割的最小工作单位，事务中的操作要么都成功，要么都失败。
- **一致性（Consistency）**：事务执行前后，数据库的完整性约束必须保持不变，即合法状态 → 合法状态。
- **隔离性（Isolation）**：多个事务并发执行时，彼此隔离互不干扰，看起来像是串行执行。
- **持久性（Durability）**：事务一旦提交，其对数据库的修改就是永久性的，即使系统崩溃也不会丢失。

## 并发事务问题

| 问题    | 描述                                                                 |
| ----- | ------------------------------------------------------------------ |
| 脏读    | 一个事务读到了另一个未提交事务的数据。                                                |
| 不可重复读 | 同一个事务内多次读取同一条记录，结果不一样（因为其他事务对该行进行了 UPDATE 或 DELETE）。               |
| 幻读    | 同一个事务中两次范围查询（如 SELECT ... WHERE age > 30），结果集数量不同（新增或删除了符合查询条件的行）。 |
## 事务隔离级别

| 隔离级别                | 脏读  | 不可重复读 | 幻读  |
| ------------------- | --- | ----- | --- |
| Read uncommitted    | √   | √     | √   |
| Read committed      | ×   | √     | √   |
| Repeatable Read（默认） | ×   | ×     | √   |
| Serializable        | ×   | ×     | ×   |
- 在最新的MySQL中，`Repeatable Read`解决了幻读问题

1. 查看事务隔离级别
```sql
select @@transaction_isolation
```
2. 设置事务隔离级别
```sql
set [session | global] transaction isolation level [read uncommitted | read committed | repeatable read | serializable]
```

# 索引

## 建立索引

```sql
create index 索引名 on 表名(字段名);
```

![[Pasted image 20250616212152.png]]
## 结构

![[Pasted image 20250616212322.png]]

- B+Tree(多路平衡搜索树)
![[Pasted image 20250616212900.png]]

## 语法

![[Pasted image 20250616213739.png]]

![[Pasted image 20250616213744.png]]

