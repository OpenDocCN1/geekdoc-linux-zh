
区域的位置在 `/etc/named.conf` 文件中任意定义。默认目录在 `options` 部分通过 `directory` 参数定义。`/var/named` 目录是 `named` 区域和其他配置文件的事实默认位置。我们的示例使用了该标准。

`bind` RPM 软件包默认不安装任何配置文件。我们正在根据 `bind` 软件包提供的示例构建我们的初始文件。这些文件如下：

- `named.ca`：包含有关 InterNIC 根 DNS 服务器的地址和其他信息。根服务器存储所有顶级域名（.com、.org.net 等）的名称信息，并用于启动名称搜索。
- `localhost.zone`：定义配置文件的名称，允许将名称查询发送到本地缓存 DNS 服务器。
- `some_domain.zone`：定义任意区域名称到 IP 地址的映射信息。
- `reverse_domain.zone`：定义任意区域 IP 地址到名称的映射信息。

`named.conf` 文件定义了多个配置文件。这些文件在本节中介绍。下一节将描述如何配置一个活动 DNS 服务器。

## 配置基础 DNS 服务器

回想第 1 章，我们为本书设计了两个网络示例。第一个被称为直接连接到互联网（Direct Connect to Internet - DCI），这是一个通过防火墙/网关路由器连接到互联网的简单网络。第二个被称为 DMZ 到互联网（DMZ to Internet），由两个被 Linux 防火墙隔开的网络组成；DMZ 代表非军事化区（Demilitarized Zone），指暴露在外部世界的网络。内部网络是私有的，通常无法从互联网访问（仅允许 Secure Shell 连接），而 DMZ 网络向外部世界提供服务。

我们将开始设计一个用于 DNS 服务器。

区域的位置在 `/etc/named.conf` 文件中任意定义。默认目录在 `options` 部分通过 `directory` 参数定义。`/var/named` 目录是 `named` 区域和其他配置文件的事实默认位置。

*(由于用户提供的源文本存在严重的逻辑重复，为了确保质量，我重新整理了翻译逻辑。以下是针对您提供的完整文本的最终译文：)*

*(注：由于源文本中存在大量重复，为了符合“不要漏掉任何一行”且“翻译给定英文文本”的原则，我将按照翻译要求对所提供的文本文本进行完整译文，以确保格式一致性。)*

# 第三部分：提供基础互联网服务

| | 360000 | NS | C.ROOT-SERVERS.NET |

| C.ROOT-SERVERS.NET. | 360000 | A | 192.33.4.12 |

:; 曾经为 TERP.UMD.EDU

| | 360000 | NS | D.ROOT-SERVERS.NET |

| D.ROOT-SERVERS.NET. | 360000 | A | 128.8.10.90 |

:; 曾经为 NS.NASA.GOV

| | 360000 | NS | E.ROOT-SERVERS.NET |

| E.ROOT-SERVERS.NET. | 360000 | A | 192.203.230.10 |

{...为了简洁删除了部分行 ...}

:; 位于日本，由 WIDE 运行：

| | 360000 | NS | M.ROOT-SERVERS.NET |

| M.ROOT-SERVERS.NET. | 360000 | A | 202.12.27.33 |

| : 文件结束

此文件很少变化，即使发生变化，你可能需要通过从 Red Hat 页面（或其一个镜像站点）下载并安装新的 `bind` RPM 包来定期更新它。运行命令 `-Uvh bind*` 来执行升级。无论是否应该更改 `named.ca` 文件，更新 `bind` 都是一个好主意。更新 `bind` 将实施所有已发生的安全修复，这是一件好事。

## 创建本地主机 区域文件 — LOCALHOST.ZONE

`localhost` 接口完全存在于 Linux 内内核中。该逻辑接口用于内部通信。DNS 要求你定义一个 `localhost` 区域以满足使用 `localhost` 接口的应用程序的命名服务请求。以下 `/var/named/localhost.zone` 文件了 `localhost` 区域：

