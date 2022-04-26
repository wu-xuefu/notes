# mysql

## 正则表达式

REGEXP

## 10.计算字段

算字段是运行时在SELECT语句
内创建的

### 拼接字段

#### 拼接 ```concat()```

#### 删除多余空格 ```LTrim() RTrim() Trim()```

为了引用，使用别名 *//别名也叫到处列*

#### AS 别名

#### 算术运算(+-*/)

now()//*返回当前时间*

## 11.函数

函数的可移植性没有SQL强

### 常用文本处理函数

|函数|说明|
|-|-|
|Left(str,length)|返回串右边的字符|
|Right()|返回串右边字符|
|Length(str)|返回串的长度|
|Locate(substr,str,[pos])|返回串的一个字串|
|Soundex()|返回串的soundex值|
|SubString(sting,position,length)|返回字串的字符|
|Upper()|将串转换为大写|
|Lower()|将串转换为小写|
|LTrim()|去掉左边空格|
|RTrim()|去掉右边空格|

### 日期和时间处理函数

|函数|说明|
|-|-|
|AddDate(date,INTERVAL value addunit)|增加一个日期（正负）（天、周）|
|AddTime(time,addtime)|增加一个时间（时、分）|
|CurDate()|返回当前日期|
|CurTime()|返回当前时间|
|DateDiff(date1,date2)|计算俩个日期之差(date1-date2)|
|Date_add()|高度灵活的日期运算函数|
|Date_format(date,format)|返回一个格式化的日期或者时间串|
|DayOfWeek(date)|返回一个日期,对应的星期几（星期天为1）|
|Now()|返回当前时间|
|Date(date)|返回日期时间的日期部分|
|Time()||
|Day()||
|Hour()||
|Minute()||
|Month()||
|Second()||
|Year()||

*格式推荐 yyyy-mm-dd 减少歧义*

总是使用4位数字的年份

|00 ~ 69|2000 ~ 2069|
|-|-|
|70~99|1970~1999|

#### 数据过滤 about 日期和时间

where过滤数据的时候应该注意日期对日期(使用date())，时间对时间(使用time())，即使该表只有日期或时间。

检索某个月所有的信息时有两种办法

```sql
WHERE Date(date) BETWEEN '2005-09-01' AND '2005-09-30' #BETWEEN为一个要匹配的时间范围
```

```sql
WHERE Year(date) = 2005 AND Month(Date) = 9;#这样做的好处在于忽略每个月多少天
```

### 数值处理函数

|函数|说明|
|-|-|
|Rand()|随机数|
|Abs()|绝对值|
|Sqrt()|平方根|
|Exp()|指数值|
|Mod()|余数|
|Pi()|PI|
|Sin()|sin|
|Cos()|cos|
|Tan()|tan|

## 12.汇总数据

### 聚集函数

|函数|说明|
|-|-|
|AVG()|忽略NULL值的行|
|COUNT()|count(*)不忽略NULL，count(column)忽略NULL值行|
|MAX()|Max忽略NULL，对于文本就跟string比大小一样|
|MIN()||
|SUM()|忽略NULL|

#### 聚集不同值

在函数中使用 `distinct` 参数（ALL 是默认行为）

```sql
select AVG(distinct id) AS avg_id
```

使用聚集函数时候取别名是个好习惯

聚集函数很高效，它们返回结果一般比你在自己的客户机应用程序中计算要快得多。

## 13.分组数据

分组允许把数据分为多个逻辑组，以
便能对每个组进行聚集计算。

*TODO* P95

1. GROUP BY子句可以包含任意数目的列
2. 如果在GROUP BY子句中嵌套了分组，数据将在最后规定的分组上
进行汇总（所以不能从个别的列取回数据）
3. 如果分组列中具有NULL值，则NULL将作为一个分组返回。
4. GROUP BY子句中列出的每个列都必须是检索列或有效的表达式
（但不能是聚集函数）。如果在SELECT中使用表达式，则必须在
GROUP BY子句中指定相同的表达式。不能使用别名。
5. 除聚集计算语句外，SELECT语句中的每个列都必须在GROUP BY子
句中给出。
6. GROUP BY子句必须出现在WHERE子句之后，ORDER BY子句之前。

