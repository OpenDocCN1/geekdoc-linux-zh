

PEAR::DB 是面向对象的，你在创建初始 DB 对象时同时指定连接详情。这是通过类似 URL 的系统完成的，该系统将数据库服务器类型、用户名、密码、服务器和数据库名称全部放在一起。指定数据库服务器后，其余部分都被抽象化，这意味着你只需更改连接行即可将代码移植到另一台数据库服务器。

此第一个脚本连接到我们的服务器并打印状态消息（参见清单 25.6）。

## LISTING 25.6 Connecting to a Database Through PEAR::DB

```
<?php

include("DB.php");
$dsn = "mysql://ubuntu:alm65z@10.0.0.1/dentists";
$conn = DB::connect($dsn);

if (DB::isError($conn)) {
    echo $conn->getMessage() . "\n";
} else {
    echo "Connected successfully!\n";
}
?>
```

你应该能够看出连接字符串是如何分解的。它首先是服务器名称，然后是用户名和密码用冒号分隔，然后是 @ 符号，后跟要连接的 IP 地址，然后是斜杠和数据库名称。请注意 connect 的调用是 DB::connect()，它直接调用 PEAR::DB 并返回一个数据库连接对象以存储在 $conn 中。变量名 $dsn 用于连接详情，因为它是 data source name 的常用缩写。

如果 DB::connect() 成功连接到服务器，它会返回一个数据库对象，我们可以用它来运行 SQL 查询。如果没有，我们会得到一个错误返回，我们可以使用 getMessage() 等函数进行查询。在之前的脚本中，如果连接失败，我们会打印错误消息，但如果成功，我们也会只打印一条消息。接下来，我们将更改它，以便在有连接时运行 SQL 查询。

运行 SQL 查询是通过数据库连接的 query() 函数完成的，将我们想要执行的 SQL 作为参数传入。这随后返回一个查询结果，可用于获取数据。可以将此查询结果视为多维数组，因为它包含许多数据行，每行都有许多属性列。这是通过 fetchInto() 函数提取的，该函数循环遍历查询结果，将一行数据转换为数组并将其作为返回值发送回来。你需要向 fetchInto() 传入两个参数，指定数据应存储的位置以及如何存储。除非你有特殊需求，否则为第二个参数指定 DB_FETCHMODE_ASSOC 是一个明智的选择。

## LISTING 25.7 Running a Query Through PEAR::DB

```
<?php

include("DB.php");
$dsn = "mysql://ubuntu:alm65z@10.0.0.1/dentists";
$conn = DB::connect($dsn);

if (DB::isError($conn)) {
    echo $conn->getMessage() . "\n";
} else {
    echo "Connected successfully!\n";

    $result = $conn->query("SELECT ID, Name FROM patients;");

    while ($result->fetchInto($row, DB_FETCHMODE_ASSOC)) {
        extract($row, EXTR_PREFIX_ALL, 'pat');
        echo "$pat_ID is $pat_Name\n";
    }
}
?>
```

第一半部分与之前的脚本完全相同，所有新操作都在成功连接时发生。

遵循“不要把能自己清理的事情留给 PHP”的说法，当前脚本存在问题。我们没有清理查询结果，也没有关闭数据库连接。如果此代码在运行数分钟的较长脚本中使用，这将是资源的巨大浪费。幸运的是，我们可以通过调用 $result->free() 和 $conn->disconnect() 来释放这两个相关的内存。如果我们在脚本末尾添加这两个函数调用，它就完整了。

## Reference

PHP 如此受欢迎，在互联网上获得了大量报道。然而，最好的信息来源是 PHP 在线手册，网址为 http://www.php.net。它内容全面、写得很好，并且定期更新：

- http://www.phpbuilder.net—一个大型 PHP 脚本和教程网站，你可以在那里学习新技术并与其他 PHP 开发者聊天。
- http://www.zend.com—由两位 PHP 核心开发者创立的公司的主页。Zend 开发和销售专有软件，包括强大的 IDE 和代码缓存，以帮助 PHP 开发者。

