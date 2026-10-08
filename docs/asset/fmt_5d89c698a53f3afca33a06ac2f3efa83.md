
# 使用 Kali Linux 2.0 进行渗透测试

- 列表 728 - 使用 DCSync 为 Administrator 转储密码哈希值

转储内容包含与最后二十九个使用的用户密码相关的多个哈希值，以及用于上述 AES 加密的的哈希值。

使用上述技术，我们可以向域控制器请求复制更新，并在获取 Active Directory 中每个账户的密码哈希值时，无需登录域控制器。

### 21.6 总结

本模块提供了 Active Directory 及其相关安全的概述和一些见解。虽然这里提到了并解释了许多技术，但还有许多其他值得探索的技术。

特别应该注意的是，本模块中对操作安全（`opsec`）的关注较少，取决于客户的成熟程度，在执行枚举和横向移动时，如果不盲目执行所示的每一个命令和技术，花些精力避免被检测，这可能是值得的。

![](img/f99f528ca9845f4c256ce54e882b1345_676_0.png)

[+] 其他特定模块参数为：`missing`, `advanced`, `evasion`, `targets`, `ac`

### 列表 734 show 命令的帮助标志

要激活一个模块，请使用 `use` 命令后接模块名称（例如示例中的 `auxiliary/scanner/portscan/tcp`）。此时，提示符将显示该模块。我们可以使用 `back` 退出当前上下文并返回主 `msf5`：

```
msf5 > use auxiliary/scanner/portscan/tcp
```

```
msf5 auxiliary(scanner/portscan/tcp) > back
```

```
msf5 >
```

列表 735 - Metasploit `use` 和 `back` 命令

`back` 的变体是 `previous`，它可以让我们切换到上一个选择的模块而不是返回提示符：

```
msf5 > use auxiliary/scanner/portscan/tcp
```

```
msf5 auxiliary(scanner/portscan/tcp) > use auxiliary/scanner/portscan/syn
```

```
msf5 auxiliary(scanner/portscan/syn) > previous
```

```
msf5 auxiliary(scanner/portscan/tcp) >
```

列表 736 - Metasploit `previous` `previous` 命令

大多数模块在运行之前都需要选项（`show options`）。我们可以使用 `set` 配置选项，并使用 `set` 和 `unset` 分别可以移除全局选项。

```
msf5 auxiliary(scanner/portscan/tcp) > show options
```

模块选项 (`auxiliary/scanner/portscan/tcp`):

| 名称 | 当前设置 | 强制 | 描述 |
|---|---|---|---|
| `CONCURRENCY` | 10 | yes | 每个线程检查的并发端口数 |
| `DELAY` | 0 | yes | 每个线程的连接之间的延迟 |
| `JITTER` | 0 | yes | 延迟抖动因子（按宽度最大值） |
| `PORTS` | 1-1000 | yes | 要扫描的端口（例如 22-25,80,110-900） |
| `RHOSTS` |  | yes | 目标地址或 CIDR 标识符 |
| `THREADS` | 1 | yes | 并发线程数 |
| `TIMEOUT` | 1000 |  | 套接字连接超时时间（毫秒） |

列表 737 - `auxiliary/scanner/portscan/tcp` 的选项

例如，要使用 `scanner/portscan/tcp` 模块对我们的 Windows 工作站进行扫描，必须先用 `set` 命令设置远程主机 IP 地址（`RHOSTS`）。

```
msf5 auxiliary(scanner/portscan/tcp) > set RHOSTS 10.11.0.22
RHOSTS => 10.11.0.22
```

列表 738 - `RHOSTS` 选项

配置好模块后，我们可以运行它：

```
# msf5 auxiliary(scanner/portscan/tcp) > run
```

- [+] 10.11.0.22: - 10.11.0.22:80 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:135 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:139 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:445 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:3389 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:5040 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:9121 - TCP OPEN

[*] 扫描了 1 个主机主机 (100% 完成)

[*] 辅助模块执行完成

列表 730 - 使用 Metasploit 进行端口扫描

### 22.1.2 Metasploit 数据库访问

如果 `postgresql` 服务正在运行，Metasploit 将把发现的主机、服务或凭据的结果和信息记录在一个方便、可访问的数据库中。

在以下列表中，数据库已经填充了我们在上一节运行的 TCP 扫描结果。我们可以使用 `services` 命令显示这些结果：

```
msf5 auxiliary(scanner/portscan/tcp) > services
Services
host             port proto name state info
---- ---- ---- ---- ---- 
10.11.0.22       80   tcp               open
10.11.0.22       135  tcp               open
10.11.0.22       139  tcp               open
10.11.0.22       445  tcp               open
10.11.0.22       3389 tcp               open
10.11.0.22       5040 tcp               open
10.11.0.22       9121 tcp               open
```

列表 740 - 数据库中的 TCP 端口扫描结果

`basic services` 命令显示所有端口，但我们通过端口号 (`-p`)、服务名称 (`-s`) 进行过滤，并在 `services -h` 的帮助输出中查看更多内容。

