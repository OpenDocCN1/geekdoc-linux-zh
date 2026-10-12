
最初，PPD 仅用于 PostScript 打印机。在这里，它们有助于向 `RIP` 发送设备特定的命令和设置，而 `RIP` 负责处理任务文件。CUPS 已将 PPD 的范围扩展到涵盖非 PostScript 打印机。这并不困难，因为它是一种标准化的文件格式。从某种意义上说，这也是合乎逻辑的：CUPS 处理 PostScript 并使用 PostScript `RIP`（Ghostscript）来处理任务文件。唯一的区别在于，PostScript 打印机内置了 `RIP`，而对于其他类型的打印机，Ghostscript `RIP` 在主机计算机上运行。

非 PostScript 打印机的 PPD 包含几行 CUPS 特有的内容。最重要的一行看起来类似于：

```text
*cupsFilter: application/vnd.cups-raster 66 rastercprinter*
```

这是 CUPS 筛选拼图中的最后一块。这行告诉 CUPS 守护进程使用 `rastercprinter` 作为最后一个筛选器。该筛选器应接收 `application/vnd.cups-raster` MIME 类型文件作为输入。因此，CUPS 应自动构建一条筛选链，其最终输出为指定的 MIME 类型。然后，该输出作为指定的 `rastercprinter` 筛选器的输入。在最后筛选器完成其工作（`rastercprinter` 是一个 Gimp-Print 筛选器）之后，文件应交给后端，由其将其发送到输出设备。

CUPS 默认只附带几个通用的 PPD，但适用于数百种打印机型号。你可能无法控制不同的纸张托盘，或者可能获得比你的特定型号支持的更大的页边距。有关摘要信息，请参阅表 21.1。

### 21.5.16 `foomatic-rip` 与原生 CUPS 打印

原生 CUPS 光栅化分两步工作：

- 第一步是 `pstoraster` 阶段。它使用 ESP Ghostscript 7.05.x 的特殊 CUPS 设备作为工具。
- 第二步是 `rasterdriver` 阶段。它使用各种设备特定的筛选器；有几家供应商为该步骤提供了高质量的筛选器。有些是自由软件，有些是共享软件，有些是专有软件。

通常，这比其他方式产生更好的质量（并具有其他几项优势）。图 21.10 展示了这一点。

## 表 21.1 随 CUPS 提供的 PPD

| PPD 文件 | 打印机类型 |
|---|---|
| `deskjet.ppd` | 旧款 HP 喷墨打印机及兼容机 |
| `deskjet2.ppd` | 新款 HP 喷墨打印机及兼容机 |
| `dymo.ppd` | 标签打印机 |
| `epson9.ppd` | Epson 24 针点阵打印机及兼容机 |
| `epson24.ppd` | Epson 24 针点阵打印机及兼容机 |
| `okidata9.ppd` | Okidata 9 针点阵打印机及兼容机 |
| `okidata24.ppd` | Okidata 24 针点阵打印机及兼容机 |
| `stcolor.ppd` | 旧款 Epson Stylus Color 打印机 |
| `stcolor2.ppd` | 新款 Epson Stylus Color 打印机 |
| `stphoto.ppd` | 旧款 Epson Stylus Photo 打印机 |
| `stphoto2.ppd` | 新款 Epson Stylus Photo 打印机 |
| `laserjet.ppd` | 所有 PCL 打印机 |

## 图 21.10 foomatic-rip 处理与原生 CUPS 对比。

![](img/86d74c6cc862465e3a42e6dc3c90935a_430_0.png)

另一种方法是 `foomatic-rip` 方式。请注意，`cupsmatic` 并非由 CUPS 开发人员制作。它是一项独立的打印开发贡献，*由* Linuxprinting.org 的人员*制作*。`6` `cupsmatic` 不再得到开发或维护。

`6` 另见 <http://www.cups.org/cups-help.html>

它也不受支持。它现在已被 `foomatic-rip` 取代。`foomatic-rip` 是旧的 `cupsomatic` 概念的彻底重写，但得到了极大的改进并推广到其他（非 CUPS）假脱机程序。强烈建议升级到 `foomatic-rip`，尤其是当你也升级到最新版本的 CUPS 时。

