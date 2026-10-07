
改为包含 `db_pgsql.inc` 而不是 `db_mysql.inc`。

如果你使用了 PHPLib 的其他部分（例如 `Template` 类），建议在 `prepend.php3` 中包含它们。`local.inc` 文件是进行 PHPLib 自定义定制的地方。

## 对 PHPLib 进行定制

在大多数情况下，PHPLib 的基类并不被直接使用；你定义自己的类，并对其自定义以适应你的环境。PHPLib 自带了默认实现，我们将在后的代码示例中使用这些实现。这些实现对你的系统做了某些假设；例如，假设你使用的是 MySQL。如果这些假设不符合你的应用程序，`local.inc` 文件就是进行更改的地方；推荐的技术是创建一个扩展 `DB_Sql` 的新对象。通过这样做，你避免了在每个应用程序中设置这些配置变量——相反，你可以在类中定义它们。

# 第6章 使用 PHP 访问数据库

建议你根据自己的需求调整 `local.inc`，你至少应该更改 `Example_Session` 类的名称；它的名称被用作会话 cookie 的名称并在 GET 模式下通过 URL ——如果 `Example_Session` 现在你的 URL 中，看起来就不太专业。

## 数据库抽象

数据库抽象层是一个 API，用于提供一组函数，以一种与实现无关的方式处理多种数据库。通过更改数据库抽象层的后端，你可以轻松地从 MySQL 切换到 Oracle，例如。DBI（数据库接口）就是这样的一层，而 Perl 的 PHPLib 中最广为人知的特性之一就是其组织在 `DB_Sql` 类中的抽象层。

## 可移植性

对于专业的 Web 应用程序程序员来说，数据库抽象可能是很有用且重要的。每个应用程序的基础都是其数据模型，即包含在数据库中的用于通用用途的一组数据结构。虽然 PHP 支持大量的数据库，但每个数据库都有不同的编程接口（API）。使用这些原生 API 将无法实现独立于操作系统和数据库的开发——如果你想将应用程序从 MySQL 迁移到 Oracle，你必须准备好大量工作，除非你使用像 PHPLib 这样的抽象层。表 6.1 显示了数据库不同系统之间的差异。

| 描述 | MySQL | Oracle 7 |
| :--- | :--- | :--- |
| 连接 | `mysql_connect()` | `ora_logon()` |
| 查询 | `mysql_query()` 或 `mysql_db_query()` | `ora_parse()`, 然后 `ora_exec()` |
| 获取结果下一行 | 或 `mysql_fetch_array()` | 使用偏移量：`ora_columnname()`, `ora_getcolumn()` |
| 结果集中的行数 | `mysql_num_rows()` | 不可能，因为 Oracle 在知道结果集中总行数之前就开始返回行。 |
| 最后插入的主键 ID | `mysql_insert_id()` | PHP 函数中没有等效项。 |

## 数据库抽象

当然，你通常不会以每周为周期更换数据库，所以这对你来说可能意义不大。此外，如果你在使用 PHPLib 时没有在项目之初就做好计划，那么数据库之间的可移植性仅仅是一个梦想。现实表明，问题不在于迁移 API，而在于特定的数据库函数。只有通过接受不能使用 RDBMS 的特定特性，你才能创建可移植的数据库代码——但你会在代码中重新创建该特性，这可能导致应用程序更难维护且运行更慢。

如果你的目标是可移植的代码，PHPLib 可以让这项任务变得简单；例如，它具有内置的序列处理和简单的表锁机制，这些都是以独立于数据库的方式工作的。

## 调试模式

`DBSql` 类有一个调试模式，允许你看到发送到数据库的查询。要开启调试，只需在程序中使用后插入 `$db->Debug = true;`。

```php
define('DEBUG', true);
$db->Debug = true;
```

## 错误处理

PHPLib 负责处理函数可能产生的所有错误。在默认设置下，脚本会在遇到每个错误时停止。这可以通过更改变量 `$H_On_Error` 来控制，该变量默认设置为 `yes`。将此变量设置为 `report` 会导致库打印错误而不退出脚本。将将其设置为 `no` 则指示库忽略所有错误。

