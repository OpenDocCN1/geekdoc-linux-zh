
## Do-It-Yourself Benchmarks

The previous examples with `hdparm` actually show you some numbers you can nail down, but how can you be sure that things have actually improved? You've done all this tweaking and it feels like commands are executing faster, but "feels like" is hardly what you would call scientific. Loading and running complex benchmark software and trying to come with some kind of base-system environment to test everything is not what happens in a real, working environment. That's what you buy and read those benchmark reports. What, then, can you do?

```bash
echo 24576 > /proc/sys/fs/inode-max
```

You should probably start by having a look at the hard drive before you change anything. Using the `-i` flag, `hdparm` will return a little information about the type of drive you have and some of the basic capabilities. Here's what happens when I run it on one of my Linux machines in the office (devsys1):

## 第26章 性能监控与调优

系统中有一个名为 `time` 的命令，你应该有所留意。这个工具的作用是为命令的执行计时。其格式如下：

`time -v command_string`

- `-v` 选项告诉 `time` 命令提供更详尽的输出。例如，当你运行 `ps ax` 命令时，系统消耗了多少时间以及使用了什么种资源？让我们来发现吧。由于我无法在你的系统上操作，我将在我的系统上演示，你之后可以试一下。

```
# time -v ps ax
```

当 `ps` 命令运行完成后，`time` 会执行它的功能并显示以下内容：

```
User time (seconds): 0.08
System time (seconds): 0.12
Percent of CPU this job got: 41%
Elapsed (wall clock) time (h:mm:ss or m:ss): 0.00:48
Average shared text size (kbytes): 0
Average unshared data size (kbytes): 0
Average stack size (kbytes): 0
Average total size (kbytes): 0
Maximum resident set size (kbytes): 0
Average resident set size (kbytes): 0
Major (requiring I/O) page faults: 197
Minor (reclaiming a frame) page faults: 60
Voluntary context switches: 0
Swaps: 0
File system inputs: 0
File system outputs: 0
Socket messages sent: 0
Socket messages received: 0
Signals delivered: 0
Page size (bytes): 4096
Exit status: 0
```

如果你在定期进行性能测量，可能还会对另一个标记感兴趣：`-o` 标记。它会做什么？将你的命令的统计数据报告到文件中。每次使用 `-o` 连续运行都会覆盖该文件，你可能还想使用 `-a` 选项。这会告诉 `time` 将输出追加到指定文件的末尾，而不是每次都覆盖——我的意思是每次迭代。这是我设置了所有选项后的完整命令：

```
time -a psout.txt -v ps ax
```

我可以通过 `crontab` 定期运行此命令，并用另一个程序来分析或绘制结果图。这种可能性是无限的。

### 资源

- `hdparm`
- http://www.ibiblio.org/pub/Linux/system/hardware/
- KDE Desktop
- http://www.kde.org/
- GNOME Desktop
- http://www.gnome.org/

## 附录 A

### 全 Linux 办公？

让我们面对现实吧。在现在以及可预见的未来，这仍然是一个 Windows 的世界。虽然 Linux 正在快速接管服务器世界，但桌面仍然属于来自雷德蒙的男孩们。

**胡说八道！**
第一段是我为了表达观点而扭曲的说法。这里是真相，也是全部真相。全 Linux 办公的时代已经到来。进行切换并在每一台运行 Linux 的桌面系统上运行办公环境是可能的。你需要的所有工具都在那里——这里的“你”指的是管理员及以下用户。这一节并不是专门关于系统管理的；它更多是关于选择和替代方案——因此它作为书中其他部分的附录出现。

在整个办公室运行 Linux 桌面对于系统管理员来说也是有意义的。掌握了在这里发现的内容，你应该有足够的素材来说服 CIO、CEO 和 CFO。

### 系统管理员的故事

当涉及到管理散落在办公室各处的各种系统时，你在个人 PC 上需要做的工作越少越好。虽然 PC 用户现在已经将经常系统死机、蓝屏和通用保护错误视为办公室日常生活的一部分，但他们的问题就是你的问题——即使这些问题是他们已经习惯的。这就是在办公室部署 Linux 的第一个红利：可靠性。

第二个红利与 Windows 有关，当用户完全搞乱他们的桌面（或他们的 PC）时，必须由管理员提供快速修复（通常涉及重启），或者更糟的是，从头开始重装他们的 PC。最后一种选择听起来有点极端，但由于几乎没有任何日志信息、无法访问源码以及使用专有 API，有时唯一的答案就是格式化并重新加载 Windows。然而，使用 Linux，你可以设置具有特定权限的个人用户桌面账户。然后你对单个用户的桌面配置进行备份。如果桌面被“弄乱”，你只需恢复默认桌面即可。如果某些功能无法运行，你有日志可以参考以帮助你隔离问题。用户和组权限意味着你可以防止用户修改他们不应该修改系统部分。

说到用户和组，现在你可以根据登录的用户完全自定义用户环境。如果你愿意，每个用户的桌面（即使多个用户在同一台 PC 上）也可以是独一无二的。

