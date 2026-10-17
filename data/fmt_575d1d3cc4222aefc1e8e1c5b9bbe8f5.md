
```text
lp:
:lp=/dev/lp0:
:sh:
:mx=0:
:sd=/var/spool/lpd:
:lf=/var/log/lpd-errors:
```

此行适用于连接到 USB 端口的打印机。对于连接到并行或“打印”端口的打印机，使用：

```text
:lp=/dev/lp0:
```

对于直接连接到网络的打印机，使用：

```text
:lp=remote=network-printer-name :rp=raw:
```

将 `network-printer-name` 替换为网络打印机的 DNS 主机名。

3. 通过编辑 `/etc/rc.conf` 添加此行启用 `lpd`：

```text
lpd_enable="YES"
```

启动服务：

```
# service lpd start
```

启动 `lpd`。

4. 打印测试：

```
# printf "1. This printer can print.\n2. This is the second line.\n" | lpr
```

## 提示

如果两行都没有从左边界开始，而是变成了“阶梯状”，请参阅第 9.5.3 节“防止纯文本打印机出现阶梯状”。

## 打印连接

现在可以使用 `lpr` 打印文本。在命令行上提供文件名，或将输出管道到 `lpr`。

```bash
% lpr textfile.txt
```

```bash
% ls -lh | lpr
```

### 9.2. Printer连接

打印机通过多种方式连接到计算机系统。小型桌面打印机通常连接到计算机的 USB 端口。旧打印机连接到并行或“打印”端口。某些打印机直接连接到网络，方便多台计算机共享。少数打印机使用稀有的串口连接。

FreeBSD 可以与所有类型的打印机通信。

USB 打印机可以连接到计算机上任何 USB 端口。

当 FreeBSD 检测到 USB 打印机时，会创建两个设备项：`/dev/ulpt0` 和 `/dev/unlpt0`。发送到任何设备的数据将转发到打印机。每个打印作业结束后，`ulpt0` 会重置 USB 端口。重置的端口可能会导致某些打印机出现问题，因此通常使用 `unlpt0` 设备。`unlpt0` 完全不会重置 USB 端口。

### 并行口 (IEEE-1284)

并行端口设备为 `/dev/lpt0`。无论是否连接了打印机或是否被检测到，该设备都会出现。

厂商已很大程度上放弃了这些“遗留”端口，许多计算机已不再拥有这些端口。可以使用适配器将文件打印机连接到 USB 端口。使用此类适配器，打印机可以被视为真正的 USB 打印机。还可以使用称为打印服务器的设备将并行打印机直接连接到网络。

### 串口 (RS-232)

串口端口是另一种遗留端口，除了某些小众应用外，很少用于打印机。电缆、连接器和所需的接线差异很大。

对于内置在主板上的串口端口，串口设备名称为 `/dev/cuau0` 或 `/dev/cuau1`。也可以使用串口 USB 适配器，它们将显示为 `/dev/cuau0`。

串口打印机通信，必须知道几个通信参数。最重要的是波特率或 BPS（每秒比特）和校验位。值各异，但典型的串口打印机使用 9600 的波特率且无校验。

### 网络

网络打印机直接连接到本地计算机网络。

必须知道打印机的 DNS 主机。如果打印机通过 DHCP 分配动态地址，则应该动态更新 DNS，以确保主机名始终具有正确的 IP 地址。网络打印机通常被赋予静态 IP 地址以避免这个问题。

大多数网络打印机理解通过 LPD 协议发送的打印作业。还可以指定打印队列名称。某些打印机根据使用的队列以不同的方式处理数据。例如，`raw` 队列原封地打印数据，而 `text` 队列则向纯文本添加回车符。

许多网络打印机还可以打印直接发送到端口 9100 的数据。

## 第9 章 打印

### 9.2.1. 总结

有线网络连接通常是最设置且打印速度最快的。对于直接连接计算机，为了速度和简单，首选 USB。并行连接可行，但在电缆长度和速度上有限制。串口连接配置较为困难。不同型号之间的电缆接线不同，且罕见。

