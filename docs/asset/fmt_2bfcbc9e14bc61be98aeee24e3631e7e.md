
如果你希望系统消息以荷兰语或法语显示，你可能需要设置 `LANG` 和 `LANGUAGE` 环境变量，从而启用所需语言的区域支持，并可能涉及与该语言字符约定相关的字体。

在大多数图形化登录系统中，如 `gdm` 或 `kdm`，你可以在登录前配置这些语言设置。

请注意，在大多数系统中，目前的默认时区往往是 `en_US.UTF-8`。这并不成问题，因为以该编码为默认值的系统也会附带支持此编码的所有程序。因此，`vi` 可以编辑系统中的所有文件，`cat` 不会出现异常行为等。

当你连接到一个不支持这种字体编码的旧系统，或者在仅支持单字节字符字体的系统上打开一个 `UTF-8` 编码的文件时，问题就出现了。`recode` 实用程序可能有助于将文件从一种字符集转换为另一种。请阅读手册页以了解功能和用法的概览。另一种解决方案可能是临时使用另一种编码定义，通过设置 `LANG` 环境变量：

```
debby:-> acroread /var/tmp/514348.pdf
Warning: charset "UTF-8" not supported, using "ISO8859-1".
Aborted

debby:-> set | grep UTF
LANG=en_US.UTF-8

debby:-> export LANG=en_US

debby:-> acroread /var/tmp/514348.pdf
<--new window opens-->
```

参考 Mozilla <http://www.mozilla.org/> 网站以获取如何获取你语言版本的 Firefox 的指导。OpenOffice.org <http://www.openoffice.org/> 网站有关于 OpenOffice.org 套件本地化的信息。

### 7.4.5 特定国家的信息

