
```perl
@row_ary    = $sth->fetchrow_array;
%ary_ref    = $sth->fetchrow_arrayref;
%hash_ref   = $sth->fetchrow_hashref;

%ary_ref    = $sth->fetchall_arrayref;
%hash_ref   = $sth->fetchall_arrayref ( \slice, $max_rows );
%hash_ref    = $sth->fetchall_hashref ( $key_field );

$rv   = $sth->rows;

$rc  = $dbh->begin_work;
$rc  = $dbh->commit;
$rc  = $dbh->rollback;

$quoted_string = $dbh->quote( $string );

$rc  = $h->err;
$str = $h->errstr;
$rv  = $h->state;

$rc  = $dbh->disconnect;
```

*上述概要仅列出了主要的方法和参数。*

## 15.4.3 如何使用 DBI

一旦通过 `use DBI` 语句将 DBI 模块加载到程序中，就只涉及五个步骤：连接数据库、准备查询、执行查询、获取结果以及断开连接。

要连接到 MySQL，请使用 `connect()` 方法。该方法通过指定数据库类型（MySQL、Oracle、Sybase、Sybase CSV 文件、Informix 等）、数据库名称、主机名、用户和密码，并附带一些用于指定错误处理和事务处理等的额外可选参数来工作。它返回一个数据库句柄（手册页中使用 $dbh，但您可以将其命名为任何有效的标量名称）。

一旦连接到 MySQL 数据库，您就拥有一个数据库句柄（指向数据库对象的引用）。现在，您可以通过准备并执行 SQL 语句来发送查询。这可以通过调用 `prepare()` 和 `execute()` 方法或使用 `do()` 方法来完成。`prepare()` 和 `execute()` 方法用于 SELECT 语句，而 `do()` 方法通常用于不返回结果集的 SQL 语句，如 INSERT、UPDATE 或 DELETE 语句。这些方法返回的内容取决于查询返回什么。例如，成功的 SELECT 查询返回结果集（在 DBI 手册页中表示为 $sth）；使用 `do()` 的成功 INSERT/UPDATE/DELETE 查询返回受影响的行数；而未成功的查询返回错误或 undef。大多数数据以字符串形式返回给 Perl 脚本，而空值则作为 undef 返回。

一旦查询被发送到数据库并返回结果集（指向结果对象的引用），您可以使用特殊方法（例如 `fetchrow_array()` 和 `fetchrow_hashref()`）来提取数据。这些方法分别将每条记录检索为 Perl 数组或 Perl 哈希引用。

最后，当您完成操作时，`finish()` 方法释放由 `prepare()` 方法返回的结果集，而 `disconnect()` 方法通过断开与数据库的连接来结束会话。

现在我们将详细讲解这五个步骤。

### 15.4.4 连接和断开数据库

加载后，DBI 模块负责为给定数据库加载相应的驱动程序。然后，您将使用模块提供的方法（如 `perldoc DBI` 输出中列出的方法）与数据库进行交互。我们将使用的第一个方法是 `connect()` 方法，用于获取数据库连接，而最后一个方法 `disconnect()` 则用于断开连接。

以下示例展示了如何检查 DBI 的可用数据库驱动程序。

#### 示例 15.22

```perl
1 use DBI;
2 my @drivers = DBI->available_drivers;
3 print join(" ", @drivers), "\n";
```

（Windows 下的输出）
DBM, ExampleP, File, Gofer, Proxy, SQLite, Sponge, mysql

**`connect()` 方法。** `connect()` 方法建立与指定数据库的连接，并返回称为数据库句柄的对象。您可以在程序中使用多个 `connect` 语句对同一个数据库甚至不同的数据库进行多次连接。`connect()` 方法接受几个参数：

```perl
"dbi:$driver:$database,$port,$username,$password"
```

