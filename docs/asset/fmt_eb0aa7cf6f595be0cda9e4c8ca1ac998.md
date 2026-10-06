
# 本地打印机的示例 `/etc/printcap` 文件

```
1 ps
2   lp=/dev/lp1
3   sd=/var/spool/lp1
4   mx#0
5 
6   sh
```

```
7 lp
8   lp=/dev/lpd
9   sd=/var/spool/lpd
10  mx#0
11  if=/var/spool/ps
12  sh
```

熟悉 Berkeley 实现 `lpd` 的读者可能会注意到 LPRng `/etc/printcap` 语法的差异。在 LPRng 中，你不需要在行末尾……仔细检查该文件的内容。你会发现这里有若干信息块。每个块实际上对应一个不同的队列。每个队列处理接收到的打印任务的方式不同。

如果你仔细观察，还可以发现两个队列之间的差异在于 `ps` 队列中以 `:if` 开头的行。这是指定打印过滤器的行；因此，`ps` 队列用于发送到打印机之前需要经过某种处理的任务。另一个队列 `lpd` 没有这一行，因此发送到那里的任务必须已经是打印机理解的格式。14.1 中的两个 `/etc/printcap` 条目都有 `:lp=` 行。此行告诉你在本地哪里发送打印任务；以及该项将任务发送到系统中的哪台打印机。

该文件的完整分解按顺序排列。由于 `ps` 项包含了 `lp` 项的所有内容并更多，因此 `ps` 是打印机

每个项的第一行——第 1 行和第 7 行——是你指定调用该 `/etc/printcap` 项名称的地方。此行可以有多个名称。

第 2 行和第 8 行指示将打印任务发送到系统的哪个设备 `/dev/lp1` 是现代 PC 标准打印端口常用的设备。有时打印端口位于 `/dev/lp0`，但这并不常见。通常情况下，其中一个可能就是你将使用的；除非你的系统中安装了多个打印机/并行端口，否则编号高于它们的设备并不常见。

对于连接到串口的打印机，需要指定串口设备而不是 `lp#` 设备。如果是这种情况，你还必须指定 `:br` 以指示串口连接的波特率。`:br` 的可能值为 50, 75, 110, 134.5, 150, 200, 300, 600, 1200, 1800, 2400, 4800, 9600 和 19200 以及 38400。

# 第 14 章 打印

速度比打印机的打印速度快被认为是一个坏主意；安全的做法是保持使用串口所使用的适当波特率。该数字由井号 `#` 后跟波特率来指定，例如：`#baud19200`。

第 9 行确定了打印队列所在的目录。队列是打印任务缓存的地方。当你连续发送多个打印任务（或者如果你的打印机是网络化的，你正在从网络上的其他用户缓存打印任务）时，该目录就是打印任务在发送到打印机之前缓存的目录。打印任务按照缓存的顺序进行处理，除非管理员手动在队列中移动任务。此实用程序可以对任务进行此类排序，这将在本章后面的“管理打印队列”部分进行介绍。

`mx` 行（第 4 行和第 10 行）指定了可接受打印任务的最大尺寸。如果设置为 0，则不实施大小限制。除非有严重的任务大小限制，否则通常使用 0 值。

与之前一样，第 11 行指定了打印过滤器和文件名（在本示例中，`/var/spool/lpd/ps` 是路径，过滤器是过滤器文件的名称）。在打印任务发送到打印机之前，需要对其进行的任何特殊处理或转换都需要在该过滤器内完成。过滤器的名称和路径没有设置在任何地方，此处使用的语法通常是标准的，并且可能需要在所有系统中遵循。

一个用于 OpenLinux 系统的典型（简单）打印过滤器可能如列表 14.2 所示。

# 列表 14.2 示例过滤器文件

```
#!/bin/sh

# 指定 ghostscript 应该将 PostScript 翻译成的语言
#（运行 'gs -h' 查看设备列表）
DEVICE=ljet4

# 打印机的最大分辨率
RESOLUTION=600x600

# 纸张尺寸 - a4 或 letter
PAPERIZE=letter

# 如果打印任务后需要 EOF（文件结束）字符
# 则输入 1；否则忽略
SENDEOF=

# 确定正确的纸张尺寸
#
if [ "$PAPERIZE" = "a4" ]; then
nT=A4
else
T=US
fi

# 如果打印任务是纯文本，则使用
```