`WITH ROLLUP`汇总数据

### 过滤分组

|||
|-|-|
|`HAVING`|过滤分组、分组后过滤|
|`WHERE`|过滤行、分组前过滤|

## 14.子查询

子查询总是从内向外处理

1. 子查询进行过滤（最常见`WHERE`的`IN`）
2. 作为计算字段

逐渐增加子查询来建立查询，由内到外建立和测试，然后，用硬编码数据建立和测试外层查询，仅在确认它正常后才嵌入子查询，重复这些步骤。

## 15.联结表

等值联结（equijoin），它基于两个表之间的相等测试。这种联结也称为内部联结。

`inner join on`

```sql
WHERE a.id = b.id

select actor.actor_id,actor_info.first_name
from actor inner join actor_info
on actor.actor_id = actor_info.actor_id  
limit 10;
```

笛卡尔积 由没有联结条件的表关系返回的结果为笛卡儿积。检索出的行的数目将是第一个表中的行数乘以第二个表中的行数

1. **自联结** 把一张表假设为两张一样的表，然后在做“多表查询
2. **自然联结** 每个列只返回一次
3. 外部联结
   1. 左联结`LEFT OUTER JOIN`
   2. 右联结`RIGHT OUTER JOIN`

**使用带聚集函数的联结**

## 17.组合查询

`UNION`合并

- UNION必须由两条或两条以上的SELECT语句组成，语句之间用关键字UNION分隔
- UNION中的每个查询必须包含相同的列、表达式或聚集函数（不过各个列不需要以相同的次序列出）
- 列数据类型必须兼容：类型不必完全相同，但必须是DBMS可以隐含地转换的类型（例如，不同的数值类型或不同的日期类型）

`UNION`从查询结果集中自动去除了重复的行

`UNION ALL`包含重复的行

用UNION组合查询时，只能使用一条ORDER BY子句，它必须出现在最后一条SELECT语句之不允许使用多条ORDER BY子句。

## 18。全文本搜素

只能用InnoDB引擎

`FULLTEXT`

```SQL
SELECT *
FROM TEXT
WHERE Match(text) against('aa')

```

TODO

## 19.插入数据

```sql
INSERT INTO TABLE
VALUES(

    );
```

编写依赖于特定列次序的SQL语句是很不安全的

编写INSERT语句的更安全（不过更烦琐）的方法如下

```sql
INSERT INTO TABLE(ACTOR_ID)
VALUES(111

    );
```

优点

1. 表的结构改变，此INSERT语句仍然能正确工作。你会发现cust_id的NULL值是不必要的，
2. 没有出现在列表中，可以不需要任何值

### 提高整体性能

指示MySQL降低INSERT语句的优先级,也适用于UPDATE和DELETE语句

INSERT操作可能很耗时（特别是有很多索引需要更新时），而且它可能降低等待处理的SELECT语句的性能

```sql
INSERT LOW_PRIORITY INTO TABLE
```

### 提高INSERT的性能

单条INSERT语句处理多个插入比使用多条INSERT语句快

### 插入检索数据

```sql
INSERT INTO TABLE()
SELECT
```

## 20.更新数据

```sql
UPDATE actor
SET last_update = now()
WHERE actor_id = 1;
```

发生错误，也继续进行更新

```sql
UPDATE IGNORE actor
```

为了删除某个列的值，可设置它为NULL（假如表定义允许NULL值）

```sql
DELETE FROM TABLE
WHERE ID = ;
```

### 更快的删除

如果想从表中删除所有行，不要使用DELETE。可使用`TRUNCATE TABLE table_name`语句

## 21.创建和操纵表

`IF NOT EXISTS`查看表名是否存在，并且仅在表名不存在时创建它

```sql
create table test2(
    id int not null AUTO_INCREMENT,
    name  char(20) DEFAULT "test",
    primary key (id)
)ENGINE = InnoDB;
```

`AUTO_INCREMENT`  自增

`DEFAULT` 只支持常量

