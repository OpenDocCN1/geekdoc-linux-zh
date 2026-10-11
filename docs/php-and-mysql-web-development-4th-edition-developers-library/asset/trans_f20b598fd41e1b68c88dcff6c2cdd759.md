

- REFRESH_LOG  
  通过关闭并重新打开日志文件来刷新日志。这适用于服务器当前打开的任何日志，等同于发出 `FLUSH LOGS` 语句。

- REFRESH_MASTER  
  指示复制主服务器删除二进制日志索引文件中列出的二进制日志文件，并截断该索引。这等同于发出 `RESET MASTER` 语句。

- REFRESH_SLAVE  
  指示复制从服务器忘记其在主日志中的位置。这等同于发出 `RESET SLAVE` 语句。

- REFRESH_STATUS  
  将状态变量重新初始化为零。这等同于发出 `FLUSH STATUS` 语句。

- REFRESH_TABLES  
  关闭所有打开的表。这等同于发出 `FLUSH TABLES` 语句。

- REFRESH_THREADS  
  刷新线程缓存。没有与此操作等效的 SQL 语句。

选项标志是位值，因此您可以使用 `|` 或 `+` 运算符以加法方式将它们组合起来。例如，以下表达式是等效的：

```
REFRESH_LOG | REFRESH_TABLES
REFRESH_LOG + REFRESH_TABLES
```

int **mysql_set_server_option** (MYSQL *conn,  
enum enum_mysql_set_option option);

设置服务器选项，如果选项设置成功则返回零，否则返回非零值。目前，唯一允许的选项是 `MYSQL_OPTION_MULTI_STATEMENTS_ON` 或 `MYSQL_OPTION_MULTI_STATEMENTS_OFF`，分别用于启用或禁用多语句执行功能。

使用 `MYSQL_OPTION_MULTI_STATEMENTS_ON` 启用多语句执行*并不*同时启用多个结果集。这与 `mysql_real_connect()` 的 `CLIENT_MULTI_STATEMENTS` 选项不同，该选项同时也启用了 `CLIENT_MULTI_RESULTS`。

int mysql_shutdown (MYSQL *conn, enum mysql_enum_shutdown_level level);

指示服务器关闭。执行此操作需要具有 SHUTDOWN 权限。第二个参数的值应为 SHUTDOWN_DEFAULT；其他关闭级别最终可能会实现。

mysql_shutdown() 成功时返回零，失败时返回非零值。

## G.3.11 多线程客户端例程

本节的例程用于编写多线程客户端。

void mysql_thread_end (void);

释放由 mysql_thread_init() 初始化的任何线程特定变量。为了避免内存泄漏，您应该显式调用此函数来终止您创建的任何线程。

my_bool mysql_thread_init (void);

初始化线程特定变量。对于您将创建的任何调用 MySQL 函数的线程，都应调用此函数。此外，在终止线程之前，您应该调用 mysql_thread_end()。

unsigned int mysql_thread_safe (void);

如果客户端库是线程安全的，则返回 1，否则返回 0。此函数的值反映了 MySQL 是否使用 --enable-thread-safe-client 选项进行了配置。

## G.3.12 调试例程

这些函数允许您在连接的客户端端或服务器端生成调试信息。这需要 MySQL 支持调试功能进行编译。（在配置 MySQL 发行版时使用 --with-debug 选项，或使用 --with-debug=full 以获取更多信息。后者选项启用 safemalloc，这是一个执行大量内存分配检查的库。）

void mysql_debug (const char *debug_str);

使用字符串 debug_str 执行 DEBUG_PUSH 操作。该字符串的格式在 MySQL 参考手册中有描述。

要使用 mysql_debug()，客户端库必须支持调试功能进行编译。

int **mysql_dump_debug_info** (MYSQL *conn);

指示服务器将调试信息写入日志。执行此操作需要具有 `SUPER` 权限。

`mysql_dump_debug_info()` 成功时返回零，失败时返回非零值。

