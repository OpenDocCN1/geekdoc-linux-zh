
## INET_NTOA($n$)

给定 IP 地址的整数表示形式，返回对应的点分十进制表示形式（字符串），如果值不合法则返回 NULL。

INET_NTOA(1075594054) → '64.28.67.70'
INET_NTOA(2130706433) → '127.0.0.1'

## LAST_INSERT_ID()

LAST_INSERT_ID($expr$)

不带参数时，返回当前服务器会话中最近一次生成的 AUTO_INCREMENT 值，如果未生成过此类值，则返回 0。

带有参数时，LAST_INSERT_ID() 的返回值为该参数值，但处理方式与自动生成的值相同，这对于生成序列非常有用。

更多详情请参阅第 3 章。对于 LAST_INSERT_ID() 的两种形式，该值由服务器按连接进行维护，其他客户端（即使是那些会导致其自身生成新的自动值的客户端）也无法更改该值。

## LOAD_FILE($file_name$)

读取文件 $file_name$ 并将其内容作为字符串返回。该文件必须位于服务器上，必须指定为绝对（完整）路径名，并且必须具有全局可读性，以确保您没有尝试读取受保护的文件。如果 secure_file_priv 系统变量非空，其值应是一个目录，且文件必须位于该目录中。由于文件必须位于服务器上，您必须拥有 FILE 权限。如果上述任何条件不满足，LOAD_FILE() 将返回 NULL。

## MASTER_POS_WAIT($log_file$, $pos$, $timeout$)

此函数用于测试复制服务器。当在主从架构的从服务器上执行时，它会阻塞，直到从服务器读取并处理了来自主服务器的事件，直至达到由 $log_file$ 和 $pos$ 参数指定的复制坐标。可选的 $timeout$ 值可用于指示 MASTER_POS_WAIT() 设置函数等待的秒数上限。值为 0 或更小等同于不设置超时。

MASTER_POS_WAIT() 返回为了到达给定的复制坐标所等待的日志文件事件数量。如果从服务器已经到达该坐标，函数将立即返回，值为 0。返回值为 -1 表示函数超时、发生错误，或者主服务器信息尚未初始化。返回值为 NULL 表示在函数等待期间，从服务器的 SQL 线程未运行或已停止。

## NAME_CONST(name,value)

此函数在内部使用（例如，用于将语句写入二进制日志）。它返回 value，列名为 name。两个参数都必须是常量。NAME_CONST() 是在 MySQL 5.0.12 中引入的。

## ROW_COUNT()

此函数作为 mysql_affected_rows() C API 函数的 SQL 级别版本运行。它返回前一条语句影响的行数。这就是插入、删除或更新的行数。值为 −1 表示前一条语句是 SELECT 语句（或返回结果集的其他语句），或者发生了错误。

ROW_COUNT() 是在 MySQL 5.0.1 中引入的。

## SCHEMA()

这是 DATABASE() 的同义词，于 MySQL 5.0.2 中引入。

## SESSION_USER()

此函数是 USER() 的同义词。

## SLEEP(seconds)

暂停指定的秒数并返回 0，如果被中断则返回 1。seconds 参数可以有小数部分。SLEEP() 是在 MySQL 5.0.12 中引入的。

## SYSTEM_USER()

此函数是 USER() 的同义词。

## USER()

返回一个 utf8 字符串，表示客户端连接到 MySQL 服务器时指定的用户名以及客户端连接的主机。返回值是 'user_name@host_name' 格式的字符串。该值是 utf8 字符串；在将值传递给接受多个字符串参数的函数时，请考虑到这一点，以避免引发排序规则不匹配错误。

USER() → 'paul@localhost'
SUBSTRING_INDEX(USER(), '@', 1) → 'paul'
SUBSTRING_INDEX(USER(), '@', -1) → 'localhost'

## UUID()

返回一个“通用唯一标识符”（UUID）。其意图是，UUID() 一次调用的返回值应与任何一次其他调用的值不同。返回值的唯一性并非绝对保证，但重复值出现的可能性极低。

UUID() → '455088e8-3c1e-1027-9cc8-78fa1f8d4d6b'
UUID() → 'cbb9ad76-3d10-1027-8c06-349c716080d3'

返回值是一个由 128 位数字生成的五部分 `utf8` 十六进制数字字符串。前四个部分应在时间上唯一，最后一个部分应在空间上唯一。值的前三个部分是从时间戳派生的。第四部分确保在时间戳序列可能不是单调的情况下（例如夏令时切换时发生的时间变化）的唯一性。第五部分是 IEEE 802 节点号。这可能是从假设在您服务器主机上是唯一的值生成的，例如网络接口地址。如果无法获取此类唯一值，则使用 48 位随机数代替。

