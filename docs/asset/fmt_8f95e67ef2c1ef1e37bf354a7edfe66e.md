
进入`/path/to/xxx`目录，找到`xxx.json`。

然后可以重新编辑并导入 `slapd.ldif`。请仅在没有其他解决方案时遵循此步骤。

这仅是服务器的配置。同一台机器也可以托管 LDAP 客户端，拥有其独立的配置。

## 30.6. 动态主机配置协议 (DHCP)

动态主机配置协议 `DHCP` 允许系统连接到网络以分配在网络上通信所需的地址信息。FreeBSD 包含了 OpenBSD 版本的客户端，用于客户端获取地址信息。FreeBSD 未安装 DHCP 服务器，但 FreeBSD Ports 中提供了多个服务器。DHCP 协议在 RFC 2131 中有详细描述。相关信息也可从 `isc.org/downloads/dhcp/` 获取。

### 配置 DHCP 客户端

本节介绍了如何使用内置的 DHCP 客户端。然后描述了如何安装和配置 DHCP 服务器。

注意

在 FreeBSD 中，DHCP 服务器和 DHCP 客户端都需要 `bpf(4)` 设备。该设备包含在随 FreeBSD 安装的 GENERIC 内核中。倾向于创建

如果使用了 DHCP，自定义内核需要保留此设备。

需要注意的是，`bpf` 也允许特权用户在该系统上运行网络数据包嗅探器。

## 30.6.1. 配置 DHCP 客户端

FreeBSD 安装程序包含了 DHCP 客户端支持，可以轻松配置新安装的系统自动从现有的 DHCP 服务器接收其网络地址信息。网络配置的示例请参考第 2.8 节“账户、时区、服务与加固”。

当在客户端机器上执行 `dhclient` 时，它开始广播配置信息的请求。

默认情况下，这些请求使用 UDP 端口 68。服务器在 UDP 端口 67 上进行响应，为客户端提供 IP 地址和其他相关的网络信息，如子网掩码、默认网关和 DNS 服务器地址。这些信息以 DHCP“租约”的形式存在，并有效期为可配置的时间。这允许不再连接到网络的客户端过期 IP 地址被自动重新使用。DHCP 客户端可以从服务器获取大量信息。详细列表可参见 `dhcp-options(5)`。

默认情况下，当 FreeBSD 系统启动时，其 DHCP 客户端会在后台运行或异步运行。其他启动脚本会在 DHCP 进程完成时继续运行，这加快了系统启动速度。

当 DHCP 服务器快速响应客户端请求时，后台 DHCP 工作良好。然而，在某些系统上，DHCP 可能需要很长时间才能完成。如果网络服务尝试 DHCP 分配网络地址信息之前尝试，它们将失败。使用同步模式下的 DHCP 可以防止此问题，因为它会暂停启动，直到 DHCP 配置完成。

`/etc/rc.conf` 中的此行用于配置后台或异步模式：

```
ifconfig_fxp0="DHCP"
```

如果系统在安装期间已配置为使用 DHCP，则此行可能已经存在。请按照第 12.5 节“设置网络接口卡”所述，将这些示例中的 `fxp0` 替换为要动态配置的接口名称。

若要配置系统使用同步模式，并在启动期间等待 DHCP 完成时暂停，请使用“SYNCDHCP”：

```
ifconfig_fxp0="SYNCDHCP"
```

还有额外的客户端选项。详情请在 `rc.conf(5)` 中搜索 `dhclient`。

DHCP 客户端使用以下文件：

- `/etc/dhclient.conf`
`dhclient` 使用的配置。通常，它只包含注释，因为默认值适用于大多数客户端。该配置在 `dhclient.conf(5)` 中描述。

- `/sbin/dhclient`
关于该命令本身的更多信息可以在 `dhclient(8)` 中找到。

- `/sbin/dhclient-script`
FreeBSD DHCP 客户端配置脚本。它在 `dhclient-script(8)` 中描述，但为了正常运行通常不需要任何用户修改。

- `/var/db/dhclient.leases.interface`
DHCP 客户端在此文件中保留有效租约的数据库，该文件以日志形式写入，并在 `dhclient-leases(5)` 中描述。

