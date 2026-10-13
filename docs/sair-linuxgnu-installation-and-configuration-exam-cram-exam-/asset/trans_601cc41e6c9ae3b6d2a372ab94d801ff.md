
## 过滤器

过滤器将您从应用程序和编辑器中想要打印的内容翻译成打印机可以理解的各种语言。两种主要的打印机图形语言是 Hewlett Packard 的 PCL 和 Adobe 的 PostScript。这些语言属于不同的类别；某些应用程序使用 PostScript 将文件翻译为 PCL。与这些语言配合使用的图形过滤器主要有三种类型：enscript、ghostscript 和 magic。您需要在 /etc/printcap 文件中设置将要使用的过滤器。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_195_0.png)

> 大多数 Linux 应用程序都使用 PostScript 文件。因此 Linux 的 PostScript 打印机驱动程序更为常见。

Enscript 是商业版 enscript 打印机过滤器的 GNU 克隆版。与其 GNU 亲戚 a2ps 一样，它将文本转换为 PostScript 格式。Enscript 和 a2ps 比其他 PostScript 过滤器更灵活，因为它们允许您在一张纸上打印两页文本。

Ghostscript 是一个 PostScript 解释器，它允许 Linux 在图形用户界面中显示 PostScript 文件，同时也是一个转换器，可将 PostScript 数据发送到许多打印机。

Magic 过滤器实际上并不是真正的过滤器。它们是脚本，可自动检测文件内部的数据类型，然后调用适当的过滤器将数据转换为打印机格式。从某种意义上说，这就像第 8 章中的 file 命令。Magic 过滤器可将 DVI 或 PostScript 等模式转换为 Hewlett Packard 的 PCL。

注意：DVI 文件是 LaTeX 或 TeX 输入文件处理后的数据。

还有一个主要的过滤器，称为 lpf。这是一个用于文本文件的过滤器。lpf 过滤器重新格式化 ASCII 文本以避免“阶梯状”现象，即打印机在每个单词后添加额外行时出现的情况。

## 排队目录

打印 spool 通常位于 /var/spool/lpd 目录中。每个作业都有自己的文件。在使用 BSD（Berkeley Standard Distribution）版行式打印机守护进程的旧版 Linux 系统上，Linux 无法处理大于 1MB 的 spool 文件，这就是 lpr -s 命令存在的原因。如果您在使用 lprm 和 lpc 等命令管理 spool 时遇到问题，您可以通过直接删除 spool 目录中的文件来终止打印作业。

打印 spool 与日志文件一样，通常存储在 /var 目录或其子目录中。

## /etc/printcap 文件

所有不同打印机的设置都存储在 /etc/printcap 文件中。在本节中，您将分析一个典型的 /etc/printcap 文件，以便使其适用于您。图 9.3 显示了来自 Corel Linux 发行版的 /etc/printcap 文件示例。

乍一看，该文件可能相当令人困惑，因此让我们先回顾一下该文件可用的一些代码。然后您就可以解释此文件或您当前 Linux 发行版中的文件。

### /etc/printcap 代码

/etc/printcap 文件中的代码可以分为以下几类：打印机名称、过滤器、spool、日志文件和特殊打印机代码。该文件还有单独条目的格式。例如，图 9.3 中显示的第一个部分可能显示为三行长代码：

```
lp|Generic dot-matrix printer entry:lp:/dev/lp0:\
sd=/var/spool/lpd/lp:af=/var/log/lp-acct:\
lf=/var/log/lp-errs:pl#66:pw#80:pc#150:mx#0:sh
```

```
# /etc/printcap: printer capability database. See printcap(5).
# You can use the filter entries df, tf, cf, gf etc. for
# your own filters. See /etc/filter.ps, /etc/filter.pcl and
# the printcap(5) manual page for further details.

lp|Generic dot-matrix printer entry\
:lp=/dev/lp0\
:sd=/var/spool/lpd/lp\
:af=/var/log/lp-acct\
:lf=/var/log/lp-errs\
:pl#66\
:pw#80\
:pc#150\
:mx#0\
:sh\

# rlp|Remote printer entry\
# :lp=\
# :rm=remotehost\
# :rp=remoteprinter\
# :sd=/var/spool/lpd/remote\
# :mx#0\
# :sh
```

