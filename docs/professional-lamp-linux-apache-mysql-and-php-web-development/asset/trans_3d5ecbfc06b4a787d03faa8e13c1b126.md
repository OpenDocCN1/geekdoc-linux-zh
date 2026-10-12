
# 第 1 章

- `dbx_fetch_row()`：从查询结果中获取行，但如果查询中未设置 DBX_RESULT_UNBUFFERED，则执行将失败。
- `fbsql_set_password()`：更改指定用户的密码。
- `file_put_contents()`：等效于打开文件、写入文件并关闭文件的操作。
- `ftp_alloc()`：向 FTP 服务器发送 ALLO 命令，该命令为上传文件预留空间。
- `get_declared_interfaces()`：返回脚本中已声明的任何接口。
- `get_headers()`：返回服务器响应 HTTP 请求时发送的头部信息。
- `headers_list()`：返回已发送（或准备发送）的响应头列表。
- `http_build_query()`：根据给定的数组返回 URL 编码的查询字符串。
- `ibase_affected_rows()`：返回受上一个查询影响的行数（Interbase）。
- `ibase_backup()`：在服务管理器中启动备份任务并立即返回（Interbase）。
- `ibase_commit_ret()`：提交事务，但不关闭它然后返回（Interbase）。
- `ibase_db_info()`：返回关于数据库的信息（Interbase）。
- `ibase_drop_db()`：删除数据库（Interbase）。
- `ibase_errcode()`：返回错误代码（Interbase）。
- `ibase_free_event_handler()`：释放已注册的事件处理程序（Interbase）。
- `ibase_gen_id()`：增量增加并返回增加后的值（Interbase）。
- `ibase_maintain_db()`：在数据库服务器上执行维护命令（Interbase）。
- `ibase_name_result()`：为结果集命名（Interbase）。
- `ibase_num_params()`：返回命名查询中的参数数量（Interbase）。
- `ibase_param_info()`：返回命名查询的参数信息（Interbase）。
- `ibase_restore()`：在服务管理器中启动恢复任务并立即返回（Interbase）。
- `ibase_rollback_ret()`：回滚事务但不关闭它（Interbase）。
- `ibase_server_info()`：返回关于数据库的信息（Interbase）。
- `ibase_service_attach()`：连接到服务管理器（Interbase）。
- `ibase_service_detach()`：断开与服务管理器的连接（Interbase）。
- `ibase_set_event_handler()`：注册用户定义的函数，以便在特定事件发生后调用（Interbase）。
- `ibase_wait_event()`：等待数据库发布的事件（Interbase）。
- `iconv_mime_decode()`：解码 MIME 头字段。
- `iconv_mime_decode_headers()`：同时解码多个 MIME 头字段。
- `iconv_mime_encode()`：创建 MIME 头字段。
- `iconv_strlen()`：返回字符串的字符数。
- `iconv_strpos()`：在字符串中查找指定字符第一次出现的位置。
- `iconv_strrpos()`：在字符串的指定范围内查找指定字符最后一次出现的位置。
- `iconv_substr()`：返回字符串的一部分。
- `idate()`：将本地时间/日期格式化为整数。
- `imagefilter()`：对图像应用命名过滤器。
- `image_type_to_extension()`：返回图像文件的扩展名。
- `imap_getacl()`: 返回指定邮箱的 ACL。
- `ldap_sasl_bind()`：使用 SASL 将资源绑定到 LDAP 目录。
- `mb_list_encodings()`：返回所有支持编码的数组。
- `pcntl_getpriority()`：返回 pid 的优先级。
- `pcntl_wait()`：暂停当前进程，直到子进程退出并返回子进程的 id。
- `pg_version()`：以数组形式返回客户端、协议和服务器的版本。
- `php_strip_whitespace()`：从源代码中移除注释、空白符和换行符，并返回结果。
- `proc_nice()`：通过给定的增量改变当前进程的优先级。
- `psapi_config_data_dir()`：设置语言数据文件的位置。
- `psapi_config_dict_dir()`：设置主单词列表的位置。
- `setrawcookie()`：等效于未经过 URL 编码值的 `setcookie()`。
- `snmp_read_mib()`：读取并解析 MIB 文件到活动的 MIB 树中。
- `sqlite_fetch_column_types()`：从给定表中返回适用的列类型。
- `str_split()`：将字符串拆分为字符数组。
- `stream_copy_to_stream()`：在流之间复制数据并返回复制的数据量。
- `stream_get_line()`：与 `fgets()` 类似，但允许指定命名分隔符。
- `stream_socket_accept()`：接受来自之前使用 `stream_socket_server()` 函数创建的套接字的连接。
- `stream_socket_client()`：打开到 Internet 或 Unix 域目的地的流。
- `stream_socket_get_name()`：返回套接字连接的名称。
- `stream_socket_recvfrom()`：从套接字接收数据，直到指定长度。
- `stream_socket_sendto()`：向指定套接字发送数据，无论其是否已连接。
- `stream_socket_server()`：在指定服务器上创建流。
- `strpbrk()`：在字符串中搜索给定字符列表中的任意字符，并从第一次成功匹配处返回字符串的剩余部分。
- `substr_compare()`：使用命名偏移量和可选的大小写敏感性比较两个字符串。
- `time_nanosleep()`：延迟脚本执行指定秒数和纳秒数。

