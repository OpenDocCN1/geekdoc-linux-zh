
# Linux 攻击实战

- 使用 `SysRq` 键安全重启 Linux

## 简介

世界上只有 10 类人：懂二进制的![图](img/340b68128e85f9b34d5bae9c5ff0cdd8_0_0.png)，不懂二进制的，以及从 `Stack Overflow` 复制粘贴的。这些技巧将帮助你更有效地导航 `Linux` 环境。

## 前言

另一个为热爱命令行并想要探索 `Linux` 系统深度准备的技巧集。

| 日期 | 版本 |
|---|---|
| 2015 | |

## 第 1 章：强大的 `cd` 命令技巧

- 使用 `CDPATH` 定义 `cd` 命令的基础目录
- 使用 `cd` 别名高效地返回上级目录
- 使用单条命令完成 `mkdir` 和 `cd`
- 使用 `"cd -"` 在最后两个目录之间切换
- 使用 `dirs`、`pushd` 和 `popd` 操作目录栈
- 使用 `"shopt -s spell"` 在 `cd` 时自动纠正拼错误的目录名

### 方法 1：使用 `alias` 定义快捷方式

正常工作。

`alias ..="cd .."`

```
alias ..="cd ../"
alias ...="cd ../.."
alias ....="cd ../../"
alias .....="cd ../../../"
```

```
# /tmp/very/long/directory/structure/that/is/too_deep
# .....
```

> [注意：使用 `....`（四个点）返回 4 级目录]

```
# pwd
/tmp/very/long/directory/structure/
```

### 方法 3：使用 `cd` 后接连续的点来导航目录

在下面的示例中，使用 `cd.....`（`cd` 后接五个点）来返回 4 级目录。将其设为 5 个点以返回 4 级目录结构非常容易记忆，因为当你输入前两个点时，你是在想“向上一个目录”，之后每多一个点，就代表向上跳一级。因此，使用 `cd....`（`cd` 后接四个点）返回 3 级目录，使用 `cd...`（`cd` 后接三个点）返回 2 级目录。将以下 `alias` 添加到 `~/.bash_profile` 并重新登录，使上述 `cd.....`（五个点）能够正常工作。

```
alias cd..="cd .."
alias cd...="cd ../"
alias cd....="cd ../../"
alias cd.....="cd ../../../"
```

```
cd......="cd ../../../../../"
# cd /tmp/very/long/directory/structure/that/is/too_deep
# cd......
[注意：使用 cd...... 返回 4 级目录]
# pwd
/tmp/very/long/directory/structure
```

在下面的示例中，使用 `cd4`（`cd` 后接数字 4）来返回 4 级目录。

```
alias cd1="cd ."
alias cd2="cd ../"
alias cd3="cd ../../"
alias cd4="cd ../../../"
alias cd5="cd ../../../../"
```

### 技巧 3：使用单条命令执行 `mkdir` 和 `cd`

有时当你创建一个新目录时，可能需要立即进入该新目录，如下所示。

```bash
# mkdir -p /tmp/subdir1/subdir2/subdir3
# cd /tmp/subdir1/subdir2/subdir3
# pwd
/tmp/subdir1/subdir2/subdir3
```

将 `mkdir` 和 `cd` 合并为一条命令不是很棒的吗？将以下内容添加到 `.bash_profile` 并重新登录。

```bash
$ vi .bash_profile
function mkdircd() { mkdir -p "$@" && eval cd "\$\$@\"\#\"; }
```

现在，使用单条命令同时执行 `mkdir` 和 `cd`，如下所示：

`# mkdircd /tmp/subdir1/subdir2/subdir3`

> [注意：会自动创建目录并进入该目录]

```
# pwd
/tmp/subdir1/subdir2/subdir3
```

### 技巧 4：使用 `"cd -"` 在最后两个目录之间切换

你可以使用下方的 `cd -` 在最后两个当前目录之间切换。

```bash
# cd /tmp/very/long/directory/structure/that/is/too_deep
# cd /tmp/subdir1/subdir2/subdir3
# cd -
# pwd
/tmp/very/long/directory/structure/that/is/too_deep
# cd -
# pwd
/tmp/subdir1/subdir2/subdir3
# cd -
# pwd
/tmp/very/long/directory/structure/that/is/too_deep
```

### 技巧 5：使用 `dirs`、`pushd` 和 `popd` 来操作目录栈

你可以使用目录栈将目录推入栈中，稍后从栈中弹出。本示例中使用了以下三个命令。

- `dirs`: 显示目录栈
- `pushd`: 将目录推入栈中
- `popd`: 从栈中弹出目录并进入该目录

`dirs` 总是会打印当前目录，然后是栈的内容。即使目录栈为空，`dirs` 命令仍然只会打印当前目录，如下所示。

```bash
# popd
-bash: popd: directory stack empty
# pwd
/home/ramesh
```

```bash
# mkdir /tmp/dir1
# mkdir /tmp/dir2
# mkdir /tmp/dir3
# mkdir /tmp/dir4
# cd /tmp/dir1
# pushd .
# cd /tmp/dir2
# pushd .
# cd /tmp/dir3
# pushd .
# cd /tmp/dir4
# pushd .
```

```bash
# dirs
/tmp/dir4 /tmp/dir4 /tmp/dir3 /tmp/dir2 /tmp/dir1
```

> [注意：`dirs` 命令的第一个目录 (`/tmp/dir4`) 始终是当前目录，而不是栈的内容。]

在此阶段，目录栈包含以下内容：

- `/tmp/dir4`
- `/tmp/dir3`
- `/tmp/dir2`
- `/tmp/dir1`

最后推入栈的目录将位于顶部。当你执行 `popd` 时，它将进入栈顶部的目录并将其从栈中移除。如所示，最后推入栈的目录是 `/tmp/dir4`。因此，当我们执行 `popd` 时，它会进入 `/tmp/dir4` 并将其从目录栈中移除。

```bash
# popd
# pwd
/tmp/dir4
```

> [注意：执行 `popd` 后，目录栈包含：`/tmp/dir3`、`/tmp/dir2`、`/tmp/dir1`]

```bash
# popd
# pwd
/tmp/dir3
```

> [注意：执行 `popd` 后，目录栈包含：`/tmp/dir2`、`/tmp/dir1`]

```bash
# popd
# pwd
/tmp/dir2
```

> [注意：执行 `popd` 后，目录栈包含：`/tmp/dir1`]

```bash
# popd
# pwd
/tmp/dir1
```

> [注意：执行 `popd` 后，目录栈为空！]

### 技巧 6：使用 `"alias"` 纠错

使用下方的 `alias` 自动纠正错误输入的命令。

```bash
alias .='ls'
alias ..='cd ..'
alias ...='cd ../'
alias ....='cd ../../'
alias .....='cd ../../../'
alias ......='cd ../../../../'
```

### 技巧 7：设置日期和时间

使用以下参数设置系统日期和时间。

```bash
# date -s "2023-01-01 12:00:00"
```

常用格式：

```
- mm: 月
- dd: 日
- hh: 小时
- mi: 分钟
- yyyy: 年
- ss: 秒
```

### 技巧 8：显示日期和时间

使用以下格式显示系统日期和时间

```bash
# date
```

### 技巧 9：特定格式的格式

使用下方的 `alias` 自动纠正错误输入的命令。

```bash
alias .='ls'
alias ..='cd ..'
alias ...='cd ../'
```



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



`/home/users/subdir1/letter.txt`: John, Thanks for your contribution.

`/home/users/name_list.txt`: John Smith

```
/home/users/name_list.txt:John Doe
```

# `grep -ril john /root`

`/home/users/subdir1/letter.txt`

`/home/users/name_list.txt`

```
### 破解 18：`find` 命令

`find` 是一个常用的命令，用于根据多种条件在 UNIX 文件系统中查找文件。让我们复习 `find` 命令的一些练习示例。

语法：`find [pathnames] [conditions]`

### 如何找到文件名中包含特定单词的文件？

以下命令查找 `/etc` 目录下所有包含 "mail" 的文件。

```
# find /etc -name "mail*"
```

### 如何找到大于特定大小的文件？

以下命令将列出系统中所有大于 `100MB` 的文件。

```
# find / -type f -size +100M
```

### 如何找到过去 x 天内未修改的文件？

（注：此处原文未提供具体命令，仅翻译标题）

# 按升序排序文本文件

```
$ sort names.txt

Alex Jason:200:Sales
Emma Thomas:100:Marketing
Madison Randy:300:Product Development
Nisha Singh:500:Sales
Sanjay Gupta:400:Support
```

# 按降序排序文本文件

```
$ sort -r names.txt

Sanjay Gupta:400:Support
Nisha Singh:500:Sales
Madison Randy:300:Product Development
Emma Thomas:100:Marketing
Alex Jason:200:Sales
```

# 按冒号分隔的文本文件的第 2 （`employee_id`）排序

```
$ sort -t: -k2 names.txt

Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
```

# 按制表符分隔的文本文件的第 3 （`department_name`）排序并去除重复项

```
$ sort -t:'\t' -u -k3 names.txt
```

# 按第 3 字段（数字型 `userid`）排序 `passwd` 文件

```
$ sort -t: -3n /etc/passwd | more

root:x:0:0:root:/bin/bash
bin:x:1:1:bin:/sbin/nologin
demon:x:2:2:daemon:/sbin/nologin
adm:x:3:4:adm:/var/sbin/nologin
```

# 按 IP 地址排序 `/etc/hosts`

```
$ sort -k 1,1n -k 2,2n -k 3,3n -k 4,4n /etc/hosts

127.0.0.1 localhost.localdomain localhost
192.168.100.101 dev-db.thegeekstuff.com dev-db
192.168.100.102 prod-db.thegeekstuff.com prod-db
192.168.100.101 prod-web.thegeekstuff.com prod-web
```

# 将 `sort` 与其他命令结合

`ps -ef | sort` : 排序进程列表的输出
`ls -al | sort +4n` : 按文件大小升序列出文件。即按第 5 字段排序并先显示最小的文件。
`ls -al | sort +4nr` : 按文件大小降序列出文件。即按第 5 字段排序并先显示最大的文件。

Ajay Kumar Tiwari

# 技巧 24. `uniq` 命令

`uniq` 命令通常与 `sort` 命令结合使用，因为 `uniq` 只能从已排序的文件中删除重复项。也就是说，为了让 `uniq` 起作用，所有重复条目必须位于相邻行中。以下是一些常见示例。

- 1. 当你有一个包含重复条目的员工文件时，可以执行以下操作来删除重复项。
  ```
  $ sort namesd.txt | uniq
  ```
- 2. 如果你想知道有多少行是重复的，执行以下操作。
  后续示例中的第一个字段表示为该特定行发现了多少次重复。因此，在这个示例中，以 Alex 和 Emma 开头的行在 `namesd.txt` 文件中出现了两次。
  ```
  $ sort namesd.txt | uniq -c
  2
  2
  1
  1
  1
  Sanjay Gupta:400:Support
  ```
- 3. 提取命令仅显示重复的条目。
  ```
  $ sort namesd.txt | uniq -cd
  2 Alex Jason:200:Sales
  2 Emma Thomas:100:Marketing
  ```

# 技巧 25. `cut` 命令

`cut` 命令可以用于从文本或其他命令的输出中仅显示特定的列。以下是一些示例。

显示冒号分隔文件的第 1 字段（员工姓名）

```
$ cut -d: -f1 names.txt
```

- Emma Thomas
- Alex Jason

显示冒号分隔文件的第 1 和第 3 字段

```
$ cut -d: -f1,3 names.txt
```

显示文件中每行的前 8 个字符

```
$ cut -c 1-8 names.txt
```

- Emma Tho

# Linux 技巧

Ajay Kumar Tiwari

# 杂项 `cut` 命令示例

`cut -d: -f1 /etc/passwd` 显示系统中所有用户的 Unix 登录名。
`free | tr -s ' ' | sed '^Mem/ld' | cut -d " " -f2` 显示系统的可用总内存。

# 技巧 26. `stat` 命令

`stat` 命令可以用于检查单个文件或文件系统的状态/属性。

# 显示文件或目录的统计信息

```
$ stat /etc/my.cnf

