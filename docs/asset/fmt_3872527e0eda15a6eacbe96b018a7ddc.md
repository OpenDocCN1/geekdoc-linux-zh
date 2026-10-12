
如果你设置 `mysql_use_result` 属性，请在调用 `prepare()` 之后且在调用 `execute()` 之前进行设置：

```perl
$sth = $dbh->prepare ($stmt_str);
$sth->{mysql_use_result} = 1;
$sth->execute();
```

或者，执行以下操作：

```perl
$sth = $dbh->prepare ($stmt_str, { mysql_use_result => 1 });
```

- `$rv` = `$sth->{mysql_warning_count};`

执行语句期间生成的警告数量。

`mysql_warning_count` 是在 DBD::mysql 4.004 中引入的。

### H.4.6 动态属性

这些属性与最近使用的句柄相关联，在下述描述中由 `$h` 表示。它们应在调用设置它们的任何句柄方法后立即使用，并在调用重置它们的另一方法之前使用。

- `$rv` = `$DBI::err`;

  这与调用 `$h->err()` 相同。

- `$str` = `$DBI::errstr`;

  这与调用 `$h->errstr()` 相同。

- `$rows` = `$DBI::rows`;

  这与调用 `$h->rows()` 相同。

## H.5 DBI 环境变量

DBI 会参考下表 H.2 中列出的几个环境变量。除 `DBI_TRACE` 外，其余所有变量均由 `connect()` 方法使用。`DBI_DRIVER` 由 `data_sources()` 方法使用，而 `DBI_TRACE` 由 `trace()` 使用。

表 H.2 DBI 环境变量

| 名称 | 含义 |
| :--- | :--- |
| `DBI_DRIVER` | DBD 级驱动程序名称（MySQL 为 "mysql"） |
| `DBI_DSN` | 数据源名称 |
| `DBI_PASS` | 密码 |
| `DBI_TRACE` | 跟踪级别和/或跟踪输出文件 |
| `DBI_USER` | 用户名 |

# PHP API 参考

本附录描述了使用 PDO 扩展与 MySQL 交互的 PHP 脚本的应用程序编程接口 (API)。该 API 由一组用于与 MySQL 服务器通信并访问数据库的类和方法组成。

本附录中的示例仅为简短的代码片段。有关完整的客户端脚本及其编写说明，请参阅第 9 章，“使用 PHP 编写 MySQL 程序”。PHP 本身的参考手册可在 PHP 网站 http://www.php.net/ 上获取。

本附录使用 PHP 5.1 及更高版本中的类常量表示法来引用 PDO 常量（例如，`PDO::FETCH_NUM`）。对于 PHP 5.0，请使用全局常量表示法代替（例如，`PDO_FETCH_NUM`）。

## I.1 编写 PHP 脚本

PHP 脚本是包含 PHP 代码和非 PHP 内容（如 HTML）混合的纯文本文件。PHP 解释器解释该脚本以生成要作为输出发送给客户端的网页。非 PHP 内容在未经解释的情况下直接复制到输出中。PHP 代码被解释并被其生成的任何输出所取代。

PHP 以文本复制模式开始解释文件。你可以使用特殊的标签切换到 PHP 代码模式并退出，这些标签标志着 PHP 代码的开始和结束。PHP 理解四种类型的标签，尽管其中一些如果你希望使用它们，必须显式启用。实现这一点的一种方法是在 PHP 初始化文件 `php.ini` 中开启它们。此文件的位置因系统而异；在许多 Unix 系统中，它位于 `/usr/lib` 或 `/usr/local/lib` 中。在 Windows 上，请在 PHP 安装目录中查找。

PHP 理解以下标签样式：

- 默认样式使用 `<?php>` 和 `?>` 标签：

  - `<?php print ('Hello, world.'); ?>`

- 短标签样式使用 `<?` 和 `?>` 标签：

  - `<? print ('Hello, world.'); ?>`

此样式还允许使用 `<?=` 和 `?>` 标签作为快捷方式，用于在不使用 `print` 语句的情况下显示表达式的结果：

```php
<?= "Hello, world." ?>
```

