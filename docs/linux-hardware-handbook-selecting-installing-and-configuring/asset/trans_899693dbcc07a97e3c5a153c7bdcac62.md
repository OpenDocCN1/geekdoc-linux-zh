

简要描述。通常的操作是将文件通过一个或多个*过滤器*，这些过滤器可以将文件转换为打印机能够理解的格式。例如，过滤器可能会将文件通过 Ghostscript 进行处理。然后 `lpd` 将过滤器处理的结果发送到打印机的端口。系统使用打印过滤器允许你创建队列，这些队列可以自动处理各种类型的文件。

在 Linux 中配置打印机的关键在于 `/etc/printcap` 文件。该文件包含每个打印机队列的一项条目。条目看起来类似以下内容：

```
epson:\
    :lp=/dev/lp0:\
    :rm=:\\
    :rp=:\\
    :sd=/var/spool/lpd/epson:\\
    :mx#0:\\
    :sh:\
    :if=/var/spool/lpd/epson/printfilter:
```

上述条目定义了一个名为 `epson` 的打印机队列。除最后一行外，该条目的每一行都以反斜杠 (\) 字符结尾。这个字符是“续行”字符——从技术上讲，每个 `/etc/printcap` 条目只占用一行，但以这种方式格式化较为不便。`/etc/printcap` 中的重要选项包括

- **`lp=`** 此行定义行式打印机设备——在本例中为 `/dev/lp0`。
- **`rm=`** 托管打印机的远程打印服务器名称。如果你使用的是带有以太网接口的打印服务器或打印机，请在此输入其机器名称或 IP 地址。
- **`rp=`** 远程打印服务器上的打印队列名称。

> **注意**
>
> 你可以*要么*通过 `lp=` 行定义本地打印机设备，*要么*通过 `rm=` 和 `rp=` 定义远程打印机设备。你可以省略与其中一种设备类型相关的选项。我在前面的示例中保留了这两个选项，以展示两种情况都是可能的。