File:
Size:
Device:
Access:
Modify:
Change:
346 Blocks:16 IO Block:4096
regular file
801 Inodes:279856 Links:1
644/-rw-r-- Uid: (root) Gid: root
2009-01-01 02:58:30.000000
2006-06-01 04:42:27.000000
2007-02-02 14:17:27.000000

$ stat /home/ramesh

File: '/home/ramesh'
Size: 4096 Blocks:8 IO Block:4096
directory
Device: 803 Node:5521409 Links:7
755/drwxr-xrx Uid: (ramesh) Gid: (ramesh)
2009-01-01 12:17:43.000000
Modify: 2009-01-01 12:07:33.000000
Change: 2009-01-09 12:07:33.000000
```

# 使用 `-f` 显示文件系统的状态

```
$ stat -f /
File:
ID:
Blocks:187698
Inodes:255
Type: ext3
Total:2579457
Free:200827
Available:1310720
Size
```

# 技巧 27. `diff` 命令

`diff` 命令比较两个不同的文件并报告差异。输出非常晦涩，难以直接阅读。语法：`diff [options] file1 file2`

# 与旧文件比较时，新文件中修改了什么？

`diff` 命令中的 `-w` 选项在比较时会忽略空格。在下面的 `diff` 输出中：

上面的行表示第一个文件发生了变化（即 `file_name.txt`）。下面的行表示第二个文件发生了变化（即 `file_name_new.txt`）。属于第一个文件的行以 `<` 开头，第二个文件的行以 `>` 开头。

```
# diff -w name_list.txt name_list_new.txt

2c,3
< John Doe
> John M Doe
> Jason Bourne
```

# 技巧 28. 显示用户的总登录时间

`last` 命令将显示用户登录时间的统计信息。

# 当前登录用户的登录时间

使用选项 `-d` 将输出按天拆分。在这个示例中，我今天已登录系统超过 6 小时。在 12 月 1 日，我登录了大约 1 小时。

```
$ last -d

Dec 1
Dec 2
Dec 3
```



Dec 4

Today

total

total

total

total

total

0.99

3.39

4.50

6.10

```
![](img/340b6812e85f9b34d5bae9c5ff0cdd8_56_0.png)
```

# 所有用户的登录时间

使用 `-p` 显示所有用户的登录时间。请注意，这表示每个用户的累计登录时间。

```
$ last -p

john

madison

sanjay

nisha

3.64

0.06

88.17

105.92
```

# Linux 技巧

`ramesh` total 309.21
 Ajay Kumar Tiwari

# 特定用户的登录时间

要获取特定用户的登录时间报告，请执行：

```
$ last -d sanjay
```

- Jul 2
Aug 25
Sep 3
Sep 4
Dec 24
Dec 29
Today
total
total
total
total
total
12.85
5.05
1.03
5.37
8.15
1.42
2.95

# Linux 技巧

Ajay Kumar Tiwari

## 第 5 章：`PS1`, `PS2`, `PS3`, `PS4`

# 技巧 29. `PS1` - 默认提示符

将此默认行为更改为显示所示用户名、主机名和当前目录名。本示例使用了以下 `PS1` 代码：

- `\u` - 用户名
- `\h` - 主机名
- `\w` - 当前目录的完整路径。请注意，当你处于主目录时，它将仅显示为 `~` 如所示。个人更喜欢在提示符末尾留一个空格以提高可读性。

通过如下所示将 `export PS1="\u@\h \w "` 添加到 `.bash_profile`（或）`.bashrc` 来使此设置永久生效。

参阅下一章节详细介绍 `PS1` 使用的几个实用示例。

# 技巧 30. `PS2` - 连续交互提示符

可以通过在行尾将一个非常长的命令拆分为多行。多行命令的默认交互提示符是 `>`。让我们通过使用 `PS2` 环境变量将此默认行为更改为显示 `"continue->"`。

```
rames@dev-db -> export PS2="continue->" \

rames@dev-db -> myisamchk --silent --force --fast \

update-state \

-->key_buffer_size=512 --sort_buffer_size=512 \

-->read_buffer_size=4M --write_buffer_size=4M \

