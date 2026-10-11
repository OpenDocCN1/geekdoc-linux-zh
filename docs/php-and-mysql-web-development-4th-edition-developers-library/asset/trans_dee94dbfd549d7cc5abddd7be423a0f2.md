
## 1.3.3 PDOException 对象方法

默认情况下，PDO 仅为 PDO 构造函数抛出异常（即调用 `new PDO()` 连接数据库服务器时），其他 PDO 方法通过其返回值来指示失败。如果在连接后启用了 PDO 异常，PDO 扩展会在其方法失败时抛出异常。PDOException 对象包含由此类异常产生的错误信息。

要启用 PDO 异常，请使用数据库句柄：

```php
$dbh->setAttribute(PDO::ATTR_ERRMODE, PDO::ERRMODE_EXCEPTION);
```

PDO 支持三种错误模式值：

- `PDO::ERRMODE_SILENT`：PDO 除了设置错误信息外不做任何其他操作。这是默认的错误模式。
- `PDO::ERRMODE_WARNING`：这与静默模式类似，但 PDO 在设置错误信息之外还会发出警告消息。
- `PDO::ERRMODE_EXCEPTION`：PDO 在设置错误信息后引发异常。

如果启用了异常，当发生错误时，可以通过异常对象的 `getCode()` 和 `getMessage()` 方法访问错误信息。

异常默认会终止您的脚本。若要自行处理它们，请使用 `try` 和 `catch`。在 catch 块中，您可以访问返回错误信息的异常方法：

```php
try
{
    $sth = $dbh->query ("SELECT * FROM no_such_table");
}
catch (PDOException $e)
{
    print ("getCode value: " . $e->getCode() . "\n");
    print ("getMessage value: " . $e->getMessage() . "\n");
}
```

- `integer` getCode (void)

返回包含错误代码的五字符 SQLSTATE 值。返回值等于 `PDO::ERR_NONE ("00000")` 表示“无错误”。

- `string` getMessage (void)

返回包含错误消息的字符串。

## 1.3.4 PDO 常量

本节描述了可与 PDO 方法一起使用的一些常量，例如用于数据库句柄的 `getAttribute()` 和 `setAttribute()` 方法。所示值仅具代表性。完整列表请参见 PHP 手册中的 PDO 章节。

通用数据库句柄属性：

- `PDO::ATTR_AUTOCOMMIT`
  - 当前自动提交模式。
- `PDO::ATTR_DEFAULT_FETCH_MODE`
  - 行获取模式。（自 PHP 5.2.4 起作为数据库句柄属性可用。）
- `PDO::ATTR_DRIVER_NAME`
  - PDO 驱动名称。
- `PDO::ATTR_ERRMODE`
  - 错误处理模式。关于允许值的描述，请参见第 1.3.3 节，“PDOException 对象方法”（在线）。

MySQL 特定的数据库句柄属性：

- `PDO::ATTR_CLIENT_VERSION`
  - 描述客户端库版本的字符串。
- `PDO::ATTR_CONNECTION_STATUS`
  - 对于 MySQL，这表明连接是如何建立的。
- `PDO::ATTR_SERVER_INFO`
  - 提供一些服务器活动信息的字符串。
- `PDO::ATTR_SERVER_VERSION`
  - 描述服务器版本的字符串。

控制结果集行获取形式的获取模式值：

- `PDO::FETCH_ASSOC`
  - 返回数组，元素通过关联索引访问。
- `PDO::FETCH_BOTH`
  - 返回数组，元素通过关联或数字索引访问。
- `PDO::FETCH_BOUND`
  - 返回行元素，这些元素由先前的 `bindColumn()` 调用绑定到 PHP 变量。
- `PDO::FETCH_CLASS`
  - 将行元素返回到新类实例的属性中。
- `PDO::FETCH_INTO`
  - 将行元素返回到现有类实例的属性中。
- `PDO::FETCH_NUM`
  - 返回数组，元素通过数字索引访问。
- `PDO::FETCH_OBJ`
  - 返回对象，元素作为属性访问。

参数类型值：

- `PDO::PARAM_BOOL`
  - 布尔参数。
- `PDO::PARAM_INT`
  - 整数参数。
- `PDO::PARAM_NULL`
  - 指示 SQL NULL 值。
- `PDO::PARAM_STR`
  - 字符串参数。

以 Web: 开头的页码：表示可通过*在 informit.com/register 注册本书*或访问 www.kitbitbird.com/mysql-book 找到的在线附录中的主题。

## 符号

- `<?php...?>` 标签，**530**
- `\!` 命令（mysql 客户端程序），**1068**
- `\#` 命令（mysql 客户端程序），**1068**
- `\\` 命令（mysql 客户端程序），**1068**
- `\?` 命令（mysql 客户端程序），**1067**
- `\"EO\"` 字符串，**446**
- `-#` 选项，**1041**
- `-1` 选项（mysqlcheck 客户端程序），**1080**
- `-?` 选项，**1038, 1041**
- `===`（恒等于运算符），PHP API，**547**
- `>`（大于）运算符，**820**
- `>=`（大于或等于）运算符，**820**
- `<`（小于）运算符，**819**
- `<=`（小于或等于）运算符，**820**
- `?`（问号）作为占位符，PHP API，**549**
- `;`（分号），语句终止符，**30**
- `@` 运算符，抑制 PHP API 错误消息，**552**
- `@{$ary_ref}` 结构，**450**

## A

- `-a` 选项
  - *mysamckh* 实用工具，**1053, 1055**
  - *mysqld*，**1084**
