
# make install clean

同样，`freep`或其他集合也是如此。为了让 X Server 检测到这些字体，请在 `/etc/X11/xorg.conf`（针对 Xorg）或 `XF86Config`（针对 XFree86）的 X Server 配置文件中添加适当的行，内容如下：

```
FontPath "/usr/X11R/lib/X11/fonts/URW/"
```

或者，在 X 会话的命令行中：

```
% xset fp+ /usr/X11R/lib/X11/fonts/URW
```

```
% xset refresh
```

当 X 会话关闭时，这些更改将会丢失，除非将其添加到普通 `startx` 会话的启动文件（`~/.xinitrc`）中，或者登录到像 `XDM` 这样的图形登录管理器。第三种方法是使用新的 `/usr/X11R6/etc/fonts/local.conf` 文件：请参见抗锯齿章节。

### 5.5.2 TrueType 字体

`XFree86` 4X 和 `Xorg` 都内置了对 TrueType 字体的支持。有两个不同的模块可以启用此功能。示例中使用了 `freetype` 模块，因为它与其他字体后端更一致。要启用 `freetype` 模块，只需在 `/etc/X11/xorg.conf` 或 `/etc/X11/XF86Config` 文件的 "Module" 部分添加以下行：

```
Load "freetype"
```

对于 `XFree86` 3.3.X，TrueType 字体格式必须嵌套。通常为此目的使用 `xft`。要安装 `xft`，只需安装 `port x11-servers/xft`。现在为字体创建一个目录（例如 `/usr/X11R6/lib/X11/fonts/TrueType`），并将所有 TrueType 字体复制到该目录。注意，TrueType 字体不能直接从 Macintosh 获取；它们必须是 UNIX 格式。一旦文件复制到此目录，使用 `mkfontdir` 创建 `.dir` 文件，以便字体渲染器知道这些新文件已安装。`mkfontdir` 可从 FreeBSD Ports `x11-fonts` 获取。

```
# cd /usr/X11R6/lib/X11/fonts/TrueType
# mkfontdir
```

现在，将 TrueType 目录添加到字体路径。这与上述 Type1 字体的方法相同：

```
# xset fp+ /usr/X11R6/lib/X11/fonts/TrueType
# xset refresh
```

或向 `xorg.conf`（或 `XF86Config`）文件添加 `FontPath` 行。这就完成了。现在 `Netscape`、`Gimp`、`StarOffice` 以及其他 X 应用程序应该能够识别 TrueType 字体。小字体（在高分辨率显示器上）和巨大的字体（在 StarOffice 中）看起来会好得多。

### 5.5.3 抗锯齿字体

由 Marcus Clarke 更新

抗锯齿从 `XFree86` 4.0.2 开始可用但在 `XFree86` 4.3.0 引入之前，字体配置非常困难。从 `XFree86` 开始，`/usr/X11R6/lib/X11/fonts/` 和 `~/fonts/` 中的所有字体自动可用抗锯齿。并不是所有应用程序都支持 `xft`，但许多程序已获得 `xft` 支持。支持 `xft` 的示例包括 `Qt` 2.3 及以上（`KDE` 桌面）、`GTK+` 2.0 及以上（`GNOME` 桌面）以及 `Mozilla` 1.2 及以上。

为了控制哪些 X11 字体抗锯齿，或配置抗锯齿属性，请创建（如果存在则编辑）文件 `/usr/X11R6/etc/fonts/local.conf`。`Xft` 系统的某些高级功能可以使用此文件进行调整；此章节描述了一些可能性。此文件为 XML 格式。请仔细注意，并确保所有标签都正确关闭。文件以 XML 头开头，随后是 DOYPE 定义，然后是 `<fontconfig>` 标签：

```xml
<?xml version="1.0"?>
<!DOCTYPE fontconfig SYSTEM "fonts.dtd">
<fontconfig>
```

如之前所述，`/usr/X11R6/lib/X11/fonts/` 和 `~/fonts/` 中的所有字体已经可用。如果你想添加另一个目录，可以在 `/X11R6/etc/fonts/local.conf` 中添加如下行：

```
<dir>/path/to/my/fonts</dir>
```

在添加新字体（或更新）后，你应该运行以下命令来重建字体缓存：

```
# fc-cache -f
```

抗锯齿会让边缘变得模糊，这使得小字体更容易读并消除大文本的“阶梯感”，但如果应用于普通文本则可能会导致疲劳。要排除小于 14 的字号抗锯齿，请包含这些行：

```
<match target="font">
  <test name="size" compare="less">
    <double>14</double>
  </test>
  <edit name="antialias" mode="assign">
    <bool>false</bool>
  </edit>
</match>
<match target="font">
  <test name="pixelsize" compare="less" qual="any">
    <double>14</double>
  </test>
  <edit name="antialias" mode="assign">
    <bool>false</bool>
  </edit>
</match>
```

等宽字体的间距在抗锯齿下也可能不合适。这似乎是 `KDE` 特有的问题。一种可能的解决方法是将此类字体的间距固定为 100。添加以下行：

```
<match target="pattern">
  <test qual="any" name="family">
    <string>fixed</string>
  </test>
  <edit name="family" mode="assign">
    <string>mono</string>
  </edit>
</match>
<match target="pattern">
  <test qual="any" name="family">
    <string>console</string>
  </test>
  <edit name="family" mode="assign">
    <string>mono</string>
  </edit>
</match>
```

（这会将常见的字体别映射为 "mono"），然后添加：

```
  <edit name="spacing" mode="assign">
    <int>100</int>
  </edit>
```

某些字体（如 Helvetica）在抗锯齿时可能会出现问题。这通常表现为字体垂直断裂。在最坏的情况下，它可能会导致 `Mozilla` 等程序崩溃。为了避免这种情况，请考虑在 `local.conf` 中添加以下内容：

一旦你编辑完 `local.conf`，你可能会发现文件缺少 `<fontconfig>` 标签。不这样做会导致你的更改被忽略。

最后，用户可以通过其个人的 `.fonts.conf` 文件添加自己的设置。为了这样做，每个用户应该创建一个 `~/.fonts.conf`。该文件也必须是 XML 格式。

最后一点：对于 LCD 屏幕，可能需要子像素采样。这基本上是单独处理（水平分离的）红、绿、蓝分量以提高水平分辨率；效果可能是显著的。要启用此功能，在 `local.conf` 文件的某处添加该行：

```
<match target="font">
  <test qual="all" name="rgba">
```

```xml
<const>unknown</const>
<test>
<edit name="rgba" mode="assign">
<const>rgb</const>
</edit>
</match>
```

**注意：** 根据显示类型，`rgb` 可能需要更改为 `bgr`、`vrgb` 或 `vbgr`；请尝试并查看哪种效果最好。

在下次启动 X 服务器时，应该启用抗锯齿。然而，程序必须知道如何利用它。目前，X 工具包已经支持这一点，因此整个 `KDE` 环境都可以使用抗锯字体。`GTK+` 以及 `GNOME` `Mozilla` 1.2 及更高版本将自动使用抗锯齿。默认情况下，请使用 `-WITHOUT_XFT` 标志重新编译。

### 5.6 X 显示管理器

由 Seth Kingsley 贡献。

### 5.6.1 概述
