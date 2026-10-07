

## 第 8 章 管理软件和系统资源

此示例还使用了 `v` 和 `h` 选项，它们提供了更详尽的哈希标记输出，以显示安装进度。你也可以在安装软件包后使用 `rpm` 查询其数据库以验证安装情况。

使用 `-V` 选项结合软件包名称来验证安装系统。例如，要验证 `pine` 软件包，可以使用如下 `rpm` 命令：

```bash
# rpm -V pine
```

> 注意
> 请注意，如果你的软件安装一切无误，在运行命令后，系统对 `rpm -V` 不显示任何响应；仅显示存在的问题。

从下面的程序输出可以看出，通过在 `-V` 选项中添加额外的验证选项（例如再添加两个 `vs`），你可以获取软件包的其他信息。要获取有关已安装软件包的更多信息，请使用一种或多种形式的 rpm 查询选项。例如，要显示已安装软件包的简要信息，请使用 `-q` 选项结合 `i` 和已安装的包名，如下（注意你的版本将与此处显示的不同）：

```bash
# rpm -qi pine
Name : pine Relocations: (not relocatable)
Version : 4.44 Vendor: Red Hat, Inc.
Release : 7 Build Date: Wed 17 Apr 2002 04:07:44 PM EDT
Install date: Fri 10 May 2002 11:35:27 AM EDT
Build Host: stripples.devel.redhat.com
Group : Applications/Internet Source rpm: pine-4.44-7.src.rpm
Size : 6725592 License: Freely Distributable
Packager : Red Hat, Inc. http://bugzilla.redhat.com/bugzilla/
URL : http://www.washington.com/pine/
Summary : A common used, MIME compliant mail and readers user agent
Description :
Pine 是一个非常流行、易用且功能齐全电子邮件编辑器，名为 Pine。Pine 支持 MIME 扩展，并包含一个名为 editorpine 的简单文本编辑器，还可以用于阅读新闻。Pine 还支持 IMAP、邮件和 MH 风格的文件夹。
```

 这种形式的 rpm 查询提供了有关软件软件包的一些信息。（你也可以通过提供路径来在安装前查询软件包。）

如果此软件包不是最新版本，你可以通过下载新版本并使用如下 `rpm` 的 `-U` 或 `upgrade` 选项来轻松地升级软件包：

## 使用 RPM 进行软件管理

```bash
# rpm -Uvh pine-4.44-7.i386.rpm
Preparing...
#################################### [100%]
########################################################### [100%]
1:pine
```

注意，没有必要移除当前安装的软件软件包——升级选项会保留旧的配置文件，然后它会自动安装新软件。

你还可以使用 `rpm` 命令的 `-F` 或 `"freshen"`（刷新）选项来升级你的系统软件，它将从远程 FTP 或 HTTP 服务器获取指定的软件包。例如，要升级 `fetchmail-conf` 软件包，可以使用如下 `rpm` 命令（在此示例中 FTP URL 已经缩短）：

```bash
# rpm -Fv http://ftp.tux.org/linux/redhat/updates/7.3/en/i386/fetchmailconf-5.9.0-11.i386.rpm
```

正在检索 http://ftp.tux.org/linux/redhat/updates/7.3/en/i386/fetchmailconf-5.9.0-11.i386.rpm

正在准备安装软件包...
fetchmailconf-5.9.0-11

如果你有宽带访问，可以快速就地升级系统而无需将其切换到运行级别 1（参见第 7 章“管理系统服务”）。这是 Xim 版本的 GNOME 的主要功能，访问 http://www.xim.com/。`rpm` 命令将检索指定的软件包，然后升级你系统上的软件。你使用 `-e` 选项结合软件包名称来通过 `rpm` 从系统中移除或删除软件。例如，要移除 `pine` 电子邮件软件包，可以使用如下 `rpm` 命令：

```bash
# rpm -e pine
```

注意，如果操作成功，系统将不会显示任何消息。你可以通过将 `rpm` 的输出通过给 `grep` 来快速搜索已安装的软件包（参见第 7 章“管理系统服务”）：

```bash
# rpm -qa | grep pine
```

### 使用 RPM 组织

| 大类 | 子类 |
| :--- | :--- |
| 应用 | 桌面、工程、游戏、办公、生产力、音频、视频 |
| 配置 | 管理、配置 |
| 开发 | 开发、内核、科学 |
| 硬件 | 桌面、硬件、支持 |
| 互联网 | 网络、邮件、办公、出版、Web |
| 邮件 | 邮件、新闻、Web |
| 服务器 | 管理、数据库、FTP、邮件、SQL、Web |
| 系统 | 管理、打印、系统 |

> 注意
> 请注意，如果你的软件安装一切无误，在运行命令后，系统对 `rpm -V` 不显示任何响应；仅显示存在的问题。

从下面的程序输出可以看出，通过在 `-V` 选项中添加额外的验证选项（例如再添加两个 `vs`），你可以获取软件包的其他信息。要获取有关已安装软件包的更多信息，请使用一种或多种形式的 rpm 查询选项。例如，要显示已安装软件包的简要信息，请使用 `-q` 选项结合 `i` 和已安装的包名，如下（注意你的版本将与此处显示的不同）：

这种形式的 rpm 查询提供了有关软件软件包的一些信息。（你也可以通过提供路径来在安装前查询软件包。）

如果此软件包不是最新版本，你可以通过下载新版本并使用如下 `rpm` 的 `-U` 或 `upgrade` 选项来轻松地升级软件包：

## Linux 和 Unix 软件管理

Red Hat RPM 系统被许多 Linux 发行版使用。SuSE 使用不同的管理系统（使用 `y2`），而 Mandrake 使用 rpm。其他 Linux 发行版如 Debian 使用不同的管理模型（apt-get）。FreeBSD、NetBSD 和 OpenBSD 也有基于 `pkg_add` 和 `pkg_delete` 的不同管理系统。然而，http://www.openpackages.org/ 正在统一 BSD 等系统的软件交付和管理。新的包设计将涉及新格式，旨在让构建、安装和维护变得更加简单。

## 处理源码 RPM 文件

有时你可能需要自己的需要修改源码包，例如添加文档、更改默认设置或对源代码本身进行补丁。Red Hat 以源码 RPM 文件的形式分发源码。你可以从下载的 CD 镜像的第 4 和第 5 磁盘中访问源码，或从 Red Hat ftp 站点获取它们。

