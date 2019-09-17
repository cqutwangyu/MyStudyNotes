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

## SQL In

IN 操作符允许我们在 WHERE 子句中规定多个值。

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name IN (value1,value2,...)
```

```sql
SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')
# 查询Persons表中LastName为'Adams'或'Carter'的
```

## SQL Between

```sql
SELECT column_name(s)
FROM table_name
WHERE column_name
BETWEEN value1 AND value2
```

```sql
SELECT * FROM Persons
WHERE LastName
BETWEEN 'Adams' AND 'Carter'
#以字母顺序显示介于 "Adams"（包括）和 "Carter"（不包括）之间的人

SELECT * FROM Persons
WHERE LastName
NOT BETWEEN 'Adams' AND 'Carter'
#以字母顺序显示介于 "Adams"（包括）和 "Carter"（不包括）之外的人
```

## SQL Alias

可以为列名称和表名称指定别名（Alias）。

```sql
SELECT column_name(s)
FROM table_name
AS alias_name
```
**Persons表：**

| Id   | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

```sql
SELECT LastName AS Family, FirstName AS Name
FROM Persons
# 查询Persons表中所有的LastName别名为Family，FirstName别名为Name
```

**结果：**

| Family | Name   |
| :----- | :----- |
| Adams  | John   |
| Bush   | George |
| Carter | Thomas |

## SQL join

**SQL join 用于根据两个或多个表中的列之间的关系，从这些表中查询数据。**

Join 和 Key

有时为了得到完整的结果，我们需要从两个或更多的表中获取结果。我们就需要执行 join。

数据库中的表可通过键将彼此联系起来。主键（Primary Key）是一个列，在这个列中的每一行的值都是唯一的。在表中，每个主键的值都是唯一的。这样做的目的是在不重复每个表中的所有数据的情况下，把表间的数据交叉捆绑在一起。

 **"Persons" 表：**

| Id_P | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

 **"Orders" 表：**

| Id_O | OrderNo | Id_P |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

"Id_O" 列是 Orders 表中的的主键，同时，"Orders" 表中的 "Id_P" 列用于引用 "Persons" 表中的人，而无需使用他们的确切姓名。

"Id_P" 列把上面的两个表联系了起来。

**引用两个表**

我们可以通过引用两个表的方式，从两个表中获取数据：

谁订购了产品，并且他们订购了什么产品？

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons, Orders
WHERE Persons.Id_P = Orders.Id_P 
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

**使用 Join**

除了上面的方法，我们也可以使用关键词 JOIN 来从两个表中获取数据。

如果我们希望列出所有人的定购，可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P = Orders.Id_P
ORDER BY Persons.LastName
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

## **不同的 SQL JOIN**

除了我们在上面的例子中使用的 INNER JOIN（内连接），我们还可以使用其他几种连接。

下面列出了您可以使用的 JOIN 类型，以及它们之间的差异。

- JOIN: 如果表中有至少一个匹配，则返回行，INNER JOIN 与 JOIN 是相同的。
- LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行
- RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行
- FULL JOIN: 只要其中一个表中存在匹配，就返回行

## SQL INNER JOIN

在表中存在至少一个匹配时，INNER JOIN 关键字返回行。

INNER JOIN 与 JOIN 是相同的。

```sql
SELECT column_name(s)
FROM table_name1
INNER JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**"Persons" 表：**

| Id_P | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

**"Orders" 表：**

| Id_O | OrderNo | Id_P |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

**内连接（INNER JOIN）实例**

现在，我们希望列出所有人的定购。

您可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |

INNER JOIN 关键字在表中存在至少一个匹配时返回行。如果 "Persons" 中的行在 "Orders" 中没有匹配，就不会列出这些行。

## SQL LEFT JOIN

LEFT JOIN 关键字会从左表 (table_name1) 那里返回所有的行，即使在右表 (table_name2) 中没有匹配的行。

