
```bash
localhost$ ssh -v -l jsmith remotehost.example.com
debug:
SshConfig/sshconfig.c:2838/ssh2_parse_config_ext:
Metaconfig parsing stopped at line 3.
debug:
SshConfig/sshconfig.c:637/ssh_config_set_param_verbose:
Setting variable 'VerboseMode' to 'FALSE'.
debug:
SshConfig/sshconfig.c:3130/ssh_config_read_file_ext:
Read 17 params from config file.
debug: Ssh2/ssh2.c:1707/main: User config file not
found, using defaults. (Looked for
'/home/jsmith/.ssh2/ssh2_config')
debug: Connecting to remotehost.example.com, port 22...
(SOCKS not used)
warning: Connecting to remotehost.example.com failed:
No address associated to the name
```

### Hack 15. 使用 SSH 转义字符切换 SSH 会话

当你从本地主机使用 `ssh` 登录到远程主机后，你可能想返回本地主机执行某些操作，然后再次返回远程主机。在这种情况下，你不需要断开与远程主机的 `ssh` 会话。相反，请按照以下步骤操作。

1. 从本地主机登录到远程主机：

```bash
localhost$ ssh -l jsmith remotehost
```

2. 现在你已连接到远程主机：

```bash
remotehost$
```

3. 要暂时返回本地主机，输入转义字符 `~` 和 `Control-Z`。

当你输入 `~` 时，在按下 `<Control-Z>` 并按回车之前屏幕上不会立即显示。所以，在远程主机上的新行中输入以下按键以使下面操作生效：`~<Control-Z>`

```bash
remotehost$ ~^Z
```

```
[1]+ Stopped ssh -l jsmith remotehost
```

```bash
localhost$
```

4. 现在你已返回本地主机，`ssh` 远程主机客户端会话作为典型的 UNIX 后台作业运行，你可以按如下所示进行检查：

```bash
localhost$ jobs
```

```
[1]+ Stopped ssh -l jsmith remotehost
```

5. 你可以通过将本地主机的后台 `ssh` 远程主机会话作业调到前台，而无需再次输入密码来返回远程主机 `ssh`。

```bash
localhost$ fg %1
```

```
ssh -l jsmith remotehost
```

```bash
remotehost$
```

### Hack 16. 使用 SSH 转义字符查看 SSH 会话统计信息

要获取有关当前 `ssh` 会话的一些有用统计信息，请执行以下操作。

这仅在 `SSH2` 客户端上有效。

1. 从本地主机登录到远程主机。

`localhost$ ssh -l jsmith remotehost`

2. 在远程主机上，输入 `ssh` 转义字符 `~` 后跟 `s`，如下所示。这将显示有关当前 `SSH` 连接的许多有用统计信息。

`remotehost$` [注意：输入时 `~s` 在命令行上不可见。]

```
remote host: remotehost
local host: localhost
remote version: SSH-1.99-OpenSSH_3.9p1
local version: SSH-2.0-3.2.9.1 SSH Secure Shell (non-commercial)
compressed bytes in: 1506
uncompressed bytes in: 1622
compressed bytes out: 4997
uncompressed bytes out: 5118
packets in: 15
packets out: 24
rekeys: 0
Algorithms:
Chosen key exchange algorithm: diffie-hellman-group1-sha1
Chosen host key algorithm: ssh-dss
Common host key algorithms: ssh-dss,ssh-rsa
Algorithms client to server:
密码：aes128-cbc
MAC：hmac-sha1
压缩：zlib

### Linux 技巧
算法 服务器到客户端：
密码：aes128-cbc
MAC：hmac-sha1
压缩：zlib

localhost$

Ajay Kumar Tiwari
```

### 附加 SSH 信息

顺便说一下，要设置基于 SSH 密钥的身份验证，请参考 `openSSH` 和 `SSH2` 教程。

### Linux 技巧

Ajay Kumar Tiwari

## 第 4 章：必备 Linux 命令

### 技巧 17. Grep 命令

`grep` 命令用于在文件中搜索特定文本。这是一个功能非常强大的命令，拥有大量选项。

语法：`grep [options] pattern [files]`

### 如何查找文件中匹配特定关键字的所有行？

在此示例中，`grep` 在 `/etc/passwd` 文件中查找文本 `John` 并显示所有匹配的行。

```bash
# grep John /etc/passwd
```

```
jsmith:x:1082:1082:John Smith:/home/jsmith:/bin/bash
jdoe:x:1083:1083:John Doe:/home/jdoe:/bin/bash
```

选项 `-v` 将显示除匹配项之外的所有行。在下面的示例中，它显示 `/etc/passwd` 中不匹配 `John` 的所有记录。

注意：`/etc/passwd` 中有几行不包含单词 `John`。下面仅显示输出的第一行。

```bash
# grep -v John /etc/passwd
```

```
jbourne:x:1084:1084:Jason Bourne:/home/jbourne:/bin/bash
```

### 特定文件中匹配文本模式的行数是多少？

在下面的示例中，它显示 `/etc/passwd` 文件中包含文本 `John` 的总行数。

```bash
# grep -c John /etc/passwd
```

```
2
```

您还可以通过传递选项 `-cv` 来获取未匹配特定模式的总行数。

```bash
# grep -cv John /etc/passwd
```

```
39
```

### 如何忽略大小写搜索文本？

传递选项 `-i`（忽略大小写），搜索时将忽略大小写。

```bash
# grep -i john /etc/passwd
```

```
jsmith:x:1082:1082:John Smith:/home/jsmith:/bin/bash
jdoe:x:1083:1083:John Doe:/home/jdoe:/bin/bash
```

### 如何在所有子目录中搜索匹配特定模式的文本？

为此使用选项 `-r`（递归）。在下面的示例中，它将忽略大小写地在 `/home/users` 下的所有子目录中搜索文本“John”。

这将以“文件名：匹配模式的行”的格式显示输出。您还可以传递选项 `-l`，它将仅显示匹配模式的文件名。

```bash
# grep -ri john /home/users
```

```
/home/users/subdir1/letter.txt:John, Thanks for your contribution.
/home/users/name_list.txt:John Smith
/home/users/name_list.txt:John Doe
```

```bash
# grep -ril john /root
```

```
/home/users/subdir1/letter.txt
/home/users/name_list.txt
```

Ajay Kumar Tiwari

### 技巧 18. Find 命令

`find` 是根据众多条件在 UNIX 文件系统中查找文件的常用命令。让我们回顾 `find` 命令的一些实践示例。

语法：`find [pathnames] [conditions]`

### 如何查找文件名中包含特定单词的文件？

以下命令查找 `/etc` 目录下文件名中包含 `mail` 的所有文件。

```bash
# find /etc -name "*mail*"
```

### 如何查找大于特定大小的所有文件？

以下命令将列出系统中大于 `100MB` 的所有文件。

```bash
# find / -type f -size +100M
```

### 如何查找最近 x 天未修改的文件？

以下命令将列出当前目录下修改时间超过 `60` 天前 的所有文件。
