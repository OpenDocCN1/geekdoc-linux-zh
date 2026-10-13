

## 我在 Webmin 中启用了 SSL，现在无法登录了。

你可能没有先将端口移到 1024 以上。要解决这个问题，请停止 Webmin，然后 `cd` 到 `/etc/webmin`。文件 `miniserv.conf` 包含各种配置，你可以将 `ssl=1` 改为 `ssl=0`，或者将 `port=1000` 改为 `port=10000`，然后重新启动 Webmin。

如果仍然遇到问题（没有常见的加密算法），你需要下载并安装最新的 Webmin。删除 `/etc/webmin` 和 `/usr/libexec/webmin` 目录，然后将 Webmin 安装到 `/usr/libexec`。运行设置脚本并采用默认值。

## 我安装了 Webmin，但不记得用户名或密码了。

你可以 `cd` 到 `/etc/webmin` 并查看 `miniserv.users` 文件。该文件包含以冒号分隔条目的行。第一列包含用户名，第二列包含加密密码，最后一列包含用户 ID 号。你可以移除加密哈希，使该行看起来像下面这样：

```
root::1
```

然后你可以以 root 身份无密码登录（但请尽快在 Webmin 用户模块中为该用户输入另一个密码）。如果 Webmin 不允许 root 用户没有密码，只需从 `/etc/shadow` 中复制并粘贴哈希密码即可。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_748_0.png)

## 附录

- A 常用命令 733
- B 查找更多关于 Linux 的信息 741

## 常用命令

本附录包含

- 使用命令 734
- 选项 734
- 使用目录 735
- 使用文件 735
- 网络工具 736
- 系统工具 737

### 使用命令

大多数 Linux 命令的执行方式与其 UNIX 对应命令完全相同。许多命令相当晦涩，因此使用 Linux 命令的典型挑战是将合适的命令与所需功能相匹配。本附录中列出的命令并非详尽无遗；相反，它旨在提供常用命令的快速参考以及每个命令功能的简要说明。这里列出的命令位于四个二进制目录之一：/bin、/sbin、/usr/bin 和 /usr/sbin。

除 cd 命令外，每个命令都有对应的在线手册页。你可以随时在 shell 提示符下输入以下内容来参阅这些手册页：

```
# man <command>
```

例如，如果你想查看创建目录命令（mkdir）的手册页，你需要在 shell 提示符下输入以下内容：

```
# man mkdir
```

在输入上述内容并按回车后，你应该会看到以下内容：

```
MKDIR(1)                              MKDIR(1)

NAME
    mkdir - make directories

SYNOPSIS
    mkdir [-p] [-m mode] [--parents] [--mode=mode] [--help] [--version] dir...

DESCRIPTION
    This documentation is no longer being maintained and may be inaccurate or
    incomplete. The Texinfo documentation is now the authoritative source.

    This manual page documents the GNU version of mkdir. mkdir creates a directory
    with each given name. By default, the mode of created directories is 0777
    minus the bits set in the umask.
```

### 选项

一些 man 页面会包含一条免责声明，指引你查看 info 页面。自由软件基金会（FSF）/GNU 的领导层一直推动用 info 页面取代 man 页面，因此许多 FSF/GNU 软件的 man 页面内容不完整，并附有指向 info 的提示。是否同意这一点由你自己决定。

你可以通过在 shell 提示符下输入 info 命令来访问 Texinfo 文档。其中有一个基于 X Window 的 tkinfo（未随 OpenLinux 附带）是更友好的版本。有关这些命令的更多详细信息，请参阅 Texinfo 文档或 man 页面。

这些命令分为以下四个类别：

- 使用目录
- 使用文件
- 网络工具
- 系统工具

### 使用目录

| 命令 | 语法（示例） | 描述 |
|---|---|---|
| cd | `cd [path]` | 切换到指定路径的目录。 |
|  | `cd ..` | 切换到当前目录的父目录。 |
|  | `cd -` | 切换到上一次 `cd` 命令之前的工作目录。 |
|  | `cd` | 切换到当前登录 ID 的主目录。 |
|  | `cd ~` | 切换到当前登录 ID 的主目录。 |
| dir |  | 参见 `ls` 命令。 |
| ls | `ls [path]` | 列出目录的内容。 |
|  | `ls -l` | 以长格式列出文件，显示所有文件属性。 |
|  | `ls -a` | 列出所有文件（包括隐藏文件，有时称为点文件）。 |
| mkdir | `mkdir <directory>` | 创建一个新目录。 |
| pwd |  | 显示当前工作目录。 |
| rmdir | `rmdir <directory>` | 删除一个目录。 |

