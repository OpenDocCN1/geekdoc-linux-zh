

将它们放在引号中。`display` 会生成指定图像的缩略图，并在一个新窗口中显示，该窗口被称为可视化图像目录。

⇒ 以下是两种使用方式。

-   要浏览 `/usr/doc/imagemagick/examples` 目录下具有 `.gif` 扩展名的图像文件，请键入：
    `$ display 'vid:/usr/doc/imagemagick/examples/*.gif' [RET]`
-   要浏览当前目录中的所有图像文件，请键入：
    `$ display 'vid:*' [RET]`

在前面的示例中，只会读取并显示那些 `display` 所支持的图像格式的文件。

注意：如果标题栏显示可视化图像目录有多页，请按 [SPACEBAR] 前进到下一页（在最后一页按 [SPACEBAR] 会循环回到开头）。

要以正常大小打开图像，请右键单击图像并选择“加载”：缩略图将被其全尺寸图像替换。要返回缩略图目录，请按 [SPACEBAR]。

### 17.1.2 将图像放入根窗口

将图像放入根窗口（所有其他窗口后面的背景）的一种方法是使用 `display`，并将 'root' 作为 `-window` 选项的参数。

⇒ 要将图像 tetra.jpeg 放入根窗口，请键入：
`$ display -window root tetra.jpeg [RET]`

## 17.2 在控制台中浏览图像

Zgv  
DEB: zgv  
RPM: zgv  
WWW: http://freshmeat.net/projects/zgv/

使用 zgv 在虚拟控制台（而非 X 窗口系统）中查看图像。你可以使用 zgv 浏览文件系统并选择要查看的图像，也可以将特定图像文件的名称作为参数给出。它能识别多种图像格式，包括 GIF、JPEG、PNG、PBM/PNM/PPM、TGA 和 PCX；它最好的特性之一是能将图像填满整个屏幕。

当你不带选项运行 **zgv** 时，它会显示当前目录中所有图像的图标，并将任何子目录显示为文件夹图标。你也可以将目录名称作为参数，以便浏览该目录中的图像。

⇒ 以下是两种使用方式。

-   要浏览当前目录中的图像，请键入：
    `$ zgv [RET]`
-   要浏览 `/usr/share/gimp/scripts` 目录中的图像，请键入：
    `$ zgv /usr/share/gimp/scripts [RET]`

使用方向键在文件显示中导航；图像或目录图标周围的红色边框表示当前选中的图像或子目录。键入 [RET] 可查看选中的图像或进入选中的目录。

你可以通过多种方式操作所查看的图像——放大和缩小图像，调整亮度和颜色，甚至自动播放图像的“幻灯片”。下表描述了 **zgv** 的一些命令行选项。

| | |
|---|---|
| -c | 切换图像居中。默认情况下图像在屏幕上居中；指定此选项将关闭居中。 |
| -i | 忽略由于文件损坏而产生的错误，并显示文件中可显示的部分。 |
| -l | 以幻灯片模式启动 **zgv**，它会循环显示所有作为参数指定的图像，直到你中断它。 |
| -M | 切换鼠标支持。鼠标支持默认关闭；此选项将其开启。 |
| -r *整数* | 每 *整数* 秒重新读取并重新显示每个图像。适用于查看网络摄像头图像或其他不断变化的图像文件。 |

## 17.3 在 Web 浏览器中查看图像

Lynx  
DEB: lynx  
RPM: lynx  
WWW: http://lynx.browser.org/

或

Mozilla  
DEB: mozilla-browser  
RPM: mozilla  
WWW: http://www.mozilla.org/

浏览器非常适合浏览文件和目录，它们同样擅长显示图像。你可以在运行于 X 环境中的 Web 浏览器中浏览本地图像，就像浏览任何文件一样（参见第 5.10 节“浏览文件和目录”，第 157 页）。如果你在 X 环境中想要查看图像文件，并且有 Web 浏览器正在运行，这会是一种快速简便的方法。

你可以使用图形浏览器（如 Mozilla），或在终端窗口中使用基于文本的浏览器 Lynx 以这种方式查看图像，在这种情况下，图像会通过“辅助”应用程序在新窗口中显示。¹ 退出辅助应用程序将返回 Lynx。

要在 Mozilla 或其他图形 Web 浏览器中查看图像文件，请在浏览器的“位置”字段中指定图像文件的完整路径名。要在 Lynx 中查看图像文件，只需将图像的完整或相对路径名作为参数给出，或者在 Lynx 中键入 *g* 以获取提示，然后键入完整路径名。

⇒ 以下是几种使用方式。

-   要使用文件 `/usr/share/doc/texmf/pdftex/base/pic.png` 启动 Mozilla，请键入：
    `mozilla /usr/share/doc/texmf/pdftex/base/pic.png`
-   要在 Mozilla 中查看文件 `/usr/share/doc/texmf/pdftex/base/pic.png`，请在其“位置”字段中键入：
    `/usr/share/doc/texmf/pdftex/base/pic.png`

> `display` 工具通常是查看图像的默认应用程序。