# 第6章 使用 PHP 访问数据库

错误消息应该是信息丰富的，并出现在根据网站身份调整的通用布局中。要将你的格式应用到错误消息，你可以创建一个扩展 `DB_Sql` 的新类并在那里覆盖 `haltmsg()` 函数。由于此函数控制错误消息的输出，通过这种方式很容易自定义：

```php
class test_db extends DB_Sql {
    function haltmsg($msg) {
        printf("Database Error: $msg<br>");
        printf("MySQL said: %s<br>", $this->Error);
    }
}
```

## DB_Sql 示例

一个简短的示例将向你展示如何使用 `Db_Sql` 类。列表 6.1 中的源代码连接到数据库并显示单个表的内容。它使用了 `local.inc` 中定义的 `Example_Db` 类，该类扩展了 `DB_Sql` 并形成了你如何创建自定义类的参考实现。为了简单起见，我们在下面的代码段在使用 PHPLib 分发包中的示例实现：

列表 6.1 使用 `DB_Sql` 的第一个示例：

```php
// 实例化 Example_Db 类
$db = new Example_Db;
// 连接到 RDBMS
$db->connect("test", "localhost", "root", "");
// 创建 SQL 语句
$sql = SELECT * FROM test';
// 执行查询
$db->query($sql);
// 遍历结果集
while($db->next_record()) {
    // 遍历 $db->Records 哈希表
    while(list($key, $value) = each($db->Record)) {
        // 只打印非数字索引
    }
}
```

```php
print(is_string($key) ? "<b>$key</b>: $value<br>" : "*");
```

```php
print('<p>');
}
```

第一行创建了 `DB_Sql` 类的新实例。默认情况下，该类定义在 `db_mysql.inc` 文件（在 `prepend.php3` 中加载），并使用 MySQL 作为数据库引擎。

下一步是连接数据库。例如，你必须将这些值更改为你的设置；在示例中，我们连接到本地上的 `test` 数据库，用户名为 `root` 且密码。你也可以使用各自的类变量显式地设置这些属性：

```php
$Db = new Example_Db;
$Db->Database = 'test';
$Db->Host = 'localhost';
$Db->User = 'root';
$Db->Password = '';
```

在调用 `$Db->query()` 时，PHPLib 会注意到尚未建立连接，并将使用之前在这些类变量中定义的值自动打开连接。

我们的示例继续使用 `$Db->query()`，它处理了向数据库发送查询所需的所有操作。它连接选择并处理可能发生的错误。如果我们设置了 `$Db->debug` 为 `true`，此函数将在将 SQL 查询发送到数据库之前输出该查询。

随后在 `while` 循环中调用了 `$Db->next_record()`。此函数从结果集中获取下一行，并将行返回到数组 `$Db->Record` 中。如果结果集中没有更多行，该函数将返回 `false` 并终止循环。

第二个循环遍历 `$Db->Record` 数组并输出字段及其对应的内容。该数组包含带有数字索引的内容（类似于默认用法下 `mysql_fetch_array()` 返回的数组）以及作为键的字段名，我们确保只输出索引为字段名的数组项。

将列表 6.1 中的 PHPLib 示例与列表 6.2 中的传统编程进行比较。它们的长度几乎相近，但 PHPLib 示例继承了我们之前提到 的所有优势。通过更改一个文件，你可以更改底层数据库层。你比另一个示例中拥有更强大的错误处理能力；通过更改一个类变量，你可以指示 PHPLib 在错误时停止、报告或忽略错误，而传统示例在错误时会退出。最后，也是同样的一点，我们内置了完整的调试支持。

# 第 6 章 使用 PHP 访问数据库

列表 6.2 传统编程示例。

```php
// 连接到 RDBMS
$link = mysql_connect('localhost', 'root', '') or die(mysql_error());
```

```php
// 选择数据库
$db = mysql_select_db('test') or die(mysql_error());
```

```php
// 创建 SQL 语句
$sql = "SELECT * FROM test";
```

```php
// 执行查询
$res = mysql_query($sql) or die(mysql_error());
```

