
> **警告** 请务必谨慎使用 `KLILO`。如果你不熟悉 Linux 如何启动以及使用 `LILO` 引导器，可能会做出导致 `LILO` 无法启动的更改。

`KLILO` 工具位于光盘 `/Part04/Execute/Klilo`。虽然此程序不包含所有可能的 `LILO` 功能配置（例如密码、启动参数和消息文本），但它让无需使用命令行即可查看和更新简单的配置。

# 136 润化你的桌面

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_155_0.png)

使用 `KLILO`，你可以点击“Add（添加）”按钮为电脑添加额外的操作系统或 Linux 内核配置。一旦添加了系统，你就可以使用“Edit（编辑）”按钮设置硬盘设备、选择运行哪个内核等。对话框顶部的整体配置选项允许你设置安装 `LILO` 的位置，并确定在启动默认操作系统（“操作系统”列表中的第一项）之前的延迟时间。

使用 `KLILO` 配置好 `lilo.conf` 文件后，按下“Install（安装）”按钮运行 `lilo` 命令并将此配置复制到引导扇、主引导记录（`MBR`）或软盘上（你必须以 `root` 登录才能安装 `LILO`）。

你可以在 `LinuxConf` 工具中使用一组与 `KLILO` 类似的配置对话框。在“Config（配置）”选项卡上，最后一项是 `boot mode`（启动模式）。该部分包含六项，可以帮助你控制 `LILO` 如何运行以启动你的 Linux 系统和其他操作系统。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_156_0.png)

`LinuxConf` 包含了 `KLILO` 中不具备的功能，例如添加可以启动的额外内核。（这在你使用不同选项重新编译了 Linux 内核并想尝试新内核时使用）。`KLILO` 是一种更容易学习 `LILO` 并进行图形化配置的方法，而不需要过多了解所有选项的背景。

`lilo.conf` 的帮助页（`man` page）提供了关于 `KLILO` 和 `LinuxConf` 提供的可能配置选项的详细信息。你也可以查看 `LILO HOWTO` 文档，它包含在 CD 的 `/A11-HOWTODocs/mini/LILO.html` 中。

# 管理你所有的密码

你越使用互联网，在全球范围内设置的账户就越多。以前你只有一个 `ISP` 账户，而现在你可能为访问网上银行、`ClickRewards` 账户、`Amazon.com`、`E*trade`、信用卡公司以及其他账户拥有独立的用户名和密码。在所有这些账户上使用相同的用户名通常是不可能的；在所有账户上使用相同的密码则是彻头彻尾愚蠢。

`Gpasman` 实用工具提供了一个简单的解决方案。它存储了你维护的各种账户的所有用户名和密码。密码以明文（可读）形式显示在屏幕上，以便在你需要访问账户时回想起它们。然而，数据以加密形式存储在磁盘上，这样其他可能访问硬盘的人就看不到 `Gpasman` 文件中的密码。

要使用 `Gpasman` 实用工具（位于 CD 的 `/Part04/Execute/Gpasman`），请使用此命令：

```bash
$ gpasman
```

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_157_0.png)

当你首次启动 `Gpasman` 时，它会创建一个存储你加密密码的隐藏文件。每当你启动 `Gpasman` 时，都必须输入你当前登录账户的密码。这防止了另一个用户在你离开座位片刻时启动 `Gpasman`。当然，当 `Gpasman` 正在将你所有的密码以明文形式显示在屏幕上时，你应该时刻小心别人从背后窥视，但使用 `Gpasman` 解决忘记密码问题要比在显示器上到处贴满账户信息的便利签要好得多。

# 其他奇的插件

你想在所有设备（包括你的 `Palm` 设备）上使用 Linux 吗？你使用 CD 刻录机创建自己的自定义音乐 CD 或数据备份吗？你喜欢阅读在线书籍来打时间吗？如果这些听起来很有趣，请继续阅读一些可以扩展你 Linux 系统实用性的精彩程序。

## 将 Linux 连接到你的 PalmPilot

随着 `Palm` 的流行，人们想要将自己的 `Palm` 与 Linux 系统同步是不可避免的。现在有几个软件包支持 `Palm` 连接到 Linux 机器。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_158_0.png)

