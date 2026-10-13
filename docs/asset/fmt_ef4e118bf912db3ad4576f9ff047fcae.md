
# 来自 401

C 下面的 C shell 示例统计了当前目录下以 `.c` 结尾的每个文件的行数。注意其语法与 Bourne 和 Korn shell 执行相同循环的示例有何不同。

```
foreach file ( *.c )
wc -l $file
end
```

`repeat` 命令根据指定的次数重复执行其随后的单条命令。下面的示例将打印 500 次“我不会在教室里嚼口香糖”。

```
@ repetition = 500
repeat $repetition echo "I will not chew gum in class."
```

## 属性

请参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| 可用性 | SUNWcsu |

## 参见

```
break(1), csh(1), ksh(1), sh(1), attributes(5)
```

# from — 显示新到达邮件的发送者和日期

### 概要

```
/usr/ucb/from [-s sender] [username]
```

## 描述

`from` 输出你邮箱文件中的邮件头行，以显示邮件来自何处。如果你指定了 `username`，则将检查 `username` 的邮箱而不是你自己的。

- `sender` 仅显示由 `sender` 发送的邮件头。

## 示例

下面的示例显示了当前用户的头行。

```
castle%
From <IMAP4.psudo.sims> Fri Aug 28 12:30:14 1998
From winsor Fri Aug 28 12:15:01 1998
From winsor Fri Aug 28 12:30:01 1998
From winsor Fri Aug 28 12:30:02 1998
From winsor Fri Aug 28 12:55:01 1998
From winsor Fri Aug 28 12:56:53 1998
From winsor Fri Aug 28 13:04:41 1998
From winsor Fri Aug 28 13:04:53 1998
From winsor Fri Aug 28 13:05:37 1998
From lp Tue Sep 29 13:11:29 1998
From lp Thu Oct 1 10:38:46 1998
castle%$
```

在接下来的示例中，有人尝试使用 `from` 命令来显示另一个用户的头行。

```
castle% from ray
Can't open /var/mail/ray
castle%
```

在接下来的示例中，超级用户检查了用户 `ray` 的头行。

## 用方法

关于遇到大于或等于 2 Gbytes (`2**31 bytes`) 文件时 `from` 的行为，请参见 `largefile(5)` 的描述。

## 文件

```
/var/spool/mail/*
```

## 属性

请参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| 可用性 | SUNWfac |

## 参见

`biff(1)`, `mail(1)`, `attributes(5)`, `largefile(5)`

# ftp — 文件传输程序

### 概要

```
/usr/bin/ftp [-dgintv] [hostname]
```

## 描述

`ftp` 命令是互联网标准文件传输协议（FTP）的用户界面。使用 `ftp` 在与远程网络站点之间传输文件。
你可以在命令行上指定 `ftp` 与之通信的客户端主机。如果你这样做了，`ftp` 会立即尝试与该主机上的 FTP 服务器 建立连接；否则，`ftp` 将进入其命令解释器并等待指令。当 `ftp` 等待命令时，它会显示提示符 `ftp> `

使用以下步骤通过 `ftp` 命令将文件从你的本地系统传输到远程系统。

> 注意 — 你可能需要在每个系统中都有一个账户，并在 `/.hosts` 文件中有一个条目才能使用文件传输程序。某些系统允许任何以匿名身份登录并在密码提示符处输入用户名的用户具有只读权限。

如果你有 NIS 或 NIS+ 账户，可以使用你的登录名和网络密码通过 `ftp` 访问远程系统。

1. 输入 `ftp` 并按回车。显示 `ftp> ` 提示符。
2. 输入 `open-remote-name` 并按回车。显示系统连接消息，并要求输入用户名。
3. 输入你在远程系统上的账户用户名并按回车。如果需要密码，会要求你输入。
4. 输入你在远程系统上的账户密码（如果需要）并按回车。显示系统登录消息和 `ftp> ` 提示符。
5. 输入 `bin` 设置二进制格式，或输入 `asc` 设置 ASCII 格式并按回车。文件类型已设置（默认是 ASCII）。
6. 输入 `put local-filename destination-filename` 并按回车。显示文件传输消息和 `ftp> ` 提示符。
7. 输入 `quit` 并按回车。显示告别消息和命令提示符。

下面的示例建立了从系统 `oak` 到系统 `elm` 的 `ftp` 连接，指定 ASCII 格式，将 `oak` 上的文件 `quest` 放入 `elm` 上的 `/tmp/quest` 目录，并退出会话。

```
oak% ftp
ftp> open elm
Connected to elm
220 elm FTP server (UNIX V Release 4.0) ready.
Name (elm): ignatz
Password required for ignatz.
Password:
User ignatz logged in.
ftp> asc
ftp> put quest /tmp/quest
200 Transfer complete.
150 data connection opened.
ftp> quit
226 Closing connection.
221 Goodbye.
```
