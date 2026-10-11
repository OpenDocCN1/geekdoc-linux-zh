
默认情况下，当 InnoDB 存储引擎的已分配存储空间用尽时，它会阻止向表中插入新数据。你需要手动扩展存储文件大小。

指定 autoextend 设置后，允许 InnoDB 存储引擎自动为文件分配更多空间。虽然这很方便，但在某些环境中也可能很危险。InnoDB 存储引擎会根据需求不断分配更多存储空间，直到服务器磁盘空间耗尽！

> 当你在 MySQL 应用程序中使用 InnoDB 存储引擎时，最好经常关注存储空间目录，以确保它没有占用完服务器的所有磁盘空间。

## 步骤 7：自定义 PHP 服务器

PHP 服务器的配置文件名为 php.ini，但它可能位于多个不同的位置。PHP 服务器按以下顺序检查的路径包括：

- 1. 在 Apache Web 服务器配置文件中由 PHPIniDir 指令指定的路径
- 2. 在名为 PHPRC 的系统环境变量中指定的路径
- 3. 存储 PHP 服务器可执行文件的文件夹
- 4. 默认 Web 服务器的文件夹
- 5. 操作系统文件夹，对于 Linux 来说就是 /usr/local/lib 文件夹

如果你不确定 PHP 服务器正在使用哪一个 php.ini 配置文件，可以在一个小的 PHP 程序中运行 `phpinfo()` 函数，例如：

```php
<?php
phpinfo();
?>
```

图 21–2 展示了在 Ubuntu 系统上运行 `phpinfo()` 函数的输出。

![](img/577d3bff979ee86b07f9836e0df274ce_429_0.png)

**图 21-2：** 在 Ubuntu 中 phpinfo() 函数的输出。

`phpinfo()` 函数显示每个配置设置的系统值，以及是否有任何设置被本地设置所覆盖。查找“Loaded Configuration File”条目，该条目显示了当前活动的 php.ini 文件的路径，以查看该文件在你的 PHP 服务器上的位置。

可想而知，php.ini 配置文件中有很多可用设置。你可能需要调整 PHP 服务器上的某些 php.ini 设置：

- `date.timezone`：定义 PHP 服务器的时区。必须使用在 https://php.net/manual/en/timezones.php 中定义的时区值。
- `display_errors`：定义 PHP 错误消息是否显示在网页上。此功能对于开发工作非常方便，但在生产服务器上应禁用。
- `error_reporting`：设置 PHP 服务器的错误报告级别。PHP 使用复杂的位模式来设置要显示的错误。它使用标签表示错误级别，并使用布尔按位运算符来组合这些级别；波浪号 (`~`) 表示 NOT（非）运算符。错误级别如下：
  - `E_ERROR`：致命运行时错误
  - `E_WARNING`：不会中断脚本的运行时警告
  - `E_PARSE`：解析语法错误
  - `E_NOTICE`：脚本遇到了可能成为错误并影响结果的情况
  - `E_CORE_ERROR`：阻止 PHP 启动的致命错误
  - `E_CORE_WARNING`：启动期间的非致命错误
  - `E_COMPILE_ERROR`：编译 PHP 代码时的致命错误
  - `E_COMPILE_WARNING`：编译期间的非致命错误
  - `E_USER_ERROR`：由你的 PHP 代码手动生成的致命错误消息
  - `E_USER_WARNING`：由你的 PHP 代码手动生成的非致命错误消息
  - `E_USER_NOTICE`：由你的 PHP 代码手动生成的通知消息
  - `E_STRICT`：PHP 检测到不符合 PHP 严格规则代码
  - `E_RECOVERABLE_ERROR`：你可以用 `try`-`catch` 块捕获的致命错误
  - `E_DEPRECATED`：PHP 解析器检测到不再受支持的代码
  - `E_USER_DEPRECATED`：由你的 PHP 代码手动生成的弃用错误
  - `E_ALL`：除 E_STRICT 之外的所有错误和警告
