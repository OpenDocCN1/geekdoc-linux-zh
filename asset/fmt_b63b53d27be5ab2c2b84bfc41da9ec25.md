
10.0.0.9       Sento failed: Permission denied

10.0.0.13      GURSTAR-ONE     <server> <unknown>  00:00:61:42:sb:bf

10.0.0.16       SERVER          <server> SERVER       00:00:00:00:00

10.0.0.255     Sento failed: Permission denied.

root@|knopsis]#

```
# 图 2.22 失败的 smb-nat 扫描
```

Session Edit View Bookmarks Settings Help

root@|knopsis]# smb-nat -10.0.0.0/13

* Checking host 10.0.0.13

* Getting list of remote NetBIOS names

* Remote systems tables:

  GURSTAR-ONE

  GURSTAR-ONE

  WORKGROUP

  WORKGROUP

  _MSBROWWER_

* Attending to connect with name: *

  Failed to connect

* Attending to connect with name: GURSTAR-ONE

* Attending to connect with protocol: MICROSOFT NETWORKS 1.03

  * Server The last of Nov 19 19:32:24 2005

  * Timeout in 15 seconds

* Failed to de-encrypt, telling it not to

* Attending to establish session:

* Attending to access share: \GURSTAR-ONE\

  Failed to access

  Segmentation fault

root@|knopsis]#

## 案例研究——工具的实战

好了，这里是这一切汇合的地方，工具与方法论的交汇点。我们将基于外部和内部渗透测试运行一系列场景，包括一个非常隐蔽的方法和一个高噪音的 IDS 测试。我们将这些场景视为渗透测试的初始轮次，并为每次任务提供一个范围。这些案例研究的目标是确定有关目标的信息，以便明智地进入漏洞利用阶段。IP 地址已被更改或混淆，以保护（无辜的）无辜者。

## 外部

外部攻击的目标是客户提供的单个地址。没有 IDS，但涉及了防火墙。目标 DNS 名称为 `alxogan.is-a-geek.org`。

第一步是执行 ping 查询和主机查询，以确保系统确实是目标。运行 `whois alxogan.is-a-geek.org` 返回 NOT FOUND，因此我们只对域名执行 `whois`，`whois.is-a-geek.org`。这返回了 DynDNS 的注册信息，这意味着目标可能是一个使用 DynDNS 作为外部可访问 DNS 名称的动态 IP 地址。这在 100% 的情况下都会使用。`dig alxogan.is-a-geek.org` 返回 IP 地址 `70.120.220.145`，即目标 IP 地址。对 `70.120.220.145` 进行反向查询得到一个与提供的不同的主机名，`70-120-220-145.houston.com` 是 RoadRunner（一家电缆 ISP）的域名，域名中的 `houston` 让我们认为该 IP 地址可能终止于德克萨斯州休斯顿。这现在可能没用，但关于目标的任何信息后续都可能有用。注意，此时已向目标发送了单个 ping，因此到目前为止的所有枚举都是完全。在图 2.23 中，我们运行 `nmap -sS -oA external-nmap alxogan.is-a-geek.org`，它执行 SYN 扫描和版本扫描，并将输出写入文件 `external-nmap`。该扫描返回三个开放的 TCP 端口——22、80 和 8080，6969 被过滤。

# 枚举与扫描

### 图 2.23 外部案例研究——nmap

![](img/2714962ecb7769011405633d4d1fc9_162.png)

为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41。

### 图 2.24 外部案例研究——nmap

![](img/2714962ecb7769011405633d4d1fc9_162.png)

为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。

。为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41。

### 图 2.25 外部案例研究——Nessus

![](img/2714962ecb7769011405633d4d1fc9_162.png)

为了识别那些开放端口在运行什么，运行了 `nmap`，显示端口 22 运行着 OpenSSH，80 运行着 Apache 2.4.41 (Ubuntu)，8080 运行着 Apache 2.4.41 (Ubuntu)，53 运行着 BIND 9.6.1，6969 被过滤。

### 图 2.26 外部案例研究——Nessus

![](img/2714962ecb7769011405633d4d1fc9_162.png)

### 图 2.27 外部案例研究——Nikto

![](img/2714962ecb7769011405633d4d1fc9_162.png)

136 第 2 章 • 扫描与枚举

### 图 2.28 外部案例研究——检测到 webmail

![](img/2714962ecb7769011405633c8d4d1fc9_166_0.png)

虽然我们还没有讨论 Nessus 和 wikto，本案例研究的目的是展示基础的外部扫描和枚举可以有多简单。将对每个发现的软件产品进行调查，以寻找已知漏洞，并对软件进行进一步测试以确定任何配置错误。

## 内部

对于内部案例研究，我们将扫描并枚举 `10.0.0.0/24` 网络。内部不存在网络防火墙，但安装了主机级防火墙。

使用 `nmap -iP -PS -oA internal-ping-sweep 10.0.0.0/24` 执行 ping 扫描发现了五个目标：`10.0.0.1`、`10.0.0.10`、`10.0.0.13`、`10.0.0.185` 和 `10.0.0.255`（最可能是广播地址）。还枚举了 DNS 名称 gw、server、gunstar-one 和 box。这如图 2.29 所示。

枚举与扫描 • 第 2 章 137

```
Session Edit View Bookmarks Settings Help

root@[knopp]# nmap -sP -PS -OA internal-ping-sweep 10.0.0.0/24

Starting map 3.75 (http://www.nmap.org/nmap/) at 2085-11-14 21:13:23 EST

Host gw.homelan.net is up.

MAC Address: 00:25:5E:79:58:BF (The Linksys Group)

Host server.homelan.net (10.0.0.10) is up.
```
