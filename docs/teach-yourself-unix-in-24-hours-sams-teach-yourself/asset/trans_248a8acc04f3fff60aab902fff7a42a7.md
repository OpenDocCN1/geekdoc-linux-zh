

# 386 第 18 小节

23 ssinfo 0353 000 ssinfo0353f
24 taylor 0889 000 taylor0889a

mathlw: 等待传输到 server.utech.edu

队列为空。

有相当多的打印作业正在等待发送，但并不明显哪一个是该打印机的输出目标。`lpq` 和 `ipstat` 命令将在本节稍后详细介绍。

- 3. 要以横向模式打印 `dickens.note` 文件，不带页眉、缩进八个空格并按反序排列，我可以使用以下标志：
  - `Ipr -hiLR - dickens.note`
  - 如果我经常这样做，设置一个 C 别名（alias）可能会很有帮助：
  - `alias Ipr... 'Ipr -hiLR'`

在 System V 机器上，你也可以创建别名 `Ias Ipr *Ip`，尽管 `Ip` 并不支持这些特定的选项。

如果你发现自己经常向几个不同的打印机打印，可以轻松地定义几个 shell 别名来创建特定打印机的命令：

  - `alias mathprint -Ipr -Paitle`
  - `alias libprint -Ipr -PLibrary`
  - `alias ediprint -Ipr -Pedlw`

在 System V 机器上，名称如下：

  - `alias mathprint -Ip -mathlw`
  - `alias libprint -Ip -dllibrary`
  - `alias ediprint -Ip -Iedlw`

- 4. 某些系统有一个 `lpinfo` 命令，也可以提供打印机的信息：

  - `lpinfo mathlw`
  mathlw: server.utech.edu; math 734; multiple Apple LaserWriter INT

要查找更多关于打印机的信息，你可以指定 `-v` 标志：

```
* lpinfo -v mathlw
mathlw description:
driver: /usr/local/lib/lp/ipmq
printer control group: cc -
graphic file: /usr/local/bin/psplot
log file: /usr/spool/ipr/mathlw/logfile
lock file: /usr/spool/ipr/mathlw/lock
hardware line: /dev/null
maximum job count per user = 25
subprocess list: mathlw,mathlw2,mathlw3
maximum print file blocks = 3000
make unique via bin change
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_394_0.png)

# 在 UNIX 环境下打印

network driver: /usr/local/lib/lp/lpnc
ditroff filter: /usr/local/lib/devps/devps
print formats: graphics, ditroff, use pr, proff
queue ordering: age
host attachment: server.utech.edu
spooling directory: server/spool/lp/mathlw
location: MATH 734
description: multiple AppleLaserWriter INT

- 5. `lpinfo` 命令也可以列出可用打印机列表，但其输出格式比 `lpinfo` 难以理解得多：
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

如果你觉得这个是可读的，那么你无疑在制作一个真正的 UNIX！

`printers` 命令的输出指定了打印该文件的打印机位置，我需要去另一栋大楼领取我的纸质。（位置在 `printers` 命令的输出中是具体的）。

# 任务 18.3：使用 pr 格式化打印作业

生成的打印机输出看起来不错，但我希望在每一页上都有一个运行的页眉，显示文件名和页码。我还希望对某些其他格式特征有更多的控制权。这正是 `pr` 命令派显用场的地方。`pr` 并不是为了打印，而是一个通用的分页和格式化命令，可以用于在屏幕上显示信息。此外，`pr` 在 BSD 和 System V UNIX 上都是可用的。

`lpinfo` 命令也可以向你显示可用打印机列表，但其输出格式比 `lpinfo` 难以理解得多：
（此处省略重复的列表内容，保持格式一致）

`pr` 命令的输出指定了打印该文件的打印机位置，我需要去另一栋大楼领取我的纸质。（位置在 `printers` 命令的输出中是具体的）。

（注：此处根据示例逻辑，主要翻译了描述性文本，未翻译未翻译的的的的的输出内容）

`pr` 命令的输出显示显示。每页产生两列输出。这些 `pr` 选项在某些情况下非常有用。

表格 18.3。pr 的常用标志：

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
% who | pr -2 | more

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

