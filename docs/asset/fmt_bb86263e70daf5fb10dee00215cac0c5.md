
关键字不区分大小写，除 `network_interface` 关键字外，只能单独使用。如果一个关键字出现多次，以第一次为准。

某些关键字依赖于其他关键字，并包含在花括号 `{}` 中。除非指定了相应的父（独立）关键字，否则无法使用这些关键字。下一页的表 12.2 列出了独立关键字。有关依赖关键字的信息，请参阅 `sysidcfg` 的主页。

作为 `sysidcfg` 的替代方案，还可以通过 DHCP 或 DNS 等网络服务指定有限的配置选项。然而，由于替代路径提供的选项有限，我们建议使用 `sysidcfg`。

以下 `sysidcfg` 示例配置了一个名为 `sake` 的系统，该系统有一个网络接口。

- 1. 参考“自定义 JumpStart 和高级安装”访问 Sun 指南，其中包含了规则文件和配置文件的完整细节。

## 第 12 章 软件安装与管理

### 12.2 JumpStart sysidcfg 文件的独立关键字

| 关键字 | 指定的内容 |
| --- | --- |
| keyboard | 键盘布局和语言 |
| name_service | NIS、DNS 或 LDAP 的名称服务配置 |
| network_interface | 连接详情：主机名、IP 地址等 |
| nfs4_domain | NFS 版本 4 使用的域 |
| root_password | 加密的 root 密码 |
| security_policy | Kerberos 网络身份认证 |
| service_profile | 可用的网络服务 |
| system_locale | 系统语言 |
| terminal | 终端类型 |
| timezone | 网络日期时间服务器 |

```
keyboard=US-English

system_locale=en_US

timezone=US/Mountain

terminal=sun-cmd

timeserver=time.nist

name_service=DNS [domain_name=solaris.booklab.astrust]

name_server=192.168.2.10

search-astrust.com,booklab.astrust.com

nfs4_domain=dynamic

root_password=m4QFOWNY

network_interface=e-1000g0 [hostname=sake]

default_route=192.168.10.254

ip_address=192.168.10.155

netmask=255.255.255.0
```

如果你将相同的 `sysidcfg` 文件分发给许多客户端，则不同系统之间的 IP 地址需要不同。你可以省略网络接口详情，以强制它们在系统首次启动时进行配置。或者，为了从 DHCP 获取网络地址而不是进行分配，静态地使用：

```
network_interface=e-1000g0 (dhcp)
```

设置好规则文件、`sysidcfg` 文件和配置后，将它们全部复制到 `/jumpstart/config` 目录并运行 Sun 的检查工具，该工具会验证配置。检查脚本应在 config 目录下运行，且是强制性的；它会创建一个 `rules.ok` 文件，向 JumpStart 证明文件在语法上是可以接受的。不要跳过此步骤，否则 JumpStart 将无法工作。

```
solaris sudo cp /jumpstart/s10sparc/Solaris_10/Misc/jumpstart_sample/check /jumpstart/config

solaris sudo ./check

Validating rules

Validating profile_A.

The Custom JumpStart configuration is ok
```

## 使用自动安装程序进行网络安装

配置过程结束后，你的 `/jumpstart/config` 目录应该如下：

```
solaris$ ls -l

-rw-xr-xr 1 root root 52152 Aug 23 19:42 check

-rw-r--r-- 1 root root 413 Aug 23 19:29 profile_a

-rw-r--r-- 1 root root 48 Aug 23 19:13 rules

-rw-r--r-- 1 root root 62 Aug 23 19:43 rules.ok

-rw-r--r-- 1 root root 62 Aug 23 19:35 sysidcfg
```

## 12.3 安装 HP-UX

作为一种面向服务器的操作系统，其目标几乎完全是针对需要大量繁重工作的大型应用程序，HP-UX 并不试图提供一种华丽的次世代安装过程。其基于文本的安装软件具有实用性，并会引导您完成基础配置选项：磁盘分区、网络设置、要安装的软件等。

