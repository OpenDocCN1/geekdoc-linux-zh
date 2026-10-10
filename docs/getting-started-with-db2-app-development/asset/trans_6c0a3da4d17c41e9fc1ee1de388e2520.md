

对于 pdo_ibm：
[DSN 别名，用于 pdo_db2]
pdo.dsn.dealerbase="ibm:sample"

对于 pdo_odbc：
[DSN 别名，用于 pdo_db2]
pdo.dsn.dealerbase="odbc:sample"

在 php.ini 文件中添加该条目后，我们即可如下所示，通过引用别名来连接数据库：

```php
$dbh = new PDO("dealerbase");
```

## 8.3.3.1 程序流程

PDO 编程使用面向对象的概念。当与 DB2 数据库建立连接时，会创建一个 PDO 基类的实例。该实例充当数据库句柄，后续在对数据库执行进一步操作时使用。在操作数据库时会创建不同的对象，它们可以分为：

- 连接对象（PDO 的实例）
- 语句对象（PDOStatement 的实例）
- 异常（PDOException 的实例）

PDO 程序在事务处理过程中的典型程序流程如下：

1.  连接数据库。
2.  准备并执行语句。
3.  处理结果。
4.  释放资源。

## 8.3.3.2 连接数据库

当使用 new PDO() 调用 PDO 类的构造函数时，即获得到数据库的连接。该构造函数有四组参数：

- 数据源名称（DSN）
- 用户名
- 密码
- 驱动程序选项

DSN 包含连接数据库所需的信息，其中包括使用的驱动程序类型（对于 DB2 来说是 CLI/ODBC）、数据源名称以及连接凭证（用户名和密码）。所需的 DSN 参数取决于你是连接到已编目数据库还是未编目数据库。如果连接的是 DB2 数据库，最好使用已编目连接。以下是假设数据库名为 SAMPLE，用户 ID 为 db2inst1，密码为 123 时，指定 DSN 的示例：

- 已编目连接的 DSN
    - 对于 pdo_ibm：
        `ibm:DSN=sample;UID=db2inst1;PWD=123`
    - 对于 pdo_odbc：
        `odbc:DSN=sample;UID=db2inst1;PWD=123`
- 未编目连接的 DSN
    - 对于 pdo_ibm：
        `ibm:DSN={IBM DB2 ODBC DRIVER};HOSTNAME=localhost;PORT=50000;DATABASE=sample;PROTOCOL=TCPIP;UID=db2inst1;PWD=123;`
    - 对于 pdo_odbc：
        `odbc:DSN={IBM DB2 ODBC DRIVER};HOSTNAME=localhost;PORT=50000;DATABASE=sample;PROTOCOL=TCPIP;UID=db2inst1;PWD=123;`

*示例 8.14* 下方提供了使用已编目方法进行连接的示例。

