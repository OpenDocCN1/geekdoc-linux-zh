
# 1 [encrypted, NOT VERIFIED]

New window created: `history_size` => 1000

```
```

## 会话 1：加密已验证

添加安全性，请确保客户端显示相同的字符串：这是一个命令会话！这意味着你可以输入 `dncat2` 命令，例如 '`ping`'！要查看完整的客户端列表，请尝试 '`help`'。

以下是命令列表（在任何一个命令上使用 `-h` 获取额外帮助）：

- `clear`
- `delay`
- `download`
- `echo`
- `exec`
- `help`
- `listen`
- `ping`
- `quit`
- `set`
- `shell`
- `shutdown`
- `suspend`
- `unset`
- `upload`
- `window`
- `windows`

## 列表 613 - 从服务器与 dncat2 客户端交互

这返回一个带有 "command" 前缀的提示符。这是 `dncat2` 命令会话，它支持许多选项。我们可以通过带有 `help` 标志运行它来学习有关每个命令的信息。

由于我们在该模块中尝试建立隧道，让我们调查端口转发选项。我们可以使用 `listen` 在我们的 `dncat2` 服务器上设置一个监听端口，并通过我们的 DNS 隧道推送 TCP 流量，在何处它被解封装并推送到套接字。我们基于控制会话的基础工作使用 `ctrl-Z` 回到命令会话，让我们运行 `listen` 在本地端口监听以连接另一端，类似于 `ssh -l`。用法：`listen [<host>:<port>] <rhost>:<report>` `--help` : 显示此消息

## 列表 614 - 监听器信息

根据消息输出，`listen` 的工作类似于 `ssh -L`。我们现在应该对它非常熟悉了。让我们尝试通过我们的 DNS 隧道连接 HRSHARES 上的 SMB 端口。我们将设置本地转发，在 FELINEAUTHORITY 的环回接口上监听 `4455`，并连接到 HRSHARES 的 `4455`

## 列表 615 - 从 FELINEAUTHORITY 到 PGDATABASE01 设置端口转发

从另一个 felineauthority：可以通过此端口转发使用 SMB 共享

```
kali@felineauthority:~$ smclient -p 4455 -L //127.0.0.1 -U hr_admin --
password=Welcome1234
```

[WORKGROUP]@hr_admin 的密码：

| Sharename | Type | Comment |
| :--- | :--- | :--- |
| ADMIN | Disk | |
| IPC | Disk | |
| IPC | Disk | |

## 列表 616 - 连接到 HRSHARES

错误：用户请求在本地端口上 Listen 以连接另一端，类似于 `ssh -l`。用法：`listen [<host>:<port>] <rhost>:<report>` `--help` : 显示此消息

`dnscat2` 进程正在使用 CNAME、TXT 和 MX 查询及响应。这揭示了一个巨大的数据传输网络，`dnscat2` 具有隐身性！服务器和响应负载已加密，因此记录流量非常有益。我们将通过 `ctrl+C` 继续使用 `tcpdump`

# 使用 Kali Linux 进行渗透测试

该工具拥有大量的功能和不同的用场景，因为它包含了信息收集、漏洞研究与开发、客户端攻击、后渗透利用等许多组件。

由于其功能极其强大，人们很容易在 Metasploit 中迷失方向。幸运的是，该框架的设计非常精妙，提供了一个统一且合逻辑的接口。

在本模块中，我们将对 Metasploit 框架进行逐步演练介绍，包括其功能和用法，并对其内部原理进行一些解释。虽然我们重点介绍的是 Metasploit，但也会讨论一些适用于其他框架的通用概念。本模块的主要目标是理解这些框架如何在真实的渗透测试中我们提供帮助。

### 20.1 熟悉 Metasploit

本学习单元涵盖了以下学习目标：

- 设置和导航 Metasploit
- 使用辅助模块（`auxiliary modules`）
- 利用利用模块（`exploit modules`）

在本学习单元中，我们将熟悉 Metasploit 框架（MSF）。我们将从设置环境和在框架中导航开始。然后，我们将熟悉两种类型的模块。⁷¹ 在 Metasploit 中，模块是与框架交互的主要方式，用于执行如扫描或利用目标等任务。首先，我们将探索 Metasploit 的辅助模块，以及我们如何使用它们执行协议枚举和端口扫描等任务。最后，我们将复习 Metasploit 中包含的利用模块。

#### 20.1.1 设置与与 MSF 工作

尽管 Metasploit 框架已预安装在 Kali Linux 上，但它在默认配置下不会启动数据库服务。虽然运行 Metasploit 并不强制要求使用数据库，但这样做有令人信服的理由，例如存储有关目标主机的信息并跟踪成功的利用尝试。Metasploit 使用 PostgreSQL⁷² 作为数据库服务，该服务在 Kali 启动时默认不是激活且启用的。

我们可以通过 `msfdb init` 启动数据库服务并创建、初始化 Metasploit 数据库。

```
kali@kali~$ sudo msfdb init
[+] Starting database
[+] Creating database user 'msf'
[+] Creating databases 'msf'
[+] Creating databases 'msf_test'
[+] Creating configuration file '/usr/share/metasploit-framework/config/database.yml'
[+] Creating initial database schema
```

列表 617 - 创建并初始化 Metasploit 数据库

> ⁷¹ (Rapid7 Documentation, 2022), https://docs.rapid7.com/metasploit/modules/
> ⁷² (PostgreSQL 2022), https://www.postgresql.org/

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

636

制作于摩洛哥

# 我们可以使用 systemctl 设置 OffSec 数据库服务的启动时间。

```
kali@kali:~ sudo systemctl enable postgresql
Synchronizing state of postgresql.service with SysV service script with
/lib/systemd/systemd-sysv-install enable postgresql
Executing: /etc/systemd/multi-user.target.wants/postgresql.service -> /lib/systemd/system/postgresql.service.
Created symlink /etc/systemd/system/postgresql.service. ...
```

> 列表 618 - 在启动时启用 Metasploit 命令行界面

现在，让我们用 `msfconsole` 启动 Metasploit 命令行界面。

```
kali@kali:~ sudo metasploit
...
+= [metasploit v0.6.2-dev]
+ -- [2251 exploits - 1187 auxiliary - 399 post]
+ ----- [951 payloads - 45 encoders - 11 hops]
+ --== [9 evasion]
```

Metasploit 小贴士：使用 `help <command>` 了解更多关于任何命令
Metasploit 文档：https://docs.metasploit.com/

> 列表 619 - 启动 Metasploit 框架

为了启动时隐藏横幅和版本信息，为 `msfconsole` 添加 `-q` 选项。当 Metasploit 命令行界面启动后，我们可以使用 `db_status` 验证连接性。

```
msf6 > db_status
[+] Connected to db. type: postgresql.
```

> 列表 620 - 确认数据库连接

`db_status` 显示数据库已连接。现在，让我们熟悉 Metasploit 的命令行界面。

Metasploit 的命令行界面提供了许多命令，分为不同的类别。这些类别包括核心命令、模块命令、作业命令、脚本命令、数据库后端命令和开发者命令。在本模块中，我们可以通过输入 `help` 获取可用命令列表。

```
msf6 > help
```

# 核心命令

# OffSec

===============
