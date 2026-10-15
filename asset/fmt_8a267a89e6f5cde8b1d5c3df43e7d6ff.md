
如果你想删除打印机或类，可以轻松地使用 `lpadmin -x` 来完成。

```
$ sudo lpadmin -x fezmo
$ sudo lpadmin -x haemer
```

好吧，聪明先生，但如果只是想暂时停用打印机进行维护而不是删除它怎么办？你可以在任一端阻塞打印队列。如果你停用队列的尾部（出口或打印机侧），用户仍可提交作业，但作业永远不会打印。如果你停用队列的头部（入口），队列中已有的作业仍可打印，但队列会拒绝提交新作业的尝试。

`cupsdisable` 和 `cupsenable` 命令控制队列的出口侧，而 `reject` 和 `accept` 命令控制提交侧。¹ 例如，

```
$ sudo cupsdisable groucho
$ sudo reject corbet
```

该用哪个？接受那些在可预见的未来没有希望被打印的打印作业是个坏主意，因此对于长时间停机请使用 `reject`。对于应该对用户不可见的短暂中断（例如更换墨粉盒），请使用 `cupsdisable`。

管理员偶尔会要求一个助记符来帮助他们记住哪些命令控制队列的哪一端。请考虑：如果 CUPS “rejects” 一个作业，那就意味着你不能 “inject” 它。另一种方法是记住，接受和拒绝是你对打印作业可以做的事，而停用和启用是你对打印机可以做的事。对打印机或队列说 “accept” 是没有意义的。

CUPS 本身有时会暂时停用它遇到问题的打印机（例如有人松动了电缆）。一旦你修复了问题，请记得重新 `cupsenable` 该队列。如果你忘记了，`lpstat` 会告诉你。 （有关此问题的完整讨论以及另一种方法，请参阅 `linuxprinting.org/beh.html`。）

### 其他配置任务

今天的打印机可以无限配置，CUPS 允许你通过其 Web 界面以及 `lpadmin` 和 `lpoptions` 命令调整各种功能。作为经验法则，`lpadmin` 用于系统范围的任务，而 `lpoptions` 用于每个用户的任务。

`lpadmin` 可以限制对打印机和队列的访问。例如，你可以设置打印配额并指定哪些用户可以打印到哪些打印机。

表 26.1 列出了随 CUPS 提供的命令，并根据其来源对其进行分类。

> 1. CUPS 的旧版本使用 `enable` 和 `disable` 而不是 `cupsenable` 和 `cupsdisable`。不幸的是，`enable` 也是 bash 的内置命令，因此 bash 假定你指的是它自己的 `enable`，除非你指定命令的完整路径名。碰巧的是，bash 的 `enable` 版本启用和禁用 bash 内置命令，因此你可以用 `enable -n enable` 来禁用它本身。

### 表26.1 CUPS的命令行工具及其来源

| 系统 | 命令 | 功能 |
|---|---|---|
| CUPS | `cups-config`<sup>a</sup> | 打印API、编译器、目录和链接信息 |
| CUPS | `cupsdconf`<sup>a</sup> | 通过KDE界面配置CUPS |
| CUPS | `cupsdisable`<sup>b</sup> | 停止打印机或打印机类上的打印 |
| CUPS | `cupsenable`<sup>b</sup> | 重新启动打印机或打印机类上的打印 |
| CUPS | `lpinfo` | 显示可用的设备或驱动程序 |
| CUPS | `lpoptions` | 显示或设置打印机选项和默认值 |
| CUPS | `lppasswd` | 添加、更改或删除摘要密码 |
| System V | `accept`, `reject` | 接受或拒绝队列提交 |
| System V | `cancel` | 取消打印作业 |
| System V | `lp` | 将作业排队等待打印 |
| System V | `lpadmin` | 配置打印机和打印机类 |
| System V | `lpmove` | 将现有打印作业移动到新目标 |
| System V | `lpstat` | 打印状态信息 |
| BSD | `lpc` | 充当通用打印机控制程序 |
| BSD | `lpq` | 显示打印队列 |
| BSD | `lpr` | 将作业排队等待打印 |
| BSD | `lprm` | 取消打印作业 |

a. 不要混淆这些工具。`cups-config`是CUPS附带的命令行工具，而`cupsdconf`是KDEPrint中的GUI工具。

b. 这些实际上只是System V中`disable`和`enable`命令的重命名版本。

