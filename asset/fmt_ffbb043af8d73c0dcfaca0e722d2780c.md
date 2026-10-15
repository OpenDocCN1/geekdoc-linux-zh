
## Ghostscript 目录的内容

![](img/e8e6b47ac20475e23d48b4c476f5d891_463_0.png)

Ghostscript 所需的所有字体都存储在主 Ghostscript 目录下的某个目录中，在本例中为 `/usr/local/ghostscript/3.33/fonts`。大多数发行版都包含大量字体。

如果您的 Linux 版本未包含 Ghostscript 实用程序的副本，您可以从 Linux 的任何标准发行点下载该集合。请参阅第 2 章“Linux 类型”以了解如何获取发行版。您也可以从 Aladdin Enterprises 获取 Ghostscript 集合。

## 使用 Ghostscript

Ghostscript 集合中的主要程序是 `gs`，它是 Ghostscript 解释器。`gs` 实用程序读取您告诉它的任何文件，并为您解释它们，在 X 窗口中显示格式正确的文档。从字符终端运行 `gs` 几乎不起作用，因为需要图形窗口来显示其操作结果。

要在 X 窗口中显示一个或多个文件，请输入以下命令，其中 `file1.ps` 是文件名（通常带有 .ps 扩展名，以显示它是 PostScript 格式文件）：

```
gs file1.ps
```

您可以指定多个文件名，每个文件将按顺序显示。当您输入 `gs` 命令时，您会看到一条类似“正在初始化...”的消息以及来自 Ghostscript 解释器的一系列消息，然后一个包含文件内容的窗口将打开。确切的 X 窗口消息和外观因您的 Ghostscript 版本而异。图 24.2 显示了在 Xterm 中输入 `gs` 命令时的输出，图 24.3 显示了 Ghostscript 显示的窗口，其中选定的文件内容被正确格式化。

![](img/e8e6b47ac20475e23d48b4c476f5d891_464_0.png)

如果您想抑制 Ghostscript 生成的所有消息（如图 24.2 所示），请使用 `-q`（安静）选项，该选项将抑制除主要消息以外的所有消息。

您可以通过 man 页面获取有关 `gs` 命令的帮助，这些页面通常难以阅读，或者使用 `-h` 或 `?` 选项从命令行获取。当您使用任一选项时（两者显示相同的屏幕输出），您将看到 `gs` 命令的所有可用选项和命令用法。由于帮助屏幕的输出超过一页，您应该将输出通过管道传输到 `more` 命令，如下所示：

```
gs -h | more
```

您将看到如图 24.4 中的屏幕。要移动到下一页帮助，请按空格键。要退出 `more` 实用程序，请使用 `q` 命令或 Ctrl+C。

## 为 X 配置 Ghostscript

某些 Linux 版本预装了经过修改的 X 系统以处理 Ghostscript 输出，但大多数并未这样做。Ghostscript 使用一组 X 资源，这些资源通常存储为程序名 `ghostscript` 和类名 `Ghostscript` 在 `.Xdefaults` 文件中。您的 `.Xdefaults` 文件至少应有三项条目，如下所示：

```
Ghostscript*geometry:             -0+0
Ghostscript*xResolution:        72
Ghostscript*yResolution:        72
```

如果这些条目缺失于您的 `.Xdefaults` 文件中，请使用编辑器输入它们，并通过重启服务器或发出以下命令（假设您在您的主目录中）重新加载默认设置：

```
xrdb -merge ./.Xdefaults
```

如果没有，请指定您的 `.Xdefaults` 文件的路径。

图 24.3。 Ghostscript 在窗口中显示 PostScript 文件供您直接查看。

![](img/e8e6b47ac20475e23d48b4c476f5d891_465_0.png)

图 24.4。 使用 more 命令显示 gs 命令的帮助屏幕。

![](img/e8e6b47ac20475e23d48b4c476f5d891_465_1.png)