- InnoDB是一个可靠的事务处理引擎（参见第26章），它不支持全文本搜索；
- MEMORY在功能等同于MyISAM，但由于数据存储在内存（不是磁盘）中，速度很快（特别适合于临时表）；
- MyISAM是一个性能极高的引擎，它支持全文本搜索，但不支持事务处理。

引擎类型可以混用，外键不能跨引擎

alter table test
add phone int，
drop column phone;

TODO 添加外键不上

外键

**级联**

```sql
ON UPDATE CASCADE
ON DELECT CASCADE
```

```
ALTER TABLE TEST1
ADD CONSTRAINT FK FOREIGN KEY (ID) REFERENCES TEST2 (ID)

### 删除表

```sql
drop table test2;
```

### 重命名表

```SQL
RENAME TABLE TEST TO TEST1;
```

## 22.视图

性能问题 因为视图不包含数据，所以每次使用视图时，都必须处理查询执行时所需的任一个检索。

- 视图用`CREATE VIEW`语句来创建。
- 使用`SHOW CREATE VIEW viewname`；来查看创建视图的语句。
- 用`DROP`删除视图，其语法为`DROP VIEW viewname`;。
- 更新视图时，可以先用`DROP`再用`CREATE`，也可以直接用`CREATE OR REPLACE VIEW`。如果要更新的视图不存在，则第2条更新语句会创建一个视图；如果要更新的视图存在，则第2条更新语句会替换原有视图。

```sql
create view selet as
select *
from actor
limit 10;
```

```sql
show create view actor_info;
```

### 更新视图

实际上是对其基表更改。

- 分组（使用GROUP BY和HAVING）；
- 联结；
- 子查询；
- 并；
- 聚集函数（Min()、Count()、Sum()等）
- DISTINCT；
- 导出（计算）列。

### 23.存储过程

优点

1. 封装
2. 提高性能

```sql

DELIMITER //
create procedure mypro2(
in pl int,
out pm decimal(8,2)
out ph decimal(8,2),
out pa decimal(8,2)
)
begin

    DECLARE TAXRATE DEFAULT 6;



    select actor_id
    into pm
    from actor
    where actor_id = pl;
    select min(actor_id)
    into pl
    from actor;
    select max(actor_id)
    into ph
    from actor;
    select avg(actor_id)
    into pa
    from actor;
end
// DELIMITER;
```

### 删除存储过程

```sql
drop procedure mypro;
DROP PROCEDURE IF EXISTS #仅当存在时删除
```

`comment` （非必须）可以在`SHOW PROCEDURE STATUS (LIKE)`显示

```sql
show create procedure;
```

## 24.游标

TODO

```SQL
DELIMITER //
create procedure mypro13(
) comment 'this is a first'
begin
declare o int;
declare done boolean default 0;

declare ord cursor
for
select actor_id from actor;

declare continue handler for sqlstate '02000' set done =1;

open ord;
    repeat
    fetch ord into o;
    select o;
until done end repeat;
close ord;
end //
DELIMITER 
```

## 25.触发器

```sql
drop trigger ;
create trigger t1 {before/after} {insert|update|delete} on table
for each row
begin
end
```

## 26.事务

事务处理（transaction processing）可以用来维护数据库的完整性，它保证成批的MySQL操作要么完全执行，要么完全不执行。

- 事务（transaction）指一组SQL语句；
- 回退（rollback）指撤销指定SQL语句的过程；
- 提交（commit）指将未存储的SQL语句结果写入数据库表；
- 保留点（savepoint）指事务处理中设置的临时占位符（place-holder），你可以对它发布回退（与回退整个事务处理不同）。


```sql
START TRANSACTION;
ROLLBACK [TO ];
COMMIT;
SAVEPOINT;


```

### 更改默认的提交行为

`SET autocommit = 0`

标志为连接专用 autocommit标志是针对每个连接而不是服务器的。

## 28. 安全管理

`create user ben IDENTIFIED by'1';`

`RENAME USER ben TO bf`

`DROP USER bf`

`show grants for`

`{grant|revoke} select on carshcours.* to bf`

`set password for bf = password('123')`

SET PASSWORD更新用户口令。新口令必须传递到Password()函数进行加密。
