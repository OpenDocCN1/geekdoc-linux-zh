
# Solaris 8 远程命令与认证

Solaris 8 提供了几个用于执行远程登录、远程拷贝和远程命令执行的命令：

- `telnet(1)`—远程网络终端工具
- `ftp(1)`—文件传输协议工具
- `rlogin(1)`—远程登录
- `rcp(1)`—远程拷贝
- `rsh(1)`—远程 shell 执行

`ftp` 和 `telnet` 命令都要求用户使用远程系统上设置的有效用户用户名和密码登录远程系统。`login`、`rcp` 和 `rsh` 命令统称为“r 命令”，它们都将使用远程认证数据库，而不需要用户用户名和密码来验证用户。

## 远程登录

有两个命令提供了通过网络作为本地用户登录远程系统的能力。这些是 `telnet` 命令和 `login` 命令。

### telnet 命令

`telnet` 命令用于通过网络远程登录到系统。用户必须在远程系统上提供有效的用户用户名和密码，因为 `telnet` 命令使用了标准的 Unix 登录/密码认证。

远程系统的主机名或 IP 地址通常作为命令行参数指定。如果未指定，`telnet` 命令将进入交互模式。远程系统会提示输入用户名和密码。以下示例使用 `telnet` 命令通过 `dia` 用户名登录到远程系统 `solaris8`：

```
$ telnet solaris8
Trying 192.168.99.8...
Connected to solaris8.
Escape character is '^]'
SunOS 5.8
login: dia
Password:
Last login: Sat Feb 3 22:34:56 from winnt40
Sun Microsystems Inc. SunOS 5.8 Generic February 2000
$
```

### login 命令

`login` 命令也可以用于通过网络远程登录系统。如果远程认证数据库已妥善设置，用户可能可以在无需提供有效用户名密码的情况下登录。此功能在本章稍后的部分描述。

如果该数据库未设置妥当，用户必须像 `telnet` 命令一样，提供定义的有效用户名和密码。如果远程系统上存在与本地系统相同的用户账户，则不需要指定用户名。如果要使用另一个用户账户，则必须通过 `login` 命令命令行参数指定。以下列表显示了使用 `login` 命令登录远程系统的三个示例。第一个示例中，已设置数据库以允许用户账户 `dla` 登录远程系统。第二个示例中，未设置数据库，并提示输入密码。第三个示例中使用了不同的用户账户 `sarah`，并通过 `-l` 参数指定了用户名。

```
$ rlogin solaris8
Last login: Sat Feb 4 21:32:12 from solaris8
Sun Microsystems Inc. SunOS 5.8 February 2000
$
```

```
$ rlogin solaris8
Password:
Last login: Sat Feb 4 21:33:45 from solaris8
Sun Microsystems Inc. SunOS 5.8 2000
$
```

```
$ rlogin -l sarah solaris8
Last login: Sat Feb 4 22:42:28 from solaris8
Sun Microsystems Inc. SunOS 5.8 2000
$
```

## 远程拷贝

有两个命令可用于系统间的文件拷贝。这些是 `ftp(1)` 命令和 `rcp(1)` 命令。

### ftp 命令

`ftp` 命令通过网络在本地系统和远程系统之间拷贝一个或多个文件。用户必须提供远程系统定义的有效用户名和密码，因为 `ftp` 命令使用了标准的 Unix 登录/密码认证。

远程系统的主机名或 IP 地址通常作为命令行参数指定。如果未指定此地址，`ftp` 命令将进入交互模式。远程系统将提示用户名和密码。

一旦登录远程系统，可以通过相应的子命令在系统间传输文件。要从本地系统拷贝到远程系统，使用 `put` 命令。要从远程系统拷贝到本地系统，使用 `get` 命令。表 10.8 列出了常用的 `ftp` 子命令。

**表 10.8：常用的 ftp 子命令**

| 子命令 | 描述 |
|---|---|
| `?` | 列出 ftp 子命令。 |
| `ascii` | 设置传输为 ASCII（执行行符映射）。ASCII 是默认模式。 |
| `binary` | 设置传输为二进制（不执行行符映射）。 |
| `cd path` | 更改远程目录为路径。 |
| `get remote local` | 将远程系统的文件 `remote` 拷贝到本地系统的文件 `local`。如果没有指定 `local`，则文件在本地系统上具有相同名称。 |
| `hash` | 每发送或接收 8192 字节打印一个井号 (`#`)。 |
| `help subcommand` | 显示子命令的简短描述。 |
| `lcd path` | 更改当前本地目录为路径。 |
| `ls` | 列出远程目录的内容。 |
| `mget meta` | 从远程系统拷贝多个文件到本地系统。文件集由 `meta` 指定，`meta` 是包含一个或多个通配符的表达式。 |
| `mput meta` | 从本地系统拷贝多个文件到远程系统。 |
| `put local remote` | 将本地系统的文件 `local` 复制到远程系统上的文件 `remote`。如果未指定 `remote`，则在远程系统上为文件赋予相同的名称。 |
| `quit` | 退出 ftp 命令。 |

