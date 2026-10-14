

## 20. 导入图像

虽然你总可以自己制作图像，但有时你可能想从其他来源导入并使用现有图像。在本章中，我将展示如何从扫描仪和 Kodak PhotoCD 光盘导入图像。我们将从截屏的配方开始。

### 20.1 截屏
截屏。
### 20.2 扫描图像
使用扫描仪扫描图像。
### 20.3 提取 PhotoCD 图像
从 Kodak PhotoCD 上获取图像。

## 20.1 截屏

截屏是显示屏全部或部分的图片。下面的配方展示了如何在 X 和控制台中截屏。

### 20.1.1 在 X 中截屏
截取 X 屏幕截图。
### 20.1.2 在控制台中截屏
截取控制台屏幕截图。

## 20.1.1 在 X 中截屏

```
@sf(Debian): `imagemagick`
@sf(WWW): `ftp://ftp.wizards.dupont.com/pub/ImageMagick/`
```

使用 ImageMagick 套件的一部分 import 在 X 中截屏。import 可以捕获整个屏幕、单个窗口或任意矩形区域，并将要保存到的文件名作为参数。与其他 ImageMagick 工具一样，输出文件的图像格式取决于你指定的文件扩展名：`.eps` 用于 EPS，`.tiff` 用于 TIFF，`.jpeg` 用于 JPEG，等等。（完整列表请参见 Converting Images between Formats）。

在你发出命令后，鼠标指针会变成一组十字准线。然后你使用鼠标指定要截屏的窗口，如下所示：

## 20.2 扫描图像

```
@sf(Debian): `sane`
@sf(WWW): http://www.mostang.com/sane/
```

SANE，“Scanner Access Now Easy”，是事实上的 Linux 扫描仪接口；使用它可以用扫描仪扫描图像并将其保存到文件中。

SANE 可与各种扫描硬件配合使用，但请确保你想要使用的扫描硬件是兼容的，可以通过检查 Hardware HOWTO 和 SANE 的支持扫描仪列表来确认。

一旦 SANE 运行起来，你就可以使用 SANE 感知的应用程序（如 GIMP（参见 section Editing Images with the GIMP））来扫描图像。

下面的配方描述了命令行 scanimage 工具的使用，该工具随 SANE 包提供。

> 注意：正如缩写所暗示的那样，让扫描仪在 Linux 系统上工作并不总是顺利。SANE 接口完全开放，其开发人员正在确保它足够通用，可以在任何硬件或操作系统上实现。

- 20.2.1 列出可用扫描仪设备 列出可用扫描仪。
- 20.2.2 测试扫描仪 测试扫描仪。
- 20.2.3 扫描图像 扫描图像。

## 20.2.1 列出可用扫描仪设备

在使用扫描仪设备之前，你需要知道其设备名称。要获取此名称，请使用带有 `--list-devices` 选项的 scanimage。

- 要列出可用的扫描仪设备，请输入：

```
$ scanimage --list-devices RET
device `unix:/dev/sgb' is a UMAX Astra 1220S flatbed scanner
$
```

在此示例中，该系统上有一个扫描设备，即 UMAX 品牌的扫描仪，可以通过将其设备名称 `umax:/dev/sgb` 作为 `-d` 选项的参数提供给 scanimage 来指定。

要列出特定设备支持的可用分辨率和选项，请使用 `--help` 选项以及 `-d` 选项后跟其设备名称。

- 要列出前一个示例中列出的设备支持的可用选项，请输入：

```
$ scanimage --help -d 'umax:/dev/sgb' RET
```

> 注意：对于所有 scanimage 命令，请通过包含 `-d` 选项并附上设备名称来指定要使用的扫描仪设备。

## 20.2.2 测试扫描仪

要对扫描仪运行诊断测试以确保可以正确读取它，请使用带有 `--test` 选项的 scanimage。

- 要测试前面列出的 UMAX 扫描仪，请输入：

```
$ scanimage --test -d 'umax:/dev/sgb' RET
```

## 20.2.3 扫描图像

@sf(Debian): `netpbm`
@sf(WWW): http://www.debian.org/Packages/stable/graphics/netpbm.html

使用 scanimage 扫描图像。大多数扫描仪允许你指定图像大小的 x 和 y 值，以像素为单位，从扫描仪平台的左上角开始。将这些坐标作为 `-x` 和 `-y` 选项的参数给出。此外，给 `--resolution` 选项一个参数来指定扫描分辨率，以 dpi（“每英寸点数”）为单位。常见的分辨率值包括 72、120、300 和 600 dpi；72 dpi 是在 Web 上使用或在屏幕上查看时最流行的分辨率，而 204 dpi 通常用于你想要发送到传真机的图像。

扫描输出发送到标准输出，因此要将图像扫描到文件中，请重定向标准输出。

scanimage 以 PNM（“便携式任意图”）格式输出图像，因此请确保你拥有

