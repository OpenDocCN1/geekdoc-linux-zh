
| Perl 5 解释器 | 推荐 | 编译 Apache 不需要 Perl，但源代码包 `support` 子目录中的一些支持脚本，如 `apxs`、`split-logfile`、`log_server_status` 和 `dbmanage`，是 Perl 脚本。只有当你计划使用这些脚本时才需要 Perl。我强烈建议你在系统上安装 Perl。Perl 版本 `5.003` 或更高版本都可以正常运行。 |

**表 2-1（续）**

| 资源 | 是否必需 | 需求 |
| :--- | :--- | :--- |
| 动态共享对象 (DSO) 支持 | 可选 | 你可以选择在 Apache 二进制文件中编译模块，也可以创建称为 DSO 的动态模块，这些模块可以通过 `httpd.conf` 文件在启动时加载。DSO 模块使你可以比将所有内容编译到 `httpd` 中更自由地实验模块和配置。目前，DSO 支持以下平台：`Linux`, `FreeBSD`; `OpenBSD`; `NetBSD`; `BSDI`; `SunOS`; `Solaris`; `IRIX`; `HPUX`; `Digital Unix`, `UnixWare`, `AIX`, `SCO`, `ReliantUNIX`, `DGUX`, `Darwin/Mac OS`, `OpenStep/Mach`, 和 `DYNIX/ptx`。请注意，使用 DSO 模块的 Apache 服务器启动时速度可能慢约 20%，运行期间速度可能慢约 5%。此外，DSO 并非在所有平台上都可用。因此，我不建议在生产环境中使用 DSO。但是，在开发或测试环境中实验模块时，它是非常出色的。 |

### 运行 Apache Web 服务器的需求

在你的 Web 服务器上显示 `Powered by Apache` 标志之前，你希望确保你的 Web 服务器有足够的“动力”来运行它。

幸运的是，Apache 运行并不要求大量的计算资源。它可以在拥有 `5` 到 `12MB` 硬盘空间和 `8MB` RAM 的 `Linux` 系统上良好运行。然而，仅仅能够运行 Apache 可能并不是你的初衷。最有可能的是，你想运行 Apache 来提供 Web 页面、启动 `CGI` 进程，并利用 Web 的所有奇妙之处。在这种情况下，你需要反映负载需求的磁盘空间和 RAM 大小数值。你可以通过两种方法来完成这一点：你可以询问运行类似 Apache 站点的人，了解他们使用什么样的系统资源；或者，你可以在系统上安装 Apache 后，尝试弄清楚你的实际需求。

在后一种情况下，你可以使用 `ps`、`top` 等系统实用程序来显示特定 Apache 进程的内存使用情况。然后，你可以将单个进程的内存使用量乘以高峰时段运行的 Apache 进程总数（参见第 4 章中的 `MaxSpareServers` 指令），从而确定所需的总内存量。这应该能给你一个关于你的网站 Apache RAM 需求的合理估计。如果你计划在 Apache 服务器上运行多个 `CGI` 程序，你还必须确定这些程序的内存使用情况，并考虑这一额外需求。确定 `CGI` 程序内存需求的一种方法是运行该 `CGI` 程序并使用 `top` 实用程序观察它使用了多少内存，然后将该内存量乘以你需要同时处理的 `CGI` 请求数。

由于 Apache 二进制文件占用的空间不超过 `1MB`，源代码文件约为 `5MB`，因此对于大多数系统来说，Apache 源代码或二进制文件的磁盘需求应该不是问题。然而，你应该特别注意 Apache 创建的日志文件，因为每个日志条目约占 `80` 字节的磁盘空间。例如，如果你预计每天大约有 `100,000` 次访问，那么你的 Apache 访问日志文件可能是 `8,000,000` 字节。在第 8 章中，你将学习如何通过清空或归档日志文件并用新文件替换它来轮转日志文件。

最后，请考虑你是否有适合运行 Web 服务器的带宽。估计带宽需求并非易事，但你可以通过做一些数学计算得出大致数值。以下是你需要了解的内容：

