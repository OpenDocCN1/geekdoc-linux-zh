
- `service:Samba:http://$HOSTNAME:901,en,65535`：这行描述了服务 URL。`Samba` 是服务类型。`http://$HOSTNAME:901` 是地址规范。`en` 是语言标签。`65535` 是寿命。`tcp-port=901` 是端口。`description` 是 Samba web 前端。

以下是 Samba 的注册文件（`/etc/slp.reg/samba.reg`）：

```
################################################################
## OpenSLP 注册文件
# 注册 Samba and SWAT
################################################################

# 注册 samba 服务器，如果它正在运行
service:smb://$HOSTNAME,en,65535
tcp-port=139
description=Samba file and print server

# 注册 samba 的 web 前端
service:Samba:http://$HOSTNAME:901,en,65535
tcp-port=901
description=Samba web front end
```

以下是 SSH 的注册文件（`/etc/slp.reg/ssh.reg`）：

```
################################################################
# OpenSLP registration file
# 注册 ssh
################################################################

# 注册 ssh
service:ssh://$HOSTNAME,en,65535
tcp-port=22
description=SSH daemon
```

这些行的解释如下：

- `service:ssh://$HOSTNAME,en,65535`：这行描述了服务 URL。`ssh` 是服务类型。`$HOSTNAME` 是地址规范。`en` 是语言标签。`65535` 是寿命。`tcp-port=22` 是端口。`description` 是 SSH 守护进程。

- `service:file://$HOSTNAME,en,65535`：这行描述了服务 URL。`file` 是服务类型。`$HOSTNAME` 是地址规范。`en` 是语言标签。`65535` 是寿命。`tcp-port=22` 是端口。`description` 是文件传输。

以下是 SSH 的注册文件（`/etc/slp.reg/ssh.reg`）：

```
################################################################
# OpenSLP registration file
# 注册 ssh
################################################################

# 注册 ssh
service:ssh://$HOSTNAME,en,65535
tcp-port=22
description=SSH daemon
```

## 使用 slptool 进行动态注册

如果需要从专有脚本为 OpenSLP 注册服务，请使用 `slptool` 命令行前端。

slptool 提供了两个基本功能：

- 它可以用于仅在 `slpd` 运行期间动态注册服务。
- 它提供了用户代理（User Agent）功能来请求服务。

要列出 slptool 的可用选项和功能，请输入：

```
slptool -help
```

或

```
slptool
```

### 显示内容如下：

```
Usage: slptool [options] command-and-arguments
options 可能为:
-v (or --version) 显示 slptool 和 OpenSLP 的版本
-s (or --scope) 后接由逗号分隔的范围列表
-l (or --language) 后接语言标签
command-and-arguments 可能为:
  findsrv service-type [filter]
  findrsvusingiflist interface-list service-type [filter]
  unicastfindsrv ip-address service-type [filter]
  findattrs url [attrids]
  unicastfindattrs ip-address url [attrids]
  findattrsusingiflist interface-list url [attrids]
  findsrvtypes [authority]
  unicastfindsrvtypes [authority]
  findsrvtypesusingiflist interface-list [authority]
  findscopes
  register url [attrs]
  deregister url
  getproperty propertyname
Examples:
  slptool register service:myserv.x://myhost.com
  "(attr1=val, attr2=val)"
  slptool findsrv service:myserv.x
  slptool findsrv service:myserv.x "(attr1=val)"
  slptool findrsvusingiflist 10.77.13.240,192.168.250.240 service:myserv.x
  slptool findrsvusingiflist 10.77.13.243 service:myserv.x "  (attr1=val)"
  slptool unicastfindsrv 10.77.13.237 service:myserv.x
  slptool unicastfindsrv 10.77.13.237 service:myserv.x "(attr1=val)"
  slptool findattrs service:myserv.x://myhost.com
```

## 目标 4 使用 SLP 前端

slptool 是一个简单的命令行程序，可以用于：

- 将向服务代理（Service Agents）动态引入 SLP 服务（仅在运行期间有效）。
- 或者
- 在网络上发现 SLP 服务。

第一个功能已经讨论过了。

以下是使用第二个功能的示例：

要查找由哪些服务器提供 SSH 服务，请执行以下操作：

1. 在命令行中，输入

```
slptool findsrvtypes
```

将显示一个类似下面的服务列表：

```
service:ntp
service:kde.sld.suse
service:smtp
service:ssh
service:fish
service:remotedesktop.kde:vnc
service:remotedesktop.java:http
service:ldap
service:smb
service:install.suse:nfs
service:install.suse:ftp
service:install.suse:http
service:smdr.novell
service:bindery.novell
service:ndap.novell
service:wbem:https
```

