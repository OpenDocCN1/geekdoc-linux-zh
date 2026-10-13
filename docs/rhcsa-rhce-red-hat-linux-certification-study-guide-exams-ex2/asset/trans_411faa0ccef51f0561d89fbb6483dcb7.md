
## 名称解析

下面的部分允许您使用 NetBIOS 名称和 IP 地址的数据库设置 Samba 服务器，以以下注释开始：

```
#---------- Name Resolution ----------------
```

Windows Internet Name Service（WINS）在 Samba 等基于 Microsoft 的网络上与 DNS 功能等效。如果激活以下命令，Samba 将在本地计算机上激活 WINS 服务器：

```
; wins support = yes
```

另外，您可以将本地计算机指向网络上的远程 WINS 服务器；当然，您需要将 w.x.y.z 替换为 IP 地址。不要在同一系统上同时激活 wins support 和 wins server 指令，因为它们不兼容。

```
; wins server = w.x.y.z
```

并非每个 Linux 系统上都安装了 Samba 服务器。在这种情况下，您可以启用以下指令，以允许仅使用 Samba 客户端软件的系统访问：

```
; wins proxy = yes
```

如果名称解析请求的答案不在 WINS 服务器中，以下指令将允许通过配置的 DNS 服务器进行相同的搜索：

```
; dns proxy = yes
```

## 打印选项

打印机包含在 RHEL 5 的 RHCT 考试目标中。然而，它们未列在 RHEL 6 的 RHCSA 或 RHCE 目标中。尽管如此，打印是默认 Samba 服务器配置的一部分。因此，您至少应扫描 Samba 配置文件中的该部分，以以下注释开始：

```
#---------- Printing Options ----------------
```

这些默认打印机设置是共享此 Samba 服务器打印机所必需的。以下三个指令加载由 printcap name = /etc/printcap 定义的打印机。

cups options = raw 指令意味着打印作业已由具有打印处理器（如 CUPS 服务）的服务处理。

```
load printers = yes
cups options = raw
printcap name = /etc/printcap
```

另外，可以配置不同的打印服务器。以下选项获取旧版 Linux 系统上配置的打印机信息：

```
printcap name = lpstat
```

## 文件系统选项

下面的部分支持扩展属性的配置，这些属性与 Microsoft 文件的访问控制列表（ACL）设置相关联。通过正确的选项，可以存储此类属性。Samba 配置文件中的注释引用了 Microsoft 磁盘操作系统（DOS），作为指定此类共享文件权限和相关 ACL 位的简写。以下内容将是所有共享目录的默认值，以以下注释开始：

```
#----------------- Filesystem Options -----------------
```

首先，map archive 指令可以控制 DOS 文件归档属性是否映射到本地 Linux 可执行位（如果 create mask 指令支持）。

```
; map archive = no
```

map hidden 指令可以控制 DOS 隐藏文件是否映射到本地 Linux 可执行位（如果 create mask 指令支持）。

```
; map hidden = no
```

map read only 指令，也称为 Samba 文档中的 map readonly，如图所示，对于 DVD 等共享挂载媒体很有用：

```
; map read only = no
```

map system 指令，如果设置为 yes，则支持对 DOS 系统文件使用 Linux 可执行位：

```
; map system = no
```

最后，如果 store dos attributes 指令处于活动状态，它将尝试存储先前配置的 DOS 文件 ACL：

```
;     store dos attributes = yes
```

## 共享 Samba 目录

主 Samba 配置文件 /etc/samba/smb.conf 的第二部分用于通过 Samba 设置共享目录和打印机。本节包括对该文件默认版本的分析。

在 Samba 中，共享目录的设置按 stanzas 组织，stanzas 是与共享名称关联的命令组。（Stanza 似乎不是技术术语，但有些人认为结构良好的配置代码就像好的诗歌。）

### 共享主目录

本节中的前四行定义了 [homes] 共享，它会自动共享已登录用户的 home 目录。每个用户都可以访问自己的 home 目录；browseable = no 命令可防止用户访问彼此的 home 目录。

