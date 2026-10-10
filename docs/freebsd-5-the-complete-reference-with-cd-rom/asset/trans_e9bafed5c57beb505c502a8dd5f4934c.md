
## 252 FreeBSD：完整参考指南

> **提示**
>
> 除了打印机输出格式外，Ghostscript 还支持一些常见的图形文件输出格式。这些包括 TIFF（tiff42anc 等）、PNG（png16、png256、png16m 等）、JPEG（jpeg）、EPS（epswrite）、PostScript（pswrite）以及 PDF（pdfwrite）。虽然从 PostScript 输入生成 PostScript 输出听起来有些奇怪，但在某些情况下这非常有用，例如当您的 PostScript 打印机因内存不足或其他问题而无法处理原始 PostScript 文件时。

当输入如上述示例的 Ghostscript 命令时，每生成新的一页您都会看到一个提示，要求按 ENTER；之后您需要在提示符处输入 `quit` 以退出程序。通过在输入文件名之前添加 `-dNOPAUSE -dBATCH` 到命令中，您可以消除这些提示。如果您创建自定义滤镜来处理 PostScript 文件，这些选项可能极其重要。

创建输出文件后，您可以将其发送到打印机（通过 `cat` 或 `lpr`——但如果您已设置滤镜，`lpr` 可能无法正常工作）。您应该会得到合理的输出。如果没有输出，或者您得到了一页又一页的乱码，可能需要尝试另一种驱动程序。如果您看不到任何打印机活动的迹象，例如指示灯闪烁，您可能需要回过头去调查基本的打印机连接问题。

## 设置智能滤镜

FreeBSD 上有几种智能滤镜包可用。这些本质上是像 9-2 列表那样的滤镜，但更加复杂。它们可以识别许多不同的文件类型，并处理文件以便它们能在您的打印机上打印。最常见的是，这些滤镜调用常见的文件转换程序将输入文件转换为 PostScript。然后，滤镜使用 Ghostscript 将文件转换为您的打印机能够理解的格式。（如果您有 PostScript 打印机，最后这一步会被跳过。）配置完成后，打印任何受支持的文件类型只需将文件提供给该滤镜即可。两个特别流行的智能滤镜包是 `affsfilter` 和 `magicfilter`，两者都可通过 `sysinstall` 的 Print 软件部分获取。本节描述了 `magicfilter` 的配置。

使用 `magicfilter` 的正常方式有点不寻常：您将它的配置文件当作程序来调用。这种技术之所以有效，是因为配置文件被标记为可执行，并以 FreeBSD 用于像 shell 脚本语言一样启动 `magicfilter` 的代码开头。各种 `magicfilter` 配置文件位于 `/usr/local/libexec/magicfilter` 目录下，并以它们依赖的 Ghostscript 驱动程序命名。例如，针对 ljjet4 Ghostscript 驱动程序的滤镜被称为 `Ljet4-filter`。作为 `magicfilter` 配置工作的一个示例，请考虑 9-3 列表，这是经过修改的 9-1 列表，用于对 Laserjet 4 或兼容打印机使用 `magicfilter`。如您所见，唯一的区别是添加了对 `magicfilter` 配置文件的调用。

**列表 9-3**
**使用 magicfilter 的 /etc/printcap 条目示例**

```text
lp|hp4000:\
:lp=/dev/lp0:\
:br#115200:\
:sd=/var/spool/lpd/hp4000:\
:mx#0:\
:s#:\n::if=/usr/local/libexec/magicfilter/ljet4-filter:
```

![](img/f34d37e3abe9f4517128e54f80ab2616_290_0.png)

如果 **magicfilter** 恰好附带了适用于您打印机的滤镜，那么打印机设置就很简单——或者至少不会比设置纯文本队列更糟。然而，如果 **magicfilter** 包缺少适用于您打印机的合适滤镜，您必须自己创建一个。

![](img/f34d37e3abe9f4517128e54f80ab2616_290_1.png)

