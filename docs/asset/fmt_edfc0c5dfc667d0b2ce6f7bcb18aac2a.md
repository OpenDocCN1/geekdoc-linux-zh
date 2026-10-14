
File 18: `/etc/pdffilter/testqueue/offset.ps`: 更改打印区域的位置

### Gamma 校正

要调整颜色之间的 Gamma 分布，使用类似 `/etc/lpdffter/testqueue/cmyk.ps` 或 `/etc/lpdffter/testqueue/rgb.ps` 的文件：

```
!PS
{cyan exp} {magenta exp} {yellow exp} {black exp}
setcolortransfer
```

## File 19: `/etc/lpdffter/testqueue/cmyk.ps`: CMYK Gamma 校正

```
!PS
{red exp} (green exp) (blue exp) currenttransfer \
setcolortransfer
```

## File 20: `/etc/lpdffter/testqueue/rgb.ps`: RGB Gamma 校正

你需要知道打印机使用的颜色模型（CMYK 或 RGB）以使之生效。青、品、黄、黑以及红、绿、蓝使用的值应通过测试来确定。通常，这些值应该在 0.001 到 9.999 之间。

为了大致了解过滤操作对输出的影响，请将它们显示在屏幕上。要查看示例文件在没有 Gamma 校正时的显示如何，请输入：

```
earth:~: # gs -r600 \
/usr/share/doc/packages/ghostscript/examples/colorcoric.ps
```

查看根据上述过滤器进行 Gamma 校正后的效果：

```
earth:~: # gs -r600 /etc/lpdffter/testqueue/cmyk.ps \
/usr/share/doc/packages/ghostscript/examples/colorcoric.ps
```

```
earth:~: # gs -r600 /etc/lpdffter/testqueue/rgb.ps \
/usr/share/doc/packages/ghostscript/examples/colorcoric.ps
```

上述命令必须作为单行输入，不要包含反斜杠。

## 重置打印机

为了将打印机重置为原始状态，使用类似 `/etc/lpdffter/testqueue/reset.ps` 的文件：

```
%!PS
statusdict begin 0
```

File 21: `/etc/lpdffter/testqueue/reset.ps`: 重置打印机

为了每次打印后将打印机重置为原始状态，使用 `/etc/lpdffter/testqueue/pre` 的文件：

```
%!PS
statusdict begin 0
```

## 激活预载文件

要激活这些预载文件，创建一个创建一个类似 `/etc/lpdfilter/testqueue/pre`：

这些脚本需要为所有用户设置执行权限，可以通过 `chmod` 命令实现：

```
earth:~: # chmod -v a+rx /etc/lpdfilter/testqueue/ascii2ps
earth:~: # chmod -v a+rx /etc/lpdfilter/testqueue/pre
```

当启用 `DEBUG="low"` 时，程序将其 `stderr` 输出到文件 `/tmp/lpdfilter.if-$$$.XXXXX`（其中 $$ 是进程 ID，XXXXX 是一个唯一的随机字符串）。

当启用 `DEBUG="medium"` 时，程序除了记录自身的错误输出外，还会记录 `/usr/lib/lpdfilter/filter` 中脚本的 `stderr` 输出，前提是这些脚本是由 `/usr/lib/lpdfilter/bin/if` 运行的。调试输出被写入 `/tmp/lpdfilter.name-$$.XXXXX`（其中 name 是运行的脚本名称，$$XXXXX 是按描述方式组合的字符串）。

当启用 `DEBUG="high"` 时，所有错误输出都将按上述方式记录。此外，所有通常指向打印机的输出都会记录 `/tmp/lpdfilter.out-$$$.XXXXX`（其中 $$XXXXX 是按描述方式组合的字符串）。

为了避免对日志活动失去控制，你可能需要在每次运行新测试之前，使用 `rm -v /tmp/lpdfilter*` 删除日志文件。

## LPR 打印队列的自定义打印过滤器