### 使用文件

| 命令 | 语法（示例） | 描述 |
|---|---|---|
| cat | `cat <file>` | 最常用于显示文件内容。源自“concatenate”一词，该命令也能实现此功能。 |
| chattr | `chattr <option> file` | 更改文件的 ext2 属性。某些选项仅对 UID 0 可用。 |
| cp | `cp <source> <dest>` | 复制文件。 |
| dd | `dd if=input of=output` | 最常用于转换文件。可用于将镜像文件从一个设备复制到另一个设备或文件。 |
| file | `file <file>` | 确定给定文件的类型。 |
| grep | `grep <pattern> <file>` | 在一个或多个文件中搜索指定的模式。 |
| gzip | `gzip <name>` | 使用 Lempel-Ziv 编码压缩文件。使用此工具压缩的文件带有 `.gz` 后缀。 |
| gunzip | `gunzip <name>` | 解压缩 gzip 压缩的文件。 |
| less | `less <file>` |  |
|  | `cat <file> \| less` | 与 more 命令类似，但便于在被查看的文件中向前和向后移动。名称来源于“Less is more”这句话。 |
| ln | `ln <source> <dest>` | 用于在同一分区上的文件之间创建硬链接。 |
|  | `ln -s <source> <dest>` | 用于在不同分区上的文件之间或目录之间创建符号（或软）链接。 |
| lsattr | `lsattr [option][file]` | 列出文件或目录的 ext2 属性。 |
| more | `more <file>` |  |
|  | `cat <file> \| more` | 用于一次一页地显示文件内容。 |
| mv | `mv <source> <dest>` | 用于重命名文件。 |
| rm | `rm <file>` | 删除指定的一个或多个文件。 |
| tar | `tar <archive> <files>` | 一个归档工具。用于归档或取消归档一组文件。 |
|  | `tar -cvf a.tar /etc` | 创建一个名为 a.tar 的归档文件，其中包含 `/etc` 目录下的文件和子目录。 |
|  | `tar -xvf a.tar` | 解压 a.tar 归档中的所有文件。 |
| unzip | `unzip [options] file` | 与处理 ZIP 归档的类似 DOS 压缩工具兼容的压缩工具。 |
| vi | `vi <file>` | 全屏编辑器。 |
| zip | `zip [options] <zipfile>` | 创建 ZIP 归档。 |

### 网络工具

| 命令 | 语法（示例） | 描述 |
|---|---|---|
| dig | `dig <domain>` | 域名信息查询工具。用于从域名服务器收集信息。 |
| dnsdomainname | `dnsdomainname` | 显示给定服务器的域名。 |
| host | `host <host>` | 使用域名服务器查找主机或主机 IP 地址。 |
| hostname | `hostname` | 显示服务器的完全限定域名（FQDN）。 |
| ifconfig | `ifconfig` | 显示当前配置的网络接口。 |
|  | `ifconfig [interface] [options]` | 配置网络接口。 |
| netstat | `netstat` | 显示网络连接状态、路由表和接口统计信息。 |
| ping | `ping <host>` | 向指定主机发送 ECHO_REQUEST 数据包。可达主机会返回响应数据包。常用于调试网络连接。 |
| nslookup | `nslookup` | 名称服务器查询工具。用于查询域名服务器。 |
| route | `route` | 显示路由表的当前配置。 |
|  | `route [options]` | 配置 IP 路由表。 |
| traceroute | `traceroute <host>` | 显示 IP 数据包的路由。对调试网络问题很有用。 |

### 系统工具

| 命令 | 语法（示例） | 描述 |
|---|---|---|
| chage | `chage [option] user` | 更改密码老化设置。 |
| chgrp | `chgrp <group> <file>` | 更改文件所属的组。 |
| chmod | `chmod <mode> <file>` | 更改指定文件或文件的访问权限。 |
| chown | `chown <owner> <file>` | 更改给定文件或文件的所有者。 |
| coastool | `coastool` | 使用 COAS 管理系统。 |
| date | `date` | 显示系统日期设置。 |
|  | `date <MMDDhhmmYY>` | 设置日期。 |
|  |  | MM = 月 |
|  |  | DD = 日 |
|  |  | hh = 小时（24 小时制） |
|  |  | mm = 分钟 |
|  |  | yy = 年 |
| df | `df` | 显示给定文件系统的空闲磁盘空间摘要。 |
| dmesg | `dmesg` | 显示上次系统启动时的启动消息。 |

