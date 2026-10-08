
其中 "`mydomain.com`" 是网关，“`@domain.com`” 是电子邮件地址。

## 测试 SquidGuard
好了，你的 SquidGuard 程序正在运行，你看到它工作正常，但等一下；通过将所有的过滤器文件转换为数据库文件，可以让 SquidGuard 运行得更快。

- 1. 首先，我们将连接合法网站。我们应该收到一个请求密码的新窗口。
- 2. 现在我们将尝试访问被屏蔽的网站。例如尝试 `www.warez.com`。

> 注意：如果你在这里收到错误消息，可能是因为你忘记了配置 squidguard 程序。请编辑 "`/http/cgi-bin/squidguard`"。

## 优化 SquidGuard
本节专门讨论为了提高和紧固 SquidGuard 的可以采取的措施。注意我们仅参考内置的功能。

## 创建预构建数据库
SquidGuard 使用的默认过滤器是纯文本，SquidGuard 需要解析过滤器文件中所有的行来决定域名/URL 是否允许。有一种更好的方法，通过将其所有过滤器文件转换为数据库文件可以获得相同的结果并运行更快。

### 步骤 1
完成此转换的第一步是使用 SquidGuard 的 "`-C`" 命令。该命令将文本文件转换为数据库文件。

- 使用以下命令将你的文本文件转换为数据库文件：
```
[root@deep]# cd /var/pool/squid/squidguard/
[root@deep]# SquidGuard -c aggressive/domains
[root@deep]# SquidGuard -c aggressive/urls
[root@deep]# SquidGuard -c gambling/domains
[root@deep]# SquidGuard -c gambling/urls
[root@deep]# SquidGuard -c hacking/domains
[root@deep]# SquidGuard -c hacking/urls
[root@deep]# SquidGuard -c porn/domains
[root@deep]# SquidGuard -c porn/urls
```
上述命令将域名列表或 URL 列表从纯文本转换为预构建数据库。

## SquidGuard 第 2 章

注意：有一个文件不能也不应该转换为 db 文件。该过滤器文件是位于 "`porn`" 目录下的 "`expressions`" 文件。

## 第 2 步

一旦我们完成了所有过滤文件的转换，我们就必须编辑 `squid.conf` 文件，更改我们过滤文件的默认扩展名以反映这些更改。**粗体文本**是我们在 Squid 配置文件中修改的部分。

+ 编辑 `squid.conf` 文件 (`vi /etc/squid/squid.conf`) 并修改以下行，使 Squid 一次性加载并解释整个文件。

```
dbhome /var/pool/squid/squidGuard

logdir /var/log/squid/squidGuard

# 时间空间声明

# 下列声明定义了一个时间规则，客户端允许在该时间段

# 内访问互联网。在此时间之外，连接

# 将被拒绝。

time workhours {

  weekly mtwhf 08:30 - 17:30

}
```

```
# 源组声明

# 下列声明定义了一个源组，或客户端组 IP

# 地址范围，允许通过代理访问

的。
```

```
src internal {

  ip 192.168.1.0/24

}
```

```
# 目标组声明

# 下列声明定义了目标组，或目标组

# 禁止连接的网站。
```

```
dest aggressive {

  domainlist aggressive/domains.db

  urllist aggressive/urls.db

}
```

```
dest gambling {

  domainlist gambling/domains.db

  urllist gambling/urls.db

}
```

```
dest hacking {

  domainlist hacking/domains.db

  urllist hacking/urls.db

}
```

```
dest porn {

  domainlist porn/domains.db

  urllist porn/urls.db

  expressionlist porn/expressions

}
```

## 重写规则组声明

## 访问控制列表

# 访问控制列表 (ACL) 将之前的定义组合成
# 针对每个客户端组的独立规则集。

```
acl {

    internal within workhours {

        pass |aggressive !gambling !hacking !porn all

    }

    default {

        pass none

        redirect http://my.proxy.com/cgi-bin/squidGuard.cgi?clientaddr=%a&clientname=%n&clientuser=%i&clientgroup=%s&targetgroup=%t&url=%u

    }

}
```

## 第 3 步

最后，我们必须重启 Squid 代理服务器使更改生效。

## 第 13 章

## FreeS/WAN VPN

本章内容

- 1. 编译 - 优化与安装 FreeS/WAN
- 2. 配置 FreeS/WAN
- 3. 配置 RSA 私钥密钥
- 4. IPSec 的网络设置
- 5. 测试 FreeS/WAN 安装

## SquidGuard | 1
第 2 章

### 摘要

