# MYSQL 基础

## 安装MYSQL
Mac OS
1. [下载MYSQL](https://dev.mysql.com/downloads/mysql/)

## 配置 MYSQL 环境变量

## 登陆 MYSQL
``` bash
mysql -uroot -p112233 # 提供用户名和密码
mysql -uroot -p # 未提供密码
mysql -h127.0.0.1 -uroot -p112233 # 提供服务器地址
```

## 启动 MYSQL
* Windows 
    ``` shell
    net start mysql(mysql-name)
    ```
## 停止 MYSQL
* Windows 
    ``` shell
    net stop mysql(mysql-name)
    ```

## 显示所有数据库
``` sql
show databases;
SHOW DATABASES; -- 不区分大小写
```

## 注释
``` sql
show databases; -- 注释内容
show databases; # 单行注释
show databases; /* 多行注释 */
```

## DDL
资料定义语言（data definition language，DDL）属于DBMS语言的一种

## [DML](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E6%93%8D%E7%B8%B1%E8%AA%9E%E8%A8%80)
数据操纵语言（Data Manipulation Language, DML）是用于数据库操作，对数据库其中的对象和资料执行访问工作的编程语句，通常是数据库专用编程语言之中的一个子集，例如在信息软件产业通行标准的SQL语言中，以INSERT、UPDATE、DELETE三种指令为核心，分别代表插入(意指新增或创建)、更新(修改)与删除(销毁)。在使用数据库的系统开发过程中，其中应用程序必然会使用的指令；而加上 SQL的SELECT语句，欧美地区的开发人员把这四种指令，以“CRUD”(分别为 Create, Retrieve, Update, Delete英文四前缀字母缩略的术语)来称呼；而亚洲地区使用汉语的开发人员，或可能以四个汉字：增 查 改 删 来略称。

## [DQL](https://en.wikipedia.org/wiki/Data_query_language)
数据查询语言


## [DCL](https://zh.wikipedia.org/wiki/%E8%B3%87%E6%96%99%E6%8E%A7%E5%88%B6%E8%AA%9E%E8%A8%80)
资料控制语言 (Data Control Language) 在SQL语言中，是一种可对资料访问权进行控制的指令，它可以控制特定用户账户对资料表、查看表、存储程序、用户自定义函数等数据库对象的控制权。由 GRANT 和 REVOKE 两个指令组成。

## CRUD解释
* C: create 创建
* R: retrieve 查询
* U: update 更新
* D: delete 删除

## 创建数据库
``` sql
CREATE DATABASE db;
CREATE DATABASE db1 CHARACTER SET UTF8; # 指定编码
```

## [显示数据库编码](https://stackoverflow.com/questions/1049728/how-do-i-see-what-character-set-a-mysql-database-table-column-is)
``` sql
SELECT default_character_set_name
FROM information_schema.SCHEMATA
WHERE schema_name = "db";
或者
SHOW CREATE DATABASE db;
```

## 切换数据库
``` sql
USE db; # 切换数据库到db
```

## 显示正在使用的数据库
``` sql
SELECT DATABASE();
```

## 显示所有数据库
``` sql
SHOW DATABASES;
```

## 默认数据库的简单介绍

## 修改数据库编码
``` sql
ALTER DATABASE db CHARACTER SET UTF8;
```

## 删除数据库
``` sql
DROP DATABASE db;
```

## 常见数据类型
* int 整形
* double 浮点型
* varchar 字符串类型（可变字符串)
* char 字符串类型(固定长度)

## 创建表
<details>
<summary>例题: 创建用户表(学号，用户名，用户密码)<br/>
</summary>

``` sql
CREATE TABLE user
(
    uid      int,
    username varchar(20),
    password varchar(20)
);
```
</details>

<details>
<summary>例题: 创建用户表(学号，用户名，用户密码，身高，生日)<br/>
</summary>

``` sql
CREATE TABLE user
(
    uid      int,
    username varchar(20),
    password varchar(20),
    height   double,
    birthday date
);
```
</details>

<details>
<summary>例题: 创建和 user 表结构相同的表<br/>
</summary>

``` sql
CREATE TABLE user_like like user;
```
</details>

## 描述表结构
``` sql
DESC user;
```

## 显示所有表
``` sql
SHOW TABLES;
```

## 显示创建表的SQL语句
``` sql
SHOW CREATE TABLE user;
```

## 删除表
``` sql
DROP TABLE user_like; # 永久删除
DROP TABLE if exists user; # 如果存在再删除
```

## 修改表的名字
``` sql
RENAME TABLE user TO new_user;
```

## 修改表的编码
``` sql
ALTER TABLE user CHARACTER SET GBK;
```

## 表添加一列
``` sql
ALTER TABLE user ADD age int; # 添加年龄列
```

## 修改表字段的类型
``` sql
ALTER TABLE user
    MODIFY password CHAR(100);
```

## 修改表字段的名称及类型
``` sql
ALTER TABLE user
    CHANGE uid user_id VARCHAR(20);
```

## 删除表字段
``` sql
ALTER TABLE user
    DROP age;
```