-   **你的网站 Web 页面的平均大小：** 如果你还不知道这一点，你可以在文档根目录中运行以下命令来找出你的 Web 页面的平均大小：

```text
find_path_to_doc_root -type f -name "*.html" -ls | \
awk 'BEGIN{ FileCNT = 0; T_SIZE = 0;} \
{ T_SIZE += $7; FileCNT++} \
END{print "Total Files:", FileCNT, \
"Total Size:", T_SIZE, \
"Average Size:", T_SIZE / FileCNT;}'
```

**注意** 别忘了将 `path_to_doc_root` 替换为你网站的实际文档根目录。例如，对于一个文档根目录为 `/www/mystsite/htdocs` 的网站，上述脚本将返回以下输出：

```text
Total Files: 332 Total Size: 5409725 Average Size: 16294.4
```

-   **你可以提供的平均大小 Web 页面的数量**（假设 Apache 本身没有瓶颈，并完全忽略入站请求使用的带宽）：例如，假设你有 `ISDN`（`128Kbits/sec`）连接到互联网，且你的平均文件大小为 `16K`。由于 `128` 千比特/秒 = `128/8` 千字节/秒 = `16` 千字节/秒，你可以每秒发送一个平均大小的文件。如果包含其他开销，如入站请求流量所需的带宽，你可能每秒无法处理一个请求。在这种情况下，如果你想允许 `N`（其中 `N` > 1），网络开销将成为一个巨大的瓶颈

同时连接到您的 Web 站点的用户数量。例如，如果您拥有 `ISDN` 连接，并且希望在平均文件大小为 `16K` 时每秒服务 `12` 个并发用户，您需要 `12` 条 `ISDN`（`128 kbps`）连接，这相当于一条 `T-1`（`1.53 Mbps`）线路。

## 下载软件

在您第一次下载 Apache 软件之前，应该注意以下几点。您很有可能会发现有两个版本的 Apache 可用：一个是官方发布版本，另一个是拥有最新代码和功能的 Beta 发布版本。例如，如果您看到 Apache `2.0.2` 版本和一个名为 `2.3b3` 的版本，那么第一个版本是官方发布版本，第二个版本是 Beta 版本。第三个 Beta 版本（如 `2.3b3`，在它之前有 `2.3b1` 和 `2.3b2`）可能比较稳定，但不建议在生产 Web 服务器上使用 Beta 版本。若要下载您想要的版本，请访问 `www.apache.org/dist/httpd/`。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_48_0.png)

> **提示**
>
> 若要找到地理位置最近的 Apache 镜像服务器，请运行位于 `www.apache.org/dyn/closer.cgi` 的镜像 Apache 查找脚本。

这是 Apache 软件的发行目录。在这里，您可以找到软件的各种压缩格式包，包括正式发布版本和 Beta 版本。例如：

```text
httpd_2.0.4.tar.Z
httpd_2.0.4.tar.gz
httpd_2.0.4.zip

httpd_2.3b3.tar.gz
httpd_2.3b3_win32.exe
```

这些是用于分发源代码的各种压缩格式的几个示例。您需要选择您的系统可以处理的压缩格式（换句话说，确保您有一个工具来解压缩代码）。通常，在 `Linux` 系统中，您只需要 `tar`、`gzip` 或 `gunzip` 实用工具即可解压缩文件。例如，要在 `Linux` 系统上解压缩 `httpd_version.tar.gz` 文件（其中 `version` 是您下载的版本号，例如 `2.0.4`），请使用 `tar xzvf httpd_version.tar.gz` 命令。您还可以使用 `gzip -d httpd_version.tar.gz ; tar xvf httpd_version.tar` 命令，该命令将在保留每个文件相对路径完整的情况下，在一个子目录中解压缩并提取所有文件。

自解压压缩文件通常是为 `Windows` 版本的 Apache 创建的。此类文件只需运行下载的文件即可解压。对于 `Windows` 特定的安装和配置详细信息，你应该跳过本章的其余部分，并阅读第 20 章。

