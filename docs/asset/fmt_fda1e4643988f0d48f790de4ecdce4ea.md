
你也可以通过在搜索-替换表达式前加上前缀来指定 `sed` 搜索特定的行。例如，要在包含字符串 `"love"` 的行中全局地将字符串 `"the"` 替换替换为 `"THE"`，你可以使用以下命令：

```
[root@server1]# # cat prologue | sed s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth the fatal loins of these two foes
A pair of star-cross'd lovers take THEIR life;
Whole misadventured piteous overflows
Do with their death bury THEIR' strife.
The fearful passage of THEIR death-mark'd love,
And the continuance of THEIR parents' rage,
Which, but THEIR children's end, could remove,
is now the two hours' traffic of our stage;
The which if you with patient ears attend,
What here shall miss, our toil shall strive to mend.
[root@server1]# #
```

你可以强制 `sed` 仅在某些行上执行搜索-替换。要在第 5 到 8 行中全局地将字符串 `"the"` 替换为 `"THE"`，你可以使用以下命令：

```
[root@server1]# # cat prologue | sed 5,8s/the/THE/g
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes civil hands unclean.
From forth THE fatal loins of THESE two foes
```

# 第 8 章 与 BASH Shell 的操作

A pair of star-cross'd lovers take THEIR life;

Whole misadvented piteous overthrows

Do with THEIR death bury their parents' strife.

The fearful passage of their death-mark'd love,

And the continuance of their parents' rage,

Which, but their children's end, nought could remove,

Is now the two hours' traffic of our stage;

Which if you with patient ears attend,

What shall miss, our toil shall strive to mend.

root@server1]#

你也可以用 `sed` 移除不需要的文本行。要删除所有包含单词 `"the"` 的行，你可以使用以下命令：

```
root@server1]# cat prologue | sed /the/d
Two households, both alike in dignity,
In fair Verona, where we lay our scene,
From ancient grudge break to new mutiny,
Where civil blood makes hands unclean.
Whole misadvented piteous overthrows
The if you with patient ears attend,
What shall miss, our toil shall strive to mend.
root@server1]#
```

与 `sed` 类似，`awk` 命令搜索文本模式并对找到的文本执行某些操作。然而，`awk` 命令将每行文本视为数据库中的一条记录，并将行中的每个单词视为数据库的字段。例如，`"Hello, how,"` `"are,"` and `"you?"` 这一行有四个字段：`$1`, `$2`, `$3`, 和 `$4`。例如，要使用包含单词 `"the"` 的 `prologue` 文件仅显示行中的第一个和第四个单词，你可以使用以下命令：

默认情况下，`awk` 命令使用空格或制表符字符作为行中每个字段的分隔符。然而，Linux 系统上的大多数配置文件是用冒号（`:`）字符分隔的。要更改 `awk` 使用的分隔符，你可以在命令中指定 `-F` 选项。例如下面的示例列出了用冒号分隔的文件 `/etc/passwd` 的最后 10 行，并仅查看文件最后 10 行中包含单词 `"bob"` 的行的第 6 和第 7 个字段：

### Shell 变量

```
[root@server1 ~]# tail /etc/passwd
ldap:x:55:55:LDAP User:/var/lib/ldap:/bin/false
mysql:x:27:27:MySQL Server:/var/lib/mysql:/bin/bash
postgres:x:26:26:PostgreSQL Server:/var/lib/pgsql:/bin/bash
fax:x:78:78:getty fax user:/var/sp:/sbin/nologin
nux:x:57:57:Network UPS Tools:/var/lib/ups:/bin/false
privoxy:x:73:73:/etc/privoxy:/sbin/nologin
tcat:x:53:53:Tomcat server:/var/tomcat:/sbin/nologin
cyrus:x:76:12:IMAP Server:/var/lib/imap:/bin/bash
exim:x:93:/spool/
bob:x:500:500:/home

[root@server1 ~]# tail /etc/passwd | awk -F ':' '/bob'
{print $6, $7}
home/bob /bin/bash
[root@server1]# _
```

两者 `awk` 和 `sed` 都允许你在搜索中指定正则表达式。

![](img/037b)

### SHELL 变量

前面的输出中的某些环境变量被用于需要系统信息的程序；`OSTYPE`（操作系统类型）`SHELL`（shell 路径）变量是前面输出中的示例。其他变量用于设置用户的运行环境；最常见的包括以下：

- `PS1`—默认 shell 提示符
- `HOME`—用户目录的绝对路径
- `PWD`—当前工作目录
- `PATH`—可执行程序的目录列表

`PS1` 代表 BASH shell 提示符。要查看此变量的内容，你可以使用 `set` 命令，如下所示：

```
[root@server1]# 
```

### 环境变量

```
[root@server1]# set
BASH=//bash
ENV=/.bashrc
BASH_VERSION='2.0-release'
COLORS=/etc/DIR_COLORS
TERM=xterm
COLUMNS=80
```

# 第 8 章 与 BASH Shell 的操作

```
[root@server1]#
```

# 第 8 章使用 BASH 壳

这是新的提示符：# `date`

Fri May 27 10:15:56 EDT 2005

这是新的提示符：# 

这是新的提示符：# `who`

root pts/0 May 30 09:58 (3.0.0.2)

这是新的提示符：# 

这是新的提示符：# `PS1="\u@\h \W"`#

```
[root@server1 root]# _
```

`HOME` 变量被那些需要指向当前家目录路径来存储或搜索文件的程序使用，因此它不应该被更改。如果 root 用户登录系统，`HOME` 变量被设置为 `/root`；或者，如果用户登录系统，`HOME` 变量被设置为 `/home/user`。此元字符表示当前用户的家目录；此元字符是下面下方显示的 `HOME` 变量的指针：