# 设置打印机

```
# 或者使用 nscript 或 enscript 来
# 将纯文本转换为 PostScript
if [ -x /usr/bin/nenscript ]; then
    nenscript -TST -ZB -p
else
    if [ "$" = "US" ]; then
        T="Letter"
    fi
    nenscript -M $T -Z -p
fi
```

```
# 如果 DEVICE 变量的值
# 为 "PostScript"，则不对打印任务
# 执行任何操作并将其发送到打印机
if [ "$DEVICE" = "PostScript" ]; then
    cat
```

```
# 否则，将数据（现在是
# PostScript 格式）通过 ghostscript
# 解释器发送，以转换为 DEVICE 中指定的语言
else
    gs -q -sDEVICE=$DEVICE \
        -r$RESOLUTION \
        -dSPAPERSIZE=$SPAPERSIZE \
        -dNOPAUSE \
        -dSAFER \
        -sOutputFile=- -
```

```
if [ "$ENDEOF" != "*" ]; then
    printf "\004"
```

```
exit 0
```

此示例过滤器执行了以下操作：

- 如果将纯文本管道到过滤器，它将被转换为 PostScript（如果安装了 nenscript-to-PostScript 转换器；否则使用 enscript 转换，它执行相同的任务）。输出通过名为 ghostscript 的解释器进行（在脚本中指定为 `gs`，因为它是可执行名称），它接收 PostScript 数据并将其翻译为特定的打印语言（在列表 14.2 中指定为 jet4 或 Laserjet 4 PCL 语言）。之后，格式化/翻译后的打印任务被发送到打印队列进行打印。

- 如果通过过滤器管道的数据已经是 PostScript

# 第 14 章 打印

在使用此类过滤器之前，请务必将其设置为可执行（有关权限的详细信息请参见第 10 章“用户、组和权限”）。

注意，这只是打印过滤器的一个例子。这里可以使用的可能性几乎是无限的。像之前那样的简单过滤器适用于基本用法，但某些情况可能需要更多处理。例如，打印任务可能需要为宽页纸或账本进行格式化。涵盖所有选项可能需要一整本书。对于过滤器来说，最好的方法是从小开始，然后逐渐增加复杂度。此外，一些过滤器包可能值得评估（例如 LPRng 以及互联网上的各种选择），它是非常简单的过滤器项，抑制了页头的使用。注意，页头与横幅页不同，例如许多与 JetDirect 等硬件连接的网络打印机打印的横幅页。横幅页必须在网络硬件中禁用；无法在 `/etc/printcap` 中禁用。对于处理包含一个本地打印机的基本 `/etc/printcap` 文件，这足够了。注意，默认设置的打印队列目录位于 `/var/pool/lpd`，所有需要的是...

# 创建队列（文件和目录）

使用 Berkeley 的 `lpd` 软件包时，你必须手动设置这些项目，包括用于每个队列的日志文件。然而，使用 LPRng 时不需要这样做。LPRng 启动一个名为 `checkqueue` 的实用程序，它可以为你构建所有项目。它读取输入到 `/etc/printcap` 的信息，并自动创建你的打印队列目录和日志、正确的所有权和权限。你只需要确保 `/etc/printcap` 中的信息对于你的打印配置来说是正确的，并运行以下命令：

```
checkqueue -f
```

# 列表 14.3 `checkqueue -f` 的输出

```
[trident /root]# checkqueue -f
LPRng version LPR-3.2
Get-perms: permissions entry /etc/lpd.perms
Get-perms: permissions entry /usr/etc/lpd.perms
Cannot open /etc/lpd.perms - 没有文件或目录
Get-perms: permissions entry /var/pool/lpd/lpd.perms.trident
Cannot open /var/pool/lpd/lpd.perms.trident - 没有文件或目录
```

