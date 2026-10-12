
```
-verbose -> 99,
-sections -> "NAME|SYNOPSIS|OPTIONS|AUTHOR"
```

各个章节用 `|` 符号分隔。`-output` 选项最终定义了信息的输出去向——对于 `verbose` 值为 0 和 1 输出到 `STDOUT`，对于 2 输出到 `STDERR`。对于完整行的输出，输出帮助可以帮你显式设置此项（否则用户必须先将 STDERR 重定向到 STDOUT 才能看到帮助）：

```
-output -> \STDOUT
```

在插件中，你首先检查 `GetOptions` 是否失败，例如因为指定了无效选项。如果出错，则执行跟随 `or` 之后的指令（在此例中为 `podusage`）：

```
GetOptions(
  or podusage(
    -exitval -> UNKNOWN,
    -verbose -> 0,
    -msg -> "*** unknown option or argument ***"
  );
```

返回值为 `UNKNOWN`，表示插件使用不当。`-verbose` 被设置为 `0`，因为在这种情况下简短的用法消息就足够了。`-msg` 向用户更精确地解释他做错了什么；此消息被放在用法消息之前。

如果用户请求在线帮助，将显示插件中包含的所有帮助文本：

```
podusage(
  -verbose -> 2,
  -exitval -> UNKNOWN,
  -output -> \STDOUT
) if ( $help ) ;
```

由于 `podusage` 通常使用 `STDERR`，`-output` 显式确保输出到 `STDOUT`。

要显示版本，可以使用 `podusage`。许多 GNU 程序在版本号中包含版权信息。为了实现这一点，你创建一个 POD 章节 `head1 LICENSE` 并配合此 `verbose -> 99:` 使用：

```
=head LICENSE
This program is free software; you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation; either version 2 of the License, or (at your option) any later version.
```

你收到了该程序的 GNU 通用许可许可证副本；如果没有，请写至 Free Software Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301。

```
=cut
podusage(
  -msg -> "\u00a9 version: \version\n"
  -verbose -> 99,
  -sections -> "NAME|LICENSE"
  -output -> STDOUT,
  -exitval -> UNKNOWN
) if ( $PRINT );
```

由于输出通常使用 `STDERR`，`-output` 显式确保输出到 `STDOUT`。

## 25.6 插件的配置文件

简单的插件始终完全可以通过命令行进行配置。如果你需要包含更复杂的默认值，或者参数不应以进程列表参数的形式出现，那么配置文件可能会很有用。`Nagios::Plugin` 模块允许你以简单的方式访问配置文件——这显然是为了将配置工作简化为统一的格式，这将极大简化 Nagios 管理员的配置工作，因为他们不再需要为每个插件都使用不同的格式。

`Nagios::Plugin` 为 `Config::Tiny` 模块提供了一个接口。该文件格式与 INI 文件对应：`rootproperty=1.0`

```
[math]
pi=3.1415
euler=2.728
```

一个节以方括号中的条目开始，在本例中为 `[math]`。在此之前的所有内容（在示例中，变量 `root-property`）被称为 `rootproperty`。指令通过 `pattern parameter=value` 模式给出。以 `#` 和 `;` 开头的行会被忽略；等号前后的空格会被简单忽略。更多信息请参阅 `Config::Tiny` 的帮助页面（man page）。

通过来自 `Nagios::Plugin::Config` 模块的 `Config` 对象来访问配置文件，该对象是通过 `read()` 方法生成的：

```perl
$Config = Nagios::Plugin::Config->read('/etc/nagios/myplugin.ini');
$myrootproperty = $Config->get('rootproperty');
$mypi = $Config->get('pi');
$meyeruler = $Config->get('euler');
```

同时，`read` 会读取指定的配置文件。如果你省略路径细节并在不带参数的情况下调用 `call()`，模块将搜索各种配置文件。搜索路径的精确列表包含在 `Nagios::Plugin::Config` 的帮助页面中。

虽然可以想象所有插件都使用同一个配置文件，但从维护角度考虑，建议为每个插件设置单独的配置文件，并包含一个示例。

`[math]` 节中的配置参数现在通过构造 `$Config->{math}->{pi}` 进行访问，而对于根属性，使用 `_` 作为节分隔符：`$Config->{_}_->{rootproperty}`。

## 第 26 章. 使用 Instant Client 监控 Oracle

如果特定任务需要你同时操作外部程序的 STDIN 并读取其 STD-OUT，则需要另一种工具，形式为 `IPC::open2` 模块。

本章将不会介绍任何现成的插件，而是通过一个监控 Oracle 的示例来说明你如何构建自己的 Oracle 插件。对于此 DBMS 已经存在插件，例如标准 Nagios 插件之一的 `check_oracle`，或者由 Mathias Kettner 编写的 `check_oracle_writeaccess`。但它们都需要标准的 Oracle 客户端，非 Oracle 管理员在尝试安装它时会感到力不从心。

幸运的是，有一个更简单的解决方案：长期以来，Oracle 一直提供 *instant client*（即时客户端），它大大减少了安装工作：解压 zip 文件，设置变量，安装就完成了——可以立即使用命令行工具 `sqlplus`。后者可以在插件中使用——就像本章介绍的 Perl 脚本一样，使用 `sqlplus` 向 Oracle 数据库发送请求并评估响应。

### 26.1 安装 Oracle Instant Client

尽管该客户端自 Oracle 10g 版本起才可用，但它也可以用于较旧的 Oracle 数据库，如 8i 或 9。软件以 zip 文件的形式在 Oracle 主页上提供，前提是你之前已经在公司网站上注册过。下载时，系统会询问你关于导出条件的一些额外问题。

尽管软件是免费的，但你必须遵守 Oracle 的许可条款。如果你的 Oracle 数据库是基于 CPU 许可的，你不需要担心另一个用户（Nagios）的额外访问。

对于 `sqlplus`，你需要两个 zip 文件：`instantclient-basic-linux32-10.1.0.3.zip` 和 `instantclient-sqlplus-linux32-10.1.0.3.zip`。

`instantclient-basic` 包大小约为 31 MB，包含了所有库，而 `instantclient-sqlplus` 只有 320 KB，包含一份简短的文档（`README_IC.html`）以及客户端本身的一个额外库。在哪里解压文件并不重要；在这种情况下我们将使用 `/usr/local/oracle`。

```bash
linux: # mkdir /usr/local/oracle
linux: # cd /usr/local/oracle
linux:local/oracle unzip instantclient-basic-linux32-10.1.0.3.zip
Archive: instantclient-basic-linux32-10.1.0.3.zip
inflating: instantclient10_1/classes12.jar
```
