
# Linux 黑客 by Mr Ajay Kumar Tiwari

![](img/d85fdc87049f4b892fa74b89bf49ed67_0_0.png)

- 使用 `mke2fs` 格式化分区

## 引言

> “世界上只有10种人——懂二进制的人，不懂的人，以及懂灰码的人”

> — 极客

![](img/d85fdc87049f4b892fa74b89bf49ed67_10_0.png)

我是阿贾伊·库马尔·提瓦里，本书的作者

我在多种语言上进行了深入编程，`C` 是我最喜欢的。我在基础设施方面做了大量工作，包括 `Linux` 系统管理、`DBA`、网络、硬件和存储（`EMC`）。

## 前言

又一个技巧合集？是的！如果你刚刚完成了第一门管理员课程或正在寻找更有效的工作方法，“Linux 技巧”电子书是一个很好的起点。这些实用技巧简洁、写得好且易于阅读。

做得好 - 我会向我的学生推荐这本电子书。

> — 教授 博士 弗里茨·梅纳，FH Südwestfalen，德国

（多款 `Vim` 插件的作者，包括 `bash-support` `vim` 插件）

## 版本

| 版本 | 1.0 |
| :--- | :--- |
| 日期 | 25-Mar-2015 |
| 修订 | 首版 |

## 第1章：强大的 `CD` 命令技巧

`cd` 是 `UNIX` 会话期间使用最频繁的命令之一。本章提到的 6 个 `cd` 命令技巧将立即提升你的生产力，并使从命令行导航目录结构变得更容易。

### Hack 1. 使用 `CDPATH` 为 `cd` 命令定义基本目录

如果你经常执行 `cd` 进入特定父目录的子目录，你可以设置 `CDPATH` 为父目录，然后在不给出父目录路径的情况下执行 `cd` 进入子目录，如下所述。

```
[ramesh@dev-db ~]# pwd
/home/ramesh
[ramesh@dev-db ~]# cd mail
-bash: cd: mail: No such file or directory
```

[注意：这是在当前目录下查找 `mail` 目录]

```
[ramesh@dev-db ~]# export CDPATH=/etc
[ramesh@dev-db ~]# cd mail
/etc/mail
```

[注意：这是在 `/etc` 下查找 `mail`，而不是在当前目录下]

```
[ramesh@dev-db /etc/mail]# pwd
/etc/mail
```

要使此更改永久生效，请将 `export CDPATH=/etc` 添加到你的 `~/.bash_profile`

与 `PATH` 变量类似，你可以在 `CDPATH` 变量中添加多个目录条目，用 `:` 分隔，如下所示。

```
export CDPATH=.:~/:/etc:/var
```

此技巧在以下情况下非常有帮助：

- `Oracle` `DBA` 经常在 `$ORACLE_HOME` 下工作，可以将 `CDPATH` 变量设置为 `oracle` 主目录

- `Unix` 系统管理员经常在 `/etc` 下工作，可以将 `CDPATH` 变量设置为 `/etc`

- 开发人员经常在项目目录 `/home/projects` 下工作，可以将 `CDPATH` 变量设置为 `/home/projects`

- 终端用户经常访问其主目录下的子目录，可以将 `CDPATH` 变量设置为 `~`（主目录）

### Hack 2. 使用 `cd` 别名有效向上导航目录

