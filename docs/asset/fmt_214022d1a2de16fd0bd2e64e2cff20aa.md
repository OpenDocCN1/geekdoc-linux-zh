
# 第16章 Web 服务器

```
#rpm -q apache
apache-1.3.9-4
```

此查询的结果表明此服务器上已加载 Apache Web 服务器 1.3.9 版本。安装过程会修改工作站启动脚本，以便在启动过程中自动启动 Apache Web 服务器。如果未安装 Apache，`rpm` 将返回以下内容：

```
#rpm -q apache
package apache is not installed
```

有关使用 `rpm` 或 GNU `rpm` 在 Red Hat Linux 工作站上安装软件包的说明，请参阅第 5 章“升级、补丁、服务包和热修复”。

## Apache 配置

Apache 配置文件位于 `/etc/httpd` 目录下。`conf` 目录包含 Web 服务器的主要配置文件。表 16.1 包含每个文件的名称和内容。

`logs` 目录包含错误日志文件（`error_logs`）和访问日志文件（`access_log`）。错误日志级别设置为 `warn`。`warn` 级别记录紧急情况、警报、严重条件、错误和警告条件的信息。访问日志文件记录对 Web 服务器的所有请求。访问日志以通用日志格式（CLF）写入。CLF 为日志文件中的每个请求写入单独的一行信息，格式如下（每个字段由空格分隔）：

```
Host ident authuser date request status bytes
```

`modules` 目录包含共享对象模块文件。Apache Web 服务器软件包包含动态共享对象（DSO）支持。DSO 在运行时加载，未编译到 Web 服务器可执行文件中，从而节省内存。在 Red Hat 中，所有标准模块都实现为 DSO。

Apache Web 服务器从 `/home/httpd/html` 目录提供页面。这在 `/etc/httpd/conf/httpd.conf` 文件中指定。`cgi-bin` 目录位于 `/home/httpd/cgi-bin`。`cgi-bin` 对于维护安全的网站非常重要。系统管理员或网站管理员可以对该目录进行更大程度的控制，以确保脚本不会对其他 Web 目录产生不利影响。

**表 16.1 Apache Web 服务器配置文件**

| File | Content |
|------|---------|
| `httpd.conf` | Contains directives controlling operation of Web server daemon (`httpd`) |
| `srm.conf` | Contains directives controlling specification of documents Web server can provide |
| `access.conf` | Contains directives controlling access to documents |

## 测试 Apache Web 服务器

最后一步是测试 Apache Web 服务器。打开你常用的浏览器，输入：

```
http://192.168.3.11
```

将上文中的 `192.168.3.11` 替换为你工作站的 IP 地址。你的浏览器应显示类似于图 16.1 的内容。

## 在 Solaris 2.6 上从源代码安装 Apache Web Server

接下来的几节将描述如何在 Solaris 2.6 工作站上从源代码安装 Apache Web Server。Apache 的 Autoconf 风格

![](img/415c89a1ede71e11e5040a0038b6916c_653_0.png)

接口（APACI）大大简化了编译和安装过程。APACI 会为操作系统生成正确的配置文件。以下 Solaris 安装步骤同样适用于任何 AIX、HPUX 或 Red Hat Linux 工作站。

### 下载软件包

安装 Apache Web Server 的源代码发行版有两个前提条件。第一个前提条件是需要一个大约有 30MB 可用磁盘空间的目录，用于下载、解包和编译源代码。第二个前提条件是 ANSI-C 编译器。输入以下命令来确定你的 Solaris 系统是否包含 ANSI-C 编译器：

```
%pkginfo SPROcc
application SPROcc      SPARCompiler C 3.0.1
```

以上输出表明已安装 SunSoft ANSI-C 编译器。如果你的系统未安装 SunSoft 编译器（错误：未找到 `SPROcc` 的信息），`www.gnu.org` 提供了适用于 Solaris、AIX 和 HPUX 的 GNU C 编译器二进制发行版的链接。可以下载该软件包，解压后使用 `pkgadd` 命令将其添加到 Solaris 系统中。GNU C 编译器软件包将安装在 `/usr/local` 目录下。

现在我们已经具备了所有必需的组件，接下来需要下载 Apache Web Server 的源代码。可以从 `http://www.apache.org` 下载最新稳定版本的 Apache Web Server。我们下载的发行版是 `apache_1.3.9.tar.gz`。`gz` 后缀表示该文件是经过压缩的。要解压缩它，请执行以下命令：

```
#gunzip apache_1.3.9.tar.gz
```

解压后得到文件 `apache_1.3.9.tar`。现在我们必须使用以下命令处理这个文件：

```
#tar -xvf apache_1.3.9.tar
```

该命令的结果是生成一个名为 `apache_1.3.9` 的新目录。现在我们可以开始配置、编译和安装 Apache Web Server 了。

### 安装 Apache Web Server

首先，使用 `cd` 命令进入 Apache 服务器发行版的顶层目录（`apache_1.3.9`）。使用 APACI 配置服务器、编译和安装只需要三条命令。我们将构建一个支持 DSO 并添加一些默认服务器中未包含的模块的服务器。

第一个命令 `configure` 在 APACI 下执行，是最重要的命令。`configure` 命令接受大约 40 个选项。要获取 `configure` 支持的所有选项列表，请执行以下命令：

```
#configure --help
```

以下列表仅包含 `configure --help` 命令中的“Configuration options:”部分：

```
Configuration options:

--enable-rule=NAME        enable a particular Rule named 'NAME'

--disable-rule=NAME       disable a particular Rule named 'NAME'

                          [DEV_RANDOM=default EXPAT=default    IRIXN32=yes

                           [IRIXN32=no       PARANOID=no       SHARED_CHAIN=de]

                           [SHARED_CORE=default SOCKS4=no      SOCKS5=no     ]

                           [WANTSHAREDEXEC=default

--add-module=FILE         on-the-fly copy & activate a 3rd-party Module

--activate-module=FILE    on-the-fly activate existing 3rd-party Module

--permute-module=NAME     on-the-fly permute module 'NAME' with module 'N2'

--enable-module=NAME      enable a particular Module named 'NAME'

--disable-module=NAME     disable a particular Module named 'NAME'

                          [access=yes       actions=yes       alias=yes

                           asis=yes         auth_anon=no      auth_dbm=no

                           auth_db=no       auth_digest=no    auth=yes

                           autoindex=yes    cern_meta=no      cgi=yes

                           digest=no        dir=yes           env=yes
```