- `variables_order`：PHP 从 HTTP 会话中填充数据的顺序。G = GET，P = POST，C = Cookies，S = 系统变量。
- `short_open_tag`：确定是否可以使用 `< ?` 标签在你的 HTML 文档中标识 PHP 代码。
- `max_execution_time`：设置 PHP 程序运行前的时间限制（以秒为单位），超过该限制后 PHP 服务器将终止它。这对于停止陷入循环的程序非常有用！
- `memory_limit`：设置 PHP 服务器可以在物理服务器上分配内存的限制。这也帮助防止失控的程序拖垮整个 Web 服务器。

既然你已经创建了 Web 服务器开发环境，你可以开始考虑为你的应用程序编码了。

## 步骤 8：创建数据库环境

对于动态 Web 应用程序，你需要数据——即要在网页上显示的内容。在本示例中，我创建一个简单的员工数据库，列出一些员工及其薪资。请按照以下步骤在 MySQL 或 MariaDB 中构建示例数据库：

1. **使用 Terminal 或 Konsole 打开命令行会话。**
2. **通过输入以下命令启动 MySQL 或 MariaDB 控制台：**

   ```bash
   sudo mysql
   ```

   该控制台提供了一个命令行界面，用于与 MySQL 服务器交互。你可以从这里提交标准 SQL 语句或专门的 MySQL 命令。
3. **在 MySQL（或 MariaDB）提示符处，通过输入以下命令为应用程序创建数据库：**

   ```sql
   create database mytest;
   ```
4. **通过输入以下命令创建供应用程序登录数据库服务器使用的用户帐户：**

   ```sql
   create user 'test'@'localhost' identified by 'test';
   ```

   MySQL 服务器使用三部分信息来允许访问——用户 ID、密码和位置。此命令创建一个名为 *test*、密码为 *test* 的用户 ID，允许从本地计算机登录。
5. **通过输入以下命令授予应用程序用户帐户对数据库的权限：**

   ```sql
   grant all on mytest.* to 'test'@'localhost';
   ```

   此命令授予 *test* 用户帐户对 *mytest* 数据库中所有表的所有权限（当从本地计算机登录时）。

很好，现在你拥有了一个数据库和一个具有访问数据库表权限的用户帐户。现在你需要做的就是向数据库中放入一些数据！为此，请按照以下步骤操作：

1. **如果尚未打开，请使用 Terminal 或 Konsole 打开一个命令行会话。**
2. **启动 MySQL 或 MariaDB 控制台：**

   ```bash
   sudo mysql
   ```
3. **将 *mytest* 数据库设置为当前会话的默认数据库：**

   ```sql
   use mytest;
   ```

   MySQL 中 SQL 语句末尾的分号非常重要——它告诉 MySQL 语句已结束。如果你不小心漏掉它并按下回车，MySQL 会提示你继续该命令。
4. **通过输入以下命令创建名为 employees 的表：**

   ```sql
   create table employees (
       empid int not null,
       lastname varchar(30),
       firstname varchar(30),
       salary float,
       primary key (empid));
   ```

   在第一行之后按下回车键时，MySQL 会提示你继续输入语句。这有助于你将长的 SQL 语句分成易于阅读的部分。只是别忘了末尾的分号！
5. **通过输入以下命令在 employees 表中创建一些数据记录：**

   ```sql
   insert into employees values (1, 'Blum', 'Rich', 25000.00);
   insert into employees values (2, 'Blum', 'Barbara', 4500.00);
   insert into employees values (3, 'Blum', 'Katie Jane', 34500.00);
   insert into employees values (4, 'Blum', 'Jessica', 52340.00);
   ```

   你可以自由添加任意数量的数据记录！只是别忘了更改每条记录的 empid 值，因为它是表的主键，所以对于每条数据记录必须是唯一的。
6. **通过输入以下命令测试你的表：**

   ```sql
   select * from employees;
   ```

   SELECT 语句从 employees 表中检索数据。输出看起来像这样：

   ```text
   mysql> select * from employees;
   +----+----------+-----------+--------+
   | empid | lastname | firstname | salary |
   +----+----------+-----------+--------+
   |    1 | Blum | Rich | 25000 |
   |    2 | Blum | Barbara | 45000 |
   |    3 | Blum | Katie Jane | 34500 |
   |    4 | Blum | Jessica | 52340 |
   +----+----------+-----------+--------+
   4 rows in set (0.05 sec)

   mysql>
   ```

现在你的表中已有数据，准备好开始为你的 Web 应用程序编码了！