```
msf5 > services -h
Usage: services -h [-u] [-a] [-r <protocol>] [-p <port1,port2>] [-s <name1,name2>] [-o <filename>]
-a,--addr           添加服务而不是搜索
-d,--delete         删除搜索的服务
-c <col1,col2>      仅显示指定的列
-h,--help           显示此信息
-s,--name           要添加的服务名称
-p,--port           搜索端口列表
-r <protocol>       添加服务的协议类型
-u,--up            仅显示哪些服务在线
-o <file>           将输出发送到 csv 格式的文件
-<column>            按指定列排序
-R,--rhosts         从结果设置 RHOSTS
-S,--search         通过字符串搜索
-U,--update         更新现有服务
```

列表 741 - `services` 命令

除了简单的 tcp 端口扫描器，我们还可以使用 `dbnmap` 封装在 Metasploit 内部执行 `nmap` 并方便访问数据库。`dbnmap` 命令与 `nmap` 语法相同，如下：

```
msf5 > dbnmap [--save] [--help] [nmap options]
msf5 > dbnmap 10.11.0.22 -A -Pn
[*] Nmap: 10.11.0.22 的扫描报告
[*] Nmap: 主机在线 (latency)。
[*] Nmap: 未显示：关闭端口
[*] Nmap: PORT STATE
[*] Nmap: 80/tcp open http
[*] Nmap: http-generator: HTTP
[*] Nmap: http-title: Enterprise
[*] Nmap: 135/tcp open Microsoft RPC
[*] Nmap: 139/tcp open Windows net-ss
[*] Nmap: 445/tcp open microsoft-ds
[*] Nmap: 3389/tcp open Terminal Services
```

列表 742 - 在 Metasploit 中执行 `nmap` 扫描

要显示为止发现的所有主机，可以使用 `hosts` 命令。例如，我们还可以通过 `services -p 445` 列出端口 445 上运行的服务。

```
msf5 > hosts
Hosts
address         mac             name           os_name        os_flavor purpose
-------------- ------------ ------------ ----------------------
10.11.0.22       00:00:2a:ae:3e    Windows Longhorn device
msf5 > services -p 445
Services
=======
host             port proto name            state info
-------------- ---- ---- ------------------ open
10.11.0.22       445    tcp    microsoft-ds open ()
```

列表 743 - 数据库中的主机和服务

为了组织数据库内容，Metasploit 允许我们将信息存储在单独的工作空间（`workspaces`）中。指定工作空间时，只会看到与该空间相关的数据库条目，有助于管理各种枚举尝试。我们可以使用 `workspace` 列出可用的工作空间，或提供工作空间名称作为参数切换到不同的工作空间，如列表 744 所示。

## 使用 Kali Linux 进行渗透测试

```
msf5 > workspace
test
* default
```

```
msf5 > workspace test
[*] workspace: test
```

列表 744 - Metasploit Framework 中的 `workspaces`

要添加或删除工作空间，可以分别使用 `-a` 或 `-d` 后接工作空间名称，依此类推。

### 22.1.3 辅助模块

Metasploit Framework 包含了数百个辅助模块，提供协议枚举、端口扫描、模糊测试、嗅探等功能。模块遵循常见的破折号分隔的分级语法（模块类型/操作系统、厂商、应用或协议/模块名称），这便于探索和使用这些模块。辅助模块适用于许多任务，包括信息收集（`gather/hierarchy` 下）以及各种服务的扫描和枚举（`scanner/hierarchy` 下）。

内容太多无法全部涵盖，我们将演示最常用辅助模块的扫描和操作。作为练习，请探索其他辅助模块，它们是 Metasploit Framework 不可缺的一部分。

要列出所有辅助模块，我们运行 `show auxiliary` 命令。这将呈现所有辅助模块的长列表，如下方的截断输出所示：

```
msf5 > show auxiliary
```

| 名称 | 级别 | 描述 |
|---|---|---|
| `scanner/smb/smb1` | normal | SMBv1 协议检测 |
| `scanner/smb/smb2` | normal | SMB 2.0 协议检测 |
| `scanner/smb/enumshares` | normal | SMB 共享枚举 |
| `scanner/smb/enumusers` | normal | SMB 用户枚举 (SAM 枚举器) |
| `scanner/smb/enumusers_domain` | normal | SMB Domain用户枚举 |
| `scanner/smb/login` | normal | SMB 登录扫描器 |
| `scanner/smb/lookupsid` | normal | SMB 用户枚举 (LookUpSID) |
| `scanner/smb/ms17_01` | normal | MS17-01 SMB RCE 检测 |
| `scanner/smb/version` | normal | SMB 版本检测 |

列表 745 - 列出所有辅助模块

我们可以使用 `search` 来减少这些大量的输出，通过应用、类型、平台等进行过滤。例如，我们可以通过 `search type:auxiliary name:smb` 搜索 SMB 辅助模块，如下列表所示。

```
msf5 > search -h
Usage: search [ options ] <keywords>
```
