# MySQL必知必会读书笔记

数据集：http://forta.com/books/0672327120

## 1 了解SQL  

### 1.1 数据库基础  

#### 1.1.1 什么是数据库  

数据库 (database) 保存有组织的数据的容器（通常是一个文件或一组文件)。  

#### 1.1.2 表  

表（table) 某种特萣类型数据的结构化清单。  

模式（schema) 关于数据库和表的布局及特性的信息  

描述表的这组信息就是所谓的模式， 模式可以用来描述数据库中特定的表以及整个数据库（和其中表的关系）。  

#### 1.1.3 列和数据类型  

列 （column) 表中的一个字段。 所有表都是由一个或多个列组成的  

#### 1.1.4 行  

#### 1.1.5 主 键  

主 键 ( primary key) 一列（或一组列)， 其值能够唯一区分表中每个行。  

表中的任何列都可以作为主键， 只要它满足以下条件：
□ 任意两行都不具有相同的主键值；
□ 每个行都必须具有一个主键值（ 主键列不允许NULL值)。  

### 1.2 什么是SQL

SQL(发音为字母S-Q-L或sequel)是结构化査询语言( Structured Queiy
Language) 的缩写 。

## 2 MySQL简介 

### 2 .1 什么是MySQL

#### 2.1.1 客户机-服务器软件  

DBMS可分为两类： 一类为基于共享文件系统的DBMS, 另一类为基
于客户机-服务器的DBMS。 前者（包括诸如Microsoft Access和FileMaker)  用于桌面用途， 通常不用于髙端或更关键的应用。

### 2.2 MySQL工具  

#### 2.2.1 mysql命令行实用程序  

* 命令输入在mysql>之后；

* 命令用;或\9结束， 换句话说， 仅按Enter不执行命令；  

* 输入 help或\h 获得特定命令的帮助，如help select
* quit/exit退出

#### 2.2.2 MySQL Administrator  

MySQL Administrator ( MySQL管理器） 是一个图形交互客户机， 用
来简化MySQL服务器的管理。  

#### 2.2.3 MySQL Query Browse

MySQL Query Browser为一个图形交互客户机， 用来编写和执行MySQL命令  

## 3 使用MySQL

### 3.1 连 接  

### 3.2 选择数据库

使用use关键字

```
mysql> use mysql
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
```

### 3.3 了解数据库和表  

SHOW DATABASES;

```
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.00 sec)
```

SHOW TABLES;

```
mysql> SHOW TABLES;
+------------------------------------------------------+
| Tables_in_mysql                                      |
+------------------------------------------------------+
| columns_priv                                         |
| component                                            |
| db                                                   |
| default_roles                                        |
| 。。。。                                              |
+------------------------------------------------------+
37 rows in set (0.00 sec)

```

SHOW也可以用来显示表列:  

SHOW COLUMNS FROM component;

```
mysql> SHOW COLUMNS FROM component;
+--------------------+--------------+------+-----+---------+----------------+
| Field              | Type         | Null | Key | Default | Extra          |
+--------------------+--------------+------+-----+---------+----------------+
| component_id       | int unsigned | NO   | PRI | NULL    | auto_increment |
| component_group_id | int unsigned | NO   |     | NULL    |                |
| component_urn      | text         | NO   |     | NULL    |                |
+--------------------+--------------+------+-----+---------+----------------+
3 rows in set (0.00 sec)
```

所支持的其他SHOW语句还有:
□ SHOW STATUS, 用于显示广泛的服务器状态信息；
□ SHOW CREATE DATABASE和SHOW CREATE TABLE, 分别用来显
示创建特定数据库或表的MySQL语句；
□ SHOW GRANTS, 用来显示授予用户（所有用户或特定用户） 的安
全权限；
□ SHOW ERRORS和SHOW WARNINGS, 用来显示服务器错误或警告
消息。  

## 4 检 索 数 据 

### 4.1 SELECT语句  

### 4.2 检索单个列  

### 4.3 检索多个列  

### 4.4 检索所有列  

### 4.5 检索不同的行  

### 4.6 限 制 结 果  

为了返回第一行或前几行， 可使用LIMIT子句。  

### 4.7 使用完全限定的表名  

```
SELECT products.prod_name
FROM products ;
```

表名也可以是完全限定的， 如下所示：

```
SELECT products .prod_name
FROM crashcourse.products;
```

假定products表确实位于crashcourse数据库中  

## 5  排序检索数据  

### 5.1 排序数据  

使用 ORDER BY 子句

```
SELECT prod—name
FROM products
ORDER BY prod_name ;
```

### 5.2 按多个列排序

```
SELECT prod_idf prod—price, prod_name
FROM products
ORDER BY prod_price, prod_name:
```

仅在多个行具有相同的prod_price值时，才按prod_name进行排序  

### 5.3 指定排序方向  

默认升序，降序必须指定DESC关键字  

```
SELECT procLid, prod_price, prod_name
FROM products
ORDER BY prod_price DESC:
```

多个列排序，DESC关键字只应用到直接位于其前面的列名。 在上例中， 只对prod_price列指定DESC， 对prodjiame列不指定。 因此，
prod_price列以降序排序， 而prodjiame列（ 在每个价格内） 仍然按标
准的升序排序  。

==在多个列上降序排序==

如果想在多个列上进行降序排序， 必须对每个列指定DESC关键字。

与DESC相反的关键字是ASC (ASCENDING), 在升序排序时可以指定
它。 但实际上， ASC没有多大用处， 因为升序是默认的（如果既不指定ASC也不指定DESC， 则假定为ASC)  。