```php
<?php
try {
    /* Use one of the following connection string */
    /* for PDO_IBM */
    $constring = 'ibm:DSN=sample;UID=db2inst1;PWD=123';
    /* for PDO_ODBC */
    // $constring = 'odbc:DSN=sample;UID=db2inst1;PWD=123';
    $dbh = new PDO($constring);
    echo 'Connected';
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**示例 8.14 – 连接到数据库的已编目连接**

在*示例 8.14*中，new PDO() 方法建立了新的连接。

若要编写一个程序使用未编目连接来连接数据库，请遵循上文第 8.3.2.2.2 节中讨论的技术。

DSN 名称可以通过三种方式提供给 PDO 程序：

- 作为构造函数参数。

使用此方法时，DSN 作为字符串在程序中提供。然而，这使得程序依赖于数据库。每次数据库位置或密码更改时，都需要更改所有引用此数据库的程序中的相应条目。*示例 8.15* 提供了使用此方法的示例。

```php
<?php
/* Use one of the following connection string */
/* The connection below is for pdo_ibm */
$string = 'ibm:sample';
/* The connection below is for pdo_odbc */
// $string = 'odbc:sample';
try {
    $dbh = new PDO($string, '', '');
    echo 'Connected';
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**示例 8.15 – 作为构造函数参数的 DSN**

- 在文件中

使用此方法时，DSN 在文件中提供，并在程序内部引用该文件。如果 DSN 参数值变更，只需更改文件即可。每当 DSN 变更时，无需更改程序。例如，在下方*示例 8.16*中，假设你已创建一个名为*dsnfile*的文件并将其存储在*/usr/local*目录中。

```php
<?php
$string = 'uri:file:///usr/local/dsnfile';
try {
    $dbh = new PDO($string, '', '');
    echo 'Connected';
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**示例 8.16 – 创建和存储文件**

- 在*php.ini*中使用别名

与*ibm_db2*扩展类似，你可以在 PDO_IBM/PDO_ODBC 中使用持久和非持久连接。如果通过设置*pdo_odbc.connection_pooling*为*strict*或*relaxed*来启用连接池，则不应使用持久连接，因为 PDO 不会将连接释放给 ODBC 层以进行连接池操作。使用连接池比使用持久连接更好。要创建非持久连接，我们使用 DSN、用户名和密码创建 PDO 实例，如下*示例 8.17*所示。

```php
<?php
/* Use one of the following connection strings */
/* The connection below is for pdo_ibm */
$constring = 'ibm:sample';
/* The connection below is for pdo_odbc */
// $constring = 'odbc:sample';
try {
    $dbh = new PDO($constring, 'db2inst1', '123');
    echo 'Connected';
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
?>
```

**示例 8.17 — 创建非持久连接**

要创建持久连接，请使用以下 `new PDO` 格式：
`$dbh = new PDO($constring, 'db2inst1', '123', array(PDO::ATTR_PERSISTENT=> true));`

## 8.3.3.3 准备和执行语句

在准备和执行 SQL 语句之前，你需要决定关于该事务的以下特征：

- 使用的游标类型
- 如何捕获错误
- 使用何种隔离级别

### 8.3.3.3.1 使用的游标类型

与 ibm_db2 扩展一样，PDO 也支持两种类型的游标：

#### 仅向前游标

此游标是 PDO 驱动程序中的默认游标。它是可用的速度最快的游标。确保在获取完所有行后且在启动另一个查询之前，使用 `PDOStatement::closeCursor` 方法关闭游标。可以在 `PDOStatement::prepare` 中使用 `PDO::ATTR_CURSOR` 并设置值为 `PDO::CURSOR_FWDONLY` 来设置仅向前游标。*示例 8.20* 提供了一个示例。

```php
$sql = "SELECT c_id, c_name, c_email FROM customer WHERE c_name = :name";
try {
    $sth = $dbh->prepare($sql, array(PDO::ATTR_CURSOR, PDO::CURSOR_FWDONLY));
    $sth->execute(array(':name' => 'Myname'));
    print_r($sth->fetchAll());
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
```

**示例 8.20 – 使用仅向前游标**

#### 可滚动游标

通过设置 **PDO::ATTR_CURSOR** 为 **PDO::CURSOR_SCROLL**，我们可以指定可滚动游标。*示例 8.21* 提供了一个示例。

```php
$sql = "SELECT c_id, c_email FROM customer WHERE c_name = :name";
try {
    $sth = $dbh->prepare($sql, array(PDO::ATTR_CURSOR, PDO::CURSOR_SCROLL));
    $sth->execute(array(':name' => 'Daniel'));
    while ($row = $sth->fetch(PDO::FETCH_NUM, PDO::FETCH_ORI_NEXT)) {
        $data = $row[0] . "\t" . $row[1] . "\t" . $row[2] . "\n";
        echo $data;
    }
    $sth->closeCursor();
} catch (PDOException $exp) {
    echo 'Exception: ' . $exp->getMessage();
}
```

**示例 8.21 – 使用可滚动游标**

### 8.3.3.3.2 在 PDO 中捕获错误

PDO 具有**异常处理程序**来捕获异常并显示其详细信息。这些处理程序具有与其他编程语言类似的"try 和 catch"结构。

当 PDO 程序引发异常时，会创建一个 **PDOException** 实例。**PDOException** 类是 Exception 类的扩展，具有三种操作模式。通过设置 PDO 属性 **PDO::ATTR_ERRMODE** 来强制应用错误处理模式。*表 8.2* 描述了其可取的值。

| 值 | 描述 |
| :--- | :--- |
| PDO::ERRMODE_SILENT | 这是 PDO 中默认的错误处理模式。相应的错误代码和 |