Ghostscript 可以利用 `.Xdefaults` 文件中的许多资源，但由于默认设置效果良好，大多数对您没什么用。可以在 Ghostscript 中设置资源如表 24.1 所示。

### 表 24.1. GHOSTSCRIPT 支持的 X 资源。

| 资源名称 | 资源类 | 默认值 |
| :--- | :--- | :--- |
| background | Background | 白色 |
| foreground | Foreground | 黑色 |
| borderColor | BorderColor | 黑色 |
| borderWidth | BorderWidth | 1 |
| geometry | Geometry | NULL |
| xResolution | Resolution | 计算得出 |
| yResolution | Resolution | 计算得出 |
| useExternalFonts | UseExternalFonts | true |
| useScalableFonts | UseScalableFonts | true |
| logExternalFonts | LogExternalFonts | false |
| externalFontTolerance | ExternalFontTolerance | 10.0 |
| palette | Palette | Color |
| maxGrayRamp | MaxGrayRamp | 128 |
| maxRGBRamp | MaxRGBRamp | 5 |
| useBackingPixmap | UseBackingPixmap | true |
| useXPutImage | UseXPutImage | true |
| useXSetTitle | UseXSetTitle | true |
| regularFonts | RegularFonts | none |
| symbolFonts | SymbolFonts | none |
| dingbatFonts | DingbatFonts | none |

## 重定向 Ghostscript 输出

Ghostscript 允许您将输出重定向到其他设备时具有相当大的灵活性。在命令行上，您可以使用 `-sDEVICE` 选项指定打印机等设备。例如，如果您有一个名为 `HPLaser` 的设备，您可以使用以下命令将 `gs` 命令的输出重定向到该打印机：

```
gs -sDEVICE=HPLaser filename.ps
```

如果您发出此命令，您不会在窗口中看到任何输出，因为输出已被重定向。如果您在命令行上指定了多个文件，如下例所示，所有文件都将发送到 `HPLaser`：

```
gs -sDEVICE=HPLaser file1.ps file2.ps file3.ps
```

重定向一直有效，直到命令终止。当然，您重定向到的设备必须存在，否则 `gs` 将返回“未知设备”消息。您可以使用以下命令查看所有已知设备的列表：

```
gs -h
```

屏幕上的很大一部分（如图 24.4 所示）列出了 Ghostscript 知道的设备。

您可以利用参数顺序对 Ghostscript 进行一些操作。由于参数给出的顺序对 Ghostscript 很重要，您可以发出如下命令，该命令在您的 X 会话中显示 `file1.ps` 和 `file2.ps`，然后将 `file3.ps` 发送到设备 `HPLaser`：

```
gs file1.ps file2.ps -sDEVICE=HPLaser file3.ps
```

如果需要，您可以在命令行上多次更改设备，因此下一个命令将把 `file1.ps` 发送到设备 `HPLaser`，把 `file2.ps` 发送到设备 `CanonBJet`：

```
gs -sDEVICE=HPLaser file1.ps -sDEVICE=CanonBJet file2.ps
```

在某些情况下，直接发出单独的命令可能更容易；否则 `gs` 命令行会变得相当复杂。

Ghostscript 还内置了其他几种功能用于修改输出设备。如果您拥有一台较旧的点阵打印机，并且它支持多种分辨率（如草稿模式和最终模式），您可以定义不同的选项让 Ghostscript 触发相应的设备。例如，以下命令告诉 Ghostscript 使用可用的最高分辨率（24 针）在 Epson 设备上打印：

```
gs -sDEVICE=Epson -r360x180
```

由于这些较旧的硬件设备正在逐渐消失，这些命令选项也很少被普遍使用。

如果出于某种原因您不想使用打印机或屏幕作为输出，您可以使用 `-sOutputFile` 选项重定向 Ghostscript 的输出，方法如下：

```
gs -sOutputFile out1.ps file1.ps file2.ps
```