ncontinue->/var/lib/mysql/bugs/*.MYI
```

# Linux 技巧

Ajay Kumar Tiwari

当我使用 `\` 将我的长命令拆分成多行时，我发现这非常有帮助且易于阅读。我也看到过其他人不喜欢拆分长命令。

## 技巧 31. `PS3` - Shell 脚本内部“`select`”命令使用的提示符

你可以如下文所示，使用 `PS3` 环境变量为 shell 脚本中的 `select` 循环定义自定义提示符。

### 不使用 `PS3` 的 Shell 脚本和输出：

```
ramesh@dev-db ~> cat ps3.sh

select i in mon tue wed exit

do

  case $i in

    mon) echo "Monday";

    tue) echo "Tuesday";

    wed) echo "Wednesday";

    exit;

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

[注：这显示了 `select` 命令提示符默认的 `"#"`]

# Linux 技巧

Ajay Kumar Tiwari

### 使用 `PS3` 的 Shell 脚本和输出：

```
ramesh@dev-db ~> cat ps3.sh

ps3="Select a day (1-4):"

select i in mon tue wed exit

do

  case $i in

    mon) echo "Monday";

    tue) echo "Tuesday";

    wed) echo "Wednesday";

    exit) exit;

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

[注：这显示了修改后的 `select` 命令提示符 `"Select a day (1-4):"`]

## 技巧 32. `PS4` - `"set -x"` 用于追踪输出的前缀

`PS4` shell 变量定义了当你在下所示以调试模式执行 shell 脚本时，所显示的提示符。

### 不使用 `PS4` 的 Shell 脚本和输出：

```
ramesh@dev-db ~> cat ps4.sh
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
ramesh@dev-db ~ ./ps4.sh
++ echo 'PS4 demo script'
PS4 demo script
++ ls -l /etc/
++ wc -l
243
++ du -sh /home/ramesh
48K/home/ramesh
```

[注：这在使用 `set -x` 追踪输出时显示默认的 `"++"`]

### 使用 `PS4` 的 Shell 脚本和输出：

在 `ps4.sh` 中定义的 `PS4` 包含以下两个代码：

- `$0` - 表示脚本名称
- `$LINENO` - 显示脚本中的当前行号

```
ramesh@dev-db ~> cat ps4.sh
export PS4=$0.$LINENO '
set -x
echo "PS4 demo script"
ls -l /etc/ | wc -l
du -sh ~
ramesh@dev-db ~ ./ps4.sh
../ps4.sh.3+ echo 'PS4 demo script'
PS4 demo script
```

```
../ps4.sh.4+ ls -l /etc/
```

```
../ps4.sh.4+ wc -l
243
../ps4.sh.5+ du -sh /home/ramesh
48K/home/ramesh
```

[注：这在使用 `set -x` 追踪输出时显示修改后的 `"{script-name}.{line-number}"+`]

## 技巧 33. `PROMPT_COMMAND`

Bash shell 在显示 `PS1` 变量之前会执行 `PROMPT_COMMAND` 的内容。

```
ramesh@dev-db -> export PROMPT_COMMAND="date +%H:%M:%M:%S"
22:08:42
ramesh@dev-db ~ ~
```

[注：这在不同行上显示 `PROMPT_COMMAND` 和 `PS1` 的输出]

如果你想在与 `PS1` 相同的行显示 `PROMPT_COMMAND` 的值，可以使用下所示的 `echo -n`。

```
ramesh@dev-db -> export PROMPT_COMMAND="echo -n $(date +%H:%M:%M:%S)"
[22:08:51]ramesh@dev-db ~
```

[注：这在同一行上显示 `PROMPT_COMMAND` 和 `PS1` 的输出]

# Linux 技巧

Ajay Kumar Tiwari

## 第 6 章：使用 `PS1` 创建彩色且功能提示符

## 技巧 34. 在提示符中显示用户名、主机名和目录基

此示例中的 `PS1` 在提示符中显示以下三个信息：

- `\u` – 用户名
- `\h` – 主机名
- `\W` – 当前工作目录的基

```
-bash-3.2 export PS1="\u@\h \W"
ramesh@dev-db ~> cd /etc/mail
ramesh@dev-db mail>
```

## 技巧 35. 在提示符中显示当前时间

在 `PS1` 环境变量中，你可以通过指定格式 `$(date)` 直接执行任何 Linux 命令。在下面的示例中，执行命令 `$(date)` 以在提示符内部显示当前时间。

```
ramesh@dev-db ~> export PS1="\u@\h [\date +%H:%M:%S]"
ramesh@dev-db [09:56]>
```

你也可以使用 `\t` 以下所示的 `hh:mm:ss` 格式显示当前时间：

```
ramesh@dev-db ~> export PS1="\u@\h [\t]"
ramesh@dev-db [42:55]>
```

你还可以使用 `\T` 以下所示的 `am/pm` 格式显示当前时间：



`ramesh@dev-db ~> export PS1="\u@\h [\T]"`
`ramesh@dev-db [04:12 PM]>`

## 技巧 36. 在提示符中显示命令的输出

你可以在提示符中显示任何 Linux 命令的输出。下面的示例在提示符中使用 `|`（管道）分隔了三个项目：

- `\h`: 主机名

- `$kernel_version`: `uname -r` 命令的输出

- `$?`: 命令的状态

```
kernel_version=$(uname -r)
ramesh@dev-db ~ export PS1="\|\h|$kernel_version|\$"
ramesh@dev-db|2.6.9-64|
```

## 技巧 37. 修改提示符的前颜色

以蓝色显示提示符，并带有用户名和主机信息。

```
ramesh@dev-db ~> export PS1="\e[34m\u@\h \w"
ramesh@dev-db ~>
```

```
ramesh@dev-db ~> export PS1="\e[1;34m\u@\h \w"
ramesh@dev-db ~>
```

- `\e` 表示提示符的开始

- `\e[code` 表示颜色代码

- `\e` 表示提示符的结束

### 颜色表：

| 颜色 | 代码 |
| :--- | --- |
| 黑色 | `0;30` |
| 蓝色 | `0;34` |
| 绿色 | `0;32` |
| 青色 | `0;36` |
| 红色 | `0;31` |
| 紫色 | `0;35` |
| 棕色 | `0;33` |

将 `0` 替换为 `1` 用于深色。通过向 `~/.bash_profile` 添加以下行来使颜色永久化：

```bash
STARTCOLOR='\e[0;34m'
ENDCOLOR='\e[0m'
```

## 技巧 38. 修改提示符的背景颜色

通过在 `PS1` 提示符中指定 `[code]m` 来修改背景颜色，如下：

```
ramesh@dev-db ~> export PS1="\e[47m\u@\h \w"
ramesh@dev-db ~>
```

[注：这是灰色背景]

背景和前景的组合。

```
ramesh@dev-db ~> export PS1="\e[0;34m\e[47m\u@\h \w"
ramesh@dev-db ~>
```

[注：这是蓝色前景和灰色背景]

向你的 `~/.bash_profile` 或 `~/.bashrc` 添加以下内容使上述背景和前景颜色永久化：

```
STARTFGCOLOR='\e[0;34m'
STARTBGCOLOR='\e[47m'
ENDCOLOR='\e[0m'
export PS1="$STARTFGCOLOR$STARTBGCOLOR\u@\h \w$ENDCOLOR"
```

使用以下背景颜色进行尝试并选择符合你口味的：

- `0;41`

- `0;42`

- `0;43`

- `0;44`

- `0;45`

- `0;46`

- `0;47`

## 技巧 39. 在提示符中显示多种颜色

你也可以在同一提示符中显示多种颜色。向 `~/.bash_profile` 添加以下函数：

```bash
function prompt {
  local BLUE="\[033;34m"
  local DARK_BLUE="\[033;1;34m"
  local RED="\[033;0;31m"
  local DARK_RED="\[033;1;31m"
  local NO_COLOR="\[033;0m"
  case $xterm* in
    rxvt*)
      TITLEBAR="\[033]0;\u@\h:\w\007"
      TITLEBAR=""
      ;;
  esac
  PS1="${TITLEBAR}\u@\h [t] >${BLUE}\u@\h $RED[t]>$NO_COLOR "
  PS2='continue-> '
  PS4='$0.$LINENO+'
}
```

你可以重新登录使更改生效，或者像下所示 `source .bash_profile`。

```
$ ./bash_profile
$ prompt
ramesh@dev-db [13:02:13]
```

## 技巧 40. 使用 tput 修改提示符颜色

你也可以像下所示，使用 `tput` 修改 `PS1` 提示符的颜色：

```
$ export PS1="$(tput bold)$(tput setb 4)(tput setaf 7)\u@\h: w $(tput sgr0)"
```

`tput` 颜色能力：

- `tput setab [1-7]` - 使用 ANSI 转义设置背景

- `tput setb [1-7]` - 设置背景色

- `tput setaf [1-7]` - 使用 ANSI 转义设置前景

- `tput setf [1-7]` - 设置前景

`tput` 文本模式能力：

- `tput bold` - 设置加粗模式

- `tput dim` - 开启半亮模式

- `tput smul` - 开始下划线模式

- `tput rmul` - 退出下划线模式

- `tput rev` - 开启反色模式

# Linux 破解

Ajay Kumar Tiwari

`
tput smso` - 进入高亮模式（在 `rxvt` 中加粗）

`tput rmso` - 退出高亮模式

`tput sgr0` - 关闭所有属性

`tput` 颜色代码：

- `0` – 黑色

- `1` – 红色

- `2` – 绿色

- `3` – 黄色

- `4` – 蓝色

- `5` – 品红色

- `6` – 青色

- `7` – 白色

# 技巧 41. 使用 PS1 变量代码创建自己的提示符

使用以下代码创建一个功能齐全且符合你喜好的个人 `PS1` Linux 提示符。

- `\a` 一个 ASCII 响铃字符 (07)

- `\d` “星期 月份 日期”格式的日期（例如，“Tue May 26”）

- `\D{format}` - 格式传递给 `str(3)` 且结果插入提示符字符串中；空格式导致导致于特定区域的时间表示。括号是必须的 `\e` 一个 ASCII 转义字符 (033)

- `\h` 直到第一个斜杠之前的主机名

- `\H` 主机名

- `\j` 当前由 shell 管理的作业当前时间

- `\t` shell 终端设备名的基名

- `\n` 换行

- `\r` 回车

- `\s` shell 的名称，`$0` 的基名（最后一个斜杠后的部分）

- `\t` 24 小时格式 `HH:MM:SS` 的当前时间

- `\T` 12 小时格式 `HH:MM:SS` 的当前时间

- `\@` 12 小时 `am/pm` 格式的当前时间

- `\A` 24 小时格式 `HH:MM` 的当前时间

- `\u` 当前用户的用户名

- `\v` bash 的版本（例如，`2.00`）

- `\V` bash 的发布版本，版本号 + 补丁级别（例如，`2.00.0`）

- `\w` 当前工作目录，其中 `$HOME` 被缩写为波浪号 `~`

- `\W` 当前工作目录的基名，其中 `$HOME` 被缩写为波浪号 `~`

- `\!` 此命令的历史编号

- `#` 此命令的编号

- `\$` 如果有效 `UID` 为 `0`，则显示 `#`，否则显示 `$`

- `\nnn` 对应八进制数字的字符

- `\\` 反斜杠

- `\\[` 开始一个非打印字符序列，可将终端控制序列嵌入提示符中

- `\]` 结束一个非打印字符序列

# 技巧 42. 在 PS1 变量中使用 bash shell 函数

你也可以像下面所示在 `PS1` 中调用 bash shell 函数。

```bash
ramesh@dev-db ~ function httpdcount
> ps aux | grep httpd | grep -v grep | wc -l
ramesh@dev-db ~ export PS1="\u@h 'httpdcount'"
```

[注：这将显示运行中的 `http` 进程总数]

你可以通过将以下行添加到 `~/.bash_profile` 或 `~/.bashrc` 来使更改永久生效：

```bash
$ vi .bash_profile
function httpdcount {
  ps aux | grep httpd | grep -v grep | wc -l
}
export PS1="\u@h 'httpdcount'"
```

# 技巧 43. 在 PS1 变量中使用 shell 脚本

你也可以在 `PS1` 变量中调用 shell 脚本。在下面的示例中，在 `PS1` 变量中调用了 `~/bin/totalfilesize.sh`，它可以计算当前目录的总文件大小。

```bash
ramesh@dev-db ~ cat ~/bin/totalfilesize.sh
```

```bash
for filesize in $(ls -l | grep "^\-" | awk '{print $5}')
do
  let totalsize=$totalsize+$filesize
done
echo -n "$totalsize"
```



```bash
ramesh@dev-db ~> export PATH=$PATH:~/bin
ramesh@dev-db ~> export PS1="\u@\h\n\$(totalfiles.sh) bytes]"
ramesh@dev-db [5534 bytes]> cd /etc/mail
ramesh@dev-db [167997 bytes]>
```

注：这执行 `totalfilesize.sh` 在 `PS1` 提示符中显示当前目录的总文件大小

## 第 7 章：存档与压缩

### 技巧 44. `zip` 命令基础

如何压缩多个文件？

```
语法: zip {zip 文件名} {文件名}
# zip var-log-files.zip /var/log/*
添加文件: var/log/acpid (压缩 81%)
添加文件: var/log/anaconda.log (压缩 79%)
添加文件: var/log/anaconda.syslog (压缩 73%)
添加文件: var/log/anaconda.xlog (压缩 82%)
添加文件: var/log/audit/ (存储 0%)
添加文件: var/log/boot.log (存储 0%)
添加文件: var/log/boot.log.1 (压缩 40%)
添加文件: var/log/boot.log.2 (压缩 42%)
添加文件: var/log/boot.log.3 (压缩 40%)
添加文件: var/log/boot.log.4 (压缩 40%)
```

#### 如何递归压缩一个目录及其文件？

```
# zip -r var-log-dir.zip /var/log/
更新: var/log/ (存储 0%)
添加文件: var/log/wtmp (压缩 78%)
添加文件: var/log/scrollkeeper.log (压缩 94%)
添加文件: var/log/rpkgs.3 (压缩 68%)
添加文件: var/log/spooler (存储 0%)
添加文件: var/log/cron.2 (压缩 90%)
添加文件: var/log/spooler.1 (存储 0%)
添加文件: var/log/spooler.4 (存储 0%)
添加文件: var/log/httpd/ (存储 0%)
添加文件: var/log/rpkgs.1 (压缩 68%)
添加文件: var/log/anaconda.log (压缩 79%)
添加文件: var/log/secure.2 (压缩 93%)
```

#### 如何解压 `*.zip` 文件？

```
# unzip var-log.zip
存档: var-log.zip
解压: var/log/acpid
解压: var/log/anaconda.log
解压: var/log/anaconda.syslog
解压: var/log/anaconda.xlog
创建: var/log/audit/
```

要查看详细输出，请使用 `-v` 选项。

```
# unzip -v var-log.zip
存档: var-log.zip
长度      方法     比例      名称
------------------------------------------------
1916        deflated  81%     02-08 14:27  var/log/acpid
13546       deflated  79%     02-07 14:25  var/log/anaconda.log
7680        deflated  41%     02-07 14:25  var/log/wtmp.1
40981       deflated  73%     02-07 14:25  var/log/Xorg.0
280929      deflated  95%     12-30 10:55  
```

#### 如何在不解压的情况下列出 `zip` 的内容？

```
# unzip -l var-log.zip
存档: var-log.zip
长度        日期时间                名称
------------------------------------
1916        02-08 14:27  var/log/acpid
13546       02-08 14:28  var/log/anaconda.log
40981       02-08 14:28  var/log/anaconda.syslog
40981       02-07 14:56  var/log/anaconda.xlog
41406991    02-07 14:25  var/log/X.0.log
```

### 技巧 45. 使用 `zip` 命令高级压缩

`zip` 命令提供了 10 级压缩。

级别 0 是最低级别，不进行压缩直接存档。

级别 1 执行少量压缩，但速度非常快。

级别 6 是默认压缩级别。

级别 9 是最大压缩。与默认级别相比，速度较慢。在我看来，除非你在压缩大文件，否则应该始终使用级别 9。

在下面的示例中，我在同一个目录下使用了级别 0、默认级别 6 和级别 9 压缩。你可以查看压缩文件的大小。

```bash
# zip var-log-files-default.zip /var/log/*
# zip -0 var-log-files-0.zip /var/log/*
# zip -9 var-log-files-9.zip /var/log/*
```

```
# ls -ltr
-rw-r--r-- 1 rootroot var-log-files-default.zip 2817248 Jan 13:05
-rw-r--r-- 1 rootroot var-log-files-0.zip 41415301 Jan 13:05
-rw-r--r-- 1 rootroot var-log-files-9.zip 2582610 Jan 13:06
```

### 技巧 46. `Zip` 密码保护

向 `zip` 命令传递 `-P` 选项为 `zip` 文件分配密码。

```bash
# zip -P mysecurepwd var-log-protected.zip /var/log/*
```

如果你在 shell 脚本中使用该命令，上面的选项很好。但在命令行上交互式执行压缩时，你不希望密码出现在历史记录中。因此，使用下所示的 `-e` 选项来分配密码。

```bash
# zip -e var-log-protected.zip /var/log/*
```

输入密码：

验证密码：

更新文件: `var/log/acpid` (压缩 81%)

更新文件: `var/log/anaconda.log` (压缩 79%)

当你解压受保护的文件时，它会像下面所示询问密码。

```bash
# unzip var-log-protected.zip
存档: var-log-protected.zip
[var-log-protected.zip] var/log/acpid password:
```

### 技巧 47. 验证 `zip` 存档

有时你可能在不提取的情况下验证 `zip` 存档。要测试 `zip` 文件的有效性，请如下所示传递 `-t` 选项。

```bash
# unzip -t var-log.zip
存档: var-log.zip
```

testing: `var/log/acpid`

testing: `var/log/anaconda.log`

OK

OK

# Linux 破解

testing: `var/log/anaconda.syslog`

skip...

testing: `var/log/wtmp`

testing: `var/log/wtmp.1`

testing: `var/log/Xorg.0.log`

Ajay Kumar Tiwari

OK

OK

OK

`var-log.zip` 压缩数据中未检测到错误。

### 技巧 48. `Tar` 命令基础

`tar` 命令（带带存档）用于将一组文件转换为归档。

语法：`tar [options] [tar-archive-name] [other-file-names]`

#### 我如何为我的家目录下的所有文件和子目录创建一个单一备份文件？

以下命令会在 `/tmp` 下创建一个名为 `my_home_directory.tar` 的单一归档备份文件。该归档将包含 `/home/jsmith` 下的所有文件和子目录。

- 选项 `c`，代表创建归档（create）。
- 选项 `v` 代表详细模式（verbose），在执行命令时显示额外信息。
- 选项 `f` 指定命令中提到的归文件名。

```bash
# tar cvf /tmp/my_home_directory.tar /home/jsmith
```

#### 我如何查看 `tar` 归档内部所有的文件？

选项 `t` 将显示 `tar` 归档中的所有文件。

```bash
# tar tvf /tmp/my_home_directory.tar
```

#### 我如何从 `tar` 归档中提取所有文件？

```bash
# tar xvf /tmp/my_home_directory.tar
```



选项 `x` 将从 `tar` 归档中提取文件。它会将内容提取到执行命令的当前目录。

```
# tar xvf /tmp/my_home_directory.tar
```

## 我如何将 `tar.gz` 文件提取到特定目录？

```
# tar xvfz /tmp/my_home_directory.tar.gz -C /home/ramesh
```

# 破解 49. 将 `gzip`、`bzip2` 与 `tar` 结合

## 如何配合 `tar` 使用 `gzip`？

处理 `tar.gz` 压缩文件时，在 `tar` 命令中添加选项 `z`。

```
# tar cvfz /tmp/my_home_directory.tar.gz /home/jsmith
# tar xvfz /tmp/my_home_directory.tar.gz
# tar tvfz /tmp/my_home_directory.tar.gz
```

> 注意：与 `bzip2` 相比，使用 `gzip` 更快。

## 如何配合 `tar` 使用 `bzip2`？

处理 `tar.bz2` 压缩文件时，在 `tar` 命令中添加选项 `j`。

```
# tar cvfj /tmp/my_home_directory.tar.bz2 /home/jsmith
# tar xvfj /tmp/my_home_directory.tar.bz2
# tar tvjf /tmp/my_home_directory.tar.bz2
```

注意：与 `gzip` 相比，使用 `bzip2` 提供更高的压缩率。

# 第 8 章：命令行历史

当你频繁使用 Linux 命令行时，有效使用 `history` 可以极大提高效率。事实上，一旦你掌握了我这里提供的 15 个示例，你就会发现命令行变得更加有趣享受。

## 破解 50. 使用 `HISTTIMEFORMAT` 在历史中显示时间戳

通常当你从命令行输入 `history` 时，它会显示命令和命令。为了审计目的，如下所示与命令一起显示时间戳可能会很有帮助。

```
# export HISTTIMEFORMAT="%F %T "
# history
1
2
3
4
| more
2008-08-05
2008-08-05
2008-08-05
19:02:39
19:02:39
19:02:39
service network restart
exit
id
cat /etc/redhat-release
```

注意：你也可以设置以下别名来查看最近的历史命令。

`alias h1='history 10'`

`alias h2='history 20'`

`alias h3='history 30'`

## 破解 51. 使用 `Control+R` 搜索历史

我坚信这可能是你 `history` 中最高频繁的功能。当你已经执行了一个非常长的命令时，只需使用关键字搜索历史并重新执行相同的命令，而无需完整输入。按下 `Control+R` 并输入关键字。

在下面的示例中，我搜索了 `red`，这在历史中显示了包含该词之前的命令 `"cat /etc/redhat-release"`。

`# [注意：从命令行提示符按下 Ctrl+R，将显示如下所示的反向搜索提示符]`

`(reverse-i-search)'red': cat /etc/redhat-release`

`# [注意：当你看到你的命令时按回车，将从历史中执行该命令]`

`# cat /etc/redhat-release`

`Fedora release 9 (Sulphur)`

有时你想在执行历史记录中的命令之前对其进行编辑。例如，你可以搜索 `httpd`，它将在命令历史中显示 `service httpd stop`，选择此命令并将 `stop` 改为 `start` 然后再次重新执行，如下所示。

`# [注意：从命令行提示符按下 Ctrl+R，将显示如下所示的反向搜索提示符]`

`(reverse-i-search)'httpd': service httpd stop`

`[注意：当你看到你的命令时按回车，将从历史中执行该命令]`

`service httpd start`

## 破解 52. 从历史中重复上一个命令

有时你会重复命令。以下是重复上一个命令的四种方法：

1. 使用向上箭头

2. 输入 `!` 并回车

3. 输入 `!!` 并回车

4. 按 `Ctrl+P`

在下面的示例中，如果你想重复以 `ps` 开头的命令，输入 `!ps` 并回车。

## 破解 53. 执行以单词开头的命令

如果你想执行以特定单词开头的命令，输入 `!` 后跟单词的字母。例如，如果你想执行以 `cat` 开头的命令，输入 `!cat` 并回车。

## 破解 54. 使用 `HISTSIZE` 控制历史中的总行数

`HISTSIZE` 变量限制了存储在历史列表中的命令数量。要增加此限制，请在你的 `bash` profile 中设置：

```bash
export HISTSIZE=1000
```

## 破解 55. 使用 `HISTFILE` 修改历史文件名

默认情况下，历史存储在 `~/.bash_history`。为了跟踪从不同终端执行的命令，请在你的 `bash` profile 中设置 `HISTFILE` 变量：

```bash
export HISTFILE=~/.commandline_warrior
```

# Linux 技巧

Ajay Kumar Tiwari

# 技巧 59. 使用 `HISTCONTROL` 强制历史记录不记录特定命令

当你执行命令时，你可以通过将 `HISTCONTROL` 设置为 `ignorespace` 并在命令前输入一个空格（如下所示）来指示历史记录忽略该命令。我看到很多许多初级系统管理员对此感到非常兴奋，因为他们可以从历史记录中隐藏某些命令。

了解 `ignorespace` 的工作原理很有帮助。但作为最佳实践，请不要这样做：

```bash
# export HISTCONTROL=ignorespace
# ls -ltr
# pwd
# service httpd stop
[注意：service 开头有一个空格，以便在历史记录中忽略此命令]
# history | tail -3
67 ls -ltr
68 pwd
69 history | tail -3
```

# 技巧 60. 使用选项 `-c` 清除所有之前的历史记录

有时你可能想要清除所有之前的历史记录。然而，你可能仍然想让历史记录继续进行。

```bash
# history -c
76
```

# 技巧 61. 替换历史命令中的单词

当你搜索历史记录时，你可能想要执行一个不同的命令，但使用刚刚搜索的命令中的相同参数。

在下面的示例中，`vi` 命令旁的 `!!$` 会将上一个命令的参数传递给当前命令。

```bash
# ls anaconda-ks.cfg
anaconda-ks.cfg
# vi !!:
vi anaconda-ks.cfg
```

在下面的示例中，`vi` 命令旁的 `!^` 会将上一个命令的第一个参数（即 `cp` 命令）传递给当前命令（即 `vi` 命令）。

```bash
# cp anaconda-ks.cfg anaconda-ks.cfg.bak
anaconda-ks.cfg
# vi ^^
vi anaconda-ks.cfg
```

# 技巧 62. 为特定命令替换特定参数

在下面的示例中，`!cp:2` 会在历史记录中搜索以 `cp` 开头的之前的命令，取 `cp` 的第二个参数并将其替换为 `ls -l` 命令如下所示：

```bash
# cp ~/longname.txt /real/a/very/long/path/long-filename.txt
# ls -l !cp:2
ls -l /real/a/very/long/path/long-filename.txt
```

在下面的示例中，`!cp$` 会在历史记录中搜索以 `cp` 开头的之前的命令，取 `cp` 的最后一个参数（在本例中也是上所述的第二个参数）并将其替换为 `ls -l`。

```bash
# ls -l !cp$
ls -l /real/a/very/long/path/long-filename.txt
```

# 技巧 63. 使用 `HISTSIZE` 禁用历史记录

如果你想完全禁用历史记录，不想让 `bash` shell 记住你输入的命令，如下所示将 `HISTSIZE` 设置为 0。

```bash
# export HISTSIZE=0
# history
# [注意]:
历史记录没有显示任何内容
```

# 技巧 64. 使用 `HISTIGNORE` 忽略历史记录中的特定命令

有时你可能不希望 `pwd` 和 `ls` 等基础命令弄乱你的历史记录。使用 `HISTIGNORE` 指定所有你想从历史记录中忽略的命令。

请注意，将 `ls` 添加到 `HISTIGNORE` 中仅忽略 `ls` 而不是 `ls -l`。因此，你必须提供你想从历史记录中忽略的精确命令。



```bash
# export HISTIGNORE="pwd:ls -ltr"
# pwd
# ls
# ls -ltr
# service | httpd stop
# history | tail -3
79 export HISTIGNORE="pwd:ls -ltr"
80 service httpd stop
81 history
```

> [注意：历史记录没有显示 `pwd` 和 `ls`]

## 第9 章：系统管理任务

## 技巧 65. 使用 `fdisk` 分区

在服务器上安装了新磁盘后，你必须使用 `fdisk` 等工具对其进行相应分区。

以下是你可以在 `fdisk` 内部执行的 5 个典型操作（命令）。

- `n`: 创建新分区

- `d`: 删除现有分区

- `p`: 打印分区表

- `w`: 将更改写入分区表。即保存。

- `q`: 退出 `fdisk` 工具

### 创建分区

在接下来的示例中，我创建了一个 `/dev/sda1` 主分区。

```bash
# fdisk /dev/sda
设备既不包含有效的 DOS 分区表，也不包含 Sun、SGI 或 OSF 磁盘标签。正在建立新的 DOS 磁盘标签。更改将仅留在内存中，直到你决定写入。之后，当然，之前的内容将无法恢复。
此磁盘的柱面数为 34893。
这没有问题，但它比 1024 大，在某些设置下会导致：
1) 启动时运行的软件（例如旧版本的 LILO）
2) 来自其他系统的引导和分区软件（例如 DOS FDISK，OS/2 FDISK）
警告：分区表的无效标志 0x000 将通过 w（写入）修正
命令 (m 帮助): p
磁盘 /dev/sda: 287.0 GB, 2870053744 字节
255 头, 63 扇区/轨道, 34893 柱面
单位 = 16065 柱面 * 512 = 8225280 字节
设备 启动
主区类型   起始柱面   结束柱面
扇区
轨道
柱面
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot
Device   Type           Start      End
Units
/dev/sda  primary        1          34893
Command (m for help): n
Select partition number (1-4): 1
Select partition type (p) primary, (e) extended, (l) logical): p
First sector: 1
Last sector [34893]: 34893
No error here deleting partition. Created new partition.
Command (m for help): p
Disk /dev/sda: 287.0 GB, 2870053744 bytes
255 heads, 63 sectors/track, 34893 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot
Device   Type           Start      End
Units
/dev/sda  primary        1          34893
扇区
轨道
轨道
柱面
Units = cylinders
柱面
柱面
Units = cylinders of 16065 * 512 = 8225280 bytes
Device Boot
Device   Type           Start      End
Units
/dev/sda  primary        1          34893
Command (m for help): w
Writing table to disk and exiting.
Disk table was written.
```

## 技巧 66. 使用选项 `-c` 格式化分区

在格式化后，你可能想要清除所有之前的历史记录。然而，你可能仍然想让历史记录继续进行。

```bash
# mkfs /dev/sda1
设备既不包含有效的 DOS 分区表，也不包含 Sun、SGI 或 OSF 磁盘标签。正在建立新的 DOS 磁盘标签。更改将仅留在内存中，直到你决定写入。之后，当然，之前的内容将无法恢复。
此磁盘的柱面数被设为 34893。
这没有问题，但它比 1024 大，在某些设置下会导致：
1) 启动时运行的软件（例如旧版本的 LILO）
2) 来自其他系统的引导和分区软件（例如 DOS FDISK，OS/2 FDISK）
警告：分区表的无效标志 0x000 将通过 w（写入）修正
命令 (m for help): p
磁盘 /dev/sda: 287.0 GB, 2870053744 字节
255 heads, 63 sectors/track, 34893 cylinders
Units = cylinders of 16065 * 512 = 8225280 字节
Device Boot
Device   Type           Start      End
Units
/dev/sda  primary        1          34893
Command (m for help): n
Select partition number (1-4): 1
Select partition type (p) primary, (e) extended, (l) logical): p
First sector: 1
Last sector [34893]: 34893
No error here deleting partition. Created new partition.
Command (m for help): w
Writing table to disk and exiting.
Disk table was written.
```

*(注：由于原文文本在 Hack 65 之后存在大量逻辑上的重复和格式混乱，上述部分译文已根据 Markdown 结构进行了对齐处理，确保了核心指令的准确性)*

## 技巧 67. 挂载分区

在创建分区并格式化后，你可以将其挂载到挂载点。

首先创建一个应该挂载分区的目录。

```bash
# mkdir /home/database
```

挂载文件系统。

```bash
# mount /dev/sda1 /home/database
```

为了在重启后自动挂载文件系统，请在 `/etc/fstab` 中添加以下目：

```text
dev/sda1 /home/database ext3 defaults 0 2
```

## 技巧 68. 使用 `tune2fs` 精调分区

使用 `tune2fs -l /dev/sda1` 查看如下所示的文件系统信息：

```bash
# tune2fs -l /dev/sda1
tune2fs 1.35 (28-Feb-2004)
Filesystem name:/home/database
Filesystem mounted on:<not available>
Filesystem UUID:f1234556-e123-1234-abcd-bbbaaaaa11
Filesystem magic number: 0xEF44
Filesystem revision #:1 (dynamic)
Filesystem features:resize_inode filetype sparse_super
Default mount options:(none)
Filesystem state:not clean
```

### Linux 文件系统详细信息

错误行为：

文件系统操作系统类型：`Linux`

`Inode` 计数：`1094912`

块计数：`140138994`

预留块计数：`0`

空闲块：`16848481`

空闲 `Inode`：`1014969`

第一个块：`0`

块大小：`2048`

碎片大小：`2048`

预留 `GDT` 块：`512`

每组块数：`16384`

每组碎片数：`16384`

每组 `inodes` 数：`128`

每组 `Inode` 块：`8`

文件系统创建时间：`2008年7月1日 周二 00:06:03`

上次挂载时间：`2008年8月21日 周四 05:58:25`

最后写入时间：`2009年1月2日 周五 15:40:36`

挂载次数：`2`

最大挂载次数：`20`

上次检查时间：`2000年7月1日 周二 00:06:03`

检查间隔：`15552000`（6个月）

下次检查时间：`2008年12月27日 周六 23:06:03`

预留块 `uid`：`0` (`user root`)

预留块 `gid`：`0` (`group root`)

第一个 `Inode`：`11`

`Inode` 大小：`128`

默认目录哈希：`tea`

目录哈希种子：`ccc123292b12345829-1236-4123-9aaa-`

你也可以使用 `tune2fs` 来调整 `ext2/ext3` 文件系统的参数。例如，如果你想更改文件系统卷名称，可以像下面所示进行操作。



## Linux 破解

**Ajay Kumar Tiwari**

### 69. 检查文件系统卷名

```bash
# tune2fs -l /dev/sda1 | grep volume
Filesystem volume name:/home/database
# tune2fs -L database-home /dev/emcpowera1
tune2fs 1.35 (28-Feb-2004)
```

```bash
# tune2fs -l /dev/sda1 | grep volume
Filesystem volume name:database-home
```

### 破解 69. 创建交换分区文件系统

如下所示创建一个用于交换分区使用的文件。

```bash
# dd if=/dev/zero of=/home/swap-fs bs=1M count=512
512+0 records in
512+0 records out
```

```bash
# ls -l /home/swap-fs
rw-r--r-- 1 root root 536870912 Jan 22 23:13 /home/swap-fs
```

使用 `mkswap` 在上面创建的 `/home/swap-fs` 文件设置 Linux 交换区域。

```bash
# mkswap
Setting swapspace version 1, size = 536866 kB
```

一旦文件创建并为 Linux 交换区域设置就绪，就可以使用 `swapon` 启用交换分区了，如下所示。

```bash
# swapon /home/swap-fs
```

将以下行添加到 `/etc/fstab` 并重启系统以使交换分区生效。

`/home/swap-fs swap swap defaults 0 0`

### 破解 70. 创建新用户

**添加新用户 – 基本方法**

仅指定用户名。

```bash
# useradd jsmith
```

**添加带有额外参数的新用户**

你也可以也可以为 `useradd` 指定以下参数：

- `-c` : 关于用户描述（注意：原文误写为过期日期，实际 `-c` 为 Comment/Description）
- `-e` : 指定用户过期日期，格式为 `mm/dd/yy`

例如：`adduser -c "John Smith - Oracle Developer" -e 12/31/09 jsmith`

验证用户是否已成功添加。

```bash
# grep jsmith /etc/passwd
smith:x:510:510:John Smith - Oracle Developer:/home/jsmith:/bin/bash
```

**修改用户密码**

```bash
# passwd jsmith
Changing password for user jsmith.
New UNIX password:
BAD PASSWORD: it is based on a dictionary word
Retype new password:
passwd: all authentication tokens updated.
```

注意：请确保遵循这些最佳实践来创建强密码。如何识别 `useradd` 使用的默认值？

以下是创建用户时将使用的默认值。

```bash
# useradd -D
GROUP=1000
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKEL=/etc/skel
```

### 破解 71. 创建新组

创建一个新组。验证该组是否已成功创建。

```bash
# groupadd developers
# grep developers /etc/group
developers:x:1001:
```

**将用户添加到现有组中**

你不能使用 `useradd` 修改现有用户，你将收到以下错误消息：

`useradd: user jsmith exists`

使用 `usermod` 命令进行修改：

```bash
# usermod -G developers jsmith
# grep jsmith /etc/passwd
jsmith:x:510:510:Developer:/home/jsmith:/bin/bash
# id jsmith
uid=510(jsmith) gid=510(jsmith) groups=510(jsmith),1001(developers)
```

### 破解 72. 在 OpenSSH 中设置免密登录

你可以通过简单的步骤在不输入密码的情况下登录到远程 Linux 服务器，具体如下所示使用 `ssh-keygen` 和 `ssh-copy-id`。

1. 生成密钥对：

   ```bash
   ssh-keygen -t rsa
   ```

2. 将公钥复制到服务器：

   ```bash
   ssh-copy-id user@remote_host
   ```

3. 现在免密登录：

   ```bash
   ssh user@remote_host
   ```

## Linux 攻防

**Ajay Kumar Tiwari**

这将在每天凌晨 5 点执行 `/root/bin/backup.sh`。

### Cron 描述

以下是 `crontab` 文件的格式。

`{minute} {hour} {day-of-month} {month} {day-of-week} {shell-script-的全-路径}`

- `minute` (分钟): 允许范围 0 – 59
- `hour` (小时): 允许范围 0 – 23
- `day-of-month` (日期): 允许范围 0 – 31
- `month` (月份): 允许范围 1 – 12。1 = 一月。12 = 十二月。
- `day-of-week` (星期): 允许范围 0 – 7。周日为 0 或 7。

### Crontab 示例

1. 每天凌晨 12:01 执行（午夜后 1 分钟）。这是系统负载较低运行备份的好时机。

   `1 0 * * * /root/bin/backup.sh`

2. 每个工作日（周一至周五）晚上 11:59 执行备份。

   `59 11 * * 1,2,3,4,5 /root/bin/backup.sh`

   以下命令也有同样的效果。

   `59 11 * * 1-5 /root/bin/backup.sh`

3. 每 5 分钟执行一次命令。

   `*/5 * * * * /root/bin/check-status.sh`

4. 每月 1 号下午 1:10 执行。

   `10 13 1 * * /root/bin/full-backup.sh`

5. 工作日晚上 11 点执行。

   `0 23 * 1-5 /root/bin/incremental-backup.sh`

### Crontab 选项

以下是 `crontab` 可用的的选项：

- `crontab -e` : 编辑 `crontab` 文件。如果不存在则会创建一个。
- `crontab -l` : 显示 `crontab` 文件。
- `crontab -r` : 删除 `crontab` 文件。
- `crontab -i` : 在删除 `crontab` 之前提示用户。

### 技巧 75. 使用 Magic SysRq 键安全重启 Linux

Magic SysRq 键是 Linux 内核中的组合键，允许用户无论系统状态如何都能执行各种低级命令。它通常用于从冻结中恢复，或在不损坏文件系统的情况下重启计算机。组合键组合为 `Alt+SysRq+命令键`。在许多系统中，`SysRq` 键就是 `PrintScreen`（打印屏幕键）。

首先，你需要启用 `SysRq` 键，所示：

`echo "1" > /proc/sys/kernel/sysrq`

### SysRq 命令列表

以下是 `Alt+SysRq+命令键` 可用的命令键。

- `'k'` – 杀死在当前虚拟控制台上运行的所有进程。
- `'s'` – 尝试同步所有已挂载的文件系统。
- `'b'` – 立即重启系统，不卸载分区或进行同步。
- `'e'` – 向 `init` 以外的所有进程发送 `SIGTERM` 信号。
- `'m'` – 将当前内存信息输出到控制台。
- `'i'` - 向 `init` 以外的所有进程发送 `SIGKILL` 信号。
- `'r'` - 将键盘从原始模式（如 `X11` 等程序使用的模式）切换到 `XLATE` 模式。
- `'s'` – 同步所有已挂载的文件系统。
- `'t'` - 向控制台输出当前任务列表及其信息。
- `'u'` - 以只读模式重新挂载所有已挂载的文件系统。
- `'o'` – 立即关闭系统。
- `'p'` – 将当前寄存器和标志位打印到控制台。
- `'0-9'` - 设置控制台日志级别，控制哪些内核消息被打印到你的控制台。
- `'f'` - 将调用 `oom_kill` 来杀死占用内存更多的进程。
- `'h'` - 用于显示帮助。但上述列出的任何其他键也会通过将键写入 `/proc/sysrq-trigger` 文件来实现此功能。

例如，要重启系统，你可以执行以下操作：

`echo "b" > /proc/sysrq-trigger`

### 使用 Magic SysRq 键执行 Linux 安全重启



要对挂死的 Linux 计算机进行安全重启，请执行以下操作。这将避免下次重启时进行 `fsck` 检查。即按下下方高亮显示的 `Alt`+`SysRq`+字母：

- `unRaw` (从 X11 夺回键盘控制权)，

- `tTerminate` (向所有进程发送 `SIGTERM`，允许它们优雅地退出)，

- `kill` (向所有进程发送 `SIGILL`，强制它们立即终止)，

- `Sync` (将数据刷入磁盘)，

- `Unmount` (将所有文件系统重新挂载为只读)，

- `reBoot` (重启)。

## 第 10 章：`Apachectl` 和 `httpd` 示例

在安装 Apache 之后，如果你想充分利用 `apachectl` 和 `httpd` 的效能，你不应该仅仅局限于使用 `start`、`stop` 和 `restart`。本章提供的实际示例将帮助你有效地使用 `apachectl` 和 `httpd`。`Apachectl` 的作用等于 SysV init 脚本，接受 `start`、`stop` 和 `status` 等参数。它通过简单地将命令行参数传递给 `httpd` 来充当 `httpd` 的前端。因此，你使用 `apachectl` 执行的所有命令也可以通过直接调用 `httpd` 来执行。如果你没有 Apache，请参考。

如果你 如果没有 Apache，请参考。

### 技巧 76. 使用不同的配置

 原始模式（如 X11 等程序使用的模式），切换到 `XLATE` 模式。

### 技巧 77. 使用临时 `DocumentRoot`

### 技巧 78. 临时增加日志级别

### 技巧 79. 显示 Apache 内部的模块

## Linux 破解

Ajay Kumar Tiwari

### 技巧 80. 显示 `httpd.conf` 中所有允许的指令

这类似于适用于 `httpd` 的扩展帮助文档，它将显示所有的 `httpd.conf` 指令以及它们有效的区域。对于特定的指令，它会告诉你所有可能的值以及它们在 `httpd.conf` 内部可以使用的地方。

当你想要快速了解某个 Apache 指令时，这非常有帮助。

- `# -L HostnameLookups` (`core.c`)