与旧的 `cupsomatic` 方法类似，Linuxprinting.org 的 `foomatic-rip`（新）方法使用传统的 Ghostscript 打印文件处理，在单一步骤中完成所有工作。因此，它依赖于 Ghostscript 内置的所有其他设备。其质量与其他假脱机程序中 Ghostscript 渲染的质量一样好（或坏）。其优势在于，该方法支持许多尚未被更现代的 CUPS 方法支持的打印机型号。

当然，你可以在一个系统上（甚至对于一个打印机，如果你设置了不同的队列）同时使用这两种方法，并找出哪种最适合你。

`cupsomatic` 在 `application/vnd.cups-postscript` 阶段之后拦截打印文件，并使其偏离通过 CUPS 外部、系统范围的 Ghostscript 安装进行处理。因此，打印文件绕过了 `pstoraster` 筛选器（同时也绕过了 CUPS 光栅驱动 `rastertosomething`）。在 Ghostscript 完成其光栅化后，`cupsomatic` 将渲染后的文件直接交给 CUPS 后端。图 21.10 展示了原生 CUPS 渲染与 Foomatic/`cupsomatic` 方法之间的区别。

## 21.5.17 筛选链示例

以下是一些常见筛选链的示例，以说明 CUPS 的工作机制。

假设你想将一个 PDF 文件打印到通过 HP JetDirect 连接的 PostScript 打印机，但你只想打印第 3-5、7 和 11-13 页，并且想以“两页一页”（two-up）和“双面打印”（duplex）的方式打印：

- 你的打印选项（所需的页面选择、两页一页、双面打印）在命令行上传递给 CUPS。
- （完整的）PDF 文件发送到 CUPS，并被自动类型识别为 `application/pdf`。
- 因此，文件必须首先经过 `pdftops` 前筛选器，生成 PostScript MIME 类型 `application/postscript`（在此处的预览仍会显示原始 PDF 的所有页面）。
- 然后文件经过 `pstops` 筛选器，该筛选器应用命令行选项：它选择第 3-5、7 和 11-13 页，创建拼版布局：“一页放两页”，并将正确的“双面打印”命令（在打印机的 PPD 中定义）插入新的 PostScript 文件；该文件现在是 PostScript MIME 类型 `application/vnd.cups-postscript`。
- 文件发送到 `socket` 后端，该后端将任务传输到打印机。

因此，生成的筛选链如图 21.11 所示。

假设你想将相同的文件打印到通过 USB 连接、安装了 CUPS `stpho02.ppd` 的 Epson Stylus Photo 打印机。前几个筛选阶段几乎相同：

### 21.5 CUPS 过滤架构

### 图 21.11 PDF 到 Socket 链路。

![](img/86d74c6cc862465e3a42e6dc3c90935a_432_0.png)

- 你的打印选项（如所需的页面选择、双拼、双面打印）通过命令行传递给 CUPS。
- （完整的）PDF 文件被发送到 CUPS，并自动识别为 `application/pdf`。
- 文件必须首先通过 `pdftops` 预过滤器，该过滤器生成 PostScript MIME 类型 `application/postscript`（此处预览仍将显示原始 PDF 的所有页面）。
- 文件随后通过 `pstops` 过滤器，该过滤器应用命令行选项：它选择第 2-5、7 和 11-13 页，创建“每页两页”的排版布局，并在新 PostScript 文件中插入正确的“双面”命令（哎呀——此打印机和 PPD 根本不支持双面打印，因此该选项将被忽略）；此时文件的 PostScript MIME 类型变为 `application/vnd.cups-postscript`。
- 文件随后通过 `pstoraster` 阶段，变为 MIME 类型 `application/cups-raster`。
- 最后，`rastertoepson` 过滤器执行其工作（如打印机 PPD 中所示），创建打印机特定的光栅数据，并将用户选择的打印选项嵌入打印数据流中。
- 文件进入 USB 后端，后端将任务传输到打印机。

因此，生成的过滤器链如图 21.12 所示。

### 图 21.12 PDF 到 USB 链路。

![](img/86d74c6cc862465e3a42e6dc3c90935a_432_1.png)
