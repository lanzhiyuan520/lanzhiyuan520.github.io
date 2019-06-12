---
layout: 兰志远
title: mysql常用命令
date: 2019-03-15 17:39:26
tags: mysql
type: "tags"
---
#### myslq常用命令

mysql登录

```mysql
mysql -h localhost -P3306 -u root -ppass;
参数：
	h : 主机名  P : 端口号 u : 用户名 p : 密码
```

修改数据库登录密码

```mysql
alter user '用户名'@'localhost' DENTIFIED BY '新密码';
```

查看所有数据库

```mysql
show databases;
```

查看所有表

```mysql
show tables;
```

创建表

```mysql
create table 表名(字段名 字段类型,字段名 字段类型);
```

查看表结构

```mysql
desc table_name;
```

切换数据库

```mysql
use 库名;
```

查看当前所在数据库

```mysql
select database();
```

查看表所有数据

```mysql
select * from table_name;
```

创建数据库

```mysql
create database test;
```

清空表数据

```mysql
truncate test;
```

mysql端口查询

```mysql
sudo netstat -anp | grep mysql
```

简单分页查询

```mysql
select * from table limit(page-1)*size,size;
/*page : 当前页数*/
/*size : 每页的数量*/
/*语法*/
select * from 表名 limit 起始索引,查询个数;
```

like操作符

```mysql
select * from user where name like '小%';
/*查询user表 name字段 以小开头的数据*/
select * from user where name like '%小%';
/*查询user表 name字段 包含小的数据*/
select * from user where name like '%小';
/*查询user表 name字段 以小结尾的数据*/
```

not like操作符

```mysql
select * from user where name not like '小%';
/*查询user表 name字段 不是以小开头的数据*/
```

IN操作符

```mysql
select * from user where name IN('小红','小紫');
/*从user表查询 name字段为IN里边的值*/
```

or运算符

```mysql
select * from user where score>80 or gender='女';
/*从user表查询 score大于80或者gender=女的数据，任意一条成立*/
```

and运算符

```mysql
select * from user where gender='女' and score>90;
/*从user表查询gender=女,且score大于90的，两边同时成立*/
```

合并查询

```mysql
select * from student,user where student.age=user.age;
/*从student和user表中查询age相同的数据*/21.
```

count()

```mysql
select count(*) from user where score>80;
/*从user表中查询满足条件score>80的数量*/
```

AVG()

```mysql
select AVG(score) from user;
/*从user表中查询score字段的平均值*/
```

sum()

```mysql
select sum(age) from user;
/*查询user表中age的和*/
```

min、max

```mysql
select min(age) from user; /*查询user表中age最小的*/
select max(age) from user; /*查询user表中age最大的*/
```

order by(排序)

```mysql
select * from user order by score;
/*从user表查询数据根据score字段进行升序*/
select * from user order by score desc;
/*从user表查询数据根据score字段进行降序*/
```

插入数据

```mysql
insert into user(name,age,score,gender) values('小红',18,90,'女');
/*向user表插入一条数据字段为user后边的 值为values后边的一一对应*/
```

更新数据

```mysql
update user set score=61,age=17 where name='小红';
/*更新user表名字为小红的score字段和age字段的值*/
/*注意：如果没有where条件的话则所有数据的score和age字段都改变*/
```

删除数据

```mysql
delete from user where name='小红';
/*删除user表中name=小红的数据*/
/*注意：没有where条件的话则删除表中所有数据*/
```

truncate

```mysql
truncate table 表名
/*清空表数据*/
```

between操作符

```mysql
select * from user where score between 60 and 80;
/*查询user表score字段60-80范围的数据*/
select * from user where score not between 60 and 80;
/*查询user表score字段不在60-80范围的数据*/
```

去重

```mysql
select distinct gender from user;
/*查询user表gender字段只显示一次去重*/
```

连接字段(concat)

```mysql
select concat(name,age) as info from user;
/*查询user表中的name和age字段并拼接成一个字段返回*/
/*例如：小红18*/
```

is null

```mysql
select * from user where name is null;
/*查询user表中name字段为null的数据*/
```

is not null

```mysql
select * from user where name is not null;
/*查询user表中name字段不为null的数据*/
```

if null

```mysql
select ifnull(age,0) from user;
/*查询user表中的年龄如果字段为null则返回0*/
```

length

```mysql
select length(name) from user;
/*查询name字段的字节个数*/
```

upper、lower

```mysql
select upper('a');
/*转大写*/
select lower('A')
/*转小写*/
```

substr(截取)

```mysql
select substr('lanzhiyuan',2,1);
/*select substr('截取的字段','截取的开始位置','截取的数量') 注意：mysql索引从1开始*/
```

instr

```mysql
select instr('lanzhiyuan','zhi');
/*查询第二个参数在第一个参数中的起始索引,查不到则返回0*/
```

