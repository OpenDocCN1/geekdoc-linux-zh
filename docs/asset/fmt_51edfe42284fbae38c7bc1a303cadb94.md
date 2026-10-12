
其中`hostname`是连接到您服务器的主机的名称或 IP 地址，`permissions`是这些用户的权限集，`num_users`是可以同时连接到该服务的最大用户数。

权限通过使用以下四个单词的任意组合来设置，或者在这些单词前加上感叹号表示“不允许”。权限关键字如下：

- `browse` — 可以查看目录内容。如果禁止此权限，用户可以访问条目，但无法获取目录内容。
- `ftp` — 允许服务器作为 FTP 服务的网关。
- `read` — 可以访问文件。如果被禁止，用户请求文件时会收到`BummerMsg`。
- `search` — 可以访问索引（输入 7 项）。如果被禁止，则不允许访问索引。这主要与 Gopher+ 一起使用。

例如，要设置访问权限以允许来自网络 chatton.com 的多达 10 个用户以完全权限访问您的 Gopher 服务器，请添加如下行：

```
access: chatton.com    browse ftp read search 10
```

每个条目之间至少有一个空格，包括权限之间也是如此。此访问条目：

```
access: bignet.org !browse !ftp read search 3
```

允许来自 bignet.org 的三个并发用户访问 Gopher 服务器并执行读取和搜索，但不允许使用 FTP 网关或浏览目录列表。

如果您使用 IP 地址，可以使用 IP 地址的子集来表示整个网络。例如，如果 bignet.com 的网络地址是 147.12，您可以使用如下一行表示整个网络：

```
access: 147.12. !browse !ftp read search 3
```

您必须在 IP 地址中指定的最后一组数字后跟一个点，否则 147.120 到 147.129 也将具有相同的权限（因为它们匹配指定的数字）。

如果您希望允许来自特定机器的访问，也可以这样做。例如，要允许您朋友的 darkstar 机器以完全权限访问您的 Gopher 服务器，请添加如下一行：

```
access: darkstar.domain.name browse ftp read search 1
```

大多数通用 Gopher 服务器倾向于允许任何人连接，因此它们使用默认条目来引用未被其他访问条目明确定义的人。默认设置通常如下：

```
access: default !browse !ftp read search 15
```

这允许任何人读取和搜索 Gopher 目录，但不允许他们遍历目录或将您的机器用作 FTP 网关。

## 设置 Makefile

为了使编译过程正确进行，需要修改两个文件。这两个文件是`Makefile.config`和`conf.h`。由于在 Linux 系统上有许多版本的 Gopher，这些文件所需的配置参数可能已经设置好了，但您应仔细检查数值以防止出现问题。

`Makefile.config`文件（由 Makefile 用于构建可执行文件）是一个很长的文件，因此在浏览它时要小心，以避免意外更改。需要检查的重要区域是目录定义以及服务器和客户端设置。以下部分将分别介绍这些内容。

您可能希望更改的一项设置是调试工具，它在大多数系统中默认启用。这可以帮助您正确运行系统，但当操作正常时，您应重新编译源代码并移除调试功能，以使过程更快、更小，并减少调试信息开销。要移除调试功能，请注释掉`DEBUGGING`行，使其看起来像这样：

```
#DEBUGGING = -DDEBUGGING
```

默认情况下，该行可能未被注释。

目录定义通常在一个包含五到七个条目的块中，具体取决于 man 页面的条目数量。典型的目录定义块看起来像这样：

```
PREFIX = /usr/local
CLIENTDIR = $(PREFIX)/bin
CLIENTLIB = $(PREFIX)/lib
SERVERDIR = $(PREFIX)/etc

MAN1DIR = $(PREFIX)/man/man1
MAN5DIR = $(PREFIX)/man/man5
MAN8DIR = $(PREFIX)/man/man8
```

大多数`Makefile.config`文件的主要更改是`PREFIX`，它用于设置 Gopher 的基本目录。默认值通常是`/usr/local`，尽管您可以将其更改为任何您想要的值（例如`/usr/gopher`）。其余变量定义了主要 Gopher 目录下的子目录，通常保持原样即可。您可以将子目录保持原样，也可以根据您的需求进行更改。如果您愿意，可以将所有文件放在一个目录中。每个变量的含义如下列表所示：

