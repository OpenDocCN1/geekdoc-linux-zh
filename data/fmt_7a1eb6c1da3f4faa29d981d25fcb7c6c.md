
with Linux

> "In real open source, you have the right to control your own destiny."

> – Linus Torvalds (developer of the Linux kernel)

说 Linux 很好当然没错，但你如何把它安装到你的电脑上？安装 Linux 非常简单，但你有几个选择。本节介绍如何下载 Linux ISO，将其安装到 PC 上作为主要操作系统，甚至如何安装虚拟环境。

使用虚拟环境，你可以在仍使用主要操作系统（无论是 Windows 还是 macOS）的同时运行 Linux。感兴趣吗？继续阅读，了解更多。

- 20 Creating a Linux Installer on Windows
- 22 Installing Linux on a PC
- 24 Installing a Virtual Environment
- 26 Installing Linux in a Virtual Environment

## Creating a Linux Installer on Windows

你需要在能够将其安装到计算机上之前，将下载的 Linux ISO 传输到 DVD 或 USB 密钥。这将是一个实时环境，允许你在安装前测试操作系统，但首先你需要创建可启动介质。

### DVD BOOTABLE MEDIA

我们在这里使用 Windows 10 PC 将 ISO 传输到 DVD。如果你使用的是 Windows 7 及更高版本的 Windows，过程非常简单。

**STEP 1** 首先找到你已下载的 Linux ISO 映像。你通常可以在 Windows 7、8.1 和 10 计算机的下载文件夹中找到它，除非你在保存时指定了其他位置。

![](img/f80199d101da92d953f18eaa6205b48e_19_0.png)

**STEP 2** 接下来将可刻录 DVD 光盘插入计算机的光驱。几秒钟后，在读取光盘时，Windows 会显示弹出消息询问你对新插入的光盘做什么。忽略它，因为我们将使用内置的映像刻录功能。

![](img/f80199d101da92d953f18eaa6205b48e_19_1.png)

**STEP 3** 右键单击 Linux ISO 并从菜单中选择 Burn Disc Image。根据 PC 的速度，可能需要几秒钟才会发生任何事情。不要太担心，除非它花费超过一分钟，在这种情况下可能值得重新启动 PC 并重试。祝你好运，Windows Disc Image Burner 应该会启动。

![](img/f80199d101da92d953f18eaa6205b48e_19_2.png)

**STEP 4** 打开 Windows Disc Image Burner 对话框后，单击“Verify disc after burning”复选框，然后单击 Burn 按钮。过程应需要几分钟，具体取决于 PC 光驱的速度。完成后它会进行验证阶段，完成后光驱应自动弹出光盘供你使用。

![](img/f80199d101da92d953f18eaa6205b48e_19_3.png)

### USB BOOTABLE MEDIA

USB 介质比 DVD 更快，通常更方便，因为大多数现代 PC 都没有安装光驱。传输映像的过程很容易，但你首先需要第三方应用程序和 4GB 或更大的 USB 闪存驱动器。

**STEP 1**
首先打开网络浏览器并访问 `www.rufus.akeo.ie/`。向下滚动页面一点，你会看到一个下载标题，其下是 Rufus 的最新版本。左键单击链接开始下载。

![](img/f80199d101da92d953f18eaa6205b48e_20_0.png)

**STEP 4**
准备就绪后，单击 Rufus 应用底部的 Start 按钮。这可能会打开另一个对话框，询问你是否下载并使用新版本的 SysLinux。SysLinux 是一组引导加载程序，用于允许现代 PC 访问并从 USB 闪存驱动器启动。这是必要的，因此如果被询问，请单击“是”继续。

![](img/f80199d101da92d953f18eaa6205b48e_20_1.png)

**STEP 2**
双击下载的 Rufus 可执行文件并单击“是”以回答 Windows 安全问题，然后单击“是”以检查更新。启动 Rufus 后，它应该已经识别出你插入的 USB 闪存驱动器；如果没有，只需移除并重新插入即可。

![](img/f80199d101da92d953f18eaa6205b48e_20_2.png)

