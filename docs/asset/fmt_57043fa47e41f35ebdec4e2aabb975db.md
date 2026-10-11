
`alias -s ....='cd ../../'`

`alias -s .....='cd ../../../'`

`alias -s ......='cd ../../../..'`

```

### 技巧 10：显示过去的日期和时间

以下是显示过去日期的各种方式：

```bash
$ date --date='3 seconds ago'

$ date --date='1 day ago'

$ date --date="1 month ago"

$ date --date="1 year ago"

$ date --date="yesterday"

$ date --date="10 months 2 day ago"
```

# 技巧 11. 显示未来的日期和时间

以下示例展示了如何显示未来的日期和时间。

```
$ date

Thu Jan 1 08:30:07 PST 2009

$ date --date='3 seconds'

Thu Jan 1 08:30:12 PST 2009

$ date --date='4 hours'

Thu Jan 1 12:30:17 PST 2009

$ date --date='tomorrow'

Fri Jan 2 08:30:25 PST 2009

$ date --date='1 day'

Fri Jan 2 08:30:31 PST 2009

$ date --date='1 days'

Fri Jan 2 08:30:38 PST 2009

$ date --date='2 days'

Sat Jan 3 08:30:43 PST 2009

$ date --date='1 month'

Sun Feb 1 08:30:48 PST 2009

$ date --date='1 week'

Thu Jan 8 08:30:53 PST 2009

$ date --date='2 months'

Sun Mar 1 08:30:58 PST 2009

$ date --date='2 years'

Sat Jan 1 08:31:03 PST 2011

$ date --date='next day'

Fri Jan 2 08:31:10 PST 2009
```

`$ date --date="-1 days ago"`
`Fri Jan 2 08:31:15 PST 2009`
`$ date --date="this Wednesday"`
`Wed Jan 7 00:00:00 PST 2009`

![](img/340b68128e85f9b34d5bae9c5ff0cdd8_28_0.png)

## 第 3 章：SSH 客户端命令

### 技巧 12. 识别 SSH 客户端版本

有时可能需要识别你当前运行的 SSH 客户端及其对应的版本号。使用 `ssh -V` 来识别版本号。请注意 Linux 自带了 `OpenSSH`。

以下示例表明该系统正在使用 `OpenSSH`：

```
$ ssh -V

OpenSSH_3.9p1, OpenSSL 0.9.7a Feb 19 2003
```

以下示例表明该系统正在使用 `SSH2`：

```
$ ssh -V

ssh: SSH Secure Shell 3.2.9.1 (non-commercial version)

on i686-pc-linux-gnu
```

### 技巧 13. 使用 SSH 登录远程主机

当你第一次从本地主机登录到远程主机时，它会显示一条“host key not found”（未找到主机密钥）的消息，你可以输入“yes”来继续。远程主机的主机密钥将被添加到你家目录下的 `.ssh2/hostkeys` 目录下，如下所示。

```
localhost$ ssh -l jsmith remotehost.example.com

Host key not found from database.

Key fingerprint:

xabie-dezbc-manud-bardt-saty-limit-nexiu-jambl-title-jarde-tumum
```

你可以通过运行 `% ssh-keygen -F publickey.pub on the keyfile.` 来获取公钥指纹。

```
Are you sure you want to continue connecting (yes/no)? Yes
Host key saved to
/homesmith/.ssh2/hostkeys/key_22_remotehost.example.com.pub
host key for remotehost.example.com, accepted by jsmith Mon May 25 18:30:50 2009
```

当你第二次从本地主机登录远程主机时，它将直接登录，而不会再次提示。

由于某些原因，如果远程主机的主密钥在你第一次登录后发生了变化，你可能会看到如下警告，这可能是因为远程主机更新了密钥，或者有人正在进行中间人攻击。在这种情况下，最好的做法是联系系统管理员以确认该主机密钥是否正确。

```
localhost$ ssh -l jsmith remotehost.example.com

@@ WARNING: REMOTE HOST IDENTIFICATION FOR 'remotehost.example.com' HAS CHANGED! @@

ED25519 fingerprint is xabie-dezbc-manud-bardt-saty-limit-nexiu-jambl-title-jarde-tumum

REMOTE HOST KEY HAS CHANGED!

NO ACCESS IS POSSIBLE!

If YOU ARE CERTAIN YOU ARE CONNECTING TO THIS HOST, run

    "ssh-keygen -R remotehost.example.com" -- and then try.
```

要解决这个问题，你可以运行：

```bash
ssh-keygen -R remotehost.example.com
```

算法服务器到客户端：
加密: `aes128-cbc`
MAC: `hmac-sha1`
压缩: `zlib`
`localhost$`

顺带一下，要设置基于 SSH 密钥认证，请参考 `openSSH` 和 `SSH2` 教程。

## 第 4 章：常用 Linux 命令

### 技巧 17：Grep 命令

`grep` 命令用于在文件中搜索特定文本。此工具非常强大。

语法：`grep [options] 模式 [files]`

### 我如何找到文件中所有匹配特定关键词的行？

在这个示例中，`grep` 在 `/etc/passwd` 文件中查找文本 "John" 并显示匹配的行。

```
# grep /etc/passwd

smith:x:1082:1082:John Smith:/home/jsmith:/bin/bash

djoe:x:1083:1083:John Doe:/home/joe:/bin/bash
```

选项 `-v` 将显示 `/etc/password` 中所有不匹配 `John` 的行。在下面的示例中，它显示 `/etc/password` 中所有不包含单词 "John" 的记录。注意：`/etc/password` 中有几行不包含该 

```
# grep -v John /etc/passwd

jbourne:x:1084:1084:Jason Bourne:/home/jbourne:/bin/bash
```

### 特定文件中有多少行匹配了文本模式？

在下面的示例中，它显示了 `/etc/passwd` 文件中包含文本 "John" 的行总数。

```
# grep -c John /etc/passwd
```

你也可以通过传递选项 `-cv` 获取不匹配特定模式的行总数。

```
# grep -cv John /etc/passwd
```

### 如何忽略大小写的情况下搜索文本？

传递选项 `-i`（忽略大小写），它将在搜索时忽略大小写。

```
# grep -i john /etc/passwd

jsmith:x:1082:1082:John Smith:/home/jsmith:/bin/bash

jdoe:x:1083:1083:John Doe:/home/jdoe:/bin/bash
```

### 我如何搜索所有子目录中匹配特定模式的文本？

为此目的，请使用选项 `-r`（递归）。在下面的示例中，它将在 `/home/users` 下的所有子目录下忽略大小写搜索文本 "John"。这将以“文件名: 行内容”的格式显示匹配模式的输出。你也可以传递选项 `-l` 选项，它将只显示匹配模式的文件名。

```
# grep -ri john /home/users
```