有关这些函数的更多信息，可在源地址中找到，http://www.php.net。

## PHP5 的其他更改

除了面向对象编程（OOP）更改的清单和大量可用的新函数外，PHP5 的发布中还做出了其他改进。

### 配置更改

在 PHP5 中，php.ini 配置文件有许多更改。这些将在第 5 章中详细讨论，但这里列出一个列表供您参考：

- mail.force_extra_parameters
- register_long_arrays
- session.hash_function
- session.hash_bits_per_character
- zend.zel_compatibility_mode

通过这些新的指令，你可以对 PHP 环境施加更多控制，从而赋予你在编码方面更多的自由度。

### MySQLi

众所周知，MySQLi 与 PHP 搭配良好，能够构建数据库驱动的动态网站。因此，MySQLi（MySQL 改进版）扩展的发布使每个人的工作都变得更加容易。

### 配置设置

php.ini 中有几个新的 MySQLi 配置设置可用。以下是简要说明：

- mysqli.max_links：设置每个进程的最大 MySQL 连接数。
- mysqli.default_port：设置连接到 MySQL 服务器的默认 TCP/IP 端口。
- mysqli.default_socket：设置连接到 MySQL 服务器的默认套接字名称。
- mysqli.default_host：设置连接到 MySQL 服务器的默认主机名。
- mysqli.default_user：设置连接到 MySQL 服务器的默认用户名。
- mysqli.default_pw：设置连接到 MySQL 服务器的默认密码。

**内置类和属性**

*mysqli* 扩展带来了一组新的内置类和属性，您可以在 PHP 脚本中访问这些类和属性。如果脚本是面向过程而非面向对象的，这些新方法也可以作为函数使用。要以面向过程的方式调用函数，只需在方法名前使用 *mysqli_* 语法即可。例如，使用 OOP 创建新连接时，您需要输入以下内容：

```php
<?php
    $connect = new mysqli("server", "user", "pass", "dbname");
    //call methods through the mysqli class
    $connect->close();
?>
```

要使用传统的面向过程编程实现相同的功能，您需要输入以下内容：

```php
<?php
    $connect = mysqli_connect("server", "user", "pass", "dbname");
    //call functions using mysqli_ prefix
    mysqli_close($connect);
?>
```

以下部分描述了 PHP5 中固有的函数类型。

### class mysqli

该类处理基本的 MySQL 连接。该类的构造函数创建一个新的 PHP/MySQL 连接，从而创建一个新的 *mysqli* 对象。您可以使用该类来操作或检索当前连接的信息，或执行基本查询功能。

该类可用的方法包括：

- ***autocommit***：切换事务是否自动提交到数据库。
- ***change_user***：切换到其他用户。
- ***character_set_name***：返回默认字符集。
- ***close***：关闭数据库连接。
- ***commit***：将事务提交到数据库。
- ***connect***：打开到 MySQL 数据库服务器的新连接（也是 *mysqli* 的构造函数）。
- ***debug***：使用 Fred Fish 调试库进行调试。
- ***dump_debug_info***：使用 Fred Fish 调试库转储调试信息。
- ***get_client_info***：检索客户端信息。