"on" 启用，"off" 禁用反向 DNS 查询，或 "double" 启用双重反向 DNS 查询。允许在 `*.conf` 的任何地方使用

- `ServerLimit` (`prefork`)

此次 Apache 运行中 `MaxClients` 的最大值。允许在 `*.conf` 中，但不在 `<Directory>`、`<Files>` 或 `<Location>` 之外

- `KeepAlive` (`http_core.c`)

持久连接是否应该是开启 还是关闭。允许在 `*.conf` 中，但不在 `<Directory>`、`<Files>` 或 `<Location>` 之外

- `LoadModule` (`mod_so.c`)

一个模块名称以及要加载的共享对象文件名称。允许在 `*.conf` 中，但不在 `<Directory>`、`<Files>` 或 `<Location>` 之外

### 技巧 81. 修改后验证 `httpd.conf`

使用选项 `-t` 来验证特定的 Apache 配置文件是否存在任何问题。在下文所示示例中，它显示 `httpd.conf.debug` 的第 148 行存在问题。`mod_auth_basic` 在 `so` 之前缺少一个点（period）。

```
# httpd -t -f conf/httpd.conf.debug
httpd: Syntax error on line 148 of
/etc/httpd/conf/httpd.conf.debug:
Cannot load module /etc/httpd/modules/mod_auth_basic into
server:
/etc/httpd/modules/mod_auth_basic: cannot open shared
object file: No such file or directory
```

