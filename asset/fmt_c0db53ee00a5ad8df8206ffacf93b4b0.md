
在构建 SWATCH 之后，你可以通过简单的 `make` 后接 `make install` 来安装它；这将同时安装主 Perl 脚本和帮助页。

```
$ make
...[ Output of make ]...
$ su
Password:
# make install
...[ Output of make install ]...
#
```

假设你已经安装了可以工作的 Perl 环境，并且所有所需的 Perl 模块也已正确安装，你现在已经拥有了一个可以运行的 SWATCH 安装。

# 使用 SWATCH 监控日志

`swatch` 命令的使用非常简单。虽然 `swatch(1)` 中记录了许多参数，但其基本操作形式为：

`swatch -c logfile -tail logfile`

`logfile` 是系统日志之一的路径。它可以是由 syslog 维护的日志，也可以是完全其他类型的日志；SWATCH 并不在乎。SWATCH 程序愿意监控任何文本文件并将其视为活动日志。

`logfile` 是一个短且简单的文件，描述了一系列 SWATCH 需要在文件中查找的文本字符串，以及每当匹配到这些字符串中的任何一个时 SWATCH 应该的操作。

## 匹配文件格式

匹配文件是一个文本文件，以一个监控关键字 `watchfor` 开头，后跟着一个正则表达式，该正则表示 SWATCH 需要关注的模式或系列系列模式。以下是一个示例：

`watchfor /ROOT LOGIN|uid=0/`

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_338_1.png)

# 322

# 第 21 小时

这一行将导致 SWATCH 监控相关日志中的 `ROOT LOGIN OR uid=0` 字符串，以便跟进正在监控日志的系统上发生的 root 级活动。在每个 `watchfor` 之后是一系列描述当匹配到模式时将发生的操作行。例如，在 watchfor 模式之后，你可能会看到以下内容：

```
echo red
mail addresses=admin@mynet.net:j2w1x.org,subject="SW.ROOT"
bell 3
```

这些行会导致 SWATCH 在控制 SWATCH 的终端上用红色显示相关的日志条目。然后，SWATCH 将该日志条目发送到两个地址——`admin@mynet.net` 和 `j2w1x.org`——并带有易于识别的主题 `.SW.ROOT`。

最后，SWATCH 将运行终端三次。

动作列表将一直持续到下一个 `watchfor` 行，该行将以另一个不同的监控模式开头。SWATCH 可以被指令列出的动作如表 21.1 所示。

## 表 21.1 SWATCH 匹配动作

| 动作 (Action) | 说明 |
| :--- | :--- |
| `echo [mode]` | 向控制终端显示匹配的日志条目。可选模式可以是粗体、下划线、闪烁、反转、黑、红、绿、黄、蓝、青、白、black_h（高亮黑）、red_h、green_h、yellow_h、blue_h、cyan_h 或 white_h。 |
| `bell [count]` | 运行终端铃声。可选计数描述了铃声应该响的次数。 |
| `exec command [args]` | 执行指定的命令以及任何提供的参数。参数中的 `$N` 将被扩展为日志条目中以空格分隔的第 $N$ 个字段，`$` 将发送到日志条目。 |
| `mail [addr],[sub]` | 将相关的日志条目发送到用户的电子邮件地址。如果提供了 `addresses=addr...`，则将邮件发送到列表地址。如果提供了 `subject=subject text...`，则使用提供的主题作为所发邮件的主题。 |
| `pipe command` | 将日志条目发送到命令的标准输入。将日志条目写入用户的终端。可以使用冒号（:）分隔列出多个用户。 |
| `throttle h:ms` | 指定如果在提供的期间（小时:分钟:秒）内日志条目重复出现一次以上，则匹配动作应在此期间仅执行一次。 |
| `continue` | 指令 SWATCH 在执行动作后，尝试将此日志条目匹配到匹配文件中的其他 watchfor 模式。 |

## 审计与监控

使用这些动作和构造良好的监控行，你可以让 SWATCH 监控你的日志中几乎任何种的活动。列表 21.1 显示了一个非常简单的文件。

### 列表 21.1 一个简单的通用型匹配文件

