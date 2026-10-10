

如果使用的是可滚动游标，我们可以通过向获取结果集下一行的方法传递 `PDO::FETCH_ORI_NEXT` 常量来滚动游标。清单 8.30 提供了一个示例。

```php
$sql = "SELECT * FROM customer";
try {
    $offset = 0;
    $sth = $dbh->prepare($sql, array(PDO::ATTR_CURSOR, PDO::CURSOR_SCROLL));
    $sth->execute();
    while ($row = $sth->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT)) {
        $data = $row[0] . "\t" . $row[1] . "\t" . $row[2] . "\n";
        echo $data;
    }
    $sth->closeCursor();
} catch (PDOException $exp) {
    print_r($sth->errorInfo());
    echo 'Exception: ' . $exp->getMessage();
}
```

### 清单 8.30 – 使用可滚动游标

### 将数据获取到对象中

通过提供常量 `PDO::FETCH_LAZY` 和 `PDO::FETCH_OBJ`，您可以直接将数据获取到对象中。在 `PDO::FETCH_LAZY` 中，用于访问列的对象变量名会在访问时创建。我们可以通过列名或相应位置来引用列。清单 8.31 提供了一个示例。

```php
while ($row = $sth->fetch(PDO::FETCH_LAZY)) {
    print_r($row->C_NAME);
}
while ($row = $sth->fetch(PDO::FETCH_OBJ)) {
    print_r($row->C_NAME);
}
```

### 清单 8.31 – 使用 Fetch 引用列

#### 8.3.3.5 释放资源

每次执行完 fetch 操作后，都需要关闭游标，以便重用语句资源。用于关闭游标的方法是 `PDOStatement::closeCursor`。将连接资源分配给 null 值即可释放该资源。清单 8.32 提供了一个示例。

```php
// 连接到数据库，使用以下方法之一
// 对于 PDO_IBM
$dbh = new PDO('ibm:sample', '', '', '');
// 对于 PDO_ODBC
$dbh = new PDO('odbc:sample', '', '');
// 在此处执行数据库操作
...
// 释放连接
$dbh = null;
```

### 清单 8.32 – 释放连接资源

## 8.4 使用 PHP 优化 DB2 的使用

一旦您的 PHP 应用程序运行起来，您可以对应用程序和 DB2 都进行调优，以获得最佳性能。DB2 拥有一个高效的基于成本的优化器，确保您编写的每个查询都能根据您的环境以最佳方式执行。

### 8.4.1 提高 PHP-DB2 性能的设计注意事项

在设计和编码应用程序时，需要考虑以下几点：

- 使用 `prepare` 和 `execute` 方法来执行反复执行的 SQL 语句。
- 在 PDO 驱动程序中使用连接池，在 `ibm_db2` 驱动程序中使用持久连接，或在 DB2 中启用连接集中器。
- 只要逻辑允许，就频繁提交。这可以释放锁，从而提高并发度。
- 将更多逻辑推送到数据库层，并使用用户定义函数、存储过程和 SQL/XML，以减少网络流量并节省计算资源。
- 最优地利用可用的存储空间；将大表存储在分布在不同磁盘上的表空间中，并将 DB2 日志存储在不同的磁盘上。
- 使用 DB2 设计顾问有效地为表列创建索引。
- 使用配置顾问向导更改您的数据库和数据库管理器配置，以针对您的环境优化 DB2。
- 定期对所有表和系统目录表运行 `RUNSTATS`。
- 如果可能，让缓冲区池使用 75% 的可用内存。
- 使用监控工具来监控 DB2 活动。
- 使用能满足应用程序数据完整性要求的最小限制隔离级别。

## 8.5 练习

在本练习中，我们将练习编写一个小 PHP 脚本以访问 SAMPLE 数据库中的数据。

在运行练习之前，请以实例所有者身份登录到服务器（例如 Linux 上的 db2inst1 或 Windows 上的 db2admin），然后：

1. 如果之前尚未创建 SAMPLE 数据库，请运行以下命令创建该数据库：`db2samp1`
2. 编写一个 PHP 脚本，向 EMPLOYEE 表插入数据并从中检索数据。
3. 要在 Apache Web 服务器上运行 PHP 脚本，在 Windows 上，请将 PHP 文件 `db2employee.php` 复制到 `C:/Program Files/Apache Group/Apache2/htdocs` 目录中。
4. 练习的示例脚本包含在随书提供的脚本 `db2employee.php` 中。您可以适当修改脚本中的用户 ID、密码和主机，并使用以下 URL 通过 Web 浏览器测试以运行此 PHP 脚本：`http://localhost/db2employee.php`

## 8.6 摘要

在本章中，我们研究了如何为在 DB2 上运行的 PHP 应用程序设置环境。您学习了一些关于 PHP 和 DB2 应用程序开发的基本概念，包括使用 `ibm_db2` 扩展和 `pdo_ibm`/`pdo_odbc` 驱动程序通过 PHP 在 DB2 上准备和执行 SQL。

