
要只查看 `HOME` 的值，你可以输入 `echo $HOME`。你也可以使用 `set` 或 `env`。

想将 `/tmp` 目录添加到 `PATH` 变量中目录列表的末尾。你可以在提示符输入什么命令来实现这一点？

你需要保留现有的目录，所以你需要输入 `PATH=$PATH:~/temp`。你还需要输入 `export PATH`。

让我们在下面的练习中练习环境变量的操作。

# 使用环境变量

在本次练习中，你将练习在 `bash` shell 中操作环境变量。请完成以下任务：

- 如果必要，启动你的 Linux 系统并以标准用户身份登录。如果你在第 3 章的实验练习中安装了系统，可以使用 `tux` 作为用户登录，密码为 `Mlinux273`。
- 输入 `su –` 后你的 root 密码切换到 root 用户账户。
- 在 shell 提示符处，输入以下命令查看相应环境变量的值：

```
echo $PWD

echo $HOME

echo $EUID

echo $PATH

echo $PS1
```

- 通过以下操作更改你的 shell 提示符，以显示当前登录的用户、Linux 主机名、当前时间、当前工作目录的完整路径以及一个冒号：
- 在 shell 提示符处输入 `PS1="\u@h \t \w:"`。提示符应该立即变化。
- 在 shell 提示符处输入 `export PS1`。
- 如果你想让对 `PS1` 环境变量的更改持久化，你应该在你特定的系统上编辑哪个文件？

考虑到这一点，我们现在来谈谈创建用户定义变量。

# 创建用户定义变量

在前面的主题中，我们重点关注了环境变量的操作。这些变量在系统每次启动时都会自动为你定义。

## 管理 Linux 环境变量 495

图 9-20 Shell - 创建用户定义变量

![](img/8156850acb7240fabbc4667ef20f2fa8_536_0.png)

然而，你实际上也可以创建自己的自定义变量。这听起来很困难，但实际上并非如此。事实上，操作方法与处理环境变量完全相同。只需在提示符处输入 `variable=value` 即可。

例如，假设我想创建一个名为 `ME` 的变量，并将其设置为值 `"Robb Tracy"`。我可以通过在提示符处输入 `ME="Robb Tracy"` 来实现。完成完成后，名为 `ME` 的命名变量被添加到我的变量列表中，并设置为值 `Robb Tracy`。你可以使用 `echo` 命令来查看 `ME` 变量的值，如图 9-20 所示。

作为环境变量，用户定义变量仅对当前 shell 实例可用。要让其他 shell（包括由当前 shell 创建的子 shell）可用，你需要使用 `export` 命令将其导出。在此例中，我会在 shell 提示符处输入 `export ME`。

除了环境变量外，你还可以像处理环境变量一样，使用 `set` 或 `env` 来查看用户定义变量。使用 `set` 查看我创建的 `ME` 变量的示例如图 9-21 所示。

作为环境变量，你可以通过将相应的命令添加到之前提到的 bash 配置文件之一来使用户定义变量持久化。在创建用户定义变量时，请记住以下规则：

- 变量名可以包含字母或数字，但不能以数字开头。
- 变量名可以包含 `_` 或 `.`。
- 虽然不是强制的，但在命名变量时应尝试使用所有大写字母。注意，当你输入 `set` 或 `env` 查看所有环境变量时，它们使用的是大写名称。你也应该这样做。

我们在这里处理的最后一个与变量相关的课题是别名（aliases）。让我们接下来讨论别名的工作原理。

# 496 第 9 章：使用 Linux Shell

使用 `set` 命令查看用户定义变量的值

![](img/8156850acb7240fabbc4667ef20f2fa8_537_0.png)

# 创建别名

别名非常酷。别名在很多方面与变量相关，但具有不同的功能。别名是 Linux 中指向不同文件或命令的快捷方式。当系统启动时，会自动为你创建一系列别名。你可以在 shell 提示符处输入 `aliases` 来查看这些内容。

注意图 9-22，列出的系列别名并不是真正的命令。相反，它们是指向命令的别名。例如，如果在 shell 提示符处输入 `dir`，`alias` 的输出告诉我们 `-l` 命令实际上正在运行。同样，输入 `..` 实际上会执行 `cd ..`。

你也可以创建自己的别名。要这样做，在提示符处输入 `alias name="command"`。假设你想在 shell 提示符处最先列出目录的长列表，你可以在提示符处输入 `alias longlist="ls -l"`。这如图 9-23 所示。现在，如果你在 shell 提示符处输入 `longlist`，就会执行 `ls -l` 命令并将其输出显示在屏幕上。这如图 9-24 所示。

# 管理 Linux 环境变量 497

图 9-22 查看系统生成的别名

```
t@linux1:~$ alias
alias +==pushd
alias -=popd
alias ...=cd
alias ..=cd ../
alias beep=echo -en "\007"
alias cd=-cd
alias dir=ls -ls
alias l=ls -la
alias ll=ls -l
alias ls=/bin/ls $LS_OPTIONS
alias l=ls -l
alias md=mkdir -p
alias c=less
alias rd=rmdir
alias rehash=hash -r
alias error=echo "Error: Try the command: ummount 1>&2; false"
alias which='_which'
alias you='su -c /sbin/yast2 online_update'
t@linux1:~$
```

