# MySQL基础操作

## 安装
TODO
## MySQL Shell
[MySQL Shell 使用教程](https://zhaodafei.github.io/2019/06/12/mysql/mysql_shell/)
[官方文档](https://dev.mysql.com/doc/mysql-shell/8.0/en/mysql-shell-getting-started.html)
Shell并不是直接使用SQL，而是一个功能更多的软件。
打开方式：在Windows cmd中输入`mysqlsh`。
主要命令：
1. 切换语言为SQL
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
6. 获得column的信息：
   ```sql
   show columns from table_name
   # 快捷方式
   DESCRIBE customers
   ```