二进制文件通常存放在另一个目录中，每个操作系统都有自己的子目录。请注意，如果您的操作系统没有出现在二进制文件目录中，这并不意味着该操作系统不受支持。这只是意味着 Apache 开发组或贡献组中还没有人为您的系统编译二进制文件。您可能会找到 `Linux`、`FreeBSD`、`Solaris`、`NetBSD`、`OS2`、`AIX`、`Ultrix`、`HPUX` 和 `IRIX` 系统的二进制文件。

### 从源代码安装 Apache

通过编译源代码发行版中的代码来安装 Apache 是首选的安装方法，因为它允许您根据需求配置服务器。您下载的任何二进制安装都包含别人的配置，您可能无法根据需求对其进行修改。

例如，如果您下载并安装了一个支持 `CGI` 的二进制文件，即使您从不运行 `CGI` 程序，您也可能不得不接受这种 `CGI` 支持。如果 `CGI` 模块被配置为动态共享模块，那么您可以轻松禁用它；但是，如果该支持是静态构建到二进制文件中的，那么您就只能忍受 `CGI` 了。然而，如果您从源代码发行版编译一个精简且高效的 Apache 服务器，您将获得所需的组件，而没有浪费进程或磁盘空间。

![](img/e11fcbd2818a3495ac70085e5d8d1c26_49_0.png)

从官方 Apache 网站或指定的镜像站点下载源代码发行版。

### 配置 Apache 源代码

Apache 源代码发行版附带一个名为 `configure` 的脚本，允许您在编译和安装二进制文件之前配置源代码树。从 Apache 源代码发行版目录中，您可以按以下方式运行此脚本：

```sh
./configure --prefix=apache_installation_dir
```

`--prefix` 选项告诉 Apache 将二进制文件及其他必要的配置和支持文件安装在 `apache_installation_dir` 中。例如：

```sh
./configure --prefix=/usr/local/apache
```

这里，Apache 源代码将被配置为将所有二进制文件和支持文件安装在 `/usr/local/apache` 目录中。

`configure` 脚本可以使用许多选项。表 2-2 显示了所有可用的配置选项。

**表 2-2 Configure 脚本的选项**

