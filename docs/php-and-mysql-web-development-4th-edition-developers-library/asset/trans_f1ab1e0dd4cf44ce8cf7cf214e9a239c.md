
执行该语句后，如果它修改了行数据，您可以通过调用 `rowCount()` 获取受影响的行数：

```php
$count = $sth->rowCount ();
```

如果该语句返回行数据，则适用 `fetch()` 和 `columnNum()` 等方法。要确定行数，请在获取行时对其进行计数。（`rowCount()`）仅适用于修改行数据的语句。

预处理语句提供了一些重要功能：

-   语句字符串可以包含占位符，而不是字面数据值。在准备语句后，在执行之前将特定的数据值绑定到占位符，PDO 会负责处理转义特殊字符或 NULL 值所需的任何操作。将值绑定到占位符有几种方法，如 9.1.7 节“使用占位符处理数据引号问题”中所述。
-   预处理语句可以反复执行。这避免了每次执行时的准备开销，这对于您计划多次执行的语句非常有用，因为它可以提供增强的性能。例如，要插入多行数据，您可以将 INSERT 语句 `prepare()` 一次。然后在循环中 `execute()` 该语句，每次循环迭代提供针对单个行数据的数据值，使用占位符将值绑定到语句中。

## 9.1.7 使用占位符处理数据引号问题

在 PHP 中构建 SQL 语句字符串时，就像在 C 和 Perl 等其他语言中一样，有必要了解引号问题。假设您正在构建一个用于向表中插入新行的语句。在语句字符串中，您可能需要对要插入到字符串列中的每个值加上引号：

```php
$last = 'O'Malley';
$first = 'Brian';
$expiration = '2013-09-01';
$stm = "INSERT INTO member (last_name, first_name, expiration)"
    . " VALUES ('$last', '$first', '$expiration')";
```