==区分大小写和排序顺序==

在==字典( dictionary )排序顺序中， A被视为与a相同==， 这是MySQL( 和大多数数据库管理系统） 的默认行为。 但是， 许多数据库管理员能够在需要时改变这种行为（ 如果你的数据库包含大量外语字符， 可能必须这样做 。

## 6 过 滤 数 据  

### 6.1 使用WHERE子句  

只检索所需数据需要指定搜索条件（ search criteria ) , 搜索条件也称为过滤条件（ filter condition ) .

### 6.2 WHERE子句操作符  

<> 不等于

!= 不等于

= 等于

BETWEEN 在指定的两个值之间

####   6.2.4 空值检查  

使用IS NULL子句  

```
SELECT FROM products prod_name
WHERE prod_price IS NULL;
```

## 7 数据过滤

### 7.1 组合WHERE子句  

AND OR

### 7.2 IN操作符  

IN取合法值的由逗号分隔的清单， 全都括在圆括号中。

```
mysql> SELECT prod_name,prod_price
    -> FROM products
    -> WHERE vend_id IN (1002,1003)
    -> ORDER BY prod_name;
```

为什么要使用IN操作符？ 其优点具体如下。
□ 在使用长的合法选项清单时， IN操作符的语法更清楚且更直观。
□ 在使用IN时， 计算的次序更容易管理（因为使用的操作符更少)。
□ IN操作符一般比OR操作符清单执行更快。
□ IN的最大优点是可以包含其他SELECT语句,使得能够更动态地建
立WHERE子句。 第14章将对此进行详细介绍。  

### 7.3 NOT操作符  

NOT WHERE子句中用来否定后跟条件的关键字。  

## 8 用通配符进行过滤  

### 8.1 LIKE操作符  

**通配符（wildcard)**： 用来匹配值的一部分的特殊字符。  

**搜索模式 （ search pattern)®** ：由字面值、 通配符或两者组合构
成的搜索条件。  

LIKE是谓词而不是搮作符  

#### 8.1.1 百分号 (%) 通配符

最常使用的通配符是百分号 (%).在搜索串中， ％表示任何字符出现
任意次数。  

```
SELECT prod_id , prod_name
FROM products
WHERE prod.nante LIKE 'jet5％’ ;
```

==搜索是区分大小写的==

注意尾空格  如 果 它 后 面 有 一 个 或 多 个 空 格， 則子句将不会匹配。

注意NULL 虽然似乎％ 配符可以匹配任何东西， 但有一个例外， 即NULL。   

#### 8.1.2 下划线(__)通配符  

