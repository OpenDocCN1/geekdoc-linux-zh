
最终，你可以将自己视为一名技术型 Linux 用户，但永远不要认为自己是专家，毕竟我们总是在学习新东西。你可以从头构建自己的发行版，帮助其他 Linux 用户解决问题，也许甚至可以在某个发行版的测试或构建阶段为改进做出贡献。接下来去哪里？

奇怪的是，大多数高端技术用户发现自己回到了原点，使用像 Linux Mint 这样的发行版。主要原因通常是它是一个简单的选项，并且是一个稳定的环境。仅仅因为你了解系统的里里外外，并不意味着你总是想修复潜在的问题。我们中的大多数人都更喜欢轻松的生活，尤其是在技术方面，所以合乎逻辑的选择是选择一个简单但仍然足够强大以完成你想要的一切的发行版，因此是 Linux Mint。

然而，归根结底，这纯粹是选择，是你个人的选择。你可能发现在阅读本书中的教程后，你不喜欢 Linux Mint 或 Cinnamon 桌面。没关系，你可能更喜欢 Ubuntu、Debian 或 openSUSE，这就是 Linux 的美妙之处。改变你想要的东西的自由，在没有成本或访问权限缺失的惩罚下，在一个发行版和另一个发行版之间跳跃。

对于“哪个发行版”这个问题的答案是，你喜欢哪一个就是哪一个！它可以像你需要的那样复杂或简单，只要它做你想要它做的事，它就是完美的。

![](img/5019375da05cbf0090115165d80772a1_16_2.png)

> “在真正的开源世界里，
>
> 你拥有掌控
>
> 自己命运的权利。”
>
> — 林纳斯·托瓦兹
>
> （Linux 内核开发者）

![](img/5019375da05cbf0090115165d80772a1_17_0.png)

## Linux 入门

谈论 Linux 有多好是一回事，但如何将其安装到计算机上又是另一回事。安装 Linux 非常简便，但你有多种选择。本节将探讨如何下载 Linux ISO 映像，将其作为主操作系统安装在 PC 上，以及如何安装虚拟环境。

使用虚拟环境，你可以在继续使用主操作系统（无论是 Windows 还是 macOS）的同时运行 Linux。感兴趣？请继续阅读以了解更多信息。

![](img/5019375da05cbf0090115165d80772a1_18_0.png)

### 在 Windows 上创建 Linux 安装介质

在将 Linux ISO 安装到计算机之前，你需要先将其传输到 DVD 或 USB 闪存盘中。这将是一个实时环境，允许你在安装前测试操作系统，但你首先需要创建可启动介质。

#### DVD 可启动介质

我们在此使用 Windows 10 PC 将 ISO 传输到 DVD。如果你使用的是 Windows 7 或更高版本，该过程极其简单。

- **步骤 1**
  首先找到你已下载的 Linux ISO 映像。通常，你可以在 Windows 7、8 和 10 计算机的“下载”文件夹中找到它，除非在保存时你指定了其他位置。
  ![](img/5019375da05cbf0090115165d80772a1_19_0.png)

- **步骤 2**
  接下来，将一张可录制 DVD 光盘插入计算机的光驱。几秒钟后，当光盘被读取时，Windows 会显示一个弹出消息，询问你如何处理新插入的光盘。请忽略此消息，因为我们将使用内置的映像烧录功能。
  ![](img/5019375da05cbf0090115165d80772a1_19_2.png)

- **步骤 3**
  右键单击 Linux ISO，从菜单中选择“Burn Disc Image”（烧录光盘映像）。根据 PC 的速度，可能需要几秒钟才会发生任何事情。不必过于担心，除非超过一分钟，在这种情况下，重新启动你的 PC 并再次尝试可能是值得的。如果顺利，Windows 光盘映像烧录器应该会启动。
  ![](img/5019375da05cbf0090115165d80772a1_19_1.png)

