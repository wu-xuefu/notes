# mysql

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

