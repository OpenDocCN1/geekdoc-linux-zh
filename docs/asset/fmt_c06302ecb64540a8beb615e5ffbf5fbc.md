
必须指定新闻服务器的 Internet 地址，例如 `news.uni-koelin.de`。通过 `getlist`，新闻服务器当前的 `active` 文件存储在 `/tmp/active.server`。由于 `innd` 尚未启动，你可以编辑该文件。目前，文件包含了当前可用的所有新闻组列表。保存文件；有时非常有用（例如，如果你想查找关于 `Java` 的所有新闻组）。由于 `INN` 必须在内存中保留整个文件，删除所有不再需要的组是有意义的。使用编辑器删除相应的行。此任务可以通过先排序文件来实现：

```bash
root /tmp/active.server > /tmp/active.sort
```

`control` 组和 `junk` 组必须保留在文件中，因为它们是 `INN` 正常运行所必需。此文件没有指定通过调制解器传输哪些新闻组，而是本地新闻服务器哪些新闻组。因此，你可以在文件中保留所有 `comp.*`。如果你以后想添加其他新闻组，必须通过 `issn` 通知 `innd`。`active` 文件也是新闻读取器的基础。文件越小，新闻读取器的处理越清晰！指定实际传输哪些文件的设置见第 491 页。

随后，你将文章编号置零（文章仅位于新闻馈中，而不适用于此文件的本地计算机上）。可以通过下面的命令完成：在命令中，每组数字被替换为 0 和 1，并扩展为十个前导零。`\` 字符仅是因为指令跨越了两行。

```bash
root cd /var/lib/news/
root sed 's/ [0-9]*/ 00000000000000001 /\
/tmp/sorted > active
root chown news active
root chmod 644 active
```

现在，`active` 文件的部分如下：

```text
de.com.misc 0000000000 0000000001
de.com.os.linux.hardware 0000000000 0000000001
de.com.os.linux.misc 0000000000 0000000001
de.com.os.linux.networking 0000000000 0000000001
de.com.os.linux.x 0000000000 0000000001
de.com.os.mac 0000000000 0000000001
```

## 启动和终止 INN

在完成这些更改后，可以首次启动 `INN`。这是通过调用 `/etc/rc.d/init.d/news start`（作为 `root`）来实现的。在首次启动之前，在另一个控制台上执行 `tail -f /var/log/messages` 可能会很有用，可以查看包含可能错误信息的日志文件。

### 490 使用 Linux 访问互联网

首先简单检查一下是否可以通过 `telnet` 运行 `innd`：

```bash
$ telnet localhost 119
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^'
200 jupiter.galactic.network InterNetNews
INN 1.4.unoff3 17-Oct-95 ready
```

当连接建立时，说明出了问题。然而，如果结果类似于上面，则说明所有操作已完成。

在出现问题的情况下，最可能的原因是 `/usr/lib/news`、`/var/lib/news` 或 `/var/spool/news` 中文件的访问权限不正确。所有文件必须属于 `news` 用户！

现在来谈谈关于电脑重启期间初始化 `innd` 的事情：如果你的发行版具有兼容 `V` 的 `init` 系统（`RedHat`、`Caldera`、从 4.2 版本开始的 `SuSE`），则应该没有问题。计算机在运行级别 3 或 5 下启动。`/etc/rc.d/rc3` 包含一个指向 `/etc/rc.d/rc5/S99news` 的符号链接，该链接指向 `/etc/rc.d/init.news`。因此，计算机在启动时，关机时会自动执行终止 `innd` 的必要命令（另见第 180 页）。

在其他发行版中，这种程度并没有被预定义。在那里，`innd` 像任何其他进程一样通过 `TERM` 信号终止。然而，这会导致“未正常关机”并在重启电脑时产生错误消息。因此，需要其他方法。例如，可以在 `/etc/inittab` 文件中重新定义对 `Ctrl+Alt+Del` 的响应：

```text
#etc/inittab
#...
# 在执行“三指礼”时执行的操作
# old: ca:rltralteld:/sbin/shutdown -t5 -rfn now
# new:
# ca:rltralteld:/sbin/shutdown
```

为了正确终止 `innd`，可执行文件 `/sbin/shutdown` 的内容如下：

```bash
#/bin/sh
# /sbin/shutdown
# /usr/lib/news/bin/innd "shutdown in" >/dev/null
# /sbin/shutdown -t5 -rfn now
```

## 日常维护

为了维护本地新闻系统，每天都需要执行一些工作。为了自动化此过程，首先执行 `su news` 然后执行 `crontab -e`。这会启动一个编辑器，你可以将以下行插入到 `crontab` 文件中用于 `news` 用户。（由 `crontab` 启动哪个编辑器可以通过变量 `EDITOR` 或 `VISUAL` 设定。如果缺少此设置，默认启动 `vi`。）

```bash
SHELL=/bin/bash
PATH=/usr/lib/news/bin:/usr/lib/news/bin:/usr/bin
# daily maintenance
10 20 * * * /usr/lib/news/bin/news.daily
```

这会导致 `cron` 守护进程每天 20:10 执行 `news.daily`（如果在 `crontab` 中指定或当发生错误时，会向邮件管理员发送适当的邮件消息）。

要配置 `news.daily`，你必须更改此文件中的两个标记：

```bash
# changes in /usr/lib/news/bin/news.daily
EXPIREDORR=true
EXPIREDFLAGS="-a"
```

此外，访问权限可能设置不正确：

```bash
root # chmod u+rx news.daily
root # chown news.daily news.daily
```

这会在 `/var/spool/news` 层次结构中创建所谓的 `.overview` 文件，允许某些新闻程序识别交叉发布。在维护工作完成后，`news.daily` 会向路由发送邮件消息，包含可用文章数量、过期并被删除的文章数量等。

为了让 `news.daily` 在 `RedHat` 3.0.3 发行版中正常工作，你必须对 `/usr/lib/news/innhellvars` 进行一个小更改：将行 `SED=sed` 改为 `SED=/bin/sed`。

## 配置新闻下载程序

现在新闻服务器运行良好，必须给它分配一些任务。这意味着必须与提供者建立连接并将新闻传输到本地系统。这个过程被称为“下载”。可以通过各种程序（`suck`、`nntget` 等）进行。`INN` 软件包包含了此类程序；但它们的缺点是未能充分利用现代线路带宽。原因在于连接的类型。新闻通过 `NNTP` 交换，这意味着远程和本地新闻服务器之间发生了如下类型的讨论：

- 本地：你有关于我的新文章吗？
- 远程：有的，文章 `xxy`。
- 本地：但我已经有了 `xxy`。
- 远程：那么 `yyy` 呢？

这种“讨论”显然是昂贵的。`UUCP` 方法的优势是，在下载之前，文章已经打包好并等待下载。

![image](img/dbea4db79a2d1f2183ab7081a3efe6a8_515_0.png)

### 492 Linux 访问互联网

通常情况下，新闻是通过 `SLIP` 提供的。为了更有效地利用现代线路，新闻通过 `NNTP` 交换，这在 `SLIP` 连接中是允许的。新闻通过 `NNTP` 交换，这意味着远程和本地新闻服务器之间发生了如下讨论：

- 本地：你有关于我的新文章吗？
- 远程：有的，文章 `xxy`。
- 本地：但我已经有了 `xxy`。
- 远程：那么 `yyy` 呢？

这种“讨论”显然是昂贵的。`UUCP` 方法的优势是，在下载之前，文章已经打包好并等待下载。

![image](img/dbea4db79a2d1f2183ab7081a3efe6a8_516_0.png)

![image](img/dbea4db79a2d1f2183ab7081a3efe6a8_517_0.png)

