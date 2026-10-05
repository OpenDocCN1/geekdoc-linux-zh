

该工具包含大量的功能和不同的用场景，因为它包含了用于信息收集、漏洞研究与开发、客户端攻击、后渗透利用等许多组件。

由于功能极其强大，人们很容易在 Metasploit 中迷失。幸运的是，该框架设计非常精良，提供了一个统一且合理的界面。

在本模块中，我们将对 Metasploit Framework 进行详细介绍，包括其功能、用法以及对其内部工作原理的解释。虽然我们重点讨论 Metasploit，但也会讨论一些适用于其他漏洞框架的各种。本模块的主要目标是理解这些框架如何在真实的渗透测试中为我们提供帮助。

## 20.1 熟悉 Metasploit

本学习单元涵盖以下学习目标：

- 设置和导航 Metasploit
- 使用辅助模块（auxiliary modules）
- 利用利用模块（exploit modules）

在本学习单元中，我们将熟悉 Metasploit Framework (MSF)。我们将从设置环境和对其进行导航开始。然后，我们将熟悉两种类型的模块⁹⁷¹。在 Metasploit 中，模块是与框架交互的主要方式，用于执行扫描或利用目标等任务。首先，我们将探索 Metasploit 的辅助模块以及如何使用它们执行协议枚举和扫描等任务。最后，我们将回顾 Metasploit 中包含的利用模块。

### 20.1.1 设置与使用 MSF

尽管 Metasploit Framework 预装在 Kali Linux 上，但在其默认配置下，它并不是启动数据库。虽然运行 Metasploit 并不强制要求使用数据库，但有充分的理由这样做，例如存储有关目标主机的信息并跟踪成功的利用尝试。Metasploit 使用 PostgreSQL⁹⁷² 作为数据库服务，该服务在 Kali 上既不是激活状态也没有在启动时运行。

我们可以启动数据库服务，并创建和初始化 msfdb init：

```bash
kali@kali~$ sudo msfdb init
[+] Starting database
[+] Creating database user 'msf'
[+] Creating databases 'msf_test'
[+] Creating databases 'msf_test'
[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'
[+] Creating initial database schema
```

列表 617 — 创建并初始化 Metasploit 数据库

> ⁹⁷ (Rapid7 Documentation, 2022), https://docs.rapid7.com/metasploit/modules/
⁹⁷² (PostgreSQL, 2022), https://www.postgresql.org/

# 启动时可以使用 systemctl 数据库数据库服务。

```bash
kali@kali:~ sudo systemctl enable postgresql
Synchronizing state of postgresql.service with SysV service script with
/lib/systemd/systemd-sysv-install enable install postgresql
Executing:
Created link /etc/systemd/multi-user.target.wants/postgresql.service -> /lib/systemd/system/postgresql.service.
```

> 行 618 - 在启动时启用 postgresql 数据库服务

现在，让我们作为 msfconsole 启动 Metasploit 命令行界面。

```bash
kali@kali:~ sudo msfconsole
...
  =[metasploit v0.2.2-dev]
  +-- [2251 exploits - 1187 auxiliary - 399 post]
  +-- [951 payloads - 45 encoders - 11 nops]
  +-- [9 evasion]
```

Metasploit 提示：使用 help <command> 学习更多任何命令
Metasploit 文档：https://docs.metasploit.com/

```bash
msf6 >
```

> 行 619 - 启动 Metasploit Framework

为了在启动时隐藏横幅和版本信息，我们可以向 msfconsole 命令添加 -q 选项。一旦启动 Metasploit 命令行界面，我们可以使用 db_status 验证数据库连接。

```bash
msf6 > db_status
[+] Connected to msf. Connection type: postgresql.
```

> 行 620 - 确认数据库连接性

列表 620 显示数据库已连接且我们已准备就绪。现在，让我们熟悉 Metasploit 的命令行界面以及如何使用它。
Metasploit 的命令行界面提供了许多用于导航和使用框架的命令，分为分类。这些类别由核心命令、模块命令、作业命令、资源脚本命令、数据库后端命令、凭据后端命令和开发者命令组成。在整个模块中，我们将使用其中大多数类别的命令。
通过输入 help 获取所有可用命令的列表。

```bash
msf6 > help
```

973 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Systemd
974 (Rapidit 7 Documentation, 2022), https://docs.rapid7.com/metasploit/msf-overview/
975 (OffSec, 2023), https://www.offensive-security.com/metasploit-unleashed/msfconsole-commands/

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

## 核心命令

| 命令 | 描述 |
| --- | --- |
| ? | 帮助菜单 |

## 模块命令

| 命令 | 描述 |
| --- | --- |
| search | 模块名称和描述 |
| show | 显示指定类型或所有模块 |
| use | 通过名称或索引与模块交互 |

## 作业命令

