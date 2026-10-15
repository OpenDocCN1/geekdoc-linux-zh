
- 2. **像往常一样登录到你的远程账户。**

- 3. **完成后，关闭连接。**

```
telnet> close <Return>
```

这通常会将你从远程账户注销并退出 `telnet`。你应该看到 UNIX shell 提示符：

```
$
```

### 15.6 连接到 Guest 账户

通常，你必须在使用 `telnet` 连接的任何远程主机上拥有账户。然而，互联网上创建了一些特殊的 `telnet` 账户来为公众提供服务。登录此类账户有两种方式。

第一种——也许是最常见的方法——要求你使用 `telnet` 连接到主机计算机，然后使用特殊的登录名称和密码登录到该账户。（许多系统不需要密码。）例如，美国国家航空航天局（NASA）维护一个名为“Spacelink”的公共服务，提供有关 NASA 过去、当前和计划活动的信息。你可以使用 `telnet` 连接到此服务：

```
$ telnet spacelink.msfc.nasa.gov <Return>
```

当你到达服务器时，它会提示你登录：

```
login:
```

使用的登录名是 `guest`；该特定服务不需要密码。

第二种方法是通过由数字指定的特殊“端口”使用 `telnet` 登录服务器。通常无需提供登录名或密码。例如，密歇根大学维护一个提供地理信息（包括美国城镇和城市的纬度、经度、海拔和邮政编码）的服务器。你可以通过以下命令访问此服务器：

```
$ telnet martini.eecs.umich.edu 3000 <Return>
```

注意数字 `3000`；这是端口号。

这些命令都是在 UNIX 提示符后输入的，并且每个命令都以 **Return** 结束。`host` 代表远程主机的地址。

**远程登录命令 (UNIX shell 提示符)**

| 命令 | 描述 |
| :--- | :--- |
| `rlogin host` | 登录到名为 `host` 的远程 UNIX 计算机 |
| `telnet host` | 登录到名为 `host` 的远程计算机 |
| `telnet` | 启动 `telnet` 程序 |

**Telnet 命令 (Telnet 提示符)**

| 命令 | 描述 |
| :--- | :--- |
| `open host` | 打开与计算机 `host` 的连接 |
| `?` | 打印 `telnet` 帮助 |
| `close` | 关闭与远程主机的连接 |
| `quit` | 退出 `telnet` 会话 |

- 1. 如果你在远程 UNIX 机器上有一个账户，使用 `rlogin` 登录到该账户。
- 2. 如果你在连接到网络的非 UNIX 机器上有一个账户，使用 `telnet` 登录到该账户。
- 3. 使用 `telnet` 登录 NASA 的“Spacelink”公共服务器。该服务器上有哪些类型的信息可用？
- 4. 使用 `telnet` 登录密歇根大学的地理服务器。关于你居住的城市或城镇，有哪些类型的信息可用？

## 16 教程：文件传输

`rcp`（“远程复制”）和 `ftp`（“文件传输协议”）都允许你在拥有账户的两个计算机系统之间传输文件。`rcp` 工具专为在两个 UNIX 系统之间工作而设计；而 `ftp` 还可以从非 UNIX 主机获取文件。此外，`ftp` 还可用于从公共文件服务器获取文件。

### 16.1 运行 rcp

在本节中，你将学习如何使用 `rcp` 从远程 UNIX 主机获取文件。要使 `rcp` 正常工作，必须满足以下三个条件：

- 你必须在远程 UNIX 主机上拥有账户。
- 两台主机必须相互“信任”。
- 你必须有复制该文件的权限。

假设满足这些条件，复制文件的过程非常简单：

- 输入 `rcp` 命令，指定远程主机和远程文件，然后是本地主机和新文件名。例如，如果你想从远程 UNIX 主机 `farhost.xyz.edu` 复制文件 `myfile`，你应输入：

```bash
$ rcp farhost.xyz.edu:myfile .:mycopy
```

- 注意，不需要密码。如果你在远程主机上没有账户，或者主机之间不相互信任，`rcp` 工具将直接拒绝工作。

### 16.2 运行 ftp

在本节中，你将学习如何使用 `ftp` 从远程主机（无论是 UNIX 还是非 UNIX 计算机，且你拥有账户）复制文件。

1. **启动 ftp 程序。**
   - `$ ftp` (回车)
   - 你将收到 ftp 提示符：`ftp>`

2. **输入 `open` 命令，后跟远程机器的 Internet 地址。** 因此，如果你在 `farhost.xyz.edu` 上有账户，请键入：
   - `ftp>` `open farhost.xyz.edu` (回车)
   - `ftp` 程序将尝试连接到远程主机。如果连接成功，远程主机将提示你输入登录名：

```text
Connected to farhost.xyz.edu.
220 farhost.xyz.edu FTP server (Version4.179) ready.
Name (farhost.xyz.edu):
```

3. **输入你的登录名。** 如果远程账户和本地账户的登录名不同，请务必使用远程账户的登录名。例如，如果你在远程主机上有一个名为 `smithj` 的账户，你应键入：
   - `Name (farhost.xyz.edu):` `smithj` (回车)
   - *注意：在此处输入你的登录名。除非你的实际登录名确实是 `smithj`，否则不要输入 "smithj"。*
   - 远程主机将提示你输入密码：

```text
331 Password required for smithj
Password:
```

4. **输入你的密码。** 当然，输入时密码不会在屏幕上显示。
   - `Password:` `XXXXXXXX`
   - *注意：在此处输入你的密码；它不会显示在屏幕上。*
   - 登录成功时你会收到通知：

```text
230 User smithj logged in.
ftp>
```

### 16.3 ftp 帮助

`ftp` 程序接受几十种命令。幸运的是，其中一条命令是 `help`，它列出并描述了一组 `ftp` 命令。

- 在 `ftp` 提示符下输入 `help` 命令。有两种方法可以做到。要么键入单词 `help`，要么键入单个问号 `?`：
  - `ftp> ?` (回车)

- 计算机将返回一个命令列表：

| | | |
| :--- | :--- | :--- |
| `account` | `dir` | `put` |
| `append` | `disconnect` | `rmdir` |
| `ascii` | `form` | `runique` |
| `binary` | `glob` | `send` |
| `bell` | `hash` | `sendport` |
| `bye` | `help` | `status` |
| `case` | `lcd` | `struct` |
| `cd` | `ls` | `sunique` |
| `cdup` | `macdef` | `tenex` |
| `close` | `mdelete` | `trace` |
| `cr` | `mdir` | `type` |
| `delete` | `mode` | `user` |
| `debug` | `pwd` | `verbose` |
| `get` | | |
| `lls` | | |

*(注：由于 OCR 表格碎片化，根据标准 FTP 命令和网格布局，列表中出现的命令包括：account, dir, put, append, disconnect, rmdir, ascii, form, runique, binary, glob, send, bell, hash, sendport, bye, help, status, case, lcd, struct, cd, ls, sunique, cdup, macdef, tenex, close, mdelete, trace, cr, mdir, type, delete, mode, user, debug, pwd, verbose, get, nput, quit, lls, nmap。 部分 OCR 条目混乱如 "$", "$$", "nput" (可能是 "put" 或 "nput" 的非标准变体), "nmap" (可能是 "nmap" 或 "map"?), "tenex", "sunique"。 以下是基于通常在这些教科书中看到的列格式对命令的清理表示，尽可能保留 OCR 中发现的唯一标识符，但纠正明显错误如根据上下文建议的 "nput" -> "put"，然而 "nput" 不是标准命令，可能是 "put" 的误读或特定变体。 观察网格：*