2. 使用 `service:ssh` 获取提供 SSH 服务的服务器信息。为此，请输入

```
slptool findsrvsrv service:ssh
```

### 显示提供 SSH 服务的主机列表：

```
service:ssh://dal1.digitalairlines.com:22,65535
service:ssh://da3.digitalairlines.com:22,65535
service:ssh://da4.digitalairlines.com:22,65535
service:ssh://da10.digitalairlines.com:22,65535
service:ssh://da11.digitalairlines.com:22,65535
```

输入 `slptool --help` 获取所有可用选项和功能的列表。

如上述“使用 slptool 进行动态注册”节所描述，slptool 也可以从处理 SLP 信息的脚本中调用。

## 练习 5-1 为 OpenSLP 提供时间服务

在此练习中，你将学习如何在你的服务器上配置 SLP，这种简单的服务独立于全网 SLP 设计考虑。

你将在练习册中找到此练习。

（练习结束）

## 总结

### 目标

#### 总结

1. 了解什么是 OpenSLP。服务发现协议（SLP）提供了服务的动态发现。

在 SUSE Linux Enterprise Server 10 上，可以使用 OpenSLP。它是 SLP v2 的开源实现。

OpenSLP 在数据库中注册服务信息，并允许 SLP 客户端查询数据库以查找这些服务。

2. 了解 OpenSLP 使用的 SLP 代理（Agents）：OpenSLP 使用代理表示网络上的应用程序和服务：

- 用户代理（User Agent）
- 服务代理（Service Agent）
- 目录代理（Directory Agent）

这些代理之间的对话限于非常简单的请求和响应消息交换。

SLP 是一种单播和多播协议。消息可以发送到：

- 一时发送给一个代理（单播）
- 或者
- 同时发送给所有（正在监听的）代理（多播）

### 目标总结

3. 配置 SLP

OpenSLP 使用代理来表示网络上的应用程序和服务：

- 用户代理
- 服务代理
- 目录代理

这些代理之间的对话限于非常简单的请求和响应消息交换。

SLP 是一种单播和多播协议。消息可以发送到：

- 一时发送给一个代理（单播）
- 或者
- 同时发送给所有（正在监听的）代理（多播）

## 配置 SLP

要配置 SLP，你需要知道以下内容：

- OpenSLP 守护进程（daemon）OpenSLP 守护进程是 `/usr/sbin/slpd`。
- 在 SUSE Linux Enterprise Server 10 上，守护进程是默认可用的。它的脚本是 `/etc/init.d/slpd`。
- 停止守护进程，输入 `/etc/init.d/slpd stop`
- 启动守护进程，输入 `/etc/init.d/slpd start`
- 重启守护进程，输入 `/etc/init.d/slpd restart`
- 检查守护进程状态，输入 `/etc/init.d/slpd status`

### 配置 SLP（续）

- SLP 配置文件：SLP 配置文件是 `/etc/slpd.conf`。
- 守护进程在启动时读取该文件。
- SLP 配置文件包含 `parameter=value` 格式
- SLP 注册文件：SLP 注册文件位于 `/etc/slpd.reg`。
- 守护进程在启动时读取该文件。

可能的注册方式有：

- 静态注册通过 `/etc/slpd.reg`
- 动态注册通过 `/etc/slpd.reg`
- 使用 slptool 进行动态注册

4. 使用 SLP 前端

slptool 是一个简单的命令行程序，可以用于：

- 动态向服务代理引入 SLP 服务（仅在运行期间有效）。
- 或者
- 在网络上发现 SLP 服务。

# 6 监控流量

在部署你的服务器后，监控网络流量是非常关键的。在 SUSE Linux Enterprise Server 10 上，可以使用工具。这些工具提供了排查问题的能力。

## 目标

1. 使用 ntop 监控流量
2. 使用 Nagios 监控主机、服务和网络
3. 使用 Wireshark 和 tcpdump 排查网络

## 目标 1 使用 ntop 监控流量

ntop 是一种基于 Web 的流量监控工具，类似于 `top` 命令。它包含在 SUSE Linux Enterprise Server 10 中。

在此目标中，你将学习：

- 配置 ntop
- 使用 ntop

### 配置 ntop

要安装 ntop，在 YaST 的软件安装中选择 ntop 包。

ntop 的配置文件是 `/etc/sysconfig/ntop`。可用选项有：

