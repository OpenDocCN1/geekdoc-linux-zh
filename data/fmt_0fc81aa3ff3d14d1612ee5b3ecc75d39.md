
| `stat(FILEHANDLE)` | 返回文件统计信息的13 元素列表 |
| `study(STRING)` | 为了预测多次模式匹配而检查字符串 |
| `substr(EXPR, OFFSET, LEN)` | 从字符串 `EXPR` 中截取子字符串 |
| `symlink(OLDFILE, NEWFILE)` | 创建指向 `OLDFILE` 的符号链接 `NEWFILE` |
| `syscall(LIST)` | 调用 `LIST` 第一个元素指定的系统函数（并将列表剩余元素作为参数传递给该调用） |
| `sysopen(FILEHANDLE, FILENAME, MODE, PERMS)` | 打开名为 `FILENAME` 的文件并关联到 `FILEHANDLE` |
| `sysread(FILEHANDLE, SCALAR, LENGTH, OFFSET)` | 从文件读取指定数量的字节 |
| `sysseek(FILEHANDLE, POSITION, WHENCE)` | 设置 `FILEHANDLE` 的位置为指定的字节数（`WHENCE` 是设置位置的参考点，可以是 `SEEK_SET`, `SEEK_CUR`, `SEEK_END` 之一） |
| `system(LIST)` | 执行 `LIST` 中的 Shell 命令 |
| `syswrite(FILEHANDLE, SCALAR, LENGTH, OFFSET)` | 向文件写入指定数量的字节 |
| `tell(FILEHANDLE)` | 返回从文件开始的当前字节位置 |
| `teldir(DIRHANDLE)` | 返回 `readdir` 函数可以从目录读取的当前位置 |

# 表 24-3：（续）

| 函数调用 | 描述 |
|---|---|
| `tie(VARIABLE, PACKENAME, LIST)` | 将变量关联到实现该变量的包 |
| `time` | 返回自 GMT 1970 年 1 月 1 日 00:00:00 以来的秒数 |
| `times` | 返回当前进程的秒数时间 |
| `tr/SEARCHLIST/REPLACE_LIST/cds` | 将搜索列表转换为替换列表 |
| `truncate(FILEHANDLE, LENGTH)` | 将文件 `FILEHANDLE` 截断至指定的 `LENGTH` |
| `uc(EXPR)` | 返回 `EXPR` 的大写版本 |
| `ucfirst(EXPR)` | 将 `EXPR` 的第一个字符改为大写后返回 |
| `umask(EXPR)` | 设置创建文件时使用的权限掩码（这规定了不允许对文件执行哪些操作） |
| `undef(EXPR)` | 取消 `EXPR` 的定义 |
| `unlink(LIST)` | 删除文件列表 |
| `unpack(TEMPLATE, EXPR)` | 将字符串解包为数组并返回该数组 |
| `shift(ARRAY, LIST)` | 将 `LIST` 插入到 `ARRAY` 的头部 |
| `untie(VARIABLE)` | 解除变量与包之间的绑定 |
| `use(MODULE)` | 开始使用一个 Perl 模块 |
| `utime(LIST)` | 修改一组文件的访问和修改时间 |
| `values(ASSOC_ARRAY)` | 返回一个包含关联数组所有值的数组 |
| `vec(EXPR, OFFSET, BITS)` | 将 `EXPR` 视为整数向量，并返回向量的指定元素 |
| `wait` | 等待子进程终止 |
| `waitpid(PID, FLAGS)` | 等待特定的子进程（由 `PID` 标识）终止 |
| `wantarray` | 返回当前子程序是否在数组上下文中调用 |
| `warn(LIST)` | 在标准错误上产生（由 `LIST` 指定）警告消息 |
| `write(FILEHANDLE)` | 向文件写入格式化后的记录 |
| `y/SEARCHLIST/REPLACE_LIST/cds` | 将搜索列表转换为替换列表 |

# 理解 Perl 包和模块

Perl 包（`package`）是数据数据和子程序分组的一种。本质上，它是一种使用变量和子程序名称而不会与程序其他部分使用的名称冲突的方法。包的概念在 Perl 4 中就已经存在。

