
首先需要做的是创建一个包含 `bill` 和 `karen` 成员的组。使用图形化用户管理工具，`bill` 创建了一个名为 的组并将 `bill` 和 `karen` 加入其中：

![](img/bf35d3b896a7fc440213722090d1b1cf_128_0.png)

接下来，`bill` 创建音乐文件的目录：

```
[bill@linuxbox ~$ sudo mkdir /usr/local/share/Music
Password:
```

由于 `bill` 正在家目录之外操作文件，需要超级用户权限。目录创建后，它具有以下所有权权限：

```
[bill@linuxbox ~]$ ls -ld /usr/local/share/Music
drwxr-xr-x 2 root 4096 2008-03-21 18:05 /usr/local/share/Music
```

我们可以看到，该目录由 `root` 所有，权限为 `755`。为了让这个目录共享，`bill` 需要更改组所有权和组权限以允许写入：

# 行使我们的权限

```
[bill@linuxbox -$] sudo chown :music /usr/local/share/Music
[bill@linuxbox -$] sudo chmod 775 /usr/local/share/Music
[bill@linuxbox -$] ls -ld /usr/local/share/Music
drwxrxr-x 2 root 4096 2008-03-21 18:05 /usr/local/share/Music
```

这一切意味着什么？这意味着我们现在有了一个目录 `/usr/local/share/Music`，它由 `root` 拥有，并且 `music` 组具有读写写权限。`music` 组包含 `bill` 和 `karen` 两个成员，因此 `bill` 和 `karen` 可以在 `/usr/local/share/Music` 目录下创建文件。其他用户可以列出目录的内容但不能创建文件。

但我们仍然面临一个问题。按照当前的权限，在 `Music` 目录中创建的文件和目录将具有 `bill` 和 `karen` 的普通权限：

```
[bill@linuxbox -$] > /usr/local/share/Music/test_file
[bill@linuxbox -$] ls -l /usr/local/share/Music
-rw-r---- 1 bill 2008-03-24 20:03 test_file
```

这里有两个问题。系统的默认 `umask` 为 `0022`，这阻止了成员向组内的其他成员写入文件。如果共享目录只包含文件，这将不是问题，但此目录将存储音乐，而音乐通常按艺术家和专辑的层级结构组织，组内成员需要能够在其他成员创建的目录内部创建文件和目录。我们需要将 `bill` 和 `karen` 使用的 `umask` 改为 `0002`。

其次，每个成员创建的每个文件和目录将属于该用户的主组，而不是 `music` 组。这可以通过在目录上设置 `setgid` 位位来解决：

```
[bill@linuxbox -$] sudo chmod g+s /usr/local/share/Music
[bill@linuxbox -$] ls -ld /usr/local/share/Music
drwxrxr-x 2 root 4096 2008-03-24 20:03 /usr/local/share/Music
```

现在我们测试新权限是否修复了问题。`Bill` 将他的 `umask` 设置为 `0002`，删除之前的测试文件，并创建一个新的测试文件和目录：

```
[bill@linuxbox -$] umask 0002
```

## 9 – 权限

```
[bill@linux~]$ rm /usr/local/share/Music/test_file
[bill@linux~]$ > /usr/local/share/Music/test_file
[bill@linux~]$ # mkdir /usr/local/share/Music/test_dir
[bill@linux~]$ ls -l /usr/local/share/Music
drwxrxr-x 2 music 4096 2008-03-24 20:24 test_file
-rw-rw-r-- 1 bill 0 2008-03-24 20:22 test_file
[bill@linux~]$
```

文件和目录都以正确的权限创建，允许 `music` 组的所有成员在 `Music` 目录内创建文件和目录。

剩下的唯一问题是 `umask`。必要的设置仅持续到会话结束，必须重置。在第11章中，我们将介绍如何永久更改 `umask`。

# 修改你的密码

本章将涵盖的最后一个主题是为你设置密码（如果你有管理权限，也可以为其他用户设置）。要设置或更改密码，`passwd` 命令的语法如下：

```
passwd [user]
```

要更改你的密码，只需输入 `passwd` 命令。系统会提示你输入旧密码和新密码：

```
me@linuxbox -]$ passwd
(current) UNIX password:
New password:
```

`passwd` 命令将尝试强制我们使用“强”密码。这意味着它将拒绝接受太短、与之前的密码太相似、字典单词或太容易猜到的密码。

```
me@linuxbox -]$ passwd
(current) UNIX password:
New password:
```

## 修改你的密码

如果你拥有超级用户权限，可以将用户名作为 `passwd` 命令的参数为另一个用户设置密码。还有其他选项允许锁定账户、密码过期等。详情请参阅 `passwd` 手册。

### 总结

在本章中，我们看到了 Linux 等类 Unix 系统如何管理权限以允许对文件和目录进行读、写、执行访问。该系统的基本思想可以追溯到 Unix 早期，并且一直有效。但类 Unix 系统的原生机制缺乏现代系统的细粒度。

### 扩展阅读

- Wikipedia 上有一篇关于恶意软件的优秀文章：http://en.wikipedia.org/wiki/Malware
- 用于创建和维护用户及组的命令行程序。更多信息，请参阅以下命令的手页：
- `useradd`
- `groupadd`

# 10 – 进程

操作系统通常...

- `bg` – 将任务放入后台
- `fg` – 将任务放入前台
- `kill` – 向进程发送信号
- `killall` – 按名称杀死进程
- `shutdown` – 关闭或重启系统

### 进程如何工作

操作系统通常是多任务的，这意味着它们通过在一个执行程序和另一个程序之间快速切换，营造出同时执行多件事的错觉。进程是 Linux 组织等待 CPU 处理的程序的方式。有时计算机会变得缓慢，或者应用程序会停止响应。在本章中，我们将查看一些可用工具，让我们检查程序在做什么，以及如何终止运行异常的进程。本章将介绍以下命令：

- `ps` – 报告当前进程的快照
- `top` – 显示任务
- `jobs` – 列出活动作业
- `bg` – 将任务放入后台
- `fg` – 将任务放入前台
- `kill` – 向进程发送信号
- `killall` – 按名称杀死进程
- `shutdown` – 关闭或重启系统

### 查看进程

当系统启动时，内核会启动一个名为 `init` 的程序，它转而运行一系列脚本来启动所有系统服务。许多服务以守护进程的形式在后台运行，没有任何用户界面。即使我们没有登录，系统至少也在忙于某些工作。内核维护关于每个进程的信息以保持组织。例如，每个进程都被分配一个称为 PID 的数字。PID 是按递顺序分配的，`init` 总是是 `1`。内核还跟踪分配给每个进程的内存。

查看进程最常用的命令是 `ps`。`ps` 有很多选项，但简单形式如下：

```
[me@linuxbox ~]$ ps
PID TTY CMD
5198 pts/1 00:00 bash
10129 pts/1 00:00 ps
```

示例结果列出了两个进程，进程 `5198` 和 `10129`，分别为 `bash` 和 `ps`。可以看到，默认情况下 `ps` 显示的与终端相关的进程很少。要查看更多，我们需要添加一些选项，在此之前，让我们看看 `ps` 产生的其他字段。TTY 是电打打终端的缩写，指的是进程的控制终端。Unix 显示其年龄。`TIME` 字段是进程消耗的 CPU 时间。可以看到，没有任何进程让计算机辛苦工作。

如果我们添加一个选项，就可以获得系统正在做什么的更大图景：