```SQL
SELECT column_name(s)
FROM table_name1
LEFT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**"Persons" 表：**

| Id_P | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

**"Orders" 表：**

| Id_O | OrderNo | Id_P |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

**左连接（LEFT JOIN）实例**

现在，我们希望列出所有的人，以及他们的定购 - 如果有的话。

您可以使用下面的 SELECT 语句：

```sql
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
LEFT JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |

LEFT JOIN 关键字会从左表 (Persons) 那里返回所有的行，即使在右表 (Orders) 中没有匹配的行。

## SQL RIGHT JOIN

RIGHT JOIN 关键字会右表 (table_name2) 那里返回所有的行，即使在左表 (table_name1) 中没有匹配的行。

```SQL
SELECT column_name(s)
FROM table_name1
RIGHT JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**"Persons" 表：**

| Id_P | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

**"Orders" 表：**

| Id_O | OrderNo | Id_P |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

**右连接（RIGHT JOIN）实例**

现在，我们希望列出所有的定单，以及定购它们的人 - 如果有的话。

您可以使用下面的 SELECT 语句：

```SQL
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
RIGHT JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
|          |           | 34764   |

RIGHT JOIN 关键字会从右表 (Orders) 那里返回所有的行，即使在左表 (Persons) 中没有匹配的行。

## SQL FULL JOIN

只要其中某个表存在匹配，FULL JOIN 关键字就会返回行。

```SQL
SELECT column_name(s)
FROM table_name1
FULL JOIN table_name2 
ON table_name1.column_name=table_name2.column_name
```

**"Persons" 表：**

| Id_P | LastName | FirstName | Address        | City     |
| :--- | :------- | :-------- | :------------- | :------- |
| 1    | Adams    | John      | Oxford Street  | London   |
| 2    | Bush     | George    | Fifth Avenue   | New York |
| 3    | Carter   | Thomas    | Changan Street | Beijing  |

**"Orders" 表：**

| Id_O | OrderNo | Id_P |
| :--- | :------ | :--- |
| 1    | 77895   | 3    |
| 2    | 44678   | 3    |
| 3    | 22456   | 1    |
| 4    | 24562   | 1    |
| 5    | 34764   | 65   |

**全连接（FULL JOIN）实例**

现在，我们希望列出所有的人，以及他们的定单，以及所有的定单，以及定购它们的人。

您可以使用下面的 SELECT 语句：

```SQL
SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
FULL JOIN Orders
ON Persons.Id_P=Orders.Id_P
ORDER BY Persons.LastName
```

**结果集：**

| LastName | FirstName | OrderNo |
| :------- | :-------- | :------ |
| Adams    | John      | 22456   |
| Adams    | John      | 24562   |
| Carter   | Thomas    | 77895   |
| Carter   | Thomas    | 44678   |
| Bush     | George    |         |
|          |           | 34764   |

FULL JOIN 关键字会从左表 (Persons) 和右表 (Orders) 那里返回所有的行。如果 "Persons" 中的行在表 "Orders" 中没有匹配，或者如果 "Orders" 中的行在表 "Persons" 中没有匹配，这些行同样会列出。

## SQL UNION 和 UNION ALL 操作符

UNION 操作符用于合并两个或多个 SELECT 语句的结果集。

请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。

**UNION 操作符选取不同的值**

```SQL
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```

**UNION ALL 允许重复的值**

```SQL
SELECT column_name(s) FROM table_name1
UNION ALL
SELECT column_name(s) FROM table_name2
```

UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名。

**Employees_China:**

| E_ID | E_Name         |
| :--- | :------------- |
| 01   | Zhang, Hua     |
| 02   | Wang, Wei      |
| 03   | Carter, Thomas |
| 04   | Yang, Ming     |

**Employees_USA:**

| E_ID | E_Name         |
| :--- | :------------- |
| 01   | Adams, John    |
| 02   | Bush, George   |
| 03   | Carter, Thomas |
| 04   | Gates, Bill    |

**使用 UNION 命令**

列出所有在中国和美国的不同的雇员名：

```SQL
SELECT E_Name FROM Employees_China
UNION
SELECT E_Name FROM Employees_USA
```

**结果**