**STEP 5**
下一步询问你希望 Linux ISO 以何种映像模式写入 USB 闪存驱动器。两种方法都适用于不同的情况，但通常，推荐的 ISO 映像模式更受欢迎。确保此模式已预先选中，然后单击 OK 继续，然后再次单击 OK 确认操作。

![](img/f80199d101da92d953f18eaa6205b48e_20_3.png)

**STEP 3**
乍一看 Rufus 界面可能看起来有点令人困惑，但不用担心，它其实非常简单。首先，单击“Disk or ISO Image (Please select)”下拉菜单旁边的 SELECT 按钮。这会启动 Windows 资源管理器窗口，你可以在其中找到并选择 Linux ISO。

![](img/f80199d101da92d953f18eaa6205b48e_20_4.png)

**STEP 6**
Linux ISO 现在已传输到 USB 闪存驱动器。过程不应花费太长时间，再次取决于 USB 设备和 PC 的速度。你可能会发现 Rufus 在过程中自动在 Windows 资源管理器中打开 USB 驱动器；不用担心，如果你愿意，可以最小化或关闭它。过程完成后，单击 Close 按钮。

![](img/f80199d101da92d953f18eaa6205b48e_20_5.png)

## Installing Linux on a PC

大多数 Linux 发行版都作为实时环境提供。这意味着你可以直接从你刚刚创建的 DVD 或 USB 启动一个实际的、完全工作的发行版。让我们看看这是如何工作的，以及你如何从那里安装 Linux。

### UEFI BIOS

统一可扩展固件接口（UEFI）用于识别硬件并在 PC 启动过程中保护 PC。它取代了传统的 BIOS，但在安装 Linux 时可能会导致问题。

**STEP 1** 将你的 DVD 或 USB 闪存驱动器插入 PC，如果尚未关闭，请关闭 Windows。在此实例中，我们使用的是 USB 启动介质，但过程几乎相同。启动 PC，并在提示时按适当的键进入 BIOS 或 SETUP，例如：`F2`、`Del` 甚至 `F12`。

![](img/f80199d101da92d953f18eaa6205b48e_21_0.png)

**STEP 3** 将 UEFI 切换为 Legacy 模式后，现在有两种启动到实时环境的方法。第一种是通过你已在其中的 BIOS。找到启动顺序并将第一个启动设备从其原始设置，通常是内部硬盘或类似设置，改为：`USB Storage Device` 用于 USB 介质选项，或 `DVD Drive` 用于 DVD 介质选项。

![](img/f80199d101da92d953f18eaa6205b48e_21_1.png)

**STEP 2** UEFI BIOS 有不同版本，因此涵盖所有版本是不可能的。你要找的是详细说明启动顺序或启动模式的部分。在这里，你可以选择关闭 UEFI 并选择 Legacy 或禁用安全启动。大多数发行版都可以使用 UEFI，但启用其启动可能是一个棘手的过程。

![](img/f80199d101da92d953f18eaa6205b48e_21_2.png)

**STEP 4** 或者使用启动选项菜单。使用此选项，你可以按 `F12`（或类似键）显示启动介质选项列表；从那里，你可以选择适当的启动介质。无论哪种方式，你现在都可以通过导航到“保存和退出”选项并选择“保存更改并退出”来保存并退出 BIOS。

![](img/f80199d101da92d953f18eaa6205b48e_21_3.png)

## 安装 Linux

一旦 Live 环境启动完成，你会看到将发行版安装到计算机的选项。先随意浏览一下，准备好后在桌面上查找安装选项。

### 第 1 步

如果已连接到互联网（如果没有，现在请连接），并且处于 Live 环境中，请双击桌面上的 Install Linux Mint 图标开始安装过程。其他发行版会显示其自己的名称，当然，但过程是相同的。准备好后点击 Continue。

![](img/f80199d101da92d953f18eaa6205b48e_22_0.png)

### 第 2 步

虽然安装过程在大多数 Linux 发行版中非常相似，但有些发行版在安装期间会提出不同的问题。通常这些问题并不太困难，没有什么很技术性的内容，但有些例如“安装第三方软件...”可能会让人困惑。在这种情况下你可以点击 Continue，但如果不确定，请确保手边有一台联网设备以便提问。
