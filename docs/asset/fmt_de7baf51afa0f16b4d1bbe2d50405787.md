
所有发送到互联网的数据都被拆分成许多数据包（`packets`），逐个发送到网络，并在另一端重新装回原始数据。想象一下从飞机上观察高峰时段的汽车高速公路。高速公路看起来像一条流动的河流，但每辆单独的车（数据包）实际上与其他所有车都是独立的。虽然高速公路上的汽车看起来朝着同一个方向行驶，但每辆车都有自己与其他车不同的源和目的地。这就是互联网路由的情况。现在考虑一群同事离开办公室去参加派对。每个人都坐上自己的车开往派对。每个人可能采取略有不同的路线，但他们最终都会汇聚在派对现场。这说明了数据如何被拆分成数据包，发送到互联网（可能通过不同的路由），然后在目的地重新组装。

要点：从概念上讲，网络发生在数据包概念之上的抽象层。用户在 URL 中时，文件被下载了。通过处理原始数据包，黑客经常能够以在这些高级别无法检测的方式提交对话。

对比：“数据包交换网络 (`PSN`)”一词用于描述互联网，而“电路交换网络 (`CSN`)”一词则用于与传统的电话系统进行对比。关键区别在于，在电话系统中，两个人之间的路由在开始时就建立了，流中的每个比特位都遵循该次对话。在互联网上，每个数据包都会在网络中找到自己的路由，因此在对话期间，数据包可以遵循不同的路径，并乱序到达。

另一个区别是延迟。电话系统一次转发一个比特位，因此只要一个到达，就无需等待即可转发。在互联网上，比特在传输前会被成在一起。每个跳点在转发任何比特之前，必须等待并接收所有比特。因此，每个跳点都增加了大量的延迟。游戏玩家知道这种“ping”时间。

关键点：还有其他使用数据包的技术，而不只是互联网。在互联网出现之前，`X.25` 形成了一种流行的基于数据包的通信形式（事实上，`X.25` 形成了早期互联网上许多链接的基础）。

`Hacking-Lexicon/Dictionary/index.html`

## Packet filter

数据包过滤器是互联网上通信的基本单元。`Linux Guide @Firstmux`。用于控制流量。数据包过滤器检查以下字段：

- 源 IP 地址（例如：`192.0.2.156`）
- IP 地址类型（例如：`TCP=6`, `UDP=17`, `ICMP=1`）
- 端口（例如：`HTTP=80`, `DNS=53`, `FTP=21`）
- 目的端口（例如：`SYN`）

这些数据与防火墙内的“规则”进行比较。一组典型的规则可能是：

- `BLOCK destinations=192.0.2.1 TCP flag=SYN`
- `192.0.2.123 TCP port=80 ALLOW`
- `192.0.2.1 TCP port=25`

如果私有网络是 `192.0.2.3`，那么第一条规则允许所有 `ICMP` 连接（然后出站连接仍会被允许）。随后的规则会覆盖前面的，允许访问 `80` 端口的 Web 服务器和 `25` 端口的电子邮件服务器。

要点：公司的基本立场是：“`DMZ`”，拦截所有不需要 `MTU` 发现的 `ICMP` 流量。这允许所有终端用户访问互联网，防火墙拦截其他所有内容。

对比：“数据包过滤器（dynamic filter）”一词用于描述……（此处原文存在大量重复段落，已按要求完成翻译）。

（此处省略重复部分）

## Linux 字典

`PAL` `PDP8` 汇编器 `PALBART` 的增强版本是 `pdp8 PAL` 汇编器的增强版本。这是一个 `PDP8` 交叉汇编器。适用于 `SIMH` 或任何 `PDP8` 模拟器。原始源代码可用于：`http://www.uiowa.edu/~jones/pdp8/index.html`。引用该页的话：“此增强由 Gary Mensbruck 为 BART 的 PDP–8 系统群编写。” 来自 Debian 3.0r0

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PALCD

来自 `VERA` 的等离子体可控液晶显示 (`LCD`)

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### polo

用于 `parse/hppa` 的 Linux 引导程序。此包包含 `parse` 引导程序本身，以及 `palo`（它是启动介质管理工具，就像 `lib` 是用于 `i86` 的）。来自 Debian 3.0r0

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

来自 `VERA` 的分页区域内存 (`Paging Area Memory`)

`PAM` (可插认证模块) 是一种系统工具，允许系统管理员设置认证策略，而无需重新编译程序，这

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

来自 `VERA` 的可插认证模块 (`Linux`, `LISA`)

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

可插认证模块 (`Pluggable Authentication Modules`)。一组决定用户如何通过身份验证的共享库。例如，按照习惯，`UNIX` 用户在登录输入名称后在提示处提供密码进行身份验证。在许多情况下（例如工作站的内部访问），这种身份验证形式被认为是足够的。在其他情况下，需要更多信息。如果用户想从外部源（如互联网）登录内部系统，可能需要备用信息，也许一次性密码。`PAM` 提供了这种能力及更多。`PAM` 模块允许你为环境配置必要的安全级别。来自 Linux 安全 (`Linux Security`)

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

来自 `VERA` 的主要访问方法 (`BS2000`)

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

来自 `VERA` 的可编程属性映射 (`DRAM`, `PCI`)

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM

来自 `VERA` 的脉冲放大调制 (`Pulse Amplification Modulation`)

`http://www.tldp.org/LDP/Linux-Dictionary/html/index.html`

参见可插认证模块 (`PAM`)。来自 Redhat-9-Glossary

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAM (可插认证模块)

用于系统安全的备替换用户身份验证模块，允许在不知道将使用何种身份验证方案的情况下编写程序。稍可以使用不同的模块替换该模块，而无需重写软件。来自 I-gloss

```
http://www.tldp.org/LDP/Linux-Dictionary/html/index.html
```

### PAML

### P

### 1161

### 来自 VERA 的公开访问邮件列表 (Internet, BBS)

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

`pam_krb5`

`pam_krb5` 是一种可与 `Linux-PAM` 和 `Kerberos 5` 一起使用的可插认证模块 (`PAM`)。`pam_krb5` 模块支持密码检查、票据创建、可选的 `TGF` 验证以及转换为 `Kerberos IV` 票据。此包还包含了用于 `AfStokens` 的 `pam_krb5af` 模块。来自 Redhat 8.0 RPM

`http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

`pam_smb`

`pam_smb` 模块可以使用外部 `SMB` 服务器验证用户身份。来自 Redhat 8.0 RPM `http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

`pan`

一个 `GTKK` 的新闻阅读器，看起来像 `Forte Agent`。`Pan` 是一个新闻阅读器，松散基于 `Agent` 和 `Gravity` 开发，使其对新用户和高级用户都非常好用。它具有新闻阅读器中找到的所有类型功能，并提供离线新闻阅读、复杂的过滤、连接以及针对用户和 `alt` 二进制文件的额外功能。来自 Debian 3.0 APT `http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

`PAN`

来自 `VERA` 的个人账号 de (`Personal Account Number`) `http://www.tld.org/LDP/Linux-Dictionary/html/index.html`

`pan`