## VERSION()

返回一个描述服务器版本的 `utf8` 字符串。

```
VERSION() → '5.1.25-rc-log'
```

该值由一个版本号组成，后面可能跟随一个或多个后缀。后缀可能包括以下内容：

- `-alpha`、`-beta` 或 `-rc` 表示 MySQL 版本的稳定性。如果这些都不存在，则该版本为通用可用性（生产质量）。
- `-debug` 表示服务器正在以调试模式运行。
- `-embedded` 表示嵌入式服务器，`libmysqlid`。
- `-log` 表示日志记录已启用。

# 系统、状态和用户变量参考

本附录描述了几种类型的 MySQL 变量：

- 提供服务器配置信息的系统变量
- 以仅限会话形式存在的系统变量（每个客户端一个）
- 提供服务器当前操作状态信息的状态变量
- 您可以定义、赋值并在表达式中引用的用户变量

表示缓冲区大小或长度的变量的值通常以字节为单位。如有例外，将予以注明。

除非另有说明，此处列出的变量至少从 MySQL 5.0.0 起就已存在。在此之后引入或含义发生变化的变量将予以注明。

## D.1 系统变量

系统变量提供有关服务器配置和功能的信息。大多数系统变量可以在服务器启动时设置，许多还可以动态修改，即在服务器运行期间进行修改。此信息在每个变量的描述中给出，位于变量名称的同一行上：

- 对于可以在服务器启动时设置的变量，您将看到单词 "startup"，后面跟着 "set directly" 或一个选项。"set directly" 表示您可以直接在命令行或选项文件中通过使用该变量同名的选项来设置该变量。（第 F.1.2.2 节，“设置程序变量”介绍了执行此操作的语法。）否则，"startup" 后面跟着用于设置变量的选项。例如，您使用 `--default-storage-engine` 选项设置 storage_engine 变量。当给出选项时，其含义可以在附录 F 中 *myqld* 程序的描述中找到：“MySQL 程序参考。”
- 对于在服务器运行期间可以修改的变量，您将看到单词 “runtime”，后面跟着 “global” 或 “session” 这两个词中的一个或两个，以指示该变量是否具有 GLOBAL 形式或 SESSION 形式，或者两者都有。

一些系统变量仅以会话形式存在。这些在第 D.2 节“仅限会话的系统变量”中描述。

可以使用 SHOW VARIABLES 语句或通过执行 mysqladmin variables 命令来显示系统变量。您还可以使用 SELECT @@GLOBAL._var_name 来显示全局变量的值，或使用 SELECT @@SESSION._var_name 或 SELECT @@var_name 来显示会话变量的值。从 MySQL 5.1.12 开始，您还可以检查名为 GLOBAL_VARIABLES 和 SESSION_VARIABLES 的 INFORMATION_SCHEMA 表以获取系统变量信息。

有关在运行时设置系统变量或检查其值的更多信息，请参阅第 12.6.1 节“检查和设置系统变量值”。

系统变量名称不区分大小写。

此处描述的一些变量仅在特定配置下存在。例如，许多以 innodb_ 开头的变量仅在 InnoDB 存储引擎可用时显示。有几个与 Falcon 相关的系统变量，但由于实现仍有些不稳定，因此未提及。

### auto_increment_increment

(startup; set directly; runtime; global, session)

每次服务器生成新的序列值时，AUTO_INCREMENT 值的增量。默认值为 1；值的范围是 1 到 65,535。此变量在 MySQL 5.0.2 中引入。

### auto_increment_offset

(startup; set directly; runtime; global, session)

AUTO_INCREMENT 序列的起始值。默认值为 1；值的范围是 1 到 65,535。此变量在 MySQL 5.0.2 中引入。

### automatic_sp_privileges

(startup; set directly; runtime; global)

当此变量为 1（默认值）时，如果创建存储过程需要，服务器会自动授予您 EXECUTE 和 ALTER ROUTINE 权限，以便您稍后可以执行、更改或删除该过程。当删除该过程时，服务器也会撤销这些权限。如果 automatic_sp_privileges 为 0，则不会自动授予和撤销权限。此变量在 MySQL 5.0.3 中引入。

### back_log

(startup; set directly)

在处理当前连接时，可以排队的待处理连接请求的最大数量。

### basedir

(startup; set directly)

MySQL 安装根目录的路径名。

