

## 测试 Apache Web 服务器

最后一步是测试 Apache Web 服务器。打开你常用的浏览器，输入：

```
http://192.168.3.11
```

将上文中的 192.168.3.11 替换为你工作站的 IP 地址。你的浏览器应显示类似于图 16.1 的内容。

## 在 Solaris 2.6 上从源代码安装 Apache Web Server

接下来的几节将描述如何在 Solaris 2.6 工作站上从源代码安装 Apache Web Server。Apache 的 Autoconf 风格

![](img/415c89a1ede71e11e5040a0038b6916c_653_0.png)

接口（APACI）大大简化了编译和安装过程。APACI 会为操作系统生成正确的配置文件。以下 Solaris 安装步骤同样适用于任何 AIX、HPUX 或 Red Hat Linux 工作站。

## 下载软件包

安装 Apache Web Server 的源代码发行版有两个前提条件。第一个前提条件是需要一个大约有 30MB 可用磁盘空间的目录，用于下载、解包和编译源代码。第二个前提条件是 ANSI-C 编译器。输入以下命令来确定你的 Solaris 系统是否包含 ANSI-C 编译器：

```
%pkginfo SPROcc
application SPROcc      SPARCompiler C 3.0.1
```

以上输出表明已安装 SunSoft ANSI-C 编译器。如果你的系统未安装 SunSoft 编译器（错误：未找到 SPROcc 的信息），www.gnu.org 提供了适用于 Solaris、AIX 和 HPUX 的 GNU C 编译器二进制发行版的链接。可以下载该软件包，解压后使用 pkgadd 命令将其添加到 Solaris 系统中。GNU C 编译器软件包将安装在 /usr/local 目录下。

现在我们已经具备了所有必需的组件，接下来需要下载 Apache Web Server 的源代码。可以从 http://www.apache.org 下载最新稳定版本的 Apache Web Server。我们下载的发行版是 apache_1.3.9.tar.gz。gz 后缀表示该文件是经过压缩的。要解压缩它，请执行以下命令：

```
#gunzip apache_1.3.9.tar.gz
```

解压后得到文件 apache_1.3.9.tar。现在我们必须使用以下命令处理这个文件：

```
#tar -xvf apache_1.3.9.tar
```

该命令的结果是生成一个名为 apache_1.3.9 的新目录。现在我们可以开始配置、编译和安装 Apache Web Server 了。

## 安装 Apache Web Server

首先，使用 cd 命令进入 Apache 服务器发行版的顶层目录（apache_1.3.9）。使用 APACI 配置服务器、编译和安装只需要三条命令。我们将构建一个支持 DSO 并添加一些默认服务器中未包含的模块的服务器。

## 第16章 Web 服务器

第一个命令 configure 在 APACI 下执行，是最重要的命令。configure 命令接受大约 40 个选项。要获取 configure 支持的所有选项列表，请执行以下命令：

```
#configure --help
```

以下列表仅包含 configure --help 命令中的“Configuration options:”部分：

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
                           example=no       expires=no        headers=no
                           imap=yes         include=yes       info=no
                           log_agent=no     log_config=yes    log_referer=no
                           mime_magic=no    mime=yes          mmap_static=no
                           negotiation=yes  proxy=no          rewrite=no
                           setenvif=yes     so=no             spelling=no
                           status=yes       unique_id=no      userdir=yes
                           usertrack=no     vhost_alias=no   ]
--enable-shared=NAME      enable a build of Module named 'NAME' as a DSO
--disable-shared=NAME     disable build of Module named 'NAME' as a DSO
--with-perl=FILE          path to the optional Perl interpreter
--without-support         disable the build and installation of support tools
--without-confadjust      disable the user/situation adjustments in config
--without-execstrip       disable the stripping of executables on installation
```

在 --disable-module=NAME 标题下方，列出了 Apache Web Server 发行版中包含的标准模块。赋值为 yes 的模块（access=yes、mime=yes...）默认包含。赋值为 no 的模块（mime_magic=no、so=no...）默认不包含。我们将为这个 Web 服务器添加 mime_magic 和 rewrite 模块。每个添加的模块都需要在配置命令行上单独使用一个 --enable-module（如 --enable-module=mime_magic）选项。我们还决定将 rewrite

