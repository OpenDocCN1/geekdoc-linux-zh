
## 第7小时

### 使用 X Window 系统

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_164_0.png)

安装在您计算机上的 X Window 系统，正如您在第3小时“配置 X Window 系统”中所学到的，是来自 XFree86 Project, Inc. 的 X11 端口。此图形界面包含约 3,500 个文件，其中近 200 个程序（客户端）、超过 500 种字体，以及近 50 兆字节软件中超过 500 个图形图像文件。您可以在 /usr/X11R6 目录下找到几乎所有（但并非全部文件或程序）的 X11 内容。

本小时向您展示几种启动 X11 的方法，讨论您在 X 会话期间可使用的一些不同的图形界面或窗口管理器，并提供针对系统上安装的几个终端程序（或 shell 控制台）的练习。您还将学习一些基本操作，例如复制和粘贴文本、调整鼠标指针或光标形状，以及进行屏幕截图。最后一节向您展示了一些您可能想要尝试的 X11 客户端示例。

请注意，诸如文本编辑器、图形程序，甚至其他 X11 窗口管理器等许多客户端在本书中各处都有讨论。

### 启动 X

当您首次登录 OpenLinux 时，会看到如下简短信息：

Welcome to your OpenLinux system!
You can start X11 with 'startx' or KDE with 'kde'.

startx 和 kde 命令几乎是相同的 shell 脚本，用于启动 X11 会话。startx 位于 /usr/X11R6/bin 目录下，而 kde 位于 /opt/kde/bin 目录下。要使用 fvwm 窗口管理器（本章稍后“X11 窗口管理器”一节中讨论）与 Looking Glass 桌面客户端启动 X11 会话，请在控制台的命令行中输入 startx，然后按 Enter，如下所示：

```
# startx
```

如果您已正确配置 X11 使其与计算机的显卡配合使用（如第3小时所述），显示屏会清空，几秒钟后 X11 桌面会出现，如图 7.1 所示。

图 7.1
带有 Looking Glass 桌面客户端的 fvwm X11 窗口管理器是使用 OpenLinux 使用 X 的几种方式之一。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_165_0.png)

要使用 K 桌面环境（第8小时“探索 K 桌面环境”中讨论）启动 X 会话，请在命令行中输入 kde，然后按 Enter，如下所示：

```
# kde
```

屏幕清空，很快您会看到 KDE 的默认桌面出现，如图 7.2 所示。

图 7.2
KDE 桌面是一个完整的 X11 环境，包含几乎所有现代图形界面的功能。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_166_0.png)

### 使用不同颜色深度启动 X11

当您使用 kde 或 startx 启动 X11 会话时，X11 使用 256 种颜色，或八位平面（一个字节，或每个像素八位）。要使用 16 位平面（或两个字节，或每个像素 16 位）启动 X 会话，请使用 -bpp 选项，后跟 16，如下所示：

```
# startx -- -bpp 16
```

或

```
# kde -- -bpp 16
```

-bpp 16 选项会传递给您在配置 X 时选择的 X 服务器，作为使用 64,000 种颜色的选项。其他颜色深度，例如 24 或 32，可能取决于显卡的功能以及您如何配置您的 XF86Config 文件。

尽管位于 /etc 目录下的 XF86Config 在第3小时中有更详细的描述，但此文件的相关部分位于 Screen 部分。示例显示在清单 7.1 中。

### 清单 7.1 典型的 XF86CONFIG 屏幕部分

```
Section "Screen"
    Driver      "svga"
    Device      "NeoMagic"
    Monitor     "Generic Multisync"
    Subsection  "Display"
        Depth       8
        Modes       "1024x768" "800x600" "640x480"
    #       Virtual 1024 768
    EndSubsection
    Subsection  "Display"
        Depth       16
        Modes       "1024x768" "800x600" "640x480"
    EndSubsection
    Subsection  "Display"
        Depth       24
        Modes       "800x600" "640x480"
    EndSubsection
EndSection
```

请注意清单中的“Display”子部分（针对 NeoMagic 视频图形显示）。每个子部分都以 Depth 设置开始，然后列出不同的 Modes，即分辨率。Depth 设置设置显示深度，即 X 会话的颜色数。如果您始终以 800×600 的分辨率使用 64,000 种颜色的 X，并且不想每次启动 X 时都输入 -- -bpp 16，请编辑您的 XF86Config 文件并简单使用如下“Screen”部分：

```
Section "Screen"
    Driver      "svga"
    Device      "NeoMagic"
    Monitor     "Generic Multisync"
    DefaultColorDepth 16
    Subsection  "Display"
        Depth       16
        Modes       "800x600"
    EndSubsection
EndSection
```