本节的目的不是教你如何构建一个 lpdfilter，而是展示 Linux 打印引擎的内部工作原理。我们通过演示如何编写自定义打印机过滤器来实现。下面解释的示例保持了简单，以展示基本机制。这也是为什么在过滤器脚本中没有安排任何错误检查的原因。此示例假设打印机连接到第一个并行端口（`/dev/lp0`）。

任何打印过滤器都必须通过标准输入从打印机接收数据。过滤器必须将数据转换为打印机特定的格式，并通过标准输出发布。现在，打印队列会处理这些数据，并确保它们从过滤器的标准输出传输到 `/dev/lp0` 打印机设备。这就是 Linux 内核感知的地方：它将所有到达打印机设备的数据传输到相应的 IO 地址（例如 0x3778）。打印机通过并行线接收这些数据并对其进行解释以打印。

在系统中，普通用户没有直接访问打印设备的权限，因此执行以下命令需要 root 权限。此外，在如 `cat ascii-file > /dev/lp0` 的命令中，请将 ascii-file 替换为现有的 ASCII 文件名。

## 过滤操作

你可以使用简单命令 `echo -en "\Hello\r\f" >/dev/lp0` 进行打印。然而，这不会激活打印队列，也不会使用任何过滤器。它直接写入打印机设备 `/dev/lp0`。该命令将 ASCII 符号 '\r', 'H', 'e', 'l', 'o', '\r' 和 '\f' 直接发送到打印机设备。回车 ASCII 字符 '\r' 会使抬字移动（打印头）返回起始位置。换页 ASCII 字符 '\f' 会使打印机出页。

命令 `cat ascii-file >/dev/lp0` 和 `echo -en "\f" >/dev/lp0` 仍然不会激活队列或打印过滤器，但再次将字符直接发送到打印机设备 `/dev/lp0`。第一个命令发送字符；第二个命令添加一个换页符以出页。

在 Linux 下，ASCII 文本行仅由换行符（line feed）分隔。相比之下，DOS 和 Windows 下的换行由一个换行 ASCII 和一个回车 ASCII 组成。如果你输入命令：

```bash
earth:- # cat /etc/hosts >/dev/lp0
earth:- # echo -en "\f" >/dev/lp0
```

直接将 ASCII 文件 >/etc/hosts 发送到打印机，输出可能如下所示：

```
first line
second line...
```

原因是打印机只执行了换行而没有执行回车（因为两行之间实际上实际上没有回车字符）。但是，可以告诉打印机在每当发送换行符时同时执行换行和回车。通过转义序列 `\0336&x26`，所有理解 PCL3 语言的打印机都可以识别为在接收到 ASCII 换行符时执行换行和回车。使用 `echo -en "\0333&x26" >/dev/lp0` 向打印机发送转义序列，之后在打印 ASCII 文件时它应该按预期方式解释换行。

在尝试打印特定国家的字符（如变音符号）时可能会出现另一个问题。DOS 和 Windows 用于这些字符的编码与 Linux 使用的不同。打印机大多预配置为 DOS 和 Windows 环境。作为补救，输入：

```bash
earth:~ # cp ascii-file ascii-file.ibmpc
earth:~ # recode lat1..ibmpc ascii-file.ibmpc
```

将 ascii-file 复制到 ascii-file.ibmpc，然后根据 DOS 和 Windows 标准对 ascii-file.ibmpc 进行重新编码。之后：

```bash
earth:~ # cat ascii-file.ibmpc >/dev/lp0
earth:~ # echo -en "\f" >/dev/lp0
```

应该正确地打印变音符号和换行。不再需要修正行行为的特殊序列，因为 ascii-file.ibmpc 已经重新编码为 DOS 和 Windows 的换行和变音符号。

总而言之，命令序列：

```bash
earth:~ # cp ascii-file ascii-file.ibmpc
earth:~ # recode lat1..ibmpc ascii-file.ibmpc
earth:~ # cat ascii-file.ibmpc >/dev/lp0
```

应该正确地打印变音符号和换行。不再需要修正行行为的特殊序列，因为 ascii-file.ibmpc 已经重新编码为 DOS 和 Windows 的换行和变音符号。

## 示例自定义过滤器

首先，成为 root 并创建一个子目录：
