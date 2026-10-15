
- `/usr/src/init/initC`—学习 Linux 如何启动的最佳地方。真的是非常引人入胜的读物。从源码获取它！

- `http://sunsite.de/linux-newbie`—《Linux 新手管理员指南》主页，对 Linux 系统管理的入门介绍。

- GRUB 手册——尚未完成的手册可以在 `http://www.gnu.org/manual/grub-0.92/html/grub.html` 找到。在你的 Red Hat 系统上，`info grub` 提供了大量信息，示例 `grub.conf` 文件位于 `/usr/doc/grub`。

- “LILO 用户指南”—Werner Almesberger 关于 Linux 加载器 `LILO` 的权威著作，以及它如何在 Intel PC 上工作。查看 `/usr/share/doc/lilo/` 目录下的 `User_Guide.ps`，可以使用相应的客户端查看。

- “使用 Red Hat 管理初始化脚本”—Jimmy Ball，《Linux Journal》，2001 年，第 128-132 页。

- “光荣的 GRUB”—Hoyt Dutt，《Linux Format》，2001 年 8 月，第 58-61 页。关于 GRUB 的教程。

# 第 8 章 管理软件和系统资源

## 本章内容介绍

### 管理软件和系统资源

* 使用 RPM 管理软件
* 监控工具
* 参考文献

本章介绍了在 Red Hat Linux 系统上管理已安装资源的概念、程序和软件。管理计算机的系统资源（包括软件、存储和内存）具有许多重要。良好的资源管理促进并支持高效、生产的会话以及满意的用户。管理这些资源涉及安装、删除、升级或重新构建软件包——每个任务都对系统安全至关重要。

作为 Red Hat 系统管理员，你还应该知道如何通过管理内存和存储来最大化利用系统资源。正确管理系统资源可以确保你有空间安装新软件，并且可以根据不断变化和新项目扩展系统。换句话说，系统资源管理对于为用户提供最好的计算体验至关重要。Red Hat Linux 提供了多种系统资源管理工具。接下来的章节将介绍 RPM 包管理器（RPM），以及命令行和图形软件管理工具。你还将学习监控和管理内存以及磁盘存储。

## 第 8 章 管理软件和系统资源

`Picasso` 于 1996 年发布。从那时起，`rpm` 命令一直是 Red Hat 独特软件管理系统的核心特征，该系统基于“原始源”（pristine sources）的概念，或者说能够使用单一的程序源代码初始存档不仅为不同的系统构建软件包，还能进行版本跟踪。随着 2002 年 Red Hat 8.0 `Psyche` 的发布，Red Hat 为其久老的 `rpm` 应用程序提供了一个略微更新的图形化管理界面。

在改进早期软件管理脚本的包管理之外，RPM 4.1 版本引入了软件功能，以简化从单组源代码文件为不同平台构建软件的任务。文件可以被修改并保留开发者的初始代码之外，并且可以同时从头构建多个软件包——同时，RPM 还会验证安装依赖关系。其他功能（如校验和和 GNU 隐私保护 `GPG` 签名）使得二进制软件包能够安全地分发，而无必担心病毒感染或包含木马代码。

`rpm` 命令使用 RPM 系统来删除（擦除）、升级、验证和构建名为 `.rpm` 文件的软件存档。这些存档（或软件包）包含包标识（签名）、校验和（通过数学得出的验证值）以及软件存档（无论是源代码还是二进制形式）。`.rpm` 软件包还包含一些额外信息，如名称、版本和基本描述，并可以包含用于安装、擦除或升级的安装前后脚本。

安装在你的计算机上的 RPM 数据库记录了已安装软件包的版本。RPM 使用你系统的 `/var/lib/rpm` 目录来存储包含系统中安装软件信息的文件（实际上是数据库）。你可以使用命令查看这些文件（显示的文件大小可能取决于你拥有的软件数量）：