```php
// 遍历结果集
while($row = mysql_fetch_array($res))
{
    // 遍历 $db->Records 哈希表
    while(list($key, $value) = each($row))
    {
        // 只打印非数字索引
        print(is_string($key) ? "<br>": $value."<br>");
    }
}
print("<p>");
```

注意一个可能的陷阱：每个每个应用程序应限制使用一个数据库。PHP 在一个脚本中处理不同数据库的访问有问题——特别是使用 MySQL 时。PHP 假设它可以静默重用使用相同用户名和密码建立的数据库连接。看下面的示例：

```php
$res_one = mysql_connect('localhost', 'root', '') or die(mysql_error());
$res_two = mysql_connect('localhost', 'root', '') or die(mysql_error());
```

你本以为这里有两个不同的连接标识符，对吧？并没有，因为 PHP 在第二次 `mysql_connect()` 调用中重用了已打开的连接。打印标识符 `$res_one` 和 `$res_two` 将为两个变量输出相同的资源标识符。这种行为的影响是，在一个连接上使用 `mysql_select_db()` 将改变另一个连接的上下文。这同样适用于 PHPLib 中的对象：为 `DB_Sql` 使用一个数据库而为会话数据使用另一个数据库会导致问题。遗憾的是，目前没有解决此办法。

## 会话

PHPLib 提供了与 PHP 内置会话管理库等效的功能；甚至函数名称通常也是相同的。虽然它在许多方面与 PHP 内部会话管理相似，但它并不完全相同。一个额外功能是自动回退模式（见下节）。

## 自动回退

默认情况下，会话管理通过 cookie 工作。如第 4 章“HTTP 与会话”所述，这是首选技术（当客户端支持时），它是会话 ID 传播中最简单的。但你可以通过更改变量 `$mode` 将其更改为 GET/POST 方法。`$mode` 变量定义了使用哪种方法作为会话 ID 传播的主要方法。可以是 `cookie` 或 `get`；默认值为 `cookie`。

PHPLib 在运行时提供自动回退。如果变量 `$fallback_mode` 设置为 `get`，当变量中指定的首选模式（通常是 `cookie`）不受客户端支持时，将使用 GET/POST 方法。将 `$mode` 设置为 `cookie` 并 `$fallback_mode` 设置为 `get` 是最合理的。

## 序列化器

在 PHP 3.0 中，你无法轻松地序列化对象。`serialize()` 函数无法正确保留类，也没有方法手动进行。PHP 3.0 对对象的支持缺少了一点：内省（introspection）。无法获取类名或其父类名。因此，PHPLib 需要使用变通方法；它要求类有两个额外值： `$classname` 和 `$persistent_slots`，分别包含类名和要序列化的类变量。由于 PHPLib 可以通过实例化创建类（`$class = new class;`）并存储在会话仓库中。当会话被激活时，此代码将使用 `eval()` 执行。PHPLib 使用相同的概念。注意：随着 PHP 4.0 的出现，这些变通方法不再需要了。PHP 4.0 拥有如 `get_class()` 和 `get_parent_class()` 等函数以实现更好的内省。而且序列化是透明的。

## 页面缓存

Session 类还允许你控制如何缓存页面。变量 `$allow_cache` 可以设置为 `no`、`private` 或 `public`。它的默认值取决于 PHPLib 的版本；例如在 7.2 版本中被设置为 `private`，在后续版本中被设置为 `no`。页面缓存机制与 4.0 提供的非常相似。

# 会话示例

在日常工作中，使用 PHPLib 会话对象就像使用 PHP 4.0 会话库一样简单。列表 6.3 中的示例反映了这一点；它的工作正如第 4 章示例所示：

```php
// 手动创建一个新实例
$sess = new Example_Session;
```

```php
// 会话
$sess->start();
```

```php
// 注册我们的会话变量
$sess->register("counter");
```

```php
// 初始化计数器
if(!isset($counter)) {
    $counter = 0;
}
```

```php
// 输出会话 ID 和计数器
printf("Our session ID is: %s<br>", $sess->id);
print("The counter value is: $%counter");
```

```php
// 计数器加一
$counter++;
```

```php
// 保存会话状态
$sess->freeze();
```
