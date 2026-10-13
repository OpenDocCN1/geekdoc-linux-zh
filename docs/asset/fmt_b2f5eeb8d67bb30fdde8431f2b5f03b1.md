
## 安装路径选项

| `--mandir=DIR` | 在 `DIR` 中安装手册（man）页 |
| `--sysconfdir=DIR` | 在 `DIR` 中安装配置文件 |
| `--datadir=DIR` | 在 `DIR` 中安装只读数据文件 |
| `--includedir=DIR` | 在 `DIR` 中安装包含文件 |
| `--localstatedir=DIR` | 在 `DIR` 中安装可修改数据文件 |
| `--runtimedir=DIR` | 在 `DIR` 中安装运行时数据 |
| `--logfiledir=DIR` | 在 `DIR` 中安装日志文件数据 |
| `--proxycachedir=DIR` | 在 `DIR` 中安装代理缓存数据 |
| `--compat` | 按照 Apache 1.2 安装路径进行安装 |

例如，如果你将日志保存在名为 `/logs` 的单独分区中，并且希望 Apache 在那里写入日志，则按如下方式运行 `configure` 脚本：

```
./configure --prefix=/usr/local/apache --logfiledir=/logs
```

如果你想百分之百确定哪个文件将安装到哪个目录，请使用 `--layout` 选项。例如，

```
./configure --prefix=/usr/local/apache --layout
```

显示以下输出：

```
Configuring for Apache, Version 1.3.9

Installation paths:
prefix: /usr/local/apache
exec_prefix: /usr/local/apache
bindir: /usr/local/apache/bin
sbindir: /usr/local/apache/bin
libexecdir: /usr/local/apache/libexec
mandir: /usr/local/apache/man
sysconfdir: /usr/local/apache/etc
datadir: /usr/local/apache/share
includedir: /usr/local/apache/include
localstatedir: /usr/local/apache/var
rundir: /usr/local/apache/var/run
logfiledir: /usr/local/apache/var/log
proxycachedir: /usr/local/apache/var/proxy

Compilation paths:
HTTPD_ROOT: /usr/local/apache
SUEEXEC_BIN: /usr/local/apache/sbin/suexec
SHARED_CORE_DIR: /usr/local/apache/libexec
DEFAULT_PIDLOG: var/run/httpd.pid
DEFAULT_SCOREBOARD: var/run/httpd.scoreboard
DEFAULT_LOCKFILE: var/run/httpd.lock
DEFAULT_XFERLOG: var/log/access_log
DEFAULT_ERRORLOG: var/log/error_log
TYPES_CONFIG_FILE: etc/mime.types
SERVER_CONFIG_FILE: etc/httpd.conf
ACCESS_CONFIG_FILE: etc/access.conf
RESOURCE_CONFIG_FILE: etc/srm.conf
```

`--layout` 选项允许你在实际使用之前验证目录结构。如果你从 1.2 升级 Apache 并希望保留旧的目录结构，可以使用 `--compat`，它使用旧式的目录结构。

![](img/c2419364ebb911c809b6a79991707c27_312_0.png)

### 提示

如果你发现自己不断覆盖默认布局，可以简单地在 `configure.layout` 文件中创建一个自定义布局。创建自定义布局最简单的方法是编辑顶层 Apache 源代码分发包中的 `configure.layout` 文件。复制从 `<Layout apache>` 行开始到 `</Layout>` 结束的现有 Apache 布局。然后，按你喜欢的方式更改目录路径，并将布局名称从 `Apache` 更改为你喜欢的名称。然后，你可以使用 `--with-layout=<你的自定义布局名称>` 选项使用此布局。

配置 Apache 的下一步是决定是否要使用 Apache 开发者提供的标准模块配置。如果你第一次编译 Apache，请坚持使用标准配置，只是为了熟悉整个过程。

`APACI` 基于配置的标准或默认配置文件是 `Configuration.apaci`，它存储在 `src` 子目录中。此文件包含三种类型的信息：

- `EXTRA_*` lines. 由 `configure` 脚本用于在 `Makefile` 中添加额外标志，而这又需要编译 Apache。
- Rule lines. 由脚本用于打开/关闭某些功能。
- `AddModule` lines. 启用应成为 Apache 可执行文件一部分的 Apache 模块。

## Makefile 配置选项

对于大多数系统，你不需要修改任何这些额外标志。另请注意，`configure` 脚本将尝试找出系统上使用的 C 编译器。如果你认为它可能由于某种原因找不到你的编译器，请取消注释 `#CC=` 行并指向你的编译器。例如：`CC = gcc`

在这种情况下，你可能还需要在以下行中提供额外的编译器标志：

```
EXTRA_CFLAGS=
EXTRA_LDFLAGS=
```

如果你的系统需要特殊的库或包含文件，请使用以下行指定它们：

```
EXTRA_LIBS=
EXTRA_INCLUDES=
```

`configure` 脚本自动将代码优化设置为 `-O2`。如果你想要不同的设置，首先取消注释以下行：

```
#OPTIM=-O2
```

然后，如果你的 C 编译器支持，将值更改为你想要的。对于大多数安装，默认设置效果很好，就像我在 Red Hat 5.2 Linux 系统上一样。

## 规则配置选项

与 `Makefile` 标志一样，你不需要修改 Rules 行。但是，如果你必须修改这些规则，可以使用 `configure` 脚本。要启用规则，请使用 `--enable-rule=NAME` 选项，其中 `NAME` 是规则的名称。例如：

```
./configure --prefix=/usr/local/apache --enable-rule=SOCKS4
```

同样，通过使用 `--disable-rule` 选项禁用规则。

前两条 Rule 行（`SHARED_CORE` 和 `SHARED_CHAIN`）与动态共享对象（DSO）支持有关，应保持不变。

默认情况下关闭 `SOCKS4` 功能。`SOCKS` 是一个控制系统，其中所有 TCP/IP 网络应用程序数据都通过 `SOCKS` 守护进程传输。这使 `SOCKS` 能够收集、审计、筛选、过滤和控制网络数据。大多数人将其用作基于软件的防火墙。如果你想使 Apache `SOCKS4` 兼容，你需要通过在 `configure` 脚本命令行中使用 `--enable-rule=SOCKS4` 选项将其设置为 Yes 来打开此功能。此外，修改 `Makefile` 配置区域中的 `EXTRA_LIBS` 设置，以指向你的 `SOCKS4` 库文件。否则，`configure` 脚本将将其设置为 `-`。同样，如果你想要 `SOCKS5` 支持，请通过在 `configure` 脚本命令行中使用 `--enable-rule=SOCKS5` 选项将其设置为 Yes 来打开它。

The `IRIXNIS` rule is for people who want to use Apache on a Silicon Graphics system running IRIX and NIS. The `IRIXN32` option is also meaningful for systems running an IRIX operating system. It tells Apache to use n32 libraries instead of o32 libraries.

The `PARANOID` rule allows you to see whether any Apache module is executing any shell scripts during configuration. Apache 1.3 allows modules to execute custom shell scripts when the `configure` script is run. This rule is turned off by default. If you want to enable it, set this to Yes using the `--enable-rule=PARANOID` option in the command line of the `configure` script.