[HOTWTOs 列表](<http://www.tldp.org/HOWTO/HOWTO-INDEX/howtos.html>)包含关于孟加拉语、白俄罗斯语、中文、世界语、芬兰语、法语、希伯来语、希腊语、拉脱维亚语、波兰语、葡萄牙语、塞尔维亚语、斯洛伐克语、斯洛文尼亚语、西班牙语、泰语和土耳其语本地化说明的参考。

## 7.5 安装新软件

### 7.5.1 概述

大多数人在安装 Linux 后看到自己拥有一个可运行、可用的计算机时会感到惊讶；大多数发行版都包含对视频卡、网卡、监视器和其他外部设备的充分支持，因此通常无需安装额外的驱动程序。常见的工具，如办公套件、Web 浏览器、电子邮件客户端等，也都包含在主要的发行版中。即便如此，初始安装可能无法满足你的需求。

如果你确实找不到需要的软件，也许它没有安装在你的系统上。也可能是你已经拥有所需的软件，但它没有按预期工作。请记住 Linux 发展迅速，软件每天都在改进。不要浪费时间在排查那些可能已经解决的问题上。

你可以随时更新系统或向其中添加软件包。大多数软件以软件包形式提供。额外的软件可以在你的安装光盘或互联网上找到。你的 Linux 发行版的网站是寻找额外软件的好地方，并包含有关如何在你的 Linux 类型上安装它的说明，参见附录 A。务必阅读随新软件提供的文档以及软件包可能包含的任何安装指南。所有软件都附带一个 `README` 文件，强烈建议你阅读它。

### 7.5.2 软件包格式

#### 7.5.2.1 RPM 软件包

##### 7.5.2.1.1 什么是 RPM？

`RPM`（RedHat Package Manager）是一个强大的软件包管理器，你可以使用它来安装、更新和删除软件包。它允许你搜索软件包，并跟踪每个软件包附带的文件。系统内置了一种机制，允许你验证从互联网下载的软件包的真实性和完整性。高级用户可以使用 `RPM` 构建自己的软件包。

一个 `RPM` 软件包由文件归档和用于安装及删除归档文件的元数据组成。元数据包括辅助脚本、文件属性以及关于软件包的描述性信息。软件包分为两种类型：二进制软件包，用于封装要安装的软件；以及源代码软件包，包含生成二进制软件包所需的源代码和配方。

许多其他发行版也支持 `RPM` 软件包，其中流行的包括 RedHat Enterprise Linux、Mandriva（前身为 Mandrake）、Fedora Core 和 SuSE Linux。除了针对你发行版的建议外，你还需要阅读 `man rpm`。

##### 7.5.2.1.2 RPM 示例

大多数软件包简单地通过 `upgrade` 选项 `-u` 进行安装，无论该软件包是否已安装。`RPM` 软件包含程序的完整版本，它会覆盖现有版本或作为新软件包安装。典型用法如下：

```
rpm -Uvh /path/to/rpm-package(s)
```

`-v` 选项产生更详细的输出，`-h` 使 `rpm` 打印进度条：

```
[root@jupiter tmp]# rpm -Uvh totem-0.99.5-1.fr.i386.rpm
Preparing...                        ###########################################
[100%]                                     ###########################################
1:totem
[100%]
[root@jupiter tmp]#
```

然而，新的内核软件包使用 `install` 选项 `-i` 进行安装，该选项不会覆盖现有的软件包版本。这样，如果新内核不起作用，你仍然可以使用旧内核启动系统。

你也可以使用 `rpm` 检查某个软件包是否已安装在你的系统上：

```
[david@jupiter ~]# rpm -qa | grep vim
vim-minimal-6.1-29
vim-X11-6.1-29
vim-enhanced-6.1-29
vim-common-6.1-29
```

或者你可以查找包含特定文件或可执行文件的软件包：

```
[david@jupiter ~]# rpm -qf /etc/profile
setup-2.5.25-1

[david@jupiter ~]# which cat
cat is /bin/cat

[david@jupiter ~]# rpm -qf /bin/cat
coreutils-4.5.3-19
```

请注意，使用 `rpm` 查询 `RPM` 数据库时，你不需要拥有管理权限。只有在添加、修改或删除软件包时才需要 `root` 权限。

# 第 7 章：温馨的 `/home` 家

```
[root@jupiter root]# rpm -e totem
[root@jupiter root]#
```

请注意，默认情况下卸载并不那么详细，看不到太多活动是正常的。如有疑问，再次使用 `rpm -qa` 验证软件包是否已移除。

`RPM` 能做的事情远不止我们在这个介绍中讨论的几个基本功能；`RPM` HOTWTO <http://www.tldp.org/HOWTO/RPM-HOWTO/index.html> 包含进一步的参考。

#### 7.5.2.2 DEB (.deb) 软件包

##### 7.5.2.2.1 什么是 Debian 软件包？

此软件包格式是 Debian GNU/Linux 的默认格式，其中 `dselect`，以及现在更常用的 `aptitude`，是管理软件包的标准工具。它用于选择你要安装或升级的软件包，但在 Debian 系统安装期间也会运行，帮助你定义要使用的访问方法、列出可用软件包并配置软件包。

Debian 网站 <http://debian.org/> 包含你需要的所有信息，包括“初学者 dselect 文档”。

根据最新消息，Debian 软件包格式越来越受欢迎。在撰写本文时，前十名发行版中有 5 个使用它。此外，`apt-get`（参见第 7.5.3.2 节）也变得越来越流行，甚至出现在非 DEB 系统上。

##### 7.5.2.2.2 DEB 工具示例

使用 `dpkg` 命令来检查软件包是否已安装。例如，如果你想知道你的机器上安装了哪个版本的 Gallery 软件：

```
nightwish@goferst:~$ dpkg -l *gallery*
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Installed/Config-Files/Unpacked/Failed-Config/Half-installed
|/ Err?=none/Hold/Reinst-r-quired/X=both-problems (Status,Err: uppercase=bad)
||/ Name Version Description
+++=-==================================================================
ii gallery 1.5-1sarge2 a web-based photo album written in php
```
