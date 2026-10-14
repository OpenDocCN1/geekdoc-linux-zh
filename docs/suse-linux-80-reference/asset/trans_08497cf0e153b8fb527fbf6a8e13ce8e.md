
手动调整打印过滤器配置文件以添加任何特殊设置。每个队列都有自己独立的配置文件 `/etc/lpdfilter/queue/conf`（将这里的 queue 替换为实际的队列名称），其中还包含每个选项的信息。

## 向打印过滤器添加特殊设置

1. 如果打印数据不是 PostScript 格式，则默认情况下会使用 `/usr/lib/lpdfilter/filter/type2ps` 将其转换为 PostScript（将 type 替换为实际打印的数据类型）。如果有一个相应的脚本保存在 `/etc/lpdfilter/queue/type2ps`（将 queue 替换为实际的队列名称，将 type 替换为实际打印的数据类型），该脚本将用于将数据转换为 PostScript。此脚本从 stdin 接收打印数据，并将 PostScript 发送到 stdout。

2. 如果在 `/etc/lpdfilter/queue/pre` 中存在相应的脚本，则可以重新格式化 PostScript 数据。您也可以使用脚本为此目的添加自己的 PostScript 预加载。此脚本从 stdin 接收 PostScript 数据，并将 PostScript 输出发送到 stdout。可以在 `psutils` 软件包中找到用于重新格式化 PostScript 数据的程序。特别是 `pstops`，具有广泛的重新格式化功能。有关此方面的更多信息，请参阅 pstops 的手册页（man `pstops`）。

3. 特殊 Ghostscript 参数：使用 YaST2 配置时，运行 Ghostscript 的参数保存在 `/etc/lpdfilter/queue/upp` 文件中。也可以手动向此文件添加特殊 Ghostscript 参数。有关 Ghostscript 参数的更多信息，请参见第 215 页的 *关于 Ghostscript 的简要说明* 一节。

4. 如果在 `/etc/lpdfilter/queue/post` 中存在合适的脚本，也可以重新格式化 Ghostscript 的输出。此脚本从 stdin 接收 Ghostscript 输出，并将特定于打印机的数据发送到 stdout。

## 一个与硬件无关的示例

假设您希望一个名为 `test` 的队列打印带行号的 ASCII 文本，并将两页缩小到一页上。然后，您可以创建脚本 `/etc/lpdfilter/test/ascii2ps` 和 `/etc/lpdfilter/test/pre`：

```bash
#!/bin/bash
cat -n - | a2ps -1 --stdin=',' -o -
```

*文件 18：`/etc/lpdfilter/test/ascii2ps`：ASCII 到 PostScript 的转换*

```bash
#!/bin/bash
pstops -q '2:0L0.6(20cm,2cm)+1L0.6(20cm,15cm)'
```

*文件 19：`/etc/lpdfilter/test/pre`：重新格式化 PostScript*

这些脚本必须对所有用户可执行，可以通过以下命令实现：

```shell
earth:  # chmod -v a+rx /etc/lpdfilter/test/ascii2ps
earth:  # chmod -v a+rx /etc/lpdfilter/test/pre
```

pstops 命令仅适用于那些能够被重新格式化的 PostScript 文件（通常都是如此）。

## 使用自定义 PostScript 预加载

PostScript 预加载是包含特殊 PostScript 命令的小型 PostScript 文件。它们可以在实际打印数据之前被发送，以初始化 PostScript 打印机或 Ghostscript。

通常，PostScript 预加载用于在 PostScript 打印机中激活双面打印或特殊纸盒，或相应地设置 Ghostscript 的页边距和 Gamma 校正。

首先，PostScript 打印机或 Ghostscript 必须能够正确处理下面列出的特殊 PostScript 命令（Ghostscript 对双面打印或纸盒命令没有响应）。

假设所涉及的队列名为 test。

**双面打印** — 要启用或禁用双面打印，请创建文件 `/etc/lpdfilter/test/duplexon.ps` 和 `/etc/lpdfilter/test/duplexoff.ps`，内容如下：

```postscript
%!PS
statusdict /setduplexmode known
statusdict begin true setduplexmode end if pop
```

*文件 20：`/etc/lpdfilter/test/duplexon.ps`：启用双面打印*

```postscript
%!PS
statusdict /setduplexmode known
statusdict begin false setduplexmode end if pop
```

*文件 21：`/etc/lpdfilter/test/duplexoff.ps`：禁用双面打印*

**纸盒选择** — 例如，要激活默认纸盒（0）或 2 号纸盒，请创建文件 `/etc/lpdfilter/test/tray0.ps` 和 `/etc/lpdfilter/test/tray2.ps`，内容如下：

```postscript
%!PS
statusdict /setpapertray known
statusdict begin 0 setpapertray end if pop
```

