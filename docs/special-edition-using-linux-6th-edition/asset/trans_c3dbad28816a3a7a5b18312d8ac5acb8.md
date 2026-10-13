

### 图 31.3：一个联网打印机场景示例。

![](img/c741b1b6b6eccaba2ad43454c979a7f8_603_0.png)

## 设置 `/etc/printcap` 文件

清单 31.1 是一个典型的 BSD printcap 文件示例（许多 Linux 系统仍在使用这种打印系统）。

### 清单 31.1：本地打印机的 `/etc/printcap` 文件示例

```text
1  lp
2      :lp=/dev/lp0
3      :sd=/var/spool/lpd/lp
4      :mx#0
5      :sh
6
7  ps
8      :lp=/dev/lp0
9      :sd=/var/spool/lpd/ps
10     :mx#0
11     :if=/var/spool/lpd/ps/filter
12     :sh
```

**注意**  
熟悉 Berkeley 版 `lpd` 实现的读者可能会注意到 LPRng 的 `/etc/printcap` 文件在语法上的差异。使用 LPRng 时，不需要在每行末尾写 `:`。如果你更喜欢加上这个字符，尽管加；LPRng 会直接忽略它们。

更仔细地检查这个文件的内容，你会看到这里有两块配置信息，每一块实际上对应一个不同的打印机队列，每个队列以不同方式处理它收到的打印作业。

如果仔细看，你还会发现这两个队列之间唯一真正的区别是各自关联的标题，以及 `ps` 队列中以 `:if=` 开头的那一行。这一行指定了一个打印过滤器；因此，`ps` 队列用于那些在发送到打印机之前需要某种特殊处理的打印作业。另一个队列 `lp` 没有这一行，所以发送到那里的打印作业必须已经是打印机能够理解的格式。清单 31.1 中的两个 `/etc/printcap` 条目都有相同的 `:lp=` 行。这一行指明在本地将打印作业发送到哪里；也就是说，`printcap` 条目将打印作业发送到系统中的哪个打印机端口。

下面有必要对这个文件中的各行进行完整说明。由于 `ps` 条目包含了 `lp` 条目的全部内容，而且还多出一些内容，因此这里以 `ps` 为例。

`ps` 条目中的第一行（第 7 行）用于指定该 `/etc/printcap` 条目可以被调用的所有名称。这一行可以有多个名称，只要所有名称之间用管道符（`|`）分隔即可。例如，如果这个 `/etc/printcap` 文件中的 `ps` 部分与一台连接到名为 `rubble` 的服务器的 HP LaserJet 5L 打印机相关联，按照惯例，`ps|rubble-lj|HP LaserJet 5L` 是一组不错的名称（通用名称|服务器-打印机类型|品牌和型号）。

第 8 行指明系统上将打印作业发送到哪个设备。设备 `/dev/lp0` 是现代 PC 标准打印机端口上相当常见的设备。偶尔打印机端口位于 `/dev/lp1`，但这并不常见。一般来说，你可能会用到其中一个；除非系统上安装了多台打印机或多个并行端口，否则编号更高的设备相当少见。

对于连接到串口的打印机，这里需要指定串口设备，而不是 `lp#` 设备。如果是这种情况，你还必须至少指定一行 `:br` 来表示串行连接的波特率。`:br` 的可能取值是 `50, 75, 110, 134.5, 150, 200, 300, 600, 1200, 1800, 2400, 4800, 9600, 19200` 和 `38400`。将速度指定为高于打印机的打印速度被认为不是个好主意；为了安全起见，请使用串口所用的适当波特率。该数字用井号（`#`）后跟波特率来表示，例如 `:br#19200`。

第 9 行指明打印队列所在的目录。队列是打印作业排队（spool）的地方。当你连续发送多个打印作业时（或者如果打印机已联网，并且你正在对网络中其他人的打印作业进行排队），打印作业在被发送到打印机之前就是在这个目录中排队的。除非管理员在队列中手动调整作业，否则打印作业按照排队的顺序被处理。本章后面的“管理打印队列”一节将介绍能够实现这种打印作业调整的工具。

mx# 行（第 10 行）指定可接受打印作业的最大大小。如果设置为 0，则不施加大小限制。除非有严格控制作业大小的需求，否则通常使用 0 值。

如前所述，第 11 行指定打印过滤器的位置和文件名（在此示例中，/var/spool/lpd/ps 是路径，filter 是过滤器文件的名称）。在打印作业被发送到打印机之前，需要进行的任何特殊处理或转换都必须在过滤器中完成。过滤器的名称和路径在任何地方都不是固定不变的，但这里使用的语法相当标准，为了跨系统的一致性，可能需要遵守。

Linux 系统上一个典型（简单）的打印过滤器可能如清单 31.2 所示。

### 清单 31.2：示例过滤器文件

```sh
#!/bin/sh

# Specify the language ghostscript should translate
# PostScript into
# (run `gs -h' to see device list)
DEVICE=lj4

# The maximum resolution for the printer
RESOLUTION=600x600

# The paper size - a4 or letter
PAPERSIZE=letter

# If an EOF (end of file) character is required
# after print jobs, put in a 1; otherwise, ignore
SENDEOF=

# Determine the correct paper size
#
if [ "$PAPERSIZE" = "a4" ]; then
    T=A4