首先，我想提到的是，关于 FreeSWAN 的这一章节是不受支持的章节。这是因为 FreeSWAN 是一个非常特殊的软件，通常需要特定的内核版本才能在系统上运行。由于内核版本的更新频繁且频率快于 FreeSWAN 版本的更新，因此无法保证你在阅读本章时使用的内核版本会与 FreeSWAN 兼容。此外，FreeSWAN 并不是互联网上所有人使用或为了使其服务器正常运行而使用的软件。

通常，只有对网络有特殊需求的专家和公司才需要安装和使用它。出于考虑，我决定不再在此书中提供关于 FreeSwan 的高级信息，但由于你们许多人非常需要，我将提供一些如何在 Linux 下编译、配置和运行它的信息。与本书其他章节不同，无法保证提供的信息一定适用于你的系统。如果你在让 FreeSwan 运行方面遇到问题，请向 FreeSwan 组寻求帮助。现在这里是关于 FreeSwan 的一些基本设置信息。

使用 POP 进行客户端到服务器及反向保护、使用 SSL 进行远程登录以及 SSL 解决方案是非常极的选择，但有时对于建立安全通信通道的环境来说，确保网关机、路由器或防火墙系统在互联网上之间完全的隐私性、真实性和数据完整性至关重要。为此，IPSEC 诞生了。

IPsec 协议安全。它利用密码学同时提供身份验证和加密服务。身份验证确保数据包来自正确的发送者且在传输过程中未被篡改。加密防止未经授权读取数据包内容。IPSEC 可以保护 IP 之上的任何协议以及 IP 之下的任何介质。

### IPSEC 还可以在“后台”提供一些安全服务，对用户没有可见的影响。更确点说，它可以保护运行在复杂介质组合（例如 IMAP/POP 等）之上的混合协议，而无需对它们进行任何更改，因为加密发生在 IP 级别。

FreeSWAN 使用了三种协议来实现这一结果：

- 1. AH（身份验证头）提供数据包层面的身份验证服务。
- 2. ESP（封装安全载荷）提供加密加身份验证。
- 3. IKE（互联网密钥交换）协商连接参数。

FreeSWAN 的实现包含三个部分：

- 1. KLIPS（内核 IPsec）在内核中实现 AH、ESP 和数据包处理。
- 2. Pluto（一个 ike 守护进程）实现 IKE，与其他协商连接。
- 3. 各种脚本提供接口。

IPsec 允许通过互联网建立隧道。

## 编译 - 优化与安装 FreeS/WAN

以下是你编译和优化 Free/WAN 必须执行的必要步骤。

## 第 1 步

IPSec 的安装需要对原始内核进行一些修改，因为 Free/WAN 的某些部分必须包含并整合到内核中。安装 Free/WAN 的第一步是进入本书的内核章节并按照说明操作。

### 第 2 步

一旦配置了内核并从软件处下载了 Free/WAN 程序，你必须在解压缩之前将其复制到 `/usr/src` 目录并切换到该位置。在 `/usr/src/linux` 下补丁 Free/WAN 会导致链接混乱，因此，请在 `/usr/src` 下扩展软件，而不是在 `/usr/src/linux` 下。

### 第 3 步

之后，进入新创建的 Free/WAN 目录，然后进行配置、编译和优化。

### 第 4 步

你必须修改 `Makefile.inc` 以以指定安装路径和优化参数。我们必须修改此文件以符合 Linux 文件系统结构，针对特定的处理器架构添加优化参数，并将 Free/WAN 文件安装到你的 PATH 环境变量下。

# FreeS/WAN VPN | 1
第 3 章

`MANTREE=$(DESTDIR)/usr/local/man`

读取：

```
USERCOMPILE=-O2
```

```
CONFDIR=$(DESTDIR)/etc
```

读取：

```
KLIPSCOMPILE=-O2
```

上述所有更改将所有与 FreeS/WAN 软件相关的文件移动到我们选择的目标目标目录。我们还添加了与系统中所用处理器类型相关的优化参数，以获得更好的性能。

### 第 5 步
一旦按照第 4 步所述对 FreeS/WAN 完成了修改，我们需要补丁 Linux 内核（Linux Kernel）以包含对 FreeS/WAN 的支持。

- 此过程可以通过以下命令完成：
```bash
[root@deep freeswan-1.95] # make all
echo "====================" >>out.kpatch
echo "date > /usr/src/linux ; pwd" >>out.kpatch
make _patches2.3 >>out.kpatch
```

`make all` 命令用于补丁内核。它将自动启动第二次内核配置，并允许你在完成并将其组件集成到内核之前回答任何内核配置。

在内核配置期间，确保你的内核在构建时已启用 FreeS/WAN 支持。按照上述方法用 FreeS/WAN 程序补丁内核后，你的内核配置中会出现一个与 FreeS/WAN 支持的 IPSec 选项相关的新章节。确保你在新内核下对以下问题选择了 Y：IPSec options (FreeS/WAN)。