当你向上导航一个非常长的目录结构时，你可能会使用 `cd ....\` 并根据要向上移动的目录数量使用多个 `..\`，如下所示。

```
# mkdir -p
/tmp/very/long/directory/structure/that/is/too/deep
# cd /tmp/very/long/directory/structure/that/is/too/deep
# pwd
/tmp/very/long/directory/structure/that/is/too/deep
# cd ../../../../
```

```
# pwd
/tmp/very/long/directory/structure
```

不要执行 `cd ../../../../` 来向上导航四级，使用以下三种别名方法之一：

#### 方法 1：使用“..n”向上导航目录

在下面的示例中，`..4` 用于向上移动 4 级目录，`..3` 用于向上移动 3 级目录，`..2` 用于向上移动 2 级目录。将以下别名添加到你的 `~/.bash_profile` 并重新登录。

```
alias ..="cd .."
alias ..2="cd ../.."
alias ..3="cd ../../.."
alias ..4="cd ../../../.."
alias ..5="cd ../../../../.."
```

```
# cd
/tmp/very/long/directory/structure/that/is/too/deep
# ..4
```

[注意：使用 `..4` 向上移动 4 级目录]

```
# pwd
/tmp/very/long/directory/structure/
```

#### 方法 2：仅使用点向上导航目录

在下面的示例中，`.....`（五个点）用于向上移动 4 级目录。

输入 5 个点来向上移动 4 个目录结构非常容易记住，因为当你输入前两个点时，你在想“向上移动一个目录”，之后每多一个点，就向上移动一级。所以，使用 `....`（四个点）来

向上移动 3 级目录并使用 `..`（两个点）向上移动 1 级目录。将以下别名添加到你的 `~/.bash_profile` 并重新登录，使 `.....`（五个点）能正常工作。

```
alias ..="cd .."
```

```
alias ...="cd ../.."
alias ....="cd ../../.."
alias .....="cd ../../../.."
alias ......="cd ../../../../.."
```

```
# cd /tmp/very/long/directory/structure/that/is/too/deep
# .....
# pwd
/tmp/very/long/directory/structure/
```

[注意：使用 `.....`（五个点）向上移动 4 级目录]

#### 方法 3：使用 `cd` 后跟连续的点向上导航目录

以下示例中，`cd.....`（`cd` 后跟五个点）用于向上移动 4 级目录。将 5 个点用于向上移动 4 个目录结构非常容易记住，因为当你输入前两个点时，你在想“向上移动一个目录”，之后每增加一个点，就向上移动一级。因此，使用 `cd....`（`cd` 后跟四个点）向上移动 3 级目录，使用 `cd...`（`cd` 后跟三个点）向上移动 2 级目录。将以下别名添加到你的 `~/.bash_profile` 并重新登录，使上述 `cd.....`（五个点）能正常工作。

```
alias cd..="cd .."
alias cd...="cd ../.."
```

```
alias cd...="cd ../.."
alias cd....="cd ../../.."
alias cd.....="cd ../../../.."
# cd /tmp/very/long/directory/structure/that/is/too/deep
# cd.....
```

[注意：使用 `cd.....` 向上移动 4 级目录]

```
# pwd
/tmp/very/long/directory/structure
```

#### 方法 5：使用 `cd` 后跟数字向上导航目录

以下示例中，`cd4`（`cd` 后跟数字 4）用于向上移动 4 级目录。

```
alias cd1="cd .."
alias cd2="cd ../.."
alias cd3="cd ../../.."
alias cd4="cd ../../../.."
alias cd5="cd ../../../../.."
```

### 技巧 3. 使用单个命令执行 `mkdir` 和 `cd`

有时当你创建新目录时，你可能会立即 `cd` 到新目录以执行某些工作，如下所示。

```
# mkdir -p /tmp/subdir1/subdir2/subdir3
# cd /tmp/subdir1/subdir2/subdir3
# pwd
/tmp/subdir1/subdir2/subdir3
```

将 `mkdir` 和 `cd` 合并到单个命令中不是很好吗？将以下内容添加到 `.bash_profile` 并重新登录。

```
$ vi .bash_profile
function mkdircd () { mkdir -p "$@" && eval cd "\"\$@\""; }
```

现在，使用单个命令同时执行 `mkdir` 和 `cd`，如下所示：

```
# mkdircd /tmp/subdir1/subdir2/subdir3
```

[注意：这会自动创建目录并 `cd` 到它]

```
# pwd
/tmp/subdir1/subdir2/subdir3
```

### 技巧 4. 使用“`cd -`”在最后两个目录之间切换



你可以使用`cd -`在最后两个当前目录之间切换，如下所示。

```
# cd /tmp/very/long/directory/structure/that/is/too/deep
# cd /tmp/subdir1/subdir2/subdir3
# cd -
# pwd
/tmp/very/long/directory/structure/that/is/too/deep
# cd -
# pwd
/tmp/subdir1/subdir2/subdir3
# cd -
# pwd
/tmp/very/long/directory/structure/that/is/too/deep
```

### 技巧 5. 使用`dirs`、`pushd`和`popd`操作目录栈

你可以使用目录栈将目录推入其中，然后稍后从栈中弹出目录。本示例中使用了以下三个命令。

- `dirs`：显示目录栈
- `pushd`：将目录推入栈
- `popd`：从栈中弹出目录并`cd`到它

`dirs`总是会打印当前目录，然后是栈的内容。即使目录栈为空，`dirs`命令仍会仅打印当前目录，如下所示。

```
# popd
-bash: popd: directory stack empty
# dirs
~
# pwd
/home/ramesh
```

如何使用`pushd`和`popd`？让我们先创建一些临时目录并将它们推送到目录栈，如下所示。

```
# mkdir /tmp/dir1
# mkdir /tmp/dir2
# mkdir /tmp/dir3
# mkdir /tmp/dir4
```

```
# cd /tmp/dir1
# pushd .
# cd /tmp/dir2
# pushd .
# cd /tmp/dir3
# pushd .
# cd /tmp/dir4
# pushd .
```

```
# dirs
```

`/tmp/dir4 /tmp/dir4 /tmp/dir3 /tmp/dir2 /tmp/dir1`

[注意：`dir`命令输出的第一个目录（`/tmp/dir4`）始终是当前目录，而不是来自栈的内容。]

此时，目录栈包含以下目录：

- `/tmp/dir4`
- `/tmp/dir3`
- `/tmp/dir2`
- `/tmp/dir1`

最后推送到栈的目录将在顶部。当你执行`popd`时，它会`cd`到栈中顶部的目录条目并将其从栈中移除。如上所示，最后推送到栈的目录是`/tmp/dir4`。因此，当我们执行`popd`时，它会`cd`到`/tmp/dir4`并将其从目录栈中移除，如下所示。

```
# popd
```

```
# pwd
```

`/tmp/dir4`

[注意：执行上述`popd`后，目录栈包含：

`/tmp/dir3`

`/tmp/dir2`

`/tmp/dir1`]

```
# popd
```

```
# pwd
```

`/tmp/dir3`

[注意：执行上述`popd`后，目录栈包含：

`/tmp/dir2`

`/tmp/dir1`]

```
# popd
```

```
# pwd
/tmp/dir2
```

[注意：执行上述`popd`后，目录栈包含：

`/tmp/dir1`]

```
# popd
# pwd
/tmp/dir1
```

[注意：执行上述`popd`后，目录栈为空！]

```
# popd
-bash: popd: directory stack empty
```

### 技巧 6. 使用“`shopt -s cdspell`”自动纠正`cd`命令中输入错误的目录名

使用`shopt -s cdspell`自动纠正`cd`命令中的拼写错误，如下所示。如果你打字不好且经常出错，这将非常有帮助。

```
# cd /etc/mall
-bash: cd: /etc/mall: No such file or directory
# shopt -s cdspell
# cd /etc/mall
# pwd
/etc/mail
```

[注意：我不小心输入了`mall`而不是`mail`，

`cd`自动纠正了它]

## 第 2 章：日期操作

### 技巧 7. 设置系统日期和时间

要更改系统日期，请使用：

```
# date {mmddhhmi yyyy.ss}
```

- `mm` – 月份
- `dd` – 日期
- `hh` – 24 小时格式
- `mi` – 分钟
- `yyyy` – 年份
- `ss` – 秒

例如，将系统日期设置为 2008 年 1 月 31 日，下午 10:19，53 秒

```
# date 013122192009.53
```

你也可以使用`set`参数更改系统日期，如下所示。

```
# date 013122192009.53
# date +%Y%m%d -s "20090131"
# date -s "01/31/2009 22:19:53"
# date -s "31 JAN 2009 22:19:53"
# date -s "31 JAN 2009 22:19:53"
```

仅设置时间：

```
# date +%T -s "22:19:53"
```

```
# date +\%T\%p -s "10:19:53PM"
```

### 技巧 8. 设置硬件日期和时间

在设置硬件日期和时间之前，请确保操作系统日期和时间已如 hack#7 所示适当设置。

根据系统日期设置硬件日期和时间，如下所示：

```
# hwclock --systohc
```

```
# hwclock --systohc --utc
```

使用`hwclock`不带任何参数，查看当前硬件日期和时间：

```
# hwclock
```

检查时钟文件以验证系统是否设置为 UTC：

```
# cat /etc/sysconfig/clock
```

```
ZONE="America/Los_Angeles"
UTC=false
ARC=false
```

### 技巧 9. 以特定格式显示当前日期和时间

以下是以各种格式显示当前日期和时间的不同方法：

```
$ date
```

`Thu Jan 1 08:19:23 PST 2009`

```
$ date --date="now"
```

`Thu Jan 1 08:20:05 PST 2009`

```
$ date --date="today"
```

`Thu Jan 1 08:20:12 PST 2009`

```
$ date --date='1970-01-01 00:00:01 UTC +5 hours' +%s
```

`18001`

```
$ date '+Current Date: %m/%d/%y%nCurrent Time:%H:%M:%S'
```

`Current Date: 01/01/09`

`Current Time:08:21:41`

```
$ date +"%d-%m-%Y"
```

`01-01-2009`

```
$ date +"%d/%m/%Y"
```

`01/01/2009`

```
$ date +"%A,%B %d %Y"
```

`Thursday,January 01 2009`

以下是可以传递给`date`命令的不同格式选项：

- `%D` 日期 (mm/dd/yy)
- `%d` 月中的天数 (01..31)
- `%m` 月份 (01..12)
- `%y` 年份最后两位数字 (00..99)
- `%a` 本地简写星期几名称 (Sun..Sat)
- `%A` 本地完整星期几名称，长度可变 (Sunday..Saturday)
- `%b` 本地简写月份名称 (Jan..Dec)
- `%B` 本地化完整月份名称，长度可变 (一月..十二月)
- `%H` 小时 (00..23)
- `%I` 小时 (01..12)
- `%Y` 年 (1970...)

### 技巧 10. 显示过去的日期和时间

以下是显示过去日期和时间的不同方法：

```
$ date --date='3 seconds ago'
Thu Jan 1 08:27:00 PST 2009
$ date --date="1 day ago"
Wed Dec 31 08:27:13 PST 2008
$ date --date="1 days ago"
Wed Dec 31 08:27:18 PST 2008
$ date --date="1 month ago"
Mon Dec 1 08:27:23 PST 2008
$ date --date="1 year ago"
Tue Jan 1 08:27:28 PST 2008
$ date --date="yesterday"
Wed Dec 31 08:27:34 PST 2008
$ date --date="10 months 2 day ago"
Thu Feb 28 08:27:41 PST 2008
```

### 技巧 11. 显示未来的日期和时间

以下示例展示如何显示未来的日期和时间。



## 第 3 章：SSH 客户端命令

### Hack 12. 识别 SSH 客户端版本

有时可能需要识别当前正在运行的 SSH 客户端及其对应的版本号。使用`ssh -V`来识别版本号。请注意 Linux 自带 OpenSSH。

以下示例表明该特定系统使用的是 OpenSSH：

```
$ ssh -V
```

`OpenSSH_3.9p1, OpenSSL 0.9.7a Feb 19 2003`

以下示例表明该特定系统使用的是 SSH2：

```
$ ssh -V
```

`ssh: SSH Secure Shell 3.2.9.1 (non-commercial version)`

`on i686-pc-linux-gnu`

### Hack 13. 使用 SSH 登录远程主机

第一次从本地主机登录到远程主机时，它会显示主机密钥未找到的消息，你可以输入 "yes" 继续。远程主机的主机密钥将被添加到你主目录下的`.ssh2/hostkeys`目录中，如下所示。

```
localhost$ ssh -l jsmith remotehost.example.com
```

主机密钥未在数据库中找到。

密钥指纹：

`xabie-dezbc-manud-bartd-satsy-limit-nexiu-jambl-title-jarde-tuxum`

你可以通过运行以下命令获取公钥的指纹

```
% ssh-keygen -F publickey.pub
```

在密钥文件上。

```
Are you sure you want to continue connecting (yes/no)? Yes
Host key saved to
/home/jsmith/.ssh2/hostkeys/key_22_remotehost.example.com.pub
host key for remotehost.example.com, accepted by jsmith Mon
May 26 2008 16:06:50 -0700
jsmith@remotehost.example.com password:
remotehost.example.com$
```

第二次从本地主机登录到远程主机时，它只会提示输入密码，因为远程主机密钥已添加到 ssh 客户端的已知主机列表中。

```
localhost$ ssh -l jsmith remotehost.example.com
jsmith@remotehost.example.com password:
remotehost.example.com$
```

由于某种原因，如果你在第一次登录后远程主机的主机密钥发生了更改，你可能会收到如下警告消息。

这可能是由于各种原因，例如：

- 系统管理员升级/重新安装了远程主机的 SSH 服务器
- 有人正在进行恶意活动等，

在对以下消息说 "yes" 之前，最好的做法是联系你的系统管理员，弄清为什么会收到主机密钥已更改的消息，并验证它是否是正确的主机密钥。

```
localhost$ ssh -l jsmith remotehost.example.com
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
@WARNING: HOST IDENTIFICATION HAS CHANGED!@
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
IT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!
Someone could be eavesdropping on you right now (man-in-the-middle attack)!
It is also possible that the host key has just been changed.
Please contact your system administrator.
Add correct host key to
"/home/jsmith/.ssh2/hostkeys/key_22_remotehost.example.com.pub"
to get rid of this message.
Received server key's fingerprint:
xabie-dezbc-manud-bartd-satsy-limit-nexiu-jambl-title-arde-tuxum
You can get a public key's fingerprint by running
% ssh-keygen -F publickey.pub
on the keyfile.
Agent forwarding is disabled to avoid attacks by corrupted servers.
Are you sure you want to continue connecting (yes/no)? yes
Do you want to change the host key on disk (yes/no)? yes
Agent forwarding re-enabled.
Host key saved to
/home/jsmith/.ssh2/hostkeys/key_22_remotehost.example.com.pub
host key for remotehost.example.com, accepted by jsmith Mon
May 26 2008 16:17:31 -0700
jsmith@remotehost.example.com's password:
remotehost$
```

### Hack 14. 调试 SSH 客户端会话

有时有必要查看调试消息以排查任何 SSH 连接问题。如以下所示，将`-v`（小写 `v`）选项传递给`ssh`以查看 ssh 调试消息。

#### 无 SSH 客户端调试消息的示例：

```
localhost$ ssh -l jsmith remotehost.example.com
warning: Connecting to remotehost.example.com failed:
No address associated to the name
```

#### 有 SSH 客户端调试消息的示例：



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



# Linux 文件管理与脚本技巧

### 如何查找最近 x 天内修改过的文件？

以下命令将列出当前目录下最近两天内修改过的所有文件。

```
find . -mtime -2
```

### 如何删除扩展名为 `*.tar.gz` 且大于 100MB 的所有归档文件？

请在执行以下命令时小心，以免误删文件。最佳做法是先使用 `ls -l` 执行相同命令，以确保您知道在执行带 `rm` 的命令时哪些文件将被删除。

```
find / -type f -name *.tar.gz -size +100M -exec ls -l {} \;
```

```
find / -type f -name *.tar.gz -size +100M -exec rm -f {} \;
```

### 如何归档最近 x 天未修改过的所有文件？

以下命令查找 `/home/jsmith` 目录下最近 60 天未修改过的所有文件，并在 `/tmp` 下创建格式为 `ddmmyyyy_archive.tar` 的归档文件。

```
find /home/jsmith -type f -mtime +60 | xargs tar -cvf /tmp/`date '+%d%m%Y'_archive.tar`
```

顺便说一下，您可以使用 `midnight commander` GUI，这是一个功能强大的基于文本的 Unix 文件管理器，来执行许多文件相关活动（包括查找文件）。

### 技巧 19. 抑制标准输出和错误消息

有时在调试 `shell` 脚本时，您可能不想看到标准输出或标准错误消息。如以下所示使用 `/dev/null` 来抑制输出。

#### 使用 `> /dev/null` 抑制标准输出

当您调试 `shell` 脚本时，这非常有帮助，您不想显示 `echo` 语句，只想查看错误消息。

```
cat file.txt > /dev/null
```

```
./shell-script.sh > /dev/null
```

#### 使用 `2> /dev/null` 抑制标准错误

当您只想查看标准输出而不想查看错误消息时，这也很有帮助。

```
cat invalid-file-name.txt 2> /dev/null
```

```
./shell-script.sh 2> /dev/null
```

### 技巧 20. `join` 命令

`join` 命令基于公共字段合并两个文件中的行。

在下面的示例中，我们有两个文件 – `employee.txt` 和 `salary.txt`。两者都有 `employee-id` 作为公共字段。因此，我们可以使用 `join` 命令按 `employee-id` 合并这两个文件中的数据，如下所示。

```
$ cat employee.txt
100 Jason Smith
200 John Doe
300 Sanjay Gupta
400 Ashok Sharma
```

```
$ cat bonus.txt
100 $5,000
200 $500
300 $3,000
400 $1,250
```

```
$ join employee.txt bonus.txt
100 Jason Smith $5,000
200 John Doe $500
300 Sanjay Gupta $3,000
400 Ashok Sharma $1,250
```

### 技巧 21. 更改大小写

#### 将文件转换为全大写

```
$ cat employee.txt
100 Jason Smith
200 John Doe
300 Sanjay Gupta
400 Ashok Sharma
$ tr a-z A-Z < employee.txt
100 JASON SMITH
200 JOHN DOE
300 SANJAY GUPTA
400 ASHOK SHARMA
```

#### 将文件转换为全小写

```
$ cat department.txt
100 FINANCE
200 MARKETING
300 PRODUCT DEVELOPMENT
400 SALES
$ tr A-Z a-z < department.txt
100 finance
200 marketing
300 product development
400 sales
```

### 技巧 22. `xargs` 命令

`xargs` 是一个非常强大的命令，它将命令的输出作为另一个命令的参数。以下是一些关于如何有效使用 `xargs` 的实用示例。

1. 当您尝试使用 `rm` 删除太多文件时，您可能会收到错误消息：`/bin/rm Argument list too long` – Linux。使用 `xargs` 避免此问题。

```
find ~ -name '*.log' -print0 | xargs -0 rm -f
```

2. 获取 `/etc/` 下所有 `*.conf` 文件的列表。有多种方法可以获得相同的结果。以下示例仅用于演示 `xargs` 的使用。此示例中 `find` 命令的输出通过 `xargs` 一次一个地传递给 `ls -l`。

```
find /etc -name "*.conf" | xargs ls -l
```

3. 如果您有一个包含要下载的 URL 列表的文件，可以按如下所示使用 `xargs`。

```
cat url-list.txt | xargs wget -c
```

4. 查找所有 `jpg` 图像并将其归档。

```
find / -name *.jpg -type f -print | xargs tar -cvzf images.tar.gz
```

5. 将所有图像复制到外部硬盘驱动器。

```
ls *.jpg | xargs -n1 -i cp {} /external-hard-drive/directory
```

### 技巧 23. `sort` 命令

`sort` 命令对文本文件的行进行排序。以下是基于以下示例文本文件对 `sort` 命令的几种实用使用示例，该文件以以下格式包含员工信息：`employee_name:employee_id:department_name`。

```
$ cat names.txt
Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
```

#### 按升序对文本文件进行排序

```
$ sort names.txt
Alex Jason:200:Sales
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Nisha Singh:500:Sales
Sanjay Gupta:400:Support
```

#### 按降序对文本文件进行排序

```
$ sort -r names.txt
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
Madison Randy:300:Product Development
Emma Thomas:100:Marketing
Alex Jason:200:Sales
```

#### 对冒号分隔的文本文件按第 2 个字段（`employee_id`）排序

```
$ sort -t: -k 2 names.txt
Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
```

#### 对制表符分隔的文本文件按第 3 个字段（`department_name`）排序并抑制重复

```
$ sort -t: -u -k 3 names.txt
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Alex Jason:200:Sales
Sanjay Gupta:400:Support
```

#### 按第 3 个字段（数字用户 ID）对 `passwd` 文件进行排序

```
$ sort -t : -k 3n /etc/passwd | more
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
```



`daemon:x:2:2:daemon:/sbin:/sbin/nologin`

`adm:x:3:4:adm:/var/adm:/sbin/nologin`

`lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin`

### 按 IP 地址对 `/etc/hosts` 文件进行排序

```
$ sort -t . -k 1,1n -k 2,2n -k 3,3n -k 4,4n /etc/hosts
```

`127.0.0.1 localhost.localdomain localhost`

`192.168.100.101 dev-db.thegeekstuff.com dev-db`

`192.168.100.102 prod-db.thegeekstuff.com prod-db`

`192.168.101.20 dev-web.thegeekstuff.com dev-web`

`192.168.101.21 prod-web.thegeekstuff.com prod-web`

### 将 `sort` 与其他命令结合使用

- `ps -ef | sort` : 对进程列表的输出进行排序

- `ls -al | sort +4n` : 按文件大小升序列出文件。 即按第 5 个字段排序并先显示最小的文件。

- `ls -al | sort +4nr` : 按文件大小降序列出文件。 即按第 5 个字段排序并先显示最大的文件。

### Hack 24. `uniq` 命令

`uniq` 命令通常与 `sort` 命令结合使用，因为 `uniq` 仅从已排序的文件中删除重复项。 即为了使 `uniq` 正常工作，所有重复条目都应位于相邻行。 以下是一些常见示例。

1. 当你有一个包含重复条目的员工文件时，可以执行以下操作来删除重复项。

```
$ sort namesd.txt | uniq
```

```
$ sort -u namesd.txt
```

2. 如果你想知道有多少行是重复的，请执行以下操作。 以下示例中的第一个字段表示为该特定行找到的重复次数。 因此，在此示例中，以 `Alex` 和 `Emma` 开头的行在 `namesd.txt` 文件中出现了两次。

```
$ sort namesd.txt | uniq -c
```

`2`

`2`

`1`

`1`

`1`

`Alex Jason:200:Sales`

`Emma Thomas:100:Marketing`

`Madison Randy:300:Product Development`

`Nisha Singh:500:Sales`

`Sanjay Gupta:400:Support`

3. 以下仅显示重复的条目。

```
$ sort namesd.txt | uniq -cd
```

`2 Alex Jason:200:Sales`

`2 Emma Thomas:100:Marketing`

### Hack 25. `cut` 命令

`cut` 命令可用于仅显示文本文件或其他命令输出的特定列。

以下是一些示例。

### 从冒号分隔的文件中显示第 1 个字段（员工姓名）

```
$ cut -d: -f 1 names.txt
```

`Emma Thomas`

`Alex Jason`

`Madison Randy`

`Sanjay Gupta`

`Nisha Singh`

### 从冒号分隔的文件中显示第 1 和第 3 个字段

```
$ cut -d: -f 1,3 names.txt
```

`Emma Thomas:Marketing`

`Alex Jason:Sales`

`Madison Randy:Product Development`

`Sanjay Gupta:Support`

`Nisha Singh:Sales`

### 仅显示文件中每行的前 8 个字符

```
$ cut -c 1-8 names.txt
```

`Emma Tho`

`Alex Jas`

`Madison`

`Sanjay G`

`Nisha Si`

### 其他 `cut` 命令示例

- `cut -d: -f1 /etc/passwd` 显示系统中所有用户的 `unix` 登录名。

- `free | tr -s ' ' | sed '/^Mem/!d' | cut -d" " -f2` 显示系统上可用的总内存。

### Hack 26. `stat` 命令

`stat` 命令可用于检查单个文件或文件系统的状态/属性。

显示文件或目录的统计信息。

```
$ stat /etc/my.cnf
```

```
File:
Size:
Device:
Access:
(0/
Access:
Modify:
Change:
`/etc/my.cnf’
346 Blocks: 16 IO Block: 4096regular file
801h/2049dInode: 279856Links: 1
(0644/-rw-r--r--) Uid: (0/root)Gid:
  root)
2009-01-01 02:58:30.000000000 -0800
2006-06-01 20:42:27.000000000 -0700
2007-02-02 14:17:27.000000000 -0800
```

```
$ stat /home/ramesh
```

`File:` `/home/ramesh’`

`Size:` `4096` `Blocks:` `8` `IO Block:`

`4096` `directory`

`Device:` `803h/2051d` `Inode:` `5521409` `Links:` `7`

`Access:` `(0755/drw xr-xr-x)` `Uid:` `( 401/ramesh)` `Gid:` `( `

`401/ramesh)`

`Access:` `2009-01-01 12:17:42.000000000 -0800`

`Modify:` `2009-01-01 12:07:33.000000000 -0800`

`Change:` `2009-01-01 12:07:33.000000000 -0800`

### 使用选项 `-f` 显示文件系统的状态

```
$ stat -f /
```

`File:`

`ID:`

`Blocks:`

`1876998`

`Inodes:`

`"/"`

`0` `Namelen:` `255` `Type:` `ext2/ext3`

`Total:` `2579457` `Free:` `2008027` `Available:`

`  Size:` `4096`

`Total:` `1310720` `Free:` `1215892`

### Hack 27. `diff` 命令

`diff` 命令比较两个不同的文件并报告差异。 输出非常晦涩，不易直接阅读。

语法：`diff [options] file1 file2`

与旧文件相比，我的新文件中修改了什么？

`diff` 命令中的选项 `-w` 将在执行比较时忽略空白。

在以下 `diff` 输出中：

- 行上方 `–`，表示 `diff` 命令中第一个文件（即 `name_list.txt`）发生的更改。

- 行下方 `–`，表示 `diff` 命令中第二个文件（即 `name_list_new.txt`）发生的更改。 属于第一个文件的行以 `<` 开头，第二个文件的行以 `>` 开头。

```
# diff -w name_list.txt name_list_new.txt
```

`2c2,3`

`< John Doe`

`–`

`> John M Doe`

`> Jason Bourne`

### Hack 28. 显示用户的总连接时间

`ac` 命令将显示有关用户连接时间的统计信息。

### 当前登录用户的连接时间

使用选项 `-d`，它将按天分解输出。 在此示例中，我今天已登录系统超过 6 小时。

`12` 月 `1` 日，我登录了大约 `1` 小时。

```
$ ac -d
```

```
Dec 1
Dec 2
Dec 3
Dec 4
Today
total
total
total
total
total
1.08
0.99
3.39
4.50
6.10
```

### 所有用户的连接时间

要显示所有用户的连接时间，请使用 `-p`，如下所示。 请注意，这表示各个用户的累计连接时间。

```
$ ac -p
```

`john`

`madison`

`sanjay`

`nisha`

`  3.64`

`0.06`

`  88.17`

` 105.92`

`45`

`ramesh`

`total 309.21`

`111.42`

### 特定用户的连接时间

要获取特定用户的连接时间报告，请执行以下操作：

```
$ ac -d sanjay
```

`Jul 2`

`Aug 25`

`Sep 3`

`Sep 4`

`Dec 24`

`Dec 29`

`Today`

`total`

`total`

`total`

`total`

`total`

`total`

`total`

`12.85`

`5.05`

`1.03`

`5.37`

`8.15`

`1.42`

`2.95`

## 第 5 章：`PS1`、`PS2`、`PS3`、`PS4` 和 `PROMPT_COMMAND`

### Hack 29. `PS1` - 默认交互提示

如下所示，可以修改 Linux 上的默认交互提示，使其更有用且更具信息性。 在以下示例中，默认的 `PS1` 为 `"\s-\v\$"`，它显示 shell 名称和版本号。 让我们更改此默认行为，以显示用户名、主机名和当前工作目录名称，如下所示。



```
-bash-3.2$
export PS1="\u@\h \w> "
ramesh@dev-db ~> cd /etc/mail
ramesh@dev-db /etc/mail>
```

[注意：提示符已更改为“username@hostname current-dir>”格式]

以下 `PS1` 代码在此示例中使用：

- `\u` – 用户名
- `\h` – 主机名
- `\w` - 当前目录的完整路径。 请注意，当你在主目录中时，这将仅显示 `~`，如上所示

请注意，`PS1` 的值末尾有一个空格。 我个人更喜欢在提示符末尾加一个空格以提高可读性。

通过将 `export PS1="\u@\h \w> "` 添加到 `.bash_profile`（或）`.bashrc` 中，如下所示，使此设置永久生效。

### Linux 技巧

Ajay Kumar Tiwari

```
ramesh@dev-db ~> vi ~/.bash_profile
```

```
ramesh@dev-db ~> vi ~/.bashrc
```

[注意：请将 `export PS1="\u@\h \w> "` 添加到上述文件之一中]

请参考下一章详细了解 `PS1` 用法的多个实用示例。

### Hack 30. PS2 - 续行交互提示

一个很长的命令可以通过在行尾加上 `\` 来拆分为多行。 多行命令的默认交互提示是 `>`。 让我们使用 `PS2` 环境变量将此默认行为更改为显示 `"continue->"`，如下所示。

```
ramesh@dev-db ~> myisamchk --silent --force --fast --update-state \
> --key_buffer_size=512M --sort_buffer_size=512M \
> --read_buffer_size=4M --write_buffer_size=4M \
> /var/lib/mysql/bugs/*.MYI
```

[注意：这使用了续行提示的默认 `>` ]

```
ramesh@dev-db ~> export PS2="continue-> "
```

```
ramesh@dev-db ~> myisamchk --silent --force --fast --update-state \
continue-> --key_buffer_size=512M --sort_buffer_size=512M \
continue-> --read_buffer_size=4M --write_buffer_size=4M \
continue-> /var/lib/mysql/bugs/*.MYI
```

[注意：这使用了修改后的 `"continue-> "` 作为续行提示]

我发现当我使用 `\` 将长命令拆分为多行时，这样非常有帮助且易于阅读。 我也见过一些人不喜欢拆分长命令。

### Hack 31. PS3 - shell 脚本中 "select" 使用的提示

您可以使用 `PS3` 环境变量为 shell 脚本中的 `select` 循环定义自定义提示，如下所述。

#### 未使用 PS3 的 shell 脚本及输出：

```
ramesh@dev-db ~> cat ps3.sh
select i in mon tue wed exit
do
  case $i in
  mon) echo "Monday";;
  tue) echo "Tuesday";;
  wed) echo "Wednesday";;
  exit) exit;;
  esac
done
ramesh@dev-db ~> ./ps3.sh
1) mon
2) tue
3) wed
4) exit
#? 1
Monday
#? 4
```

[注意：这显示了 `select` 命令提示的默认 `"#?"` ]

#### 使用 PS3 的 shell 脚本及输出：

```
ramesh@dev-db ~> cat ps3.sh
PS3="Select a day (1-4): "
select i in mon tue wed exit
do
  case $i in
  mon) echo "Monday";;
  tue) echo "Tuesday";;
  wed) echo "Wednesday";;
  exit) exit;;
  esac
done
```

```
ramesh@dev-db ~> ./ps3.sh
1) mon
2) tue
3) wed
4) exit
Select a day (1-4): 1
Monday
Select a day (1-4): 4
```

[注意：这显示了修改后的 `"Select a day (1-4):"` 作为 `select` 命令提示]

### Hack 32. PS4 - 由 "set -x" 用于前缀跟踪输出

`PS4` shell 变量定义了在调试模式下执行 shell 脚本时显示的提示，如下所示。

#### 未使用 PS4 的 shell 脚本及输出：

```
ramesh@dev-db ~> cat ps4.sh
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
```

```
ramesh@dev-db ~> ./ps4.sh
  ++ echo 'PS4 demo script'
PS4 demo script
++ ls -l /etc/
++ wc -l
243
++ du -sh /home/ramesh
48K/home/ramesh
```

[注意：使用 `set -x` 跟踪输出时，这显示了默认的 `"++"` ]

#### 使用 PS4 的 shell 脚本及输出：

下面在 `ps4.sh` 中定义的 `PS4` 包含以下两个代码：

- `$0` - 表示脚本的名称
- `$LINENO` - 显示脚本内的当前行号

```
ramesh@dev-db ~> cat ps4.sh
export PS4='$0.$LINENO+ '
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
ramesh@dev-db ~> ./ps4.sh
../ps4.sh.3+ echo 'PS4 demo script'
PS4 demo script
../ps4.sh.4+ ls -l /etc/
51
../ps4.sh.4+ wc -l
243
../ps4.sh.5+ du -sh /home/ramesh
48K/home/ramesh
```

[注意：使用 `set -x` 跟踪输出时，这显示了修改后的 `"{script-name}.{line-number}+"` ]

### Hack 33. PROMPT_COMMAND

Bash shell 在显示 `PS1` 变量之前执行 `PROMPT_COMMAND` 的内容。

```
ramesh@dev-db ~> export PROMPT_COMMAND="date +%k:%m:%S"
22:08:42
ramesh@dev-db ~>
```

[注意：这在不同的行上显示 `PROMPT_COMMAND` 和 `PS1` 输出]

如果您想在同一行上显示 `PROMPT_COMMAND` 的值与 `PS1`，请使用 `echo -n`，如下所示。

```
ramesh@dev-db ~> export PROMPT_COMMAND="echo -n [$(date +%k:%m:%S)]"
[22:08:51]ramesh@dev-db ~>
```

[注意：这在同一行上显示 `PROMPT_COMMAND` 和 `PS1` 输出]

## Chapter 6: Colorful and Functional Shell Prompt Using PS1

### Hack 34. 在提示中显示用户名、主机名和目录基名

此示例中的 `PS1` 在提示中显示以下三个信息：

- `\u` – 用户名
- `\h` – 主机名
- `\W` – 当前工作目录的基名

```
-bash-3.2$ export PS1="\u@\h \W> "
ramesh@dev-db ~> cd /etc/mail
ramesh@dev-db mail>
```

### Hack 35. 在提示中显示当前时间

在 `PS1` 环境变量中，您可以通过指定格式 `$(linux_command)` 直接执行任何 Linux 命令。 在以下示例中，命令 `$(date)` 被执行以在提示中显示当前时间。

```
ramesh@dev-db ~> export PS1="\u@\h [\$(date +%k:%m:%S)]> "
ramesh@dev-db [11:09:56]>
```

您还可以使用 `\t` 以 `hh:mm:ss` 格式显示当前时间，如下所示：

```
ramesh@dev-db ~> export PS1="\u@\h [\t]> "
ramesh@dev-db [12:42:55]>
```

您还可以使用 `\@` 以 12 小时 `am/pm` 格式显示当前时间，如下所示：



```
ramesh@dev-db ~> export PS1="[\@] \u@\h> "
```

```
[04:12 PM] ramesh@dev-db>
```

### Hack 36. 在提示中显示任何命令的输出

您可以在提示中显示任何 Linux 命令的输出。 以下示例在命令提示中以 `|` 管道 分隔显示三项：

- `\!`: 命令的历史编号
- `\h`: 主机名
- `$kernel_version`: 来自 `$kernel_version` 变量的 `uname -r` 命令的输出
- `\?`: 上一个命令的状态

```
ramesh@dev-db ~> kernel_version=$(uname -r)
```

```
ramesh@dev-db ~> export PS1="\!|\h|$kernel_version|\?> "
```

```
473|dev-db|2.6.25-14.fc9.i686|0>
```

### Hack 37. 更改提示的前景色

以蓝色显示提示，同时显示用户名、主机和当前目录信息

```
$ export PS1="\e[0;34m\u@\h \w> \e[m "
```

[注意：这适用于浅蓝色提示]

```
$ export PS1="\e[1;34m\u@\h \w> \e[m "
```

[注意：这适用于深蓝色提示]

- `\e[`: 表示颜色提示的开始
- `x;ym`: 表示颜色代码。 使用下面提到的颜色代码值。
- `\e[m`: 表示颜色提示的结束

#### 颜色代码表：

| 颜色 | 代码 |
|------|------|
| 黑色 | `0;30` |
| 蓝色 | `0;34` |
| 绿色 | `0;32` |
| 青色 | `0;36` |
| 红色 | `0;31` |
| 紫色 | `0;35` |
| 棕色 | `0;33` |

[注意：用 `1` 替换 `0` 以获得深色]

使颜色更改永久生效，请将以下行添加到您的 `~/.bash_profile` 或 `~/.bashrc` 中

```
$ vi ~/.bash_profile
```

```
STARTCOLOR='\e[0;34m';
ENDCOLOR="\e[0m"
export PS1="$STARTCOLOR\u@\h \w> $ENDCOLOR"
```

### Hack 38. 更改提示的背景色

通过在 `PS1` 提示中指定 `\e[{code}m` 来更改背景色，如下所示。

```
$ export PS1="\e[47m\u@\h \w> \e[m "
```

[注意：这适用于浅灰色背景]

背景和前景的组合。

```
$ export PS1="\e[0;34m\e[47m\u@\h \w> \e[m "
```

[注意：这适用于浅蓝色前景和浅灰色背景]

将以下内容添加到您的 `~/.bash_profile` 或 `~/.bashrc` 中以使上述背景和前景颜色永久生效。

```
$ vi ~/.bash_profile
STARTFGCOLOR='\e[0;34m';
STARTBGCOLOR="\e[47m"
ENDCOLOR="\e[0m"
export PS1="$STARTFGCOLOR$STARTBGCOLOR\u@\h \w> $ENDCOLOR"
```

通过使用以下背景颜色进行尝试并选择最符合您口味的一种：

- `\e[40m`
- `\e[41m`
- `\e[42m`
- `\e[43m`
- `\e[44m`
- `\e[45m`
- `\e[46m`
- `\e[47m`

### Hack 39. 在提示中显示多种颜色

您还可以在同一提示中显示多种颜色。 将以下函数添加到您的 `~/.bash_profile` 中

```
function prompt {
    local BLUE="\[\033[0;34m\]"
    local DARK_BLUE="\[\033[1;34m\]"
    local RED="\[\033[0;31m\]"
    local DARK_RED="\[\033[1;31m\]"
    local NO_COLOR="\[\033[0m\]"
    case $TERM in
    xterm*|rxvt*)
    TITLEBAR='\[\033]0;\u@\h:\w\007\]'
    ;;
    *)
    TITLEBAR=""

    ;;
esac
PS1="\\u@\\h [\\t]> "
PS1="${TITLEBAR}\
$BLUE\\u@\\h $RED[\\t]>$NO_COLOR "
PS2='continue-> '
PS4='$0.$LINENO+ '
}
```

### Linux 技巧

Ajay Kumar Tiwari

您可以重新登录以使更改生效，或按如下所示 `source .bash_profile`。

```
$ ./.bash_profile
```

```
$ prompt
```

```
ramesh@dev-db [13:02:13]>
```

### Hack 40. 使用 tput 更改提示符颜色

您也可以按如下所示使用 `tput` 更改 `PS1` 提示符的颜色：

```
$ export PS1="[$(tput bold)$(tput setb 4)$(tput setaf 7)]\u@\h:\w $ [$(tput sgr0)]"
```

`tput` 颜色功能：

- `tput setab [1-7]` - 使用 ANSI 转义设置背景颜色
- `tput setb [1-7]` - 设置背景颜色
- `tput setaf [1-7]` - 使用 ANSI 转义设置前景颜色
- `tput setf [1-7]` - 设置前景颜色

`tput` 文本模式功能：

- `tput bold` - 设置粗体模式
- `tput dim` - 打开半亮模式
- `tput smul` - 开始下划线模式
- `tput rmul` - 退出下划线模式
- `tput rev` - 打开反转模式

### Linux 技巧

Ajay Kumar Tiwari

- `tput smso` - 进入突出模式（rxvt 上的粗体）
- `tput rmso` - 退出突出模式
- `tput sgr0` - 关闭所有属性

`tput` 的颜色代码：

- `0` – 黑色
- `1` – 红色
- `2` – 绿色
- `3` – 黄色
- `4` – 蓝色
- `5` – 洋红
- `6` – 青色
- `7` - 白色

### Hack 41. 使用 PS1 变量的可用代码创建自己的提示符

使用以下代码创建您自己的功能性且符合您口味的 `PS1` Linux 提示符。

- `\a` ASCII 铃声字符 (`07`)
- `\d` 日期格式为“星期几 月 日”（例如，“Tue May 26”）
- `\D{format}` - 格式传递给 `strftime(3)`，结果插入到提示符字符串中；空格式会导致特定于区域设置的时间表示。需要大括号
- `\e` ASCII 转义字符 (`033`)

### Linux 技巧

Ajay Kumar Tiwari

- `\h` 主机名直到第一部分
- `\H` 主机名
- `\j` shell 当前管理的作业数
- `\l` shell 终端设备名称的基名
- `\n` 换行
- `\r` 回车
- `\s` shell 的名称，`$0` 的基名（斜杠之后的部分）
- `\t` 24 小时制 `HH:MM:SS` 格式的当前时间
- `\T` 12 小时制 `HH:MM:SS` 格式的当前时间
- `\@` 12 小时制 am/pm 格式的当前时间
- `\A` 24 小时制 `HH:MM` 格式的当前时间
- `\u` 当前用户的用户名
- `\v` `bash` 的版本（例如，`2.00`）
- `\V` `bash` 的发行版，版本 + 补丁级别（例如，`2.00.0`）
- `\w` 当前工作目录，`$HOME` 用波浪号缩写
- `\W` 当前工作目录的基名，`$HOME` 用波浪号缩写
- `\!` 此命令的历史编号
- `\#` 此命令的命令编号
- `\$` 如果有效 UID 为 `0`，则为 `#`，否则为 `$`
- `\nnn` 八进制数 `nnn` 对应的字符
- `\` 反斜杠
- `\[` 开始非打印字符序列，可用于在提示符中嵌入终端控制序列

### Linux 技巧

Ajay Kumar Tiwari

- `\]` 结束非打印字符序列

### Hack 42. 在 PS1 变量中使用 bash shell 函数

您也可以按如下所示在 `PS1` 中调用 `bash shell` 函数。

```
ramesh@dev-db ~> function httpdcount {
> ps aux | grep httpd | grep -v grep | wc -l
> }
```

```
ramesh@dev-db ~> export PS1="\u@\h [`httpdcount`]> "
```

`ramesh@dev-db [12]>`

[注意：这会显示正在运行的 `httpd` 进程的总数]

您可以将以下行添加到 `~/.bash_profile` 或 `~/.bashrc` 以使此更改永久生效：

```
$ vi .bash_profile
```

```
function httpdcount {
```



### Hack 43. 在 PS1 变量中使用 shell 脚本

您也可以在 `PS1` 变量中调用 shell 脚本。下面示例中，`~/bin/totalfilesize.sh` 计算当前目录的总文件大小，被调用在 `PS1` 变量中。

```
ramesh@dev-db ~> cat ~/bin/totalfilesize.sh
```

#### Linux 技巧

Ajay Kumar Tiwari

```
for filesize in $(ls -l . | grep "^-" | awk '{print $5}')
do
  let totalsize=$totalsize+$filesize
done
echo -n "$totalsize"
```

```
ramesh@dev-db ~> export PATH=$PATH:~/bin
ramesh@dev-db ~> export PS1="\u@\h
[$(totalfilesize.sh) bytes]> "
ramesh@dev-db [534 bytes]> cd /etc/mail
ramesh@dev-db [167997 bytes]>
```

注意：这会执行 `totalfilesize.sh` 以在 `PS1` 提示符中显示当前目录的总文件大小

### Linux 技巧

Ajay Kumar Tiwari

## 第 7 章：归档和压缩

### Hack 44. Zip 命令基础

#### 如何压缩多个文件？

语法：`zip {.zip 文件名} {文件名}`

```
# zip var-log-files.zip /var/log/*
adding: var/log/acpid (deflated 81%)
adding: var/log/anaconda.log (deflated 79%)
adding: var/log/anaconda.syslog (deflated 73%)
adding: var/log/anaconda.xlog (deflated 82%)
adding: var/log/audit/ (stored 0%)
adding: var/log/boot.log (stored 0%)
adding: var/log/boot.log.1 (deflated 40%)
adding: var/log/boot.log.2 (deflated 42%)
adding: var/log/boot.log.3 (deflated 40%)
adding: var/log/boot.log.4 (deflated 40%)
```

#### 如何递归压缩目录及其文件？

```
# zip -r var-log-dir.zip /var/log/
updating: var/log/ (stored 0%)
adding: var/log/wtmp (deflated 78%)
adding: var/log/scrollkeeper.log (deflated 94%)
adding: var/log/rpmpkgs.3 (deflated 68%)
adding: var/log/spooler (stored 0%)
adding: var/log/cron.2 (deflated 90%)
adding: var/log/spooler.1 (stored 0%)
adding: var/log/spooler.4 (stored 0%)
adding: var/log/httpd/ (stored 0%)
adding: var/log/rpmpkgs.1 (deflated 68%)
adding: var/log/anaconda.log (deflated 79%)
adding: var/log/secure.2 (deflated 93%)
```

### Linux 技巧

#### 如何解压 *.zip 压缩文件？

```
# unzip var-log.zip
Archive: var-log.zip
  inflating: var/log/acpid
  inflating: var/log/anaconda.log
  inflating: var/log/anaconda.syslog
  inflating: var/log/anaconda.xlog
  creating: var/log/audit/
```

Ajay Kumar Tiwari

要查看解压时的详细输出，请按如下所示传递 `-v` 选项。

```
# unzip -v var-log.zip
Archive: var-log.zip
LengthMethodSize RatioDateTime
Name
____ __ __ _____
-
  1916 Defl:N369 81% 02-08-08 14:27
var/log/acpid
  13546 Defl:N2900 79% 02-02-07 14:25
var/log/anaconda.log
skip..
  7680 Defl:N411
var/log/wtmp.1
  40981 Defl:N7395
var/log/Xorg.0.log
______
__
414069912809229
files
95%
82%
_
93%
12-30-08 10:55
02-08-08 14:28
fe876ee9
6386a95e
_
56
CRC-32
__
e2ffd c0c
34cc03a1
_
```

### 如何在不解压的情况下列出 zip 文件的内容？

```
# unzip -l var-log.zip
```

```
Archive: var-log.zip
  LengthDateTime
  _______
  1916 02-08-08 14:27
Name
--
var/log/acpid
13546
..skip..
40981
40981
——
41406991
02-08-08 14:28
02-02-07 14:56
02-02-07 14:25
Ajay Kumar Tiwari
var/log/anaconda.log
var/log/Xorg.0.log
var/log/Xorg.0.log.old
——
56 files
```

### Hack 45. 使用 zip 命令进行高级压缩

`zip` 命令提供了 10 级压缩。

级别 0 是最低级别，仅在不压缩的情况下归档文件。

级别 1 会进行少量压缩。但速度会很快。

级别 6 是压缩的默认级别。

级别 9 是最大压缩。与默认级别相比，这会更慢。在我看来，除非您正在压缩一个巨大的文件，否则您应该始终使用级别 9。

在下面的示例中，我对同一个目录使用了级别 0、默认级别 6 和级别 9 压缩。请自行查看压缩文件大小。

```
# zip var-log-files-default.zip /var/log/*
# zip -0 var-log-files-0.zip /var/log/*
# zip -9 var-log-files-9.zip /var/log/*
# ls -ltr
-rw-r--r--1 rootroot
var-log-files-default.zip
-rw-r--r--1 rootroot
var-log-files-0.zip
-rw-r--r--1 rootroot
var-log-files-9.zip
2817248 Jan
41415301 Jan
2582610 Jan
1 13:05
1 13:05
1 13:06
```

### Linux 技巧

Ajay Kumar Tiwari

### Hack 46. Zip 文件的密码保护

将选项 `-P` 传递给 `zip` 命令以分配 `zip` 文件的密码。

```
# zip -P mysecurepwd var-log-protected.zip /var/log/*
```

如果您在 shell 脚本中用于后台作业，则上述选项是好的。然而，当您在命令行上交互式执行压缩时，您不希望密码在历史记录中可见。因此，按如下所示使用选项 `-e` 来分配密码。

```
# zip -e var-log-protected.zip /var/log/*
```

```
Enter password:
Verify password:
updating: var/log/acpid (deflated 81%)
updating: var/log/anaconda.log (deflated 79%)
```

当您解压受密码保护的文件时，它会按如下所示要求输入密码。

```
# unzip var-log-protected.zip
```



`Archive: var-log-protected.zip`

`[var-log-protected.zip] var/log/acpid password:`

```
### Hack 47. 验证 zip 归档

有时您可能希望在不提取的情况下验证 zip 归档。要测试 zip 文件的有效性，请按如下所示传递选项 `-t`。

# unzip -t var-log.zip

Archive: var-log.zip

testing: var/log/acpid

testing: var/log/anaconda.log

OK

OK
```

`Linux 技巧`

`testing: var/log/anaconda.syslog`

`skip...`

`testing: var/log/wtmp`

`testing: var/log/wtmp.1`

`testing: var/log/Xorg.0.log`

`Ajay Kumar Tiwari`

`OK`

`OK`

`OK`

`OK`

`No errors detected in compressed data of var-log.zip.`

`### Hack 48. Tar 命令基础`

`tar` 命令（tape archive，磁带归档）用于将一组文件转换为归档。

语法：`tar [options] [tar-archive-name] [other-file-names]`

如何为我的主目录下的所有文件和子目录创建一个单一的备份文件？

以下命令在 `/tmp` 下创建一个名为 `my_home_directory.tar` 的单一归档备份文件。该归档将包含 `/home/jsmith` 下的所有文件和子目录。

- 选项 `c` 表示创建归档。
- 选项 `v` 表示详细模式，在执行命令时显示额外信息。
- 选项 `f` 表示命令中提到的归档文件名。

```
# tar cvf /tmp/my_home_directory.tar /home/jsmith
```

`67`

`Linux 技巧`

`Ajay Kumar Tiwari`

`### 如何查看 tar 归档中的所有文件？`

选项 `t` 将显示 `tar` 归档中的所有文件。

```
# tar tvf /tmp/my_home_directory.tar
```

`### 如何从 tar 归档中提取所有文件？`

选项 `x` 将从 `tar` 归档中提取文件，如下所示。这将把内容提取到执行命令时的当前目录位置。

```
# tar xvf /tmp/my_home_directory.tar
```

`### 如何将 tar.gz 文件提取到特定目录？`

```
# tar xvfz /tmp/my_home_directory.tar.gz -C /home/ramesh
```

`### Hack 49. 使用 tar 结合 gzip、bzip2`

`### 如何使用 tar 与 gzip？`

处理 `tar.gz` 压缩文件时，在 `tar` 命令中添加选项 `z`。

```
# tar cvfz /tmp/my_home_directory.tar.gz /home/jsmith
```

```
# tar xvfz /tmp/my_home_directory.tar.gz
```

```
# tar tvfz /tmp/my_home_directory.tar.gz
```

注意：与 `bzip2` 相比，使用 `gzip` 更快。

`Linux 技巧`

`Ajay Kumar Tiwari`

`### 如何使用 tar 与 bzip2？`

处理 `tar.bz2` 压缩文件时，在 `tar` 命令中添加选项 `j`。

```
# tar cvfj /tmp/my_home_directory.tar.bz2 /home/jsmith
# tar xvfj /tmp/my_home_directory.tar.bz2
# tar tvfj /tmp/my_home_directory.tar.bz2
```

注意：与 `gzip` 相比，使用 `bzip2` 提供了更高级别的压缩。

`Linux 技巧`

`Ajay Kumar Tiwari`

## 第 8 章：命令行历史

当你经常使用 Linux 命令行时，有效地使用历史记录可以大幅提升生产力。事实上，一旦你掌握了我在此提供的 15 个示例，你会发现使用命令行更有趣、更有乐趣。

### Hack 50. 使用 `HISTTIMEFORMAT` 在历史记录中显示时间戳

通常当你从命令行输入 `history` 时，它会显示命令编号和命令。出于审计目的，如下所示同时显示时间戳可能有益。

```
# export HISTTIMEFORMAT='%F %T '
# history

1 2008-08-05 19:02:39 service network restart
2 2008-08-05 19:02:39 exit
3 2008-08-05 19:02:39 id
4 2008-08-05 19:02:39 cat /etc/redhat-release
| more
```

注意：你也可以设置以下别名来查看最近的历史命令。

```
alias h1='history 10'
```

```
alias h2='history 20'
```

```
alias h3='history 30'
```

### Hack 51. 使用 `Control+R` 搜索历史记录

我坚信这可能是你最频繁使用的历史记录功能。当你已经执行了一个很长的命令时，你只需使用关键字搜索历史记录并重新执行该命令，而无需完全输入它。按 `Control+R` 并输入关键字。

在以下示例中，我搜索了 `red`，它显示了历史记录中包含单词 `red` 的上一个命令“`cat /etc/redhat-release`”。

`注意：从命令行提示符按 Ctrl+R，这将显示如下所示的 reverse-i-search 提示符`

```
(reverse-i-search)`red': cat /etc/redhat-release
```

`注意：当你看到你的命令时按 Enter，这将从历史记录中执行该命令`

```
# cat /etc/redhat-release
```

`Fedora release 9 (Sulphur)`

有时你想在执行历史记录中的命令之前编辑它。例如，你可以搜索 `httpd`，这将显示命令历史中的 `service httpd stop`，选择此命令并将 `stop` 改为 `start`，然后再次重新执行，如下所示。

`注意：从命令行提示符按 Ctrl+R，这将显示 reverse-i-search 提示符`

```
(reverse-i-search)`httpd': service httpd stop
```

`注意：当你看到你的命令时按左右箭头键中的任意一个，这将在执行之前显示命令供你编辑`

```
# service httpd start
```

`Linux 技巧`

`Ajay Kumar Tiwari`

### Hack 52. 使用 4 种不同方法快速重复上一个命令

有时由于各种原因你可能会重复之前的命令。以下是重复上一个已执行命令的 4 种不同方法。

- 1. 使用上箭头查看上一个命令并按 `Enter` 执行它。
- 2. 在命令行输入 `!!` 并按 `Enter`
- 3. 在命令行输入 `!-1` 并按 `Enter`。
- 4. 按 `Control+P` 将显示上一个命令，按 `Enter` 执行它

`Linux 技巧`

`Ajay Kumar Tiwari`

### Hack 53. 从历史记录中执行特定命令

在以下示例中，如果你想重复命令 `#4`，按如下所示执行 `!4`。

```
# history
1 service network restart
2 exit
3 id
4 cat /etc/redhat-release
| more

# !4
cat /etc/redhat-release
Fedora release 9 (Sulphur)
```

`Linux 技巧`

`Ajay Kumar Tiwari`

### Hack 54. 执行以特定单词开头的上一个命令

输入 `!` 后跟你想要重新执行的命令的开头几个字母。在以下示例中，输入 `!ps` 并按 `Enter`，执行了以 `ps` 开头的上一个命令，即 '`ps aux | grep yp`'。

```
# !ps
ps aux | grep yp
  root 16947 0.0 Sl 13:10 0:00 ypbinding
  root 17503 0.0 S+ 19:19 0:00 grep yp
```

### Hack 55. 使用 `HISTSIZE` 控制历史记录中的总行数

将以下两行附加到 `.bash_profile` 并重新登录 `bash` shell 以查看更改。在此示例中，只有 450 条命令将被存储在 `bash` 历史记录中。

```
HISTSIZE=450
HISTFILESIZE=450
```



# Hack 55. 使用 HISTSIZE 和 HISTFILESIZE 增加历史命令数

`vi ~/.bash_profile`

```
HISTSIZE=450
HISTFILESIZE=450
```

### Hack 56. 使用 HISTFILE 更改历史文件名称

默认情况下，历史记录存储在 `~/.bash_history` 文件中。将以下行添加到 `.bash_profile` 并重新登录 `bash` shell，以将历史命令存储在 `.commandline_warrior` 文件中而不是 `.bash_history` 文件中。我尚未弄清楚此功能的实际用途。我认为当你想使用不同的历史文件名跟踪不同终端中执行的命令时，这会很有用。

```
# vi ~/.bash_profile
HISTFILE=/root/.commandline_warrior
```

### Hack 57. 使用 HISTCONTROL 从历史记录中消除连续重复的条目

在以下示例中，`pwd` 被输入了三次，当你执行 `history` 时，你可以看到它的全部 3 次连续出现。为了消除重复，将 `HISTCONTROL` 设置为 `ignoredups`，如下所示。

```
# pwd
# pwd
# pwd
# history | tail -4
  44 pwd
  45 pwd
  46 pwd
  47 history | tail -4
```

[注意：如上所示执行 `pwd` 3 次后，历史记录中有三个 `pwd` 命令]

```
# export HISTCONTROL=ignoredups
# pwd
# pwd
# pwd
# history | tail -3
  56 export HISTCONTROL=ignoredups
  57 pwd
  58 history | tail -4
```

### Linux 技巧

Ajay Kumar Tiwari

[注意：即使如上所示执行 `pwd` 3 次，历史记录中也只有一个 `pwd` 命令]

### Hack 58. 使用 HISTCONTROL 在整个历史记录中删除重复项

上面显示的 `ignoredups` 仅在命令连续时才删除重复项。要在整个历史记录中消除重复项，将 `HISTCONTROL` 设置为 `erasedups`，如下所示。

```
# export HISTCONTROL=erasedups
# pwd
# service httpd stop
# history | tail -3
  38 pwd
  39 service httpd stop
  40 history | tail -3
# ls -ltr
# service httpd stop
# history | tail -6
  35 export HISTCONTROL=erasedups
  36 pwd
  37 history | tail -3
  38 ls -ltr
  39 service httpd stop
  40 history | tail -6
```

[注意：`pwd` 之后的之前的 `service httpd stop` 被删除了]

### Linux 技巧

Ajay Kumar Tiwari

### Hack 59. 使用 HISTCONTROL 强制历史不记录特定命令

当你执行命令时，可以通过将 `HISTCONTROL` 设置为 `ignorespace` 并在命令前输入一个空格来指示历史忽略该命令，如下所示。我看到很多初级系统管理员对此感到兴奋，因为他们可以从历史记录中隐藏命令。

了解 `ignorespace` 的工作原理是好的。但作为最佳实践，不要故意从历史记录中隐藏任何内容。

```
# export HISTCONTROL=ignorespace
# ls -ltr
# pwd
#
service httpd stop
```

[Note: `service` 命令开头有一个空格，用于忽略该命令不被记录到历史]

```
# history | tail -3
67 ls -ltr
68 pwd
69 history | tail -3
```

### Hack 60. 使用 -c 选项清除所有之前的历史记录

有时你可能想要清除所有之前的历史记录。然而你可能仍然希望历史记录继续向前。

```
# history -c
```

### Hack 61. 替换历史命令中的单词

在浏览历史记录时，你可能想要执行不同的命令，但使用刚刚搜索到的命令中的相同参数。

在下面的示例中，`vi` 命令旁边的 `!!:$` 会将前一个命令的参数获取到当前命令。

```
# ls anaconda-ks.cfg
anaconda-ks.cfg
# vi !!:$
vi anaconda-ks.cfg
```

在下面的示例中，`vi` 命令旁边的 `!^` 会将前一个命令（即 `cp` 命令）的第一个参数获取到当前命令（即 `vi` 命令）。

```
# cp anaconda-ks.cfg anaconda-ks.cfg.bak
anaconda-ks.cfg
# vi !^
vi anaconda-ks.cfg
```

### Hack 62. 为特定命令替换特定参数

在下面的示例中，`!cp:2` 会在历史记录中搜索以 `cp` 开头的上一个命令，取出 `cp` 的第二个参数并将其替换为 `ls -l` 命令，如下所示。

```
# cp ~/longname.txt /really/a/very/long/path/long-filename.txt
```

```
# ls -l !cp:2
```

```
ls -l /really/a/very/long/path/long-filename.txt
```

在下面的示例中，`!cp:$` 会在历史记录中搜索以 `cp` 开头的上一个命令，取出 `cp` 的最后一个参数（在本例中也是如上所示的第二个参数）并将其替换为 `ls -l` 命令，如下所示。

```
# ls -l !cp:$
```

```
ls -l /really/a/very/long/path/long-filename.txt
```

### Hack 63. 使用 HISTSIZE 禁用历史记录的使用

如果你想完全禁用历史记录，不希望 `bash` shell 记住你输入的命令，请将 `HISTSIZE` 设置为 `0`，如下所示。

```
# export HISTSIZE=0
```

```
# history
```

[Note: 历史记录未显示任何内容]

### Hack 64. 使用 HISTIGNORE 从历史记录中忽略特定命令

有时你可能不希望用诸如 `pwd` 和 `ls` 之类的基本命令 clutter 历史记录。使用 `HISTIGNORE` 指定你希望从历史记录中忽略的所有命令。

请注意，将 `ls` 添加到 `HISTIGNORE` 只会忽略 `ls` 而不会忽略 `ls -l`。因此，你必须提供确切想要从历史记录中忽略的命令。

```
# export HISTIGNORE="pwd:ls:ls -ltr:"
# pwd
# ls
# ls -ltr
# service httpd stop
# history | tail -3
```

```
79 export HISTIGNORE="pwd:ls:ls -ltr:"
80 service httpd stop
81 history
```

[Note: 历史记录未显示 `pwd` 和 `ls`]

## 第 9 章：系统管理任务

### Hack 65. 使用 fdisk 进行分区

在服务器上安装全新的磁盘后，你必须使用工具如 `fdisk` 对其进行相应分区。

以下是在 `fdisk` 内部可以执行的 5 个典型操作（命令）。

- `n` – 新建分区
- `d` – 删除现有分区
- `p` - 打印分区表
- `w` – 将更改写入分区表。即保存。
- `q` – 退出 `fdisk` 工具

#### 创建分区

在以下示例中，我创建了一个 `/dev/sda1` 主分区。

```
# fdisk /dev/sda
```

设备既不包含有效的 DOS 分区表，也不包含 Sun、SGI 或 OSF 磁盘标签 正在构建新的 DOS 磁盘标签。更改将仅保留在内存中，直到你决定写入它们。之后，当然，以前的<|message|>

The number of cylinders for this disk is set to 34893. There is nothing wrong with that, but this is larger than 1024, and could in certain setups cause problems with:

1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs (e.g., DOS FDISK, OS/2 FDISK)

```

Warning: invalid flag 0x0000 of partition table 4 will



be corrected by `w(rite)`

`Command (m for help): p`

```
Disk /dev/sda: 287.0 GB, 287005343744 bytes
255 heads, 63 sectors/track, 34893 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot Start End Blocks Id System
```

`Command (m for help): n`

```
Command action
   e extended
   p primary partition (1-4)

p
Partition number (1-4): 1
First cylinder (1-34893, default 1):
Using default value 1
Last cylinder or +size or +sizeM or +sizeK (1-34893, default 34893):
Using default value 34893
Command (m for help): w
The partition table has been altered!
Calling ioctl() to re-read partition table.
Syncing disks.
```

#### 验证分区是否成功创建

```
# fdisk /dev/sda
The number of cylinders for this disk is set to 34893.
There is nothing wrong with that, but this is larger than 1024, and could in certain setups cause problems with:
1) software that runs at boot time (e.g., old versions of LILO)
2) booting and partitioning software from other OSs (e.g., DOS FDISK, OS/2 FDISK)

Command (m for help): p
Disk /dev/sda: 287.0 GB, 287005343744 bytes
255 heads, 63 sectors/track, 34893 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot Start End Blocks Id System
/dev/sda1
Start 1
End 34893
Blocks 280277991
Id 83
System Linux
Command (m for help): q
```

### Hack 66. 使用 mke2fs 格式化分区

在对磁盘进行分区后，它仍然无法使用，因为我们需要格式化磁盘。在此阶段，如果你尝试查看磁盘信息，它会给出以下错误消息，表明没有有效的超级块。

```
# tune2fs -l /dev/sda1
tune2fs 1.35 (28-Feb-2004)
tune2fs: Bad magic number in super-block while trying to open /dev/sda1
Couldn't find valid filesystem superblock.
```

要格式化磁盘，请按如下所示使用 `mke2fs`。

```
# mke2fs /dev/sda1
```

你也可以向 `mke2fs` 传递以下可选参数。

- `-m 0` : reserved-blocks-percentage – 这表示为 `root` 用户保留的文件系统块的百分比。默认为 5%。在以下示例中，它被设置为 0。
- `-b 4096` : block-size specified in bytes. Valid values are 1024, 2048 and 4096 bytes per block.

```
# mke2fs -m 0 -b 4096 /dev/sda1
mke2fs 1.35 (28-Feb-2004)
Filesystem label=
OS type: Linux
Block size=4096 (log=2)
Fragment size=4096 (log=2)
205344 inodes, 70069497 blocks
0 blocks (0.00%) reserved for the super user
First data block=0
Maximum filesystem blocks=71303168
2139 block groups
32768 blocks per group, 32768 fragments per group
96 inodes per group
Superblock backups stored on blocks:
32768, 98304, 163840, 229376, 294912, 819200, 884736, 1605632, 2654208, 4096000, 7962624, 11239424, 20480000, 23887872
Writing inode tables: done
Writing superblocks and filesystem accounting information: done
This filesystem will be automatically checked every 32 mounts or 180 days, whichever comes first. Use tune2fs -c or -i to override.
```

The above command will create an ext2 filesystem. To create an ext3 file system do the following:

```
# mkfs.ext3 /dev/sda1
# mke2fs -j /dev/sda1
```

### Hack 67. 挂载分区

创建分区并格式化后，你可以将其挂载到挂载点。

首先创建分区应挂载到的目录。

```
# mkdir /home/database
```

挂载文件系统。

```
# mount /dev/sda1 /home/database
```

要使文件系统在重新启动后自动挂载，请将以下条目添加到 `/etc/fstab`

```
/dev/sda1 /home/database ext3 defaults 0 2
```

### Hack 68. 使用 tune2fs 微调分区

使用 `tune2fs -l /dev/sda1` 查看文件系统信息，如下所示。

```
# tune2fs -l /dev/sda1
```



```
tune2fs 1.35 (28-Feb-2004)

Filesystem volume name:/home/database

Last mounted on:<not available>

Filesystem UUID:f1234556-e123-1234-abcd-bbbbbaaaaae11

Filesystem magic number: 0xEF44

Filesystem revision #:1 (dynamic)

Filesystem features:resize_inode filetype sparse_super

Default mount options:(none)

Filesystem state:not clean
```

### Linux 技巧

Ajay Kumar Tiwari

### `tune2fs -l` 输出

| 字段 | 值 |
|---|---|
| 错误行为 | 继续 |
| 文件系统 OS 类型 | Linux |
| Inode 计数 | 1094912 |
| 块计数 | 140138994 |
| 预留块计数 | 0 |
| 空闲块 | 16848481 |
| 空闲 inode | 1014969 |
| 第一个块 | 0 |
| 块大小 | 2048 |
| 碎片大小 | 2048 |
| 预留 GDT 块 | 512 |
| 每组块数 | 16384 |
| 每组碎片数 | 16384 |
| 每组 inode 数 | 128 |
| 每组 inode 块数 | 8 |
| 文件系统创建于 | Tue Jul 1 00:06:03 2008 |
| 最后挂载时间 | Thu Aug 21 05:58:25 2008 |
| 最后写入时间 | Fri Jan 2 15:40:36 2009 |
| 挂载次数 | 2 |
| 最大挂载次数 | 20 |
| 最后检查 | Tue Jul 1 00:06:03 2008 |
| 检查间隔 | 15552000 (6 个月) |
| 下次检查后 | Sat Dec 27 23:06:03 2008 |
| 预留块 uid | 0 (用户 root) |
| 预留块 gid | 0 (组 root) |
| 第一个 inode | 11 |
| Inode 大小 | 128 |
| 默认目录哈希 | tea |
| 目录哈希种子 | 12345829-1236-4123-9aaa- |

你也可以使用 `tune2fs` 来调整 `ext2`/`ext3` 文件系统参数。例如，如果你想更改文件系统卷名，可以按如下所示操作。

```
# tune2fs -l /dev/sda1 | grep volume

Filesystem volume name:/home/database

# tune2fs -L database-home /dev/emcpowera1

tune2fs 1.35 (28-Feb-2004)
```

```
# tune2fs -l /dev/sda1 | grep volume

文件系统卷名:database-home
```

### Hack 69. 创建一个交换文件系统。

按如下所示创建用于交换的文件。

```
# dd if=/dev/zero of=/home/swap-fs bs=1M count=512
```

512+0 条记录已读

512+0 条记录已写

```
# ls -l /home/swap-fs
```

-rw-r--r-- 1 root root 536870912 Jan 2 23:13 /home/swap-fs

使用 `mkswap` 在上面创建的 `/home/swap-fs` 文件中设置 Linux 交换区。

```
# mkswap /home/swap-fs
```

正在设置 swapspace 版本 1，大小 = 536866 kB

一旦文件创建并已为 Linux 交换区设置好，就可以使用 `swapon` 按如下所示启用交换。

```
# swapon /home/swap-fs
```

将以下行添加到 `/etc/fstab` 并重新启动系统以使交换生效。

```
/home/swap-fs swap swap defaults 0 0
```

### Hack 70. 创建新用户

### 添加新用户 – 基本方法

仅指定用户名。

```
# useradd jsmith
```

### 使用额外参数添加新用户

你也可以为 `useradd` 指定以下参数

- `-c` : 用户描述。
- `-e` : 用户到期日期，格式为 mm/dd/yy

```
# adduser -c "John Smith - Oracle Developer" -e 12/31/09 jsmith
```

验证用户是否已成功添加。

```
# grep jsmith /etc/passwd
```

```
jsmith:x:510:510:John Smith - Oracle Developer:/home/jsmith:/bin/bash
```

### 更改用户密码。

```
# passwd jsmith
```

正在更改用户 jsmith 的密码。

新的 UNIX 密码：

BAD PASSWORD: 它基于字典单词

重新输入新的 UNIX 密码：

passwd: 所有身份验证令牌均已成功更新。

注意：请确保遵循这些最佳实践为用户创建强密码。

### 如何识别 `useradd` 使用的默认值？

以下是创建用户时将使用的默认值。

```
# useradd -D
```

```
GROUP=100

HOME=/home

INACTIVE=-1

EXPIRE=

SHELL=/bin/bash

SKEL=/etc/skel
```

### Hack 71. 创建新组并分配给用户

创建一个新的 `developer` 组。

```
# groupadd developers
```

验证组是否已成功创建。

```
# grep developer /etc/group
```

```
developers:x:511:
```

将用户添加到现有组。

你不能使用 `useradd` 修改现有用户，否则会收到以下错误消息。

```
# useradd -G developers jsmith
```

useradd: 用户 jsmith 已存在

```
# usermod -g developers jsmith
```

验证用户的组是否已成功修改。

```
# grep jsmith /etc/passwd
```

jsmith:x:510:511:Oracle Developer:/home/jsmith:/bin/bash

```
# id jsmith
```

uid=510(jsmith) gid=511(developers)
groups=511(developers)

```
# grep jsmith /etc/group
```

jsmith:x:510:
developers:x:511:jsmith

### Hack 72. 在 OpenSSH 中设置 SSH 无密码登录

你可以使用 `ssh-keygen` 和 `ssh-copy-id` 按以下示例中的说明，通过 3 个简单步骤在不输入密码的情况下登录到远程 Linux 服务器。
`ssh-keygen` 创建公钥和私钥。`ssh-copy-id` 将本地主机的公钥复制到远程主机的 `authorized_keys` 文件。`ssh-copy-id` 还为远程主机的 `home`、`~/.ssh` 和 `~/.ssh/authorized_keys` 分配适当的权限。

### 步骤 1：使用 `ssh-keygen` 在本地主机上创建公钥和私钥

```
jsmith@local-host$ ssh-keygen
```



正在生成公钥/私钥 `rsa` 密钥对。

输入要保存密钥的文件(`/home/jsmith/.ssh/id_rsa`):[按 Enter 键]
输入密码短语（为空则不设密码）：[按 Enter 键]
再次输入相同的密码短语：[按 Enter 键]
你的身份已保存在
`/home/jsmith/.ssh/id_rsa`。
你的公钥已保存在
`/home/jsmith/.ssh/id_rsa.pub`。
密钥指纹为：
`33:b3:fe:af:95:95:18:11:31:d5:de:96:2f:f2:35:f9`
`jsmith@local-host`

### 步骤 2：使用 `ssh-copy-id` 将公钥复制到远程主机

`jsmith@local-host$ ssh-copy-id -i ~/.ssh/id_rsa.pub remote-host`
`jsmith@remote-host's password:`
现在尝试使用 `ssh 'remote-host'` 登录机器，并检查：
`.ssh/authorized_keys` 以确保我们没有添加
意外的额外密钥。
注意：`ssh-copy-id` 将密钥附加到远程主机的
`.ssh/authorized_keys`。

### 步骤 3：在不输入密码的情况下登录到远程主机

`jsmith@local-host$ ssh remote-host`
`最后登录：Sun Nov 16 17:22:33 2008 from 192.168.1.2`
`[注意：SSH 未要求输入密码。]`
`jsmith@remote-host$ [注意：你现在在远程主机上]`

### Hack 73. 使用 `ssh-copy-id` 配合 `ssh-agent`

### 使用 `ssh-copy-id` 配合 `ssh-add`/`ssh-agent`

当未为选项 `-i` 传递值且 `~/.ssh/identity.pub` 不可用时，`ssh-copy-id` 将显示以下错误消息。

```
jsmith@local-host$ ssh-copy-id -i remote-host

/usr/bin/ssh-copy-id: ERROR: No identities found
```

如果你已使用 `ssh-add` 将密钥加载到 `ssh-agent` 中，则 `ssh-copy-id` 将从 `ssh-agent` 获取密钥以复制到远程主机。也就是说，当你不向 `ssh-copy-id` 传递选项 `-i` 时，它会将 `ssh-add -L` 命令提供的密钥复制到远程主机。

```
jsmith@local-host$ ssh-agent $SHELL

jsmith@local-host$ ssh-add -L

The agent has no identities.

jsmith@local-host$ ssh-add

Identity added: /home/jsmith/.ssh/id_rsa

(/home/jsmith/.ssh/id_rsa)

jsmith@local-host$ ssh-add -L

ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAsJIEILxftj8aSxMa3d8t6JvM79D aHrtPhTYpq7kIEMUNzApnyxsHpH1tQ/Ow== /home/jsmith/.ssh/id_rsa

jsmith@local-host$ ssh-copy-id -i remote-host

jsmith@remote-host's password:
```

现在尝试使用 `ssh 'remote-host'` 登录机器，并检查：`.ssh/authorized_keys` 以确保我们没有添加意外的额外密钥。

`[注意：这已添加 ssh-add -L 显示的密钥]`

### `ssh-copy-id` 的三个小烦恼

以下是 `ssh-copy-id` 的一些小烦恼。

- 默认公钥：`ssh-copy-id` 使用 `~/.ssh/identity.pub` 作为默认公钥文件（即当未向选项 `-i` 传递值时）。相反，我希望它使用 `id_dsa.pub` 或 `id_rsa.pub` 或 `identity.pub` 作为默认密钥。也就是说，如果其中任何一个存在，它应该将其复制到远程主机。如果存在两个或三个，它应该将 `identity.pub` 作为默认值。
- 代理中没有身份：当 `ssh-agent` 正在运行且 `ssh-add -L` 返回“代理中没有身份”（即没有密钥添加到 `ssh-agent`）时，`ssh-copy-id` 仍会将消息“代理中没有身份”复制到远程主机的 `authorized_keys` 条目中。
- `authorized_keys` 中的重复条目：我希望 `ssh-copy-id` 验证远程主机的 `authorized_keys` 中的重复条目。如果你多次在本地主机上执行 `ssh-copy-id`，它会在不检查重复的情况下不断将相同的密钥附加到远程主机的 `authorized_keys` 文件中。即使有重复条目，一切仍按预期工作。但我希望我的 `authorized_keys` 文件保持整洁。

### Hack 74. Crontab

使用 `cron` 你可以在特定时间和日期执行 shell 脚本或 Linux 命令。例如，系统管理员可以安排每天运行的备份作业。

如何向 `cron` 添加作业？

```
# crontab -e

0 5 * * * /root/bin/backup.sh
```

### Linux 技巧
Ajay Kumar Tiwari

这将在每天凌晨5点执行 `/root/bin/backup.sh`。

## Cron 字段说明
以下是 `crontab` 文件的格式。

```
{minute} {hour} {day-of-month} {month} {day-of-week} {full-path-to-shell-script}
```

```
0
0
0
0
0
```

`minute`: 允许范围 0 – 59

`hour`: 允许范围 0 – 23

`day-of-month`: 允许范围 0 – 31

`month`: 允许范围 1 – 12。1 = 一月。12 = 十二月。

`Day-of-week`: 允许范围 0 – 7。星期日为 0 或 7。

## Crontab 示例
1. 在每天凌晨12:01运行。午夜后1分钟。这是在系统负载不高时运行备份的好时机。

```
1 0 * * * /root/bin/backup.sh
```

2. 在每个工作日（周一 – 周五）晚上11:59运行备份。

```
59 11 * * 1,2,3,4,5 /root/bin/backup.sh
```

以下操作也会产生相同效果。

```
59 11 * * 1-5 /root/bin/backup.sh
```

3. 每5分钟执行一次命令。

```
*/5 * * * * /root/bin/check-status.sh
```

4. 在每月1日的下午1:10执行

```
10 13 1 * * /root/bin/full-backup.sh
```

5. 在工作日晚上11点执行。

```
0 23 * * 1-5 /root/bin/incremental-backup.sh
```

## Crontab 选项
`crontab` 可用的选项如下：

`crontab -e`: 编辑 `crontab` 文件。如果不存在则会创建 `crontab`

`crontab -l`: 显示 `crontab` 文件。

`crontab -r`: 删除 `crontab` 文件。

`crontab -ir`: 删除 `crontab` 前会提示用户。

### Hack 75. 使用 Magic SysRq 键安全重启 Linux
Magic SysRq 键是 Linux 内核中的一个键组合，允许用户在系统状态如何的情况下执行各种低级命令。

它常用于从冻结中恢复，或在不损坏文件系统的情况下重启计算机。键组合为 `Alt+SysRq+commandkey`。在许多系统中，`SysRq` 键是打印屏幕键。

首先，需要启用 `SysRq` 键，如下所示。

```
echo "1" > /proc/sys/kernel/sysrq
```



### SysRq 命令键列表
以下为 `Alt+SysRq+commandkey` 可用的命令键。

- `'k'` – 终止当前虚拟控制台上运行的所有进程。
- `'s'` – 这将尝试同步所有已挂载的文件系统。
- `'b'` - 立即重启系统，而不卸载分区或同步。
- `'e'` – 向除 `init` 外的所有进程发送 `SIGTERM`。
- `'m'` – 将当前内存信息输出到控制台。
- `'i'` - 向除 `init` 外的所有进程发送 `SIGKILL` 信号
- `'r'` - 将键盘从原始模式（由 `X11` 等程序使用的模式）切换到 `XLATE` 模式。
- `'s'` – 同步所有已挂载的文件系统。
- `'t'` - 将当前任务列表及其信息输出到控制台。
- `'u'` - 以只读模式重新挂载所有已挂载的文件系统。
- `'o'` – 立即关闭系统。
- `'p'` – 将当前寄存器和标志打印到控制台。
- `'0-9'` - 设置控制台日志级别，控制哪些内核消息会打印到你的控制台。
- `'f'` - 将调用 `oom_kill` 杀死占用更多内存的进程。
- `'h'` – 用于显示帮助。但除上述列出的键之外的任何其他键都会打印帮助。

我们也可以通过向 `/proc/sysrq-trigger` 文件回显键来实现。例如，要重启系统可以执行以下操作。

```
echo "b" > /proc/sysrq-trigger
```

### 使用 Magic SysRq 键执行 Linux 安全重启
要对挂起的 Linux 计算机执行安全重启，请执行以下操作。这将避免下次重启时进行 `fsck`。即按下 `Alt+SysRq+下方突出显示的字母`。

- `unRaw`（从 `X11` 重新夺回键盘控制权，
- `tErminate`（向所有进程发送 `SIGTERM`，允许它们优雅终止），
- `kIll`（向所有进程发送 `SIGILL`，强制它们立即终止），
- `Sync`（将数据刷新到磁盘），
- `Unmount`（重新挂载所有文件系统为只读），
- `reBoot`。

## 第10章：Apachectl 和 Httpd 示例
安装 `Apache2` 后，如果你想最大化使用 `apachectl` 和 `httpd` 的潜力，你应该超越使用 `start`、`stop` 和 `restart`。本章提供的 9 个实用示例将帮助你非常有效地使用 `apachectl` 和 `httpd`。

`Apachectl` 充当 `SysV init` 脚本，接受 `start`、`stop`、`restart` 和 `status` 等参数。它也充当 `httpd` 命令的前端，只需将命令行参数传递给 `httpd`。因此，使用 `apachectl` 执行的所有命令也可以通过直接调用 `httpd` 来执行。

如果你没有 `Apache`，请参考教程：从源码安装 `apache` 或使用 `yum` 安装 `LAMP` 堆栈。

### Hack 76. 向 apachectl 传递不同的 httpd.conf 文件名
通常你会修改原始的 `httpd.conf` 来尝试不同的 `Apache` 指令。如果某些操作不成功，你会恢复更改。不要在原始 `httpd.conf` 上随意尝试，将其复制到新的 `httpd.conf.debug` 并使用选项 `-f` 在测试时使用此新的 `httpd.conf.debug` 文件，如下所示。

```
# apachectl -f conf/httpd.conf.debug

# httpd -k start -f conf/httpd.conf.debug
```

[注意：如上所示，你可以使用 `apachectl` 或 `httpd`]

```
# ps -ef | grep http

root 25080 1 0 23:26 00:00:00 /usr/sbin/httpd -f conf/httpd.conf.debug

apache 25099 25080 0 23:28 00:00:00 /usr/sbin/httpd -f conf/httpd.conf.debug
```

[注意：`ps` 显示 `httpd` 正在使用 `httpd.conf.debug` 文件运行]

一旦你对更改满意，并且 `Apache` 在使用 `httpd.conf.debug` 时没有问题，你可以将更改复制到 `httpd.conf` 并按如下所示正常启动 `Apache`。

```
# cp httpd.conf.debug httpd.conf

# apachectl stop

# apachectl start

# ps -ef | grep httpd
```

```
root 25114 1 0 23:28 00:00:00 /usr/sbin/httpd -k start
daemon 25115 25114 0 23:28 00:00:00 /usr/sbin/httpd -k start
```

[注意：`ps` 表明 `httpd` 正在使用默认配置文件运行]

### Hack 77. 在不修改 httpd.conf 的情况下使用临时 DocumentRoot
当你尝试网站的不同布局并且不想修改默认 `DocumentRoot` 下的原始文件时，这非常有帮助。

将原始 `DocumentRoot` 目录 (`/var/www/html`) 复制到新的临时 `DocumentRoot` 目录 (`/var/www/html_debug`)。在此临时 `DocumentRoot` 目录 (`/var/www/html_debug`) 下进行所有更改，并使用选项 `-c` 按如下所示使用此临时目录启动 `Apache`。

```
# httpd -k start -c "DocumentRoot /var/www/html_debug/"
```

如果你想使用默认 `DocumentRoot` (`/var/www/html`) 返回原始配置，只需按如下所示重启 `Apache`。

```
# httpd -k stop
```

```
# apachectl start
```

### Hack 78. 临时提高日志级别
在调试问题时，你可以使用选项 `-e` 临时更改 `Apache` 的 `LogLevel`，而无需修改 `httpd.conf` 中的 `LogLevel` 指令，如下所示。在此示例中，`LogLevel` 设置为 `debug`。

```
# httpd -k start -e debug
```

```
[Sun Aug 17 13:53:06 2008] [debug] mod_so.c(246):

loaded module auth_basic_module
```

```
[Sun Aug 17 13:53:06 2008] [debug] mod_so.c(246):

loaded module auth_digest_module
```

可以传递给选项 `-e` 的可能值有：

- `debug`
- `info`
- `notice`
- `warn`
- `error`
- `crit`
- `alert`
- `emerg`
- `99`

### Hack 79. 显示 Apache 内部的模块
显示编译在 `Apache` 内部的模块

```
# httpd -l
```

编译进来的模块：

- `core.c`
- `prefork.c`
- `http_core.c`
- `mod_so.c`

### 显示 Apache 加载的静态和动态模块
当你向 `httpd` 传递选项 `-l` 时，它只会显示静态模块。

传递选项 `-M` 将显示静态和共享模块，如下所示。

```
# httpd -M
```

已加载模块：

- `core_module` (`static`)
- `mpm_prefork_module` (`static`)
- `http_module` (`static`)
- `so_module` (`static`)
- `auth_basic_module` (`shared`)
- `auth_digest_module` (`shared`)
- `authn_file_module` (`shared`)
- `authn_alias_module` (`shared`)

语法正确

### Linux 技巧

`Ajay Kumar Tiwari`

### Hack 80. 在 httpd.conf 中显示所有已接受的指令

这就像 `httpd` 的扩展帮助，它将显示所有 `httpd.conf` 指令及其有效的位置。对于特定指令，它会列出所有可能的值以及在 `httpd.conf` 中可以使用的位置。

这在你想快速了解某个 `Apache` 指令时非常有帮助。

```
# httpd -L
```



### Hack 80. Apache 配置指令详解

`HostnameLookups` (`core.c`)
- “on” 表示启用，“off” 表示禁用反向 DNS 查找，或 “double” 表示启用双重反向 DNS 查找
- 允许在 `*.conf` 中的任何位置

`ServerLimit` (`prefork.c`)
- Apache 此次运行的 `MaxClients` 最大值
- 仅允许在 `*.conf` 中 `<Directory>`、`<Files>` 或 `<Location>` 之外

`KeepAlive` (`http_core.c`)
- 是否应将持久连接设为 `On` 或 `Off`
- 仅允许在 `*.conf` 中 `<Directory>`、`<Files>` 或 `<Location>` 之外

`LoadModule` (`mod_so.c`)
- 一个模块名称以及从中加载它的共享对象文件名
- 仅允许在 `*.conf` 中 `<Directory>`、`<Files>` 或 `<Location>` 之外

### Hack 81. 修改后验证 httpd.conf

使用选项 `-t` 来验证特定 Apache 配置文件是否存在问题。以下示例显示 `httpd.conf.debug` 第 148 行存在问题。`mod_auth_basicso` 在 `so` 之前缺少一个 `.`（句点）。

```bash
# httpd -t -f conf/httpd.conf.debug
```

输出：
```
httpd：语法错误在第 148 行的
/etc/httpd/conf/httpd.conf.debug：
无法加载 /etc/httpd/modules/mod_auth_basicso 到服务器：
/etc/httpd/modules/mod_auth_basicso：无法打开共享对象文件：没有此类文件或目录
```

修复问题后，它将显示 `Syntax OK`。

```bash
# httpd -t -f conf/httpd.conf.debug
```

输出：
```
Syntax OK
```

### Hack 82. 显示 httpd 构建参数

使用选项 `-V`（大写 `V`）来显示 Apache 版本号以及构建 Apache 时使用的所有参数。

```bash
# httpd -V
```

输出：
```
服务器版本：Apache/2.2.9 (Unix)
服务器构建时间：Jul 14 2008 15:36:56
服务器模块魔术数字：20051115:15
服务器加载：APR 1.2.12，APR-Util 1.2.12
编译使用：APR 1.2.12，APR-Util 1.2.12
架构：32 位
服务器 MPM：Prefork
线程化：否
分叉：是（可变进程数）
服务器编译时使用....

-D APACHE_MPM_DIR="server/mpm/prefork"
-D APR_HAS_SENDFILE
-D APR_HAS_MMAP

APR_HAVE_IPV6 (IPv4-mapped addresses enabled)
APR_USE_SYSVSEM_SERIALIZE
APR_USE_PTHREAD_SERIALIZE
SINGLE_LISTEN_UNSERIALIZED_ACCEPT
APR_HAS_OTHER_CHILD
APR_HAVE_RELIABLE_PIPED_LOGS
DYNAMIC_MODULE_LIMIT=128

HTTPD_ROOT="/etc/httpd"
SUEXEC_BIN="/usr/sbin/suexec"
DEFAULT_PIDLOG="logs/httpd.pid"
DEFAULT_SCOREBOARD="logs/apache_runtime_status"
DEFAULT_LOCKFILE="logs/accept.lock"
DEFAULT_ERRORLOG="logs/error_log"
AP_TYPES_CONFIG_FILE="conf/mime.types"

SERVER_CONFIG_FILE="conf/httpd.conf"
```

如果只想显示 Apache 版本号，请使用以下所示的选项 `-v`（小写 `v`）。

```bash
# httpd -v
```

输出：
```
服务器版本：Apache/2.2.9 (Unix)
服务器构建时间：Jul 14 2008 15:36:56
```

### Hack 83. 按需加载特定模块

有时你可能不想在 Apache 中加载所有模块。例如，你可能只想在测试 LDAP 时才向 Apache 加载与 `ldap` 相关的模块。这可以按如下方式实现。

修改 `httpd.conf` 并添加名为 `load-ldap` 的 `IfDefine` 指令（你可以随意命名）。

```apache
<IfDefine load-ldap>
    LoadModule ldap_module modules/mod_ldap.so
    LoadModule authnz_ldap_module modules/mod_authnz_ldap.so
</IfDefine>
```

当你正在测试 `ldap` 并希望加载与 `ldap` 相关的模块时，将 `load-ldap` 传递给选项 `-D`，如下所示：

```bash
# httpd -k start -e debug -Dload-ldap -f /etc/httpd/conf/httpd.conf.debug
```

输出示例：
```
[Sun Aug 17 14:14:58 2008] [debug] mod_so.c(246):
loaded module ldap_module
[Sun Aug 17 14:14:58 2008] [debug] mod_so.c(246):
loaded module authnz_ldap_module
```

[注意：传递 `-Dload-ldap` 以将 `ldap` 模块加载到 Apache]

如果不加载特定模块，正常启动 Apache：

```bash
# apachectl start
```

[注意：如果不想加载 `ldap` 模块，请正常启动 Apache。]

## 第 11 章：Bash 脚本

### Hack 84. .bash_* 文件的执行顺序

以下文件的执行顺序是什么？

- `/etc/profile`
- `~/.bash_profile`
- `~/.bashrc`
- `~/.bash_login`
- `~/.profile`
- `~/.bash_logout`

#### 交互式登录 shell 的执行顺序

以下伪代码解释了这些文件的执行顺序。

```bash
execute /etc/profile

IF ~/.bash_profile exists THEN
  execute ~/.bash_profile
ELSE
  IF ~/.bash_login exist THEN
    execute ~/.bash_login
  ELSE
    IF ~/.profile exist THEN
      execute ~/.profile
    END IF
  END IF
END IF
```

当你退出交互式 shell 时，执行顺序如下：

```bash
IF ~/.bash_logout exists THEN
  execute ~/.bash_logout
END IF
```

请注意，`/etc/bashrc` 由 `~/.bashrc` 执行，如下所示：

```bash
# cat ~/.bashrc
if [ -f /etc/bashrc ]; then
. /etc/bashrc
fi
```

#### 交互式非登录 shell 的执行顺序

启动非登录交互式 shell 时，执行顺序如下：

```bash
IF ~/.bashrc exists THEN
  execute ~/.bashrc
END IF
```

注意：当非交互式 shell 启动时，它会查找 `ENV` 环境变量，并执行 `ENV` 变量中提到的文件名值。

### Hack 85. 如何在 bash shell 中生成随机数

使用 `$RANDOM` bash 内置函数生成 0 – 32767 之间的随机数，如下所示。

```bash
$ echo $RANDOM
106
$ echo $RANDOM
22543
$ echo $RANDOM
25387
$ echo $RANDOM
647
```

### Hack 86. 调试 shell 脚本

要调试 shell 脚本，请在脚本顶部使用 `set -xv`。

无调试命令的 Shell 脚本：

```bash
$ cat filesize.sh
#!/bin/bash
for filesize in $(ls -l . | grep "^-" | awk '{print $5}')
do
  let totalsize=$totalsize+$filesize
done
echo "Total file size in current directory: $totalsize"
```

无调试命令的 Shell 脚本输出：

```bash
$ ./filesize.sh
当前目录总文件大小：652
```

带有调试命令的 Shell 脚本：

现在在 shell 脚本中添加 `set -xv` 以调试输出，如下所示。

```bash
$ cat filesize.sh
#!/bin/bash
```



```bash
set -xv

for filesize in $(ls -l . | grep "^-" | awk '{print $5}')

do

  let totalsize=$totalsize+$filesize

done

echo "Total file size in current directory: $totalsize"
```

带有调试命令的 Shell 脚本输出：

```bash
$ ./fs.sh

++ ls -l .
++ grep '^-'
++ awk '{print $5}'
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=+178
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=178+285
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=463+189
+ echo 'Total file size in current directory: 652'

Total file size in current directory: 652
```

使用调试选项执行 Shell 脚本：

除了在 shell 脚本内部给出 `set -xv` 外，你也可以在执行 shell 脚本时提供它，如下所示。

```bash
$ bash -xv filesize.sh
```

### Hack 87. 引号

不带特殊字符的 `echo` 语句。

```bash
$ echo The Geek Stuff
```

The Geek Stuff

`echo` 语句带有一个特殊字符 `;`。分号是 `bash` 中的命令终止符。在以下示例中，“The Geek” 对 `echo` 有效，而 “Stuff” 被视为单独的 Linux 命令并导致命令未找到。

```bash
$ echo The Geek; Stuff
```

The Geek

`-bash: Stuff: command not found`

为避免这种情况，你可以在分号前添加 `\`，这将移除分号的特殊含义并仅将其打印出来，如下所示。

```bash
$ echo The Geek\; Stuff
```

The Geek; Stuff

### 单引号

当你想逐字打印单引号内的所有内容时，使用单引号。即使是 `$HOSTNAME` 这样的特殊变量也会被打印为 `$HOSTNAME`，而不是打印 Linux 主机的名称。

```bash
$ echo 'Hostname=$HOSTNAME ; Message=\$ is USD'
```

Hostname=$HOSTNAME ;

Message=\$ is USD

Current User=`whoami` ;

### 双引号

当你想显示特殊变量的真实含义时，使用双引号。

```bash
$ echo "Hostname=$HOSTNAME ; Message=\$ is USD"
```

Current User=`whoami` ;

### Linux 技巧

Ajay Kumar Tiwari

主机名=dev-db ; 当前用户=ramesh ; 消息=$ 是 USD

双引号将移除所有字符的特殊含义，除了以下情况：

- `$` 参数替换。
- `` ` `` 反引号
- `\$` 字面美元符号。
- `` \` `` 字面反引号。
- `\"` 嵌入式双引号。
- `\` 嵌入式反斜杠。

### Hack 88. 在 shell 脚本中读取数据文件字段

本示例展示了如何从数据文件中读取特定字段并在 shell 脚本中对其进行操作。例如，假设 `employees.txt` 文件的格式为 `{employee-name}:{employee-id}:{department-name}`，以冒号分隔的文件如下所示。

```bash
$ cat employees.txt
Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
```

以下 shell 脚本解释了如何从此 `employees.txt` 文件中读取特定字段。

```bash
$ vi read-employees.sh
#!/bin/bash
IFS=:
echo "Employee Names:"
echo "_____"
while read name empid dept
do
  echo "$name is part of $dept department"
done < ~/employees.txt
```

为 shell 脚本分配执行权限并执行它。

```bash
$ chmod u+x read-employees.sh
```

```bash
$ ./read-employees.sh
```

员工姓名：

Emma Thomas 是 Marketing 部门的一员

Alex Jason 是 Sales 部门的一员

Madison Randy 是 Product Development 部门的一员

Sanjay Gupta 是 Support 部门的一员

Nisha Singh 是 Sales 部门的一员

## 第 12 章：系统监控与性能

### Hack 89. free 命令

`free` 命令显示有关系统物理（RAM）和交换内存的所有必要信息。

语法：`free [options]`

### 我的系统总 RAM 是多少？

在下面的示例中，此系统的总物理内存为 1GB。以下显示的值以 KB 为单位。

```bash
# free
              total       used       free     shared    buffers     cached
Mem:       1034624    1006696      27928          0      174136     615892
-/+ buffers/cache:
Swap:      2031608          0     2031608
```

### 包括 RAM 和 Swap 在内，我系统的总内存是多少？

在以下命令中：

- 选项 `m` 以 MB 显示值
- 选项 `t` 显示“Total”行，即物理内存和交换内存值的总和
- 选项 `o` 用于隐藏上述示例中的 buffers/cache 行。

```bash
# free -mto
```

输出：

| | 总计 | 已用 | 空闲 | 共享 | 缓冲 | 缓存 |
|---|---|---|---|---|---|---|
| 内存 | 1010 | 983 | 27 | 0 | 170 | 601 |
| 交换 | 1983 | 0 | 1983 | | | |
| 总计 | 2994 | 983 | 2011 | | | |

### Hack 90. top 命令

`top` 命令显示有关系统各种性能指标的实时信息，例如 CPU 负载、内存使用情况、进程列表等。

语法：`top [options]`

### 如何查看包括 CPU 使用率在内的当前系统状态？

从命令行不带任何选项执行 `top`，将显示下面所示的输出。`top` 命令输出将持续显示实时值，直到您按“Control + c”或 `q` 退出命令输出为止。

```bash
# top
top - 13:10:13 up 171 days, 20:21, 3 users, load average: 0.01, 0.05, 0.00
Tasks: 194 total, 1 running, 193 sleeping, 0 stopped, 0 zombie
Cpu(s): 0.6% us, 0.7% sy, 0.0% ni, 98.7% id, 0.0% wa, 0.0% hi, 0.0% si
Mem: 1034624k total, 1007420k used, 27204k free, 174540k buffers
Swap: 2031608k total, 0k used, 2031608k free, 615904k cached
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m 3916 S 10.2 0:46.35 httpd
19299 oracle 19 0 279m 18m 17m S 10.2 0:00.03 oracle
11398 jsmith 16 0 107m 28m 6404 S 0.4 0:03.07 perl
```

### 如何阅读上面显示的 top 命令输出？

- 第 1 行“top”表示系统已运行 171 天。
- 第 2 行“Tasks”显示进程总数以及运行中、睡眠中、已停止和僵尸进程数的细分。



- 第 3 行“`Cpu(s)`”显示系统的当前 CPU 利用率。在此示例中，CPU 空闲 98.7%

- 第 4 行“`Mem`”和第 5 行“`Swap`”提供内存信息。这与 `free` 命令中的信息相同。

其余行显示系统上的所有活动进程，默认按 CPU 使用率（`%CPU` 列）排序。即最占用 CPU 的进程默认会显示在顶部。

`top` 命令有多个命令行选项和交互选项。让我们回顾一下 `top` 命令的几个基本选项。

### 如何识别最占用内存的进程？

在显示 `top` 命令输出时，按 `F`，将显示以下消息并显示所有可用于排序的字段，按 `n`（用于按内存排序进程）并按回车。这将按内存使用情况对 `top` 输出中的进程进行排序。

```
Current Sort Field: K for window 1:Def

Select sort field via field letter, type any other key to return
```

### 如何向 top 输出添加额外字段（例如 CPU 时间）？

在 `top` 命令运行时，按 `f`，将显示以下消息并显示所有可用于显示的字段，按 `l`，将在 `top` 输出的显示列中添加 CPU 时间。

```
Current Fields: AEHIOQTWKNMbcdfgjplrsuvyzX for window 1:Def

Toggle fields via field letter, type any other key to return
```

### 如何获取正在运行进程的完整路径名和参数？

在 `top` 命令运行时，按 `c`，将在命令列中显示正在运行进程的完整路径名，如下所示。即不是显示 `httpd`，而是显示 `/usr/local/apache2/bin/httpd`。

```
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m 3916 S 0.2 0:46.35 /usr/local/apache2/bin/httpd
```

### 如何在 top 命令中查看各个 CPU？

在 `top` 命令运行时，按 `1`（数字一），将显示该机器上各个 CPU 的性能数据，如下所示。

```
top - 13:10:13 up 171 days, 20:21, 3 users, load average: 0.01, 0.05, 0.00
Tasks: 194 total, 1 running, 193 sleeping, 0 stopped, 0 zombie
Cpu0 : 10.2% us, 2.6% sy, 0.0% ni, 86.8% id, 0.3% wa, 0.0% hi, 0.0% si
Cpu1 : 9.6% us, 8.0% sy, 0.0% ni, 82.4% id, 0.0% wa, 0.0% hi, 0.0% si
Cpu2 : 1.3% us, 1.3% sy, 0.0% ni, 95.0% id, 2.3% wa, 0.0% hi, 0.0% si
Cpu3 : 0.0% us, 0.0% sy, 0.0% ni, 100.0% id, 0.0% wa, 0.0% hi, 0.0% si
Mem: 1034624k total, 1007420k used, 27204k free, 174540k buffers
Swap: 2031608k total, 0k used, 2031608k free, 615904k cached
```

### Hack 91. ps 命令

`ps` 命令（process status）将显示所有活动进程的快照信息。

语法：`ps [options]`

#### 如何显示系统中运行的所有进程？

使用“`ps aux`”，如下所示。

```
# ps aux | more
```

```
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 1 0.0 0.0 2044 588 ? Ss Jun27 0:00 init [5]
apache 31186 0.0 1.6 23736 17556 ? S Jul26 0:40 /usr/local/apache2/bin/httpd
apache 31187 0.0 1.3 20640 14444 ? S Jul26 0:37 /usr/local/apache2/bin/httpd
```

您也可以使用“`ps -ef | more`”来获得类似的输出

#### 打印进程树

您可以使用 `ps axuf` 或 `ps -ejH` 以树格式显示进程。

树结构有助于立即可视化进程及其父进程。为了清晰起见，下面的输出中已截断了几列。

```
# ps axuf
```

```
root
root
root
root
root
root
root
root
root
511
511
Oct14
Oct14
Oct14
Oct14
Oct14
Oct 14
Dec03
Dec22
23:35
23:35
0:00 /opt/VRTSralus/bin/beremote
0:00 \_/opt/VRTSralus/bin/beremote
0:00\_/opt/VRTSralus/bin/beremote
0:00\_/opt/VRTSralus/bin/beremote
0:01\_/opt/VRTSralus/bin/beremote
0:00\_/opt/VRTSralus/bin/beremote
0:01 /usr/local/sbin/sshd
1:08 /usr/local/sbin/sshd
0:00 \_/usr/local/sbin/sshd
0:00\_ -bash
\_ ps axuf
```

注意：您也可以使用 `pstree` 命令以树结构显示进程。

#### 查看特定用户拥有的进程

以下命令显示 Linux 用户名 `oracle` 所拥有的所有进程：

```
$ ps U oracle
```

```
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnslsnr
0:00 ora_q002_med
0:00 ora_cjq0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oraclemed (LOCAL=NO)
```

## 查看当前用户拥有的进程

以下命令显示当前用户拥有的所有进程。

```
$ ps U $USER
```

```
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
TIME COMMAND
0:00 sshd: ramesh@pts/1,pts/2
0:00 -bash
10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U ramesh
```

### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

#### 我的系统上有多少 GB 磁盘空间可用？

如下所示使用 `df -h`。选项 `-h` 以人类可读的格式显示值（例如：`K` 表示 Kb，`M` 表示 Mb，`G` 表示 Gb）。在下面的示例输出中，`/` 文件系统有 17GB 磁盘空间可用，而 `/home/user` 文件系统有 70GB 可用。

```
# df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 70G | 49% | /home/user |

#### 我的系统上使用什么类型

以下命令显示 Linux 用户名 `oracle` 所拥有的所有进程：

```
$ ps U oracle
```

```
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnslsnr
0:00 ora_q002_med
0:00 ora_cjq0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oraclemed (LOCAL=NO)
```

## 查看当前用户拥有的进程

以下命令显示当前用户拥有的所有进程。

```
$ ps U $USER
```

```
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
TIME COMMAND
0:00 sshd: ramesh@pts/1,pts/2
0:00 -bash
10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U ramesh
```



### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

### 我的系统上有多少 GB 磁盘空间可用？

如下所示使用`df -h`。选项`-h`以人类可读的格式显示值（例如：`K`表示 `Kb`，`M`表示 `Mb`，`G`表示 `Gb`）。在下面的示例输出中，`/`文件系统有 17GB 磁盘空间可用，而`/home/user`文件系统有 70GB 可用。

```
# df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 70G | 49% | /home/user |

### 我的系统上使用什么类型的

以下命令显示 Linux 用户名 `oracle` 所拥有的所有进程：

```
$ ps U oracle
```

```
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnslsnr
0:00 ora_q002_med
0:00 ora_cjq0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oraclemed (LOCAL=NO)
```

## 查看当前用户拥有的进程

以下命令显示当前用户拥有的所有进程。

```
$ ps U $USER
```

```
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
TIME COMMAND
0:00 sshd: ramesh@pts/1,pts/2
0:00 -bash
10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U ramesh
```

### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

### 我的系统上有多少 GB 磁盘空间可用？

如下所示使用`df -h`。选项`-h`以人类可读的格式显示值（例如：`K`表示 `Kb`，`M`表示 `Mb`，`G`表示 `Gb`）。在下面的示例输出中，`/`文件系统有 17GB 磁盘空间可用，而`/home/user`文件系统有 70GB 可用。

```
# df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 70G | 49% | /home/user |

### 我的系统上使用什么类型的

以下命令显示 Linux 用户名 `oracle` 所拥有的所有进程：

```
$ ps U oracle
```

```
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnslsnr
0:00 ora_q002_med
0:00 ora_cjq0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oraclemed (LOCAL=NO)
```

## 查看当前用户拥有的进程

以下命令显示当前用户拥有的所有进程。

```
$ ps U $USER
```

```
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
TIME COMMAND
0:00 sshd: ramesh@pts/1,pts/2
0:00 -bash
10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U ramesh
```

### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

### 我的系统上有多少 GB 磁盘空间可用？

如下所示使用`df -h`。选项`-h`以人类可读的格式显示值（例如：`K`表示 `Kb`，`M`表示 `Mb`，`G`表示 `Gb`）。在下面的示例输出中，`/`文件系统有 17GB 磁盘空间可用，而`/home/user`文件系统有 70GB 可用。

```
# df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 70G | 49% | /home/user |

### 我的系统上使用什么类型的

以下命令显示 Linux 用户名 `oracle` 所拥有的所有进程：

```
$ ps U oracle
```

```
PID TTY
5014 ?
7124 ?
8206 ?
8852 ?
8854 ?
8911 ?
STAT
Ss
Ss
Ss
Ss
Ss
Ss
TIME COMMAND
0:01 /oracle/bin/tnslsnr
0:00 ora_q002_med
0:00 ora_cjq0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oraclemed (LOCAL=NO)
```

## 查看当前用户拥有的进程

以下命令显示当前用户拥有的所有进程。

```
$ ps U $USER
```

```
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
TIME COMMAND
0:00 sshd: ramesh@pts/1,pts/2
0:00 -bash
10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U ramesh
```

### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

### 我的系统上有多少 GB 磁盘空间可用？



### 我的系统上使用什么类型的文件系统及磁盘空间？

#### Hack 92. Df 命令

`df` 命令（disk free）显示已挂载文件系统上总计和空闲磁盘空间的数量。

语法：`df [options] [name]`

#### 我的系统上有多少 GB 磁盘空间可用？

如下所示使用 `df -h`。选项 `-h` 以人类可读的格式显示值（例如：K 表示 Kb，M 表示 Mb，G 表示 Gb）。在下面的示例输出中，`/` 文件系统有 17GB 磁盘空间可用，而 `/home/user` 文件系统有 70GB 可用。

```
# df -h
```

| 文件系统 | 大小 | 已用 | 可用 | 使用% | 挂载点 |
|------------|------|------|-------|------|------------|
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 70G | 49% | /home/user |

### 测试翻译

### Linux 技巧

**Ajay Kumar Tiwari**

注意：`/etc/cron.d/sysstat` 文件随 `sysstat` 包一起提供，其中包含 `sa1` 和 `sa2` 的一些默认值，你可以根据需要进行更改。

#### 使用 Sar 命令显示 CPU 统计信息

```
# sar -u
```

```
Linux 2.6.9-42.ELsmp (dev-db)
12:00:01 AM CPU %user %nice
12:05:01 AM all 3.70 0.00
12:10:01 AM all 4.59 0.00
12:15:01 AM all 3.90 0.00
12:20:01 AM all 4.06 0.00
12:25:01 AM all 3.89 0.00
12:30:01 AM all 3.89 0.00
Skipped..
Average: all 4.56 0.00 1.00 0.15 94.29 01/01/2009
%system %iowait
0.85 0.00
1.19 0.06
0.95 0.04
1.00 0.01
0.87 0.00
0.87 0.00
%idle
95.45
94.16
95.11
94.93
95.23
95.23
```

注意：如果需要各个 CPU 的性能数据细分，请执行以下命令。

```
# sar -u -P ALL
```

#### 使用 sar 命令显示磁盘 IO 统计信息

```
# sar -d
```

```
Linux 2.6.9-42.ELsmp (dev-db)
12:00:01 AM DEV
12:05:01 AM dev2-0
12:10:01 AM dev8-1
Skipped..
Average:
dev2-0
dev8-1
4.66
1.89
120.77
3.17
69.45
8.02
01/01/2009
tps rd_sec/s
1.65 1.28
4.08 8.11
wr_sec/s
45.43
21.81
125
```

### Linux 技巧

**Ajay Kumar Tiwari**

#### 使用 sar 命令显示网络统计信息

```
# sar -n DEV | more
Linux 2.6.9-42.ELsmp (dev-db)
12:00:01 AM IFACE rxpck/s
rxcmp/s txcmp/s
rxmcst/s
12:05:01 AM lo 0.17
0.00 0.00
0.00
12:10:01 AM eth0 52.92
0.00 0.00
0.00
01/01/2009
txpck/s rxbyt/s
txbyt/s
0.16
25.31
23.33
53.64
10169.74
12178.57
```

```
# sar -n SOCK | more
Linux 2.6.9-42.ELsmp (dev-db)
12:00:01 AM tot sck t cpsck
12:05:01 AM 50 13
12:10:01 AM 50 13
12:15:01 AM 53 13
01/01/2009
udpsck rawsck
30
40
50
ip-frag
0
```

## Hack 97. vmstat 命令

对于典型的性能监控，你只需要 `vmstat` 命令。

它显示内存、交换、IO、系统和 CPU 性能信息。

以下命令每 1 秒执行 `vmstat` 100 次。

```
# vmstat 1 100
```

```
procs ------memory----- -swap- ---io--- -system-- --cpu--
r b swpd free buff cache si so
0 0 0 0 0 0 0 0
0 0 282120 134108 5797012 0 0
bi bo in cs
0 0 0 0
0 0 0 0
us sy id wa
0 0 100 0
1 0 100 7 359 0 0 100 0
0 0 1 117 577 0 0 100 0
0 0 1 1007 366 0 0 100 0
```

**Ajay Kumar Tiwari**

### Vmstat procs 部分

`r` 字段：可运行进程的总数

`b` 字段：阻塞进程的总数

### 内存部分

`swpd` 字段：已使用的交换空间

`free` 字段：可用空闲 RAM

`buff` 字段：用于缓冲区的 RAM

`cache` 字段：用于文件系统缓存的 RAM

### 交换部分

`si` 字段：每秒从磁盘交换到内存的内存量

`so` 字段：每秒从内存交换到磁盘的内存量

### IO 部分

`bi` 字段：从磁盘接收的块数

`bo` 字段：发送到磁盘的块数。

### 系统部分

`in` 字段：每秒中断数。

`cs` 字段：每秒上下文切换数。

### CPU 部分

`us` 字段：运行用户代码（非内核代码）所花费的时间。

`sy` 字段：运行内核代码所花费的时间。

`id` 字段：空闲时间。

`wa` 字段：等待 IO 所花费的时间

## Hack 98. Netstat 命令

`netstat` 命令显示网络相关信息，例如网络连接、路由表、接口统计信息。以下是有关如何使用 `netstat` 命令的几个示例。

### 使用 netstat 显示活动 Internet 连接和域套接字

```
# netstat -an
```

活动 Internet 连接（服务器和已建立）

| Proto | Recv-Q | Send-Q | Local Address | Foreign Address | State |
| :--- | :--- | :--- | :--- | :--- | :--- |
| tcp | 0 | 0 | 0.0.0.0:5666 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:1110 | 0.0.0.0:* | LISTEN |
| tcp | 0 | 0 | 0.0.0.0:4086 | 0.0.0.0:* | LISTEN |

活动 UNIX 域套接字（服务器和已建立）

| Proto | RefCnt | Flags | Type | State | I-Node | Path |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| unix | 2 | [ ACC ] | STREAM | LISTENING | 7894 | /tmp/.font-unix/fs7100 |
| unix | 2 | [ ACC ] | STREAM | LISTENING | 9662 | /tmp/.gdm_socket |
| unix | 2 | [ ACC ] | STREAM | LISTENING | 10897 | @/tmp/fam-root- |

### 显示带进程 ID 和程序名称的活动连接

这对于识别哪个程序启动了特定的网络连接非常有帮助。



### 显示活动连接

```
# netstat -tap
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp 0 0 *:nrpe *:* LISTEN 16277/xinetd
tcp 0 0 localhost.localdomain:smtp *:* LISTEN 7263/sendmail: acce
tcp 340 0 localhost.localdomain:54221 localhost.localdomain:4089 CLOSE_WAIT 29881/httpd
tcp 0 3216 dev-db:ssh cpe-76-94-215-154.soca:4682 ESTABLISHED 11717/sshd: ramesh
```

### 显示路由表

```
# netstat -r
Kernel IP routing table
Destination Gateway Genmask Flags Iface MSS Window irtt
192.168.1.0 * 255.255.255.0 U eth0 0 0
162.244.0.0 * 255.255.0.0 U eth0 0 0
default 192.168.1.1 0.0.0.0 UG eth0 0 0
```

### 显示 RAW 网络统计信息

```
# netstat --statistics --raw
```

`Ip:`

`129 11080343 total packets received`
`0 forwarded`
`1 with unknown protocol`
`0 incoming packets discarded`
`11037744 incoming packets delivered`
`11199763 requests sent out`

`Icmp:`

`577135 ICMP messages received`
`64 input ICMP message failed.`
`ICMP input histogram:`
`destination unreachable: 537`
`timeout in transit: 65`
`source quenches: 2`
`echo requests: 576476`
`echo replies: 12`
`timestamp request: 3`
`address mask request: 3`

`581558 ICMP messages sent`
`0 ICMP messages failed`
`ICMP output histogram:`
`destination unreachable: 5079`
`echo replies: 576476`
`timestamp replies: 3`

### 杂项 Netstat 命令

`# netstat --tcp --numeric` 列出机器进出 TCP 连接。

`# netstat --tcp --listening --programs` 显示服务器正在监听的 TCP 端口以及正在监听该端口的程序。

`# netstat -rnC` 显示路由缓存。

## Hack 99. Sysctl 命令

Linux 内核参数可以使用 `sysctl` 命令实时更改。

### Linux 技巧

`Ajay Kumar Tiwari`

`sysctl` 有助于在运行时配置 Linux 内核参数。

```
# sysctl -a
```

```
dev.cdrom.autoclose = 1
fs.quota.writes = 0
kernel.ctrl-alt-del = 0
kernel.domainname = (none)
kernel.exec-shield = 1
net.core.somaxconn = 128
net.ipv4.tcp_window_scaling = 1
net.ipv4.tcp_wmem = 4096 16384
net.ipv6.route.mtu_expires = 600
sunrpc.udp_slot_table_entries = 16
vm.block_dump = 0
```

### 在 /etc/sysctl.conf 中修改内核参数以实现永久更改

修改 `/etc/sysctl.conf` 中的内核参数后，执行 `sysctl -p` 以提交更改。重启后更改仍然存在。

```
# vi /etc/sysctl.conf
```

```
# sysctl -p
```

### 临时修改内核参数

要临时修改内核参数，请执行以下命令。

请注意，重启后这些更改将会丢失。

```
# sysctl -w {variable-name=value}
```

### Linux 技巧

`Ajay Kumar Tiwari`

## Hack 100. Nice 命令

内核根据 `nice` 值决定进程所需的处理器时间。可能的 `nice` 值范围为：-20 到 20。`nice` 值为 -20 的进程优先级非常高。`nice` 值为 20 的进程优先级非常低。

使用 `ps axl` 显示所有正在运行进程的 `nice` 值，如下所示。

```
# ps axl
F UID PID PPID PRI NI SZ RSS WCHAN STAT TTY
TIME COMMAND
4010 160 2172 552 -S ?
0:17 init [5]
1031 34 1900 ksofti SN ?
3:18 [ksoftirq/0]
1010 15 -100 0 worker S <?
0:01 [events/0]
40 51451 25 10 32124 18592 -SNs ?
0:08 /usr/bin/python /usr/bin/rhn-applet-gui --sm-client-id default4
40 5147 5142 160 3528 604 -S ?
0:00 /sbin/pam_timestamp_check -d root
1503 17552 4180 160 14208 3920 -S ?
0:01 /home/www/apache2/bin/httpd -f
/home/www/apache2/conf/httpd.conf -k start
```

### 如何为 shell 脚本分配较低的优先级？（较高的 nice 值）

在下面的示例中，当我在后台启动 `nice-test.sh` 脚本时，它采用的 `nice` 值为 0。

```
$ ./nice-test.sh &
[3] 13009
$ ps axl | grep nice-test
0509 13009 12863 170
4652
972 wait
S
132
### Linux 技巧
pts/1
Ajay Kumar Tiwari
0:00 /bin/bash ./nice-test.sh
```

[Note: 第 6 列的值为 0 是 `nice` 值。]

现在，让我们使用不同的 `nice` 值执行相同的 shell 脚本，如下所示。

```
$ nice -10 ./nice-test.sh &
```

```
[1] 13016
```

```
$ ps axl | grep nice-test
```

```
0509 13016 12863 30 10 4236 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
```

`SN`

[Note: 第 6 列的值为 10 是 shell 脚本的 `nice` 值。]

### 如何为 shell 脚本分配高优先级？（降低 nice 值）

在下面的示例中，让我们将 `nice` 值 -10（负 10）分配给 `nice-test.sh` shell 脚本。

```
$ nice -10 ./nice-test.sh &
```

```
[1] 13021
```

```
$ nice: cannot set priority: Permission denied
```

注意：只有 `root` 用户才能设置负的 `nice` 值。请以 `root` 身份登录并尝试相同操作。请注意，下面的 `nice` 命令中 10 前面有两个破折号。

```
# nice -10 ./nice-test.sh &
```

```
[1] 13060
```

```
# ps axl | grep nice-test
```

```
40 13060 13024 10 -10 5388 964 wait
pts/1 0:00 /bin/bash ./nice-test.sh
```

`133 S<`

### Linux 技巧

`Ajay Kumar Tiwari`

[Note: 第 6 列的值为 -10 是 shell 脚本的 `nice` 值。]



### Hack 101. Renice 命令

`renice` 会更改正在运行进程的调度优先级。

如何降低正在运行进程的优先级？（增加 `nice`）

在下面的示例中，一个现有的 shell 脚本以 `nice` 值为 `10` 运行。

（`ps` 输出中的第 6 列）

```
$ ps axl | grep nice-test
0509 13245 13216 30 10 5244 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

要增加 `nice` 值（从而降低优先级），请按如下所示执行 `renice` 命令。

```
$ renice 16 -p 13245
13245: old priority 10, new priority 16
$ ps axl | grep nice-test
0509 13245 13216 36 16 5244 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

[Note: 现在，`nice-test.sh`（`PID` 13245）的第 6 列显示新的 `nice` 值为 16。]

如何提高正在运行进程的优先级？（降低 `nice`）

在下面的示例中，一个现有的 shell 脚本以 `nice` 值为 `10` 运行。

134

### Linux 技巧

（`ps` 输出中的第 6 列）

Ajay Kumar Tiwari

```
$ ps axl | grep nice-test
0509 13254 13216 30 10 4412 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

要提高优先级，请按如下所示给出较低的 `nice` 值。但是，只有 `root` 才能提高正在运行进程的优先级，否则您会收到以下错误消息。

```
$ renice 5 -p 13254
renice: 13254: setpriority: Permission denied
```

以 `root` 身份登录以提高正在运行进程的优先级

```
$ su -
# renice 5 -p 13254
13254: old priority 10, new priority 5
# ps axl | grep nice-test
0509 13254 13216 255 4412 968 wait
pts/1 0:00 /bin/bash ./nice-test.sh
SN
```

[Note: 第 6 列现在显示较低的 `nice` 值为 5（优先级提高）]

### Linux 技巧

Ajay Kumar Tiwari

### Linux 技巧