- 第一个参数是 DSN 字符串（Data Source Name，数据源名称），它是数据库的逻辑名称。定义数据源的任何属性都会分配给 DSN，供驱动程序检索。DSN 包含 DBI 模块的名称 `dbi`，后跟一个冒号和数据库驱动程序（MySQL、Sybase、Oracle），另一个冒号和要连接的实际数据库名称，以及/或主机名（默认为 `localhost`）、端口等，并以分号结束。
- 连接到数据库的下一个参数是用户名。
- 下一个参数是用户密码（可选）。
- 最后，有一个指向哈希的引用（用于错误处理、自动提交等的可选属性集合）。

#### 示例 15.23

```perl
1  $dbh=DBI->connect("dbi:RDBMS:database=", <username>, <password>,
                    \attributes) or die ("Couldn't connect");
2  $dbh=DBI->connect("DBI:mysql:sample_db","root",'quigley1') or
   die "Can't connect";
3  $dbh=DBI->connect('DBI:mysql:database=sample_db;user=root;
    password=quigley1') or die "Couldn't connect to sample_db"
    . DBI->errstr;

4  $dsn = dbi:mysql:northwind; $username="root"; $password="letmein";
   $dbh = DBI->connect($dsn, $user, $password,
      { PrintError => 0, RaiseError => 1, AutoCommit => 0 });
-----------------------使用其他数据库系统---------------------
5  $dbh = DBI->connect('dbi:Oracle:payroll', 'scott', 'tiger');
   $dbh = DBI->connect("dbi:Oracle:host=torch.cs.dal.ca;sid=TRCH";
                       $user, $password);
6  $dbh = DBI->connect('dbi:odbc:MSS_pubs', 'sa', '12mwm_1')
   (MS SQL Server)
```

#### 解释

- *connect* 方法将返回一个数据库句柄。这是您使用的连接格式。至少，您必须有 DSN 字符串，即模块名称 *dbi*、数据库驱动程序名称和数据库名称，表示为 <*database>*。用户名、主机名、密码和其他属性是可选的。
- 我们连接到名为 *sample_db* 的 *mysql* 数据库，登录名为 *root*，密码为 *quigley1*。
- *connect* 方法的参数，当作为单个字符串给出时，应放在同一行，且参数周围没有空格。*DBI->errstr* 返回无法连接的原因——

**`disconnect()` 方法。** 正如您可能在第 10 章“掌握文件句柄”中记得的那样，在使用用户定义的文件句柄打开文件后，我们在完成时使用内置的 `close` 函数关闭了它。除非是词法作用域的（`open` 的三段式参数），如果我们忘记关闭文件，那就得靠操作系统在 Perl 脚本退出时来关闭了。关闭数据库时也是一样的道理。在使用完数据库后，使用 `disconnect` 方法关闭连接始终是个好习惯。当然，由于数据库句柄是一个对象，一旦程序退出或对象超出作用域，Perl 会自动移除对它的引用。您可以像这样使用 `disconnect` 方法：

```perl
$dbh->disconnect();
```

## 15.4.5 准备语句句柄并获取结果

SQL `select` 语句可能是查询数据库时最常用的语句。在为数据库准备 `select` 语句时，查询作为字符串参数发送给 DBI 的 `prepare` 方法。查询就像您在 MySQL 控制台中输入的一样，只是没有分号。数据库句柄调用 `prepare` 方法。数据库确定如何执行查询（创建“计划”），DBI 返回一个包含查询执行细节的语句句柄。语句句柄（表示为 `$sth`）封装了在数据库中要执行的单个 SQL 语句，并调用 `execute` 方法。

这个 `execute` 方法告诉数据库*执行*该 SQL 语句（执行其“计划”），并将结果返回给程序。如果发生错误，将返回 *undef*。无论受影响的行数多少，成功的执行总是返回真，即使影响了零行也可以。可以创建和执行的语句句柄数量基本上没有限制。

尽管您已经执行了计划，但除非使用另一个 DBI 方法（如 `dump_results()`、`fetchrow_array()` 或 `fetch()`）来获取，否则您无法看到结果。

选择、执行并转储结果。DBI 的 `dump_results` 方法从语句句柄对象中获取所有行，并用一条简单的语句打印结果。在下面的示例中，我们将连接数据库，准备查询，执行查询并打印结果。

![](img/8556abcb353c0991f12099420ec28735_592_0.png)
