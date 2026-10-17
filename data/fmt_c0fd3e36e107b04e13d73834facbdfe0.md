
# 示例配置命令

`echo "Use information to the end of the file" >> /home/mj/.bashrc`

`echo "alias=rm -i" >> /home/mj/.bashrc`

## 第 8 章：管理与维护

| 命令 | 解释 |
| --- | --- |
| `i` | 在光标当前位置进入插入模式。 |
| `o` | 在光标当前位置正下方打开新行，然后进入插入模式。 |
| `O` | 在光标当前位置正上方打开新行，然后进入插入模式。 |
| `:q` | 进入执行模式并退出 `vi`。如果你对文件进行了更改，此命令将执行失败。 |
| `q!` | 进入执行模式并退出 `vi`，即使你对文件进行了更改。所有更改都将丢失。与 `wq` 命令对比。 |
| `w` | 写入当前文件。 |
| `wq` | 写入当前文件并退出 `vi`。 |
| `x` | 删除单个字符。 |
| `/search` | 在当前文件中查找单词 "search"，区分大小写。 |

![](img/6ee4859e736a0839007ea9afb576c195_263_0.png)

有许多 `vi` 参考卡可用，包括由 `SSC` 为 `Linux Journal` 在 `www.ssc.com/ssc/productlist.html` 创建的一张。

# 重复性任务的脚本

计算机需要维护。由于维护会影响计算机和网络性能，大多数管理员会在半夜或活动最少的时间段维护网络。如果你正在管理一个计算机网络，你可以熬夜并设置一个脚本来自动维护它们。

`Red Linux` 通常会安装许多定期运行任务的脚本。这些脚本通过 `Linux` 的 `cron` 服务运行，并默认存储在以下目录中：

```
/etc/cron.hourly
/etc/cron.daily
/etc/cron.weekly
/etc/cron.monthly
```

我将向你展示这些目录中的脚本是如何调度的，带你了解两个标准的每日 `cron` 脚本，并向你展示如何使用 `at` 守护进程一次性运行作业。

# cron 调度器

默认情况下，`Red Linux` 在半夜运行许多维护任务。这些任务由 `Linux` 的 `cron` 服务运行，通过 `/etc/crontab` 配置文件进行配置。请看**图 5** 中该文件的默认版本。

虽然前面的命令看起来可能很神秘，但它们其实非常简单。就像你可以在代数中将 `x` 设置为某个数字一样，你也可以将变量设置为某些值。例如，以下命令将 `bash` 设置为默认的 `SHELL` 变量：

```
SHELL=/bin/bash
```

```
SHELL=/bin/bash
PATH=/bin:/sbin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * root run-parts /etc/cron.hourly
02 4 * * root run-parts /etc/cron.daily
22 4 * * root run-parts /etc/cron.weekly
42 4 1 * * run-parts /etc/cron.monthly
```

# 图 5. cron 任务调度表。

如前所述，`PATH` 是 `Linux` 中默认的 shell。接下来的命令为命令设置搜索路径。这里使用的 `path` 命令告诉 `Linux` 按照列出的顺序，自动在指定的目录中查找给定的命令：

```
PATH=/bin:/sbin:/usr/bin
```

例如，如果你运行 `run-parts` 命令，`Linux` 会按照顺序在 `/sbin`、`/bin`、`/usr/sbin` 目录中搜索命令。它找到的第一个 `run-parts` 命令就是这些目录之一。
`MAILTO` 命令对管理员很有用；每当 `Linux` 运行 `cron` 作业时，命令会将消息发送给指定的管理员 `root`。你可以将其设置为你喜欢的名称。如果你设置了邮件服务器，可以设置为你的互联网电子邮件地址。

```
MAILTO=root
```

最后，`HOME` 变量设置了脚本中后续命令的起始目录——在本例中，是顶级根目录 (`/`)：

```
HOME=/
```

如前面的章节所述的，任何以井号 (`#`) 或分号 (`;`) 开头的命令都是注释：`#run-parts` 行只是对后续命令的注释。现在情况变得稍微复杂了一点点。在 `/etc/crontab` 文件中，命令有特定的格式。例如，该文件的默认版本在每天每小时的第 1 分钟运行 `/etc/cron.hourly` 目录：