对于需要基于网络和自动化的安装的站点，可以使用 HP 的 Ignite-UX 选项。Ignite-UX 可以通过网络同时安装多个 HP-UX 系统。PA-RISC 客户端使用 BOOTP 启动，而 Titanium 系统使用 DHCP。您可以配置多个软件仓库。例如，安装包可以从一个位置提供，补丁从另一个位置提供而应用程序包从第三个位置提供。作为额外奖励，Ignite-UX 还包含一个恢复服务，可以从最近的镜像恢复机器配置。

设置 Ignite-UX 需要以下步骤：

- 在服务器上安装 Ignite-UX 软件和 HP-UX 软件包。
- 配置 Ignite-UX 以提供适当的安装选项。
- 启用 Ignite-UX 服务依赖项，如 NFS 和 BOOTP。
- 将客户端的 MAC 和 IP 地址添加到服务器。

配置好服务器后，您可以在客户端系统上（通过 HP 的 EFI Boot Manager）添加启动选项，使它们能够从 Ignite-UX 服务器安装 HP-UX。或者，对于已经在运行 HP-UX 的系统，您可以使用 `bootsys` 将安装从客户端推送到服务器。

在我们的示例系统中，自带了 Ignite-UX，但如果您的系统没有它，请尝试命令 `swinstall -s /vdrom Ignite-UX`。在这里，`/vdrom` 是包含操作系统介质的 DVD 的挂载点，在 HP 的术语中称为“操作系统环境”。安装将产生许多已安装包，其中一些列在下方。

```
hp-ux sudo swlist Ignite-UX
```

| Ignite-UX | C.7.142 | HP UX 系统安装服务 |
| :--- | :--- | :--- |
| Ignite-UX BOOT-COMMON-IA | C.7.142 | IPF 客户端的启动组件 |
| ignite-UX BOOT-COMMON-PA | C.7.142 | PA-RISC 客户端的启动组件 |
| Ignite-UX BOOT-KRN-11-11 | C.7.142 | B.11.11 客户端的启动内核 |
| Ignite-UX BOOT-KRN-11-23 | C.7.142 | B.11.23 客户端的启动内核 |
| ignite-UX BOOT-KRN-11-31 | C.7.142 | B.11.31 客户端的启动内核 |
| Ignite-UX BOOT-SERVICES | C.7.142 | 安装所需的启动服务 |

Ignite-UX 将其配置文件和二进制文件随意地分布在文件系统中。下一页的表 12.3 列出了最重要的组件。

## 表 12.3 Ignite-UX 使用的重要二进制二进制文件、目录和配置文件

| 文件名 | 用途 |
| :--- | :--- |
| /etc/bootptap | 作为 bootpd 的纯文本“数据库” |
| /opt/ignite/instl_bootapt | 记录启动 PA-RISC 客户端的 IP 地址 |
| /opt/ignite/bin/bootsys | 更新已经在运行 HP-UX 的客户端 |
| /opt/ignite/bin/make_config | 使用安装库创建配置文件 |
| /opt/ignite/bin/make_depots | 从某些源介质创建安装库 |
| /opt/ignite/bin/manage_index | 向 Ignite-UX 索引添加存储库 |
| /opt/ignite/libn/setup_server | 通过 NFS 共享 /var/opt/ignite/clients |
| /var/opt/ignite/clients | 存储配置文件 (目录) |
| /var/opt/ignite/data | 传统上用于安装库 (目录) |
| /var/opt/ignite/INDEX | 索引 Ignite-UX 已知的所有库 |

`make_depots` 命令提取安装包并将其设置为用于安装到客户端的操作系统环境。在创建存储库后，运行 `make_config` 读取库的内容并创建一个描述它们的配置文件。通过 `manage_index` 命令将配置转变为 Ignite-UX，该命令将配置添加到 INDEX 文件中。以下是版本 11i3 的示例命令序列：

```
hp-ux cd /opt/ignite/bin

hp-ux sudo ./make_depots -s /dev/dsk2t2d0

cd /var/opt/ignite/depots/Rel.B11.31/oe_media

hp-ux sudo ./make_config -s /var/opt/ignite/depots/Rel.B11.31/core_media

cd /var/opt/ignite/data/Rel.B11.31/oe_media_cfg

hp-ux sudo ./manage_index -n "HP-UX 11.31 Default" -c "11i v3"

hp-ux sudo ./manage_index -a

- /var/opt/ignite/data/Rel.B11.31/oe_media_cfg -c "11i v3"
```