Perl 包提供了一种控制命名空间的方法——命名空间是指变量和子程序名称的集合。尽管你可能没有意识到，但当你编写 Perl 程序时，它自动属于一个名为 `main` 的包。此外，Perl 库中还有其他 Perl 包（这些包位于你的 Red Hat Linux 系统的 `/usr/lib/perl5` 下，子目录名称与你运行的包同名），你也可以定义自己的包。

正如你将学到的，Perl 模块（`modules`）遵循这些特定指南。

你可以将 Perl 包看作组织一组相关 Perl 子程序的方便方式。另一个用处是，在包中定义的变量和子程序名称与程序中其他地方使用的名称冲突。因此，一个包中名为 `$count` 的变量对该包来说是唯一的，不会与另一个 Perl 包中使用的 `$count` 冲突。

一个 Perl 包是一个单文件。`package` 语句用于文件开头，用于声明该文件为一个包并给该包命名。例如，`ctime.pl` 文件在不同位置存有以下 `package` 语句：

```
package ctime;
```

该包声明的效果是，所有后续的变量名和子程序名都被认为属于 `ctime` 包。你可以将此类 `package` 语句放在实现该包的文件开头。

如果你正在实现一个包，并且需要引用另一个包中的子程序或变量怎么办？正如你猜的，你只需要同时指定包名和变量（或子程序）名。Perl 5 提供了以下语法来引用另一个包中的变量：

```
$Package::Variable
```

这里的 `Package` 是包名，`Variable` 是该包中的变量名。如果你省略了包名，Perl 会假设你正在引用 `main` 包中的变量。注意，C++ 在引用另一个 C++ 类中的变量时恰恰使用了类似的语法（类基本上是数据和函数的集合——一种模板）。

要在程序中使用包，你可以简单地调用 `require` 函数并将包文件名作为参数。例如，`ctime.pl` 文件定义了一个名为 `ctime` 的包。该包包含了 `ctime` 子程序，它可以将二进制时间转换为字符串。下面的简单程序使用了 `ctime.pl` 文件中的 `ctime` 包：

## 第五部分：红 Hat Linux 编程

```
#!/usr/bin/perl -w

# 调用 ctime 子程序。
$time = ctime(time());

# 打印时间字符串。
print $time;
```

你可以看到，该程序使用 `require` 函数将 `ctime.pl` 文件引入程序中。当你运行此程序时，它应该打印格式化后的当前日期和时间，如示例所示：

Sun Feb 9 18:25:46 2033

Perl 5 将包的概念更进了一步，引入了模块（`module`）。模块是一个遵循特定指南并设计为可重用的包。每个模块-包都定义在与包同名但扩展名为 `.pm` 的文件中。每个 Perl 对象都实现为一个模块。例如，`Shell` 对象实现为 `Shell` 模块，存储在名为 `Shell.pm` 的文件中。

Perl 5 自带了大量的模块。你可以在 `/usr/lib/perl15` 目录下与你的 Perl 版本对应的子目录下找到这些模块。对于 Perl 5.8.0，这些模块位于 `/usr/lib/perl15/5.8.0` 目录（路径的最后一部分是 Perl 版本号）。寻找以 `.pm`（Perl 模块）结尾的文件。

# 使用 Perl 模块

你可以使用 `require` 函数或 `use` 函数将 Perl 模块引入你的程序。例如，一个名为 `Cwd` 的 Perl 模块（如预期定义在 `Cwd.pm` 文件中）提供了一个返回当前目录的 `getcwd` 子程序。你可以调用 `require` 函数引入 `Cwd` 模块，并如下调用 `getcwd`：

```
require Cwd; # 不需要完整文件名。
$scurdir = Cwd::getcwd(); print $scurdir
```

```
print "Current directory = $scurdir\n";
```

第一行将 `Cwd` 模块加载到程序中。当你运行此程序时，它应该打印格式化后的当前目录，如示例所示：

第二行展示了如何使用模块：

```
use Cwd;
$scurdir = Cwd::getcwd(); print $scurdir
print "Current directory = $scurdir\n";
```

Perl 5 将包的概念更进了一步，引入了模块。模块是一个遵循特定指南并设计为可重用的包。每个模块-包都定义在与包同名但扩展名为 `.pm` 的文件中。每个 Perl 对象都实现为一个模块。例如，`Shell` 对象实现为 `Shell` 模块，存储在名为 `Shell.pm` 的文件中。

# 第五部分：在红帽 Linux 上进行编程

续上
