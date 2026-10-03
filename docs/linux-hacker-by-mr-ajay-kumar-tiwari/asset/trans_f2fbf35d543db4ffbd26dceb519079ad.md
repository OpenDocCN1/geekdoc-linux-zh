
![](img/d85fdc87049f4b892fa74b89bf49ed67_0_0.png)

## Linux 技巧

阿贾伊·库马尔·提瓦里

## Linux 技巧

## Linux 技巧

阿贾伊·库马尔·提瓦里

## 目录

引言

前言

版本

## 第1章：强大的 CD 命令技巧

使用 CDPATH 为 cd 命令定义基本目录

使用 cd 别名有效向上导航目录

使用单个命令执行 mkdir 和 cd

使用“cd -”在最后两个目录之间切换

使用 dirs、pushd 和 popd 操作目录堆栈

使用“shopt -s cdspell”在 cd 时自动纠正输入错误的目录名

## 第2章：日期操作

设置系统日期和时间

设置硬件日期和时间

以特定格式显示当前日期和时间

显示过去的日期和时间

显示未来的日期和时间

## 第3章：SSH 客户端命令

识别 SSH 客户端版本

使用 SSH 登录远程主机

调试 SSH 客户端会话

使用 SSH 转义字符切换 SSH 会话

使用 SSH 转义字符查看 SSH 会话统计信息

## 第4章：必备 Linux 命令

Grep 命令

Find 命令

抑制标准输出和错误消息

Join 命令

更改大小写

Xargs 命令

Sort 命令

Uniq 命令

Cut 命令

Stat 命令

Diff 命令

显示用户的总连接时间

## 第5章：PS1、PS2、PS3、PS4 和 PROMPT_COMMAND

PS1 - 默认交互提示

PS2 - 继续交互提示

PS3 - shell 脚本中“select”使用的提示

PS4 - 由“set -x”用于前缀跟踪输出

PROMPT_COMMAND

## 第6章：使用 PS1 的彩色和功能性 Shell 提示

在提示中显示用户名、主机名和目录基名

在提示中显示当前时间

在提示中显示任何命令的输出

更改提示的前景色

更改提示的背景色

在提示中显示多种颜色

使用 tput 更改提示颜色

使用 PS1 变量的可用代码创建自己的提示

在 PS1 变量中使用 bash shell 函数

在 PS1 变量中使用 shell 脚本

## 第7章：归档和压缩

Zip 命令基础

使用 zip 命令的高级压缩

Zip 文件的密码保护

验证 zip 归档

Tar 命令基础

将 gzip、bzip2 与 tar 结合使用

## 第8章：命令行历史

使用 HISTTIMEFORMAT 在历史中显示时间戳

使用 Control+R 搜索历史

使用 4 种不同方法快速重复上一个命令

从历史中执行特定命令

执行以特定单词开头的上一个命令

使用 HISTSIZE 控制历史中的总行数

使用 HISTFILE 更改历史文件名称

使用 HISTCONTROL 消除历史中的连续重复条目

使用 HISTCONTROL 删除整个历史中的重复项

使用 HISTCONTROL 强制历史不记住特定命令

使用 -c 选项清除所有先前的历史

替换历史命令中的单词

为特定命令替换特定参数

使用 HISTSIZE 禁用历史的使用

使用 HISTIGNORE 从历史中忽略特定命令

## 第9章：系统管理任务

- 使用 fdisk 分区
- 使用 mke2fs 格式化分区
- 挂载分区

使用 tune2fs 精细调整分区

创建交换文件系统

创建新用户

创建新组并分配给用户

在 OpenSSH 中设置 SSH 无密码登录

使用 ssh-agent 配合 ssh-copy-id

Crontab

使用 Magic SysRq 键安全重启 Linux

## 第10章：Apachectl 和 Httpd 示例

向 apachectl 传递不同的 httpd.conf 文件名

在不修改 httpd.conf 的情况下使用临时 DocumentRoot

临时提高日志级别

显示 Apache 内部的模块

显示 httpd.conf 内部接受的所有指令

更改后验证 httpd.conf

显示 httpd 构建参数

按需仅加载特定模块

## 第11章：Bash 脚本编写

.bash_* 文件的执行顺序

如何在 bash shell 中生成随机数

调试 shell 脚本

引用

在 shell 脚本中读取数据文件字段

## 第12章：系统监控和性能

Free 命令

