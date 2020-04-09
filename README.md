## 一、演示简单的MySQL命令，此处示例创建数据库

```
mysql> create database homework;
Query OK, 1 row affected (0.00 sec)

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| homework           |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.00 sec)

```

## 二、创建数据表、修改数据表等（承接上文的SQL代码）

```
mysql> use homework;
Database changed

# 1.创建表格t_dept;


mysql> create table t_dept(
    ->  deptno INT,
    -> dname  VARCHAR(20),
    -> loc    VARCHAR(40)
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> describe t_dept;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| deptno | int(11)     | YES  |     | NULL    |       |
| dname  | varchar(20) | YES  |     | NULL    |       |
| loc    | varchar(40) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

# 2.向表格t_dept中添加字段；

mysql> ALTER TABLE t_dept
    -> ADD descri VARCHAR(20);
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> ALTER TABLE t_dept
    -> ADD descri_head VARCHAR(20) FIRST;
Query OK, 0 rows affected (0.06 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe t_dept;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| descri_head | varchar(20) | YES  |     | NULL    |       |
| deptno      | int(11)     | YES  |     | NULL    |       |
| dname       | varchar(20) | YES  |     | NULL    |       |
| loc         | varchar(40) | YES  |     | NULL    |       |
| descri      | varchar(20) | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

# 3.修改字段数据类型；

mysql> ALTER TABLE t_dept
    -> MODIFY deptno VARCHAR(20);
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe t_dept;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| descri_head | varchar(20) | YES  |     | NULL    |       |
| deptno      | varchar(20) | YES  |     | NULL    |       |
| dname       | varchar(20) | YES  |     | NULL    |       |
| loc         | varchar(40) | YES  |     | NULL    |       |
| descri      | varchar(20) | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

mysql> ALTER TABLE t_dept
    -> MODIFY deptno INT;
Query OK, 0 rows affected (0.07 sec)
Records: 0  Duplicates: 0  Warnings: 0

mysql> describe t_dept;
+-------------+-------------+------+-----+---------+-------+
| Field       | Type        | Null | Key | Default | Extra |
+-------------+-------------+------+-----+---------+-------+
| descri_head | varchar(20) | YES  |     | NULL    |       |
| deptno      | int(11)     | YES  |     | NULL    |       |
| dname       | varchar(20) | YES  |     | NULL    |       |
| loc         | varchar(40) | YES  |     | NULL    |       |
| descri      | varchar(20) | YES  |     | NULL    |       |
+-------------+-------------+------+-----+---------+-------+
5 rows in set (0.00 sec)

# 4.创建表格t_dept2；

mysql> create table t_dept2(
    -> detno INT(20) NOT NULL,
    -> dname VARCHAR(20),
    -> loc VARCHAR(40)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> describe t_dept2;
+--------+-------------+------+-----+---------+-------+
| Field  | Type        | Null | Key | Default | Extra |
+--------+-------------+------+-----+---------+-------+
| deptno | int(20)     | NO   |     | NULL    |       |
| dname  | varchar(20) | YES  |     | NULL    |       |
| loc    | varchar(40) | YES  |     | NULL    |       |
+--------+-------------+------+-----+---------+-------+
3 rows in set (0.00 sec)

# 5.向数据表t_dept和t_dept2中插入数据；

mysql> INSERT INTO t_dept (descri_head, deptno, dname, loc, descri) VALUES ("head", 1, "myName", "Hangzhou", "waha");
Query OK, 1 row affected (0.00 sec)

mysql> INSERT INTO t_dept (descri_head, deptno, dname, loc, descri) VALUES ("head2", NULL, "myName2", "Shanghai", "newPlace");
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM t_dept;
+-------------+--------+---------+----------+----------+
| descri_head | deptno | dname   | loc      | descri   |
+-------------+--------+---------+----------+----------+
| head        |      1 | myName  | Hangzhou | waha     |
| head2       |   NULL | myName2 | Shanghai | newPlace |
+-------------+--------+---------+----------+----------+
2 rows in set (0.00 sec)

mysql> INSERT INTO t_dept2 (deptno, dname, loc) VALUES (1, "myName_t2", "Hangzhou_t2");
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO t_dept2 (deptno, dname, loc) VALUES (NULL, "myName_t2", "Hangzhou_t2");
ERROR 1048 (23000): Column 'deptno' cannot be null（此处因为创建数据表t_dept2时添加了约束detno INT(20) NOT NULL）

mysql> select * FROM t_dept2;
+--------+-----------+-------------+
| deptno | dname     | loc         |
+--------+-----------+-------------+
|      1 | myName_t2 | Hangzhou_t2 |
|      1 | myName_t2 | Hangzhou_t2 |
+--------+-----------+-------------+
2 rows in set (0.00 sec)

# 6.删除表t_dept数据，添加PRIMARY KEY 约束，再插入数据；

mysql> drop table t_dept;
Query OK, 0 rows affected (0.12 sec)

mysql> create table t_dept(
    -> deptno INT(20) PRIMARY KEY AUTO_INCREMENT,
    -> dname VARCHAR(20),
    -> loc VARCHAR(40)
    -> );
Query OK, 0 rows affected (0.03 sec)

mysql> INSERT INTO t_dept (dname, loc) VALUES ("myName_1", "Hangzhou_1");
Query OK, 1 row affected (0.01 sec)

mysql> INSERT INTO t_dept (dname, loc) VALUES ("myName_2", "Hangzhou_2");
Query OK, 1 row affected (0.00 sec)

mysql> SELECT * FROM t_dept;
+--------+----------+------------+
| deptno | dname    | loc        |
+--------+----------+------------+
|      1 | myName_1 | Hangzhou_1 |
|      2 | myName_2 | Hangzhou_2 |
+--------+----------+------------+
2 rows in set (0.00 sec)