## 9.3. 页面描述语言

发送到打印机的数据必须是打印机能理解的语言。这些语言被称为页面描述语言（PDL）。

### ASCII

纯 ASCII 文本是向打印机发送数据最简单的方法。字符与打印内容一一对应：数据中的 A 会在页面上打印 A。可用格式非常少。没有方法选择字体或等比例间距。纯 ASCII 的强制简单性意味着文本可以直接从计算机打印，几乎或完全不需要编码或转换。打印输出与发送的内容直接对应。

### PostScript®

PostScript® 与 ASCII 几乎相反。PostScript® 程序不是简单的文本，是一组绘制最终文档的指令。可以使用不同的字体和图形。然而，这种能力是有代价的。必须编写绘制页面的程序。通常此程序由应用程序生成，因此该过程对用户是不可见的。

廉价打印机有时为了节省成本而省略 PostScript® 兼容性。

### PCL (打印机命令语言)

PCL 是 ASCII 的扩展，增加了用于格式化、字体选择和打印图形的转义序列。许多打印机提供 PCL5 支持。某些支持较新的 PCL6 或 PCLXL。这些后期版本是 PCL5 的超集，可以提供更快的打印速度。

### 基于主机 (Host-Based)

制造商可以通过为打印机配备简单的处理器和极小的内存来降低成本。这些打印机无法打印纯文本。相反，文本和图形的位图由主机计算机上的驱动程序绘制，然后发送到打印机。这些被称为基于主机的打印机。

驱动程序与基于主机的打印机之间的通信通常通过私有或未定义的协议进行，使其仅有效。

### 9.3.1. 将 PostScript® 转换为其他 PDL

来自 Ports Collection 的许多应用程序和 FreeBSD 工具产生 PostScript® 输出。此表显示了可将其转换为其他常见 PDL 的工具：

表 9.1. 输出 PDL

| 输出 PDL | 生成自 |or |

| :--- | :--- | :--- |

| PCL 或 PCL5 | print/ghostscript9-base | 单色使用 `-sDEVICE=ljet4`，彩色使用 `-sDEVICE=cljet5` |

| PCLXL 或 PCL6 | print/ghostscript9-base | 单色使用 `-sDEVICE=pxmono`，彩色使用 `-sDEVICE=pxlcolor` |

| ESC/P2 | print/ghostscript9-base | `-sDEVICE=unprint` |

| QXQ | print/foo2zjs | |

### 9.3.2. 总结

为了最简单的打印，请选择支持 PostScript® 的打印机。支持 PCL 的打印机是次选。通过 `print/ghostscript9-base`，这些打印机可以像原生支持 PostScript® 一样使用。直接支持 PostScript® 或 PCL 的打印机几乎也支持直接打印纯 ASCII 文件。

像典型喷墨机那样的行打印机通常不支持 PostScript® 或 PCL。它们通常可以打印纯 ASCII 文件。`print/ghostscript9-base` 支持这些某些打印机使用的 PDL。然而，由于需要传输和打印的数据量巨大，在这些打印机上打印整个基于图形的页面通常非常慢。

基于主机的打印机通常更难设置。某些无法无法，因为使用了私有 PDL。尽可能避免使用这些打印机。各种 PDL 的描述可以在 http://www.undprint.org/page_languages。

## 9.4. 直接打印

对于偶尔打印，文件可以直接发送到打印机而无需任何设置。例如，将 `sample.txt` 发送到 USB 打印机：

```
# cp sample.txt /dev/unpt0
```

直接打印到网络打印机取决于打印机的能力，但大多数接受 9100 端口，可以使用 `nc` 使用它们。向主机名为 `netlaser` 的打印机打印文件：

```
# nc netlaser 9100 < sample.txt
```

## 9.5. LPD (行守护进程)

后台打印文件称为池化。守护进程允许用户在等待打印机缓慢完成打印作业时继续操作。FreeBSD 包含名为 `lpd(8)` 的守护进程。通过 `lpr(1)` 提交打印作业。

### 9.5.1. 初始化