你甚至可以使用分号（`;`）在单个别名中包含多个命令。例如，如果你想创建一个挂载 CD 驱动器并生成文件长列表的别名，你可以在 shell 提示符处输入：

```
alias mcd="mount -t /dev/cdrom;ls -l /media/cdrom"
```

之后，你可以在提示符处输入 `mcd` 来挂载 CD 并生成其文件列表。任何用 `alias` 命令定义的别名都不是持久的。如果你重启系统，它们在系统启动时就会消失。你可以通过将别名添加到 bash 配置文件之一来使别名持久化。

# 498 第 9 章：使用 Linux Shell

图 9-23 使用 `alias` 命令创建新别名

```bash
tux@linux1:> alias longlist='ls -l'
tux@linux1:> alias +==pushd
alias -==popd
alias ===cd
alias ..='cd ../
alias beepa='echo -en "\007"
alias cd..='cd'
alias dir..='ls -l'
alias ls='ls -la
alias rehash=hash -r
alias error=echo "Error: Try the command: ummount 1>&2; false"
alias which='_which'
alias you='su -c /sbin/yast2 online_update'
tux@linux1:>
```

你可以将别名添加到 `/etc/profile`，如果你希望它们对所有用户都有效。你可以将它们添加到用户家目录下的文件，如果你希望它们仅对该用户有效。

# 管理 Linux 环境变量 499

图 9-24 在 shell 提示符处运行

```
tux@linux1:> longlist
total 3169
-rw-xr-x 2 users 72 2006-11-16 09:55 magraton-0.2.7-38.i586.rpm
-rw-xr--x 1 users 121592 2006-11-21 16:36 backup
-rw-xr--x 3 users 72 2006-11-11 09:59 commands
drwx------ 1 users 5 2006-11-16 20:51 sched
drwx------ 2 users 528 2006-11-22 15:51 Desktop
lwmxxr-x 2 users 15 2006-11-16 05:34 docs -> /usr/share/doc/
-rw-xr--x 2 users 80 2006-11-10 14:47 Documents
-rw-xr--x 1 users 895043 2006-11-16 12:55 gftp-0.18-23.i586.rpm
-rw-xr--x 1 users 508060 2006-11-22 12:34 gftp-2.0.9-k6.rpm
-rw-xr--x 1 users 0 2006-11-19 19:55 mfile.txt
-rw-xr--x 2 users 80 2006-11-10 14:47 public_html
-rw-xr--x 10 users 1680 2006-11-22 12:41 pure-ftpd-1.0.21
-rw-xr--x 1 users 594394 2006-11-16 21:43 pure-ftpd-1.0.21.tar.gz
```

# 500 第 9 章：使用 Linux Shell

3. 在 shell 提示符处，创建一个名为 `mntplf` 的别名，它可以自动挂载软磁盘并列出软驱器中已挂载的文件系统列表：`alias mntplf="mount -t vfat /dev/fd0 /media/floppy;mount"`。

如果你使用的是 Fedora 或 Red Hat 发行版，请使用 `/mnt/floppy` 代替 `/media/floppy`。

- 4. 在 shell 提示符处输入 `alias` 并验证别名是否已创建。
- 5. 在软驱器中插入一张 DOS 格式的软盘。
- 6. 在 shell 提示符处输入 `mntplf` 测试您的软盘。
- 7. 验证您的软盘已挂载到挂载表中。
- 8. 在 shell 提示符处输入 `umount /dev/fd0` 卸载软盘。
- 9. 在您的 shell 中输入 `ls -a`。如果您想让别名持久，在您特定的发行版中需要编辑哪个文件？

现在您已经知道了如何管理变量，是时候讨论如何重定向 shell 命令的输出了。让我们接下来进行这一点。

## 认证目标 9.03

## 管理 shell 命令的输入输出

shell（以及其他 Linux shell）非常强大且灵活。使其具有这种特性的功能之一是其操纵命令输入和输出的能力。在本章的这部分，我们将探索如何实现。具体来说，我们将涵盖以下内容：

- 标准 `bash` 文件描述符
- 重定向 shell 命令的输出和输入
- 管道传输信息

让我们从复习 `bash` 文件描述符开始。

### 标准 bash 文件描述符

在学习如何重定向或管道 `bash` 命令的输出之前，您必须首先理解 `bash` 文件描述符。三个文件描述符

# 管理 shell 命令的输入输出 501

图 9-25

![](img/8156850acb7240fabbc4667ef20f2fa8_542_0.png)

shell 文件描述符

您在 shell 提示符处输入的每个命令都可以可以使用这些描述符。它们如图 9-25 所示。这三个文件描述符包括以下内容：

- `stdin`: 此描述符代表标准输入。标准输入是提供给特定命令进行处理的输入。命令的 `stdin` 用数字 `0` 表示。
- `stdout`: 此描述符代表标准输出。标准输出就是特定命令的输出。例如，`ls` 命令的目录列表就是它的 `stdout`。命令的 `stdout` 用数字 `1` 表示。
- `stderr`: 此描述符代表标准错误。标准错误是命令生成的（如果有的话）错误代码。命令的 `stderr` 用数字 `2` 表示。