trim

```mysql
select trim('  lan  ');
/*去除前后空格*/
select trim('a' from 'aaaalanaaaa');
/*去除前后指定字符(a)*/
```

lpad、rpad(填充指定个数字符)

```mysql
select lpad('lan',5,'*');
/*向左填充指定长度指定字符*/
select rpad('lan',5,'*');
/*向右填充指定长度指定字符*/
/*如果长度小于字段长度则从右截取*/
```

replace

```mysql
select replace('lanzhiyuan','an','**');
/*将第一个参数中的an全部替换为第三个参数*/
```

round(四舍五入)

```mysql
select round(1.56,2)
/*第一个参数是要四舍五入的字段，第二个参数是小数点后保留的位数，默认取整*/
```

ceil(向上取整)

```mysql
select clil(1.2);
/*向上取整*/
```

floor(向下取整)

```mysql
select floor(1.2);
/*向下取整*/
```

truncate(截断)

```mysql
select truncate(1.2222,1)
/*小数点后保留一位*/
```

mod(取余)

```mysql
select mod(10,3);
/*取余数*/
```

now(当前时间+日期)

```mysql
select now();
/*返回当前时间包含时间*/
```

curdate(当前日期)

```mysql
select curdate();
/*返回当前日期不包括时间*/
```

curtime

```mysql
select curtime();
/*返回当前时间不包含日期*/
```

日期格式字符

```mysql
%Y --- 四位年份 1998
%y --- 2位年份 98
%m --- 月份(01、02...)
%c --- 月份(1、2...)
%d --- 日(01、02...)
%H --- 小时(24小时制)
%h --- 小时(12小时制)
%i --- 分钟
%s --- 秒
```

str_to_date

```mysql
select str_to_date('9-13-1999','%m-%d-%Y');
/*将字符转换成指定格式的日期*/
```

data_format

```mysql
select data_format(date,'%y-%m-%d');
/*将指定日期转换为字符*/
```

if函数

```mysql
select name,age,if(score is null,'无','有') from student;
/*如果score字段是null则返回无否则返回有*/
```

case函数

```mysql
/*第一种情况*/
select age,name,case age when 18 age*1.1 when 20 then age*1.2 else age end as new_age from user;
/*如果age等于18返回age*1.1，如果等于20返回age*1.2,否则返回age*/

/*第二种情况*/
select name,age,score, case  when score > 90 then '优秀' when score > 60 then '及格' else '不及格' end as 成绩级别 from student;
/*如果成绩大于90显示优秀，大于60显示及格，否则显示不合格*/
/*
区别：case 后边加变量和不加变量，和后边返回值或者表达式
*/
```

group by

```mysql
select max(age),gender from user group by gender;
/*以gender字段进行分组查询，查询年龄最大的*/
```

having

````mysql
select count(*),gender from user group by gender having count(*)>10;
/*以gender字段进行分组查询，返回查询个数大于10的，进行分组后的条件筛选*/
````

等值连接(sql99语法)

```mysql
select student_name,teacher_name from student s inner join teacher t on s.id = t.id;
/*查询学生名字和对应老师的名字*/
/*语法：*/
select 查询字段 from 表名 inner join 表2 on 连接条件 inner join 表3 on 连接条件 where 筛选条件(可省略) group by 分组(可省略) order by 排序(可省略)。。。
/*inner可省略*/
```

外连接

```mysql
select s.name from student s left outer join teacher t on s.teacher_id = t.teacher_id where t.id is null;
/*查询没有老师的学生名字，left左边为主表，右外连接则相反*/
```

标量子查询(一行一列)

案例1

```mysql
select * from student where age > (select age from student where name = '小明');
/*从student表中查询比小明年龄大的同学*/
```

案例2(多条子查询)

```mysql
select * from student where score > (select score from student where name = '小明') and age > (select age from student where name = '小明');
/*从student中查询成绩大于小明并且年龄大于小明的同学*/
```

案例3

```mysql
select name,score from student where score = (select min(score) from student);
/*从student表中查询成绩最低的同学名字和成绩*/
```

列子查询(多行子查询)

案例1

```mysql
select name from student where teacher_id in (select teacher_id from teacher where teacher_id in (1,4))
/*查询老师id为4和1的所有学生姓名*/
```

案例2

```mysql
select t.*,(select count(*) from student s where s.teacher_id = t.teacher_id) count from teacher t;
/*查询每个老师的信息包含每个老师的学生个数 select后子查询*/
```

提示：子查询可以放在select、from、where、having、in、all等后边

union

```mysql
select * from student where name like '%a%' union select * from student where age > 20;
/*联合查询将多条语句查询结果合并*/
/*查询的列数要一致*/
/*语句默认自动去重，如果不去重使用union all*/
```