Ghostscript——因此也包括 **magicfilter**——为打印机类别提供驱动程序。例如，许多激光打印机使用与各种 *Hewlett-Packard* 型号相同的打印机控制语言（PCL），因此您可能能够使用 *laserjet*、*ljet2dp*、*ljet3*、*ljet4* 以及类似的驱动程序（以及名称相似的 **magicfilter** 配置文件）来处理由 *Lexmark*、*Brother*、*Okidata* 和其他厂商销售的打印机。请咨询 **Linux Printing** 网站 (http://www.linuxprinting.org/printer-list.cgi) 以获取有关哪个 *Ghostscript* 驱动程序与您的打印机配合良好的信息。

如果您需要创建自定义的 **magicfilter** 配置文件，我建议从复制类似打印机的现有滤镜开始。最重要的标准是*不要*选择 PostScript 文件（这些文件以 *%!* 或 *%ps* 开头），因为这些文件将 PostScript 输出直接发送到打印机端口，而不调用 **Ghostscript**。大多数滤镜文件在文件的开头部分都包含对 **Ghostscript** 的引用，如下所示：

```text
# PostScript
0 !\t filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
0 `004!` filter /usr/local/bin/gs -q -dSAFER -dNO_PAUSE -r600 -dDEVICE=ljet4 -oOutputFile-
```

要修改您复制的配置文件，您必须更改由 *-SDEVICE* 选项指定的 **Ghostscript** 驱动程序名称。再次，**Linux Printing** 网站的数据库在了解此处应填写什么内容时可能非常有价值。许多 **magicfilter** 配置包含允许滤镜识别打印机原生语言文件中的行。此功能使您能够打印那些能产生原生特定输出的应用程序生成的文件。如果您使用无关打印机的滤镜作为模型，您可能希望删除这些行。如果您想在 **The GIMP** 等应用程序中打印打印机特定的驱动程序，您必须为打印机的格式创建新规则，这可能很棘手。通常，打印 PostScript 并使用 **magicfilter** 的正常 PostScript 处理规则要更容易。

即使对于 **magicfilter** 支持的打印机，您也可能想要创建现有配置文件的变体。例如，您可能想要创建配置以在不同分辨率下打印（更改对 *gs* 调用中的 *-r* 值）并设置多个打印队列，每个分辨率一个队列。例如，您可能有 *epson360* 和 *epson720* 队列，分别以 360 和 720 dpi 向 *Epson inkjet* 打印机打印。

一旦您修改了 /etc/printcap 文件以使用您的新滤镜，请重启 lpd。然后，您可以使用 lpr 打印各种文件来测试打印功能。翻阅您的滤镜文件以了解您的滤镜支持哪些文件类型。当您尝试打印 magicfilter 不支持的文件时，该文件应从队列中悄无声息地消失，从而防止可能出现的乱码纸张喷发。（尽管 root 用户会收到拒绝的电子邮件通知。）如果文件类型受支持，它应被处理，并且您应得到合理的输出。

## 控制打印机

如果您按照本章阅读配置了系统，您现在应该在 FreeBSD 系统上拥有一个可用的打印队列。本节描述了如何使用此打印队列，既作为普通用户，也作为系统管理员。主题包括提交打印作业、检查队列中的作业、删除作业、重新排序作业以及更改打印队列的可用性。

### 提交打印作业

本章已经提到了 `lpr` 实用程序，它是 FreeBSD 中向队列提交打印作业的工具。这个工具非常重要，以至于它值得进行扩展描述。您还应该了解应用程序如何与 `lpr` 交互，以便您可以直接从程序打印，而不是生成 PostScript 文件然后手动使用 `lpr` 打印它。

### 使用 lpr

`lpr` 程序接受许多选项，其中一些相当晦涩。请查阅 `lpr` 手册页以了解详细信息。简化的语法是

```bash
lpr [-P*printer*] [-*num*] [-U *user*] [-hnmrs] [*filename*...]
```

这些选项的含义是：

- `-P*printer*` 此选项设置要使用的打印机队列。在支持多台打印机的系统上，这可能是最常用的 `lpr` 选项。默认值是 *PRINTER* 环境变量的值，如果该变量不存在，则为 `lp`。某些版本的 `lpr` 要求 `-P` 和队列名称之间没有空格，但 FreeBSD 随附的 BSD LPD 可以容忍空格。
- `-#*num*` 此选项告诉 `lpr` 生成 *num* 份打印副本。例如，`lpr -#4 afile.ps` 创建 `afile.ps` 的四份副本。
- `-U *user*` FreeBSD 跟踪谁提交了打印作业。此选项仅对 *root* 和 *daemon* 可访问，使您可以指定与打印作业相关联的用户。