- **`sd=`** 这是设备的暂存目录——即 `lpr` 放置你要打印文件的目录。
- **`mx#`** 这是最大作业大小，以千字节为单位。注意，此选项使用井号 (#) 代替了等号 (=)。
- **`sh`** 如果你想抑制页头页面，请包含此选项。如果没有此选项，`lpd` 会打印一个页头页面，其中标识提交打印作业的个人。
- **`if=`** 此行标识输入过滤器。大多数发行版使用暂存目录中的脚本来调用过滤器，并使用适当的选项来处理打印作业。如果你省略此行，`lpd` 将不使用过滤器；它会直接将结果传递给打印机。

配置打印机中许多棘手的部分在于设置打印过滤器。Linux 有多种可用的“智能过滤器”包。大多数 Linux 发行版都附带自己的过滤器包，因此你不需要安装任何特殊内容即可让过滤器与你的打印机队列配合工作。

事实上，大多数发行版都包含打印机配置实用程序，帮助你设置 `/etc/printcap` 文件和打印机过滤器配置的所有细节，包括 Ghostscript 选项。例如，图 20.5 展示了 Caldera COAS 实用程序的打印机配置区域。你可以使用下拉选项按钮选择选项，或直接输入数据字段，视情况而定。GUI 打印机配置实用程序的具体细节因发行版而异；例如，Red Hat 使用一个名为 `printtool` 的程序来执行此任务。

![](img/860d0c38bd76c9ded976e9d1e179ef25_571_0.png)

**图 20.5**  
*GUI 打印机配置实用程序通常允许你通过型号选择打印机，设置一些选项，而无需处理 Ghostscript 或打印机过滤器配置的细节。*

为了更深入地了解 Linux 打印机配置，有必要更多地了解 Ghostscript。Ghostscript 基本上是 PostScript 的第三方实现。与你在许多打印机中看到的第三方 PostScript 解释器不同，Ghostscript 运行在你的计算机上。你可以使用它在屏幕上查看 PostScript 文件，或在非 PostScript 打印机上打印 PostScript 文件。你可以在 http://www.cs.wisc.edu/~ghost 找到最新版本的 Ghostscript，包括完整文档。

# **注意**

Ghostscript 有两种形式。其中一种是 Aladdin Ghostscript，这是最新版本。Aladdin Ghostscript 对大多数用途是免费的，但如果没有向 Aladdin 支付许可费，就不能将其包含在任何收费软件包中。在 Aladdin Ghostscript 的某个版本发布一段时间后，该公司会将其许可证更改为 GNU 通用公共许可证 (GPL)，从而允许更广泛的分发。因此，Linux 发行版附带的是 GNU Ghostscript，也就是这种较旧的版本。在大多数情况下，GNU Ghostscript 就足够了，但如果你想使用最新功能，必须从其主要网站或其他网站获取 Aladdin Ghostscript。

Ghostscript 包含大量针对各种打印机、显示器和图形文件格式的驱动程序。这些驱动程序必须编译到 Ghostscript 二进制文件中，因此为了节省空间，大多数 Ghostscript 二进制版本省略了一些驱动程序。你可以通过输入 `gs -help` 来查看你的版本包含哪些驱动程序。这将产生输出，其中包含驱动程序列表，名称如 epson、laserjet、stcolor、pcx256、pngmon 和 pdfwrite 等。

不幸的是，Ghostscript 的设备名称可能有些晦涩，因此你可能需要咨询一些有用的资源来学习应使用哪个设备与你的打印机配合。最有用的单一资源是位于 http://www.picanite.com/~gtaylor/phl/printer_list.cgi 的 Printing HOWTO 支持数据库。该网站包含一个搜索引擎，让你可以找到关于特定打印机型号的意见，包括与给定打印机一起使用的 Ghostscript 驱动程序。

如果你发现你的 Ghostscript 二进制文件不包含对打印机的支持，你必须查找另一个 Ghostscript 二进制文件或自行编译。后者是一项极其繁琐的工作，因此我建议你寻找包含适当支持的二进制文件。分别在 http://rufus.w3.org/linux/RPM/ 或 http://www.debian.org/distrib/packages 上查看 RPM 或 Debian 软件包以获取 Ghostscript 二进制文件。我还发现 Ghostscript 5.10 的二进制 RPM 位于 http://www.users.dircon.co.uk/~typhoon/，非常完整，但现在既然 Ghostscript 6.0 已发布，这个来源可能不再那么吸引人。

![](img/860d0c38bd76c9ded976e9d1e179ef25_573_0.png)

你可以通过将 PostScript 文件传递给程序来检查基本的 Ghostscript 功能。（Ghostscript 附带多个示例 PostScript 文件，通常位于 /usr/share/ghostscript/x.yz/examples 目录中，其中 x.yz 是 Ghostscript 版本号。）你必须指定输出文件名、要使用的驱动程序以及其它各种选项，如下所示：

```
gs -dNOPAUSE -dBATCH -q -r100x100 -sDEVICE=png256 -sOutputFile=test.png test.ps
```

此命令从 test.ps 输入文件创建一个名为 test.png 的 PNG 文件。你可以使用 GIMP 等 Linux 图形程序查看 test.png。你可以更改设备驱动程序名称和分辨率（分别是 `-sDEVICE=` 和 `-r` 选项）以匹配你的打印机。然后你可以直接将文件发送到打印机设备，例如：

```
cat test.pcl > /dev/lp0
```

如果这产生了良好的打印效果，你可以配置打印机队列以使用这些选项来使用 Ghostscript。

# 在 Linux 打印机队列中使用 Ghostscript

在 Linux 中配置使用 Ghostscript 最简单的方法是使用你的发行版的打印机队列配置工具，例如 Caldera 的 COAS 或 Red Hat 的 printtool。但是，如果你需要查找新的 Ghostscript 驱动程序，那么你的发行版的工具可能尚未设置为处理该打印机，因此你可能需要手动编辑配置文件。我建议你先使用一个你不使用的打印机驱动程序创建打印机队列。然后你可以编辑此配置以使用正确的驱动程序。

你可能需要查找配置文件，这可能是一个繁琐的过程。你的起点是 /etc/printcap 及其 if= 行。该行上列出的文件通常是一个调用过滤器程序的脚本。此脚本可能会调用其他脚本或直接包含 Ghostscript 选项。你应该尝试查找这些脚本或配置文件。其中一个将包含你必须修改的 Ghostscript 选项。例如，Caldera 将有关要使用的打印机驱动程序的信息放在 /etc/sysconfig/printers 目录中的文件中。在 Red Hat 中，等效信息出现在 /var/spool/lpd/queuename/postscript.cfg 文件中，其中 queuename 是打印机队列的名称。

![](img/860d0c38bd76c9ded976e9d1e179ef25_573_1.png)