```
$ ls -l /var/lib/rpm
total 51188
-rw-r--r-- 1 rpm rpm 1046520 May 23 14:05 Basenames
-rw-r--r-- 1 rpm rpm 12288 May 23 14:03 Conflictname
-rw-r--r-- 1 rpm rpm 1138688 May 23 14:05 Dirnames
-rw-r--r-- 1 rpm rpm 1054310 May 23 14:05 Filemd5s
-rw-r--r-- 1 rpm rpm 24576 May 23 14:05 Installtid
-rw-r--r-- 1 rpm rpm 45056 May 23 14:05 Name
-rw-r--r-- 1 rpm rpm 3358140 May 23 14:05 Packages
-rw-r--r-- 1 rpm rpm 335872 May 23 14:05 Providename
-rw-r--r-- 1 rpm rpm 86016 May 23 14:05 Provisionversion
-rw-r--r-- 1 rpm rpm 405504 May 23 14:05 Requireename
-rw-r--r-- 1 rpm rpm 192512 May 23 14:05 Requireversion
-rw-r--r-- 1 rpm rpm 86016 May 14 09:55 Shaheader
-rw-r--r-- 1 rpm rpm 86016 May 23 14:05 Sigmd5
-rw-r--r-- 1 rpm rpm 12288 May 23 14:05 Trigganname
```

已安装软件的主要数据库包含在名为 `Packages` 的文件中。如前面的示例所示，如果你完整安装了 Red Hat Linux（超过 3GB 的软件），该数据库的大小可能会增长到 33MB（甚至更大）。在安装 Red Hat Linux 后，`rpm` 及相关命令将使用此目录进行软件管理操作。

### 命令行和图形化 RPM 客户端

- 安装新软件
- 擦除或移除过时或不需要的软件包
- 升级已安装的软件软件包
- 查询以获取有关软件包的信息
- 验证软件包的安装或完整性

作为 Red Hat Linux 系统管理员员，你将使用 `rpm` 命令或 Red Hat 图形化客户端来执行五项基本任务之一。这些操作必须由 root 操作员执行，包括以下内容：

`rpm` 命令有超过 60 个命令行选项，但其管理功能可以根据上述五种操作类型进行分组。图形化客户端为这些操作提供了易于使用的界面。作为系统管理员，你可以在使用图形化界面和使用 `rpm` 的各种命令行选项之间进行选择。`rpm` 命令的标准格式为：

```
# rpm option packagename
```

基本选项如下：

- `-i`—安装选定的软件包或软件包。
- `-e`—擦除（移除）选定的软件包或软件包。
- `-U`—移除当前安装的软件包，然后用所选软件包或软件包的内容安装软件，保留现有的配置文件。
- `-q`—查询系统或选定的软件包或软件包。
- `-V`—验证已安装或选定的软件包或软件包。

> 注：由于原文中存在大量 OCR 重复，译文已根据逻辑进行了去重处理

此示例还使用了 `v` 和 `h` 选项，这些选项提供了更详细的输出并显示哈希标记以指示安装进度。

你也可以在安装包后使用 `rpm` 查询其数据库以验证安装情况。使用 `-V` 选项配合软件包名称来验证系统上的安装。例如，要验证 `pine` 邮件包，可以使用如下的 `rpm` 命令：

```bash
# rpm -V pine
```

> 注意
如果你的软件安装一切正常，在运行 `rpm -V` 命令后，系统将不会显示任何内容；只有显示问题时。

从下面的程序输出可以看出，你可以通过向 `-V` 选项添加额外的验证选项（例如多加两个 `v`）来获取软件包的附加信息。要获取有关已安装软件包的信息，可以使用一个或多个 `rpm` 查询选项。例如，要显示已安装软件包的信息，使用 `-q` 选项配合 `i` 选项和已安装包名称，如下（你的版本将与所示不同）：