```
watchfor    /ROOT LOGIN|uid=0/
echo red
mail addresses=admin@mynet.net,subject="*.SW.Root Activity"
bell 2
watchfor    /REPEATED|repeated|/
echo red
mail addresses=admin@mynet.net,subject="*.SW.Repeat Activity"
bell 2
watchfor    /FAILED|failed|/
echo red
mail addresses=admin@mynet.net,subject="*.SW.Fail Activity"
bell 2
watchfor    /changed by/
echo blue
mail addresses=admin@mynet.net,subject="*.SW.Change"
bell 2
watchfor    /caught signal|abnormal|aborted|registered/
echo blue
mail addresses=admin@mynet.net,subject="*.SW.Unknown"
bell 3 (等等，让我重新检查一下 OCR 文本)
bell 2
watchfor    /kernel:init:/
echo blue
mail addresses=admin@mynet.net,subject="*.SW.System"
bell 2
watchfor    /LOGIN FROM/
```

21.1 中的文件尝试跟踪一组可疑的条目并在本地显示它们，通知管理员或二者兼顾。当你配置好 SWATCH 以满足你的需求时，你可能考虑在后台启动它。

![](img/5b265b1d98ba2e1a657c3f9cdc5ce677_340_0.png)

### 总结

在这个小时里，你学习了如何使用 SAINT 及其基于 Netscape 的图形界面对主机进行基本的安全审计。然后你学习了如何搜索 SAINT 提供的信息并用它消除网络中的漏洞。你还学习了安装和使用 SWATCH，这是一个监控日志的简单但非常有用的工具。通过 SWATCH，你可以持续监控某些模式并通知管理员或采取行动。

### 问答

- 我有一个文件或配置问题 SAINT 说可能代表漏洞，但我认为它本该在那里。我应该删除它吗？

这取决于许多因素。首先，如果 SAINT 说某个文件可能指示后门或根内核包，而你确定它是原始文件，有一个简单的方法可以确认。将文件的校验和、大小和日期与发行包中的原始文件对比。如果它们匹配，则文件是原始的。这并不意味着它是安全的。请确保检查发行维护者的更新，以防原始文件包含漏洞。

- 我如何知道在 SWATCH 中匹配哪些字符串？

示例 SWATCH 匹配文件中的字符串从未在我的日志中出现过。

- 我们不应该也在匹配文件中包含字符串 "N" 吗？

由于 Linux 发行版有许多不同的守护进程 syslog 版本，字符串会在不同系统之间变化，取决于供应商和组装日期。即使是像基础的 init 二进制可能基于完全不同的代码库。你的 SWATCH 匹配文件必须基于经验。也就是说，你必须先被攻击过才能构建一个好的文件。

# 审计与监控

通过在你自己的网络上挂载一系列“攻击”或至少是“有趣的”行为，你可以看到每个操作在日志中是如何显示的，并可以对这些字符串进行监控。运行像 SAINT 这样的软件可以生成许多日志条目，这些条目可能指示坏事正在发生。此外，你实际上控制某些系统的日志记录——例如 TCP Wrappers 和 Apache。由于你从一开始就决定了要记录的字符串，因此用 SWATCH 与它们进行匹配应该很容易。

## Q 我的日志非常不活跃，或者是空的。

- 首先，如果曾经非常活跃的日志现在变得极不活跃或几乎为空，这几乎可以确定是发生了某种攻击。运行 SAINT 来检查问题，并仔细查看你的旧日志，特别注意它们停止的时间点。你可能会发现你的系统已经被攻破了。

- 第二，你可能仅仅需要重新配置你的守护进程（daemons），使其在日志记录方面更加详细。这需要在你的 `init` 脚本中、`/etc/inetd.conf` 以及你的 `/etc` 配置文件中根据具体情况进行修复。你可能想要考虑重新安装或切换到另一个记录日志更多的发行版。

- 还有一个稍显明显的理由导致你的日志可能是空的。你检查过确保磁盘没有满且没有满过吗？Syslog 在遇到磁盘满时会停止，并且不会自动重启，即使空间再次可用。

## 网络术语