- * IP 安全性协议 (FreeS/WAN IPSec) (CONFIG_IPSEC) [Y/n]
- * IPSec: IN-IP 封装（隧道模式） (CONFIG_IPSEC_IPIP) [Y/n]
- * IPSec: 身份验证头 (CONFIG_IPSEC_AH) [Y/n]
- * HMAC-MD5 认证算法 (CONFIG_IPSEC_AUTH_HMAC_MD5) [Y/n]
- * HMAC-SHA1 认证算法 (CONFIG_IPSEC_AUTH_HMAC_SHA1) [Y/n]
- * IPSec: 安全载荷封装 (CONFIG_IPSEC_ESP) [Y/n]
- * 3DES 加密算法 (CONFIG_IPSEC_3DES) [Y/n]
- * IPSec: IP 压缩 (CONFIG_IPSEC_COMP) [Y/n]
- * IPSec 调试选项 (CONFIG_IPSEC_DEBUG) [Y/n]

注意：所有对内核的自定义在你第一次运行 `make config`、`make dep` 和 `make clean` 命令时会被保留，因此你不需要重新配置内核的每个部分；只需使用 FreeS/WAN 添加的名为 IPSec options (FreeS/WAN) 的新章节即可，如上所示。

某些网络选项会自动开启，即使你之前关闭了它们；这是因为 IPSEC 需要解决几个问题：无论你使用哪个程序，都应该仔细注意以下几个问题：特别是，要在内核配置的 *Networking Options* 下禁用任何以下项：

```
Kernel/User netlink socket (CONFIG_NETLINK) [Y/n]?
Netlink 设备仿真 (CONFIG_NETLINK_DEV) [Y/n]?
```

### 第 6 步
一旦完成 `make` 命令，你的 FreeS/WAN 软件和带有 FreeS/WAN 支持的 Linux 内核就准备好安装到服务器上了。在安装软件和内核之前，我们在系统中列出文件列表，之后再列出一个，然后使用 `diff` 工具进行比较，找出文件放置的位置，最后在你的服务器上安装 FreeS/WAN 和带有 FreeS/WAN 支持的新内核：

```bash
[root@deep freeswan-1.95]# cd
[root@deep] find * > Freeswan
[root@deep] cd /usr/src/freeswan-1.95/
[root@deep freeswan-1.95]# make install
[root@deep freeswan-1.95]# cd
[root@deep] find * > Freeswan2
[root@deep] diff Freeswan Freeswan2 > Freeswan-Installed
```

`make install` 命令将所有 FreeS/WAN 和内核组件一起安装到服务器适当的位置。

### 第 7 步
在 FreeS/WAN 安装的此阶段，你必须按照书中 Linux 内核章节的说明规则正常安装内核。此时，在你构建并安装了新内核镜像、system.map 或模块（如有必要），并设置了 lilo 加载新内核后，你必须在重启系统之前编辑并自定义与 FreeS/WAN 相关的配置文件 "`ipsec.conf`" 和 "`ipsec.secrets`"。

### 第 8 步
一旦完成软件的编译、优化和安装，你可以删除不再需要的程序 tar 包档和相关的源码目录来释放一些磁盘空间。

- 要删除 FreeS/WAN 及其源码目录，请使用以下命令：
```bash
[root@deep /]# cd /usr/src/
[root@deep src]# rm -rf freeswan-version/
[root@deep src]# rm -f freeswan-version.tar.gz
```

# 配置 FreeS/WAN

构建 FreeS/WAN 后，你的下一步是验证或根据需要更改 FreeS/WAN 配置中的选项。这些是：

- `/etc/ipsec.conf` (FreeS/WAN 配置)
- `/etc/ipsec.secrets` (FreeS/WAN 密钥)

`/etc/ipsec.conf` 文件允许你配置 IPSec 参数。例如：

```
# 基本配置

config setup

  interfaces="ipsec0-eth0"

klipsdebug=none

  plutebug=none

  plutoload=%search

  plutostart=%search

# 示例连接

conn deep-mail

  left=208.164.188.1

  leftsubnet=192.168.1.0/24

  leftnextop=205.151.222.250

  right=208.164.186.2

  rightsubnet=192.168.1.0/24

  rightnextop=205.151.222.251

  keyingries=0

  auth=ah

  auto=start
```

这告诉 ipsec.conf `ipsec0-eth0` 为此特定配置设置。默认设置 `interfaces=%defaultroute` 将寻找默认互联网连接或公司网络。你也可以指定一个或多个特定接口。例如：

```
interfaces="ipsec0-eth0"
interfaces="ipsec0-eth0 ipsec1-ppp0"
```