```
LPD lockfile /var/spool/lpd/lpd.lock.trident
Checking directory: '/var/spool/lpd'
checking file '/var/spool/lpd/lpd.log.trident'
Truncating LPD log file '/var/spool/lpd/lpd.log.trident'
Checking /var/spool/lpd/lpd.log.trident
--file /var/spool/lpd/lpd.log.trident
checkqueue: Warning - cannot open /var/spool/lpd/lpd.log.trident
lp: Checking printer 'lp'
lp: Checking directory: '/var/spool/lpd/lp'
lp: directory stat /var/spool/lpd/lp failed - 没有目录
lp: Printer ''' dir /var/sp/// needs fixing
lp: creating /var/spool/lpd/lp
checkqueue: Warning - creating /var/spool/lpd/lp
checkqueue: Warning - changing ownership /var/spool/lpd/lp/
lp: checking file /var/spool/lpd/lp.control.lp
lp: checking file /var/spool/lpd/lp.status.lp
lp: checking file /var/spool/lpd/lp/log
checkqueue: Warning - changing owner of /var/spool/lpd/lp/control.lp
are = 0/2, 2/2
checkqueue: Warning - changing owner of /var/spool/lpd/lp/status.lp
are = 0/2, 2/2
checkqueue: Warning - changing owner of /var/spool/lpd/lp/log
are = 0/2, 2/2
lp: Need to fix 'lp' files, control dir /var/spool/lpd/lp/log/
lp: checking log file /var/spool/lpd/lp/log
lp: log @ 0 bytes long: no truncation
[root@trident ~]#
```

粗体文本表示根据 `/etc/printcap` 配置进行了更改。目录创建、日志文件创建和所有权更改等操作会在 `checkqueue` 检测到打印队列设置存在不一致时执行（这是可以理解的，因为在执行 `checkqueue` 时不存在打印队列）。

## 第 14 章 打印

列表 14.4 是远程打印机条目的一个示例。

### 列表 14.4 远程打印机的样本 `/ETC/PRINTCAP` 文件

```
remote
:mx=#
:rm=server.domain.com
:rp=ps
```

这里引入了两个行：`:rm=` 和 `:rp=` 行通过其使用的标签可能并不直观，其中，`rm` 代表远程机器（remote machine，不要与删除文件和目录的 `rm` 命令混淆），`rp` 代表远程打印机（remote printer）。这些行是为了取代 `:lp` 行而添加的，因为远程打印机不需要指定本地打印机端口（对此有一个例外，将在本章稍后的部分讨论）。

请注意，为了使此功能生效，远程机器上的打印机需要在自身的 lp/lpd 打印机系统中设置。换句话说，如果 `server.domain.com` 是一台运行 Windows 95 的机器，而你没有在那台机器上通过某种 Windows 95 版本的 `lpd` 设置好 `ps` 打印机，那么前面的打印机就是毫无用处的；`lpd` 系统只与 `lpd` 系统通信，与其他系统不通。

如前面提到的，远程打印队列通常预期执行格式化/过滤以成功处理传入的任务。这就是为什么在列表 14.4 的远程队列条目中没有 `:if` 行的原因。远程服务器端的过滤器与本地打印机的过滤器没有任何不同。设置打印服务器和客户端使用的是相同的软件；在打印服务器上设置好本地打印机后，它就可以被网络上的远程客户端使用。只需使用前述语法即可将所有打印任务重定向到远程打印机。

## 远程打印机的本地过滤—— 方案 I（过滤器重定向）

如果远程打印服务器端没有运行过滤器会发生什么？随着带有网卡的打印机日益普及，这实际上正成为一种常见现象。在这些情况下，打印机接受打印作业，并期望作业的格式足以使用打印机使用的图形对其进行打印。换句话说，打印机没有连接到服务器，它没有任何内置的过滤功能，而且基本上，如果你在发送打印作业之前没有对其进行格式化/过滤，它们将无法打印。

针对这些情况，你必须执行一些小技巧来在本地缓冲（spool）并过滤你的打印作业。遵循列表 14.2 中打印过滤器的逻辑，某种巧妙的命令可以让你展示实现这一目标的一种方法。

