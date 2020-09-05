# 在线Markdown

数据库：

[下载PDF](http://127.0.0.1:9998/download?ip=10.0.4.104&port=3306&database=ssm_crm&username=root&password=root&selector=mysql)

- [1.contact](http://127.0.0.1:9998/login.action#1.contact)
- [2.customer](http://127.0.0.1:9998/login.action#2.customer)
- [3.follow](http://127.0.0.1:9998/login.action#3.follow)
- [4.orderform](http://127.0.0.1:9998/login.action#4.orderform)
- [5.role](http://127.0.0.1:9998/login.action#5.role)
- [6.role_permission](http://127.0.0.1:9998/login.action#6.role_permission)
- [7.user_customer](http://127.0.0.1:9998/login.action#7.user_customer)
- [8.user_follow](http://127.0.0.1:9998/login.action#8.user_follow)
- [9.user_operation_log](http://127.0.0.1:9998/login.action#9.user_operation_log)
- [10.user_orderform](http://127.0.0.1:9998/login.action#10.user_orderform)
- [11.user_role](http://127.0.0.1:9998/login.action#11.user_role)
- 12.users

## 1.contact

基本信息: InnoDB utf8

| 序列 |           列名           |    类型     | 可空 | 默认值 | 注释 |
| :--: | :----------------------: | :---------: | :--: | :----: | :--: |
|  1   | contactID auto_increment |   int(11)   |  NO  |        |  …   |
|  2   |        customerID        |   int(11)   | YES  |        |  …   |
|  3   |     contactPosition      | varchar(50) | YES  |        |  …   |
|  4   |       contactName        | varchar(50) | YES  |        |  …   |
|  5   |        contactSex        |   int(11)   | YES  |        |  …   |
|  6   |       contactPhone       | varchar(50) | YES  |        |  …   |
|  7   |        contactQQ         | varchar(50) | YES  |        |  …   |
|  8   |       contactEmail       | varchar(50) | YES  |        |  …   |
|  9   |       contactDate        |    date     | YES  |        |  …   |

| 序列 |     索引名     |   类型    |  包含字段  |
| :--: | :------------: | :-------: | :--------: |
|  1   |    PRIMARY     |  PRIMARY  | contactID  |
|  2   |    Index_1     | UNIQUEKEY | contactID  |
|  3   | FK_Reference_5 |    KEY    | customerID |

## 2.customer

基本信息: InnoDB utf8

| 序列 |           列名            |     类型     | 可空 | 默认值 | 注释 |
| :--: | :-----------------------: | :----------: | :--: | :----: | :--: |
|  1   | customerID auto_increment |   int(11)    |  NO  |        |  …   |
|  2   |       customerName        | varchar(50)  |  NO  |        |  …   |
|  3   |       customerPhone       | varchar(50)  | YES  |        |  …   |
|  4   |      customerAddress      | varchar(255) | YES  |        |  …   |
|  5   |        customerUrl        | varchar(255) | YES  |        |  …   |
|  6   |       customerType        |   int(11)    | YES  |        |  …   |
|  7   |      customerStatus       |   int(11)    | YES  |        |  …   |
|  8   |       customerDate        |     date     | YES  |        |  …   |
|  9   |            lng            |    double    | YES  |        |  …   |
|  10  |            lat            |    double    | YES  |        |  …   |

| 序列 | 索引名  |   类型    |        包含字段         |
| :--: | :-----: | :-------: | :---------------------: |
|  1   | PRIMARY |  PRIMARY  | customerID,customerName |
|  2   | Index_1 | UNIQUEKEY |       customerID        |

## 3.follow

基本信息: InnoDB utf8

| 序列 |          列名           |     类型     | 可空 | 默认值 | 注释 |
| :--: | :---------------------: | :----------: | :--: | :----: | :--: |
|  1   | followID auto_increment |   int(11)    |  NO  |        |  …   |
|  2   |       customerID        |   int(11)    | YES  |        |  …   |
|  3   |        contactID        |   int(11)    | YES  |        |  …   |
|  4   |      followContent      | varchar(255) | YES  |        |  …   |
|  5   |       followDate        |     date     | YES  |        |  …   |
|  6   |       followType        |   int(11)    | YES  |        |  …   |

| 序列 |     索引名     |   类型    |  包含字段  |
| :--: | :------------: | :-------: | :--------: |
|  1   |    PRIMARY     |  PRIMARY  |  followID  |
|  2   |    Index_1     | UNIQUEKEY |  followID  |
|  3   | FK_Reference_3 |    KEY    | customerID |
|  4   | FK_Reference_4 |    KEY    | contactID  |

## 4.orderform

基本信息: InnoDB utf8

| 序列 |          列名          |     类型     | 可空 | 默认值 | 注释 |
| :--: | :--------------------: | :----------: | :--: | :----: | :--: |
|  1   | orderID auto_increment |   int(11)    |  NO  |        |  …   |
|  2   |       customerID       |   int(11)    | YES  |        |  …   |
|  3   |       contactID        |   int(11)    | YES  |        |  …   |
|  4   |       orderName        | varchar(255) |  NO  |        |  …   |
|  5   |       orderDate        |     date     | YES  |        |  …   |
|  6   |      orderAmount       | float(11,2)  |  NO  |        |  …   |
|  7   |       orderNote        |     text     | YES  |        |  …   |

| 序列 |     索引名     |   类型    |     包含字段      |
| :--: | :------------: | :-------: | :---------------: |
|  1   |    PRIMARY     |  PRIMARY  | orderID,orderName |
|  2   |    Index_1     | UNIQUEKEY |      orderID      |
|  3   | FK_Reference_1 |    KEY    |    customerID     |
|  4   | FK_Reference_2 |    KEY    |     contactID     |

## 5.role

基本信息: InnoDB utf8

| 序列 |       列名        |     类型     | 可空 | 默认值 |  注释  |
| :--: | :---------------: | :----------: | :--: | :----: | :----: |
|  1   | id auto_increment |   int(11)    |  NO  |        | 角色ID |
|  2   |     roleName      | varchar(255) | YES  |        | 角色名 |

| 序列 | 索引名  |  类型   | 包含字段 |
| :--: | :-----: | :-----: | :------: |
|  1   | PRIMARY | PRIMARY |    id    |

## 6.role_permission

基本信息: InnoDB utf8

| 序列 |       列名        |     类型     | 可空 | 默认值 |    注释    |
| :--: | :---------------: | :----------: | :--: | :----: | :--------: |
|  1   | id auto_increment |   int(11)    |  NO  |        |     …      |
|  2   |      roleId       |   int(11)    |  NO  |        |   角色ID   |
|  3   |     tableName     | varchar(255) | YES  |        | 可操作的表 |
|  4   |      action       | varchar(255) |  NO  |        | 可做的操作 |

| 序列 |       索引名       |  类型   | 包含字段 |
| :--: | :----------------: | :-----: | :------: |
|  1   |      PRIMARY       | PRIMARY |    id    |
|  2   | role_action_roleId |   KEY   |  roleId  |

## 7.user_customer

基本信息: InnoDB utf8

| 序列 |       列名        |  类型   | 可空 | 默认值 |  注释  |
| :--: | :---------------: | :-----: | :--: | :----: | :----: |
|  1   | id auto_increment | int(11) |  NO  |        |   …    |
|  2   |      userId       | int(11) | YES  |        | 用户ID |
|  3   |    customerId     | int(11) | YES  |        | 客户ID |

| 序列 |   索引名   |  类型   |  包含字段  |
| :--: | :--------: | :-----: | :--------: |
|  1   |  PRIMARY   | PRIMARY |     id     |
|  2   |   userId   |   KEY   |   userId   |
|  3   | customerId |   KEY   | customerId |

## 8.user_follow

基本信息: InnoDB utf8

| 序列 |       列名        |  类型   | 可空 | 默认值 | 注释 |
| :--: | :---------------: | :-----: | :--: | :----: | :--: |
|  1   | id auto_increment | int(11) |  NO  |        |  …   |
|  2   |      userId       | int(11) | YES  |        |  …   |
|  3   |     followId      | int(11) | YES  |        |  …   |

| 序列 |  索引名  |  类型   | 包含字段 |
| :--: | :------: | :-----: | :------: |
|  1   | PRIMARY  | PRIMARY |    id    |
|  2   | followId |   KEY   | followId |
|  3   |  userId  |   KEY   |  userId  |

## 9.user_operation_log

基本信息: InnoDB utf8

| 序列 |               列名               |     类型     | 可空 | 默认值 | 注释 |
| :--: | :------------------------------: | :----------: | :--: | :----: | :--: |
|  1   |        id auto_increment         |   int(11)    |  NO  |        |  …   |
|  2   |              userId              |   int(11)    | YES  |        |  …   |
|  3   |              action              | varchar(255) | YES  |        |  …   |
|  4   | time on update CURRENT_TIMESTAMP |   datetime   | YES  |        |  …   |

| 序列 | 索引名  |  类型   | 包含字段 |
| :--: | :-----: | :-----: | :------: |
|  1   | PRIMARY | PRIMARY |    id    |
|  2   | userId  |   KEY   |  userId  |

## 10.user_orderform

基本信息: InnoDB utf8

| 序列 |       列名        |  类型   | 可空 | 默认值 | 注释 |
| :--: | :---------------: | :-----: | :--: | :----: | :--: |
|  1   | id auto_increment | int(11) |  NO  |        |  …   |
|  2   |      orderId      | int(11) |  NO  |        |  …   |
|  3   |      userId       | int(11) |  NO  |        |  …   |

| 序列 | 索引名  |  类型   | 包含字段 |
| :--: | :-----: | :-----: | :------: |
|  1   | PRIMARY | PRIMARY |    id    |
|  2   | orderId |   KEY   | orderId  |
|  3   | userId  |   KEY   |  userId  |

## 11.user_role

基本信息: InnoDB utf8

| 序列 |       列名        |  类型   | 可空 | 默认值 |  注释  |
| :--: | :---------------: | :-----: | :--: | :----: | :----: |
|  1   | id auto_increment | int(11) |  NO  |        |   …    |
|  2   |      userId       | int(11) | YES  |        | 用户ID |
|  3   |      roleId       | int(11) | YES  |        | 角色ID |

| 序列 |   索引名    |  类型   | 包含字段 |
| :--: | :---------: | :-----: | :------: |
|  1   |   PRIMARY   | PRIMARY |    id    |
|  2   | role_userId |   KEY   |  userId  |
|  3   | user_roleId |   KEY   |  roleId  |

## 12.users

基本信息: InnoDB utf8

| 序列 |       列名        |     类型     | 可空 |                            默认值                            |        注释        |
| :--: | :---------------: | :----------: | :--: | :----------------------------------------------------------: | :----------------: |
|  1   | id auto_increment |   int(11)    |  NO  |                                                              |       用户ID       |
|  2   |     userName      | varchar(255) |  NO  |                                                              |        帐号        |
|  3   |     password      | varchar(255) |  NO  |                                                              |        密码        |
|  4   |      petName      | varchar(255) |  NO  |                        Normal Editor                         |      用户昵称      |
|  5   |      avatar       | varchar(255) |  NO  | https://wpimg.wallstcn.com/f778738c-e4f8-4870-b634-56703b4acafe.gif |      用户头像      |
|  6   |     available     |   int(11)    |  NO  |                              1                               | 0为不可用，1为可用 |

| 序列 |  索引名  |   类型    |  包含字段   |
| :--: | :------: | :-------: | :---------: |
|  1   | PRIMARY  |  PRIMARY  | id,userName |
|  2   | userName | UNIQUEKEY |  userName   |