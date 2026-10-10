
```
# rpm -qi dosfstools
Name    : dosfstools      Relocations: (not relocatable)
Version : 3.0.1           Vendor: Fedora Project
Release		: 4.fcl1			Build Date: Mon 10 Aut 2009 11:05:22 AM EDT
Install Date:	Sun 27 Nov 2009 05:57:12 PM EDT Build Host:	xenbuilder2.fedora.redhat.com
Group		: Applications/System	Source RPM:	dosfutils-3.0.1-6.fc12.src.rpm
Size		: 185139			License:	GPLv3+
Signature :	(RDM/6, Mon 28 Sep 2009 03:13:56 PM EDT, Key ID 94dcc34857b2bbcba
Package		: Fedora Project
URL			:	http://www.daniel-bausman.ch/software/dosfstools/
Summary		: Utilities for making and checking MS-DOS FAT filesystems on Linux
Description:	
The dosfstools package includes the mkdosfs and dosfsck utilities,
which respectively make and check MS-DOS FAT filesystems on hard
drives or on floppies.
```

要了解软件包的内容，您可以将 `-l`（列表）选项与查询一起使用。以下示例显示了 `dosfstools` 软件包中包含的文件的完整路径名：

```
# rpm -ql dosfstools | less
/sbin/dosfsck
/sbin/fsck.msdos
/sbin/fsck.vfat
/sbin/mkdosfs
/sbin/mkfs.msdos
/sbin/mkfs.vfat
/usr/share/man/man8/dosfsck.8.gz
```

您是否想知道如何使用软件包中的组件？使用查询加上 `-d` 选项将显示随软件包包含的文档（man 页、README 文件、HOWTO 等）。如果您在使 X 窗口系统正常运行方面遇到问题，可以使用以下命令行找到可能有用的文档：

```
# rpm -qd xorg-x11-server-Xorg | less
/usr/share/man/man1/Xorg.1.gz
/usr/share/man/man1/cvt.1.gz
/usr/share/man/man1/gtf.1.gz
/usr/share/man/man4/exa.4.gz
/usr/share/man/man4/fbdevhw.4.gz
/usr/share/man/man5/xorg.conf.5.gz
```

许多软件包都有相关的配置文件。要查看与特定软件包相关的配置文件，请将 `-c` 选项与查询一起使用。例如，这是您输入以查找 `ppp` 软件包所用配置文件的示例：

```
# rpm -qc ppp
/etc/logrotate.d/ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

如果您想知道某个特定命令或配置文件来自哪个软件包，您可以使用 `-qf` 选项。在以下示例中，`-qf` 选项显示 `chgrp` 命令来自 `fileutils` 软件包：

```
# rpm -qf /bin/chgrp
coreutils-7.6-1.fc12.i386
```

在安装软件包之前，您可以对其执行与对已安装软件包相同的查询。这是一个很好的工具，可用于在软件包位于当前目录或软件存储库中时查找信息。以下是使用 `-qp` 选项配合 `-i` 查看软件存储库中软件包描述的示例：

```
# rpm -qp -i http://ayo.freshrpms.net/fedora/linux/9/i386/freshrpms/RPMS/a52dec-0.7.4-8.fc7.i386.rpm
Name    : a52dec Relocations: (not relocatable)
Version : 0.7.4 Vendor: Freshrpms.net
Release : 8.fc7 Build Date: Wed 30 May 2007 01:02:28 PM CDT
Install Date: (not installed) Build Host: python3.freshrpms.net
Group   : Applications/Multimedia Source RPM: a52dec-0.7.4-8.fc7.src.rpm
Size    : 106856 License: GPL
Signature : DSA/SHA1, Wed 30 May 2007 01:02:58 PM CDT, Key ID 692ac55e42d5447b
Packager : Matthew Sauve <matthias@sauveforge.net>
URL     : http://liba52.sourceforge.net/
Summary : Library for decoding ATSC A/52 (aka AC-3) audio streams
Description :
liba52 is a free library for decoding ATSC A/52 streams. It is released under the terms of the GPL license. The A/52 standard is used in a variety of applications, including digital television and DVD. It is also known as AC-3.
```

在上面的示例中，显示在三行上的长命令行实际上应该在一行输入。如果您担心下载软件包的内容或合法性，此示例提供了一种在下载软件包之前阅读其描述的方法。

在以下示例中，该命令列出了位于当前目录中的软件包所包含的文件：

```
# rpm -qp -l AdobeReader\_enu-8.3.1-1.i486.rpm
```

再次强调，这是在安装软件包之前了解其内容的绝佳方式。

### 使用 rpm 验证已安装的软件包

如果软件包中的某些内容运行不正常，或者您怀疑您的系统已被篡改，`rpm` 的验证（`-V`）选项可以帮助您将已安装软件与其原始软件包进行验证。每个已安装软件包的信息存储在

你的计算机在 RPM 数据库。通过使用 verify 选项，你可以检查包中的组件是否有任何更改。

> **注意：** verify 选项使用大写字母（~v），而 verbose 选项使用小写字母（~v）。

在执行 verify 操作期间，会进行各种文件大小和权限测试。如果一切正常，则没有输出。任何自安装以来发生更改的组件将被打印出来，并附上说明其如何更改的信息。以下是一个示例：

```
# rpm -v ppp
S.5....T.  c /etc/ppp/chap-secrets
S.5....T.  c /etc/ppp/options
S.5....T.  c /etc/ppp/pap-secrets
```

此输出显示 `ppp` 包（使用点对点协议（PPP）拨入 TCP/IP 网络（如互联网）的软件包）自安装以来已有三个文件发生更改。开头的标注显示文件大小（S）、MD5 校验和（5）以及修改时间（T）均已更改。字母 `c` 表示这些都是配置文件。通过审查这些文件，确认更改仅是我为了让 PPP 正常工作而所做的修改，我可以验证该软件没有问题。

在验证配置文件内容时，你可能会看到以下指示符：

- `5`（**MD5 校验和**）—— MD5 校验和指示文件内容的更改。

- `S`（**文件大小**）—— 文件中的字符数已更改。

- `L`（**符号链接**）—— 文件已变为指向另一个文件的符号链接。

- `T`（**修改时间**）—— 文件的修改时间已更改。

- `D`（**设备**）—— 文件已变为设备特殊文件。

- `U`（**用户**）—— 拥有该文件的用户名已更改。

- `G`（**组**）—— 分配给该文件的组已更改。

- `M`（**模式**）—— 文件的所有权或权限已更改。

> **提示：** 有一个工具可以在 Microsoft Windows 下浏览 RPM 文件的内容。使用 `rpmbrowser.exe` 工具，你可以列出并提取 RPM 发行版中的文件。此工具可从 wintsite.com 获取（从 http://www.wintsite.com/search 搜索 rpmbrowser）。

### 在救援模式下使用 RPM