下划线只匹H5单个字符而不是多个字符  

### 8.2 使用通配符的技巧  

在确实需要使用通配符时， 除非绝对有必要， 否则不要把它们用
在搜索模式的开始处。 把通配符置于搜索模式的幵始处， 搜索起
来是最慢的。 

## 9 用正则表达式进行搜索 

### 9.2.1 基本字符匹配  

REGEXP后所跟的东西作为正则表达式（ 与文字正文1000匹配的一个正则表&式） 处理 。

.是正则表达式语言中一个特殊的字符。 它表示匹配任意一个字符  

```
SELECT prod_name
FROM products
WHERE prod
ORDER BY prod ^name_name REGEXP ;
```

LIKE匹配整个列。 如果被匹配的文本在列值中出现， LIKE将不会找到它， 相应的行也不被返回（ 除非使用 通 配 符 而REGEXP在列值内进行匹配， 如果被匹配的文本在列值中出现， REGEXP将会找到它， 相应的行将被返回.这是一个非常重要的差别  

==匹配不区分大小写==

### 9.2.2 进行OR匹配

为搜索两个串之一 （或者为这个串，或者为另一个串），使用丨，如下：

```
SELECT prod—name
FROM products
WHERE prod_name REGEXP '1000|2000|3000 *
ORDER BY prod_name
```

### 9.2.3 匹配几个字符之一  

匹配任何单一字符。 只匹配特定的字符，可通过指定一组用[ 和]括起来的字符来完成。

```
SELECT FROM products prod_name
WHERE prod.name REGEXP '[123] Ton'/REGEXP '1|2|3 Ton'
ORDER BY prod_name;
```

