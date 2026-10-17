
无论是原始的 PostScript 打印机 PPD，还是由 Linuxprinting.org 生成的 PPD），如今所有受支持的打印后台处理程序（spoolers）都能随心所欲地利用 PPD 的强大功能。用户只需将 `foomatic-rip` 集成到他们的系统中即可。对于用户而言，媒体类型和来源的支持得到了改进——纸张尺寸和纸盒的配置变得更加简单。

此外，新一代的 Linuxprinting.org PPD 不再包含 Perl 数据结构。如果您是一个发行版维护者，并且之前使用的是旧版本的 Foomatic，您可能希望尝试一下新版本，但请记住通过新的 `foomatic-db-engine`[34] 生成新版本的 PPD 集合。普通用户只需按照 Foomatic 教程或本章中列出的步骤[35]，为其特定型号生成一个新的 PPD 即可。这一新发展确实令人惊叹。

`foomatic-rip` 是一个极其巧妙的封装器，它解决了为每种不同的打印机或打印后台处理程序运行 Ghostscript 时需要不同语法、选项、设备选择和/或过滤器的问题。同时，它可以读取与打印队列关联的 PPD，并根据用户的选择修改打印作业。随之而来的是新 Foomatic PPD 对 Adobe 规范的 100% 符合性。Foomatic 概念中的一些创新功能可能会让用户感到惊讶。它将支持许多打印机的自定义纸张尺寸，并支持在同一作业中从不同纸盒拉取媒体进行打印（在这两种情况下，即使基于 Windows 的厂商打印机驱动并不支持此功能）。

##### 21.13.1.6 外部驱动程序开发

大部分驱动程序开发工作本身并不在 Linuxprinting.org 内部进行。驱动程序由独立的维护者编写。Linuxprinting.org 只是汇集所有信息并将其存储在数据库中。此外，它还提供了 Foomatic 粘合层，将众多驱动程序集成到世界上已知的任何现代（或遗留）打印系统中。说到不同的驱动程序开发小组，目前大部分工作都在以下三个项目中进行：

- Omni[36] — 这是 IBM 的一个自由软件项目，旨在将其过去 OS/2 时期的打印机驱动知识转化为适用于 Linux/UNIX 的现代、模块化、通用驱动架构（目前仍处于测试版阶段）。目前支持 437 种型号。

- HPLJS[37] — 这是 HP 的一个自由软件项目，旨在为其自身产品系列提供支持（非常成熟，大多数情况下打印效果完美并提供真正的照片级质量）。目前支持 369 种型号。

- Gimp-Print[38] — 这是一个自由软件项目，由 Michael Sweet（也是 CUPS 的主要开发人员）发起，现由 Robert Krawitz 主导，该项目达到了惊人的照片打印质量水平（许多 Epson 用户甚至宣称其质量优于 Epson 为 Microsoft 平台提供的厂商驱动）。目前支持 522 种型号。

> 34 <http://www.linuxprinting.org/download/foomatic/foomatic-db-engine-3.0.0beta1.tar.gz>

> 35 <http://www.linuxprinting.org/sefiles/LinuxKongress2002/Tutorial/II.Foomatic-User/II.tutorial-handed-foomatic-user.html>

> 36 <http://www-124.ibm.com/developersworks/oss/linux/projects/omni/>

> 37 <http://hpljjet.sf.net/>

> 38 <http://gimp-print.sf.net/>

### 21.13.1.7 论坛、下载、教程、操作指南（也适用于 Mac OS X 和商业 UNIX）

如今，Linuxprinting.org 是下载打印机驱动程序的一站式商店。查找打印机信息和教程[39]，或在其热门论坛[40]中解决打印问题。该论坛不仅面向 GNU/Linux 用户，商业 UNIX 系统管理员[41]也会访问那里，而相对较新的 Mac OS X 论坛[42]在短短几周内就成为了访问频率最高的论坛之一。

Linuxprinting.org 和围绕 Ghostscript 的 Foomatic 驱动程序封装器现在是所有重要发行版打印的标准工具链。它们底层大多也使用 CUPS。尽管近年来大部分打印机数据都是由 Kampetper 添加的，但也来自 SuSE、Red Hat、Connectiva、Debian 以及其他厂商工程师的许多额外贡献。厂商中立性是 Foomatic 项目的重要目标。Mandrake 和 Connectiva 已合并，现在称为 Mandriva。

> Mandrakesoft 的 Till Kampetper 利用业余时间为维护 Linuxprinting.org 和 Foomatic 做出了卓越的工作。因此，如果您经常使用它们，请给他发一封电子邮件以表达您的感激之情。

##### 21.13.1.8 Foomatic 数据库生成的 PPD