图 9.3 一个典型的 /etc/printcap 打印机配置文件。

不幸的是，这种类型的代码管理会使除最有经验的 Linux 管理员之外的所有人生活更加困难。您在该文件或任何其他程序中设置和呈现代码的方式有助于向其他管理员传达您的意图。有三个标点符号可以帮助您管理 /etc/printcap 代码。

- **冒号 (:)**—冒号分隔代码行。如果您看到冒号，即使在行内，它也会开始一个新命令。
- **反斜杠 (\ )**—如果一行以反斜杠结尾，则表示代码继续到下一行。回想一下第 7 章，反斜杠告诉 shell 忽略空字符、回车等字符。
- **竖线 (|)**—/etc/printcap 文件中竖线后的行是注释。如您所见，前面的代码行和图中所显示的行描述了某种类型的打印机。但这些注释很重要，因为您可以使用它们来指定特定打印机。

> 注意：/etc/printcap 段落中的第一行通常定义打印机。您可以看到前面显示的行以 lp 开头，这是默认打印机的代码。

打印机名称基于 /dev/ 目录中安装并可用的驱动程序。典型的打印机名称包括 lp、lp1、lp2、sp1 和 lf1。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_197_0.png)

> 默认打印机在 /etc/printcap 文件中具有 lp 标签。如果没有此标签的打印机，则该文件中的第一个打印机成为默认打印机。

前面讨论的打印过滤器可以指定为输入过滤器 (if) 或输出过滤器 (of)。如果单台打印机上有多个打印作业，则每个打印作业都只使用输入过滤器。输出过滤器仅应用于一系列打印作业中的第一个作业。

spool 目录 (sd) 是在将过滤后的打印作业发送到打印机之前存储它们的位置。Linux 需要一个地方来存储这些打印作业，因为打印机并不总是可用。例如，您的打印机可能已断开连接或正在处理另一个打印作业。此外，Linux 联系远程计算机上的打印机可能需要时间。

当您打印时，Linux 可以跟踪打印成本和打印错误。用于这些功能的日志文件是记账过滤器 (af) 和行过滤器 (lf)。记账过滤器不言自明。行过滤器收集错误。

还有许多其他代码。其中一些更重要的代码记录在表 9.5 中。

表 9.5 /etc/printcap 文件的特殊代码。

| 代码 | 功能 |
|------|------|
| rm | 远程机器：将此设置为远程打印服务器的主机名或 IP 地址（例如，rm=192.168.0.66 命令告诉行式打印机守护进程 [lpd] 您的远程打印机的 IP 地址为 192.168.0.66）。 |
| rp | 远程打印机：如果您正在打印 PostScript 文件而打印机无法检测此类型文件，请将此值设置为 raw（rp=raw）。 |
| mx | 最大文件大小：帮助您使用旧版 BSD 行式打印机守护进程（lpd）。如果您不想要最大文件大小，请将此值设置为 0（mx=0）。 |
| pw | 页面宽度，以字符为单位：美国信纸上的标准页面宽度为 80（pw#80）。 |
| pl | 页面长度，以行数为单位：美国信纸上的标准页面长度为 66（pl#66）。 |
| sh | 抑制页眉：当您看到此命令时，打印机不会打印包含作业和用户名的页面。 |

*注意：有关 /etc/printcap 文件内部语法的更多信息可在其手册页上找到。*

## 一个典型的 /etc/printcap 文件

一旦了解基本语法，您就可以阅读大多数典型的 /etc/printcap 文件。返回图 9.3。您知道 lp 是默认打印机的名称，其设备位于设备文件 /dev/lp0 中。发送到该打印机的文件首先在 sd 定义的目录中进行 spool，即 /var/spool/lpd/lp:。

同样，记账过滤器的输出存储在 /var/log/lp-acct 文件中。错误由行过滤器接收并发送到 /var/log/lp-errs 文件。页面长度 (pl) 为 66 行。页面宽度 (pw) 为 80 个字符。价格代码 (pc) 为每页 1.5 美分。打印机 spool 文件的大小没有限制（mx#0）。抑制页眉 (sh) 命令可防止打印机打印包含您的用户名和打印作业编号的页面。

您将在练习问题中查看其他示例。

