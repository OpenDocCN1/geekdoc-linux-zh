
第一行指定了接收的主机名。第三列让这些条目有点不同，它们将指定 `domain.com.` 的主 DNS 服务器。这是备用服务器将填充缓存的地方。最后一列指定了 `domain.com` 的。留在系统。

# TCP/IP 网络管理

## 第13 章

> 站点通常会为所有主机选择一种命名方案。这往往有助于更容易记住它们的名称，特别是随着规模的扩大。例如，办公室的东翼使用著名的乐队为他们的机器命名，而西翼使用乐器名称。这使得通过名称定位机器变得更容易。

列表 13.1 包含了 `domain.hosts` 文件。

### 列表 13.1. domain.hosts 文件。

```
+   ; domain.com. hosts 文件的正映射
; 更新历史:
  ; August 6, 1997 - sshah@domain.com
  ; 设置 domain.com. 的主 DNS
```

### 列表 13.1. 继续

```
@ IN SOA domain.com. hostmaster.domain.com. (
    ; 序列号
    199700600 ; refresh rate (30 hours)
    18000 ; retry (30 minutes)
    1209600 ; expire (2 weeks)
    648000 ; minimum (1 week)

IN NS ns1.domain.com
IN NS ns2.domain.com
IN MX 10 mailhub.domain.com
numark IN CNAME ns1 192.168.42.1
domain. IN CNAME numark 192.168.42.2
mtx IN CNAME ns2 192.168.42.3
pionier IN A 192.168.42.4
denon IN A 192.168.42.5
atus IN A 192.168.42.6
technics IN A 192.168.42.7
vestax IN CNAME vestax
www IN CNAME rane 192.168.42.8
mailhub IN A rane
```

注意到这里使用了 `@` 符号而不是域名吗？这是一个你可以使用的快捷方法，因为域名名已经在 `/etc/named.boot` 文件中指定。

关于名称的额外说明。在前面的示例中，从管理的角度来看，使用机器命名是有帮助的。列表 13.1 使用了制造专业音频设备的公司名称。然而，遵循这种方式，你可能会遇到其他人对你的系统（例如你的 Web 服务器）有特定名称的情况。默认情况下，大多数人期望 Web 服务器的名称为 `www.domain.com`。虽然你可以将机器命名为 `www.`，但会产生两个问题：首先，命名方案破坏了。如果你的站点足够大，这可能会成为问题。如果你想启动一个新的 Web 服务器，你必须相应更改所有机器的配置。相比之下，将 DNS 中的 `CNAME` 指向一个新的 Web 服务器要容易得多。

列表 13.2 `domain.reverse` 文件。

## 列表 13.2. `domain.reverse` 文件。

```
; domain.com 的反向映射
; 版本修订历史：ssah@domain.com, 1997年8月6日
@ IN SOA domain.com. hostmaster.domain.com. (
    ; 序列号
    199700600 ; refresh rate (30 hours)
    18000 ; retry (30 minutes)
    1209600 ; expire (2 weeks)
    648000 ; minimum (1 week)

IN NS ns1.domain.com
IN NS ns2.domain.com
```

# 第 13 章

| 192.168.42.1 | IN PTR numark |

| 192.168.42.2 | IN PTR mtx |

| 192.168.42.3 | IN PTR pioneer |

| 192.168.42.4 | IN PTR denon |

| 192.168.42.5 | IN PTR atux |

| 192.168.42.6 | IN PTR technics |

| 192.168.42.7 | IN PTR vestax |

| 192.168.42.8 | IN PTR rane |

最后，13.3 包含了 `local.reverse` 文件。

## 列表 13.3. `local.reverse` 文件。

```
; local.reverse domain.com. hostmaster.domain.com. (
@ IN SOA 1997086000 ; 序列号
10000 ; refresh rate (3 hours)
1800 ; retry (20 minutes)
1209600 ; expire (2 weeks)
604800 ; minimum (1 week)
IN NS ns1.domain.com
IN NS ns2.domain.com
1 IN PTR localhost.domain.com.)
```