- `CLIENTDIR` Gopher 客户端软件
- `CLIENTLIB` 客户端帮助文件（gopher.hlp）
- `MAN1DIR` Gopher 客户端的 Man 页面
- `MAN8DIR` gopherd 的 Man 页面
- `SERVERDIR` Gopher 服务器（gopherd）和配置文件（gopherd.conf）

为了让 Gopher 客户端在您的系统上正确运行，您必须修改`Makefile.config`文件中的`CLIENTOPTS`行。控制`CLIENTOPTS`行行为的两个选项如下：

- `-DNOMAIL` 禁止远程用户通过邮件发送文件。
- `-DAUTOEXITONIU` 允许使用 u 命令以及 q 命令退出 Gopher 客户端。

要使用这些选项中的一个或两个，请像这样将它们添加到`CLIENTOPTS`行：

```
CLIENTOPTS = -DNOMAIL -DAUTOEXITONIU
```

与 Gopher 服务器相关的四个变量也必须设置。这些指定主机域名、Gopher 应使用侦听连接的端口、数据文件的位置以及选项标志。

域名通过`DOMAIN`变量设置。名称中应有一个前导点，例如：

```
DOMAIN = .tcpi.com
```

如果 hostname 命令返回服务器的完全限定域名，则无需设置此变量。在这种情况下，请留空该值。

`SERVERPORT`变量定义了 Gopher 用于等待服务的端口，通常设置为 TCP 端口 70。此行通常看起来像这样：

```
SERVERPORT = 70
```

如果您不允许互联网用户对您的 Gopher 站点进行通用访问，您可以更改此值。但是，如果您希望允许互联网用户（即使是一个非常小的子集）访问，您应该保持端口为 70。如果您只为小网络设置 Gopher 站点，那么可以选择任何您想要的端口号（介于 1024 和 9999 之间），并确保所有 Gopher 客户端也使用该号码。

`SERVERDATA`变量定义了您的 Gopher 服务器提供的数据位置。其默认设置通常如下：

```
SERVERDATA = /gopher-data
```

将变量设置为您用于 Gopher 项目的文件位置。

`SERVEROPTS`变量接受多个关键字，这些关键字会改变 Gopher 服务的行为。典型的条目看起来像这样：

```
SERVEROPTS = -DSETPROCTITLE -DCAPFILES #-DBIO -DDL
```

井号后的关键字在 Makefile 运行时会被忽略，因此如果变量顺序允许这种简单方法，您可以调整其位置来设置所需的选项。以下列出了`SERVEROPTS`条目中允许的不同关键字的含义：

- `-DADD_DATE_AND_TIME`
  在标题中添加日期和时间。
- `-DBIO`
  仅用于 Don Gilbert 开发的 WAIS 版本（wais8b5）。
- `-DDL` 提供支持 `dl` 数据库实用工具

- `-DDL` 提供支持 `dl` 数据库实用工具的功能（需要在名为 `DLPATH` 的目录变量中包含 `dl` 系统，并且取消注释 `DLOBJS` 行以显示文件 `getdesc.o` 和 `enddesc.o` 的位置）。
- `-DCAPFILES` 提供与 `cap` 目录的向后兼容性。
- `-DLOADRESTRICT` 基于并发用户数量限制用户访问权限（参见下一节）。
- `-DSETPROCTITLE` 设置由 `ps` 命令显示的名称（仅限基于 BSD UNIX 的系统）。

`conf.h`文件在编译过程中用于设置关于 Gopher 服务的其他参数。对于设置 Gopher 服务而言，重要的设置至少包括那些与查询数量和超时变量相关的设置。这些设置通常位于`conf.h`文件的末尾。

`WAISMAXHITS`变量定义了查询 WAIS 数据库时可以提供结果的最大命中数，通常设置为 40 左右。该变量的定义如下：

```c
#define WAISMAXHITS 40
```

请注意，由于这是用 C 语言编写的，井号不是注释符号。井号是预处理器指令的重要组成部分，应保留原样。定义中也没有等号。