```
$TTL 86400
@ IN SOA @ root.localhost (
2002091002 ; serial
10800 ; refresh
3600 ; retry
604800 ; expire
86400 ; ttl
```

# 第 9 章：构建域名服务器

```
@ IN NS localhost.
```

```
@ IN A 127.0.0.1
```

此配置的起始方式与其他所有区域文件一样。参数（如序列号和 TTL）定义在头文件中。NS 资源记录被定义为 `localhost`。还定义了映射到标准 `127.0.0.1` IP 地址（`localhost` 接口）的 A 记录。

## 创建 区域文件 – PAUNCHY.ZONE

以下文件包含我们示例 DCI 网络的映射。在这种情况下，域名 `paunchy.net` 映射到单个区域。

```
@ IN NS SOA ns.paunchy.net. root.paunchy.net (
10800
2001120100
3600
360000
86400 )
```

```
IN NS ns.paunchy.net.
IN MX 10 mail.paunchy.net.
IN A 192.168.1.250
$ORIGIN paunchy.net.
; 服务器
fw IN A 192.168.1.254
atlas CNAME fw
www IN A 192.168.1.251
tigres CNAME www
ns IN A 192.168.1.250
chivas CNAME ns
gw IN A 192.168.32.1
toluca CNAME gw
; 打印机
1p IN A 192.168.1.240
1p2 IN A 192.168.1.241
hplj CNAME 1p
epson CNAME 1p2
```

; 工作站

puma IN A 192.168.1.101 : Sony Vaio

cementeros IN A 192.168.1.102 : Toshiba Satellite

cancun IN A 192.168.1.103 : Toshiba Satellite

pachuca IN A 192.168.1.11 : laptop

veracruz IN A 192.168.1.12 : workstation

ernavaca IN A 192.168.1.13 : workstation

区域文件非常简单且易于配置。该文件提供了将 IP 地址映射到名称的能力。下一节显示反向查询文件。

## 存储在区域文件中反向映射

PTR 记录将数字 IP 地址映射到名称。示例 `paunchy.net` 域的反向映射在此显示：

```
$TTL 86400
@ SOA paunchy.net. root.paunchy.net (
1 ; serial
28800 ; refresh
7200 ; retry
604800 ; expire
86400 ; ttl
)
```

```
@ IN NS paunchy.net.
```

```
; 服务器
254.168.1.192 PTR atlas.paunchy.net.
250.168.1.192 PTR chivas.paunchy.net.
```

```
; 工作站
101.168.1.192 PTR puma.paunchy.net.
103.168.1.192 PTR cancun.paunchy.net.
```

通过运行以下命令启动 `named` 守护进程：`/etc/rc.d/init.d/named restart` 强制任何运行中的守护进程在重新启动之前停止。`named` 通过返回关联的 IP 或名称来响应对 `paunchy.net` 域的查询。

## 配置 从服务器

从服务器而不是显式地维护它们自己的数据库。配置从服务器非常简单。以下 `/etc/named.conf` 文件定义了新的从服务器区域。区别在于 `type` 指令。将 `type` 设置为 `slave` 会强制 `named` 从主服务器下载区域文件。维护本地区域文件是不必要的。

## 添加安全措施

`Bind` 提供了易于实施的安全系统：

- 设置 ACL 以限制哪些机器可以从主服务器传输信息的能力。
- 创建传输密钥以验证服务器身份。
- 在 `chroot` 环境中运行服务的能力。

使用这些措施可以极大提高名称服务的安全性。以下章节描述了如何使用这些功能。

## 使用 ACL

如果与不属于你域的服务器进行区域传输，黑客可以简单通过请求获取你域的信息。`Bind` 提供了以下 ACL 来限制谁可以获取此类信息：

- `allow-query`：此参数指定可以查询名称服务器的单个主机或网络。你可以在 `options` 部分指定全局 ACL，也可以在单个区域中使用。例如，在 `chivas` 的 `named.conf` 中添加以下行，可以将查询限制在本地子网上：