第 30 章. 网络服务器

## 30.6.2. 安装和配置 DHCP 服务器

本节演示了如何使用互联网系统协会（ISC）的 DHCP 服务器实现来配置 FreeBSD 系统充当 DHCP 服务器。该实现及其文档可以通过 `net/isc-dhcp43-server` 软件包或端口进行安装。

安装 `net/isc-dhcp43-server` 会安装一个示例配置文件。将 `/usr/local/etc/dhcpd.conf.example` 拷贝到 `/usr/local/etc/dhcpd.conf` 并对此新文件进行任何编辑。

该文件由子网和主机的声明组成，定义了提供给 DHCP 客户端的信息。例如，这些行配置了以下内容：

```
option domain-name "example.org";

option domain-name-servers ns1.example.org;

option subnet-mask 255.255.255.0;

default-lease-time 600;

max-lease-time 72400;

dns-update-style none;

subnet 10.254.239.0 netmask 255.255.255.224 {

  range 10.254.239.10 10.254.239.20;

  option routers rtr-239-1.example.org, rtr-239-2.example.org;

}
```

```
host fantasia {

  hardware ethernet 08:00:07:26:c0:a5;

  fixed-address fantasia.fugue.com;

}
```

此选项指定提供给客户端的默认搜索域名。更多信息请参考 `resolv.conf(5)`。

此选项指定客户端应使用的 DNS 服务器逗号分隔列表。它们可以通过其完全限定域名（FQDN）列出（如示例所示），可以通过 IP 地址列出。

提供给客户端的子网掩码。

默认租约过期时间（秒为单位）。可以配置客户端来覆盖此值。

租约的最大长度（秒为单位）。如果客户端请求更长的租约，仍会发放租约，但 `dns-update-style none` 会禁用动态 DNS。

指定此主机应始终被赋予相同的 IP 地址。使用主机名是正确的，因为 DHCP 服务器在返回租约之前会解析主机名。

指定客户端的硬件 MAC 地址，以便 DHCP 服务器在客户端发出请求时识别它。

此行创建一个留供分配的可用 IP 地址池。子网必须在上一行指定。

## 30.7. 域名系统 (DNS)

域名系统（DNS）是用于域名映射到 IP 地址以及反之的协议。DNS 通过一套复杂的根、顶级域名（TLD）和其他规模名称服务器在互联网上进行协调，这些服务器托管并缓存单个域名信息。在系统中不需要运行名称服务器即可执行 DNS 查询。

下表描述了与 DNS 相关的一些术语：

表 30.4 DNS 术语

| 术语 | 定义 |
| --- | --- |
| 正向 DNS | 主机名到 IP 地址的映射。 |
| 反向 DNS | IP 地址到主机名的映射。 |

DHCP 服务器使用以下内容。注意手册随软件一起安装。

- `/usr/local/etc/dhcpd.conf`
服务器配置需要包含提供给客户端的所有信息，以及有关服务器运行的信息。该配置见 `dhcpd.conf(5)`。

- `/var/db/dhcpd.leases`
DHCP 服务器在此文件中保留已发行租约的数据库，该文件以日志形式写入。参考 `dhcpd-leases(5)`，它提供了稍详细的描述。

- `/usr/local/sbin/dhcrelay`
此守护进程用于高级环境，其中一个 DHCP 服务器将客户端的请求转发到位于不同网络的另一个 DHCP 服务器。如果需要此功能，请安装 `net/isc-dhcp43-relay` 软件包或端口。安装包含了 `dhcrelay(8)`，它提供了更多细节。

一旦完成 `dhcpd.conf` 配置，在 `/etc/rc.conf` 中启用 DHCP 服务器：

```
dhcpd_enable="YES"
```

```
dhcpd_ifaces="dc0"
```

将 `dc0` 替换为 DHCP 服务器应该监听 DHCP 请求的接口（或接口，用空格分隔）。

通过执行以下命令启动服务器：

```
# service isc-dhcpd start
```

对配置的任何更改都要求使用 `service(8)` 停止并重新启动 `dhcpd` 服务。