# Perl DBI API 参考

本附录介绍了 Perl DBI 应用程序编程接口。该 API 由一组用于与数据库服务器通信并从 Perl 脚本访问数据库的方法和属性组成。附录还介绍了 DBD:MySQL（MySQL 数据库驱动）提供的 DBI 的 MySQL 特定扩展。

DBI 目前处于 1.601 版本，虽然此处的大部分内容也适用于较早的版本。这里假设 DBI 的最低版本为 1.40，这需要至少 Perl 5.6.0（并且推荐使用 5.6.1 而非 5.6.0）。我还假设 DBD:MySQL 的最低版本为 3.0000_0。在那些最低版本之后引入的 DBI 或 DBD:MySQL 行为变化会有所注明。为了支持 mysql_server_prepare，最好使用 DBD:MySQL 3.0009 或更高版本，因为前面某些版本中该功能的默认值发生了一些变化。

要确定您的 DBI 和 DBD:MySQL 版本，请运行此程序：

```perl
#!/usr/bin/perl
# dbi-version.pl  查看 DBI 和 DBD:MySQL 版本
use strict;
use warnings;
use DBI;
print "DBI::VERSION: $DBI::VERSION\n";
use DBD:MySQL;
print "DBD:MySQL::VERSION: $DBD:MySQL::VERSION\n";
```

一些 DBI 方法和属性在此处未加讨论，因为它们不适用于 MySQL，或者因为它们是在开发过程中可能发生变化甚至可能被弃用的实验性方法。一些 MySQL 特定的 DBD 方法也未加讨论。如果您想了解更多关于新方法或废弃方法的信息，请查看 DBI 文档或 MySQL DBD 文档，您可以通过运行以下命令获取这些文档：

```
% perldoc DBI
% perldoc DBI::FAQ
% perldoc DBD:MySQL
```

更多信息也可以在 http://dbi.perl.org/ 上获取。
本附录中的示例仅为简短的代码片段。有关完整的客户端脚本及其编写说明，请参见第 8 章“使用 Perl DBI 编写 MySQL 程序”。

## H.1 编写脚本

每个使用 DBI 模块的 Perl 脚本都必须包含以下行：

```perl
use DBI;
```

通常不需要包含特定 DBD 级别模块的 `use` 行，因为 DBI 会在您连接到服务器时自动激活正确的模块。
通常，DBI 脚本使用 `connect()` 方法打开与 MySQL 服务器的连接，并使用 `disconnect()` 关闭连接。在连接打开期间，可以执行 SQL 语句。执行此操作的方法因语句类型而异。非 `SELECT` 语句通常通过 `do()` 方法执行。`SELECT` 语句通常通过将语句传递给 `prepare()` 来执行，然后调用 `execute()`，最后在一个循环中逐行检索结果集，该循环反复调用行获取方法，如 `fetchrow_array()` 或 `fetchrow_hashref()`。
当您在 DBI 脚本中执行语句时，每个语句字符串必须由单个 SQL 语句组成，并且不应以分号字符串（`;`）或 `\g` 序列结尾。`;` 和 `\g` 是 `mysql` 客户端程序的约定，在 DBI 中不使用。

## H.2 DBI 方法

这里的方法描述采用的格式与附录 G“C API 参考”（在线）中用于 C 函数的格式以及附录 I“PHP API 参考（在线）”中用于 PHP 函数的格式略有不同。那些附录中的函数以原型形式书写，明确列出了返回值类型和参数类型。这里的描述使用变量来指示参数和返回值类型，其中每个变量的首字符表示其类型：`$` 表示标量，`@` 表示数组，`%` 表示哈希（关联数组）。此外，以 `\` 开头的参数表示对给定类型变量的引用，而不是变量本身。变量名后缀为 `ref` 表示该变量的值是一个引用。
某些变量名在本附录中反复出现，并具有表 H.1 中所示的约定含义。