# 网络信息服务

网络信息服务 `NIS` 是一个简单的客户端/服务器数据库系统。该协议是通用的，可以用于任何地方。但在 Linux 下，它最常用的用途是跨网络共享密码文件和组文件。本节涵盖了主 NIS 和服务器 NIS 的设置，以及让客户端使用它们的配置。

# 简史

`NIS` 由太阳微系统公司 `Sun Microsystems` 作为其 `SunOS` 操作系统的一部分开发，最初被称为“黄页” `Yellow Pages`，简称 `YP`。遗憾的是，“黄页”这一名称已被注册了商标，随后的诉讼迫使该名称更改为 `NIS`。然而，你会发现所有的命令都以 `yp` 为前缀。

`NIS` 协议已经公开，其实现迅速扩展到其他 UNIX 变体中。Linux 从起初就支持 `NIS`。由于 Linux 遵循 `NIS` 标准，因此它可以作为 `NIS` 服务器或客户端与其它版本的 UNIX 配合使用。

最近，`NIS` 以 `NIS+` 的形式进行了更新。`NIS+` 解决了 `NIS` 的许多问题，最显著是在安全领域。然而，到此为止，Linux 通过 `NIS` 库对 `NIS+` 的支持还很弱。服务器支持尚未就绪，客户端软件也不完整。由于 `NIS+` 仍处于开发阶段，因此此处未对其进行介绍。

# 硬件连接与设备

## 第三部分

# 理解 NIS

当你配置网络时，你会发现你的某些配置文件并不是固定的，但它们需要频繁更新。`/etc/passwd` 和 `/etc/group` 是两个很快就会想到的文件。`NIS` 允许你建立一个存储文件的主服务器，并将网络上的每台机器配置为该客户端。当客户端需要从 `/etc/passwd` 文件获取条目时，它会调用 `NIS` 服务器。

为了让文件可以通过 `NIS` 共享，必须满足两个前提。首先，文件必须是表格形式，并且在整个文件中至少有一个字段是唯一的。在 `/etc/passwd` 文件中，该条目可以是登录名或 `UID`。其次，原始格式的文件必须是文本文件。

根据标准，这些文件被转换为 `DBM` 文件，这是一种快速搜索的简单数据库格式。需要为每个键创建一个单独的 `DBM` 以进行搜索。在 `/etc/passwd` 文件中，你需要能够通过登录名搜索的数据库。

# 硬件连接与设备

## 第三部分

大部分条目可以保持不变。你可能需要更改的少数项是 `GROUP`、`PASSWD`、`SHADOW`、`ALIAS` 以及可能的 `HOSTS`。

`GROUP` 行显示控制组信息的文件位于 `/etc/group`。你可能希望在服务器上保留本地组文件，而不是从你的 `NIS` 组文件同步，因为你的本地组文件可能包含某些你不希望在 `NIS` 中共享的服务器特定组组，例如用于你 Web 服务器的 `www` 组。

其他行的情况也是如此，特别是 `PASSWD` 行。你可能想要使用一个简单的约定来表示该文件在 `NIS` 中共享，只需以 `.yp` 结尾。生成的行如下所示：

```
PASSWD = $(PPWDDIR)/passwd.yp
```

设置好文件名后，你现在可以确定要发布哪些文件。向下滚动 `Makefile` 找到以下代码块：

```bash
# 如果你不想构建这些映射中的某些项，可以随意
# 从此列表中注释掉它们。
# 注意，我们默认不构建 ethers 或 bootmaps 映射
# 因为 /etc/ethers 和 /etc/bootmaps 在所有系统上可能都不存在
```

你的代码应该位于此处：

```
all: passwd hosts group netid protocols rpc services netgrp
tmail shadow ypsvers publicickey ethers # amd.home bootmaps
```

此行指定了将通过 `NIS` 提供哪些映射。`ethers` 之后的 `#` 符号是注释符号。`amd.home` 和 `bootmaps` 映射目前被注释掉了。