# 第 30 章 网络服务器

| 术语 | 定义 |
| :--- | :--- |
| 解析器 (Resolver) | 机器通过其查询服务器获取区域信息的系统进程。 |
| 反向 DNS (Reverse DNS) | IP 地址到主机名的映射。 |
| 根区域 (Root zone) | 互联网区域层次结构的起点。所有区域都位于根区域之下，类似于文件中的所有文件都位于根目录下。 |
| 区域 (Zone) | 由同一实体管理的单个域名、子域名或 DNS 部分。 |

区域的示例：
- `.` 是文档中通常对根区域的称呼。
- `.org.` 是根区域下的一个顶级域名 (TLD)。
- `.example.org.` 是 org. 顶级域名下的一个区域。
- `1.168.192.in-addr.arpa` 是一个引用所有属于 `192.168.1.*` IP 地址空间的区域。

众所周知，主机名越具体的部分越靠左侧。例如，`example.org.` 比 `org.` 更具体，而 `org.` 比根区域更具体。主机名每个部分的布局非常像系统：`/dev` 目录位于根目录下，以此此类推。

## 30.7.1. 运行名称服务器 true

名称服务器通常有两种形式：权威名称服务器（authoritative name servers）和缓存名称服务器（也称为解析名称服务器）。

在以下情况下需要权威名称服务器：
- 某想要向世界提供 DNS 信息，对查询做出权威答复。
- 注册了域名（例如 `example.org`），并需要为其下的主机名分配 IP 地址。
- IP 地址块需要反向 DNS 词目（IP 到主机名）。
- 需要一个备份或第二个名称服务器（称为从服务器 slave）来响应查询。

在以下情况下需要缓存名称服务器：
- 本地 DNS 服务器可以缓存并响应，速度比查询外部名称服务器更快。

当用户查询 `www.FreeBSD.org` 时，解析器通常会查询上游 ISP 的名称服务器并获取回复。通过本地缓存 DNS 服务器，缓存 DNS 服务器仅需向外部世界发起一次查询。由于信息已在本地缓存，额外的查询将无需离开本地网络。

## 30.7.2. DNS 服务器配置

FreeBSD 基础系统中提供了 Unbound。默认情况下，它仅为本地机器提供 DNS 解析。虽然基础系统包可以配置为提供本地机器之外的解析服务，但建议通过 FreeBSD Ports Collection 安装 Unbound 来满足此类需求。

要启用 Unbound，请向 `/etc/rc.conf` 中添加以下内容：

```
local_unbound_enable="YES"
```

`/etc/resolv.conf` 中的任何现有名称服务器将在新的 Unbound 配置中被配置为转发器 (forwarders)。

注意
如果列出的名称服务器中任何一个不支持 DNSSEC，本地 DNS 解析将失败。请确保测试每个名称服务器并移除任何测试失败的。以下命令将显示运行在 `192.168.1.1` 上的名称服务器的信任树或失败情况：

```bash
% drill -S FreeBSD.org @ 192.168.1.1
```

确认每个名称服务器都支持 DNSSEC 后，启动 Unbound：

```bash
# service local_unbound start
```

这将处理 `/etc/resolv.conf`，使得对 DNSSEC 安全域名的查询能够正常工作。例如，运行以下命令来验证 `FreeBSD.org` 的 DNSSEC 信任树：

```bash
% drill -S FreeBSD.org
```

```
;; Number of trusted keys: 1
```

```
;; Chasing freebsd.org. A
```

DNSSEC 信任树：
`freebsd.org.` (A)

```text
|---freebsd.org. (DNSKEY keytag: 36786 alg: 8 flags: 256)
|---freebsd.org. (DNSKEY keytag: 32659 alg: 8 flags: 257)
|---freebsd.org. (DS keytag: 32659 digest type: 2)
|---org.org. (DNSKEY keytag: 49587 alg: 7 flags: 256)
|---org.org. (DNSKEY keytag: 9795 alg: 7 flags: 257)
|---org.org. (DNSKEY keytag: 21366 alg: 7 flags: 256)
|---org.org. (DS keytag: 21366 digest type: 1)
```