## 8.7 复习题

1. 使用 `db2_connect` 和 `db2_pconnect` 释放资源有什么区别？
2. 什么是连接池？在什么情况下它是有益的？
3. 如何在 Apache HTTP Server 2.x 中启用 PHP 支持？
4. 如何确定您的 PHP 安装环境的配置文件路径？
5. 要将之前为 Unified ODBC 编写的应用程序移植到 `ibm_db2`，需要遵循哪些步骤？
6. 以下与 `ibm_db2` 扩展一起使用的不同 FETCH 方法中，哪一项除外：
    - A. `db2_fetch_array`
    - B. `db2_fetch_assoc`
    - C. `db2_fetch_both`
    - D. `db2_fetch_column`
    - E. 以上都不是
7. `ibm_db2` 是什么？
    - A. 驱动程序
    - B. 扩展
    - C. 适配器
    - D. 数据对象
    - E. 以上都不是
8. 使用 PDO 的 SQL 存储过程使用以下哪种类型的参数？
    - A. INPUT
    - B. OUTPUT
    - C. EXECUTE
    - D. INOUT
    - E. 以上都不是
9. 以下哪个文件保存 PHP 的配置详细信息？
    - A. `httpd.conf`
    - B. `php_conf`
    - C. `php.ini`
    - D. `httpd.ini`
    - E. 以上都不是
10. 就安全性和性能而言，执行 SQL 语句的最佳方式是什么？
    - A. 先准备然后执行
    - B. 执行
    - C. 准备
    - D. 同时准备和执行
    - E. 以上都不是

## 第 9 章 – 使用 Perl 进行应用程序开发

*Perl*（*Practical Extraction and Reporting Language*，实用提取和报告语言）是一种平台无关的、解释型脚本语言，它是免费的，并随许多操作系统提供，例如 Windows、Linux、UNIX 和 Mac OS X。作为一种开源语言，Perl 解释器可以免费下载源码或二进制形式。

由于其强大的文本处理功能，例如对正则表达式的强大支持，Perl 不仅被广泛用于报表生成应用程序，还被用于独立或基于 Web 的数据库应用程序。您可以轻松生成动态 SQL 查询，并使用 Perl 脚本获取和处理返回的数据。

在本章中，您将了解：

- 设置 Perl 环境以配合 DB2 工作
- 从 Perl 应用程序连接到 DB2 数据库
- 开发访问 DB2 数据的 Perl 应用程序

> **注意：**
> 如果您是 Perl 编程语言的新手，请回顾本系列图书中免费电子书 *Getting Started with Perl*（Perl 入门）的内容。

### 9.1 Perl - DB2 应用程序：宏观视角

Perl 应用程序使用 *Perl Database Interface*（*Perl 数据库接口*，*DBI*）来访问大多数关系数据库，包括 DB2。Perl DBI 是一个开放标准应用程序编程接口（API），它使 Perl 应用程序能够在不了解每个特定数据库细节的情况下，使用相同的语法访问不同的数据库。这些细节由底层由支持 Perl DBI 的数据库供应商提供的 *DataBase Drivers*（*数据库驱动*，*DBD*）处理。

*图 9.1* 展示了 Perl 脚本如何通过 DBI 模块和 DBD 驱动访问不同的数据库。

![](img/5f6ba170efa3a607142589708531bef8_320_0.png)

![](img/5f6ba170efa3a607142589708531bef8_321_0.png)

**图 9.1 - Perl 脚本使用 DBI 和 DBD 驱动访问数据库**

如 *图 9.1* 所示，DBI 模块提供了一个数据库独立接口，位于 Perl 应用程序和一个或多个数据库驱动模块之间。应用程序只需要知道该接口，而底层由数据库提供的 DBD 驱动将执行实际工作。对于 Perl - DB2 应用程序，驱动是 *DBD::DB2* 驱动，它提供了访问 DB2 数据库所需的详细信息。

由于 Perl DBI 模块定义了标准的数据库访问接口，您可以轻松地将用 DBI 编写的访问某个 DBMS（如 Oracle）的应用程序移植到访问另一个 DBMS（如 IBM DB2）。此外，Perl DBI 模块使用的接口与 ODBC 和 JDBC 接口非常相似，这使得将用 DBI 编写的 Perl 应用程序移植到 ODBC 和 JDBC 接口（或反之）变得容易。

> 注意：
> 有关 Perl DBI 的更多信息，请参阅 http://dbi.perl.org/
> 要获取最新的 DBD::DB2 驱动及相关信息，请访问 http://www.ibm.com/software/data/db2/perl/ 和 http://search.cpan.org/~ibmtordb2/

### 9.2 设置环境

为了从 Perl 应用程序访问 DB2 数据库，您需要设置一个能与 DB2 协同工作的 Perl 环境。需要以下 3 个步骤：

1. 安装 Perl 语言环境