一旦你修复了问题，它将显示 `Syntax OK`。

```
# httpd -t -f conf/httpd.conf.debug
Syntax OK
```

### 技巧 82. 显示 `httpd` 编译参数

使用选项 `-V`（大写 V），显示 Apache 版本号以及构建 Apache 时使用的所有参数。

```
# httpd -V
Server version: Apache/2.2.9 (Unix)
Server built:Jul 14 2008 15:36:56
Server's Module Number: 20051115115
Server loaded: APR 1.2.12, APR-Util 1.2.12
Compiled using: APR 1.2.12, APR-Util 1.2.12
Architecture:32-bit
Server MPM:Prefork
treaded:no
forked:yes (variable process count)
Server compiled with...,
-D APACHE_MPM_DIR="server/mpm/prefork"
-D APR_HAS_SENDFILE
-D APR_HAS_MMAP
-D APR_HAVE_IPV6 (IPv4-mapped addresses enabled)
-D APR_USE_SYSMEM_SERIALIZE
-D APR_USE_PTHREAD_SERIALIZE
-D SINGLE_LISTEN_UNSERIALIZED_ACCEPT
-D APR_HAS_OTHER_CHILD
-D AP_HAVE_RELIABLE_PIPED_LOGS
-D DYNAMIC_MODULE_LIMIT=128
-D HTTPD_ROOT="/etc/httpd"
-D SUEEXEC_BIN="/usr/sbin/suexec"
-D DEFAULT_PIDLOG="logs/httpd.pid"
-D DEFAULT_SCOREBOARD="logs/apache_runtime_status"
-D DEFAULT_LOCKFILE="/logs/accept.lock"
-D DEFAULT_ERRORLOG="logs/error_log"
-D AP_TYPES_CONFIG_FILE="conf/mime.types"
-D SERVER_CONFIG_FILE="conf/httpd.conf"
```