并不是所有命令都使用这三个描述符，但许多命令确实使用。让我们来看一些例子。假设我使用 `cat /test2.txt` 显示用户主目录下某个文件的内容，如图 9-26 所示。

`cat` 命令在屏幕上显示了文件的内容。这就是 `cat` 命令的 `stdout`。现在，假设我输入相同的命令，但指定了一个不存在的文件，如图 9-27 所示。

由于文件不存在，`cat` 命令生成了错误。这就是 `cat` 命令的 `stderr`。了解了这些描述符后，您可以在命令执行时重定向每一个。让我们接下来讨论如何实现这一点。

图 9-26 查看 `cat` 命令的 `stdout`

```
linux@linux1:~$ Shell - Console
Session Edit View Bookmarks Settings Help
tux@linux1:~$ cat ./test2.txt
Et reque veri atomorum vel, eos sale partiendo id, quae salutanduis vis at a.
t vis cibo partim, maxim mandamus at pro.Usu agam legere delicata ut, per dmocri scriptorem an.tuk@linux1:~
Shell
```

# 502 第 9 章：使用 Linux Shell

图 9-27 查看 `cat` 命令的 `stderr`

![](img/8156850acb7240fabbc4667ef20f2fa8_543_0.png)

## 重定向 shell 命令的输出输出

通过这三个描述符，您可以操纵命令获取输入以及发送输出的地方。在本章的这部分，我们将回顾您如何在命令行中实现这一点。我们将讨论：

- 重定向输出
- 重定向输入

让我们从讨论如何重定向输出开始。

### 重定向输出

`bash` 允许您操纵命令生成的输出去向。默认情况下，它显示在屏幕上。但是，您可以指定它去往其他地方。例如，将命令的输出重定向到文本文件是非常常见的，特别是当命令的输出很长时。重定向是通过命令行中的 `>` 字符实现的。重定向输出的语法是 `command output>filename`。例如，假设我们想使用 `tail` 命令查看 `/var/log/messages` 文件的最后几行，并将输出保存到名为 `lastmessages` 的文件中。我们可以通过重定向 `tail /var/log/messages 1> lastmessages` 来实现。这告诉 shell 重定向 `tail /var/log/messages 1> lastmessages`。（此处省略了大量重复的描述句）

# 管理 Shell 命令的输入输出 505

# 图 9-30

```
linux1:~# tail /var/log/messages
Dec 8 12:53:19 linux1 SUSEFirewall2: Setting up rules from /etc/sysconfig/SUSE
Dec 8 12:53:21 linux1 SUSEFirewall2: Firewall rules successfully set
Dec 8 12:53:23 linux1 SUSEFirewall2: batch committing...
Dec 8 12:53:23 linux1 SUSEFirewall2: Error: iptables-batch failed, re-running u
Dec 8 12:53:25 linux1 SUSEFirewall2: Firewall rules successfully set
Dec 8 12:53:25 linux1 kernel: bootsplash: status on console 0 changed to on
Dec 8 13:03:03 linux1 zmd ShutdownManager (WARN): Preparing to sleep...
Dec 12/09/2006 12:43:03 zmd ShutdownManager (WARN): Going to sleep, waking up at
Dec 8 13:52:57 linux1 syslog-ng[2231]: STATS: dropped 0
Dec 8 14:03:15 linux1 su: (to root) tux on /dev/pts/3
linux1:~# #
```

当你需要向期望接收文本的命令发送大量文本时，重定向就大显身手。

例如，你可以将文本文件中的单词列表发送到 `sort` 命令，并让它为你进行排序。在图 9-31 中，我使用 `vi` 编辑器创建了一个名为名为 `words` 的文本文件，其中包含文本。

# 图 9-31

```
who
what
why
where
how
```

# 506 第 9 章：使用 Linux Shell

图 9-32 在命令行处重定向输入

![](img/8156850acb7240fabbc4667ef20f2fa8_547_0.png)

创建此文件后，我可以指定将其作为 `sort` 命令的输入。我可以在 shell 提示符下输入 `sort <./words` 来。输出将显示在屏幕上，如图 9-32 所示。

| 场景与解决方案 |
| :--- |
| 你想将 `mount` 命令的标准输出 (`stdout`) 写入名为 `mountedfs` 的文件，并将标准错误 (`stderr`) 写入名为 `fserr` 的文件。你会使用什么命令来实现这一点？ | 你将输入 `mount 1>mountedfs 2>fserr`。 |
| 写入名为 `myprocesses` 的文件且不覆盖文件的现有内容。你会使用什么命令来实现？ | 你将输入 `top 1>>myprocesses` 或 `top >myprocesses`。 |

- 1. 如果必要，启动你的 Linux 系统并以标准用户身份登录。如果你使用了第 3 章的实验练习来安装系统，可以使用密码 `M3linux273` 以 `root` 身份登录。
2. 通过输入 `su` 后跟你的 root 密码切换到 root 用户账户。
