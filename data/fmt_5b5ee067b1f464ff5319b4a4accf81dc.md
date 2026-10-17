
## 4.1.3 YUM 安装软件包

### 1. YUM 概述

在 Linux 系统中安装软件包最大的难点就是软件包之间的依赖关系。当安装软件时，`rpm` 会根据数据库查询其他软件是否满足，如果满足则安装，否则安装。YUM 是 Yellow Updater 的简化版，经过优化的。YUM 可以配置多个资源库（Repository）和简单的配置文件（`/etc/yum.conf`），能够自动解决 RPM 遇到的依赖性问题，保持与 RPM 数据库一致性。通过详细的日志查看升级和安装软件包等信息。

### 2. YUM 结构

YUM 由以下部分构成：

- `yum` 命令：通过 `yum` 命令才能使用 `yum` 提供的功能。
- `yum` 仓库（repository）：它是软件包的“更新”。它是存放 RPM 的目录，仓库中包含 `repodata` 的目录。该目录存放 RPM 的各种信息，包括描述、文件、依赖性。客户端通过 `ftp://` 或 `file://` 访问本地或远程仓库，完成查询、安装、更新操作。
- `yum` 缓存：`yum` 客户端运行时从软件包下载仓库文件和 RPM 软件包，并存储在 `/var/cache/yum`
- `yum` 插件：用于进行 `yum` 扩展。

### 3. 使用 yum 命令

语法：`yum [选项] [命令][软件或程序名]`
通过 `yum` 命令可以快速安装软件及其依赖关系，选项及功能描述如表 4-1 所示。

表 4-1 yum 命令选项功能描述

| 选项 | 功能描述 |
| --- | --- |
| `check-update` | 显示所有可更新的软件清单 |
| `clean` | 删除缓存中 RPM 头文件和软件包，与 `clean all` 相同 |
| `clean packages` | 删除缓存中的软件包 |
| `info` | 显示可用的软件包信息 |
| `info 软件包名` | 显示指定软件包信息 |
| `install 软件包名` | 安装指定软件包 |
| `list` | 显示可用的软件包列表 |
| `list installed` | 显示已安装的软件包列表 |
| `list updates` | 显示可升级的软件包列表 |
| `provides 软件包名` | 显示软件包包含的内容 |
| `remove 软件包名` | 删除指定的软件包，确认指定软件包的依赖关系 |
| `search 关键字` | 利用关键字搜索软件包，搜索 RPM 文件名、Package (包)、Description 的类型 |
| `update` | 升级所有可升级的软件包 |
| `update 软件包名` | 升级指定的软件包 |

## 4. yum 配置文件

yum 的配置文件分为两部分：`main` 和 `repository`。`main` 部分定义了全局选项，整个 `yum` 的配置文件应该有一个如图 4-3 所示，位于 `/etc/yum.conf`。`repository` 部分定义了每个源的具体配置，可以有多个，位于 `/etc/yum.repo.d` 目录下的文件中。

### 1) 主配置文件 /etc/yum.conf

```
root@localhost: 文件(F) 插入(E) 写入(W) 退出(Q) 

main:

cachedir=/var/cache/yum/

debuglevel=3

logfile=/var/log/yum.log

basearch=0

gpgcheck=1

# metadata_cache_timeout is the default, if you make this then yum won't see the metadata

# in the repo and you will lose the benefit of not having to

# download it every time you run a command.

# It is important to get correct metadata, for distributions like

# which don't keep old packages.

# update metadata once a month

metadata_expire=0

# REPOS HERE OR separate named file,

/etc/yum.repo.d/
```

### 2) 配置文件 /etc/yum.repo

```
[main]

name=base

baseurl=http://mirror.centos.org/centos/$releasebase/$basearch/

enabled=1

gpgcheck=1

installonly=5
```

## 4.1. 源码安装

源码源是可选的软件包，需要用户自己编译成执行文件。优点在于定制硬件、操作系统及环境。在实际使用中，许多源码包都采用 tar 包，一般源码安装分为以下步骤：

1. 解压：源码包常见的是 `gzip` 和 `bzip2`。
2. 配置：检查环境并生成 `Makefile`。
3. 编译：生成可执行文件。
4. 安装：将文件拷贝到系统目录。

## 4.2 项目实施

### 4.2.1 使用 RPM 安装 OpenOffice 软件

ApacheOffice 是一款先进的开源办公软件，包含本文档、电子表格、演示文稿、绘图、数据库。它将所有的数据以国际开放格式存储起来，并能够写入其他通用软件包。ApacheOffice 可以被完全自由下载和使用无需任何许可费用。该软件可以在 `http://www.openoffice.org/` 中下载。

将下载好的 Apache 放入 `~/home` 下，具体的步骤如下：
(1) 解压 OpenOffice，解压之后出现 `/zh-CN/` 如图 4-6 所示

## 学习环境一 Linux 基本应用

```bash
licenses readmes RPMS

[@localhost zh-CN]$# cd RPMS/

[@localhost RPMS]$# ls
```

```
root@localhost/home/zh-CN/RPMS
```

```
文件(F) 编辑(E) 查找(V) 搜索(S) 帮助(H)

root@localhost RPMS]$# ls

desktop-integration

openoffice-4.1.5.9789.x86_64.rpm

openoffice-base-4.1.5.9789.x86_64.rpm

openoffice-brand-base-4.1.5.9789.x86_64.rpm

openoffice-brand-calc-4.1.5.9789.x86_64.rpm

openoffice-brand-draw-4.1.5.9789.x86_64.rpm

openoffice-brand-impress-4.1.5.9789.x86_64.rpm

openoffice-brand-math-4.1.5.9789.x86_64.rpm

openoffice-brand-writer-4.1.5.9789.x86_64.rpm

openoffice-brand-zh-CN-4.1.5.9789.x86_64.rpm

openoffice-calc-4.1.5.9789.x86_64.rpm

openoffice-core-4.1.5.9789.x86_64.rpm

openoffice-core01-4.1.5.9789.x86_64.rpm

openoffice-core02-4.1.5.9789.x86_64.rpm

openoffice-core03-4.1.5.9789.x86_64.rpm

openoffice-core04-4.1.5.9789.x86_64.rpm

openoffice-core05-4.1.5.9789.x86_64.rpm

openoffice-core06-4.1.5.9789.x86_64.rpm

openoffice-core07-4.1.5.9789.x86_64.rpm

openoffice-draw-4.1.5.9789.x86_64.rpm

openoffice-gnome-integration-4.1.5.9789.x86_64.rpm

openoffice-graphics-4.1.5.9789.x86_64.rpm

openoffice-impress-4.1.5.9789.x86_64.rpm

openoffice-javacol-4.1.5.9789.x86_64.rpm

openoffice-math-4.1.5.9789.x86_64.rpm
```

图 4-7 安装 Office 的 RPM 软件包

(3) 安装所有 RPM 软件包，如图 4-8 所示。

```bash
[@localhost RPMS]$# cd ~/home/zh-CN/RPMS

root@localhost/home/zh-CN/RPMS
```

```
文件(F) 编辑(E) 查找(V) 搜索(S) 帮助(H)

root@localhost RPMS]$# ls -R *.rpm
```
