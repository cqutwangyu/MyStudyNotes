# SQL 基础

## SQL select

SELECT 语句用于从表中选取数据。

结果被存储在一个结果表中（称为结果集）。

```sql
SELECT 列名称 FROM 表名称
SELECT * FROM 表名称
```

```sql
select * from tableName
# *代表所有字段

select LastName,FirstName from Persons
# 查询Persons表中所有记录的LastName,FirstName字段
```

## SQL distinct

在表中，可能会包含重复值。这并不成问题，不过，有时您也许希望仅仅列出不同（distinct）的值。

关键词 DISTINCT 用于返回唯一不同的值。

```sql
SELECT DISTINCT 列名称 FROM 表名称
```

```sql
SELECT DISTINCT Company FROM Orders 
# 查询Orders表中的Company字段，且不重复，如有多条相同数据，只显示一条。
```

## SQL where

如需有条件地从表中选取数据，可将 WHERE 子句添加到 SELECT 语句。

```sql
SELECT 列名称 FROM 表名称 WHERE 列 运算符 值
```

```sql
SELECT * FROM Persons表中 WHERE City='Beijing'
# 查询Persons表中City字段为'Beijing'的所有记录的所有字段。
```

## SQL and & or

AND 和 OR 可在 WHERE 子语句中把两个或多个条件结合起来。

如果第一个条件和第二个条件都成立，则 AND 运算符显示一条记录。

```sql
SELECT * FROM Persons WHERE FirstName='Thomas' AND LastName='Carter'
# 查询Persons表中FirstName='Thomas'并且LastName='Carter'的所有记录的所有字段。
```


如果第一个条件和第二个条件中只要有一个成立，则 OR 运算符显示一条记录。
```sql
SELECT * FROM Persons WHERE firstname='Thomas' OR lastname='Carter'
# 查询Persons表中firstname='Thomas'或者lastname='Carter'的所有记录的所有字段。
```

## SQL order by

ORDER BY 语句用于根据指定的列对结果集进行排序。

ORDER BY 语句默认按照升序对记录进行排序。

如果您希望按照降序对记录进行排序，可以使用 `DESC` 关键字。

```sql
SELECT Company, OrderNumber FROM Orders ORDER BY Company
# 查询Orders表中的所有记录的Company, OrderNumber字段，并按照Company升序排序

SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC
# 查询Orders表中的所有记录的Company, OrderNumber字段，并按照Company降序排序
```

## SQL insert

 INSERT INTO 语句用于向表格中插入新的行。

```sql
INSERT INTO 表名称 VALUES (值1, 值2,....)
```

我们也可以指定所要插入数据的列：

```sql
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
```

```sql
INSERT INTO Persons VALUES ('Gates', 'Bill', 'Xuanwumen 10', 'Beijing')
# 将括号中的数据插入到Persons表中，每个字段默认对应表中字段顺序。

INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')
# 将后面括号中的数据插入到Persons表中，每个字段依次对应前面括号中的字段名。
```

## SQL update

Update 语句用于修改表中的数据。

```sql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```

```sql
UPDATE Person SET FirstName = 'Fred' WHERE LastName = 'Wilson' 
# 将Person表中LastName字段值为'Wilson'的记录的FirstName字段值改为'Fred'。

UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing'
WHERE LastName = 'Wilson'
# 将Person表中LastName字段值为'Wilson'的记录的Address字段值改为'Zhongshan 23'，并把City字段值改为'Nanjing'。
```

## SQL delete

DELETE 语句用于删除表中的行。

```sql
DELETE FROM 表名称 WHERE 列名称 = 值
```

```sql
DELETE FROM Person WHERE LastName = 'Wilson' 
# 删除Person表中LastName字段值为'Wilson'的记录。
```

# SQL 高级

## SQL Top

TOP 子句用于规定要返回的记录的数目。

对于拥有数千条记录的大型表来说，TOP 子句是非常有用的。

可以使用`PERCENT`关键字。

**注释：**并非所有的数据库系统都支持 TOP 子句。

```sql
SELECT TOP 2 * FROM Persons
# 查询Persons表中前两条记录的所有字段

SELECT TOP 50 PERCENT * FROM Persons
# 查询Persons表中前50%的记录
```

## SQL Like

LIKE 操作符用于在 WHERE 子句中搜索列中的指定模式。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern
```

```sql
SELECT * FROM Persons
WHERE City LIKE 'N%'
# 查询Persons表中City字段值以N开头的记录

SELECT * FROM Persons
WHERE City LIKE '%g'
# 查询Persons表中City字段值以g结尾的记录

SELECT * FROM Persons
WHERE City LIKE '%lon%'
# 查询Persons表中City字段值包含lon的记录

SELECT * FROM Persons
WHERE City NOT LIKE '%lon%'
# 查询Persons表中City字段值不包含lon的记录
```

## SQL 通配符

在搜索数据库中的数据时，SQL 通配符可以替代一个或多个字符。

SQL 通配符必须与 LIKE 运算符一起使用。

在 SQL 中，可使用以下通配符：

| 通配符                     | 描述                       |
| :------------------------- | :------------------------- |
| %                          | 替代一个或多个字符         |
| _                          | 仅替代一个字符             |
| [charlist]                 | 字符列中的任何单一字符     |
| [^charlist]或者[!charlist] | 不在字符列中的任何单一字符 |

```sql
SELECT * FROM Persons
WHERE City LIKE 'Ne%'
# 查询 Persons表中City字段值以Ne开头的所有记录

SELECT * FROM Persons
WHERE City LIKE '%lond%'
# 查询 Persons表中City字段值包含lond的所有记录

SELECT * FROM Persons
WHERE FirstName LIKE '_eorge'
# 查询 Persons表中FirstName字段值第一个字符后是eorge的所有记录

SELECT * FROM Persons
WHERE LastName LIKE 'C_r_er'
# 查询 Persons表中FirstName字段值为C+一个任意字符+r+一个任意字符+er的所有记录

SELECT * FROM Persons
WHERE City LIKE '[ALN]%'
# 查询Persons表中City字段值以A或L或N开头的记录 

SELECT * FROM Persons
WHERE City LIKE '[!ALN]%'
# 查询Persons表中City字段值不以A或L或N开头的记录 
```

## SQL Limit

查询`i`到`i+n`条记录

```sql
select * from tableName limit i,n
# tableName：表名
# i：为查询结果的索引值(默认从0开始)，当i=0时可省略i
# n：为查询结果返回的数量
# i与n之间使用英文逗号","隔开

# limit n 等同于 limit 0,n
```
```sql
# MySQL 语法
SELECT column_name(s)
FROM table_name
LIMIT number

# 例子
SELECT *
FROM Persons
LIMIT 5
# 查询Persons表中第0到5条记录的所有字段。
```