- `NTOPD_IFACE`：指定 ntop 使用的网络接口。如果你输入多个接口，用逗号分隔。
- `NTOPD_PORT`：指定 ntop 使用的端口（默认：3000）。
- `NTOPD_SSL_PORT`：定义 SSL 端口。使用此选项运行时你需要生成证书。
- `NTOP_USER`：定义运行 ntop 的用户。这不应该是 root！
- `NTOPD_ARGS`：使用 `/etc/init.d/ntop` 启动 ntop 时的额外参数。

参见 `man 8 ntop` 获取所有命令行选项。

### 使用 ntop

在启动 ntop 之前，你必须设置管理员密码：

```
da51:~ # ntop -A u wwwrun
Tue May 24 04:32:57 2005 初始化 gdbm 数据库
Tue May 24 04:32:57 2005 现在以请求的用户 'wwwrun' (uid:8) 运行

请输入管理员密码：
再次输入密码：
Tue May 24 04:32:59 2005 管理密码已设置
da51:~ #
```

- `-A` 参数启动 ntop、设置管理员密码并退出 top。A 会提示用户输入密码。
- `-u` 参数指定 ntop 在初始化后应该运行的用户。

密码存储在 `/var/lib/ntop/ntop_pw.db` 文件中。

ntop 通常必须以 root 启动，以便有足够的权限以杂杂模式打开网络接口以接收原始帧。

启动 ntop 后，进程将以命令行指定的用户的 UID 运行。在 SUSE Linux Enterprise Server 10 上，通常使用 wwwrun 用户运行 ntop。

本节涵盖以下内容：

- 在 Web 模式下使用 ntop
- ntop 的命令行选项

#### 在 Web 模式下使用 ntop

进入 ntop 后，您可以在浏览器中输入以下 URL 访问 ntop 界面：

http://hostname:3000

### 图 6-1

欢迎使用 ntop | 关于 | 摘要 | IP 摘要 | 所有协议 | 本地 | FC | SCSI | 管理 | (C) 1998-2004 - L. Dari

摘要: 流量 | 主机 | 网络负载 | ASN 信息 | VLAN 信息 | NetFlow

| 全局流量统计 | |
| :--- | :--- |
| 网络接口 | 设备名称 | 类型 | 速率 | 采样率 | MTU | 地址 | IPv4 地址 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| eth0 | eth0 | 以太网 | | 1 | 1014 | 19.0.0.1 | |
| | | | | | | digitalstatistics.com | |
| 本地域名 | | | | | | | 2023年5月27日 周六 15:05:23 |
| 采样存储 | 3 | | | | | | |
| 活跃端端节点 | | | | | | | |
| "eth0" [switch] 流量报告 | | |
| :--- | :--- | :--- |
| 丢弃（输入） | 0.0% | 0 |
| 丢弃（输出） | 0.0% | 0 |
| 总丢弃 (icmp) | | 0 |
| 总处理数据包 | 71.6% | 5 |
| 唯一 | 14.3% | 1 |
| 广播 | 14.2% | 1 |
| 组播 | | |

| | |
| :--- | :--- |
| 最短 | 60 字节 |
| 平均大小 | 120 字节 |
| 最长 | 440 字节 |
| < 64 字节 | 42.5% | 3 |
| < 128 字节 | 28.6% | 2 |
| < 256 字节 | 0.0% | 0 |
| < 512 字节 | 28.0% | 2 |
| < 1024 字节 | 0.0% | 0 |
| < 1518 字节 | 0.0% | 0 |
| > 1518 字节 | | |

### CNI 仅供使用- 允许质印

严禁复制本手册的全部或部分或分发此类副本。如发现疑似侵权行为，请拨打 1-800-PIRATES。

在顶行共有八部分：

- **关于 (About)**：此部分包含：
  - ntop 配置概述。
  - 帮助。

- **摘要 (Summary)**：此部分包含：
  - 网络流量的摘要。
  - 主机网络信息。
  - 网络负载信息。
  - 自治系统流量统计。
  - VLAN 流量统计。
  - 网络流。（流是匹配指定规则的捕获数据流。）

- **IP 摘要 (IP Summary)**：此部分包含：
  - 每个主机的网络流量信息。
  - 组播统计。
  - 所有域的统计。
  - IP 协议分布。
  - 本地和远程 IP 流量。

- **所有协议 (All Protocols)**：此部分包含：
  - 每个主机使用的协议。
  - 网络吞吐量。
  - 主机活动时间表。

- **本地 IP (Local IP)**：此部分包含：
