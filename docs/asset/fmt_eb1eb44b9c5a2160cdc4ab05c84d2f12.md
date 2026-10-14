
```
DAZ/: # rpm -qi wget
Relocations: (not relocatable)
Name : wget
Version : 1.11.4
Vendor: SUSE LINUX Products GmbH
nuremberg, Germany
Release : 1.9
Build Date: Fri 23 Jan 2009 09:57:01 PM MST
Install Date: Fri 06 Feb 2009 02:36 AM MST Build Host: albeniz
Group : Productivity/Networking/Web/Utilities Source RPM: wget-11.4.1-1.9.src.rpm
Size : 1530350 License: GPL, v3 or later
Signature : RSA/8, Fri 23 Jan 2009 09:57:12 PM MST, Key ID ea3a5c360307e3d5d4
URL : http://www.gnu.org/software/wget/
Summary : A Tool for acquiring FTP and HTTP Servers
Description :
Wget 使你能够从服务器检索 WWW 文档或 FTP 文件。
这可以通过脚本文件或通过命令行完成。
```

作者：

-------

Hrvoje Niksic <hniksic@srcce.hr>

发行: SUSE-LE-11:0

- `-f` 选项仅在指定了带有完整路径的完整时才有效。你可以输入多个文件名，如下所示：

```
DAZ/: # rpm -qf /bin/rpm /usr/bin/wget
rpm-4.4.2.23.58
wget-1.11.4.1-9
```

这会同时返回 `/bin/rpm` 和 `/usr/bin/wget` 的信息。

借助 RPM 数据库的帮助，你可以使用 `-V` 或 `--verify` 选项进行验证检查。如果软件包中的任何文件自安装以来发生了更改，它们将被显示出来。

RPM 使用以下字符来提供有关更改的提示：

# 表 4-2 RPM --verify 输出

| 字符 | 说明 |
|---|---|
| 5 | MD5 校验和 |
| S | 文件大小 |
| L | 符号链接 |
| T | 修改时间 |
| D | 主、次设备号 |
| U | 所有者 |
| G | 组 |
| M | 模式（权限和文件类型） |

## 使用 Yast CLI 命令作为 RPM 的前端

YaST 的主要功能之一是软件安装。如果你知道软件包的名称，`-i` 选项（安装）非常有用。例如：

```
yast -i wireshark
```

此示例安装了 Wireshark 软件包以及 Wireshark 需要的安装介质的任何软件包。使用 `yast -i` 的优势是会自动解析任何依赖关系。

你也可以使用 `-i` 选项安装任何 RPM 软件包，指定 RPM 文件名，而不仅仅是软件包的名称。例如：

```
yast -i apache2-2.2.10-18.1586.rpm
```

然而，在这种情况下依赖关系不会被解析。

## 使用 yum 命令作为 RPM 的前端

`yum` 或 Yellowdog Updater Modified 用于兼容的 Linux 系统，`yum` 进化（从 YUP 演变而来）是为了更新和管理 RHL 系统。从那时起，它已用于其他 Linux 发行版，例如 Fedora、RHEL 和 CentOS。

在目标的此部分，你将学习如何使用 `yum` 执行以下操作：

- 使用 `yum` 命令
- 管理 `yum` 配置
- 使用 `yumdownloader`

### 使用 yum 命令

`yum` 是 RPM 的命令行前端。它在安装软件包时会处理依赖关系等事务：基本语法如下：

```
yum option command package name
```

`yum` 定义了软件包仓库的布局。基于此标准的仓库也可以与 YaST 使用。

`yum` 有一个命令行界面，并有一个插件接口，`yum` 扩展可以用于执行软件包的查询、管理清理以及执行仓库同步。

常用的 `yum` 命令包括：

**表 4-3** `yum` 命令

| 命令 | 说明 |
|---|---|
| list all | 列出所有可用的软件包。 |
| list installed | 列出已安装的软件包。 |
| list updates | 列出有更新的软件包。 |
| list duplicate | 列出重复的软件包。 |
| install | 安装指定的软件包。 |
| update | 更新指定的软件包。 |
| remove | 删除指定的软件包。 |
| search | 搜索软件包。 |
| info | 显示软件包的详细信息。 |
| provides | 显示软件包提供的功能。 |
| requires | 列出软件包所需的权限。 |
| verify | 验证软件包的完整性。 |
| clean | 清理缓存的元数据和软件包。 |
| yumdownloader | 下载软件包。 |

### 管理 yum 配置

`yum` 配置文件位于 `/etc/yum.conf` 和 `/etc/yum.d/`。

- `yum.conf` 是 `yum` 的配置文件。你可以通过取消注释或在文件末尾添加行来填充它，以包含仓库项。

# 管理软件

```
[suselinux-extras]
name=SUSE Linux Extras $releaselever $basesearch - Extra Packages
baseurl=http://mirrors.backupstore.org/pub/linux/suse/sll/base/
$releaselever/$basesearch/os
ailmethod=priority
```

```
[core]
name=SUSE Linux Core $releaselever $basesearch-'core'
baseurl=http://user.novell.com/linux/suse/core/$releaselever/
$basesearch/core
```

```
[SUSE Linux Enterprise 11 stable]
name=SUSE Linux Core $releaselever Stable
baseurl=http://suselinux.novell.com/suse/linux/$releaselever/$basesearch/yum/
stable
http://suselinuxde.linux.de/suse/linux/$releaselever/$basesearch/yum/
stable
http://mirrors.backupstore.org/pub/suse/linux/enterprise1/
$releaselever/$basesearch/yum/stable
```