```bash
# rpm -q i pine
Name : pine Relocations: (not relocable)
Version : 4.44 Vendor: Red Hat, Inc.
Release : 7 Build Date: Wed 17 Apr 2002 04:07:44 PM EDT
Install date: Fri 10 May 2002 11:35:27 AM EDT
Build Host: stripples.dev.redhat.com
Group : Applications/Internet Source RPM: pine-4.44-7.src.rpm
Size : 6725592 License: Free Distributable
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
URL : http://www.washington.edu/pine/
Summary : A commonly used, MIME compliant mail and news readers.
```

描述
`Pine` 是一个非常流行、易用且功能齐全的用户代理，包含一个简单的文本编辑器 `pico`。`Pine` 支持 MIME 扩展，还可以用于读取新闻。`Pine` 还支持 IMAP、邮件和 MH 风格的文件夹。

这种形式的 `rpm` 查询提供了关于软件软件包的一些信息。（你也可以通过提供其路径来在安装前对其进行查询。）

如果此包不是最新版本，你可以通过加载新版本并然后使用 `rpm` 的 `-U` 或 `upgrade` 选项来快速升级该包：

```bash
# rpm -Uvh pine-4.44-7.i1386.rpm
Preparing...                                     ########################### [100%]
:pine                                                              ########################### [100%]
```

请注意，不需要移除当前已安装的软件包——该选项会移除旧版本的软件（保留旧配置文件），然后自动安装新软件。

你可以使用 `rpm` 命令的 `-F` 或 "freshen" 选项来升级系统软件，它将从远程 FTP 或 HTTP 服务器获取指定的软件包。例如，要升级 `fetchmail-conf` 包，可以使用如下的 `rpm` 命令（在此示例中 FTP URL 已缩短）：

```bash
# rpm -Fv ftp://ftp.tux.org/linux/redhat/updates/7.3/en/os/i386/fetchmailconf-5.9.0-11.rpm
```

正在检索 `ftp://ftp.tux.org/linux/redhat/updates/7.3/en/os/i386/fetchmailconf-5.9.0-11.rpm`
正在准备安装包...
`fetchmailconf-5.9.0-11.1`

如果你有宽带访问，可以相当快速地直接升级系统，而无需运行到运行级别 1（第 7 章，“管理系统服务”）。这是 Xian 的 GNOME 系统（`http://www.ximian.com/`）的一个主要特性。`rpm` 命令将检索指定的软件包，然后升级你系统上的软件。

使用 `-e` 选项配合软件包名称，用 `rpm` 从你的系统中移除或擦除软件。例如，要移除 `pine` 邮件包，可以使用如下的 `rpm` 命令：

```bash
# rpm -e pine
```

注意，如果操作成功，系统上不会显示任何消息。你可以通过将 `rpm -qa` 的输出通过管道给 `grep` 和 `sort` 来快速搜索已安装软件包的名称（第 5 章，“Linux 入门”），获取有关 `grep` 和 `sort` 的更多信息；以下是进行该搜索的方法：

```bash
$ rpm -qa | grep mail | sort
fetchmail-5.9.0-5
mail-3.0.0-4
mailcap-2.1.9-2
mailman-2.0.9-1
mailx-8.1.1-22
ametail-2.7-28
procmail-3.22-5
redhat-switchmail-0.5.1-1
redhat-switchmail-gnome-0.5.1-1
sendmail-8.11.65-15
sendmail-cf-8.11.65-15
sendmail-devel-8.11.65-15
sendmail-doc-8.11.65-15
```

此示例返回了所有名称包含 "mail" 单词的软件包排序列表。

> 注意
`rpm` 命令的另一个基本功能是 `--rebuilddb`。

#### 使用 RPM 进行软件包组织

Red Hat 上的软件包被组织成组。你可以使用以下命令查看可用组：

```bash
$ rpm -qa --qformat '%{GROUP}\n' | sort |
```

输出显示了组列表。每个组包含若干个子类别，如下所示：