你还可以节省很多路。从远程工作站，你可以轻松地在那些桌面上安装软件。我在第 9 章和第 19 章再次提到过不同的远程控制方法。此外，访问命令行的简单性和强大性意味着你可以在后台工作而不影响你的用户。最后，Linux 系统极少需要重启。

这对于你作为系统管理员来说非常棒，但对你的用户来说呢？

### 用户的故事

如果你花点时间思考问题的核心，你会发现大多数用户（尽管我承认，不是*所有用户*）的桌面体验是：

### 文字处理器

在这个领域，你将看到一些熟悉的成员再次出现：KOffice 的 KWord 和 StarOffice 的 StarWriter。它们在各自的环境中都得到了很好的集成，但正如我在上一节中提到的，有时所有你需要的是一个可靠、独立的应用程序。这正是 AbiWord 发挥作用的地方。

虽然它在技术上是 GNOME 桌面环境的一部分，但你不需要运行 GNOME（除非你想运行）。对于对要求最严苛的文字处理用户来说，这是一个优秀的软件包，它可以导入你现有的 Word 或 WordPerfect 文件（以及其他格式）。

http://www.abisource.com AbiWord

### 表格软件

在这个领域，你将看到一些熟悉的成员再次出现：KOffice 的 Spread 和 StarOffice 的 StarCalc。它们在各自的环境中都得到了很好的集成，但正如我在上一节中提到的，有时所有你需要的是一个可靠、独立的应用程序。这正是 Gnumeric 发挥作用的地方。

虽然它在技术上是 GNOME 桌面环境的一部分，但你不需要运行 GNOME（除非你想运行）。对于对要求最严苛的电子表格用户来说，这是一个优秀的软件包，它可以导入你现有的 Excel 或 Lotus 1-2-3 文件（以及其他格式）。

http://www.gnome.org/projects/gnumeric Gnumeric

### 集成办公套件

在过去的几个章节中，我提过，在讨论文字处理器和电子表格等办公应用时，我们通常按套件来讨论，即这些关键应用的集成集合，它们在各个组件之间共享相同的视觉和感受。Linux 在这方面也不例外，提供了多个套件。同样，我将从来自 Sun 公司的 StarOffice 开始，但我还会扩展这个选项。

1999 年，Sun Microsystems 在 GPL 下发布了 StarOffice，将整个项目变成了一个开源项目。OpenOffice.org 项目继续开发 StarOffice 应用程序套件。实际上，有两种许可证在生效。另一种是 SISSL，即 Sun 行业标准源许可证，它为基于源码的商业应用程序开发提供了一些灵活性。你应该查看 StarOffice 网站和 OpenOffice.org 项目。

你还应该考虑 KOffice，这是 KDE 的办公套件，包含 KWord、KSpread（用于演示文稿图形）等。另一个值得关注的套件是来自 VistaSource 的 Applix。它在舒适的界面中为文档格式提供了广泛支持。最后，在你赶路之前，请看看 SIAG（全称 Scheme In A Grid），这是我运行过的最轻量级且功能最丰富的办公套件之一。

- http://www.vistasource.com Applix Office
- http://www.koffice.org KOffice
- http://www.openoffice.org OpenOffice.org Project
- http://siag.nu SIAG
- http://www.sun.com/products/staroffice StarOffice at Sun Microsystems

### 邮件代理

电子邮件是现代业务通信的核心。我们依靠它来与供应商、客户和同事保持联系。它已成为保持联系、发送备忘录、跟踪业务计划等手段。我们依赖它，并总是期望它在那儿。

Linux 上存在许多基于文本或字符的电子邮件软件包。你会发现 elm、pine 和 mutt（可能已经作为发行版的一部分安装了），但在办公环境中，我们通常使用图形化桌面。两个主要的桌面环境 KDE 和 GNOME 分别带有它们自己的邮件软件包 KMail 和 Balsa。这些是功能完备的邮件软件包，很好地集成到它们各自的环境中。我几乎专门使用 KMail，但这些选择通常取决于个人的偏好。

KMail 和 Balsa 都是纯粹的邮件软件包，而不是地址簿、计划表和联系人管理器的结合体（像 Outlook 那样）。总的而言，我们统称这些东西为 PIMs（个人信息管理器）。如果你想要一个更完整集成这些额外功能的邮件软件包，请考虑使用你的 StarOffice 软件包。它的邮件包对 Outlook 用户来说会非常熟悉。

同样值得提到的是来自 The Company 的 Aethera，以及作为 GNOME 办公开发一部分的 Evolution。不过，我在这里想提的最后一点（尽管这绝对不是你的最后选择）是 Netscape 或 Mozilla。你的 Web 浏览器（我将在下一节中讨论）通常带有它自带的集成邮件软件包。

- http://www.thecompany.com/projects/aethera Aethera
- http://www.balsa.net/main.html Balsa
- http://www.ximian.com/apps/evolution.php3 Evolution
- http://kmail.kde.org KMail
