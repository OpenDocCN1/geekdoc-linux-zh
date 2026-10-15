
在本章中，我们将探讨绕过计算机安全控制的艺术。这包括绕过 Windows 安全、杀毒软件安全和防火墙安全。我们还将深入研究社交工程以及用于渗透测试和网络安全评估的各种技术。本章将提供宝贵的见解和技能，用于评估和增强安全控制的有效性。

## 结构

在本章中，我们将讨论以下主题：

- 安全控制的重要性
- 安全控制的进展
- 网络绕过
- 绕过 Windows Defender
- AV 规避技术和工具
    - 利用 Metasploit 模板和自定义二进制文件规避杀毒软件
    - Shellter
    - Phantom-Evasion
- Invoke-stealth
- 演进 WAF 策略
- 演进社交工程
- 钓鱼模拟
- Gophish

> 注意：绕过安全控制可以揭示被忽视的漏洞并暴露安全技术的局限性，使组织能够加强对新兴威胁的防御。

## 安全控制的进展

随着技术的进步，攻击者不断调整其方法，这使得渗透测试人员理解并评估安全控制的最新进展至关重要。现在让我们深入研究图 9.1 所示的安全控制的显著增强：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_289_0.png)

图 9.1：安全控制的进展

## 前沿技术

在现代网络安全领域，三项关键进展正在重塑组织保护数字资产的方式：

- 下一代防火墙：通过深度包检测等高级功能，增强对复杂攻击的检测和预防。
- 基于行为的异常检测：快速检测网络和用户行为的偏差，提醒安全团队注意潜在威胁。
- AI 驱动的威胁情报：通过分析数据集和关联指标主动猎捕威胁，辅助威胁的识别和缓解。

## 智能系统

驱动数字防御演化的两个智能系统：

- 机器学习与人工智能：引入机器学习和人工智能改进了安全控制，实现了实时异常检测、自动化响应和自适应威胁建模。
- 自动化与编排：具有自动化的安全控制简化了事件处理，能够更快速地遏制和缓解威胁。

## 演变的威胁态势

以下两点突出了在日益复杂的威胁中，网络安全实践的演变：

- 零信任架构：这种安全模型拒绝对用户和设备的自动信任，要求在访问资源时进行持续的身份验证和校验。
- 结合机器学习的高级恶意软件检测：安全控制利用机器学习算法识别并对抗复杂的恶意软件，包括多态威胁和零日威胁。

## 云特定安全控制

以下点讨论了用于保护云环境的云特定安全控制和框架：

- 云安全态势管理 (CSPM)：这些控制通过监控配置、识别漏洞以及确保符合最佳实践来帮助保护云环境。
- 云安全矩阵 (CSM)：`CSM` 是一个稳健的框架，指导组织保护其云环境。它整合了行业公认的标准，如云安全联盟 (CSA)、云控制矩阵 (CCM)、互联网安全中心 (CIS) 控制措施以及美国国立标准与技术研究院 (NIST) 网络安全框架。

> 注意：在追求遵循零信任架构原则的过程中，组织必须优先采用前沿技术、智能系统和云特定控制。

## 网络侦察中的安全控制绕过

在利用 `Nmap` 进行侦察时，有几种技术可以用于绕过安全控制。让我们探索这些类别及其子项，以及相关的命令和步骤：

首先，让我们检查目标 Windows 10 机器是否启用或禁用了 Windows 防火墙。如图 9.2 所示，观察到 Windows 防火墙目前开启状态：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_291_0.png)

图 9.2：Windows 防火墙已启用

### 源端口操纵

源端口操纵涉及将源端口更改为常用端口，增加 IDS 或防火墙识别并阻止扫描活动的难度。要执行此技术，请使用图 9.3 所示的命令 `nmap -g <common-source-port> targetIP`：

```bash
[umnedel@hall:~/desktop]$
sudo nmap -g 80 192.168.29.24
[sudo password for umnedel]
Nmap Starting 7.92 (https://nmap.org) on 2023-07-07 07:11 EDT
Nmap scan report for 192.168.29.24
Host is up (0.0008ms latency).
Not all 100 ports are filtered (tcp)
PORT SERVICE
80/tcp open http
135/tcp open ms-rpc
139/tcp open ms-nmb
445/tcp open registry-clt
2105/tcp open eklog
3139/tcp open ms-mgmt
3389/tcp open ms-server
5985/tcp open wget
8443/tcp open https-alt
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address scanned in 5 seconds
```

