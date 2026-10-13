
标准的 Apache 源码发行版约为 5–6 兆字节 (MB)。Apache 组建议你留 12MB 的临时磁盘空间用于编译。然而，如果你只安装预编译的二进制发行版，则不需要源代码。二进制发行版的大小取决于操作系统，但不太可能超过 5-6MB 的限制。无论哪，对于 Apache 软件本身，你只需要 5–6MB 的磁盘空间。

如果你计划安装其他第三方模块（如 `mod_fastcgi`、`mod_perl` 或 `mod_php`），你需要额外的磁盘空间。

尽管 Apache 本身可能只占用少量磁盘空间，但如果你在高流量网站上安装 Apache，你可能需要仔细考虑日志空间需求。高流量网站可能会产生大量的日志记录，这可能需要大量磁盘空间。例如，一条典型的日志记录可能占用约 80 字节的磁盘空间。如果你预计每天大约有一百次访问，那么你的 Apache 访问日志文件每天可能会增长八字节。提前计划并为 Apache 分配足够的日志空间。

## 足够的内存 (RAM)

足够的内存可能是最重要的安装前要求。Apache 在“服务器池”模式下运行，这意味着多个 Apache 服务器进程 (`httpd`) 实例将运行以处理请求。你的系统上运行的服务器进程数量可以通过 Apache 指令（如 `MinSpareServers`、`MaxSpareServers` 等）进行配置。这些服务器进程都会使用大致相同的内存。要计算所需的内存，公式如下：

Apache 所需内存 = 最大 Apache 进程数 × 单个 Apache 进程所需的内存

这将给你一个所需内存大致的想法。在运行标准 Apache 的 Red Hat 5.2 系统上（即直接来自发行版），每个 Apache 进程大约占用 1.5MB。如果我想最多运行十个进程（使用 `MaxSpareServers`），那么 Apache 需要 15MB 内存，再加上操作系统和其他服务器进程所需的内存。请记住，内存需求随平台而异，而且当你向 Apache 添加第三方模块时，内存需求也会增加。例如，`mod_perl` 无疑会让 Apache 进程变大。事实上，每个启用了 `mod_perl` 的 Apache 进程都包含你的 Perl 脚本，这将增加内存需求。因此，如果你计划在 Apache 中使用 `mod_perl`，请确保内存充足。在这种情况下，不要忘记计算你计划配合 `mod_perl` 使用的 CGI 所需的内存。

## 其他要求

某些支持脚本（如 `dbmanager` 和 `apxs`）使用 Perl 5 解释器。我建议从以下网站下载最新的 Perl 解释器：http://www.perl.com/。

Apache 1.3 还可以利用动态共享对象 (`DSO`) 机制在运行时加载和卸载模块。虽然 Linux 支持 `DSO`，但我个人在编译 Apache 时未使用 `DSO` ，因为它显然会导致服务器执行速度降低约 5%。

## 从网上获取 Apache

虽然 Red Hat Linux 官方自带预编译 Apache Web 服务器的 RPM 包，但你可能仍然想从 Apache 官方网站下载最新版本，URL 为：http://www.apache.org/

如果你不在美国，从附近的 Apache 镜像站点获取 Apache 源码和二进制文件可能会更快。使用 URL http://www.apache.org/dyn/closer.cgi 来寻找你附近的良好镜像站点。我假设你从官方 Apache 网站获取软件，Apache 软件（包括源码和二进制文件）可以在 http://www.apache.org/dist/ 找到。

你会看到许多使用各种压缩程序归档的 Apache 发行版本。例如：

```
Apache_1.3.6.tar.gz
Apache_1.3.6.tar.Z
```

这些都是 Apache 1.3.6 版本源码分发的示例。区别在于由于压缩技术的不同导致的大小。这些文件中，无论你选择下载哪种格式，你需要的都是 `tar` 工具以及 `gunzip` 或 `gzip` 工具来解压文件。例如，在我的 Red Hat 5.2 系统上解压 Apache 1.3.6.tar.gz 文件，我使用以下命令：

```
tar xvzf apache_1.3.6.tar.gz
```

或者我可以使用：

```
gzip -d apache_1.3.6.tar.gz
tar xvf apache_1.3.6.tar.gz
```

这将解压并提取子目录中的所有文件，同时保持每个文件的相对路径完整。

二进制文件通常保存在一个目录中，每个操作系统都有自己的子目录。自己编译 Apache 源码而不是使用他人的二进制文件是一个好主意。当你使用下载的二进制文件时，你是在让别人（可能是一个你不认识的人）决定你的 Web 服务器中启用了哪些模块和功能。偶尔，下载的二进制文件可能在你的系统上无法运行，因为二进制文件所需的库文件与系统上的可用文件之间可能存在不兼容性。如果这是可以接受的或者对你来说无法编译，请确保下载二进制文件的网站是可靠的。在本章中，我将假设你想要编译自己的副本，并在后续章节中讨论创建自定义 Apache 服务器涉及的过程。

## 创建自定义 Apache 服务器

一旦你将源码解压到选择的目录中，就可以准备配置并编译你自定义的 Apache 版本。你可以手动配置 Apache，也可以使用名为 `APACI` 的新 Autoconf 风格接口。我更倾向于使用 `APACI` 方法，因为它更快且对 Apache 配置细节的了解要求较少；换句话说，你只需要更少的 `README` 和 `INSTALL` 文件即可完成工作。因此，这也是推荐的方法。

### 使用 APACI 配置 Apache 源码

在源码分发的顶目录下，你会找到一个名为 `configure` 的脚本，这就是你使用 `APACI` 配置 Apache 所需要的。你可以如下所示运行该脚本：

```
./configure --help
```

这将允许你看到所有可用选项。

配置 Apache 的第一步是确定你想将它安装在哪里。例如，要将 Apache 安装在名为 `/usr/local/apache` 的目录中，你可以如下运行配置脚本：

```
./configure --prefix=/usr/local/apache
```

这会将 Apache 文件安装在指定的目录下。然而，如果由于某些原因你需要将某些文件安装在目录之外，可以使用 `--prefix` 选项：

- `--exec-prefix=DIR`: 在 `DIR` 中安装依赖于架构的文件。
- `--bindir=DIR`: 在 `DIR` 中安装执行文件。
- `--sbindir=DIR`: 在 `DIR` 中安装系统管理执行文件。
- `--libexecdir=DIR`: 在 `DIR` 中安装程序执行文件。
- `--mandir=DIR`: 在 `DIR` 中安装手册（man）页。
- `--sysconfdir=DIR`: 在 `DIR` 中安装配置文件。
- `--datadir=DIR`: 在 `DIR` 中安装只读数据文件。
- `--includedir=DIR`: 在 `DIR` 中安装包含文件。
- `--localdir=DIR`: 在 `DIR` 中安装可修改的数据文件。
- `--runtimedir=DIR`: 在 `DIR` 中安装运行时数据。
- `--logfiledir=DIR`: 在 `DIR` 中安装日志文件数据。
- `--proxycachedir=DIR`: 在 `DIR` 中安装代理缓存数据。
- `--compat`: 根据 Apache 1.2 安装路径安装。

例如，如果你将日志保留在名为 `/logs` 的独立分区中，并希望 Apache 将日志写到那里，你可以如下运行配置脚本：

```
./configure --prefix=/usr/local/apache --logfiledir=/logs
```

## 第四部分：设置内网/互联网服务

如果你想百分之百确定哪个文件将安装在哪个目录，请使用 `--layout` 选项。例如：

```
./configure --prefix=/usr/local/apache --layout
```

这将显示以下输出：

Configuring Apache, Version 1.3.6