> **注意：** 你可能也听过 Linux 可以运行在 `PDA` 上。这是 true，但在这里解释起来有点复杂。基本上，Linux 有针对 `Compaq IPaq` `PDA` 设备的移植。其他公司（特别是三星）也创建了原生基于 Linux 的新 `PDA` 设备。我们可以预计明年看到更多此类设备，随着硬件成本的降低，人们意识到他们需要比 `Palm OS` 更多的功能（而且他们不想向微软支付版税）。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_158_1.png)

在可以使用 `Palm` 的图形界面之前，你需要安装与设备建立接口的基本功能。这包含在 `pilot-link` 软件包中。虽然 `Red Hat 7` 默认安装了 `pilot-link` 软件包，但它的版本还不够新，不支持我在本节描述的 `Palm` 工具（从 `Gnome-Pilot` 开始）。你可以在 CD 的 `/Part04/Execute/Gnome-Pilot` 找到更高版本。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_158_2.png)

使用这些命令删除现有的 `pilot-link` 软件包及其支持包，然后从 CD 安装带有其支持包的新 `pilot-link` 软件包：

```bash
# cd /mnt/cdrom/Part04/Execute/Gnome-Pilot
# rpm -e pilot-link-devel
# rpm -e kpilot
# rpm -e pilot-link
# rpm -Uvh libpilot-link3-0.9.5-0.3.2mdk.i586.rpm
# rpm -Uvh pilot-link-link-0_9_3-10_i386.rpm
```

> **注意：** 如果你在卸载软件包时（使用 `rpm -e`）遇到问题，可以随时从原始的 `Red Hat 7` CD 重新安装相同的软件包。

一旦更新了 `pilot-link`，你就可以通过桌面访问你的 `Palm`。我在这里提到的两个工具是 `Gnome-Pilot` 和 `KPilot`。

> **注意：** 记住你在 `Red Hat 7` 系统上同时安装了 `Gnome` 和 `KDE`，无论你使用哪种桌面，都可以运行两者。冲突只发生在某个应用程序尝试在一个桌面上工作而你却在另一个桌面时。使用 `switch-kde` 在它们之间进行切换。

要从 `Gnome` 同步你的 `Palm`，请尝试 `Gnome-Pilot`。这是一个功能强大的程序，但安装我目前描述的大部分其他程序有点复杂。

在更新 `pilot-link` 后，你可以通过单个 `rpm` 命令从目录安装 `Gnome-Pilot` 软件包：

```bash
# rpm -Uvh gnome-pilot-0.1.55-0.i586.rpm
```

现在你可以尝试 `Gnome-Pilot` 了。我建议只在 `Gnome` 桌面运行此程序，因为它与 `Gnome` 交互会让 `KDE` 感到困惑。你在 `Gnome` 控制中心内部 `Gnome-Pilot`。安装 `Gnome-Pilot` 会安装两个主要项目：`Peripheral > Pilot Conduits`（包含五个子项）和 `Peripheral > Pilot Link`。当你第一次点击 `Pilot Link` 项时，会启动一个向导帮助你设置 `Palm` 连接。此向导大约四个屏幕，这里显示的是第三个。你输入设备信息以便 Linux 与 `Palm` 同步。

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_160_0.png)

设置初始连接后，你可以使用 `Pilot Link` 项管理你的连接。此窗口包含三个选项卡：`Pilots`、`Devices` 和 `Advanced`。在 `Pilots` 选项卡内点击“Add（添加）”或选择某个设置并点击“Edit（编辑）”时，会弹出一个示例：`Pilot Settings`（`Pilot` 设置）对话框。

# 润化你的桌面

![](img/35c1af90d4f3af9cd7cfd006c6b752f5_161_0.png)

一旦你配置了 `Palm` 设备，就可以使用 `Peripheral > Pilot Conduits` 下的任何一个通道页面在你的 Linux 系统和 `Palm` 之间同步数据。在 `Memo File`（备忘录文件）通道页面上，你可以选择从或向 `Palm` 复制或合并数据。

配置此备忘录-`Palm` 通道

## 其他天才级附加组件 143

如果你正在运行 `KDE` 桌面，你需要的连接到 `Palm` 的工具叫做 `KPilot`。它位于光盘的 `/Part04/Execute/KPilot` 目录下。`KPilot` 的开发持续进行，新版本定期发布，并带有额外的功能。当你启动 `KPilot` 时，会出现一个如所示的配置对话框。在这个对话框中，你可以选择 `Palm` 连接的设备、用于 `Palm` 连接的用户账户以及其他选项。
