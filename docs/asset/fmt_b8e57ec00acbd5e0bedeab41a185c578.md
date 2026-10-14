
# 第 6 章：Linux 客户机操作系统

安装程序对 X 服务器的符号链接执行相同的操作，该链接简单命名为`X`。如果安装程序重命名了一个链接然后创建了另外两个，这可能会令人困惑。这是在安装 VMware Tools 之前，带有`XFree86_SVGA`服务器的 Red Hat 系统上的`/etc/X11/X`：

```
lrwxrxr-x 1 root root 30 Mar 7 04:27 X -> ../usr/X11R6/bin/XFree86_SVGA
```

（记住`.../`在这里仅表示路径。）这是之后的样子：

```
lrwxrxr-x 1 root root 13 Mar 11 2001 X -> /etc/X11/XF86Config.vm
lrwxrxr-x 1 root root 30 Mar 7 04:27 X.org -> ../usr/X11R6/bin/XFree86_SVGA
lrwxrxr-x 1 root root 26 Mar 8 14:07 X.vm -> /usr/X11R6/bin/XFree86_VMware
```

在其他系统（如 Caldera）上，`X`链接可能在`/usr/X11R6/bin`。如果 Tools 安装程序使用该链接，它会在`/etc`中创建信息。如果没有使用，你需要手动寻找这些文件并创建链接。其他发行版（如 Debian）使用不同的方案。它们不使用链接`X`，而是使用`/etc/X11`中的`Xserver`文件。该文件的前两行如下：

```
/usr/X11R6/bin/Console
```

第一行告诉你使用哪个服务器。要配合 VMware Tools 使用 X 服务器，只需将该行改为`/usr/X11R6/bin/XFree86_VMware`。鉴于你已安装 VMware Tools，你可能期望它会将原始`Xserver`文件移动到`Xserver.org`，创建一个带有 VMware 必要更改的新文件`Xserver.vm`，并从`Xserver`创建指向`Xserver.vm`的符号链接。事实并非如此。相反，Tools 安装程序会在`Xserver`的第一行寻找原始可执行文件——如所示。一旦找到服务器，安装程序会将二进制文件重命名为`X86_VGA16.org`并创建两个符号链接：一个指向`X86_VMware`的`X86_VGA16.vm`，另一个指向`X86_vm`的`X86_VGA16`，因此`/usr/X11R6/bin`目录看起来如下：

```
-lrwxr-xr-x 1 root root 13 Mar 13 03:04 X86_VGA16 -> X86_VGA16.vm
-lrwxr-xr-x 1 root root 184652 20 Nov 18 05:44 X86_VGA16.org
-lrwxr-xr-x 1 root root 11 Mar 13 03:04 X86_VGA16.vm -> X86_VMware
-lrwxr-xr-x 1 root root 168878 13 Mar 13 03:03 X86_vm
```

你可能在好奇用`.org`和`.vm`后缀命名文件和链接的目的是为了启用双配置。例如，如果你最初不是在 VMware 下安装的 Linux 系统，如果你仍然想在真实硬件上运行它，你会希望 Linux 配置文件与真实硬件匹配，VMware 安装程序会尝试处理这个问题，我们将在 6.5.7 节处理。但首先测试`X86_VMware`服务器并根据你的显示器和喜调整分辨率（见 6.5.3）。

## XFree86 版本 4

在 XFree86 4.x 版本中，并不是各种显卡驱动的二进制文件，只有一个 X 二进制文件，且驱动是作为共享库加载的。由于这个原因，VMware 还为 XFree86 4 提供了一个名为`vmware_drv.o`的驱动。它包含在适用于 Linux 的 VMware Tools 中，随 XFree86 4 及以上版本提供。

Tools 应该将驱动模块`vmware_drv.o`安装在你的`/usr/X11R6/lib/modules`目录下。然而，配置文件的名称取决于你的发行版。大多数发行版使用`/etc/X11/X86Config-4`，但`/etc/X11/X86Config`也可以。如果你有`XF86Config`和`XF86Config-4`，可能会很混乱，X 服务器使用`X86Config-4`。无论如何，Tools 都会检测你需要哪，重命名原始文件并安装带有`.vm`后缀的新文件，因为适用于 XFree86 3.x（见上一节）。

