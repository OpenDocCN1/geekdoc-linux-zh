
network driver: `/usr/local/lib/lp/lpnc`

ditroff filter: `/usr/local/lib/devps/devps`

print formats: graphics, ditroff, use pr, proff

queue ordering: age

host attachment: `server.utech.edu`

spooling directory: `server/spool/lp/mathlw`

location: MATH 734

description: multiple AppleLaserWriter INT

- 5. `lpinfo` 命令也可以列出可用打印机列表，但其输出格式比 `lpinfo` 难以理解得多：

```
% lpinfo -a head -15
glw: server.utech.edu; AG 23; multiple Apple LaserWriter INT
glw1: server.utech.edu; AG 23; Apple LaserWriter INT
glw2: server.utech.edu; AG 23; Apple LaserWriter INT
glw3: server.utech.edu; AG 23; Apple LaserWriter INT
alpsw: sentinel.utech.edu; 111; Apple LaserWriter INT
bio: ace.utech.edu; COM B117; DataPrinter (self-service)
cary: franklin.utech.edu; Cuad (NE-87); IBM 4019 Laser Printer
cslw: server.utech.edu; CS 2249; Apple LaserWriter HTX
cs115w1: expert.utech.edu; IBM 4019 LaserPrinter (for CS1800)
cs115w2: expert.utech.edu; CS 115; IBM 4019 LaserPrinter (for CS1800)
csg40w1: franklin.utech.edu; CS 0040; IBM 4019 LaserPrinter
csg50w1: expert.utech.edu; CS 0050; IBM 4019 LaserPrinter
cspl1: expert.utech.edu; CS 073; C.Itoh, white paper (self-service)
eng130w2: age.utech.edu; ENG 130; C.Itoh, white paper (self-service)
```

如果你觉得这个是可读的，那么你无疑在制作一个真正的 UNIX！

`printers` 命令的输出指定了打印该文件的打印机位置，我需要去另一栋大楼领取我的纸质。（位置在 `printers` 命令的输出中是具体的）。

# 任务 18.3：使用 pr 格式化打印作业

生成的打印机输出看起来不错，但我希望在每一页上都有一个运行的页眉，显示文件名和页码。我还希望对某些其他格式特征有更多的控制权。这正是 `pr` 命令派显用场的地方。`pr` 并不是为了打印，而是一个通用的分页和格式化命令，可以用于在屏幕上显示信息。此外，`pr` 在 BSD 和 System V UNIX 上都是可用的。

`lpinfo` 命令也可以向你显示可用打印机列表，但其输出格式比 `lpinfo` 难以理解得多：

（此处省略重复的列表内容，保持格式一致）

`pr` 命令的输出指定了打印该文件的打印机位置，我需要去另一栋大楼领取我的纸质。（位置在 `printers` 命令的输出中是具体的）。

（注：此处根据示例逻辑，主要翻译了描述性文本，未翻译未翻译的的的的的输出内容）

`pr` 命令的输出显示显示。每页产生两列输出。这些 `pr` 选项在某些情况下非常有用。

表格 18.3。`pr` 的常用标志：

| 标志 | 含义 |
| --- | --- |
| -n | 每页产生 n 列输出。 |
| -t | 在第 n 页开始打印。 |
| -f | 不打印页眉和页脚。 |
| -h | 使用标题作为页眉。 |
| -w | 设置页面宽度为 n 个字符。 |
| -m | 一次打印所有文件。 |

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_394_0)

在某些 UNIX 系统上，`-f` 标志会导致程序在页面底部结束。

注意 `pr` 不仅让这个列表分两列，还添加了一个不包含任何命令信息的页眉。幸运的是，我可以通过以下命令轻松地添加页眉：

```
% who | pr -2 | more
```

这样好多了。

- 3. 我可能想比较两个目录的内容。记得使用的 `-1` 标志是 `pr` 标志用于每行列出一个文件名，这样就可以创建一个这种格式的文件池：

```
% ls -1 src/src.listing
% ls -1 /tmp/tmp.listing
```

这些文件看起来像：

```
# head src.listing tmp.listing
=== src.listing ===
calc-helpnccalc.c
fixit.c
info.o
info.o
```

```
== tmp.listing ===
Erik/
Gl/
Garry/
MnisAlive
```

Re01759

Re13201

Sting/

VR001187

VR002540

VR002678

现在我将使用 `pr` 来构建双列输出：

```
% pr -m src.listing tmp.listing | head -15
Dec 9 13:53 1993    Page 1
calc-help
calc-c
fixit.c
info.c
info.o
message.c
Erik/
Giri/
Garry/
MmsAlive
Re01759
Re13201
Sting/
VR001187
VR002540
```

管道断开

+ 4. 如果我能自动关闭每个列表页顶部自动包含的空行，那将更有帮助，这是 `-f` 标志的工作（或者如果你的 `pr` 版本中 `-f` 表示分页符，则使用 `-t`）：

```
% pr -f
pr -m src.listing tmp.listing | head -15
Dec 9 13:53 1993    Page 1
calc-help
calc-c
fixit.c
info.c
info.o
message.c
Erik/
Giri/
Garry/
MmsAlive
Re01759
Re13201
Sting/
VR001187
VR002540
VR002678
VR002477
```

管道断开

+ 5. 看起来不错。现在是时候通过将 `pr` 命令管道到 `lpr` 命令来执行打印了：

```
% lpr | lpr
pr -f -m src.listing tmp.listing | head -15 | lpr
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_398_0.png)

# 在 UNIX 环境下打印

`pr` 命令可以用来确保你的打印输出始终整洁且易读。再次，这是一个创建别名的绝佳位置：`alias 'pr' | 'lpr'` 或 `alias 'pr' | 'lprq'`。即使不使用任何标志，`pr` 也会自动在每页顶部添加页码。

## 第 18.4 节：使用打印队列

在个人系统中，打印机直接连接到系统可能会有所帮助，这样使用 PRT（在 DOS 上）或 File|Print（在 Mac 上）打印的任何内容立即打印。遗憾的是，UNIX 并没有拥有私人打印机的奢侈。相反，它在打印队列中处理打印请求，这是一个待打印文件的管理列表。当你将文件发送到打印机时，它会被添加到等待打印的文件队列中。你的请求将位于列表底部，任何随后的打印请求将排在下方。你的打印请求会逐渐移动到列表顶部并打印，而不会中断你之前的打印请求。

有时等待打印输出可能会令人沮丧。然而，与简单允许用户共享一个打印机相比，使用队列系统有一些优点。最大的优点可以使用 `lpr` 命令改变主意，并在浪费纸之前从队列中移除打印请求。`pr` 命令与作业名称配合，你可以通过使用 `ipq` 打印队列来了解它。`lpr` 和 `ipq` 都可以使用 DEFAULT 设置，或者通过 `-Pprinter` 指定打印机。`ipq` 命令还可以通过通过在命令中添加账户名称来限制输出。

如果你的系统没有 `lpr`，请使用 `cancel` 命令从打印队列中删除项目。`ipstat` 命令是 System V 对 `ipq` 命令的替代，尽管许多站点设置了 `ipq = ipstat` 以让生活方便一点。

要取消，你需要指定打印机名称和作业 ID，如 `ipstat` 输出所示。如果我在硬拷贝打印机上有 37 号请求，可以使用 `cancel -37` 取消该打印。

+ 扫一眼 `mathw` 队列显示有很多文件等待打印：

```
* ipq
```