以下示例使用 `ftp` 命令通过 `dla` 用户帐户名访问远程系统 `solaris8`。使用了多种子命令在不同系统之间传输文件：

```
$ ftp solaris8
Connected to solaris8.
220 solaris8 FTP server (SunOS 5.8) ready.
Name (solaris8:dla): dla
331 Password required for dla.
Password:
230 User logged in.
ftp> cd /tmp
250 CWD command successful.
ftp> ls
200 PORT command successful.
150 ASCII data connection for /bin/ls (0 bytes).
ab2.socat.cache
dtdbcache:0
file.txt
mp5eaaNc
mpfna0Fc
mpJaWMc
mpqvaC
ps_data
sdtvolcheck388
226 ASCII Transfer complete.
100 bytes received in 0.0032 seconds (30.14 Kbytes/s)
ftp> lcd /export/home/dla
Local directory now /export/home/dla
ftp> get file.txt
200 PORT command successful.
150 ASCII data connection for xx (3448 bytes).
226 ASCII Transfer complete.
local: file.txt remote: file.txt
3529 bytes received in 0.0044 (776.02 Kbytes/s)
ftp> binary
200 Type set to I.
ftp> mget mp*
mget mp5eanC? n
mget mpfna0Fc? y
200 PORT command successful.
150 ASCII data connection for mpfna0Fc (16198 bytes).
226 ASCII Transfer complete.
local: mpfna0Fc remote: mpfna0Fc
16726 bytes received in 0.0074 seconds (221.89 Kbytes/s)
mget mpjAaWMc? y
200 PORT command successful.
150 ASCII data connection for mpjAaWMc (0 bytes).
226 ASCII Transfer complete.
mget mpqvaOmC? n
ftp> quit
221 Goodbye.
```

### rcp 命令

你可以使用 `rcp(1)` 命令从本地系统将指定的文件复制到远程系统。目标被指定为 `host:path`，其中 `host` 是远程系统的名称，`path` 是目录或文件的完整路径。如果远程系统上使用了不同的用户帐户，则将其指定在 `host` 之前，并用 `@` 符号分隔。`rcp` 命令使用远程认证数据库。

以下列表显示了本地系统上的 `dia` 帐户尝试将文件复制到远程系统中两个不同用户帐户的家目录，因为远程系统上的远程认证数据库不允许本地 `dia` 用户访问远程 `sarah` 用户帐户：

```
$ rcp /tmp/file.txt solaris8:/export/home/dia/file.txt
$ rcp /tmp/file.txt sarah@solaris8:/export/home/sarah/file.txt
$
```

## 远程 shell 执行

`rsh(1)` 命令用于在远程系统上执行命令。`remsh` 命令是 `rsh` 命令的符号链接。

### rsh 命令

`rsh` 命令在远程系统上执行命令。最少需要两个命令行参数：远程主机的名称和要执行的命令。与其他命令一样，它也使用远程认证数据库。如果所需的远程用户帐户与本地用户帐户不同，则使用 `-l` 命令行参数进行标识。在以下示例中，在远程系统 `solaris8` 上对 `/tmp` 目录执行了 `ls`：

```
$ rsh solaris8 "ls /tmp"
ab2.socat.cache
dtdcache_:0
file.txt
mp5caaNc
mpfa0Fc
mpJaAWMc
mpqvaData
ps_data
sdtvolcheck388
$
```

## 远程认证数据库

远程认证数据库用于确定哪些远程主机和用户被视为“受信任”。`rlogin`、`rsh` 和 `rcp` 命令（统称为“r 命令”）使用远程认证数据库。该数据库由两种类型的文件组成：适用于整个系统的 `/etc/hosts.equiv` 文件以及适用于单个用户帐户的 `.rhosts` 文件（后者位于用户帐户的家目录中）。

你使用远程认证数据库来确定远程系统上的用户是否可以使用相同的用户帐户访问本地系统。例如，如果远程系统上的“guest”帐户被授权访问本地系统，然后通过 `rlogin` 命令这样操作，用户将自动登录到本地系统并作为“guest”，无需提供用户帐户和密码。

远程认证程序首先检查远程系统的主机名是否列在 `/etc/hosts.equiv` 文件中。如果列出，则远程认证成功并授予用户访问权限。

如果远程系统的主机名不在列表中，则远程认证将失败。

---

# 练习题

### 第1题

哪些命令使用远程认证数据库？[选择所有适用项]

- a. telnet
- b. rlogin
- c. rcp
- d. ftp
- e. rsh

**答案**：b、c、e 是正确的。`rlogin`、`rcp` 和 `rsh` 命令使用远程认证数据库。`telnet` 和 `ftp` 命令使用用户名和密码。因此，答案 a 和 d 是错误的。

### 第2题

哪个 `mkdir` 命令行参数可以创建父目录？

- a. -P
- b. -c
- c. -p
- d. -m

**答案**：c 是正确的。`-p` 命令行参数可以创建任何父目录。`-P`、`-c` 和 `-m` 不是 `mkdir` 命令的有效命令行参数。因此，答案 a、b 和 d 是错误的。

### 第3题

以下哪些 vi 命令会将字符串 `old` 的所有出现处替换为字符串 `new`？

