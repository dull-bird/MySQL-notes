# MySQL 基础操作

## 安装

可以直接安装在自己的电脑上。

[下载地址](https://dev.mysql.com/downloads/mysql/)

### 安装教材配套数据集

1. 下载[数据集](https://forta.com/wp-content/uploads/books/0672327120/mysql_scripts.zip)。
2. 启动 Windows cmd，输入`mysqlsh`，进入 MySQL Shell.
3. 连接到服务器，输入`create database crashcourse`，创建一个名为`crashcourse`的数据库。
4. 执行 create.sql 脚本`source \path\to\create.sql`。注意需要指定绝对路径。
5. 执行 populate.sql 脚本。

## MySQL Shell

[MySQL Shell 使用教程（博客）](https://zhaodafei.github.io/2019/06/12/mysql/mysql_shell/)

[官方文档](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-getting-started.html)

Shell 并不是直接使用 SQL，而是一个功能更多的软件。

打开方式：在 Windows cmd 中输入`mysqlsh`。

主要命令：

1. 切换语言为 SQL
   ```shell
   \sql
   ```
2. 连接到数据库
   ```shell
   \connect root@localhost:3306
   ```
3. 查看当前数据库
   ```SQL
   SHOW databases
   ```
4. 切换数据库
   ```SQL
   USE crashcourse
   ```
5. 获得数据库内表的列表：
   ```SQL
   SHOW TABLES
   ```
6. 获得 column 的信息：
   ```sql
   show columns from table_name
   # 快捷方式
   DESCRIBE customers
   ```

## 教材数据集一览

安装好数据集后，使用下面的命令查看所有的表名：

```sql
use crashcourse
show tables
```

```
+-----------------------+
| Tables_in_crashcourse |
+-----------------------+
| customers             |
| orderitems            |
| orders                |
| productnotes          |
| products              |
| vendors               |
+-----------------------+
```

给定一个 table_name，可以查看整个表的信息：

```sql
select * from table_name
```

- `customers`

```
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
| cust_id | cust_name      | cust_address        | cust_city | cust_state | cust_zip | cust_country | cust_contact | cust_email          |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
|   10001 | Coyote Inc.    | 200 Maple Lane      | Detroit   | MI         | 44444    | USA          | Y Lee        | ylee@coyote.com     |
|   10002 | Mouse House    | 333 Fromage Lane    | Columbus  | OH         | 43333    | USA          | Jerry Mouse  | NULL                |
|   10003 | Wascals        | 1 Sunny Place       | Muncie    | IN         | 42222    | USA          | Jim Jones    | rabbit@wascally.com |
|   10004 | Yosemite Place | 829 Riverside Drive | Phoenix   | AZ         | 88888    | USA          | Y Sam        | sam@yosemite.com    |
|   10005 | E Fudd         | 4545 53rd Street    | Chicago   | IL         | 54545    | USA          | E Fudd       | NULL                |
+---------+----------------+---------------------+-----------+------------+----------+--------------+--------------+---------------------+
```

- `orderitems`

```
+-----------+------------+---------+----------+------------+
| order_num | order_item | prod_id | quantity | item_price |
+-----------+------------+---------+----------+------------+
|     20005 |          1 | ANV01   |       10 |       5.99 |
|     20005 |          2 | ANV02   |        3 |       9.99 |
|     20005 |          3 | TNT2    |        5 |      10.00 |
|     20005 |          4 | FB      |        1 |      10.00 |
|     20006 |          1 | JP2000  |        1 |      55.00 |
|     20007 |          1 | TNT2    |      100 |      10.00 |
|     20008 |          1 | FC      |       50 |       2.50 |
|     20009 |          1 | FB      |        1 |      10.00 |
|     20009 |          2 | OL1     |        1 |       8.99 |
|     20009 |          3 | SLING   |        1 |       4.49 |
|     20009 |          4 | ANV03   |        1 |      14.99 |
+-----------+------------+---------+----------+------------+
```

- `orders`

```
+-----------+---------------------+---------+
| order_num | order_date          | cust_id |
+-----------+---------------------+---------+
|     20005 | 2005-09-01 00:00:00 |   10001 |
|     20006 | 2005-09-12 00:00:00 |   10003 |
|     20007 | 2005-09-30 00:00:00 |   10004 |
|     20008 | 2005-10-03 00:00:00 |   10005 |
|     20009 | 2005-10-08 00:00:00 |   10001 |
+-----------+---------------------+---------+
```

- `productnotes`

```
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
| note_id | prod_id | note_date           | note_text                                                                                                                                                 |
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
|     101 | TNT2    | 2005-08-17 00:00:00 | Customer complaint: Sticks not individually wrapped, too easy to mistakenly detonate all at once. Recommend individual wrapping.                          |
|     102 | OL1     | 2005-08-18 00:00:00 | Can shipped full, refills not available. Need to order new can if refill needed.                                                                          |
|     103 | SAFE    | 2005-08-18 00:00:00 | Safe is combination locked, combination not provided with safe. This is rarely a problem as safes are typically blown up or dropped by customers.         |
|     104 | FC      | 2005-08-19 00:00:00 | Quantity varies, sold by the sack load. All guaranteed to be bright and orange, and suitable for use as rabbit bait.                                      |
|     105 | TNT2    | 2005-08-20 00:00:00 | Included fuses are short and have been known to detonate too quickly for some customers. Longer fuses are available (item FU1) and should be recommended. |
|     106 | TNT2    | 2005-08-22 00:00:00 | Matches not included, recommend purchase of matches or detonator (item DTNTR).                                                                            |
|     107 | SAFE    | 2005-08-23 00:00:00 | Please note that no returns will be accepted if safe opened using explosives.                                                                             |
|     108 | ANV01   | 2005-08-25 00:00:00 | Multiple customer returns, anvils failing to drop fast enough or falling backwards on purchaser. Recommend that customer considers using heavier anvils.  |
|     109 | ANV03   | 2005-09-01 00:00:00 | Item is extremely heavy. Designed for dropping, not recommended for use with slings, ropes, pulleys, or tightropes.                                       |
|     110 | FC      | 2005-09-01 00:00:00 | Customer complaint: rabbit has been able to detect trap, food apparently less effective now.                                                              |
|     111 | SLING   | 2005-09-02 00:00:00 | Shipped unassembled, requires common tools (including oversized hammer).                                                                                  |
|     112 | SAFE    | 2005-09-02 00:00:00 | Customer complaint: Circular hole in safe floor can apparently be easily cut with handsaw.                                                                |
|     113 | ANV01   | 2005-09-05 00:00:00 | Customer complaint: Not heavy enough to generate flying stars around head of victim. If being purchased for dropping, recommend ANV02 or ANV03 instead.   |
|     114 | SAFE    | 2005-09-07 00:00:00 | Call from individual trapped in safe plummeting to the ground, suggests an escape hatch be added. Comment forwarded to vendor.                            |
+---------+---------+---------------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------+
```

(有亮点)

- `products`

```
+---------+---------+----------------+------------+----------------------------------------------------------------+
| prod_id | vend_id | prod_name      | prod_price | prod_desc                                                      |
+---------+---------+----------------+------------+----------------------------------------------------------------+
| ANV01   |    1001 | .5 ton anvil   |       5.99 | .5 ton anvil, black, complete with handy hook                  |
| ANV02   |    1001 | 1 ton anvil    |       9.99 | 1 ton anvil, black, complete with handy hook and carrying case |
| ANV03   |    1001 | 2 ton anvil    |      14.99 | 2 ton anvil, black, complete with handy hook and carrying case |
| DTNTR   |    1003 | Detonator      |      13.00 | Detonator (plunger powered), fuses not included                |
| FB      |    1003 | Bird seed      |      10.00 | Large bag (suitable for road runners)                          |
| FC      |    1003 | Carrots        |       2.50 | Carrots (rabbit hunting season only)                           |
| FU1     |    1002 | Fuses          |       3.42 | 1 dozen, extra long                                            |
| JP1000  |    1005 | JetPack 1000   |      35.00 | JetPack 1000, intended for single use                          |
| JP2000  |    1005 | JetPack 2000   |      55.00 | JetPack 2000, multi-use                                        |
| OL1     |    1002 | Oil can        |       8.99 | Oil can, red                                                   |
| SAFE    |    1003 | Safe           |      50.00 | Safe with combination lock                                     |
| SLING   |    1003 | Sling          |       4.49 | Sling, one size fits all                                       |
| TNT1    |    1003 | TNT (1 stick)  |       2.50 | TNT, red, single stick                                         |
| TNT2    |    1003 | TNT (5 sticks) |      10.00 | TNT, red, pack of 10 sticks                                    |
+---------+---------+----------------+------------+----------------------------------------------------------------+
```

- `vendors`

```
+---------+----------------+-----------------+-------------+------------+----------+--------------+
| vend_id | vend_name      | vend_address    | vend_city   | vend_state | vend_zip | vend_country |
+---------+----------------+-----------------+-------------+------------+----------+--------------+
|    1001 | Anvils R Us    | 123 Main Street | Southfield  | MI         | 48075    | USA          |
|    1002 | LT Supplies    | 500 Park Street | Anytown     | OH         | 44333    | USA          |
|    1003 | ACME           | 555 High Street | Los Angeles | CA         | 90046    | USA          |
|    1004 | Furball Inc.   | 1000 5th Avenue | New York    | NY         | 11111    | USA          |
|    1005 | Jet Set        | 42 Galaxy Road  | London      | NULL       | N16 6PS  | England      |
|    1006 | Jouets Et Ours | 1 Rue Amusement | Paris       | NULL       | 45678    | France       |
+---------+----------------+-----------------+-------------+------------+----------+--------------+
```