这里的问题是，带引号的值中有一个本身就包含引号（'O'Malley'），如果您将语句发送到 MySQL 服务器，这将导致语法错误。为了在 C 中处理此问题，我们可以调用 `mysql_real_escape_string()` 或 `mysql_escape_string()`。在 Perl DBI 脚本中，我们可以使用 `quote()`。PDO 具有数据库句柄 `quote()` 方法，可以实现相同的目标。例如，调用 `quote('O\'Malley')` 将返回 'O\\'Malley'。要在语句构建中使用 `quote()`，请将其返回的值直接插入到语句字符串中，不要自己额外添加引号：

```php
$last = $dbh->quote('O'Malley');
$first = $dbh->quote('Brian');
$expiration = $dbh->quote('2013-09-01');
$stm = "INSERT INTO member (last_name, first_name, expiration)"
    . " VALUES ('$last', '$first', '$expiration')";
```

不幸的是，与 DBI 中同名的功能相比，`quote()` 存在一些缺点，降低了其实用性：

-   并非所有驱动程序都实现了此功能，在这种情况下，它返回 FALSE 而不是带引号的字符串。
-   对于值为 NULL 的情况，您希望在语句字符串中插入单词“NULL”，而不添加任何周围的引号。但如果您将 NULL 传递给 `quote()`，它会返回空字符串 ('')。为了解决这个问题，您必须通过某种方式知道该值是什么，或者对其进行测试，并根据它是否表示 NULL 值进行不同的处理。这很快就会变得混乱。

由于这些缺陷，我建议避免使用 `quote()`，除非您确定您只处理非 NULL 的字符串值数据。一种更好的方法是使用预处理语句。然后您可以在 SQL 语句中指定占位符，让 PDO 为您处理所有的引号操作。要指示在准备 SQL 语句时数据值应放在哪里，请使用 `?` 字符作为占位符标记。然后在执行语句时，将数据值作为参数数组提供给该语句：

```php
$stmt = "INSERT INTO member (last_name, first_name, expiration) VALUES(?,?,?);";
$sth = $dbh->prepare($stmt);
$sth->execute(array('O'Malley', 'Brian', '2013-09-01'));
```

PDO 会处理字符串中特殊字符所需的任何操作，并正确处理非字符串值，如数字和 NULL。

提供数据值的另一种方法是在调用 `execute()` 之前使用 `bindValue()` 将它们逐个绑定到占位符：

```php
$stmt = "INSERT INTO member (last_name, first_name, expiration) VALUES(?,?,?);";
$sth = $dbh->prepare($stmt);
$sth->bindValue(1, 'O'Malley');
$sth->bindValue(2, 'Brian');
$sth->bindValue(3, '2013-09-01');
$sth->execute();
```

前面的示例使用了位置占位符：`?` 标记都是相同的，仅通过它们在语句字符串中的位置来区分。PDO 还支持命名占位符样式，其中占位符由一个前导冒号加名称组成。准备要执行的语句，然后向 `execute()` 传递一个关联数组值，将每个值绑定到相应的名称：

```php
$stmt = "INSERT INTO member (last_name, first_name, expiration)
VALUES(:last_name, :first_name, :expiration)";
$sth = $dbh->prepare($stmt);
$sth->execute(array(
':last_name' => 'O'Malley',
':first_name' => 'Brian',
':expiration' => '2013-09-01'
));
```

或者，在调用 `execute()` 之前将每个值绑定到其占位符名称：

```php
$stmt = "INSERT INTO member (last_name, first_name, expiration)
VALUES(:last_name, :first_name, :expiration)";
$sth = $dbh->prepare($stmt);
$sth->bindValue(':last_name', 'O\'Malley');
$sth->bindValue(':first_name', 'Brian');
$sth->bindValue(':expiration', '2013-09-01');
$sth->execute();
```

命名占位符的一个优点是，当参数数量很多时，更容易跟踪占位符与数据值之间的关联。

## 9.1.8 处理错误

在与 MySQL 交互时，安排处理错误是至关重要的。如果您假设每次调用都会成功，那么当确实发生错误时，弄清楚脚本为什么不工作将会困难得多。

当您通过调用 `new PDO()` 尝试连接到数据库服务器时，如果尝试失败，就会发生异常。假设尝试成功并且您获得了一个有效的数据库句柄，PDO 将根据 PDO 错误模式处理基于该句柄的后续操作错误。您可以按以下方式设置错误模式：

```php
$dbh->setAttribute (PDO::ATTR_ERRMODE, mode_value);
```

PDO 支持三种错误模式值：

-   `PDO::ERRMODE_SILENT`：PDO 除了为导致错误的对象设置错误信息外不做任何事情。这是默认的错误模式。
-   `PDO::ERRMODE_WARNING`：这与静默模式类似，但 PDO 除了设置错误信息外还会发出警告消息。
-   `PDO::ERRMODE_EXCEPTION`：PDO 在设置错误信息后引发异常。

在所有情况下，如果您知道发生错误的对象，您可以调用其 `errorCode()` 或 `errorInfo()` 方法来获取错误信息：

-   `errorCode()` 返回一个五字符的 SQLSTATE 值。返回值等于 `PDO::ERR_NONE`（“00000”）意味着“无错误”。
-   `errorInfo()` 返回一个包含三个元素的数组，包括 SQLSTATE 值以及驱动程序特定的代码和消息。对于 MySQL，后两个值是数字错误代码和描述性错误消息。

在静默或警告模式下，错误处理涉及检查每个可能失败的 PDO 操作的结果。例如：

```php
else if (!$sth->execute ())
    die ('Cannot execute statement: ' . $sth->errorCode () . "\n");
```

请注意，`errorCode()` 是使用发生错误的句柄调用的。`errorInfo()` 也是如此。

如果您启用异常，当 PDO 操作发生错误时，PHP 会抛出 `PDOException`。如果没有发生错误，则操作成功。否则，该异常会导致 PHP 终止您的脚本，除非您捕获该错误。为此，请将可能失败的代码放入 `try` 块中，将错误处理代码放入相应的 `catch` 块中：

```php
try
{
    # ... 执行数据库操作 ...
}
catch (PDOException $e)
{
    # ... 处理错误 ...
}
```

异常对象（示例中的 `$e`）有其自己的方法来提供错误信息：

-   `getCode()` 返回错误代码。
-   `getMessage()` 返回包含错误消息的字符串。

以下示例启用异常，并展示了在语句执行失败时如何显示错误信息：

```php
$dbh->setAttribute (PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
try
{
    $dbh->exec('DELETE FROM non_existent_table');
}
catch (PDOException $e)
{
    # 打印异常对象的错误信息
    print ('getCode value: ' . $e->getCode () . "\n");
    print ('getMessage value: ' . $e->getMessage () . "\n");
    # 打印数据库句柄的错误信息
    print ('errorCode value: ' . $dbh->errorCode () . "\n");
    print ('errorInfo value: ' . join ('.', $dbh->errorInfo ()) . "\n");
}
```

该示例显示异常对象（`$e`）的信息，也显示数据库句柄对象（`$dbh`）的信息。之所以在这里可能，是因为在 `try` 块中使用的唯一 PDO 句柄是 `$dbh`。如果您在 `try` 块中使用了多个句柄，那么在 `catch` 块中您将无法知道其中哪一个导致了错误，因此您只能依靠