Top 命令

Ps 命令

Df 命令

Kill 命令

Du 命令

Sar 命令

vmstat 命令

Netstat 命令

Sysctl 命令

Nice 命令

Renice 命令

lsof 命令

## Linux 技巧

阿贾伊·库马尔·提瓦里

## 引言

> “世界上只有10种人——懂二进制的人，不懂的人，以及懂灰码的人”
> — 极客

![](img/d85fdc87049f4b892fa74b89bf49ed67_10_0.png)

我是阿贾伊·库马尔·提瓦里，本书的作者

我在多种语言上进行了深入编程，C 是我最喜欢的。我在基础设施方面做了大量工作，包括 Linux 系统管理、DBA、网络、硬件和存储（EMC）。

版权所有 © 2015 – 阿贾伊·库马尔·提瓦里

## Linux 技巧

阿贾伊·库马尔·提瓦里

## 前言

又一个技巧合集？是的！如果你刚刚完成了第一门管理员课程或正在寻找更有效的工作方法，“Linux 技巧”电子书是一个很好的起点。这些实用技巧简洁、写得好且易于阅读。

做得好 - 我会向我的学生推荐这本电子书。

> — 教授 博士 弗里茨·梅纳，FH Südwestfalen，德国

（多款 Vim 插件的作者，包括 bash-support vim 插件）

## 版本

| 版本 | 1.0 |
| 日期 | 25-Mar-2015 |
| 修订 | 首版 |

## Linux 技巧

阿贾伊·库马尔·提瓦里

## 第1章：强大的 CD 命令技巧

cd 是 UNIX 会话期间使用最频繁的命令之一。本章提到的 6 个 cd 命令技巧将立即提升你的生产力，并使从命令行导航目录结构变得更容易。

### Hack 1. 使用 CDPATH 为 cd 命令定义基本目录

如果你经常执行 cd 进入特定父目录的子目录，你可以设置 CDPATH 为父目录，然后在不给出父目录路径的情况下执行 cd 进入子目录，如下所述。

```
[ramesh@dev-db ~]# pwd
/home/ramesh
[ramesh@dev-db ~]# cd mail
-bash: cd: mail: No such file or directory
```

[注意：这是在当前目录下查找 mail 目录]

```
[ramesh@dev-db ~]# export CDPATH=/etc
[ramesh@dev-db ~]# cd mail
/etc/mail
```

[注意：这是在 /etc 下查找 mail，而不是在当前目录下]

```
[ramesh@dev-db /etc/mail]# pwd
/etc/mail
```

要使此更改永久生效，请将 export CDPATH=/etc 添加到你的 ~/.bash_profile

与 PATH 变量类似，你可以在 CDPATH 变量中添加多个目录条目，用 : 分隔，如下所示。

```
export CDPATH=.:~/:/etc:/var
```

此技巧在以下情况下非常有帮助：

- Oracle DBA 经常在 $ORACLE_HOME 下工作，可以将 CDPATH 变量设置为 oracle 主目录
- Unix 系统管理员经常在 /etc 下工作，可以将 CDPATH 变量设置为 /etc
- 开发人员经常在项目目录 /home/projects 下工作，可以将 CDPATH 变量设置为 /home/projects
- 终端用户经常访问其主目录下的子目录，可以将 CDPATH 变量设置为 ~（主目录）

### Hack 2. 使用 cd 别名有效向上导航目录

当你向上导航一个非常长的目录结构时，你可能会使用 cd ....\ 并根据要向上移动的目录数量使用多个 ..\，如下所示。

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

阿贾伊·库马尔·提瓦里

不要执行 cd ../../../../ 来向上导航四级，使用以下三种别名方法之一：

### 方法 1：使用“..n”向上导航目录

在下面的示例中，..4 用于向上移动 4 级目录，..3 用于向上移动 3 级目录，..2 用于向上移动 2 级目录。将以下别名添加到你的 ~/.bash_profile 并重新登录。

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

[注意：使用 ..4 向上移动 4 级目录]

```
# pwd
/tmp/very/long/directory/structure/
```

### 方法 2：仅使用点向上导航目录

在下面的示例中，.....（五个点）用于向上移动 4 级目录。

输入 5 个点来向上移动 4 个目录结构非常容易记住，因为当你输入前两个点时，你在想“向上移动一个目录”，之后每多一个点，就向上移动一级。所以，使用 ....（四个点）来
