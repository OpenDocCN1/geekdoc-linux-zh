

此命令为切换——再次输入 prompt 即可为本次会话重新打开文件提示。

## 34.2.2 从远程主机下载文件

get 命令的工作方式与 put 类似，但方向相反——指定远程系统上的文件，get 会将其副本保存到本地系统的当前目录中。同样，在下载非文本文件时请先使用 binary。 （你也可以使用 i 下载文本文件，因此在传输文件前始终使用它是一个好习惯；大多数 Linux 系统在连接后会立即将类型设置为 i）。

⇒ 要下载远程系统当前目录中的文件 `INDEX.gz`，并将其保存到你的 `/tmp` 目录，输入：

```
ftp> lcd ~/tmp [RET]
Local directory now /home/james/tmp
ftp> get INDEX.gz [RET]
local: INDEX.gz remote: INDEX.gz
Transferred 10942677 bytes
ftp>
```

**NOTES:** mget 命令的工作方式与 get 类似，但允许使用通配符；与 mput 一样，除非你先使用 `prompt` 命令将其关闭，否则在传输每个文件前都会提示你进行验证。

## 34.3 使用安全 Internet 服务

```
OpenSSH
  DEB: ssh
  RPM: openssh
  WWW: http://www.openssh.com/
```

这些涉及安全加密连接的新方法取代了前面食谱中描述的用于连接到远程系统以及在远程系统之间传输文件的旧方法。当需要或要求增强安全性时，请改用它们代替 `telnet` 和 `ftp`。

你仍然可以使用旧方法，对于本地网络来说可能足够好，但在 Internet 上，安全变体已在大多数地方成为标准——Net 已不再是十年前的安全港湾，实际上，很少有站点再允许 telnet 访问。

以下食谱描述了如何使用 openssh 实现的著名 ssh（“Secure Shell”）协议。OpenSSH 包含对旧的 rlogin、rsh 和 rcp 安全连接工具的当代替代品。

NOTES: 第一次使用其中一个工具连接到远程系统时，你可能会收到一条消息，告知“主机密钥”未在已知主机列表中找到，并询问是否继续连接——回答“yes”。

### 34.3.1 通过安全 Shell 连接到远程主机

使用 ssh 安全地连接到远程系统。它在你作为参数给出的主机名上的远程系统上打开登录连接。

⇒ 要打开到 arctic.example.org 的安全连接，输入：

```
$ ssh arctic.example.org [RET]
ernie@arctic.example.org's password: snowshoe [RET]
Last login: Wed Aug 13 11:39:29 EDT 2003

Welcome to arctic.example.org!

[ernie@arctic ~]
```

在此示例中，用户名 ernie 通过 SSH 连接到系统 arctic.example.org，其密码为“snowshoe”。“~ $”是该系统上的 shell 提示符，他可以在此运行命令，直到通过运行 exit 命令或在 shell 提示符下输入 CTRL-D 退出为止。

如果你在远程系统上的用户名与本地系统上的用户名不同，请使用 -l 选项指定不同的用户名。

⇒ 要使用远程用户名 scout 打开到 arctic.example.org 的安全连接，输入：

```
$ ssh -l scout arctic.example.org [RET]
scout@arctic.example.org's password: igloo [RET]
Last login: Wed Aug 13 13:14:53 EDT 2003

Welcome to arctic.example.org!

You have new mail.
[scout@arctic ~]
```

在此示例中，用户以用户名 scout 登录到 arctic.example.org，其密码为“igloo”。

### 34.3.2 向远程主机进行安全文件复制

使用 scp 在本地系统和远程主机之间进行安全文件复制。它以要复制的文件名和要复制到的文件名作为参数。对于本地系统上的文件，只需像平常一样给出文件名；以以下格式指定远程系统上的文件名：

```
user@remote:filename
```

对于 user，给出你在远程系统上的用户名（如果与本地系统相同，则省略它以及后面的 at 符号 @）。对于 remote，给出要连接到的远程系统的主机名，对于 filename 给出文件在 user 的主目录中应出现的名称。

⇒ 要将 local_html 目录中的文件 index.html 复制到系统 arctic.example.org 上你的账户中的 public_html 目录，输入（全部在一行）：

```
$ scp local_html/index.html arctic.example.org:public_html/index.html [RET]
ernie@arctic.example.org's password: snowshoe [RET]
index.html 100% |********************************| 2365 00:00
$
```

在此示例中，用户在两个系统上的用户名均为 ernie；在 scp 退出前，复制进度会显示在屏幕上。

使用 -r 选项复制整个目录树。

