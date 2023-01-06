# MySql数据库

## 一、DDL

### 1.DDL新建表格

create table emp {
	id int comment '编号',
	workno varchar(10) comment '工号',
	name varchar(10) comment '姓名',
	gender char(1) comment '性别',
	age tinyint unsigned comment '年龄',
	idcard char(18) comment '身份证号',
	entrydate date comment '入职时间'
} comment ‘员工表’;

### 2.DDL增删改查字段

DDL-表操作
为表格增加字段
alter table 表名 add 字段名 类型(长度) [comment注释] [约束]
alter table emp add nickname varchar(20) comment '昵称'

修改数据类型
alter table 表名 modify 字段名 新数据类型(长度)
修改字段名和字段类型
alter table 表名 change 旧字段名 新字段名 类型(长度) [comment 注释] [约束]
alter table emp change nikename username varchar(30) comment'用户名'

删除字段
alter table 表名 drop 字段名
alter table emp drop username

修改表名
alter table 表名 rename to 新表名
alter table emp rename to employee

 删除表
drop table [if exists] 表名
drop table if exists tb_user;
删除指定表，并重新创建该表
truncate table 表名
truncate table employee;(删除后重新删除 重新创建后数据消失 只有表结构)

## 二、DML

添加数据
给指定字段添加数据
insert into 表名(字段名1,字段名2...) values(值1,值2....)
给全部字段添加数据
insert into 表名 values (值1,值2,....)
批量添加数据(一次性插入多条数据)
insert into 表名(字段名1,字段名2,...) values(值1,值2,...),(值1,值2,...),(值1,值2,...);
insert into 表名 values(值1,值2,...),(值1,值2,...),(值1,值2,...);

修改数据
update 表名 set 字段名1 = 值1, 字段名2 = 值2, ...[where 条件]
(修改语句的条件可以有，也可以没有，如果没有条件，会修改整张表的所有数据)

删除数据
delete from 表名 [where 条件]

## 三、DQL

DQL
基本查询
查询多个字段
select 字段1,字段2,字段3...from 表名;
select*form 表名
设置别名
select 字段1[as 别名1],字段2[as 别名2]...from 表名;
去除重复记录
select dstnct 字段列表 from 表名;

条件查询
select 字段列表 from 表名 where 条件列表

聚合函数
select 聚合函数(字段列表) from 表名
null值不参与聚合函数的运算

分组查询
select 字段列表 from 表名[where 条件] group by 分组字段名 [having 分组后过滤条件]
分组前过滤用where 分组后过滤用having
执行顺序：where>聚合函数>having

排序查询
select 字段列表 from 表名 order by 字段1 排序方式1，字段2 排序方式2
排序方式：asc 升序(默认值) desc 降序

分页查询
select 字段列表 from limit 起始索引，查询记录数
注意：起始索引从0开始，起始索引=(查询页码 - 1) * 每页每条记录数

编写顺序
select from where groupby having orderby limit
执行顺序
from where groupby和having select orderby limit

## 四、DCL

DCL
查询用户
use mysql
select * from user
创建用户
create user '用户名@主机名' identifed by '密码';
修改用户密码
alter user '用户名@主机名' identifed with mysql_native_password by '新密码'
删除用户
drop user '用户名'@'主机名'
主机名可以使用%通配

dcl权限控制
查询权限
show grants for '用户名'@'主机名'
授予权限
grant 权限列表 on 数据库名.表名 '用户名'@'主机名'
撤销权限
revoke 权限列表 on 数据库名.表名 from '用户名'@'主机名'