可以通过 PHP 初始化文件中的指令启用短标签：

```ini
short_open_tag = On;
```

- 与 Active Server Page 兼容的样式使用 `<%` 和 `%>` 标签：

  ```asp
  <% print ("Hello, world."); %>
  ```

此样式还允许使用 `<%=` 和 `%>` 标签作为快捷方式，用于在不使用 `print` 语句的情况下显示表达式的结果：

```asp
<%= "Hello, world." %>
```

ASP 样式标签可以通过 PHP 初始化文件中的指令启用：

```ini
asp_tags = On;
```

- 如果你使用不理解其他标签的 HTML 编辑器，可以使用 `<script>` 和 `</script>` 标签：

  ```html
  <script language="php"> print ("Hello, world."); </script>
  ```

## I.2 PDO 类

本附录讨论了 PDO 扩展中的以下类：

- `PDO` 是主要类。类构造函数用于连接数据库服务器。它返回一个具有进一步与服务器交互方法的数据库句柄对象。

- `PDOStatement` 是语句句柄类，由 `PDO` 对象的 `query()` 和 `prepare()` 方法返回。语句句柄提供对语句结果的访问，例如语句元数据和结果集内容。

- `PDOException` 是 PDO 错误类。该类的对象支持在因发生 PDO 错误而抛出异常时获取诊断信息的方法。

## I.3 PDO 方法

以下描述讨论了可用的 PDO 方法，按与其关联的类进行组织。本附录的方法描述中反复出现某些对象名称，并具有以下约定含义：

- 数据库句柄方法使用 `$dbh` 对象调用。该对象通过调用 `PDO` 类构造函数 `new PDO()` 获得。

- 语句句柄方法使用由 `$dbh->prepare()` 或 `$dbh->query()` 返回的 `$sth` 对象进行调用。

- 异常对象由 `$e` 表示。

方法描述中指明了返回值和参数的数据类型。类型为 mixed 表示根据值的使用情况，该值可能具有不同的数据类型。

许多方法返回一个表示成功或失败的指示值。如果未启用 PDO 异常，此值将起作用，并且应当对其进行测试以确定方法结果。如果启用了 PDO 异常，方法错误会导致 PDO 抛出 `PDOException`，这可以通过使用 try/catch 结构来捕获。（参见 1.3.3 节，“`PDOException` 对象方法”（在线））

语法描述中的方括号（[ ]）表示可选参数。如果可选参数后跟 = value，则表示如果在方法调用中省略该参数，value 即为其默认值。

示例中的代码大部分以纯文本形式打印消息和查询结果。这样做的目的是使代码更易于阅读。然而，对于打算在 Web 环境中执行的脚本，如果输出可能包含 HTML 中的特殊字符（如 ‘<’、‘>’ 或 ‘&’），通常应使用 `htmlspecialchars()` 对输出进行编码。

在以下描述中，“SELECT 语句”一词应理解为 SELECT 语句或其他返回行的语句，例如 DESCRIBE、EXPLAIN 或 SHOW。

### I.3.1 PDO 类方法

`PDO` 类包含用于以下操作的方法：连接数据库服务器、准备和执行 SQL 语句，以及设置或获取连接属性。

#### `PDO::__construct([string $dsn [, string $username [, string $password [, array $options]]]])`

这是 `PDO` 构造函数，在调用 `new PDO()` 时执行。构造函数尝试连接数据库服务器，如果成功则返回一个代表数据库句柄的对象。如果发生错误，PHP 将抛出 `PDOException`：

```php
try {
    $dbh = new PDO("mysql:host=localhost;dbname=sampdb", "sampadm", "secret");
} catch (PDOException $e) {
    die($e->getMessage() . "\n");
}
```

要关闭连接，请将数据库句柄设置为 `NULL`：

```php
$dbh = NULL;
```

`$dsn` 参数代表数据源名称（DSN）。DSN 可以有几种形式：

- 驱动 DSN 以驱动名称和冒号开头，后跟可选的驱动特定参数。对于 **MySQL**，驱动 DSN 看起来像这样：

```text
mysql:host=host_name;dbname=db_name
```