图 9.3：源端口操纵

## IP 地址欺骗

IP 地址欺骗允许创建或手动选择诱骗地址，为 IDS 和防火墙准确识别真实源带来障碍。要使用此技术，请利用图 9.4 所示的命令 `nmap -S <decoy-IP> -D targetIP`：

```bash
ummedeel@kali:~/Desktop
sudo nmap -S 192.168.2.40 -D <random host>
Starting Nmap 7.93 (https://nmap.org) at 2022-07-02 07:13 EDT
Nmap scan for 192.168.2.40
Host is up (0ms-latency).
Not shown: 991 ports filtered (no-response)
PORT SERVICE
80/tcp open http
135/tcp open ms-rpc
1381/tcp open ms-rpc
2103/tcp open zephyr-clt
2105/tcp open ms-login
2187/tcp open ms-mgmt
3389/tcp open ms-ds-server
5357/tcp open wsdapi
8443/tcp open https-alt
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address scanned in 5.04 seconds
```

图 9.4：IP 地址欺骗

### 数据分片

分片技术涉及向目标发送分包并在接收后进行重组。这种方法可以有效绕过入侵检测系统 (IDS) 和防火墙。要利用此技术，执行图 9.5 所示的命令 `nmap -f targetIP`：

```bash
ummedeel@kali:~/Desktop
sudo nmap -f 192.168.2.40
Starting Nmap 7.93 (https://nmap.org) at 2022-07-02 07:15 EDT
Nmap scan for 192.168.2.40
Host is up (0ms-latency).
Not shown: 991 ports filtered (no-response)
PORT SERVICE
80/tcp open http
135/tcp open ms-rpc
1381/tcp open ms-rpc
2103/tcp open zephyr-clt
2105/tcp open ms-login
2187/tcp open ms-mgmt
3389/tcp open ms-ds-server
5357/tcp open wsdapi
8443/tcp open https-alt
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address (host) scanned in 4.92 seconds
```

图 9.5：数据分片

## MAC 地址欺骗

MAC 欺骗涉及更改原始 MAC 地址以隐藏网络流量的真实身份。要执行此方法，使用图 9.6 所示的命令 `nmap --spoof-mac <spoofed-mac> targetIP`：

```bash
$unnamed@kali:~$ nmap
sudo nmap -sn --spoof-mac 192.168.0.248
Starting Nmap 7.9 (https://nmap.org) at 2023-07-02 07:27 EDT
Spoofing MAC address AC:BD:A5:E2:B3:8 (No registered vendor)
You have found some options that require root access.
These options will not be honored for TCP scan.
Nmap scan for 192.168.0.248
Host is up (0.00992ms, latency).
Not shown: 911 filtered ports (no-response)
STATE SERVICE PORT
80/tcp open http
135/tcp open ms-rpc
1481/tcp open msnq
2183/tcp open zephry-clt
2105/tcp open eklogin
2107/tcp open msnq-mgmt
3389/tcp open ms-web-server
5357/tcp open wsadpi
8443/tcp open https-alt
Nmap done: 1 IP address (host up) scanned in 19.36 seconds
```

图 9.6：MAC 地址欺骗

## 自定义包创建

创建自定义包允许发送特制包以扫描目标防火墙和安全措施。

1. `--data-length` 命令便于指定附加数据所需的长度。要使用此功能，执行图 9.7 示例所示的命令 `nmap --data-length <length> targetIP`：

```bash
$unnamed@kali:~/Desktop
sudo nmap --data-length 10 192.168.0.248
Starting Nmap 7.9 (https://nmap.org) at 2023-07-02 07:30 EDT
Nmap scan for 192.168.0.248
Host is up (0.00992ms, latency).
Not shown: 918 filtered ports (no-response)
STATE SERVICE PORT
80/tcp open http
135/tcp open ms-rpc
1481/tcp open msnq
2183/tcp open zephry-clt
2105/tcp open eklogin
2107/tcp open msnq-mgmt
3389/tcp open ms-web-server
5357/tcp open wsadpi
8443/tcp open https-alt
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address (host up) scanned in 4.46 seconds
```

图 9.7：自定义包创建 (Data-length)

2. `--data-string` 命令允许在数据包中添加特定字符串，从而包含自定义内容。要利用此功能，如图 9.8 所示，执行命令 `nmap --data-string <string> targetIP`：