| E_Name         |
| :------------- |
| Zhang, Hua     |
| Wang, Wei      |
| Carter, Thomas |
| Yang, Ming     |
| Adams, John    |
| Bush, George   |
| Gates, Bill    |

# SQL 函数

## SQL GROUP BY

GROUP BY 语句用于结合合计函数，根据一个或多个列对结果集进行分组。

```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
```

**"Orders" 表：**

| O_Id | OrderDate  | OrderPrice | Customer |
| :--- | :--------- | :--------- | :------- |
| 1    | 2008/12/29 | 1000       | Bush     |
| 2    | 2008/11/23 | 1600       | Carter   |
| 3    | 2008/10/05 | 700        | Bush     |
| 4    | 2008/09/28 | 300        | Bush     |
| 5    | 2008/08/06 | 2000       | Adams    |
| 6    | 2008/07/21 | 100        | Carter   |

现在，我们希望查找每个客户的总金额（总订单）。

我们想要使用 GROUP BY 语句对客户进行组合。

我们使用下列 SQL 语句：

```sql
SELECT Customer,SUM(OrderPrice) FROM Orders
GROUP BY Customer
```

**结果集：**

| Customer | SUM(OrderPrice) |
| :------- | :-------------- |
| Bush     | 2000            |
| Carter   | 1700            |
| Adams    | 2000            |

很棒吧，对不对？

让我们看一下如果省略 GROUP BY 会出现什么情况：

```sql
SELECT Customer,SUM(OrderPrice) FROM Orders
```

**结果集：**

| Customer | SUM(OrderPrice) |
| :------- | :-------------- |
| Bush     | 5700            |
| Carter   | 5700            |
| Bush     | 5700            |
| Bush     | 5700            |
| Adams    | 5700            |
| Carter   | 5700            |

上面的结果集不是我们需要的。

那么为什么不能使用上面这条 SELECT 语句呢？解释如下：上面的 SELECT 语句指定了两列（Customer 和 SUM(OrderPrice)）。"SUM(OrderPrice)" 返回一个单独的值（"OrderPrice" 列的总计），而 "Customer" 返回 6 个值（每个值对应 "Orders" 表中的每一行）。因此，我们得不到正确的结果。不过，您已经看到了，GROUP BY 语句解决了这个问题。

**GROUP BY 一个以上的列**

我们也可以对一个以上的列应用 GROUP BY 语句，就像这样：

```sql
SELECT Customer,OrderDate,SUM(OrderPrice) FROM Orders
GROUP BY Customer,OrderDate
```

## SQL HAVING

在 SQL 中增加 HAVING 子句原因是，**WHERE 关键字无法与合计函数一起使用**。

```SQL
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value
```

 **"Orders" 表：**

| O_Id | OrderDate  | OrderPrice | Customer |
| :--- | :--------- | :--------- | :------- |
| 1    | 2008/12/29 | 1000       | Bush     |
| 2    | 2008/11/23 | 1600       | Carter   |
| 3    | 2008/10/05 | 700        | Bush     |
| 4    | 2008/09/28 | 300        | Bush     |
| 5    | 2008/08/06 | 2000       | Adams    |
| 6    | 2008/07/21 | 100        | Carter   |

现在，我们希望查找订单总金额少于 2000 的客户。

我们使用如下 SQL 语句：

```SQL
SELECT Customer,SUM(OrderPrice) FROM Orders
GROUP BY Customer
HAVING SUM(OrderPrice)<2000
```

**结果集：**

| Customer | SUM(OrderPrice) |
| :------- | :-------------- |
| Carter   | 1700            |

现在我们希望查找客户 "Bush" 或 "Adams" 拥有超过 1500 的订单总金额。

我们在 SQL 语句中增加了一个普通的 WHERE 子句：

```SQL
SELECT Customer,SUM(OrderPrice) FROM Orders
WHERE Customer='Bush' OR Customer='Adams'
GROUP BY Customer
HAVING SUM(OrderPrice)>1500
```

**结果集：**

| Customer | SUM(OrderPrice) |
| :------- | :-------------- |
| Bush     | 2000            |
| Adams    | 2000            |