## 26.3 从桌面环境打印

我们已经提到，我们鼓励使用原生CUPS GUI进行管理，而不是使用为KDE设计的附加组件。原生GUI具有权威性，而且恰好也相当不错。

另一个需要考虑的要点是可移植性。你可能已经在应付三种不同的打印系统家族了——为什么还要费力去学几种不同的管理GUI，进一步增加混淆呢？如果你的CEO想从他崭新的Macintosh上打印，你可能不知道在哪里点击才能找到Apple最新设计的GUI配置小部件。但如果你浏览到`localhost:631`，你就会发现自己身处熟悉的环境。

不过，如果所有用户都在某个特定的桌面环境中，你可能会决定使用该桌面的GUI来支持他们。例如，考虑KDEPrint，即KDE下打印的总体框架。

KDEPrint提供了自己的工具来添加打印机、管理打印作业、重新启动打印服务器等。与其他KDE工具一样，它具有KDE的外观和感觉，为KDE用户提供一致性。（你可能已经注意到，甚至KDE工具的名称也有独特的外观和感觉。曾有人问我们`ksh`是不是KDE应用程序。）

### 打印

KDEPrint并不依赖于CUPS。虽然它可以处理CUPS的所有功能，但它也可以配置为与从LPRng到通用外部程序的任何系统协同工作。如果出于某种原因你无法运行CUPS（或者更糟，你不得不在打印系统之间来回切换），你仍然可以使用KDEPrint来管理打印。需要预先提醒的是，CUPS比其他打印系统功能更强大，所以如果你不得不降级到替代打印系统，KDEPrint的某些功能可能会消失。

以下是KDEPrint的主要组件，你应该了解：

- `kprinter`，一个提交打印作业的GUI工具
- `添加打印机向导`，可以自动检测网络打印机（JetDirect、IPP和SMB）以及一些本地连接的打印机。添加打印机向导还允许你添加和配置它未自动检测到的打印机。
- `打印作业查看器`，用于移动和取消打印作业，并显示打印作业状态信息
- `KDEPrint手册`，记录了该系统。它可以通过KDE帮助中心获得，但可能非常难以找到。更简单的途径是调用类似`kprinter`的工具并点击“帮助”。另一种方法是使用KDE浏览器`konqueror`，运行`konqueror help:/kdeprint`。KDEPrint文档也可以在`printing.kde.org`找到。
- `打印管理器`，是打印系统的主要GUI管理工具。它也可能有点难找。你可以主桌面菜单中查找，尽管在菜单树中的位置因发行版而异。另一个选项是运行`kcmshell printmgr`或`konqueror print:/manager`。

添加打印机向导和打印作业管理器可以通过`kprinter`或KDE打印管理器访问，更不用说Konqueror中的URL `print:/manager`和`print:/printers`了。

KDEPrint的每用户信息存储在`~/.kde`下。这些文件是人类可读的，但设计为通过打印管理器进行更改。擅自修改后果自负。

### kprinter：打印文档

`kprinter`是`lpr`的GUI替代品。它可以在没有GUI的情况下从命令行使用。例如，命令

```
$ kprinter --nodialog -5 -P lj4600 riley.ps gillian.pdf zoe.prn
```

等同于

```
$ lpr -5 -P lj4600 riley.ps gillian.pdf zoe.prn
```

你的用户可能并不在意；他们想要一个 GUI。向他们展示如何将文件从文件管理器或桌面拖放到 `kprinter` 对话框中，然后打印整个批次。将浏览器打印对话框中的 `lpr` 替换为 `kprinter`，他们就会拥有一个 GUI 打印对话框。教他们点击“打印后保持此对话框打开”复选框，这样他们每次打印时就不会遇到重启延迟。

请注意“当前使用的打印系统”菜单，这是 KDEPrint 系统中立性的证明。还请注意，即使你的网络上没有实际的打印机，`kprinter` 也提供打印到 PDF 和打印到传真的功能。高级选项也值得一看；你可以将简历排队打印，并指定在老板下班后再打印。

### Konqueror 与打印

许多网络浏览器都识别一组特殊用途的 URI，它们充当通往特有功能的网关。你可能至少在 Firefox 中尝试过 `about:config` 和 `about:mozilla`。同样，`print:` 系列 URI 是 Konqueror 通往 KDEPrint 世界的秘密入口。
