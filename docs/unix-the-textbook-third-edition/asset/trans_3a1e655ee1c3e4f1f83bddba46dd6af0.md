
以下是 `lpstat` 命令的 BSD 对应命令 `lpq` 的简要说明。

### 语法

```
lpq [options]
```

用途：显示打印机上打印作业的状态

常用选项/功能：

- `-P printer-list` 显示 printer-list 中指定打印机上的打印作业状态
- `-l` 显示使用 `lpr` 命令发送到默认打印机的打印作业的长格式状态

最常用的选项是 `-P`。在以下会话中，第一个命令用于显示 `mpr` 打印机上打印作业的状态。命令输出显示打印机队列中有四个作业：作业 3991、3992、3993 和 3994。活动作业位于打印队列的头部。当打印机准备好打印时，它将首先打印活动作业。第二个命令显示 `qpr` 打印机没有任何要打印的作业。

```
$ lpq -Pmpr
mpr is ready and printing
```

| 排名 | 所有者 | 作业 | 文件 | 总大小 |
| --- | --- | --- | --- | --- |
| 活动 | sarwar | 3991 | mail.bob | 1056 字节 |
| 第 1 | sarwar | 3992 | csh.man | 93874 字节 |
| 第 2 | davis | 3993 | proposals1.nsa | 2708921 字节 |
| 第 3 | tom | 3994 | memo | 8920 字节 |

```
$ lpq -Pqpr
no entries
$
```

## 6.8.4 取消你的打印作业

如果你意识到自己提交了错误的文件进行打印，你会希望取消打印请求。执行此任务的 System V 命令是 `cancel`。以下是该命令的简要说明。

### 语法

```
cancel [options] [printer]
```

用途：取消通过 `lp` 命令发送的打印请求——也就是将这些作业从打印队列中移除

常用选项/功能：

- `jobID-list` 取消 jobID-list 中指定的打印作业
- `-u login` 取消用户 login 发出的所有打印请求

以下命令展示了如何取消打印作业。你可以使用 `lpstat` 或 `lpq` 命令显示打印机上打印作业的作业 ID，如第 6.8.3 节所示。第一个命令取消打印作业 `mpr-3991`。第二个命令取消用户 `sarwar` 在所有打印机上的所有打印请求。你只能取消自己的打印作业。因此，最后一个命令只有在 `sarwar` 或超级用户运行时才有效。

```
$ cancel mpr-3991
request "mpr-3991" canceled
$ cancel -u sarwar mpr
request "mpr-3992" canceled
request "mpr-3995" canceled
$
```

`cancel` 命令的 BSD 对应命令是 `lprm`。以下是该命令的简要说明。

### 语法

```
lprm [options] [jobID-list] [user(s)]
```

用途：取消使用 `lpr` 命令发出的打印请求——即从打印队列中移除这些作业；jobID-list 中的作业 ID 取自 `lpq` 命令的输出

常用选项/功能：

- 移除用户拥有的所有打印作业
- `-P ptr` 指定 ptr 打印机的打印队列

以下 `lprm` 命令执行与上一节中描述的 `cancel` 命令相同的任务。

```
$ lprm -P mpr 3991
mpr-3991 dequeued
$ lprm -P mpr sarwar
mpr-3997 dequeued
mpr-3998 dequeued
$
```

当不带参数运行时，`lprm` 命令会移除当前活动的作业，前提是该作业属于你。

以下章内练习将帮助你练习使用与打印相关的命令。

## 练习 6.11

你如何在打印机 `ece_hpl` 上打印文件 memo 的五份副本？请分别给出 System V 和 BSD UNIX 的命令。

这两个文件是相同的。`uniq` 命令可以用于删除连续重复的行，只保留其中一次出现。使用 `-d` 选项，该命令可以用于显示重复的行。

`lp`（System V）或 `lpr`（BSD）命令可用于在打印机上打印文件。`lpstat`（System V）或 `lpq`（BSD）命令可用于检查打印机上所有打印作业（请求）的状态（等待、打印中等）。`cancel`（System V）或 `lprm`（BSD）命令可用于从打印机队列中移除打印作业，从而不打印请求的文件。所有这些打印命令在 PC-BSD 和 Solaris 中均可用。

## 问题与习题

1. 列出你可以在 UNIX 文件上执行的 10 种操作。
2. 给出一条命令行，用于查看当前工作目录中所有文件的大小（以行数和字节数表示）。
3. `tail -10r ../letter.John` 命令的作用是什么？
4. 给出一条查看你的主目录大小的命令。给出一条显示主目录中所有文件大小的命令。
5. 给出一条命令，用于显示 students 文件中从第 25 行开始的所有行。
6. 给出一条命令，用于复制主目录中 courses 目录下的所有文件和目录。假设你在主目录中。给出另一条命令，假设你不在主目录中，来完成同样的任务。
7. 重做问题 6，但给出的命令需要保留文件的修改时间和权限。
8. `cp -r ~/courses ~/backups` 和 `cp -r ~/courses/ ~/backups` 命令之间有什么区别？
9. 给出 `rm` 命令的一个选项，该选项可以保护你不会意外删除文件，尤其是当你在命令中使用 `*` 和 `?` 等通配符时。
10. 以下命令分别做什么？
    a. `cp -f sample sample.bak`
    b. `cp -fp sample sample.bak`
    c. `rm -i ~/personal/memo*.doc`
    d. `rm -i ~/unixbook/final/ch??.prn`
    e. `rm -f ~/unixbook/final/*.o`