它的意思是匹配1或2或3 ,事实上， 正则表达式 [ 123】 Ton
为 [ 1 | 2 | 3 ]Ton的缩写， 也可以使用后者。  

### 9.2.4 匹配范围  

[0123456789]
为简化这种类型的集合， 可使用-来定义一个范围。 下面的式子功能
上等同于上述数字列表：
[0-9]  

此外， 范围不一定只是数值的， [ a- z 】 匹配任意字母字符。   

### 9.2.5 匹配特殊字符  

我们己经看到_ 、[ ] 、|和-等， 还有其他一些字符。 请问， 如果你需要匹配这些字符， 应该怎么办呢？ 例如， 如果要找出包含.字符的值， 怎样搜索？  

为了匹配特殊字符， 必须用\ \ 为前导。  \ \\- 表示査找 -   

![image-20220407213500410](MySQL必知必会.assets/image-20220407213500410.png)

匹配\ :为了匹配反斜杠（ \ ) 字符本身， 需要使用 \\ \ \.

\或 \ \?: 多数正则表达式实现使用单个反斜杠转义特殊字符， 以便能使用这些字符本身。 但MySQL要求两个反斜杠( MySQL自己解释一个， 正则表达式库解释另一个).

### 9.2.6 匹配字符类  

存在找出你自己经常使用的数字、 所有字母字符或所有数字字母字
符等的匹配。 为更方便工作， 可以使用预定义的字符集， 称为字符类
( character class)。 表9-2列出字符类以及它们的含义。  

![image-20220407213651557](MySQL必知必会.assets/image-20220407213651557.png)

### 9.2.7 匹配多个实例  

有时需要对匹配的数目进行更强的控制。 例如， 你可能需要寻找所有的数， 不管数中包含多少数字， 或者你可能想寻找一个单词并且还能够适应一个尾 随的s (如果存在)， 等等 。

这可以用表9-3列出的正则表达式重复元字符来完成 。

![image-20220408002615782](MySQL必知必会.assets/image-20220408002615782.png)

举几个例子 

```
mysql> SELECT prod_name
    -> FROM products
    -> WHERE prod_name REGEXP '\\([0-9] sticks?\\)'
    -> ORDER BY prod_name;
+----------------+
| prod_name      |
+----------------+
| TNT (1 stick)  |
| TNT (5 sticks) |
+----------------+
2 rows in set (0.01 sec)
```

正则表达式`\ \([0\- 9 ] StickS?\ \)`需要解说一下。 `\ \`(匹配） ，[ 0-9] 匹配任意数字（ 这个例子中为1和5 )， sticks?匹配stick和sticks (s后的?使s可选，因为？匹配它前面的任何字符的0次或1次出现）， \ \ ) 匹配） 。 没有？， 匹配stick和sticks会非常困难。 

```
mysql> SELECT prod_name FROM products WHERE prod_name REGEXP '[[:digit:]]{4}' ORDER BY prod_name;
+--------------+
| prod_name    |
+--------------+
| JetPack 1000 |
| JetPack 2000 |
+--------------+
2 rows in set (0.00 sec)

```

[[:digit:]]{4}匹配连在一起的任意4位数字 

###  9.2.8 定位符

目前为止的所有例子都是匹配一个串中任意位置的文本。  为了匹配特定位置的文本， 需要使用表9-4列出的定位符。  

![image-20220408005540417](MySQL必知必会.assets/image-20220408005540417.png)



```
where prod_name REGEXP '^[0-9\\.]'
```

^匹配串的开始。 因此， '^[0-9\\.]'只在.或任意数字为串中第
一个字符时才匹配它们。  

## 10 创建计算字段  

### 10.1 计算字段

存储在数据库表中的数据一般不是应用程序所需要的格式。 

我们需要直接从数据库中检索出转换、 计算或格式化过的数据； 而不是检索出数据， 然后再在客户机应用程序或报告程序中重新格式化 。

计算字段并不实际存在于数据库表中。 计算字段是运行时在SELECT语句内创建的。  

==字段 (field)==： 基本上与列（ column ) 的意思相同， 经常互换使
用， 不过数据库列一般称为列， 而术语字段通常用在计算字段的
连接上。  

### 10.2 拼接字段  

拼接（concatenate)： 将值联结到一起构成单个值。  

MySQL的不同之处多数DBMS使用 +或丨 |来实现拼接，
MySQL則使用==Concat( )==函数来实现。

![image-20220408142050932](MySQL必知必会.assets/image-20220408142050932.png)

Concat( )拼接串， 即把多个串连接起来形成一个较长的串 .

通过删除数据右侧多余的空格来整理数据， 这可以使用MySQL的RT rim( )函数来完成 。

![image-20220408142323627](MySQL必知必会.assets/image-20220408142323627.png)

使用别名  AS

### 10.3 执行算术计算 

+-*/

## 11 使用数据处理函数  

### 11.1 函数  

### 11.2 使用函数  

大多数SQL实现支持以下类型的函数。
□ 用于处理文本串（ 如删除或填充值， 转换值为大写或小写） 的文本函数。
□ 用于在数值数据上进行算术操作（ 如返回绝对值， 进行代数运算）
的数值函数，
□ 用于处理日期和时间值并从这些值中提取特定成分（ 例如， 返回
两个日期之差， 检查日期有效性等） 的日期和时间函数。
□ 返回DBMS正使用的特殊信息（ 如返回用户登录信息， 检查版本
细节） 的系统函数    

#### 11.2.1 文本处理函数  

Upper( )将文本转换为大写  

![image-20220408201853263](MySQL必知必会.assets/image-20220408201853263.png)

![image-20220408202000233](MySQL必知必会.assets/image-20220408202000233.png)SOUNDEX是一个将任何文本串转换为描述其语音表示的字母数字模式的算法。SOUNDEX考虑了类似的发音字符和音节， 使得能对串进行发音比较而不是字母比较。 虽然SOUNDEX不是SQL概念。

使用Soundex0函数进行搜索， 它匹配所有发音类似于
Y.Lie的联系名。

```
mysql> SELECT cust_name,cust_contact FROM customers WHERE Soundex(cust_contact)=Soundex('Y Lie');
+-------------+--------------+
| cust_name   | cust_contact |
+-------------+--------------+
| Coyote Inc. | Y Lee        |
+-------------+--------------+
1 row in set (0.00 sec)
```

### 11.2.2 日期和时间处理函数  

![image-20220408205151912](MySQL必知必会.assets/image-20220408205151912.png)

```
SELECT cust_id p order_num
FROM orders
WHERE Date(order_date) = '2005-09-01';
```

如果要的是日期 则使用Date( )是一个良好的习惯.

### 11.2.3 数值处理函数  

![image-20220408213042488](MySQL必知必会.assets/image-20220408213042488.png)

## 12 汇总数据

###   12.1 聚集函数  

![image-20220408213638879](MySQL必知必会.assets/image-20220408213638879.png)

### 12.2 聚集不同值  

指定DISTINCT参数

AVG(DISTINCT prod_price)

## 13 分组数据

### 13.1 数据分组  

### 13.2 创建分组  

GROUP BY子句  

HAVING子句  

HAVING和WHERE的差别这里有另一种理解方法， WHERE在数据分组前进行过滤， HAVING在数据分组后进行过滤。 这是一个重要的区别， WHERE排除的行不包括在分组中。 这可能会改变计算值， 从而影响HAVING子句中基于这些值过滤掉的分组。

### 13.4 分组和排序  

虽然GROUP BY和ORDER BY经常完成相同的工作， 但它们是非常不
同的 .

![image-20220409020343580](MySQL必知必会.assets/image-20220409020343580-16494410249251.png)

## 14 使用子查询

### 14.1 子查询  

SQL还允许创建子查询（ subquery ) , 即嵌套在其他查询中的查询  

### 14.2 利用子查询进行过滤  

```
SELECT cust_id
FROM orders
WHERE order_num IN (SELECT order_num
FROM orderitems
WHERE prod_id='TNT2');
```

格式化SQL 包含子查询的SELECT语句难以阅读和调试,特别是它们较为复杂时更是如此。 如上所示把子查询分解为多行并且适当地进行缩进， 能极大地简化子查询的使用。

### 14.3 作为计算字段使用子查询  

```
mysql> SELECT cust_name,cust_state,
    -> (SELECT COUNT(*)
    -> FROM orders
    -> WHERE orders.cust_id=customers.cust_id) AS orders
    -> FROM customers
    -> ORDER BY cust_name;
+----------------+------------+--------+
| cust_name      | cust_state | orders |
+----------------+------------+--------+
| Coyote Inc.    | MI         |      2 |
| E Fudd         | IL         |      1 |
| Mouse House    | OH         |      0 |
| Wascals        | IN         |      1 |
| Yosemite Place | AZ         |      1 |
+----------------+------------+--------+
5 rows in set (0.01 sec)

```

相关子查询 （ correlated subquery) : 涉及外部査询的子查询。  

## 15 联 结 表  

### 1 5 . 1 联 结  

#### 15.1.1 关系表

 外键 (foreign key) 外键为某个表中的一列， 它包含另一个表
的主键值， 定义了两个表之间的关系。  

#### 15.1.2 为什么要使用联结  

分解数据为多个表能更有效地存储， 更方便地处理， 并且具有更大的可伸缩性。 但这些好处是有代价的。如果数据存储在多个表中， 怎样用单条SELECT语句检索出数据？答案是使用联结。

### 15.2 创建联结  

```
WHERE vendors •vend_id = products . vend_id
```

两个表用WHERE子句正确联结， WHERE子句指示MySQL匹配vendors表中的vend_id和products表中的vend_id。

#### 15.2.1 WHERE子句的重要性  

笛卡儿积（cartesian product) ：由没有联结条件的表关系返回的结果为笛卡儿积。 检索出的行的数目将是第一个表中的行数乘以第二个表中的行数。

#### 15.2.2 内部联结  

目前为止所用的联结称为等值联结 (equijoin)  

```
mysql> SELECT vend_name,prod_name,prod_price
    -> FROM vendors INNER JOIN products
    -> ON vendors.vend_id = products.vend_id;
+-------------+----------------+------------+
| vend_name   | prod_name      | prod_price |
+-------------+----------------+------------+
| Anvils R Us | .5 ton anvil   |       5.99 |
| Anvils R Us | 1 ton anvil    |       9.99 |
| Anvils R Us | 2 ton anvil    |      14.99 |
| LT Supplies | Fuses          |       3.42 |
| LT Supplies | Oil can        |       8.99 |
| ACME        | Detonator      |      13.00 |
| ACME        | Bird seed      |      10.00 |
| ACME        | Carrots        |       2.50 |
| ACME        | Safe           |      50.00 |
| ACME        | Sling          |       4.49 |
| ACME        | TNT (1 stick)  |       2.50 |
| ACME        | TNT (5 sticks) |      10.00 |
| Jet Set     | JetPack 1000   |      35.00 |
| Jet Set     | JetPack 2000   |      55.00 |
+-------------+----------------+------------+
14 rows in set (0.01 sec)
```

## 16  创建高级联结  

### 16.1 使用表别名  

### 16.2 使用不同类型的联结  

#### 16.2.1 自联结

假如你发现某物品（ 其ID为DTNTR)存在问题， 因此想知道生产该物
品的供应商生产的其他物品是否也存在这些问题。 此查询要求首先找到
生产ID为DTNTA的物品的供应商， 然后找出这个供应商生产的其他物品。
下面是解决此问题的一种方法：  

```
SELECT prod_id, prod_name
FROM products
WHERE vend_id=(SELECT vend_id
FROM products
WHERE prod_id='DTNTR');
```

#### 16.2.2 自然联结  

标准的联结（ 前一章中介绍的内部联结） 返回所有数据， 甚至相同的列多次出现。 自然联结排除多次出现， 使每个列只返回一次 .

事实上， 迄今为止我们建立的每个内部联结都是自然联结 .

#### 16.2.3 外部联结  

在使用OUTER JOIN语法时， 必须使用RIGHT或LEFT
关键字指定包括其所有行的表（RIGHT指出的是OUTER JOIN右边的表，
而LEFT指出的是OUTER JOIN左边的表）  使用LEFT OUTER
JOIN从FROM子句的左边表（ customers表） 中选择所有行。  

## 17 组合查询

UNION操作符将多条SELECT语句组合成一个结果集。

### 17.1 组合查询  

### 17.2 创建组合查询  

#### 17.2.1 使用UNION  

举一个例子， 假如需要价格小于等于5的所有物品的一个列表， 而且
还想包括供应商1001和1002生产的所有物品（ 不考虑价格).当然， 可
以利用WHERE子句来完成此工作， 不过这次我们将使用UNION。
正如所述， 创建UNION涉及编写多条SELECT语句。  

```
SELECT vend_id, prod_id, prod_price
FROM products
WHERE prod_price <= 5
UNION
SELECT vend_id, prod_idf prod_price
FRW products
WHERE vend_id IN (1001,1002);
```

使用UNION可能比使用WHERE子句更为复杂。但对于更复杂的过滤条件， 或者从多个表（ 而不是单个表） 中检索数据的情形， 使用UNION可能会使处理更简单 .

#### 17.2.2 UNION规则  

□ UNION必须由两条或两条以上的SELECT语句组成， 语句之间用关键字UNION分隔（因此， 如果组合4条SELECT语句， 将要使用3个UNION关键字）。
□ UNION中的每个査询必须包含相同的列、 表达式或聚集函数（ 不过各个列不需要以相同的次序列出）。
□ 列数据类型必须兼容： 类型不必完全相同， 但必须是DBMS可以隐含地转换的类型（例如， 不同的数值类型或不同的日期类型)。如果遵守了这些基本规则或限制， 则可以将并用于任何数据检索任务。

#### 17.2.3 包含或取消重复的行  

 UNION从査询结果集中==自动去除了重复的行==（换句话说， 它的行为与
单条SELECT语句中使用多个WHERE子句条件一样)。

这是UNION的默认行为， 但是如果需要， 可以改变它。 事实上， 如果
想返回所有匹配行， 可使用==UNION ALL==而不是UNION。  

#### 17.2.4 对组合查询结果排序  

只能使用一条ORDER BY子句， 它必须出现在最后一条SELECT语句之后,不允许使用多条ORDER BY子句 。

18 