*文件 22：`/etc/lpdfilter/test/tray0.ps`：激活 0 号纸盒*

```postscript
%!PS
statusdict /setpapertray known
statusdict begin 2 setpapertray end if pop
```

*文件 23：`/etc/lpdfilter/test/tray2.ps`：激活 2 号纸盒*

**页边距设置** — 要更改页边距设置，请创建文件 `/etc/lpdfilter/test/margin.ps`，内容如下：

```postscript
%!PS
<<
/.HWMargins [left bottom right top]
/PageSize [width height]
/Margins [left-offset top-offset]
>>
setpagedevice
```

*文件 24：`/etc/lpdfilter/test/margin.ps`：页边距设置*

页边距设置 left、bottom、right 和 top 以及纸张尺寸的 width 和 height 必须以点为单位指定，一个点为 1/72 英寸（约 0.35 毫米）。另一方面，页边距偏移量 left-offset 和 top-offset 应根据分辨率以点阵为单位指定。

如果只需要在纸张上移动打印输出的位置，以下文件就足够了：`/etc/lpdfilter/test/offset.ps`

```postscript
%!PS
<< /Margins [left-offset top-offset] >> setpagedevice
```

*文件 25：`/etc/lpdfilter/test/offset.ps`：打印输出的位置*

## Gamma 校正

要修改颜色的亮度范围，请创建文件 `/etc/lpdfilter/test/cmyk.ps` 和 `/etc/lpdfilter/test/rgb.ps`，内容如下：

```postscript
%!PS
cyan exp magenta exp yellow exp black exp setcolortransfer
```

*文件 26：`/etc/lpdfilter/test/cmyk.ps`：CMYK Gamma 校正*

```postscript
%!PS
red exp green exp blue exp currenttransfer setcolortransfer
```

*文件 27：`/etc/lpdfilter/test/rgb.ps`：RGB Gamma 校正*

颜色模型（CMYK 或 RGB）必须与打印机兼容。为青色、品红色、黄色、黑色、红色、绿色和蓝色设置的值必须介于 0.001 和 0.999 之间。

您可以通过以下命令（不使用 Gamma 校正）在图形界面中总体了解上述文件的效果：

```shell
earth:  # gs -r60 \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps
```

（使用 Gamma 校正时，以下任一示例均可）：

```shell
earth:  # gs -r60 /etc/lpdfilter/test/cmyk.ps \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps

earth:  # gs -r60 /etc/lpdfilter/test/rgb.ps \
    /usr/share/doc/packages/ghostscript/examples/colorcir.ps
```

使用 `Ctrl` + `C` 退出。

## 重置打印机

要恢复打印机的基本设置，请创建文件 `/etc/lpdfilter/test/reset.ps`，内容如下：

```postscript
%!PS
serverdict begin 0 exitserver
```

*文件 28：`/etc/lpdfilter/test/reset.ps`：重置打印机*

要激活 PostScript 预加载文件，请创建脚本 `/etc/lpdfilter/test/pre`，内容如下：

```bash
#!/bin/bash
cat /etc/lpdfilter/test/preload.ps -
```

*文件 29：`/etc/lpdfilter/test/pre`：加载 PostScript 预加载*

将 preload 替换为实际的预加载文件名。该脚本必须对所有用户可执行且可读，这可以通过 chmod 实现：

```shell
earth:  # chmod -v a+rx /etc/lpdfilter/test/pre
earth:  # chmod -v a+r /etc/lpdfilter/test/preload.ps
```

同样的机制也可以用于在实际 PostScript 打印数据之后向打印机发送 PostScript 文件。要在打印作业完成后恢复打印机的原始设置，请创建脚本 `/etc/lpdfilter/test/pre`，内容如下：

```bash
#!/bin/bash
cat /etc/lpdfilter/test/preload.ps - /etc/lpdfilter/test/reset.ps
```

*文件 30：`/etc/lpdfilter/test/pre`：PostScript 预加载与 PostScript 重置*

## 配置 GDI 打印机的示例

GDI 打印机通常无法在 Linux 中使用。请参见第 192 页的 *GDI 打印机* 一节。但是，某些 GDI 打印机有特殊的驱动程序应用程序。这些驱动程序应用程序通常通过将 Ghostscript 输出转换为打印机特定格式来补充 Ghostscript。此类驱动程序应用程序通常只允许有限的打印选项，例如仅黑白打印。因此，Ghostscript 和驱动程序应用程序按如下方式协同工作（另请参见第 215 页的 *关于 Ghostscript 的简要说明* 一节）：

1. Ghostscript 将 PostScript 数据解析为包含各个像素的矩阵。然后将矩阵数据以合适的格式和分辨率传递给相应的 Ghostscript 驱动程序。

2. 然后，驱动程序应用程序将矩阵数据转换为打印机特定格式。

