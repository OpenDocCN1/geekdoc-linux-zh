
## 表 13.6 `ftp` 命令子集（续）

| 命令 | 功能 |
| :--- | :--- |
| `cd` | 在本地主机上更改目录 |
| `ls` | 获取远程主机上的目录列表 |
| `mdelete` | 在远程主机上删除多个文件 |
| `mget` | 从远程主机检索多个文件 |
| `mkdir` | 在远程主机上创建目录 |
| `mput` | 将多个文件从本地拷贝到远程主机 |
| `open` | 建立到远程主机的连接 |
| `prompt` | 交互提示 |
| `put` (或 send) | 将单个文件从本地拷贝到远程主机 |
| `pwd` | 显示远程主机上的当前工作目录 |
| `rename` | 在远程主机上重命名文件 |
| `rmdir` | 在远程主机上删除目录 |
| `status` | 显示 `ftp` 的状态 |

你可以使用位于本地主机父目录的隐藏文件 `~/-user/.netrc` 来避免每次建立 `ftp` 连接时都输入用户名和密码（与位于远程主机上的 `~/.netrc_hosts` 比较）。

### UNIX

**格式：**

`% machine *host* *login *username* *password *password*`

示例：

```
% cat ~fred/.netrc
machine cuhhmd.hhmi.columbia.edu
login fred password mypassword
```

在此示例中，用户可以使用用户名 `fred` 和密码 `mypassword` 向远程主机 `cuhhmd.hhmi.columbia.edu` 建立 `ftp` 连接。主机名必须是官方 Internet 主机名，即 `/etc/hosts` 文件中主机的第一个条目，而不是别名。

458

由于 `~/-user/.netrc` 文件包含远程主机上的用户密码，该文件不应允许用户（和 `root`）之外的任何人读取。事实上，如果世界或其他组对 `~/-user/.netrc` 有访问权限，该文件将无法运行。（并不是所有的 UNIX 版本都包含此安全特性。在世界世界或组可访问 `~/-user/.netrc` 的情况下仍运行的实现会带来巨大的安全风险。）以下示例展示了到远程主机的 `ftp` 连接，分别带有没有 `~/-user/.netrc` 文件。

### UNIX

**格式：**

`$ ftp [*options*] *`

示例：

```
$ ftp cuhhmd
Connected to cuhhmd.hhmi.columbia.edu.
220 cuhhmd FTP server (Version 4.1 Tue Mar 31 21:45:47 EST 1997) ready.
Name (cuhhmd.hhmi.columbia.edu): fred
Password (cuhhmd.hhmi.columbia.edu:fred) : [password not echoed]
331 Password required for fred.
230 User fred logged in.
ftp>pwd
251 "/usr/users/fred" is current directory.
ftp>bye
221 Goodbye.
$
```

示例：

```
$ cat ~/.netrc
machine cuhhmd.hhmi.columbia.edu username fred password mypassword
$ ftp cuhhmd
Connected to cuhhmd.hhmi.columbia.edu.
220 cuhhmd FTP server (Version 4.1 Tue Mar 31 21:45:47 EST 1997) ready. 331 Password required for fred.
230 User fred logged in.
ftp>pwd
251 "/usr/users/fred" is current directory.
ftp>bye
221 Goodbye
$
```

只有第二个示例使用了 `~/-user/.netrc` 文件。在两个示例中，都在远程主机上执行了 `ftp` 命令 `pwd` 以确定该主机上的当前工作目录。在两个示例中，`ftp` 都通过 `bye` 命令结束，这会注销远程主机用户并返回本地 shell 提示符。

459

`~/-user/.netrc` 文件也可以用于启用匿名 `ftp`；详情请参阅手册页（`man page`）。

我们现在转向建立连接后可以使用的 `ftp` 命令。

### UNIX

示例：

```
ftp>!bob.txt
```

示例：

```
ftp>put (local-file) bob.txt (remote-file) old.txt
```

示例：

```
ftp>put bob.txt
```

示例：

```
ftp>!bob.txt
200 PORT okay. Opening data connection for /tmp/bob.txt (128 bytes), Transfer complete. 211 bytes received in 2 seconds (54 bytes/s)
```

示例：

```
ftp>mget (remote-files) batch.out
237 mget batch.out
```

示例：

```
ftp>status
Connected to cuhhmd.hhmi.columbia.edu Mode: stream; Type: ascii; form: non-print; Structure: file Verbose: on; Bell: off; Prompting: on; Globbing: on Hash mark printing: off; Use of PORT cmds: on
```

示例：

```
ftp>prompt (Interactive mode off)
```

示例：

```
ftp>mput batch.out
```

在第一个示例中，`!bob.txt` 确定文件是否存在于本地主机的当前目录。任何以感叹号（`!`，在 UNIX 术语中被称为 "bang"）开头的命令都会指示 `ftp` 将命令传递给本地主机上的 shell 进行执行；即 `ftp` 会派生出一个新 shell 来执行该命令。在第二个示例中，不带参数的 `put` 会提示 `ftp` 首先请求要从本地主机拷贝的现有文件名，其次是它在远程主机上接收的文件名。然后，本地主机上的 `bob.txt` 被拷贝（`put`）到远程主机上的 `old.txt`。第三个示例 `put bob.txt` 说明了仅给出本地文件名而非远程文件名的情况：文件将以其在本地主机上的相同名称拷贝（`put`）到远程主机。在第四个示例中，`!bob.txt` 通过检查远程主机上 `bob.txt` 是否存在来验证拷贝是否成功。

在第五个示例中，`mget` 从远程主机拷贝（`gets`）多个文件。默认情况下，用户会被提示拷贝每个文件（对比 OpenVMS 命令 `copy`）。你可以通过两种方式之一关闭交互提示。首先，`ftp` 命令提示符会切换交互提示的值；你可以通过 `status` 命令确定当前值（开启或关闭）。其次，你可以在调用 `ftp` 时使用 `-i` 选项，这将抑制交互提示。最后一个示例 `input batch.out` 展示了在关闭交互模式的情况下从本地到远程主机的批量拷贝：所有文件均无注释地拷贝。

在第四个示例中，`ftp` 显示了指示传输字节数和传输速率的诊断信息。这些诊断在所有 `ftp` 传输期间都会显示，但为了简洁，除了第四个示例外均已省略。

460

远程命令执行：`rsh`

除非本地主机被远程主机信任，否则无法从本地主机向远程主机执行命令。对于不受信任的主机，本地用户必须先登录远程主机，然后通过 `telnet` 或 `ftp` 执行命令。`rsh`（远程 shell）工具通过在远程主机上调用 shell，在远程信任主机上执行命令或脚本。任何可以被远程 shell 解析的命令都是有效的。OpenVMS 命令始终由本地节点解析。这一事实在访问文件时不会产生问题，因为 OpenVMS 文件规范可以包含远程节点。例如，OpenVMS 用户想要显示节点 `BOSTON` 的目录内容，可能会输入命令 `DIRECTORY BOSTON:DUA2:[FRED]`。UNIX 用户使用命令 `rsh boston "-fred"` 完成相同的任务。OpenVMS 和 UNIX 命令都很直观。但是，如果本地用户想要查看节点 `BOSTON` 上的交互用户列表呢？

### OpenVMS

示例：

```
DIRECTORY /SYS$OUTPUT
[FRED]
DEFINE USER SYS$OUTPUT
[FRED]
```

### UNIX

示例：

```
rsh boston "who"
```

## 1.3.2 网络通信