```
01 * * * root run-parts /etc/cron.hourly
```

下一个命令在每天凌晨 4 点运行 `/etc/cron.daily` 目录中的脚本：

```
02 4 * * * run-parts /etc/cron.daily
```

第三个命令在每周日的凌晨 4 点运行 `/etc/cron.weekly` 目录中的脚本：

```
22 4 * * 0 run-parts /etc/cron.weekly
```

最后一个命令在每月 1 日凌晨 4 点运行 `/etc/cron.monthly` 目录中的脚本：

```
42 4 1 * * root run-parts /etc/cron.monthly
```

如你所见，这些命令都有一个特定的模式。前五列决定了 `cron` 运行命令的时间。用户 `root` 以所示的数据运行 `run-parts` 命令。在每情况下，`run-parts` 命令的输入都是目录。表 7 详细列出了这些每一列的含义，从左到右。

表 7. cron 作业的调度表列。

| 项目 | 解释 |
| --- | --- |
| 分钟 | 设置在 0 到 59 之间的分钟。 |
| 小时 | 设置在 0 到 23 之间的小时。 |
| 日期 | 设置在 1 到 31 之间的日期。 |
| 月份 | 设置在 1 到 12 之间的月份。 |
| 星期 | 设置在 0 到 6 之间的星期。 |
| 用户 | 运行命令的用户。 |
| 命令 | 要运行的命令。 |

# 维护脚本细节

`locate` 命令数据库。否则，当 `Linux` 下次运行 `slocate.cron` 脚本时，它将扫描任何已挂载 CD 上的文件。

更改非常简单；我在 `slocate.cron` 脚本的命令末尾添加了 `/mnt`：

```
/usr/bin/updatedb -f /usr/smbfs,nfs,proc,devpts own-e "/tmp,/var/tmp,/usr/tmp,/afs,/net"
```

## 一次性任务

如果你有一个需要大量计算机资源的大型数据库，且只想在周末运行它？你可以牺牲自己的周末亲自运行该任务。你可以设置一个 `cron` 任务；遗憾的是，如果你忘记停用该任务，`cron` 守护进程可能会运行它多次。

在 `Linux` 中，管理员通过 `at` 守护进程运行一次性任务。`at` 命令实际上会启动一个类似 shell 的界面，你可以在其中输入你选择的任务。假设你想在凌晨 1:00 开始通过 `/usr/sbin/kitchen` 脚本处理 `home/mj/gallery` 文件。如果今天是周三，你可以运行以下命令：

```
$ at 1:00 + 3 days
warning: commands will be executed using (in order) a) $SHELL b) login shell
c) /bin/sh
at /sbin/kitchen /home/mj/galley
at> <Ctrl>D
```

运行环境指定了 shell。默认情况下，`SHELL` 的值为 `/bin/bash`。你可以通过 `echo SHELL` 命令检查此值。正如书中前面描述的，默认的登录 shell 是 `bash`。正如本章前面提到的，`/bin/sh` 也会启动 `bash` shell。

之前的命令设置了任务，在三天后的凌晨 1:00 运行。你可以使用以下命令进行检查：

```
$ atq
2	2003-06-28 01:00
```

此命令告诉我，编号为 2 的 `at` 任务将在 2003 年 12 月 20 日凌晨 1:00 运行。你可以在 `/var/spool` 目录下查看 `at` 将如何执行此任务。相应的任务属于目标用户。你可以使用以下命令（以 `root` 身份）进行检查：

```
# ls -l /var/spool/at
total 12
-rw-r--r-- 1root	root	1794 Jun 25 14:27	a00001010cc08c
-rw-r--r-- 1mj	mj	1309 Jun 25 14:53	a00002010cc08c
drwxr-xr-x 2daemon	ddaemon	4096 Jan 24 16:54	spool
#
```

在这种情况下，用户 `mj` 的 `at` 任务存储在 `a00002010cc08c` 文件中。如果你需要，可以使用以下命令删除任务 2：

```
$ at rm 2
```
