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

![](https://github.com/spicychicken9/-/blob/master/1.png)

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

![](https://github.com/spicychicken9/-/blob/master/2.png)

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

![](https://github.com/spicychicken9/-/blob/master/3.png)

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

![](https://github.com/spicychicken9/-/blob/master/4.png)

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

![](https://github.com/spicychicken9/-/blob/master/5.png)

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

mysql> show tables;
+--------------------+
| Tables_in_homework |
+--------------------+
| t_dept             |
| t_dept2            |
+--------------------+
2 rows in set (0.00 sec)

![](https://github.com/spicychicken9/-/blob/master/6.png)

```

## 三、演示老师上课时进行的命令

```

mysql>  create table t_employee(
    ->     deptno INT NOT NULL,
    -> empno INT  PRIMARY KEY,
    -> ename VARCHAR(20),
    -> job  VARCHAR(20),
    ->     MGR  INT,
    -> Hiredate Date,
    -> sal    float,
    -> comm   float
    -> );
Query OK, 0 rows affected (0.04 sec)

mysql> INSERT INTO t_employee(empno, ename, job, MGR, Hiredate, sal, comm, deptno) VALUES
    ->     (7369, "SMITH", "CLERK", 7902, "1981-03-12", 800.00, NULL, 20),
    -> (7499, "ALLEN", "SALESMAN", 7698, "1982-03-12", 1600, 300, 30),
    -> (7521, "WARD", "SALESMAN", 7698, "1838-03-12", 1250, 500, 30),
    -> (7566, "JONES", "MANAGER", 7839, "1981-03-12", 2975, NULL, 20),
    -> (7654, "MARTIN", "SALESMAN", 7698, "1981-01-12", 1250, 1400, 30),
    -> (7698, "BLAKE", "MANAGER", 7839, "1985-03-12", 2450, NULL, 10),
    -> (7788, "SCOTT", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7839, "KING", "PRESIDENT", NULL, "1981-03-12", 5000, NULL, 10),
    -> (7844, "TURNER", "SALESMAN", 7689, "1981-03-12", 1500, 0, 30),
    -> (7878, "ADAMS", "CLERK", 7788, "1981-03-12", 1100, NULL,20),
    -> (7900, "JAMES", "CLERK", 7698,"1981-03-12",  950, NULL, 30),
    -> (7902, "FORD", "ANALYST", 7566, "1981-03-12", 3000, NULL, 20),
    -> (7934, "MILLER", "CLERK", 7782, "1981-03-12", 1300, NULL, 10)
    -> ;
Query OK, 13 rows affected (0.00 sec)
Records: 13  Duplicates: 0  Warnings: 0

mysql> DROP TABLE IF EXISTS t_dept;
Query OK, 0 rows affected (0.01 sec)

mysql> CREATE TABLE t_dept (
    ->     deptno INT PRIMARY KEY,
    -> dname VARCHAR(30),
    -> loc VARCHAR(50)
    -> );
Query OK, 0 rows affected (0.05 sec)

mysql> INSERT INTO t_dept VALUES
    -> (10, "ACCOUNTING", "NEW YORK"),
    -> (20, "RESEARCH", "DALLAS"),
    -> (30, "SALES", "CHICAGO"),
    -> (40, "OPERATIONS", "BOSTON")
    -> ;
Query OK, 4 rows affected (0.01 sec)
Records: 4  Duplicates: 0  Warnings: 0

mysql> select *
    -> from t_employee t1 inner join t_employee t2
    -> on t1.empno = t2.mgr;
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
| deptno | empno | ename | job       | MGR  | Hiredate   | sal  | comm | deptno | empno | ename  | job      | MGR  | Hiredate   | sal  | comm |
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
|     20 |  7902 | FORD  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7369 | SMITH  | CLERK    | 7902 | 1981-03-12 |  800 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7499 | ALLEN  | SALESMAN | 7698 | 1982-03-12 | 1600 |  300 |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7521 | WARD   | SALESMAN | 7698 | 1838-03-12 | 1250 |  500 |
|     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |     20 |  7566 | JONES  | MANAGER  | 7839 | 1981-03-12 | 2975 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7654 | MARTIN | SALESMAN | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |     10 |  7698 | BLAKE  | MANAGER  | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |     20 |  7788 | SCOTT  | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |
|     20 |  7788 | SCOTT | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7878 | ADAMS  | CLERK    | 7788 | 1981-03-12 | 1100 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7900 | JAMES  | CLERK    | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |     20 |  7902 | FORD   | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
10 rows in set (0.00 sec)

mysql> select * from t_employee t1 inner join t_employee t2 on t1.empno = t2.mgr;
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
| deptno | empno | ename | job       | MGR  | Hiredate   | sal  | comm | deptno | empno | ename  | job      | MGR  | Hiredate   | sal  | comm |
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
|     20 |  7902 | FORD  | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7369 | SMITH  | CLERK    | 7902 | 1981-03-12 |  800 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7499 | ALLEN  | SALESMAN | 7698 | 1982-03-12 | 1600 |  300 |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7521 | WARD   | SALESMAN | 7698 | 1838-03-12 | 1250 |  500 |
|     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |     20 |  7566 | JONES  | MANAGER  | 7839 | 1981-03-12 | 2975 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7654 | MARTIN | SALESMAN | 7698 | 1981-01-12 | 1250 | 1400 |
|     10 |  7839 | KING  | PRESIDENT | NULL | 1981-03-12 | 5000 | NULL |     10 |  7698 | BLAKE  | MANAGER  | 7839 | 1985-03-12 | 2450 | NULL |
|     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |     20 |  7788 | SCOTT  | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |
|     20 |  7788 | SCOTT | ANALYST   | 7566 | 1981-03-12 | 3000 | NULL |     20 |  7878 | ADAMS  | CLERK    | 7788 | 1981-03-12 | 1100 | NULL |
|     10 |  7698 | BLAKE | MANAGER   | 7839 | 1985-03-12 | 2450 | NULL |     30 |  7900 | JAMES  | CLERK    | 7698 | 1981-03-12 |  950 | NULL |
|     20 |  7566 | JONES | MANAGER   | 7839 | 1981-03-12 | 2975 | NULL |     20 |  7902 | FORD   | ANALYST  | 7566 | 1981-03-12 | 3000 | NULL |
+--------+-------+-------+-----------+------+------------+------+------+--------+-------+--------+----------+------+------------+------+------+
10 rows in set (0.00 sec)


```

![](https://github.com/spicychicken9/-/blob/master/7.png)

## 四、用join完成查询

## 五、运行演示的存储过程和函数

```

mysql> DELIMITER $$
mysql> CREATE PROCEDURE proce_employee_sal1 ()
    -> BEGIN
    ->     SELECT sal
    -> FROM t_employee;
    -> END$$
Query OK, 0 rows affected (0.00 sec)

mysql> DELIMITER ;
mysql> CALL proce_employee_sal1();
+------+
| sal  |
+------+
|  800 |
| 1600 |
| 1250 |
| 2975 |
| 1250 |
| 2450 |
| 3000 |
| 5000 |
| 1500 |
| 1100 |
|  950 |
| 3000 |
| 1300 |
+------+
13 rows in set (0.01 sec)

Query OK, 0 rows affected (0.10 sec)

mysql>
mysql> DELIMITER $$
mysql> CREATE FUNCTION func_employee_sal (empno INT)
    -> RETURNS DOUBLE
    -> BEGIN
    ->     RETURN (SELECT sal FROM t_employee WHERE t_employee.empno = empno);
    -> END$$
Query OK, 0 rows affected (0.00 sec)

mysql> DELIMITER ;
mysql> SELECT func_employee_sal(7369);
+-------------------------+
| func_employee_sal(7369) |
+-------------------------+
|                     800 |
+-------------------------+
1 row in set (0.00 sec)

```

![](https://github.com/spicychicken9/-/blob/master/8.png)












