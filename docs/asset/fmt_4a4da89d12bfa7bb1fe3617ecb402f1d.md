
# 254 第 7 章 桌面级 Linux：处理图形和 GUI 应用程序

## X 窗口中的字体

与其他窗口系统一样，X 包含了字体。字体非常多，有成千上万个。你可以通过此命令查看所有字体：

```
xlsfonts | less
```

你通过 `-fn` 选项告诉 X 应用程序使用它们。例如，在 RedHat 7.3 系统上，你可以输入

```
xedit -fn -adobe-times-medium-r-normal--20-140-100-100-p-96-iso8859-1
```

此时 `xedit` 不会以其通常的类 Courier 字体显示，而是以 Times Roman 字体显示。注意字体的名称由 13 部分组成：

- 第一个字段 `adobe` 标识创建者。
- 第二个字段 `times` 描述字体族。其他常见的字体族包括 `helvetica`、`courier`、`symbol`、`lucida`、`arial`，任何 Microsoft 操作系统用户都应该熟悉这些名称。
- 第三个字段 `medium` 描述字体的粗细或“亮度”。其他典型值包括 `bold`、`black`、`light`、`regular` 和 `demibold`。
- 第四个字段 `r` 描述倾斜度——字体是斜体（i）还是不是斜体（r）。还有一个 `v`，它似乎能产生斜体并在行间留出额外的空间。Dan 告诉我可以把这归因于排字字体；某些字体没有斜体字，而是倾斜字，因此用了 `o`。
- 第五个字段 `normal` 描述字体的水平宽度。其他值包括 `narrow`、`condensed`、`semi-condensed` 和 `bold`。是的，`bold` 作为一个选项确实很奇怪，因为第三个字段已经涵盖了它。
- 第六个字段是空的，因此两个横线紧挨在一起。它将填充一个描述任何“额外”样式的值。它在许多字体上不使用，但典型值是 `medium` 或 `sans`。
- 第七个字段 `20` 描述字符的像素最大高度。
- 第八个字段 `140` 描述字符的最大高度，以排字单位磅（point）为，，磅是 1/72 英寸。
- 第九和第十个字段 `100` 和 `100` 描述该字体所基于的打印字体水平和垂直尺寸（每英寸点数）。
- 第十一个字段 `p` 表示它是比例字体。另一种是等宽字体或单间字体，用 `m` 表明。
- 第十二个字段 `96` 是字体的平均宽度，单位是像素的十分分之一。
- 最后一个字段 `iso8859-1` 描述字符集。

如果你喜欢，可以将其中任何字段替换为星号 `*`，X 将替换任何符合提及标准的字体。如果你想看看字体看起来像什么样，可以使用名为 `xfd` 的程序配合 `-fn` 选项，如下所示：

```
xfd -fn-adobe-medium-r-normal--20-140-100-100-p-96-is08859-1
```

`xfd` 并不是唯一让你玩字体的程序；还有 `xfontsel` 和 `showfont`。

字体、颜色、偏移量等在 X 中被统称为“资源”`resources`。现在你已经理解了从 X 的角度来看“资源”的含义，稍后我们处理 X 配置文件时就会变得更容易了。在下一节中，我将向你展示如何改进 GUI 程序的外观。

> TIP 你可能在 wonder 是否可以在 X 程序启动后更改其资源。例如，一旦通过 `xinit` 出现的 `xterm` 会话运行，你如何更改该窗口的字体大小？据我所知，没有简单的方法可以做到。但较新的程序可能通过其用户界面暴露了更改颜色、字体等方法。

## 安装 TrueType 字体

你可能已经注意到 Linux 自带的字体比你习惯的 TrueType 字体边缘更粗糙。没问题——Red Hat 7.3 支持 TrueType 字体。只需提前获取一些——你可以在 http://www.microsoft.com/typography/links/links.asp?type=free&part=1 找到多个免费字体源的链接。以下是安装方法。

1. 获取一些 TrueType 字体并将它们复制到 `/usr/X11R6/lib/X11/fonts/TTF`。
2. 进入该目录：
   `cd /usr/X11R6/lib/X11/fonts/TTF`