由于过滤必须在本地进行，且打印作业需要发送到远程队列，你必须同时设置本地和远程队列来实现此。列表 14.5 是 `/etc/printcap` 文件外观的一个良好示例。

### 列表 14.5 用于远程打印作业本地过滤的样本 `/ETC/PRINTCAP` 文件

```
ps
  :lp=/dev/null
:sd=/var/spool/lpd/ps
:mx#0
:if=/var/spool/lpd/ps/filter
:sh
```

```
remote
  :mx#0
  :rm=server.domain.com
  :rp=ps
```

此时，似乎没有什么特别之处或不同。`:lp` 指向 `/dev/null`是因为在这种情况下没有本地打印机——正在使用本地队列对远程打印作业进行过滤。有一个用于过滤的打印队列和一个位于 `server.domain.com` 的打印队列。

那么重定向发生在哪里呢？技巧发生在过滤器内部。

在列表 14.2 中，你看到很多地方都有 `-`。这些实际上是离开过滤器的路由。它们占据文件名的位置，并简单地表示：“在我施完魔术之后，将进入此过滤器的任何内容立即重新发送出去。”在过滤器的这些部分中，每个需要发生的是重定向到 `/etc/printcap` 中的远程队列。

列表 14.6 是列表 14.2 中过滤器的修订版本，并应用了用于本地过滤的必要更改。

### 列表 14.6 用于远程打印作业本地过滤的修改样本过滤器文件

```bash
#!/bin/sh

DEVICE=jet4
RESOLUTION=600x600
PAPERSIZE=letter
SENDEOF=

if [ "$PAPERSIZE" = "a4" ]; then
  T=A4
else
  T=US
fi
```

### 列表 14.6 续

```bash
if [ -x /usr/bin/nscript ]; then
nenscript -TST -ZB -p | lpr -Promote
else
if [ "$T" = "US" ]; then
T="Letter"
enscccript -M $T -Z -p | lpr -Promote
fi
if [ "$DEVICE" = "PostScript" ]; then
cat - | lpr -Promote
else
gqs -q -DEVICE=$DEVICE \
r$RESOLUTION \
-sPAPERSIZE=$PAPERSIZE \
-dnOPAUSE \
-dSAFER \
-sOutputFile=- | lpr -Promote
fi
if [ "$SENDEOF" != "*" ]; then
printf "\004"
fi
exit 0
```

现在，离开此过滤器的每个路由现在都管道到 `/etc/printcap` 中指定的远程队列。打印作业通过此过滤器发送，根据过滤器顶部 `DEVICE` 行的设置进行处理。

## 远程打印机的本地过滤—— 方案 II（回弹队列）

如果远程打印服务器端没有运行过滤器会发生什么？随着打印机内置网卡的普及，这实际上正成为一种常见现象。在这些情况下，打印机接受打印作业，并期望作业的格式足以使用打印机使用的图形进行打印。换句话说，打印机没有连接到服务器，它没有任何内置的过滤功能，而且基本上，如果你在发送打印作业之前没有对其进行格式化/过滤，它们将无法打印。

针对这些情况，你必须执行一些小技巧来在本地缓冲（spool）并过滤你的打印作业。遵循列表 14.2 中打印过滤器的逻辑，某种巧妙的命令可以让你展示实现这一目标的一种方法。

由于过滤必须在本地进行且打印作业需要发送到远程队列，你必须同时设置本地和远程队列来实现此。列表 14.5 是 `/etc/printcap` 文件外观的一个良好示例。

LPRng提供的提供的功能之一是回弹队列（bounce queue，在 `/etc/printcap` 中通过 `:bq` 行指定）。这允许系统在打印机准备好之前缓冲作业。列表 14.7 是使用此功能的 `/etc/printcap` 文件示例。

### 列表 14.7 利用回弹队列的样本 `/ETC/PRINTCAP`

```
ps
:lp=/dev/null
:sd=/var/spool/lpd/ps
:mx#0
:bq=ps@server.domain.com
:if=/var/spool/lpd/ps/filter
:sh
```
