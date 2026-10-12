
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

## 22.1.3 辅助模块

Metasploit Framework 包含了数百个辅助模块，提供协议枚举、端口扫描、模糊测试、嗅探等功能。模块遵循常见的破折号分隔的分级语法（模块类型/操作系统、厂商、应用或协议/模块名称），这便于探索和使用这些模块。辅助模块适用于许多任务，包括信息收集（`gather/hierarchy` 下）以及各种服务的扫描和枚举（`scanner/hierarchy` 下）。

内容太多无法全部涵盖，我们将演示最常用辅助模块的扫描和操作。作为练习，请探索其他辅助模块，它们是 Metasploit Framework 不可缺的一部分。

要列出所有辅助模块，我们运行 `show auxiliary` 命令。这将呈现所有辅助模块的长列表，如下方的截断输出所示：

```
msf5 > show auxiliary
```

| 名称 | 级别 | 描述 |

|---|---|---|

| scanner/smb/smb1 | normal | SMBv1 协议检测 |

| scanner/smb/smb2 | normal | SMB 2.0 协议检测 |

| scanner/smb/enumshares | normal | SMB 共享枚举 |

| scanner/smb/enumusers | normal | SMB 用户枚举 (SAM 枚举器) |

| scanner/smb/enumusers_domain | normal | SMB Domain用户枚举 |

| scanner/smb/login | normal | SMB 登录扫描器 |

| scanner/smb/lookupsid | normal | SMB 用户枚举 (LookUpSID) |

| scanner/smb/ms17_01 | normal | MS17-01 SMB RCE 检测 |

| scanner/smb/version | normal | SMB 版本检测 |

列表 745 - 列出所有辅助模块

我们可以使用 `search` 来减少这些大量的输出，通过应用、类型、平台等进行过滤。例如，我们可以通过 `search type:auxiliary name:smb` 搜索 SMB 辅助模块，如下列表所示。

```
msf5 > search -h
Usage: search [ options ] <keywords>
```

# 使用 Kali Linux 2.0 进行渗透测试

选项：

`-h`

`-o <file>`

`-S <string>`

显示此帮助信息

将输出以 csv 格式发送到文件

用于行过滤的搜索字符串

- 关键字：

  - `aka` 具有匹配别名（also-known-as）名称的模块

  - `author` 由此作者编写的模块

  - `arch` 影响此架构的模块

  - `bid` 具有匹配 Bugtrag ID 的模块

  - `cve` 具有匹配 CVE ID 的模块

- `target` 影响此目标的模块

  - `type` 特定类型的模块（利用程序、载荷、编码器、逃逸）

示例：

`search cve:2089 type:exploit`

```
msf5 > search type:auxiliary name:smb

匹配的模块
```

| 名称 | 评级 | 描述 |

|---|---|---|

| auxiliary/admin/oracle/ora_ntl_stealer | normal | Oracle SMB 继攻击执行 |

| auxiliary/admin/smb/check_dir_file | normal | SMB 扫描检查文件/目录 |

| auxiliary/admin/smb/delete_file | normal | SMB 文件删除工具 |

| auxiliary/admin/smb/download_file | normal | SMB 文件下载工具 |

756 - 搜索 SMB 辅助模块

在用 `use` 调用模块后，我们可以按照以下方式请求其更多信息：

```
msf5 > use scanner/smb/smb2
msf5 auxiliary(scanner/smb/smb2) > info
```

> 名称: SMB 2.0 协议检测

模块: auxiliary/scanner/smb/smb2

许可证: Metasploit Framework 许可证 (BSD)

评级: Normal

提供者：

hdm <xhdm.io>

检查支持：

是

| 名称 | 当前设置 | 是否需要 | 描述 |

|---|---|---|---|