- a. `:old/s/new/`
- b. `:!/old/new/`
- c. `:%s/old/new/g`
- d. `:1,$s/old/new`

**答案**：c 是正确的。`:%s/old/new/g` 命令会替换全文中所有 `old` 为 `new`。`:old/s/new/` 和 `:1,$s/old/new` 命令会替换每行中第一个 `old` 为 `new`。因此，答案 a 和 d 是错误的。`:!/old/new/` 将无法工作，因为 `!` 用于执行 shell 命令。因此，答案 b 是错误的。

### 第4题

将以下 ftp 子命令与其描述相匹配。

- a. binary — 3. 传输时不映射换行符。
- b. hash — 6. 每传输 8192 个字符打印一个 "#"。
- c. ascii — 4. 传输时映射换行符。
- d. mput — 1. 将多个文件传输到远程系统。
- e. mget — 2. 将多个文件传输到本地系统。
- f. lcd — 5. 更改本地工作目录。

**答案**：a-3, b-6, c-4, d-1, e-2, f-5 是正确的。`binary` 命令设置二进制传输模式（不映射换行符）。`hash` 每传输 8192 字节打印一个 `#`。`ascii` 模式映射传输数据中的换行符。`mput` 子命令将多个文件传输到远程系统。`mget` 子命令将多个文件传输到本地系统。`lcd` 子命令更改本地工作目录。

### 第5题

以下哪项是 `rsh` 命令的正确语法？

- a. `rsh -c command -s system`
- b. `rsh -s system -c command`
- c. `rsh system command`
- d. `rsh command system`
- e. `rsh system:command`

**答案**：c 是正确的。系统名应该在命令之前指定。用空格分隔系统和命令。其他语法选项都是无效的。因此，答案 a、b、d 和 e 都是错误的。

### 第6题

在文件 `abc`、`abc123` 和 `123abc` 的列表中，以下哪一个元字符表达式会选择这些文件中的一个或多个[选择所有适用项]

- a. `abc*`
- b. `?*123`
- c. `*2*`
- d. `???`

**答案**：a、b 和 c 是正确的。`abc*` 会选择 `abc` 和 `abc123`。`?*123` 会选择 `abc123`。`*2*` 会选择 `abc123` 和 `123abc`。`???` 不会选择任何一个指定的文件，因为所有文件名长度均不为3。因此，答案 d 是错误的。

### 第7题

以下哪些 vi 模式在退出时会返回命令模式（Command mode）[选择所有适用项]

- a. Input（输入）
- b. Last Line（末行）
- c. Search（搜索）
- d. Replace（替换）
- e. File control（文件控制）

**答案**：a 和 b 是正确的。Input 和 Last Line 模式在退出时返回命令模式。搜索、替换和文件控制是功能，但它们不是 vi 模式。因此，答案 c、d 和 e 是错误的。

### 第8题

以下哪项是 `rcp` 命令目标文件的正确格式？

- a. `system:file`
- b. `system@file`
- c. `system!file`
- d. `file@system`

**答案**：a 是正确的。`system:file` 是 `rcp` 命令目标文件的正确格式。另一种格式是 `user@system:file`，其中 `user` 指定文件的所有者。其他格式均无效。因此，答案 b、c 和 d 都是错误的。

---

## 参考资料

- Lamb, Linda, *Learning vi* (O'Reilly & Associates, Englewood Cliffs, NJ, 1994), ISBN 0-937175-67-6.
- Mulligan, John P., *Solaris 8 Essential Reference* (New Riders, Indianapolis, IN, 2001), ISBN 0-7357-1007-4.
- Peek, Jerry, Grace Todino, and John Strang, *Learning the UNIX Operating System* (O'Reilly & Associates, Englewood Cliffs, NJ, 1998), ISBN 1-56592-390-1.
- Sorbek, Mark G., *A Practical Guide to Solaris* (Addison-Wesley, Reading, MA, 1999), ISBN 0-201-89548-X.
- Sun Microsystems, *System Reference Manual, Section 1 - User Commands*. 提供纸质版（部件号 806-0624-10）、网页版 docs.sun.com，以及随 Solaris 8 操作系统一起提供的在线文档 AnswerBook2。

---

# 第 11 章：模拟测试 I

本章提供了相关提示，帮助你制定成功的应试策略，包括如何选择正确答案、如何解码歧义、如何在 Solaris 测试框架内工作、如何决定需要记忆的内容，以及如何准备考试。章节末有 57 个与考试 310-011（“Solaris 8 Sun 认证系统管理员，第一部分”）相关的题目。

请记住，要获得认证，你必须通过这次考试和第二次考试（310-012）。第二次考试的模拟测试在第 22 章。

## 问题，问题，还是问题

你心里应该完全没有疑问，你面对的是一个充满特定且有针对性问题的测试。第一部分考试是固定长度的；包含 57 个问题，你将有 90 分钟的时间完成。你需要获得 66% 或以上的分数才能通过考试。

对于这次考试，问题属于四种类型之一：

- 单选题（单个答案）
- 多选题（多个答案）
- 多项匹配（拖放）
- 填空题（自由选择）