创建存储打印作业的目录，设置所有者，并设置权限以防止其他用户查看文件内容：

```
# mkdir -p /var/spool/lpd/lp
# chown daemon:daemon /var/spool/lpd/lp
# chmod 770 /var/spool/lpd/lp
```

打印机定义在 `/etc/printcap` 中。每个打印机的条目包括名称、连接的端口以及各种设置。使用以下内容创建 `/etc/printcap`：

lp:\
:lp=/dev/unpt0:\
:sh:\
:mx#0:\
:sd=/var/spool/lpd/lp:\
:lf=/var/log/lpd-errs:

此打印机的名称。`lpr(1)` 将打印作业发送到 `lp` 打印机，除非用 `-P` 指定另一个打印机，因此默认打印机应命名为 `lp`。

打印机连接的设备。根据此处连接类型替换此行。

连接类型

`/etc/printcap` 中的设备

USB

```
:lp=/dev/unpt0:
```

这是非重置 USB 打印机设备。如果遇到问题，请使用 `ultp0`，它会在每次使用时重置 USB 端口。

并行

```
:lp=/dev/lpt0:
```

网络

对于支持 LPD 协议的打印机：

```
:lp=:rm= network-printer-name :rp=raw:
```

对于支持 9100 端口打印的打印机：

```
:lp=9100 @ network-printer-name :
```

对于两种类型，将 `network-printer-name` 替换为网络打印机的 DNS 主机名。

串口

```
:lp=/dev/cuau0:br=9600:pa=none=\
```

这些值适用于连接到主板串口端口的典型串口打印机。波特率为 9600，且不使用校验位。

在打印作业开始时抑制打印标题页。

不限制打印作业的最大尺寸。

此打印机的打印目录路径。每台打印机都使用自己的打印目录。

报告此打印机上错误的日志文件。

创建 `/etc/printcap` 后，使用 `chkprintcap(8)` 测试其是否有错误：

```
# chkprintcap
```

在继续之前修复任何报告的问题。

在 `/etc/rc.conf` 中启用 `lpd(8)`：

```
lpd_enable="YES"
```

启动服务：

```
# service lpd
```

### 9.5.2. 使用 lpr(1) 打印

使用 `lpr` 将文档发送到打印机。待打印的文件可以在命令行中指定名称，也可以通过管道传递给 `lpr`。这两个命令是等价的，都会将 `doc.txt` 的内容发送到默认打印机：

```
% lpr doc.txt
```

```
% cat doc.txt | lpr
```

可以使用 `-P` 选择打印机。要打印到名为 `laser` 的打印机：

```
% lpr -Plaser doc.txt
```

### 9.5.3. 过滤器

到目前为止的示例都是将文本文件的内容直接发送到打印机。只要打印机理解这些文件的内容，输出就能正确打印。

某些打印机不具备打印纯文本的能力，输入文件可能甚至不是纯文本。

过滤器允许对文件进行转换或处理。典型用法是将一种类型的输入（如纯文本）转换为打印机可以理解的格式（如 PostScript® 或 PCL）。过滤器还可以用于提供额外功能，例如添加页码或高亮源代码以使其更易阅读。

这里讨论的过滤器是输入过滤器或文本过滤器。这些过滤器将传入的文件转换为不同的形式。

在创建文件之前，请使用 `su(1)` 成为 root 身份。

过滤器在 `/etc/printcap` 中通过 `if=` 标识符指定。要使用 `/usr/local/libexec/lf2crlf` 作为过滤器，请如下修改 `/etc/printcap`：

```
lp:
:lp=/dev/unpt0:\n:sh:\n:mx#0:\n:sd=/var/spool/lpd/lp:\n:if=/usr/local/libexec/lf2crlf:\n:lf=/var/log/lpd-errs:
```

`if` 标识将用于输入文本的输入过滤器。

提示

`printcap` 条目行尾的反斜杠行延续符字符表明，打印机条目实际上是一条长行，由由冒号分隔的条目组成。之前的示例可以重写为单行但可读性较差：

