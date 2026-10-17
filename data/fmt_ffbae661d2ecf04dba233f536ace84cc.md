
这些是 Apache 1.3.12 版本源代码发行版的示例。它们之间的唯一区别在于大小，这是由于使用的压缩技术不同造成的。请下载其中一个文件。无论下载哪种格式，你都需要 `tar` 工具以及 `gzip` 或 `bzip2` 工具来解压文件。例如，要在我的 Red Hat 7.0 系统上解压 `Apache 1.3.12.tar.gz` 文件，我使用以下命令：

```bash
tar xvzf apache_1.3.12.tar.gz
```

或者我可以使用

```bash
gzip -d apache_1.3.12.tar.gz
tar xvf apache_1.3.12.tar
```

这将解压并提取所有文件到一个子目录中，同时保持每个文件的相对路径完整。

自己编译 Apache 源代码而不是使用别人的二进制文件是个好主意。当你使用下载的二进制文件时，你实际上是在让其他人（可能是你都不认识的人）决定在你的 Web 服务器中启用哪些模块和功能。偶尔，由于二进制文件所需的库文件与你系统上可用的文件之间的不兼容性，下载的二进制文件在你的系统上可能完全无法工作。如果这是可以接受的，或者对你来说编译不是选项，请确保你下载二进制文件的站点是信誉良好的。本章假设你将编译自己的副本。

## 创建自定义 Apache 服务器

提取源代码后，你就可以配置和编译你的自定义 Apache 副本。你可以手动配置 Apache，或者使用称为 `APACI` 的新式 Autoconf 接口。我推荐 `APACI` 方法，因为它更快，并且对 Apache 配置细节的知识要求较少；换句话说，你需要阅读更少的 `README` 和 `INSTALL` 文件就能完成任务。

### 使用 APACI 配置 Apache 源代码

在源代码发行版的顶级目录中有一个名为 `configure` 的脚本，这是你需要用来通过 `APACI` 配置 Apache 的工具。按以下方式运行此脚本：

```bash
./configure --help
```

这使你可以查看所有可用的选项。

这将所有 Apache 文件安装到指定的目录下。但是，如果你需要安装某些文件到目录外部，可以使用表 12-1 中显示的 `--prefix` 选项。

#### 表 12-1 configure 脚本的选项

| 前缀选项 | 描述 |
| :--- | :--- |
| `--exec-prefix=DIR` | 在 `DIR` 中安装架构相关的文件 |
| `--bindir=DIR` | 在 `DIR` 中安装可执行文件 |
| `--sbindir=DIR` | 在 `DIR` 中安装系统管理可执行文件 |
| `--libexecdir=DIR` | 在 `DIR` 中安装程序可执行文件 |
| `--mandir=DIR` | 在 `DIR` 中安装手册 `man` 页 |
| `--sysconfdir=DIR` | 在 `DIR` 中安装配置文件 |
| `--datadir=DIR` | 在 `DIR` 中安装只读数据文件 |
| `--includedir=DIR` | 在 `DIR` 中安装头文件 |
| `--localstatedir=DIR` | 在 `DIR` 中安装可修改的数据文件 |
| `--runimedir=DIR` | 在 `DIR` 中安装运行时数据 |
| `--logfiledir=DIR` | 在 `DIR` 中安装日志文件 |
| `--proxycachedir=DIR` | 在 `DIR` 中安装代理缓存数据 |
| `--compat` | 按照 Apache 1.2 的安装路径安装 |

例如，如果你将日志保存在名为 `/logs` 的分区中，并希望 Apache 在那里写入日志，请按以下方式运行 `configure` 脚本：

```bash
./configure --prefix=/usr/local/apache --logfiledir=/logs
```

如果你想 100% 确定哪个文件将安装到哪个目录，请使用 `--layout` 选项。例如，

```bash
./configure --prefix=/usr/local/apache --layout
```

显示以下输出：

Configuring for Apache, Version 1.3.12

```text
Installation paths:
prefix: /usr/local/apache
exec_prefix: /usr/local/apache
```

### Apache 目录结构配置

以下显示了编译时的默认目录路径：

```
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
```

编译路径详情：

```
HTTP_ROOT: /usr/local/apache
SUEXEC_BIN: /usr/local/apache/sbin/suexec
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

`--layout` 选项允许你在实际创建目录结构之前对其进行验证。如果你正在从 Apache 1.2 升级，并希望保留旧的目录结构，请使用 `--compat`，该选项使用旧式目录结构。

配置 Apache 的下一步是决定你是否希望使用开发人员提供的标准模块配置。如果你第一次编译 Apache，请坚持使用标准配置，以便熟悉整个流程。

> 提示
> 如果你发现自己经常需要覆盖默认布局，你可以简单地通过在 `confignore.layout` 文件中创建自定义布局来实现。创建自定义布局最简单的方法是编辑顶级 Apache 源发行版中的 `confignore.layout` 文件。复制以 `<Layout apache>` 行开始并以 `</Layout>` 结尾的现有 Apache 布局。然后，按你的意愿更改目录路径，并将布局名称从 Apache 更改为你喜欢的任意名称。然后，你可以使用 `--with-layout=<你的自定义布局名称>` 选项来使用该布局。

基于 `APACI` 的标准或默认配置文件是 `Configuration.apaci`，它存储在 `src` 子目录中。该文件包含三种类型的信息：

- `EXTRA *` 行。用于在 `Makefile` 中添加额外标志，供 `configure` 脚本使用，进而用于编译 Apache。
- `Rule` 行。用于让脚本开启或关闭某些功能。
- `AddModule` 行。启用应作为你的 Apache 可执行文件一部分的 Apache 模块。

### Makefile 配置选项

对于大多数系统，你不需要修改这些额外标志中的任何一个。还要注意，`configure` 脚本将尝试确定你在系统上使用的 C 编译器。如果你认为它可能因为某种原因无法找到你的编译器，请取消注释 `#CC=` 行并将其指向你的编译器。例如：`CC=gcc`。

在这种情况下，你还可能需要提供以下行中的额外编译器标志：

```
EXTRA_CFLAGS=
EXTRA_LDFLAGS=
```

如果你的系统需要特殊的库或 `include` 文件，请使用以下行指定：

```
EXTRA_LIBS=
EXTRA_INCLUDES=
```

`configure` 脚本自动将代码优化设置为 `-O2`。如果你想要不同的设置，首先取消注释以下行：

```
#OPTIM=-O2
```

然后，将值更改为你想要的任何值（如果 C 编译器支持的话）。对于大多数安装，默认设置工作良好，就像在 Red Hat 7.0 Linux 系统上对我来说那样。

### 规则配置选项