对于每个虚拟主机，将 `ServerName` 和 `DocumentRoot` 的值替换为要使用的值。

有关设置虚拟主机的更多信息，请参考 Apache 官方文档：`http://httppd.apache.org/docs/vhosts/`。

## 30.8.3 Apache 模块

Apache 使用模块来增强基础服务器提供的功能。请参考 `http://httpd.apache.org/docs/current/mod/` 获取可用模块配置详情的完整列表。

在 FreeBSD 中，某些模块可以通过 `www/apache24` 端口进行编译。在 `/usr/ports/www/apache24` 中输入 `make config` 以查看哪些模块是可选以及哪些是默认启用的。如果该模块没有通过端口编译，FreeBSD Ports Collection 了一了一种安装许多模块的简单方法。本节描述了三个最常用的模块。

### 30.8.3.1. SSL 支持

在过去的某个时期，Apache 内部对 SSL 支持需要一个名为 `mod_ssl` 的二级模块。现在已不再如此，Apache 的默认安装版本已经在 Web 服务器中内置了 SSL。有关如何启用 SSL 网站支持的示例可以在已安装的文件找到，位于 `/usr/local/etc/apache24/extra` 目录下的 `httpd-ssl.conf`。该目录下还有一个同名为 `ssl.conf` 的示例文件。建议评估这两个文件，以便在 Apache Web 服务器中正确设置安全网站。

SSL 配置完成后，必须取消主 `httpd.conf` 中下述行的注释，以便在下一次重启或重载 Apache 时激活更改：

```
#Include etc/apache24/extra/httpd-ssl.conf
```

## 警告

SSL 版本二和版本三存在已知的漏洞问题。强烈建议启用 TLS 1.2 和 1.3 版本代替旧的 SSL 选项。这可以通过 `ssl.conf` 中设置以下选项来实现：

```
SSLProtocol all -SSLv3 +TLSv1.2 +TLSv1.3
```

```
SSLProxyProtocol all -SSLv2 -SSLv3 -TLSv1 -TLSv1.1
```

要完成 Web 服务器的 SSL 配置，取消以下行的注释，以确保配置在重启或重载期间被加载到 Apache：

```
# Secure (SSL/TLS) connections
```

```
Include etc/apache24/extra/httpd-ssl.conf
```

为了在 Apache 中完全支持 SSL，必须在 `httpd.conf` 中取消以下行的注释：

```
LoadModule authn_socache_module
libexec/apache24/mod_authn_socache.so
```

```
LoadModule socache_shmcb_module
libexec/apache24/mod_socache_shmcb.so
```

```
LoadModule ssl_module libexec/apache-24/mod_ssl.so
```

下一步是与证书机构合作，在系统中安装相应的证书。这将为站点建立信任链，并防止任何自签名证书的警告。

588

# 第 30 章 网络服务器

### 30.8.3.2. mod_perl

`mod_perl` 使得使用 Perl Apache 模块成为可能。此外，嵌入服务器的持久解释器避免了启动外部解释器的开销以及 Perl 启动时间的惩罚。

可以使用 `www/mod_perl2` 软件包或端口安装 `mod_perl`。使用此模块的文档可以在 `http://perl.apache.org/docs/2.0/index.html` 找到。

### 30.8.3.3. mod_php

由 Tom Rhodes 编写。

PHP：超文本预处理器（PHP）是一种通用的脚本语言，特别适用于 Web 开发。它能够嵌入到 HTML 中，其语法借鉴了 C、Java™ 和 Perl，旨在允许 Web 开发人员快速编写动态生成的网页。

通过安装相应的端口，可以添加对 Apache PHP 支持以及该语言编写的任何其他功能。

对于所有支持的版本，使用 `pkg` 搜索软件包数据库：

```
# pkg search php
```

将显示一个列表，包括版本及其提供的额外功能。这些组件是完全模块化的，这意味着通过安装相应的端口即可启用功能。要为 Apache 安装 PHP 7.4 版本，请执行以下命令：

```
# pkg install mod_php74
```