没有默认的 /homes 目录。它只是一个标签。您无需提供 home 目录，因为 Samba 会读取 /etc/passwd 中的用户账户记录以确定要共享的目录。

默认情况下，这不允许未知用户访问（guest ok = no）。此外，您可以使用前面描述的 hosts allow 和 hosts deny 等指令限制可以使用此共享的系统。hosts allow 和 hosts deny 指令的效果仅限于使用它们的共享 stanza。

```
#=========================== Share Definitions ===========================
[homes]
    comment = Home Directories
    browseable = no
    writable = yes
```

smb.conf 中有一些拼写不正确的变量，例如 browseable。在某些情况下，正确的拼写（browsable）也有效。即使拼写错误，它们仍然是被接受的 Samba 变量，通常应按照 Samba 默认设置拼写，而不是标准书面英语。

考试提示 在共享主目录实际上可以通过 Samba 共享文件之前，SELinux samba_enable_home_dirs 布尔值必须处于活动状态。

### 共享打印机

[printers] stanza 通常按原样工作，允许计算机或域上拥有账户的所有用户访问。尽管 spool 目录（/var/spool/samba）不可浏览，但相关打印机可以通过其 NetBIOS 名称浏览。虽然更改很简单，但标准选项意味着不允许访客用户打印，相关的打印 spool 不可写，并且 printable = yes 是加载相关配置文件（如 CUPS）的先决条件。

```
# NOTE: If you have a BSD-style print system there is no need to
# specifically define each individual printer
[printers]
comment = All Printers
path = /usr/spool/samba
browseable = no
# Set public = yes to allow user 'guest account' to print
guest ok = no
writable = no
printable = yes
```

### 域登录

以下 stanza 中的命令支持为 Microsoft Windows 工作站配置 [netlogon] 共享。由于即使对于启用 Samba 的 Linux 工作站也没有 [netlogon] 共享，本节需要 Microsoft Windows 计算机来验证功能。如果您认为在 Red Hat 考试期间会使用 Microsoft Windows 计算机，请仔细学习本节。

```
# Un-comment the following and create the netlogon directory for
# Domain Logons
; [netlogon]
; comment = Network Logon Service
; path = /var/lib/samba/netlogon
; guest ok = yes
; writable = no
; share modes = no
```

### 工作站配置文件

下一个 stanza 配置 Microsoft Windows 工作站的配置文件。由于这些配置文件在登录这些工作站之一时成为 Microsoft Windows 注册表的一部分，您不太可能在仅 Linux 计算机网络中配置本节。请自行判断本节在 RHCE 考试期间是否适用。

```
# Un-comment the following to provide a specific roving profile
# share; the default is to use the user's home directory
;[Profiles]
; path = /var/lib/samba/profiles
; browseable = no
; guest ok = yes
```

### 组目录

以下 stanza，如注释所建议，配置 /home/samba 目录由名为 staff 的组共享。您可以配置此常用用户组共享此目录。要为 /home/samba 配置特殊所有权和权限，您还需要配置适当的权限。这两个过程均在第 8 章中描述。

```
# A publicly accessible directory, but read only, except for
# people in the "staff" group
;[public]
; comment = Public Stuff
; path = /home/samba
; public = yes
; writable = yes
; printable = no
; write list = +staff
```

为了在共享目录上设置适当的权限，您可能还希望包含以下用于创建文件和目录的指令：

```
create mask = 0770
directory mask = 2770
```

Samba 的一个区别是 Microsoft 身份验证数据库不允许用户和组具有相同的名称。此外，/home/samba 目录以及该目录中包含的任何文件通常必须具有正确的 SELinux 文件类型，这可以通过以下命令实现：

```
# chcon -R -t samba_share_t /home/samba
```

当然，您希望确保此类更改在 SELinux 重新标记后仍然存在，并且可以通过以下命令为所述目录配置：

```
# semanage fcontext -a -t samba_share_t /home/samba
```