- **步骤 4**
  在打开的 Windows 光盘映像烧录器对话框中，点击“Verify disc after burning”（烧录后验证光盘）复选框，然后点击“Burn”（烧录）按钮。根据你 PC 光驱的速度，该过程可能需要几分钟。完成后，它将运行验证阶段，完成时，光驱应该会自动弹出光盘。
  ![](img/5019375da05cbf0090115165d80772a1_19_3.png)

#### USB 可启动介质

USB 介质比 DVD 更快且通常更方便，因为大多数现代 PC 都没有安装光驱。传输映像的过程很简单，但你首先需要第三方应用和一个 4GB 或更大的 USB 闪存盘。

- **步骤 1** 首先打开网页浏览器，访问 www.rufus.akeo.ie/。向下滚动页面一点，你会看到一个“Download”（下载）标题，下面是 Rufus 的最新版本。左键单击链接以开始下载。
  ![](img/5019375da05cbf0090115165d80772a1_20_0.png)

- **步骤 2** 双击下载的 Rufus 可执行文件，对 Windows 安全询问点击“Yes”（是），对检查更新点击“Yes”（是）。Rufus 启动后，它应该已经识别了你插入的 USB 闪存盘；如果没有，只需拔出并重新插入。
  ![](img/5019375da05cbf0090115165d80772a1_20_1.png)

- **步骤 3** 乍一看，Rufus 界面可能有点令人困惑，但别担心，它其实相当简单。首先，点击“Disk or ISO Image (Please select)”（磁盘或 ISO 映像（请选择））下拉菜单旁边的“SELECT”（选择）按钮。这将启动一个 Windows 资源管理器窗口，你可以在其中定位并选择 Linux ISO。
  ![](img/5019375da05cbf0090115165d80772a1_20_2.png)

- **步骤 4** 当你准备好时，点击 Rufus 应用底部的“Start”（开始）按钮。这可能会打开另一个对话框，询问你是否下载并使用新版本的 SysLinux。SysLinux 是一组引导加载程序，用于允许现代 PC 访问并从 USB 闪存盘引导。这是必需的，因此如果询问，请点击“Yes”（是）以继续。

> This image uses Syslinux 6.03/20151222 but this application only includes the installation files for Syslinux 6.03/2014-10-06.
>
> 由于新版本的 SysLinux 彼此不兼容，且 Rufus 无法包含所有版本，必须从 Internet 下载两个额外文件（“ldlinux.sys”和“ldlinux.bin”）：
>
> - 选择“Yes”（是）以连接 Internet 并下载这些文件
> - 选择“No”（否）以取消操作
>
> > Note. The files will be downloaded to the current application directory and will be reused automatically if present.

- **步骤 5** 下一步询问你希望以哪种映像模式将 Linux ISO 写入 USB 闪存盘。两种方法在不同情况下均可行，但通常推荐的 ISO 映像模式更为流行。请确保预先选择了此模式，点击 Ok（确定）继续，然后再次点击 Ok（确定）以确认操作。

If the image you have selected is an ‘ISO9660’ image. This means it can be written either in ISO Image (file mode), copy mode or DD Image (disk image) mode. Rufus recommends using ISO Image mode, so that you always have full access to the drive after writing it. However, if you encounter issues during boot, you can try writing this image again in DD mode.

Please select the mode that you want to use to write this image:

- Write in ISO Image mode (Recommended)
- Write in DD Image mode

- **步骤 6** Linux 映像现在正在从 ISO 传输到 USB 闪存盘。该过程不应花费太长时间，具体取决于 USB 设备和 PC 的速度。你可能会发现 Rufus 在过程中会自动在 Windows 资源管理器中关闭 USB 驱动器；别担心，如果你想的话可以最小化或关闭它。当过程完成时，点击“Close”（关闭）按钮。
  ![](img/5019375da05cbf0090115165d80772a1_20_3.png)

## 在 PC 上安装 Linux