| 顶级分类 | 子类别 |
| :--- | :--- |
| 桌面 | 应用、工程、图形、互联网、办公/效率、音频、视频 |
| 服务器 | 配置、DNS、FTP、邮件、新闻、SQL、Web |
| 开发 | 连接、内核、软件、工具 |
| 系统 | 管理、打印 |

要查看特定组内的软件包，使用 `-qgroup` 选项配合组名：

```bash
# rpm -q --group mail
```

这将列出属于 "mail" 组的所有软件包。你也可以使用 `--what` 选项查看特定软件包属于哪个组：

```bash
# rpm -q --what pine
```

#### 从 RPM 中提取单个文件

有时，从 RPM 软件包中提取单个文件是有用的。你可以使用 `mc`（Midnight Commander）的命令行来实现这一点，如图 8.1 所示。Midnight Commander 是著名的 DOS 文件管理工具 Norton Commander 的 UNIX 克隆版本。使用 `mc`，只需高亮 RPM 文件并按回车；RPM 文件的内容就会显示出来。在列表中，你可以浏览 RPM 文件的结构并使用 `mc` 从从中复制文件。

#### 处理源 RPM 文件

你可能希望为了自己的用途修改源包，例如添加文档、更改默认设置或对源代码本身进行补丁。Red Hat 以 RPM 文件的形式提供源码。你可以从下载的 CD 镜像的第 4 和第 5 磁盘中访问源码，或者从 Red Hat ftp 站点获取它们。

![](img/e862c5b60f9f55ef43a34453c49f252f_271_0.png)

图 8.1 经典的双面板目录视图和下拉菜单显示了 Midnight Commander 对操作系统的灵感，但它是一个功能完备的命令行文件管理器。

> 提示 RPM 文件的一个重要部分是 `.spec` 文件。它告诉 RPM 如何处理特定的源文件。

作为一个示例，我们将使用从 `http://elektron.tudel.nl/-rbos3/freetype2` 找到的信息来修改 Red Hat `freetype` 库，以启用字节码解释器。由于许可考虑，它默认是禁用的。启用它将提高 TrueType 字体体的渲染效果。我们使用 Red Hat 7.3 的文件作为示例，但 8.0 的源代码同样适用。

首先通过 `rpm -i` 安装 RPM 软件包开始工作。它将被放置在 `/usr/src/redhat/SRPMS`。在本示例中，获取 `freetype-2.0.9-2.src.rpm` 并使用 `rpm -i` 安装它。源代码存放在 `/usr/src/redhat/SOURCES/`。

将源文件（一个压缩 tar 包）拷贝到 `/tmp`，然后 `cd`（切换目录）以解压并修改它：

```bash
# cp freetype-2.0.9.tar.bz2 /tmp
# cd /tmp
```

由于它是一个 `.bz2` (BZip 压缩) tar 文件，使用以下命令解压：

```bash
# tar xjvf freetype-2.0.9.tar.bz2
```

并进入新目录：

```bash
# cd freetype-2.0.9
```

使用你喜欢的文本编辑器编辑 `include/freetype/config/ftoption.h` 文件，并找到这一行：

```bash
#undef TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

将其更改为：

```bash
#define TT_CONFIG_OPTION_BYTECODE_INTERPRETER
```

保存并退出文本编辑器。

接下来，重新创建存档：

```bash
# cd /tmp
# tar cfj freetype-2.0.9.tar.bz2 ./freetype-2.0.9/
```

将其放回源目录：

```bash
# mv freetype-2.0.9.tar.bz2 /usr/src/SPECS
```

现在编辑 `/usr/src/redhat/SPECS` 中的 `.spec` 文件，更改以 Release 开头的行以增加找到找到的数字。（我们通过这种方式更改了版本号，因此它就不会与我们要替换的应用程序版本冲突。）如果你愿意，可以对 `%description` 行进行任何更改以描述你的修改，然后保存文件。

使用以下命令构建二进制 RPM：

```bash
# rpmbuild -bb freetype.spec
```