在服务器被客户端使用之前，您必须启用 BOOTP 并共享客户端目录。单个客户端还必须添加到 `instl_bootapt` 中。`make_depots` 命令提取安装包并将其设置为用于安装到客户端的操作系统环境。在您创建存储库后，运行 `make_config` 读取库的内容并创建一个描述它们的配置文件。配置通过 `manage_index` 命令转变为 Ignite-UX，该命令将配置添加到 INDEX 文件中。以下是版本 11i3 的示例命令序列：

在服务器被客户端使用之前，您必须启用 BOOTP 并共享客户端目录。单个客户端还必须添加到 `instl_bootapt` 中。在配置好服务器后，您可以在客户端系统上（通过 HP 的 EFI Boot Manager）添加启动选项，使它们从 Ignite-UX 服务器安装 HP-UX。或者，对于已经在运行 HP-UX 的系统，您可以使用 `bootsys` 将安装从客户端推送到服务器。

在我们的示例系统中，自带了 Ignite-UX，但如果您的系统没有它，请尝试命令 `swinstall -s /vdrom Ignite-UX`。在这里，`/vdrom` 是包含操作系统介质的 DVD 的挂载点，在 HP 的术语中称为“操作系统环境”。安装将产生许多已安装包，其中一些列在下方。

```
hp-ux sudo swlist Ignite-UX
```

Ignite-UX 将其配置文件和二进制文件随意地分布在文件系统中。下一页的表 12.3 列出了最重要的组件。

## 表 12.3 Ignite-UX 使用的重要二进制二进制文件、目录和配置文件

（表格内容已在上文翻译）

`make_depots` 命令提取安装包并将其设置为用于安装到客户端的操作系统环境。在您创建存储库后，运行 `make_config` 读取库的内容并创建一个描述它们的配置文件。配置通过 `manage_index` 命令转变为 Ignite-UX，该命令将配置添加到 INDEX 文件中。以下是版本 11i3 的示例命令序列：

（代码块已在上文翻译）

## 12.3 安装 HP-UX

作为一种面向服务器的操作系统，其目标几乎完全是针对需要大量繁重工作的大型应用程序，HP-UX 并不试图提供一种华丽的次世代安装过程。其基于文本的安装软件具有实用性，并会引导您完成基础配置选项：磁盘分区、网络设置、要安装的软件等。

对于需要基于网络和自动化的安装的站点，可以使用 HP 的 Ignite-UX 选项。Ignite-UX 可以通过网络同时安装多个 HP-UX 系统。PA-RISC 客户端使用 BOOTP 启动，而 Titanium 系统使用 DHCP。您可以配置多个软件仓库。例如，安装包可以从一个位置提供，补丁从另一个位置提供而应用程序包从第三个位置提供。作为额外奖励，Ignite-UX 还包含一个恢复服务，可以从最近的镜像恢复机器配置。

设置 Ignite-UX 需要以下步骤：

- 在服务器上安装 Ignite-UX 软件和 HP-UX 软件包。
- 配置 Ignite-UX 以提供适当的安装选项。
- 启用 Ignite-UX 服务依赖项，如 NFS 和 BOOTP。
- 将客户端的 MAC 和 IP 地址添加到服务器。

配置好服务器后，您可以在客户端系统上（通过 HP 的 EFI Boot Manager）添加启动选项，使它们能够从 Ignite-UX 服务器安装 HP-UX。或者，对于已经在运行 HP-UX 的系统，您可以使用 `bootsys` 将安装从客户端推送到服务器。

在我们的示例系统中，自带了 Ignite-UX，但如果您的系统没有它，请尝试命令 `swinstall -s /vdrom Ignite-UX`。在这里，`/vdrom` 是包含操作系统介质的 DVD 的挂载点，在 HP 的术语中称为“操作系统环境”。安装将产生许多已安装包，其中一些列在下方。

```
hp-ux sudo swlist Ignite-UX
```