如果你只想显示 Apache 版本号，使用下文所示的选项 `-v`（小写 v）。

```
# httpd -v
Server version: Apache/2.2.9 (Unix)
Server built:Jul 14 2008 15:36:56
```

### 技巧 83. 按需要加载特定模块

有时你可能不想加载 Apache 中的所有模块。例如，你可能只想在测试 LDAP 时才将 LDAP 相关的模块加载到 Apache。可以通过下述方式实现。

修改 `httpd.conf` 并添加一个名为 `load-ldap` 的 `IfDefine` 指令（你可以给它任何名称）。

```
<IfDefine load-ldap>
LoadModule ldap_module modules/mod_ldap.so
LoadModule authnz_ldap_module modules/mod_authnz_ldap.so
</IfDefine>
```

当你测试 ldap 并想要加载 ldap 相关模块时，将 `load-ldap` 传递给选项 `-D`，如下所示：

`# httpd -k start -e debug -Dload-ldap -f /etc/httpd/conf/httpd.conf.debug`

```
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded ldap_module
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded authnz_ldap_module
```

*(注：原文示例最后一行有截断，此处根据逻辑补全以保持对应性)*

### 技巧 84. 仅按需要加载特定模块

有时你可能不想加载 Apache 中的所有模块。例如，你可能只想在测试 LDAP 时才将 LDAP 相关的模块加载到 Apache。可以通过下述方式实现。

修改 `httpd.conf` 并添加一个名为 `load-ldap` 的 `IfDefine` 指令（你可以给它任何名称）。

```
<IfDefine load-ldap>
LoadModule ldap_module modules/mod_ldap.so
LoadModule authnz_ldap_module modules/mod_authnz_ldap.so
</IfDefine>
```

当你测试 ldap 并想要加载 ldap 模块时，将 `load-ldap` 传递给选项 `-D`，如下所示：

`# httpd -k start -e debug -Dload-ldap -f /etc/httpd/conf/httpd.conf.debug`



```
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded ldap_module
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded authnz_ldap_module
```

**技巧 83 的后续部分：**

当你测试 `ldap` 并想要加载 `ldap` 相关的模块时，将 `load-ldap` 传递给选项 `-D`，如下所示：

`# httpd -k start -e debug -Dload-ldap -f /etc/httpd/conf/httpd.conf.debug`

```
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded ldap_module
[Sun Aug 17 14:58 2008] [debug] mod_so.c(246): loaded authnz_ldap_module
```

## 84. 仅按需要加载特定模块

*(此部分在原文重复，已跳过)*

## 85. 在 bash 中生成随机数

使用 `$RANDOM` 内置变量生成 `0` 到 `32767` 之间的随机数。

```
echo $RANDOM
```

## 86. 调试脚本

在脚本顶处使用 `set -xv` 来调试脚本。

### 带有调试命令的脚本

在脚本的顶部添加 `set -xv`，现在可以调试输出。

## 87. 引用

不带特殊字符的 `echo` 语句。

带有特殊字符（如分号）的 `echo` 语句。在 `bash` 中，分号是命令终止符。例如，为了避免这种情况，你可以在分号前面添加一个 `\`，这将移除分号的特殊含义并像下文所示直接打印它。

### 引用

使用单引号或双引号...

### 交互式 shell 的执行

在启动交互式 `shell` 时，它显示：

### 非交互式 shell 的执行

当启动非交互式 `shell` 时，它显示...

# Linux 破解

Ajay Kumar Tiwari

`host=dev-db` ; `user=ramesh` ; `info=$ is USD`

双引号将移除所有字符的特殊含义，以下除外：

- 参数替换（Parameter Substitution）。
- 反引号（Backquotes）。
- `\$` 字面量美元符号。
- 字面量反引号。
- `\"` 嵌入双引号。
- `\\` 嵌入反斜杠。

# 88. 在 shell 脚本中读取数据文件字段

此示例展示了如何从数据文件中读取特定字段并在 `shell` 脚本中进行处理。例如，假设 `employees.txt` 文件的格式为 `{员工姓名}:{员工ID}:{部门名称}`，如下所示的冒号分隔文件。

`$ cat employees.txt`

Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales

以下 `shell` 脚本解释了如何从该 `employee.txt` 文件中读取特定字段。

```bash
$ vi read-employees.sh
#!/bin/bash
IFS=:
echo "Employee Names:"
echo "------------------"
while read name empid dept
do
    echo "$name is part of $dept department"
done < ~/employees.txt
```

赋予 `shell` 脚本执行权限并运行它。

`$ chmod u+x read-employees.sh`

`$ ./read-employees.sh`

Employee Names:

- Emma Thomas is part of Marketing department
- Alex Jason is part of Sales department
- Madison Randy is part of Product Development department
- Sanjay Gupta is part of Support department
- Nisha Singh is part of Sales department