| 命令 | 描述 |
| --- | --- |
| ... | |

## 资源脚本命令

| 命令 | 描述 |
| --- | --- |
| ... | |

## 数据库后端命令

| 命令 | 描述 |
| --- | --- |
| db_nmap | 执行 nmap 并自动记录 |
| hosts | 列出数据库中的所有主机 |
| loot | 列出数据库中的所有收获 |
| notes | 列出数据库中的所有备注 |
| services | 列出数据库中的所有服务 |
| vulns | 列出数据库中的所有漏洞 |
| workspace | 切换工作空间 |

## 凭据后端命令

| 命令 | 描述 |
| --- | --- |
| creds | 列出数据库中的所有凭据 |

## 开发者命令

| 命令 | 描述 |
| --- | --- |
| ... | |

## 使用 Kali Linux 进行渗透测试

在 Metasploit 中操作之前，让我们先讨论一个重要概念：工作空间（workspaces）。假设我们已经进行了渗透测试，Metasploit 存储了关于目标及其基础设施的信息。在开始下次渗透测试时，为了避免混合不同评估的结果，可以使用 workspaces 命令。创建一个新的工作空间，需要将工作空间名称作为参数提供给命令。

```bash
msf6 > workspace
* default

msf6 > workspace -a pen200
[*] Added workspace: pen200
[*] Workspace: pen200
```

列表 622 - 创建工作空间 pen200一旦创建，Metasploit 将使用列表 622 所示的当前工作空间。现在，让我们填充数据库并熟悉一些数据库命令。这些，我们将使用 db_nmap 在 Metasploit 内部执行 nmap，语法与 nmap 相同：

```bash
msf6 > db_nmap
[*] Usage: db_nmap [-A target] [-h] [nmap options]

msf6 > db_nmap -A 192.168.50.200
[*] Starting Nmap 7.92 (https://nmap.org) at 2022-07-28 03:48 EDT
[*] Nmap scan report for 192.168.50.200
[*] Host is not down (0.1ms latency).
[*] Nmap Not shown: 99 closed ports (reset)
[*] PORT      STATE    VERSION
[*] 21/tcp    open    ftp
[*] 135/tcp  open    msrpc          Microsoft Windows RPC
[*] 139/tcp  open    netbios-ssn Microsoft Windows netbios-ssn
[*] 445/tcp  open    microsoft-ds     
[*] 3389/tcp  open ms-wbt-server  Microsoft Terminal Services
[*] 5357/tcp  open http             Microsoft HTTPAPI httpd 2.0 (SSDP/UpnP)
[*] Nmap: 8080/tcp open http         Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
```

PWK - © 2023 OffSec Services Limited. All rights reserved.

[+] Nmap: Nmap done: 1 IP address (1 host up) scanned in 67.72 seconds

列表 623 - 使用 db_nmap 扫描

列表 623 显示使用 nmap 执行的端口扫描结果。如前，如果数据库服务正在运行，Metasploit 将将发现主机的信息或凭据记录在方便访问的数据库中。

要获取到为止发现的所有主机列表，可以输入 hosts。

```bash
msf6 > hosts
Hosts
=====
address         mac      name    os_name      os_flavor os_sp purpose info comments
------------  ----  ----  ----------  ----------  ----  -------  ----  -------
192.168.0.202                Windows 2016                               server
```

此外，我们可以输入 services 显示端口扫描发现的服务。我们也可以通过提供 -p 对应的参数来过滤特定的端口号。

```bash
msf6 > services
Services
=======
host            port  proto name        state    info
------------  ----  ----  ----  ----  -------
192.168.0.202   21    tcp   ftp               open
192.168.0.202   135   tcp   msprpc            open    Microsoft Windows RPC
192.168.0.202   139   tcp   netbios-ssn      open    Microsoft Windows netbios-ssn
192.168.0.202   445   tcp   microsoft-ds     open
192.168.0.202   3389  tcp   ms-wbt-server  open    Microsoft Terminal Services
192.168.0.202   5357  tcp   http             open    Microsoft HTTPAPI httpd 2.0 (SSDP/UpnP)
192.168.0.202   8000  tcp   http              open    Golang net/http server (Go-IPFS json-rpc or InfluxDB API)
```

```bash
msf6 > services -p 8000
Services
=======
host            port  proto name        state    info
------------  ----  ----  ----  ----  -------
192.168.0.202   8000  tcp   http              open    Golang net/http server (Go-IPFS rc or InfluxDB API)
```

列表 625 - 显示所有发现的服务

列表 624 显示了此为止发现的所有的服务。通过过滤特定的数字，我们可以快速识别所有运行特定服务的主机。

当对具有多个目标系统进行评估时，数据库后端命令在识别重要信息和发现潜在攻击向量方面非常有价值的。我们还可以将存储在数据库中的结果作为模块的输入，将在下一节讨论。