3. 为字体系统创建比例指南：
   `tmkfdir > fonts.scale`
4. 将该文件复制到 `fonts.dir`：
   `cp -f fonts.scale fonts.dir`
   你可能还需要在重启之前将此目录添加到 xfs 字体路径，否则它看不到任何 TrueType 字体。在 `/etc/X11/XF86Config-4` 中，在 `Files` 部分添加如下的一行：
   `FontPath "usr/X11R6/lib/X11/fonts/TTF/*"`
5. 重启字体系统：
   `/etc/rc/init.d/init restart`

如果你在带有 Windows 的电脑上运行 Linux，且 Windows 是 FAT 或 FAT32 分区，那么就更简单了。

1. 首先，挂载驱动器。
2. 编辑 `/etc/X11/XF86Config-4`。
3. 在 `Files` 部分下，添加如下的一行：
4. FontPath "usr/X11R6/lib/X11/fonts/TTF/*"
5. 重启字体系统：
   `/etc/rc/init.d/init restart`

如果你在带有 Windows 的电脑上运行 Linux，且 Windows 是 FAT 或 FAT32 分区，那么就更简单了。

1. 首先，挂载驱动器。
2. 编辑 `/etc/X11/XF86Config-4`。
3. 在 `Files` 部分下，添加如下的一行：
4. FontPath "usr/X11R6/lib/X11/fonts/TTF/*"
5. 重启字体系统：
   `/etc/rc/init.d/init restart`

如果你在带有 Windows 的电脑上运行 Linux，且 Windows 是 FAT 或 FAT32 分区，那么就更简单了。

1. 首先，挂载驱动器。
2. 编辑 `/etc/X11/XF86Config-4`。
3. 在 `Files` 部分下，添加如下的一行：
4. FontPath "usr/X11R6/lib/X11/fonts/TTF/*"
5. 重启字体系统：
   `/etc/rc/init.d/init restart`

## 存储 X 资源

现在假设你有一组喜欢的应用程序设置。例如，由于你怀念 IBM 3270 终端的时代，并希望 `xterm` 以黑色背景和绿色字体出现。你可以通过在启动 `xterm` 时使用以下命令来实现：

```
xterm -bg black -fg green
```

这种方法效果良好，但记住所有设置很麻烦。你也可以另一种方式告诉 X 启动 `xterm` 时使用这些颜色。启动时，X 会在主目录下查找名为 `.Xdefaults` 或 `.Xresources` 的文件——在 Red Hat 发行版中是 `.Xdefaults`。这些文件确实以点开头。`ls` 不显示它们——再次，这是 Linux 隐藏文件的方式——所以你需要使用 `ls -a` 来看到它们。

无论何种方式，使用包含如下行的 ASCII 文件：

```
xterm*cursor:Orchid
```

该行以及资源文件中的其他行告诉 Linux 如何运行各种程序。第一个项目（星号之前的）是程序名称。第二个是你想要控制的程序的特定属性，第三个（与属性名称之间至少有一个空格）是设置给该属性的值。上面的示例表示：“当运行 `xterm` 时，将其光标颜色设置为 Orchid（一种紫色）。”这非常像 NT/2000 注册表项中的值或 INI 文件中的设置。在 NT 世界中，例如，我们可能有一个类似 `HKEY_CURRENT_USER\Software\Microsoft\xterm\parameters` 的虚拟键，其中有一个名为 `cursorcolor` 的类型为 `REG_SZ` 的值为 `Orchid`。

通过将这三个命令放入 `.Xdefaults` 或 `.Xresources` 中，我们可以让 `xterm` 以这种方式运行：

```
xterm*background: black
xterm*foreground: green
xterm*cursorcolor: green
```

X 还可以通过 `xrdb` 命令随时加载一组新资源；执行 `xrdb filename` 即可。

唯一的遗憾是，这些资源设置只适用于基本的 X 应用程序。相比之下，为现代的 KDE 和 GNOME 桌面环境编写的 Linux GUI 应用程序不会查看 X 资源来获取颜色或其他设置。