```bash
ummeedel@kali:~/Desktop
$ sudo nmap --data-string "meel book" 192.168.29.240
Starting Nmap 7.92 (https://nmap.org ) at 2023-07-02 07:32 EDT
Nmap scan for 192.168.29.240
Host is 1 IP address (0.00012 latency).
Not shown: 998 (filtered) tcp ports (no-response)
PORT STATE SERVICE
80/tcp open http
135/tcp open msrpc
1681/tcp open msnmp
2183/tcp open rphayr-clt
2105/tcp open eklogin
2107/tcp open ms-mgmt
3389/tcp open ms-wbt-server
5357/tcp open wsdapi
8443/tcp open https
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address (host up) scanned in 4.95 seconds
```

图 9.8: 自定义数据包创建（Data-string）

3. 另一方面，`--data-command` 通过提供十六进制格式的数据，允许包含包括二进制内的多种格式自定义数据。要利用此功能，如图 9.9 所示，执行命令 `nmap --data <hex string>`：

```bash
ummeedel@kali:~/Desktop
$ sudo nmap --data 756d056432333 192.168.29.240
[sudo] password for ummeedel
Starting Nmap 7.92 (https://nmap.org ) at 2023-07-02 08:45 EDT
Nmap scan for 192.168.29.240
Host is 1 IP address (0.00122 latency).
Not shown: 998 (filtered) tcp ports (no-response)
PORT STATE SERVICE
80/tcp open http
135/tcp open msrpc
1681/tcp open msnmp
2183/tcp open rphayr-clt
2105/tcp open eklogin
2107/tcp open ms-mgmt
3389/tcp open ms-wbt-server
5357/tcp open wsdapi
8443/tcp open https
MAC Address: 00:0C:29:9F:7A:5D (VMware)
Nmap done: 1 IP address (host up) scanned in 4.33 seconds
```

图 9.9: 自定义数据包创建（Data）

# Nmap 脚本引擎脚本

Nmap 脚本引擎 (NSE) 脚本允许利用定制的脚本来绕过防火墙限制并发现漏洞。这些脚本涵盖了数据包分片、源端口操纵、IP 地址欺骗等专门设计用于绕过防火墙的方法。要执行脚本，如图 9.10 所示，使用命令 `nmap --script=firewall-bypass targetIP`：

```bash
$ user0@kali:~/Desktop
$ sudo nmap --script=firewall-bypass 192.168.29.240
Starting Nmap 7.92 (https://nmap.org ) at 2023-07-02 08:07:42 EDT
Nmap scan report for 1 host (192.168.29.240)
Host is up (0.00082s latency).
Not shown: 99 filtered ports (no response)
PORT   STATE
80/tcp open http
443/tcp open https
139/tcp open msrpc
445/tcp open rephry-clt
2181/tcp open ekolog
3109/tcp open wget
3389/tcp open ms-bt-server
5357/tcp open wapdi
8043/tcp open https
MAC Address: 00:29:9F:7A:5D (VMware)
Nmap done: 1 IP address (1 host) scanned in 6.27 seconds
```

图 9.10: Nmap NSE 脚本

> 注意：在进行防火墙绕过侦察时，对目标进行深入研究、采用隐蔽扫描技术、加密和隧道方法、规避基于特征的检测并熟练地操纵网络流量至关重要。

## 绕过 Windows Defender

Windows 系统带有名为 Windows Defender 的内置安全防护。在本节中，我们的目的是绕过 Windows Defender 的检测能力并建立反向连接。为了说明这一点，让我们考虑这样一个场景：作为攻击者，已经获得了受害者组织内 Windows 10 工作站的低权限访问。该系统的 Windows Defender 正在运行并开启了所有保护措施。我们的目标是执行多个恶意脚本进行枚举和横向移动，这些操作可能会被 Defender 拦截。

我们将分两个阶段探索这一概念。第一阶段涉及生成通用载负载并评估其是否被安全措施拦截。第二阶段，我们将采用高级方法生成一个完全不可检测（FUD）状态的载负载，允许我们绕过安全控制。

# 阶段 1：探索 Windows 10 上反向连接的基本方法

在本节中，我们将利用 `msfvenom` 使用基本方法生成反向连接载负载。让我们探索下面的分步方法：

1. 首先，让我们检查 Windows Defender 的启用和更新状态，如图 9.11、9.12 和 9.13 所示：

参考下方的图 9.11，该图展示了作为目标的 Windows 10 系统：

![](img/e4f93a89908ca3f498ee2517ddfbfd77_296_0.png)

> 图 9.11: Windows 10

图 9.12 显示了 Windows Defender 的当前状态：