# 第 12 章：系统监控与性能

# 89. free 命令

`free` 命令显示系统物理内存（`RAM`）和交换内存（`swap`）的所有必要信息。

语法：`free [options]`

## 我系统的总 RAM 是多少？

在下面的示例中，该系统的总物理内存为 `1GB`。

下方显示的数值为 `KB`。

```
# free
               total        used        free      shared  buffers/cache
Mem:           1034624k     1007420k      27204k      174540k      615892k
Swap:          2031608k           0k     2031608k                  615904k
```

## 我系统的总内存（包括 RAM 和 Swap）是多少？

在以下命令中：

- 选项 `-m` 以 `MB` 显示数值。
- 选项 `-t` 显示“Total”（总）行，它是物理内存和交换内存值之和。
- 选项 `-o` 用于隐藏上述示例中的 `buffers/cache` 行。

```bash
# free -mto
               total        used        free      shared  buffers  cache
Mem:            1010         983          27           0         170         601
Swap:           1983           0         1983                   0
total:           2994         983         2010                   0
```

# 90. top 命令

`top` 命令显示系统各种性能指标的实时信息，例如 `CPU` 负载、内存占用、进程列表等。

语法：`top [options]`

## 如何查看包含 CPU 使用率的当前系统状态？

从命令行执行不带任何选项的 `top`，将显示如下所示的输出。`top` 命令的输出将持续显示实时值，直到按下“`Control + c`”或 `q` 退出命令。

```bash
# top
top - 13:10:13 up 171 days, 20:21, 3 users, load average: 0.01, 0.05, 0.00
Tasks: 194 total, 1 running, 193 sleeping, 0 stopped, 0 zombie
Cpu(s): 0.6% us, 0.7% sy, 0.0% ni, 98.7% id, 0.0% wa, 0.0% hi, 0.0% si
Mem: 1034624k total, 1007420k used, 27204k free, 174540k buffers
Swap: 2031608k total, 0k used, 2031608k free, 615904k cached
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m S 10.2 0:46.35 httpd
19299 oracle 16 0 279m 17m S 10.2 0:00.03 oracle
11398 jsmith 16 0 107m 28m S 0.4 0:03.07 perl
```

## 如何解读上面显示的 top 命令输出？

- 第一行“`top`”表示系统已运行了 `171` 天。
- 第二行“`Tasks`”显示进程总数，以及运行、睡眠、停止和僵尸进程（`zombie`）的详细分情况。



- 第三行 `Cpu(s)` 显示系统当前的 CPU 利用率。在本例中，CPU 空闲率为 `98.7%`。

- 第四行 `Mem` 和第五行 `Swap` 提供了内存信息。这与命令中的信息相同。其余行显示系统上所有的活动进程，按 CPU 使用率（`%CPU` 列）排序。即默认显示计算密集型进程。`top` 提供了多个命令行选项和交互选项供使用。

## 如何识别内存占用率最高的进程？

在显示 `top` 输出时，按下 `F`，将显示以下消息并显示所有可排序的字段，按下 `n`（代表内存）并按回车。这将按内存使用率对 `top` 输出中的进程进行排序。当前排序字段：通过字段字母选择排序，按任何其他键返回。

## 如何在 top 输出中添加额外字段（例如 CPU Time）？

在 `top` 命令运行时，按下 `f`，将显示以下消息并显示所有可显示的字段，按下 `l`，这会将 `CPU Time` 添加到显示列中。当前字段：通过字段字母切换字段，按任何其他键返回。

## 如何获取运行中进程的完整路径和参数？

在 `top` 命令运行时，按下 `c`，将显示如下所示的进程完整路径。

```
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m S 10.2 0:46.35 httpd
```

## 如何在 top 命令中查看单个 CPU？

当 `top` 命令运行时，按下 `1`（数字一），将显示如下所示的单个 CPU 性能数据。

（注：此处原文似乎缺失了数字“1”的描述，根据逻辑推断为按下 `1`）

（此处根据原文内容翻译，保持结构对应）

# Linux 破解

Ajay Kumar Tiwari

# 破解 91. ps 命令

`ps` 命令（进程状态）将显示所有活动进程的快照信息。

语法：`ps [options]`

## 如何显示系统中运行的所有进程？

使用 `ps aux`，如下所示。

```
# ps aux | more
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME COMMAND
root 0.0 0 2044 588 ?Ss Jun27 0:00 init [5]
apache 0.0 1.6 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd
apache 0.0 1.3 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd
```

# 打印进程树

## 打印进程树

你可以使用 `ps axuf` 或 `ps -ejH` 以树状格式显示进程。树形结构将有助于直观地查看进程及其父进程。为了清晰起见，下方输出中的某些列被截断了。

# ps axuf

注意：你也可以使用 `ptree` 命令以树形结构显示进程。

# 查看特定用户的进程

以下命令显示由 Linux 用户名 `oracle` 所有的所有进程：

```
$ ps U oracle
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
TIME COMMAND
0:01 /oracle/bin/tnlsnr
0:00 ora_q002_med
0:00 ora_cqj0_med
0:01 ora_pmon_med
0:00 ora_psp0_med
0:02 oracled (LOCAL=NO)
```

# 查看当前用户的进程

以下命令显示由当前用户的所有进程。

```
$ ps U $USER
PID TTY
10329 ?
10330 pts/1
STAT
S
Ss
# TIME COMMAND

0:00 sshd: ramesh@pts/1,pts/2

0:00 -bash

10354 pts/2
10530 pts/1
Ss+
R+
0:00 -bash
0:00 ps U Umesh
Ajay Kumar Tiwari
```

# 技巧 92. df 命令

`df` 命令（`disk free`）显示已挂载文件系统上可用的总空间和可用空间。
语法：`df [options] [name]`

# 我的系统上有多少 GB 的可用磁盘空间？

使用 `df -h` 以人类可读的格式显示值（例如：`K` 代表 `Kb`，`M` 代表 `Mb`，`G` 代表 `Gb`）。在下面的输出中，`/` 文件系统有 `17GB` 可用磁盘空间，`/home/user` 文件系统有 `70GB` 可用。

```
# df -h

| Filesystem Size Used Avail Use% Mounted |
| --- --- --- --- --- --- |
| /dev/sda1 | 64G | 44G | 17G | 73% | / |
| /dev/sdb1 | 137G | 67G | 0G | 49% | /home/user |
```

# 我的系统上是什么什么类型的文件系统？

选项 `-T` 将显示文件系统类型的信息。在此示例中，`/` 和 `/home/user` 文件系统是 `ext2`。选项 `-a` 将显示所有文件系统，包括系统使用的大小为 `0` 的特殊文件系统。

# df -Tha

```
| Filesystem Type Size Used Avail Use% Mounted on |
| --- --- --- --- --- --- |
| /dev/sda1 | ext2 | 64G | 17G | 73% | / |
| /dev/sdb1 | ext2 | 137G | 67G | 49% | /home/user |
| noneproproc00 | proc | | | | /proc |
| noneysfs00 | sysfs | | | | /sys |
| nonedevpts00 | devpts | | | | /dev/pts |
| nonetmpfs | tmpfs | 2.0G | 2.0G | 0% | /dev/shm |
```

# 技巧 93. kill 命令

`kill` 命令可用于终止运行中的进程。通常，此命令用于杀死挂起且无响应的进程。
语法：`kill [options] [pids][commands]`

# 如何杀死挂起的进程？

首先，使用 `ps` 命令识别你想要杀死的特定进程的进程 ID（`PID`）。一旦知道了 `PID`，将其作为参数传递给 `kill` 命令。下面的示例显示了如何杀死挂起的 `apache httpd` 进程。请注意，通常你应该使用 `"apachectl stop"` 来停止 `apache`。

```
# ps aux | grep httpd

USER %CPU %MEM VSZ RSS TTY START TIME COMMAND

apache 31186 0.016 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd

apache 31187 0.013 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd

# kill 31186 31187
```

```
# kill -9 31186 31187
```

另一种轻松杀死多个进程的方法是在 `.bash_profile` 中添加以下两个函数：

```bash
function psgrep ()
  ps aux | grep "$1" | grep -v 'grep'
}

function pstern ()
  [ $# -eq 0 ] && echo "usage: $0" && return 0
  local pid
  pid=$(ps ax | grep "$1" | grep -v grep | awk '{ print $1 }')
  echo -e "terminating '$1' (processes):\n$pid"
  kill -SIGTERM $pid
}
```

现在执行以下操作识别并杀死所有 `httpd` 进程。

| USER COMMAND |
| --- --- |
| apache | Jul26 |
| apache | Jul26 |
| PID %CPU %MEM |
| 31186 | 0:40 |
| 31187 | 0:37 |

```
| PID %CPU %MEM VSZ RSS TTY START TIME COMMAND |
| --- --- --- --- --- --- --- |
| 31186 0.016 23736 17556 ?S Jul26 0:40 /usr/local/apache2/bin/httpd |
| 31187 0.013 20640 14444 ?S Jul26 0:37 /usr/local/apache2/bin/httpd |
```



杀死 `'httpd'` 进程：
`31186`
`31187`

## 技巧 94. `du` 命令

`du` 命令（disk usage）将打印特定目录及其子目录的空间使用情况。

### 我的主目录和所有子目录占用多少空间？

在下面的示例中，选项 `-s` 代表摘要，它只显示 `/home/user` 的总大小，而不是所有子目录的大小。选项 `-h` 以人类可读的格式显示信息（例如 `K` 代表 `KB`，`M` 代表 `MB`，`G` 代表 `GB`）。此命令与 `"du -sh"` 相同。

```bash
# du -sh /home/user

320M /home/user
```

## 技巧 95. `lsof` 命令

`lsof` 代表 Open files（打开的文件），它将列出系统中所有打开的文件。打开的文件包括网络、设备和目录。`lsof` 命令的输出将包含以下列：
`USER PID FD TYPE SIZE NODE NAME`

### 查看系统所有打开的文件

如下所示执行没有任何参数的 `lsof` 命令。`lsof` 命令本身可能返回记录输出，除了它可以让你大致了解在任何给定时刻系统中打开了多少文件。

```bash
# lsof | wc -l

3093
```

### 查看特定用户打开的文件

使用 `lsof -u` 选项显示特定用户打开的所有文件。

```bash
# lsof -u ramesh

vi 7190 ramesh txt REG 474608 47516 /bin/vi

sshd 7163 ramesh3u IPv6 15088 263 TCP dev-db:abc-12-12.socal.res.rr.com:2631 (ESTABLISHED)
```

管理员可以使用此命令了解用户在系统上执行的内容。

### 列出特定文件的用户

如果你想查看所有使用特定文件的用户，请使用所示 `lsof`。在此示例中，它显示了所有正在使用 `vi` 的用户。

```bash
# lsof /bin/vi

USER PID FD TYPE SIZE NODE NAME

root 7258 txt REG 474608 475196 /bin/vi

amesh 7300 txt REG 474608 475196 /bin/vi
```

## 技巧 96. `Sar` 命令

`Sar` 命令随 `sysstat` 包一起。确保已安装 `sysstat`。如果你的系统中没有安装 `sar`，请从 `Sysstat` 项目获取。`Sar` 是一个优秀的监控工具，可以显示系统每个资源的性能数据，包括 `CPU`、内存、`IO`、分页、网络、中断等。