```
lp:lp=/dev/unpt0:sh:mx#0:sd=/var/spool/lpd/lp:if=/usr/local/libexec/lf2crlf:lf=/var/log/lpd-errs:
```

#### 9.5.3.1. 防止纯文本打印机上出现阶梯现象

典型的 FreeBSD 文本每行末尾只包含一个换行符。这些行在标准打印机上会形成“阶梯”状：

打印出的文件看起来像被风吹散的楼梯。

过滤器可以将换行符转换为回车符和换行符。回车符会使每行结束后返回左侧。使用以下内容创建 `/usr/local/libexec/lf2crlf`：

```
#!/bin/sh

CR=$"r"

/usr/bin/sed -e "s$/${CR}/g"
```

设置权限并使其可执行：

```bash
# chmod 555 /usr/local/libexec/lf2crlf
```

修改 `/etc/printcap` 以使用新过滤器：

```
:if=/usr/local/libexec/lf2crlf:\
```

通过打印相同的纯文本来测试过滤器。回车符将导致每行都从页面的左侧开始。

#### 9.5.3.2. 使用 print/encscript 在 PostScript® 打印机上打印花式纯文本

GNU Enscript 将纯文本转换为格式良好的 PostScript® 以在 PostScript® 打印机上打印。它添加了页码、自动换行，并提供了许多其他功能使打印的文本更易阅读。根据本地纸张大小，从 Ports Collection 安装 `print/encscript-letter` 或 `print/encscript-a4`。

使用以下内容创建 `/usr/local/libexec/encscript`：

```
#!/bin/sh
/usr/local/bin/encscript -o -
```

设置权限并使其可执行：

```bash
# chmod 555 /usr/local/libexec/encscript
```

修改 `/etc/printcap` 以使用新过滤器：

```
:if=/usr/local/libexec/encscript:\
```

通过打印纯文本来测试过滤器。

#### 9.5.3.3. 将 PostScript® 转换为 PCL

许多程序产生 PostScript® 文档。然而，廉价打印机只识别纯文本。此过滤器在发送到打印机之前将 PostScript® 转换为 PCL。从 Ports Collection 安装 Ghostscript 解释器。使用以下内容创建 `/usr/local/libexec/ps2pcl`：

```
#!/bin/sh
IFS="" read -r first_line
case "$first_line" in
    !)
        echo "$first_line" | /usr/local/bin/gs -dSAFER -dBATCH -sOutputFile=- && exit 0
        ;;
    *)
        echo "$first_line" | cat
        ;;
esac
```

设置权限并使其可执行：

```bash
# chmod 555 /usr/local/libexec/ps2pcl
```

修改 `/etc/printcap` 以使用新过滤器：

```
:if=/usr/local/libexec/ps2pcl:\
```

通过向其发送一个小型 PostScript 作业来测试过滤器：

```
printf "Helvetica findfont showpage" | lpr
```

#### 9.5.3.4. 智能过滤器

编写一种能够识别并正确格式化多种类型的过滤器是挑战性的。来自 Ports Collection 的 `print/apsfilter` 是一种智能魔法过滤器，它可以将其转换为打印机理解的 PDL。更多详情请见 http://www.apsfilter.org。

### 9.5.4. 多队列

`/etc/printcap` 中的条目是队列的真实定义。单台打印机可以有多个队列。与过滤器结合时，多队列为用户提供了对打印方式的更多控制。例如，考虑办公室中的一台网络 PostScript 激光打印机。大多数用户想要打印纯文本，但少数高级用户希望能够直接打印 PostScript® 文件。在 `/etc/printcap` 中为同一台打印机创建两个条目：

```
textprinter:\
:lp=9100@officaser:\
:sh:\
:mx#0:\
:sd=/var/spool/lpd/textprinter:\
:if=/usr/local/libexec/encscript:\
:lf=/var/log/lpd-errs:
psprinter:\
:lp=9100@officaser:\
:sh:\
:mx#0:\
:sd=/var/spool/lpd/psprinter:\
:lf=/var/log/lpd-errs:
```