else
    T=US
fi

# If the print job is pure text, use
# either nenscript or enscript to
# convert the plain text to PostScript
#
if [ -x /usr/bin/nenscript ]; then
nenscript -T$T -ZB -p-
else
if [ "$T" = "US" ]; then
T="Letter"
fi
enscript -M $T -Z -p -
fi |

# If the value of the DEVICE variable
#   is "PostScript", do nothing to the
#   print job and send it to the printer
#
if [ "$DEVICE" = "PostScript" ]; then
cat -

# Otherwise, send the data - now in
#   PostScript format - through the
#   ghostscript interpreter to be converted
#   into the language specified in DEVICE above
else
gs -q -sDEVICE=$DEVICE \
-r$RESOLUTION \
-sPAPERSIZE=$PAPERSIZE \
-dNOPAUSE \
-dSAFER \
-sOutputFile=- -
fi

if [ "$SENDEOF" != "" ]; then
printf '\004'
fi

exit 0
```

这个示例过滤器会执行以下操作：

- 如果纯文本被管道送入过滤器，它会被转换成 PostScript（如果安装了 `nenscript` 文本到 PostScript 转换器，则由它完成转换；否则使用 `enscript` 进行转换，后者执行相同的任务）。输出通过一个名为 `ghostscript` 的解释器进行管道处理（脚本中指定为 `gs`，因为这是它的可执行文件名），该解释器接收 PostScript 数据并将其转换成特定的打印机语言（在清单 31.2 中指定为 `lj4`，即 LaserJet 4 PCL 语言）。之后，格式化/转换后的打印作业被发送到打印队列进行打印。
- 如果通过过滤器管道传输的数据已经是 PostScript，则直接发送到 ghostscript 解释器进行转换。如果过滤器开头指定的打印机是 PostScript（表示该打印机在硬件中内置了 PostScript 处理能力），则过滤器接收或创建的 PostScript 数据会绕过 ghostscript，直接从过滤器输出并送往打印机（`cat -` 这一行实现了这一点）。

使用这样的过滤器之前，请务必将其设置为可执行（有关权限的详细信息，请参阅第 11 章“用户、组和权限”）。

请注意，这只是一个打印过滤器的示例。这里可以使用的可能性几乎无穷无尽。像前面这样简单的过滤器足以满足基本使用，但某些情况可能需要更复杂一些的过滤器。例如，打印作业可能需要针对宽幅打印机、分类账纸或支票打印进行格式化。要涵盖所有选项，本身可能就需要一整本书。

对于过滤器，最好的做法是从小而简单的方案开始，然后逐步提高到更复杂的程度。此外，还有许多值得评估的打印过滤器软件包可用（例如 LPRng 的 lpf，以及互联网上的各种免费产品，如 apsfilter 和 magicfilter）。

:sh 是一个相当简单的配置项，它会抑制打印作业中标题的使用。与其说是别的，不如说它是一个节省纸张的配置项。请注意，标题与横幅页不同，例如使用 HP JetDirect 卡等硬件联网的许多打印机所打印的那种横幅页。这些横幅页必须在网卡硬件中禁用；无法在 `/etc/printcap` 中禁用。

对于处理一个无过滤器和一个有过滤器的本地打印机配置的基本 `/etc/printcap` 文件来说，这些应该已经足够了。请注意，Linux 默认设置的打印队列目录位于 `/var/spool/lpd`，因此在创建 `/etc/printcap` 之后，需要设置的只是在 `/var/spool/lpd` 中为每个包含 `:sd=` 行的打印队列建立相应的子目录。

## 创建队列（文件和目录）

使用 Berkeley 的 lpd 软件包时，你必须手动设置这些项目，包括每个打印队列使用的日志文件。而使用 LPRng 时，则不需要这样做。

LPRng 附带一个名为 checkpc 的实用程序，可以为你创建所有这些项目。它读取你输入到 `/etc/printcap` 文件中的信息，并自动生成打印队列目录和日志，甚至精确到各个文件的所有者和权限。你只需要确保 `/etc/printcap` 中的信息对于你的打印配置是正确的，然后运行以下命令：

```
checkpc -f
```

你将会看到与清单 31.3 中所示输出类似的内容。

### 清单 31.3：执行 `checkpc -f` 的输出

```
[root@trident /root]# checkpc -f
LPRng version LPRng-3.2.3
Get_perms: permissions entry '/etc/lpd.perms'
Get_perms: permissions entry '/usr/etc/lpd.perms'
Cannot open '/usr/etc/lpd.perms' - No such file or directory
Get_perms: permissions entry '/var/spool/lpd/lpd.perms.trident'
Cannot open '/var/spool/lpd/lpd.perms.trident' - No such file or directory
LPD lockfile '/var/spool/lpd/lpd.lock.trident'
  Checking directory: '/var/spool/lpd'
    checking file '/var/spool/lpd/lpd.lock.trident'
Truncating LPD log file '/var/spool/lpd/lpd.log.trident'
Checking /var/spool/lpd/lpd.log.trident file '/var/spool/lpd/lpd.log.trident'
checkpc: Warning - cannot open '/var/spool/lpd/lpd.log.trident'
lp: Checking printer 'lp'
```

