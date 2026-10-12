
# 模块命令

Command          Description
-----------------

# 作业命令

Command          Description
-----------------

# 脚本命令

Command          Description
-----------------

# 数据库后端命令

Command          Description
-----------------

# 开发者命令

Command          Description
-----------------

# Sec

| Command | Description |
| --- | --- |
| ... | |

列表 621 MSF 帮助菜单

使用 Kali Linux 进行渗透测试

在进入 Metasploit 操作之前，让我们先讨论一个重要概念：工作区（workspaces）。假设我们执行了渗透测试，Metasploit 将目标及其基础设施的信息存储在数据库中。为了解决不同评估结果相互混合的问题，我们可以使用工作区。`workspace` 命令列出所有已创建的工作区。通过添加名称切换到工作区。创建一个新的工作区需要向 `-a` 参数提供工作区名称。让我们创建一个名为 pen200 的工作区，并将此处和后续部分的存储其中。

```
msf6 > workspace

* default

msf6 > workspace -a pen200

[*] Added workspace: pen200

[*] Workspace: pen200
```

> 列表 622 - 创建工作区 pen200

一旦创建，Metasploit 将将其作为当前工作区如 622 所示。

现在，让我们填充数据库并熟悉数据库后端命令。对于这一点，我们将使用 `db_nmap`，它是在 Metasploit 内部执行 Nmap并将结果保存到数据库的封装。该命令与 Nmap 语法相同：

```
msf6 > db_nmap

[*] Usage: db_nmap [--save] [--help] [-hmap] [nmap options]

msf6 > db_nmap -A 192.168.50.202

[*] Nmap scan report 7:92 (https://nmap.org) at 2022-07-28 23:48 EDT

[*] Nmap scan report for 192.168.50.202

[*] Host is up (0.0ms latency).

[*] Not shown: 993 closed ports (reset)

[*] PORT STATE SERVICE VERSION

[*] 21/tcp open ftp

[*] 135/tcp open msrpc Microsoft Windows RPC

[*] 139/tcp open netbios Microsoft Windows netbios-ssn

[*] 445/tcp open microsoft-dsi

[*] 3389/tcp open ms-wbt-server Microsoft Terminal Services

[*] 5357/tcp open http Microsoft HTTPAPI http 2.0 (SSDP/UpnP)

[*] Nmap: 8000/tcp open Golang net/http server (Go-IPFS json-rpc or

InfluxDB API)
```

# OffSec

使用 Kali Linux 进行渗透测试

[+] Nmap: Nmap 完成：扫描了 1 个 IP 地址（1 个主机在线），耗时 67.72 秒。

## 列表 623 - 使用 db_nmap 扫描 BRUTE2

列表 623 显示了使用 Nmap 执行的端口扫描结果。如前所述，如果数据库服务正在运行，Metasploit 将将发现的主机结果、信息或凭据记录在方便、易于访问的数据库中。

要获取目前为止发现的所有在线主机列表，你可以输入 `hosts`。

```bash
msf6 > hosts

Hosts
=====

address      mac name      os_name os_flavor os_sp purpose info comments
----------- ----------- ----------- ---------- ----- --------- ------ -----------
192.168.50.202                Windows 2016                            server
```

## 列表 624 - 显示所有发现的服务

此外，我们可以输入 `services` 来显示端口扫描中发现的服务。我们也可以通过提供 `-p` 参数指定的端口号来过滤特定端口。

```bash
msf6 > services

Services
=======

host                 port proto name      state info
192.168.50.202      21    tcp  ftp               open
192.168.50.202      135   tcp  msrpc              open  Microsoft Windows RPC RPC
192.168.50.202      139   tcp  netbios-ssn      open  Microsoft Windows netbios-ssn
192.168.50.202      445   tcp  microsoft-ds     open  Microsoft Terminal Services
192.168.50.202      5389  tcp  ms-web-server    open  Microsoft HTTPAPI httpd 2.0
SSDP/UpnP
json-rpc or InfluxDB API
```

```bash
192.168.50.202      8000  tcp  http              open  Golang net/http server Go-IPPS
192.168.50.202      8000  tcp  http               open  Golang net/http server Go-IPPS or -
InfluxDB API
```

```bash
msf6 > -p 8000

Services
=======
```

```bash
host                 port proto name      state info
192.168.50.202      8000  tcp  http               open  Golang net/http server Go-IPPS or -
InfluxDB API
```

## 列表 625 - 显示所有发现的服务

列表 624 显示了目前发现的所有服务。由于我们可以过滤特定的数字，因此快速识别出所有运行特定服务的主机。

在对具有许多目标系统的评估时，数据库后端命令（Database Backend Commands）对于识别重要信息和发现潜在攻击向量极具价值。我们还可以将存储在数据库中的结果作为模块的输入，我们将在下一节讨论这一点。

PWK - 版权 © 2023 OffSec Services Limited. 保留所有。

制作于摩洛哥

# OffSec

使用 Kali Linux 进行渗透测试

在进入下一节之前，让我们再次简单回顾模块（modules）。如所述，模块用于在 Metasploit 中执行任务，如扫描或利用目标。该框架包含数千个模块，分为若干类别。

类别显示在启动屏幕摘要中，但我们也可以使用 `show -h` 命令查看它们。

```bash
msf6 > -h

[*] "show" 命令的有效参数为: all, encoders, nops, exploits, payloads, auxiliary, post, plugins, info, options

[*] 额外的模块特定参数为: missing, advanced, evasion, actions

msf6
```
