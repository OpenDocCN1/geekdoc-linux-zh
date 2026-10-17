
管道通常用于对数据执行复杂操作。可以将多个命令组合成一个管道。通常以这种方式使用的命令被称为过滤器。过滤器接收输入，以某种方式更改它，然后输出它。我们要尝试的第一个是`sort`。假设我们想要制作`/bin`和`/usr/bin`中所有可执行程序的合并列表，按排序顺序排列，并查看 resulting 列表。

```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | less
```

因为我们指定了两个目录（`/bin`和`/usr/bin`），所以`ls`的输出将由两个排序列表组成，每个目录一个。通过在管道中包含`sort`，我们更改了数据以产生一个单一的、排序的列表。

### > 与 | 的区别

乍一看，很难理解管道操作符`|`执行的重定向与重定向操作符`>`执行的重定向之间的区别。简单地说，重定向操作符将一个命令与一个文件连接起来，而管道操作符将一个命令的输出与第二个命令的输入连接起来。

```
command1 > file1
command1 | command2
```

很多人学习管道时会尝试以下操作，“只是想看看会发生什么”：

```
command1 > command2
```

答案：有时会发生非常糟糕的事情。

这里有一个实际例子，由一位读者提交，他正在管理一台基于 Linux 的服务器设备。作为超级用户，他这样做了：

```
### cd /usr/bin
### ls > less
```

第一个命令将他置于大多数程序存储的目录中，第二个命令告诉 shell 用`ls`命令的输出覆盖文件`less`。由于`/usr/bin`目录中已经包含一个名为`less`的文件（less 程序），第二个命令用`ls`的文本覆盖了`less`程序文件，从而破坏了他系统上的`less`程序。

### `grep`: 打印匹配模式的行

`grep`是一个强大的程序，用于在文件中查找文本模式。它的使用方式如下：

```
grep pattern filename
```

当`grep`在文件中遇到“`pattern`”时，它会打印出包含它的行。`grep`可以匹配的模式可以非常复杂，但现在我们将集中于简单的文本匹配。我们将在第 19 章介绍高级模式，称为正则表达式。

假设我们想要找到程序列表中所有文件名中包含单词`zip`的文件。这样的搜索可能会让我们了解系统上与文件压缩有关的某些程序。我们会这样做：

```
[me@linuxbox ~]$ ls /bin /usr/bin | sort | uniq | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

`grep`有几个方便的选项。

- `-i`，这会导致`grep`在执行搜索时忽略大小写（通常搜索区分大小写）

- `-v`，这告诉`grep`只打印那些不匹配模式的行

### `head`/`tail`: 打印文件的开头/结尾部分

有时你并不想要某个命令的所有输出。你可能只想要前几行或最后几行。`head`命令会打印文件的最初 10 行，而`tail`命令会打印最后 10 行。默认情况下，两个命令都打印 10 行文本，但这可以通过`-n`选项进行调整。

```
[me@linuxbox ~]$ head -n 5 ls-output.txt
total 343496
-rwxr-xr-x 1 root root      31316 2017-12-05 08:58 [
-rwxr-xr-x 1 root root       8240 2017-12-09 13:39 411toppm
-rwxr-xr-x 1 root root      111276 2017-11-26 14:27 a2p
-rwxr-xr-x 1 root root       25368 2016-10-06 20:16 a52dec
[me@linuxbox ~]$ tail -n 5 ls-output.txt
-rwxr-xr-x 1 root root       5234 2017-06-27 10:56 znew
-rwxr-xr-x 1 root root        691 2015-09-10 04:21 zonetab2pot.py
-rw-r--r-- 1 root root        930 2017-11-01 12:23 zonetab2pot.pyc
-rw-r--r-- 1 root root        930 2017-11-01 12:23 zonetab2pot.pyo
lrwxrwxrwx 1 root root          6 2016-01-31 05:22 zsoelim -> soelim
```

这些命令也可以在管道中使用：

```
[me@linuxbox ~]$ ls /usr/bin | tail -n 5
znew
zonetab2pot.py
zonetab2pot.pyc
zonetab2pot.pyo
zsoelim
```

`tail`有一个选项可以让你实时查看文件。这对于在日志文件被写入时观察其进展非常有用。在下面的示例中，我们将查看`/var/log`中的`messages`文件（如果`messages`缺失，则为`/var/log/syslog`文件）。在某些 Linux 发行版上，需要超级用户权限才能执行此操作，因为`/var/log/messages`文件可能包含安全信息。

```
[me@linuxbox ~]$ tail -f /var/log/messages
Feb  8 13:40:05 twin4 dhclient: DHCPACK from 192.168.1.1
Feb  8 13:40:05 twin4 dhclient: bound to 192.168.1.4 -- renewal in 1652 seconds.
Feb  8 13:55:32 twin4 mountd[3953]: /var/NFSv4/musicbox exported to both 192.168.1.0/24 and twin7.localdomain in 192.168.1.0/24,twin7.localdomain
Feb  8 14:07:37 twin4 dhclient: DHCPREQUEST on eth0 to 192.168.1.1 port 67
Feb  8 14:07:37 twin4 dhclient: DHCPACK from 192.168.1.1
Feb  8 14:07:37 twin4 dhclient: bound to 192.168.1.4 -- renewal in 1771 seconds.
Feb  8 14:09:56 twin4 smartd[3468]: Device: /dev/hda, SMART Prefailure Attribute: 8 Seek_Time_ Performance changed from 237 to 236
Feb  8 14:10:37 twin4 mountd[3953]: /var/NFSv4/musicbox exported to both 192.168.1.0/24 and twin7.localdomain in 192.168.1.0/24,twin7.localdomain
Feb  8 14:25:07 twin4 sshd(pam_unix)[29234]: session opened for user me by (uid=0)
Feb  8 14:25:36 twin4 su(pam_unix)[29279]: session opened for user root by me(uid=500)
```

使用`-f`选项，`tail`会持续监控文件，当有新行追加时，它们会立即显示在屏幕上。这会一直持续到你输入 CTRL-C 为止。

### `tee`: 从标准输入读取并输出到标准输出和文件

按照我们的管道比喻，Linux 提供了一个名为`tee`的命令，它在我们的管道上创建了一个“T”型接头。`tee`程序读取标准输入，并将其复制到标准输出（允许数据继续沿管道传输）以及一个或多个文件中。这对于在处理的中期阶段捕获管道的内容非常有用。这里我们重复之前的其中一个示例，这次加入`tee`来在`grep`过滤管道内容之前，将整个目录列表捕获到文件`ls.txt`中：

```
[me@linuxbox ~]$ ls /usr/bin | tee ls.txt | grep zip
bunzip2
bzip2
gunzip
gzip
unzip
zip
zipcloak
zipgrep
zipinfo
zipnote
zipsplit
```

### 总结

一如既往，请查阅本章中我们介绍过的每个命令的文档。我们只看到了它们最基本的使用方法。它们都有许多有趣的选项。随着我们 Linux 经验的积累，我们会发现命令行重定向功能对于解决专门问题非常有用。有许多命令使用标准输入和输出，几乎所有命令行程序都使用标准错误来显示其信息性消息。