## 6.5.3 测试和自定义 VMware 服务器

要测试 VMware 服务器，输入`X`查看 VMware 窗口或屏幕是否变为像图 6.1 样的 1280x1024 屏幕。如果是，并且你可以移动鼠标指针，说明服务器工作正常；使用`ctrl–alt–backspace`杀死它。

如果你得到一个也像图 6.1 样的 640x480 屏幕，你正在运行`X86_VGA16`，它在 VMware 下可以工作，但非常慢（丑）。在这种情况下（或者如果你什么都没有得到），找到上一节提到的链接或文件并修复它们。

如果你的显示器很小，1280x1024 的分辨率可能工作起来不舒服。要在 XFree863.x 中更改此设置，请编辑结尾的`XF8Config.vm`文件，它看起来如下：

```
Section "Screen"
Driver "accel"
Device "SVGA"
Monitor "VMware"
Subsection "Display"
Modes "1280x1024"
# Modes "1600x1024" "1280x1024" "1152x864" "1024x768" "800x600"
# Modes "640x480"
# Modes "800x600"
# Modes "1024x768"
```

以`#`开头的行是被注释掉的活动状态；如你所示，1280x1024 是默认的激活模式。要更改模式，在激活行前面加上`#`以禁用，并移除你想使用的模式前面的`#`。

更改在 X 服务器重启时生效。

对于 XFree86.4x，你必须更改`XF86Config`或`X86Config-4`文件中的`Screen`部分。这里是一个 24 位、1024x768 显示的示例：

```
Section "Screen"
Identifier "Screen 1"
Device "VMware SVGA"
Monitor "VMware Monitor"
Subsection "Display"
深度 24
模式
"1024x768*"
EndSection
EndSection
```

现在你已经准备好使用 X Window 系统了。你可以使用`startx`或`xinit`来启动会，也可以激活显示管理器，例如`gdm` (GNOME)、`kdm` (KDE) 或`xdm`。（在章节的早期 6.4 节中，当我们讨论如何在 VMware 下管理现有的 Linux 安装时，我们已经讨论过如何禁用这些系统。）

如果你尝试过`XF86_VMware`服务器，可能是因为共享库依赖问题。尽管它不依赖于任何 FreeX86 3x 共享库并且可以在没有 FreeX86 3x 的运行，但可能存在其他依赖；请使用`lld XF86_VMware`来查找它们。如果你可以安装这些库，应该考虑为 FreeX86 4.x 使用 VMware SVGA 驱动。

## 6.5.4 额外的 VMware X Server 信息

与大多数驱动不同，FreeX86 服务器及其驱动模块旨在提供几乎任何分辨率和深度而不会产生冲突。FreeX86 让你随所欲；如果你想要 800x100 的分辨率，只要你能够确定显示器的时序，就没有问题。

VMware X 服务器更进了一步；由于它通过虚拟显示运行，你可以按照自己喜欢的方式定义分辨率。

如果你查看 VMware 提供的`XF86Config`文件中的`Monitor`部分（你应该去看看），你会看到许多非标准的显示尺寸（例如 2364x1773）。如果你想添加新模式，`ModelLine`的“计算”非常简单——只需在水平和垂直像素后的每个连续数字上加 1 即可。然而，有一个小的限制：水平分辨率必须是 8 的倍数（如果不是，VMware X 服务器将其向上舍入到下一个 8 的倍数）。

## 6.5.5 VMware Toolbox

为了访问主机与客户机操作系统交互的一些 VMware 功能，你需要使用 VMware Toolbox。默认情况下，该工具将其安装在 X 二进制目录`/usr/X11/rc/bin`下，名为`vmware-toolbox`的单个程序。

Toolbox 允许在主机和客户机系统之间进行复制和粘贴。具体而言，Toolbox 会捕获并处理有关`X_PRIMARY`选择的信息。在 Linux 系统上，必须运行`vmware-toolbox`程序才能使此功能生效。