- `-A` 选项
  - *mysql* 客户端程序，**1063**
  - *mysqlcheck* 客户端程序，**1080**
  - *mysqldump* 实用工具，**1105**
- `--abort-slave-event-count` 选项（*mysqld*），**1097**
- *Aborted_clients* 状态变量，924
- *Aborted_connects* 状态变量，924
- *ABS()* 函数，834
- 绝对更新，相对更新与之对比，184
- 访问控制
  - 管理员职责，582
  - 针对数据目录，588-589
  - 文件系统访问，699
    - 数据目录，访问权限，701-702
    - 数据目录，锁定，702-706
    - 选项文件，锁定，707-708
    - 需要保护的文件类型，700-701
    - Unix 套接字文件，锁定，706-707
  - 网络访问，699, 709
    - 客户端访问控制，719-724
    - 示例场景，724-728
    - 授权表，709, 712-719
    - 授权表，注意事项，728-731
  - C API 中的访问器宏，Web:1135
- 账户
  - 初始账户，设置密码，610-615
  - 登录账户，创建，782
  - 管理，630-631
    - 更改/重置密码，644-645
    - 授予权限，634-643
    - 撤销权限，643-644
    - 指定账户名称，632-634
    - 指定主机名，634
    - 查看权限，643
  - 服务器启动时
    - 在 Unix 上，616-621
    - 在 Windows 上，621-624
  - 设置，27-28
  - 非特权登录账户，使用其运行服务器，617-618
- ACID 特性（事务），175
- ACOS() 函数，834
- ALTER TABLE 语句中的操作，940-944
  - ADD 子句，940
  - ADD FOREIGN KEY 子句，941
  - ADD FULLTEXT 子句，941
  - ADD INDEX 子句，941
  - ADD KEY 子句，941
  - ADD PARTITION 子句，945
  - ADD PRIMARY KEY 子句，942
  - ADD SPATIAL 子句，942
  - ADD UNIQUE 子句，942
  - `--add-drop-database` 选项（*mysqldump* 实用工具），1105
  - `--add-drop-table` 选项（*mysqldump* 实用工具），750, 1105
  - `--add-locks` 选项（*mysqldump* 实用工具），1105
- ADDDATE() 函数，853
- 加法运算符，816
- 地址窗口扩展，897
- ADDTIME() 函数，853
- `--add-test` 选项（*mysqlhotcopy* 实用工具），1114
- 管理
  - 访问控制和安全职责，582
  - 账户管理，630-631
    - 更改/重置密码，644-645
    - 授予权限，634-643
    - 撤销权限，643-644
    - 指定账户名称，632-634
    - 指定主机名，634
    - 查看权限，643
  - 备份和复制职责，582-583
  - 连接，监听，629-630
  - 数据库维护职责，582-583
  - 一般职责，581-582
  - 国际化和本地化，681
    - 配置字符集支持，684–685
    - 配置时区支持，682–683
    - 选择错误消息语言，684
  - LOAD DATA 语句
    - 启用/禁用 LOCAL 能力，681
  - 日志，645
    - 二进制日志，650–651
    - 启用，646
    - 错误日志，648–649
    - 过期方法，653–654, 657–659
    - 刷新，647
    - 一般查询日志，649
    - 输出目的地，652–653
    - 中继日志，652
    - 慢查询日志，649–650
  - 多个服务器，685–688
    - 配置，688–690
    - *mysqld_multi* 脚本，691–693
    - 在 Windows 上运行，693–695
    - 指定启动选项，690–691
  - 无连接时重新获得服务器控制权，626
  - 安全。参见安全
  - 服务器关闭，626
  - 服务器启动
    - 指定选项，624–626
    - 在 Unix 上，616–621
    - 在 Windows 上，621–624
  - 存储引擎，669
  - 系统变量，660
    - 检查状态变量，667–668
    - 检查/设置，661–665
    - 列表，663–667
- C API 中的管理函数，Web:1173–Web:1175
- Perl DBI API 中的管理方法，Web:1196–Web:1197
- 管理权限列（授权表），710
- 管理权限，636, 713–715
- 管理级查询优化，334–336
  - 硬件优化，339–340
  - MyISAM 键缓存，336–337
  - 查询缓存，337–339
- 咨询锁定函数，875–876
- AES_DECRYPT() 函数，871
- AES_ENCRYPT() 函数，872
- AFTER 触发器，297, 968
- AGAINST() 函数，196, 846
- 基于年龄的复制，657
- 聚合函数，868
- ALGORITHM 子句，970
- 别名
  - 大小写敏感性，106
  - 列别名，69, 999
  - PHP API 中的列别名，546
  - Shell 别名，95
  - 表别名，1000
- ALL 关键字，161–162, 998, 1026
- `--all` 选项（*mysqldump* 实用工具），1105
- ALL 权限，637–638, 981
- `--all-databases` 选项，745, 750, 759
  - *mysqlcheck* 客户端程序，1080
  - *mysqldump* 实用工具，1105
- `--all-in-1` 选项（*mysqlcheck* 客户端程序），1080
- `--all-tablespaces` 选项（*mysqldump* 实用工具），1105
- 分配语句处理程序，423
- ALLOW_INVALID_DATES 模式，254, 914
- `--allow-keywords` 选项（*mysqldump* 实用工具），1105
- `--allow-suspicious-udfs` 选项（*mysqld*），1084
- `--allowold` 选项（*mysqlhotcopy* 实用工具），1114
- ALTER DATABASE 语句，114, 938
- ALTER EVENT 语句，939