Modes 行告诉 X 服务器在水平和垂直方向上使用特定数量的每英寸点数。您选择的 X 服务器会自动使用与 XF86Config 文件中相应模式行匹配的第一个可用模式值（例如 800×600）。在清单 7.1 中，如果所有模式都有效，您的 X 会话将以每像素八位启动，显示屏宽度为 1024 像素，高度为 800 像素。要在 X 会话期间切换到较低分辨率或模式（例如从 1024×768 切换到 800×600），请按 Ctrl+Alt+KeyPad-。也就是说，按住 Ctrl+Alt，然后按键盘小键盘上的减号 (-) 键。要切换到更高分辨率，请按 Ctrl+Alt+KeyPad+。

清单 7.1 中的 Virtual 行使您能够拥有比屏幕物理区域更大的显示。如果您的计算机显卡和显示器仅支持较低分辨率，例如 800×600，但您需要在更高分辨率下运行 X11 客户端（程序），例如 1024×768，这非常方便。清单 7.1 中的 Virtual 行使用井号 (#) 禁用，但您可以删除井号然后重新启动 X 来启用它。然后您的显示成为一个滚动窗口，当鼠标指针被拖动到屏幕边缘之外时，它会在更大的虚拟显示中移动。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_168_0.png)

> 不幸的是，一些 X 客户端，例如图形绘图程序 xfig 或街机动作游戏 xboing，需要更大的显示区域。您的屏幕分辨率取决于显卡在特定 X 服务器上的支持程度、显卡上安装的视频内存量、计算机显示器或笔记本电脑屏幕的分辨率能力，以及您如何配置 XF86Config 文件。例如，您不能在仅支持 800×600 分辨率的笔记本电脑上使用 1024×768 显示，但如果安装了足够的视频内存，您可能能够使用 1024×768 或更大的虚拟分辨率。

### 使用 X11 的虚拟控制台

尽管在使用 rxvt 等终端客户端（如本章稍后“使用 X11 终端程序”一节中讨论）时，您可以在 X 会话期间进入 shell 命令行，但在使用桌面计算机上的 X 时，您也可以进入 OpenLinux 控制台。OpenLinux 支持六个不同的虚拟控制台或登录屏幕。当您不使用 X 时，您可以通过按 Alt+FX 进入六个不同的登录提示，其中 X 为 F1 至 F6。

例如，当您首次登录 OpenLinux 时，您位于第一个虚拟控制台。登录后，按 Alt+F2。然后您会看到另一个登录提示，您可以作为另一个用户登录或启动另一个 OpenLinux 会话。要返回到第一个登录屏幕，请按 Alt+F1。

当您登录 OpenLinux 并使用 startx 或 kde 启动 X11 会话时，X 默认使用第七个虚拟屏幕。因为您是从第一个虚拟控制台启动 X 的，所以该控制台不可用。但是，您可以通过按 Ctrl+Alt+F2 进入另一个虚拟控制台，例如第二个。然后您会看到 OpenLinux 登录提示。要返回到 X 会话，请按 Ctrl+Alt+F7。使用这种方法，您可以在 X 会话和不同控制台之间来回切换。

### 启动多个 X11 会话

不仅可以在 X 会话期间使用 OpenLinux 的多个虚拟控制台，您还可以在 OpenLinux 会话期间启动并使用多个 X 控制台。这意味着您可以登录，使用特定颜色深度的一个窗口管理器启动 X，然后转到不同的控制台，登录并使用不同的窗口管理器和颜色深度启动另一个 X 会话。然后，在您的 X 会话期间，在不同的控制台和 X 窗口管理器之间切换！

以下是一个逐步示例，展示如何同时登录并使用 startx 和 kde 命令：

- 1. 启动 OpenLinux 并登录。在命令行中，使用以下命令以 256 种颜色启动 KDE 的 X 会话：
  ```
  # kde
  ```
- 2. 按 Enter 启动 X 会话（它使用第七个虚拟屏幕）。
- 3. KDE 桌面出现后，按 Ctrl+Alt+F2。您位于第二个虚拟控制台和 OpenLinux 登录提示。再次登录 OpenLinux。
- 4. 在命令行中，使用 startx 命令启动一个使用 64,000 种颜色的 X 会话，使用 fvwm 窗口管理器和 Looking Glass 桌面。包含 :1 和 vt8 命令行选项以使用第八个虚拟屏幕启动名为 :1 的第二个 X11 会话，如下所示：
  ```
  # startx -- :1 -bpp 16 vt8
  ```
  屏幕清空，fvwm 和 Looking Glass 桌面出现（如图 7.1 所示）。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_169_0.png)

> Looking Glass 桌面是一个 X11 客户端，用于在 X11 会话期间提供图形工作区。当您使用 startx 启动 X 会话时，Looking Glass 客户端默认出现。当桌面出现时，单击 Caldera 或 Netscape 图标以阅读 Looking Glass 手册。您可以在此处找到使用此客户端与 X 所需的所有信息。