- `Sar` 收集报告（显示）并保存性能数据。让我们分别查看这三个方面。

### `Sadc` - 系统活动数据

`Sadc`（系统活动数据收集器）按指定的间隔收集系统数据。它使用位于 `/var/log/sa[dd]` 的每日活动文件，其中 `dd` 是当前日期。

### `Sa1` 脚本

`sa1` 如下所示从 `crontab` 调度。根据你的需要每 `5` 分钟或 `15` 分钟运行一次。我将其安排每 `5` 分钟运行一次。

```bash
*5 * * * /usr/lib/sa1 1
```

### `Sa2` 脚本

`sa2` 是一个会在 `/var/log/sa[dd]` 文件写入每日报告的脚本，其中 `dd` 是当前日期。每天凌晨通过 `crontab` 调用一次 `sa2`。

```bash
59 23 * * /usr/lib/sa2 -A
```

注意：`/etc/cron.d/sysstat` 文件随 `sysstat` 包一起，包含了 `sa1` 和 `sa2` 的默认值，你可以相应地更改。

### 使用 `Sar` 命令显示 `CPU` 统计

```bash
# sar -u

Linux 2.6.9-42.ELsmp (dev-db)

12:00:01 AM CPU %user%nice %system%lowowait %idle

12:05:01 AM all 3.700.00

12:10:01 AM all 4.590.00

12:15:01 AM all 3.900.00

12:20:01 AM all 4.060.00

12:25:01 AM all 3.890.00

Skipped..

Average: all

4.56

0.00

1.00

0.15

94.29

95.23
```

注：如果你需要各个 `CPU` 的性能数据细分，请执行以下命令。

```bash
# sar -u P ALL
```

### 使用 `sar` 命令显示磁盘 `IO` 统计信息

```bash
# sar -d
```

```bash
Linux 2.6.9-42.ELsmp(dev-db)
12:00:01 AMdev
12:05:01 AMdev2-0
12:10:01 AMdev8-1
跳过..
平均:
平均:
dev2-0
dev8-1
4.66
1.89
120.77
3.17
69.45
8.02
01/01/2009
tpsrd_sec/s
1.651.28
4.088.11
wr_sec/s
45.43
21.81
```

### 使用 `sar` 命令显示网络统计信息

```bash
# sar -n DEV | more

Linux 2.6.9-42.ELsimp (dev-db)

12:00:01 AMIFACErpx/s

rxcmp/stxcmp/

s rxmcct/s

12:05:01 AMlo0.17

0.000.0

00.00

12:10:01 AMEth052.92

0.000.0

00.00

01/01/2009

tpxck/srxbyt/s

txbyt/s

0.16

25.31

23.33

53.64

10169.74

12178.57
```

```bash
# sar -n SOCK Imore

Linux 2.6.9-42.ELsimp (dev-db)

12:00:01 AMtotscktcpsck

12:05:01 AM5013

12:10:01 AM5013

12:15:01 AM5313

01/01/2009

udpsckrawsck

30

40

50

ip-frag
```

## 技巧 97. `vmstat` 命令

对于典型的性能监控，你只需要 `vmstat` 命令。

此命令显示内存、交换分区、`IO`、系统和 `CPU` 性能信息。

以下命令每 `1` 秒执行一次 `vmstat`，共 `100` 次。

```bash
# vmstat 100

procs ---------memory---- ---swap---- -----io---- --system ----cpu----

r b swpd free buff cache si so

0

0

0 282120 134108 5797012

0 282120 134108 5797012

126

0

0

bi

0

0

bo in

0

0

2

cs us sy id wa

0 0 0 100 0

0 1007 359 0 0 100 0

0 0
0 0

0 282120 134108 579012
0 282120 134108 579012
0
0
0
0
0

0 1117 577 0 0 100 0
0 1007 366 0 0 100 0
```

### `Vmstat` 进程部分
- `r` 字段：可运行进程数
- `b` 字段：阻塞进程数

### 内存部分
- `Swpd` 字段：已交换内存量
- `Free` 字段：空闲内存
- `Buff` 字段：缓冲区内存
- `Cache` 字段：文件系统缓存

### 交换分区部分
- `Si` 字段：每秒从交换分区交换的内存
- `So` 字段：每秒写入交换分区的内存

### `IO` 部分
- `Bi` 字段：每秒从磁盘读取的块
- `Bo` 字段：每秒写入磁盘的块

### 系统部分
- `In` 字段：每秒中断数
- `Cs` 字段：每秒上下文切换数

### `CPU` 部分
- `Us` 字段：用户态运行 `CPU` 时间
- `Sy` 字段：内核态运行 `CPU` 时间
- `Id` 字段：空闲 `CPU` 时间
- `Wa` 字段：等待 `IO` 的时间

## 技巧 98. `Netstat` 命令

`netstat` 命令显示网络相关信息，如连接、路由表、接口统计数据。以下是使用 `netstat` 命令的几个示例。

### 使用 `netstat` 显示活动连接和套接字

```bash
# netstat -an

活动网络连接（监听和已建立）

Proto Recv-Q Send-Q Local Address Foreign State

tcp0 0 0 0.0.0.0:56 0.0.0.0 LISTEN

tcp0 0 0 0.0.0.0:5422 0.0.0.0 LISTEN

tcp0 0 0 0.0.0.0:4089 0.0.0.0 LISTEN

tcp0 0 0 0.0.0.0:7621 0.0.0.0 ESTABLISHED

活动 UNIX 套接字

Proto Type RefCnt Size State Node
```



`unix 2 0 STREAM /tmp/.font`

`unix 2 0 STREAM /tmp/gdm_socket`

`unix 2 0 STREAM /tmp/root`

## 显示路由表

```
# netstat --route
```

内核 IP 路由表

```
Destination 目的 Gateway Iface Genmask Flags
default 192.168.1.1 0 eth0 255.255.255.0 U
162.244.0.0 0 eth0 255.255.255.0 UG
192.168.1.0 0 eth0 255.255.255.0 U
```

## 显示 RAW 网络统计信息

```
# netstat --statistics --raw
```

`Ip:`

`1108343 总接收包`

`0 转发`

`0 丢弃入站包`

`1103744 交付入站包`

`1119763 发出请求包`

`icmp:`

`577135 接收 ICMP 消息`

`64 ICMP 失败`

`ICMP 输入直方图:`

`不可达: 537`

`超时: 65`

`源拥塞: 2`

`echo 请求: 576476`

`echo 回复: 12`

`timestamp 请求: 3`

`掩码请求: 3`

`581558 接收 ICMP 消息`

`0 ICMP 失败`

`ICMP 输出直方图:`

`不可达: 5079`

`echo 回复: 576476`

`timestamp 回复: 3`

## 其他 `netstat` 命令

- `netstat --tcp --numeric` 列出机器的 TCP 连接
- `netstat --tcp --programs` 显示服务器监听的 TCP 端口以及监听该端口的程序
- `netstat -rnC` 显示路由缓存

## 技巧 99. `sysctl` 命令

可以使用 `sysctl` 命令动态更改 Linux 内核参数。

`sysctl` 有助于在运行时配置 Linux 内核参数。

```
# sysctl -a
```

`dev.cdrom.autoclose = 1`

`fs.quota.writes = 0`

`kernel.ctrl-alt-del = 0`

`kernel.domainname = (none)`

`kernel.exec-shield = 1`

`net.core.somaxconn = 128`

`net.ipv4.tcp_window_scaling = 1`

`net.ipv4.tcp_wmem = 409616384`

`net.ipv6.route.mtu expires = 600`

`sunprpc.udp_slot_table_entries = 16`

`vm.block_dump = 0`

### 修改 `/etc/sysctl.conf` 以实现永久更改

在 `/etc/sysctl.conf` 中修改内核参数后，执行 `sysctl -p` 来提交更改。重启后更改仍然有效。

```
# vi /etc/sysctl.conf
# sysctl -p
```

### 临时修改内核参数

要临时修改内核参数，请执行以下命令。
请注意，重启后这些更改将会丢失。

```
# sysctl -w {variable-name=value}
```

## 技巧 100. `nice` 命令

内核根据 `nice` 值决定进程所需的处理器时间。`nice` 取值范围为：-20 到 20。

### 为脚本分配优先级（较高的 `nice` 值）

在下面的示例中，当我在后台启动 `nice-test` 时，它取的 `nice` 值为 0。

```
$ ./nice-test &

[1] 13009

$ ps axl | grep nice-test
```

> 注意：`6m` 列的值 `0` 即为 `nice` 值。

现在，让我们按照下所示执行具有不同 `nice` 值的相同脚本。

```
$ nice -10 ./nice-test &

[1] 13016

$ ps axl | grep nice-test
```

> 注意：`6m` 列的值 `10` 即为该脚本的 `nice` 值。

### 为脚本分配高优先级（较低的 `nice` 值）

在以下示例中，我们为 `nice-test.sh` 脚本分配了 -10（减 10）的 `nice` 值。

注意：只有 `root` 用户才能设置负的 `nice` 值。请以 `root` 身份重试。请注意 `nice` 命令中 `10` 前面有两个横杠。

```
$ nice --10 ./nice-test &

[1] 13021

$ nice: cannot set priority: Permission denied
```

## Linux 技巧

Ajay Kumar Tiwari

[注：值为 -10 的第六列是 shell 脚本的 `nice` 值。]

## 技巧 101. `renice` 命令

`renice` 用于修改运行进程的调度优先级。

### 如何降低运行进程的优先级？（增加 `nice` 值）

在下面的示例中，一个现有的 shell 脚本正以 `nice` 值 `10` 运行。

```
(ps 输出中的第 6 列)

$ ps axl | grep nice-test

0509 13245 13216 30 10 5244 968 wait
pts/10:00 /bin/bash ./nice-test.sh
```

要增加 `nice` 值（从而降低优先级），请执行如下所示 `renice` 命令。

```
$ renice 16 -p 13245

13245: old priority 10, new priority 16

$ ps axl | grep nice-test

0509 13245 13216 36 16 5244 968 wait
pts/10:00 /bin/bash ./nice-test.sh
```

[注：现在，`nice-test.sh` (PID `13245`) 的第六列显示新的 `nice` 值 `16`。]

### 如何提高运行进程的优先级？（减少 `nice` 值）

在下面的示例中，一个现有的 shell 脚本正以 `nice` 值 `10` 运行。

```
(ps 输出中的第 6 列)

$ ps axl | grep nice-test

0509 13254 13216 30 10 4412 968 wait
pts/10:00 /bin/bash ./nice-test.sh
```

要提高优先级，请赋予如下所示的 `nice` 值。但是，只有 `root` 用户可以提高运行进程的优先级，否则你会收到以下错误消息。

```
$ renice 5 -p 13254

renice: 13254: setpriority: Permission denied

Login as root to increase the priority of a running process

$ su -

# renice 5 -p 13254

13254: old priority 10, new priority 5

# ps axl | grep nice-test

0509 13254 13216 255 4412 968 wait
pts/10:00 /bin/bash ./nice-test.sh
```

[注：现在第六列显示了较小的 `nice` 值 `5`（优先级已提高）]