| **选项** | **含义** |
| :--- | :--- |
| `--cache-file=file` | 在 `file` 中缓存测试结果 |
| `--help` | 打印此消息 |
| `--no-create` | 不创建输出文件 |
| `--quiet` 或 `--silent` | 不打印“正在检查……”消息 |
| `--version` | 打印创建 `configure` 的 `autoconf` 版本 |
| `--prefix=prefix` | 在 `prefix` 中安装与体系结构无关的文件 [`/usr/local/apache2`] |
| `--exec-prefix=eprefix` | 在 `eprefix` 中安装与体系结构相关的文件 [与 `prefix` 相同] |
| `--bindir=dir` | 在 `dir` 中放置用户可执行文件 [`EPREFIX/bin`] |
| `--sbindir=dir` | 在 `dir` 中放置系统管理可执行文件 [`EPREFIX/sbin`] |
| `--libexecdir=dir` | 在 `dir` 中放置程序可执行文件 [`eprefix/libexec`] |
| `--datadir=dir` | 在 `dir` 中放置只读的与体系结构无关的数据 [`eprefix/share`] |
| `--sysconfdir=dir` | 在 `dir` 中放置只读的单机数据 [`eprefix/etc`] |
| `--sharedstatedir=dir` | 在 `dir` 中放置可修改的与体系结构无关的数据 [`eprefix/com`] |
| `--localstatedir=dir` | 在 `dir` 中放置可修改的单机数据 [`eprefix/var`] |
| `--libdir=dir` | 在 `dir` 中放置目标代码库 [`eprefix/lib`] |
| `--includedir=dir` | 在 `dir` 中放置 C 头文件 [`eprefix/include`] |
| `--oldincludedir=dir` | 在 `dir` 中放置非 `GCC` 的 C 头文件 [`/usr/include`] |
| `--infodir=dir` | 在 `dir` 中放置 `Info` 文档 [`eprefix/info`] |
| `--mandir=dir` | 在 `dir` 中放置 `Man` 文档 [`eprefix/man`] |
| `--srcdir=dir` | 在 `dir` 中查找源代码 [`configure dir` 或 ...] |
| `--program-prefix=prefix` | 在已安装的程序名称前添加 `prefix` |
| `--program-suffix=suffix` | 在已安装的程序名称后添加 `suffix` |
| `--program-transform-name=program` | 对已安装的程序名称运行 `sed`（流编辑器）程序 |
| `--build=build` | 为在 `build` 上构建进行配置 |
| `--host=host` | 为主机进行配置 |
| `--target=target` | 为 `TARGET` 进行配置 [TARGET=HOST] |
| `--disable-feature` | 不包含 `feature`（与 `--enable-FEATURE=no` 相同） |
| `--enable-feature[arg]` | 包含 `feature` [arg=yes] |
| `--with-package[arg]` | 使用 `package` [arg=yes] |
| `--without-package` | 不使用 `package`（与 `--with-package=no` 相同） |
| `--x-includes=dir` | X 包含文件位于 `dir` |
| `--x-libraries=dir` | X 库文件位于 `dir` |
| `--with-optim=flag` | 已弃用（使用 `OPTIM` 环境变量） |
| `--with-port=port` | 监听端口（默认为 `80`） |
| `--enable-debug` | 开启调试和编译时警告 |
| `--enable-maintainer-mode` | 开启调试和编译时警告 |
| `--enable-layout=layout` | 启用目录布局 |
| `--enable-modules=module-list` | 启用一个或多个指定的模块 |
| `--enable-mods-shared=module-list` | 将一个或多个指定模块作为共享模块启用 |
| `--disable-access` | 禁用基于主机的访问控制 |
| `--disable-auth` | 禁用基于用户的访问控制 |
| `--enable-auth-anon` | 启用匿名用户访问 |
| `--enable-auth-dbm` | 启用基于 `DBM` 的访问数据库 |
| `--enable-auth-db` | 启用基于 `DB` 的访问数据库 |
| `--enable-auth-digest` | 启用 `RFC2617` `Digest` 认证 |
| `--enable-file-cache` | 启用文件缓存 |

## 表 2-2（续）

| 选项 | 含义 |
| :--- | :--- |
| `--enable-dav-fs` | 启用文件系统 `DAV` 提供程序 |
| `--enable-dav` | 启用 `WebDAV` 协议处理 |
| `--enable-echo` | 启用 `ECHO` 服务器 |
| `--enable-charset-lite` | 启用字符集转换 |
| `--enable-cache` | 启用动态文件缓存 |
| `--enable-disk-cache` | 启用磁盘缓存模块 |
| `--enable-ext-filter` | 启用外部过滤模块 |
| `--enable-case-filter` | 启用示例大写转换过滤器 |
| `--enable-generic-hook-export` | 启用钩子导出器示例 |
| `--enable-generic-hook-import` | 启用钩子导入器示例 |
| `--enable-optional-fn-import` | 启用可选函数导入器示例 |
| `--enable-optional-fn-export` | 启用可选函数导出器示例 |
| `--disable-include` | 禁用服务器端包含 |
| `--disable-http` | 禁用 `HTTP` 协议处理 |
| `--disable-mime` | 禁用文件扩展名到 `MIME` 的映射 |
| `--disable-log-config` | 禁用日志配置 |
| `--enable-vhost-alias` | 启用多主机模块 |
| `--disable-negotiation` | 禁用内容协商 |
| `--disable-dir` | 禁用目录请求处理 |
| `--disable-imap` | 禁用内部映像图（imagemaps） |
| `--disable-actions` | 禁用请求触发的操作 |
| `--enable-spellings` | 启用常见 `URL` 拼写错误纠正 |
| `--disable-userdir` | 禁用用户请求映射 |
| `--disable-alias` | 禁用请求转换 |
