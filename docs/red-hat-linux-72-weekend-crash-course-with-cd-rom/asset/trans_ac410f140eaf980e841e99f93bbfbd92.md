
## 配置 X 窗口系统

如果在 X 配置步骤期间安装程序无法检测到您的视频卡，您可以跳过该步骤，并在完成安装的其他部分后再配置 X。完成安装后，请使用以下步骤配置 X：

1.  安装完成并重启电脑后，您将看到一个文本登录屏幕。以 root 身份登录，并输入 `Xconfigurator` 以运行该名称的工具程序。`Xconfigurator` 工具可让您创建 X 服务器所需的配置文件。
2.  `Xconfigurator` 程序启动时会显示一个欢迎对话框，其中包含关于 X 配置文件的消息。阅读完消息后，按 Enter 键继续配置过程。

`Xconfigurator` 会自动检测您的视频卡使用的芯片组，并显示一条摘要消息，如图 2-1 所示。

![](img/5fe8f856723cde0b366f73584b9e64b8_39_0.png)

**图 2-1** Xconfigurator 探测视频卡后生成的消息

在这种情况下，Xconfigurator 发现了一块基于 nVidia GeForce 256 DDR 芯片组的视频卡，并建议使用 nv XFree4 驱动。图 2-1 中的对话框仅是一个示例，因此您看到的对话框可能不同。确保 Xconfigurator 识别了正确的显卡，然后按 Enter 继续其余配置。您看到的下一个对话框可让您从列表中选择监视器。

按上箭头和下箭头键浏览列表。如果您在列表中找到了您的监视器型号，请将光标定位到该监视器上，然后按 Enter。否则，选择 Custom（自定义）并按 Enter。如果您选择 Custom，Xconfigurator 将显示另一个对话框，您必须为监视器提供两个关键参数：

- **水平同步频率** 是监视器每秒绘制水平线的次数，单位为千赫兹（kHz）。
- **垂直同步速率** 或垂直刷新率是监视器每秒绘制整个屏幕的次数。

您可以在监视器手册中找到这些频率参数，或者在许多情况下，在制造商的网站上找到。按 Enter 继续。Xconfigurator 将显示预定义的水平同步范围列表。

监视器同步速率的值应与您的监视器规格相匹配。不要猜测！如果您指定的速率超出了监视器的实际能力，可能会损坏它。

例如，如果您的监视器手册说它可以以 60Hz 显示 1,280 × 1,024 分辨率，那么您应该选择与此规格匹配的项目。选择完水平同步能力后，按 Enter。

Xconfigurator 接下来提示您输入监视器的垂直同步速率。选择最接近监视器规格的垂直同步范围并按 Enter。

如果 Xconfigurator 无法检测视频卡上的显存容量，它将显示一个对话框，提示您从列表中选择一个显存容量。选择最接近视频卡内存容量的数值并按 Enter。

Xconfigurator 提示您识别时钟芯片——视频卡上的一个定时设备。您可以放心地按 Enter 接受默认选择，该选择标记为 No Clockchip Setting (recommended)（无时钟芯片设置（推荐））。

然后，Xconfigurator 显示一个“选择视频模式”对话框，其中包含视频模式列表，即像素分辨率和颜色深度的组合，例如 800 × 600 像素或 1,280 × 1,024 以及每像素 16 位或 24 位，如图 2-2 所示。您的显卡或监视器仅支持某些视频模式，因此如有必要，请再次参考监视器手册。

![](img/5fe8f856723cde0b366f73584b9e64b8_40_0.png)

按 Tab 键将光标移动到视频模式上，然后按空格键选择该模式。您可以选择任意数量的模式。然后按 Tab 键选择 OK（确定）按钮并按 Enter。

接下来，Xconfigurator 为您提供启动 X 以测试配置的机会。您应该按 Enter。会出现图形 X 屏幕，Xconfigurator 显示一个对话框，询问您是否能看到文本。用鼠标单击关闭对话框。

最后，Xconfigurator 会在 /etc/X11 目录中写入 XF86Config-4 文件并退出。这完成了 X 配置。下次重启电脑时，X 应该启动，并且您应该能看到一个图形登录屏幕。

## 配置打印机

Red Hat 安装程序不包含打印机配置步骤。但是，只要 Linux 内核能够检测到电脑的并行端口，您就可以从 X 工具程序中配置打印机。要查看 Red Hat Linux 是否检测到并行端口，请在终端窗口中输入 `dmesg | grep par`。以下是该命令的典型输出：

```text
dmesg | grep par
parport0: PC-style at 0x378 [SPP,PS2]
parport0: no IEEE-1284 device present.
lpd: using parport0 (polling)
```

第一行以 `parport0` 开头，表明 Linux 检测到了并行端口。文本 `parport0` 是“Linux 术语”，指并行端口零，即第一个并行端口（在 DOS 和 Windows 中称为 LPT1）。

要设置打印机，您必须正在运行 X。从图形登录屏幕登录为 root，并从 GNOME 桌面选择 Programs->System->Printer Configuration（程序->系统->打印机配置）。打印机配置工具名为 `printconf-gui`。图 2-3 说明了其主要窗口。

![](img/5fe8f856723cde0b366f73584b9e64b8_41_0.png)

**图 2-3** *printconf-gui 使您可以管理打印机。*

单击 New（新建）按钮以配置新打印机，这将启动 Red Hat 的新打印机配置向导。单击 Next（下一步）按钮开始配置打印机，首先选择打印机类型并为其命名，如图 2-4 所示。如果打印机连接到您的电脑，请单击 Local Printer（本地打印机），然后单击 Next 继续。

![](img/5fe8f856723cde0b366f73584b9e64b8_42_0.png)

**图 2-4** 在 printconf-gui 中配置打印机

在图 2-4 中，已选择了本地打印机，并且队列，即打印机名称，已设置为 lp1。下一步是指定如何访问打印机（见图 2-5）。

> lp1 代表 Line Printer 1（行打印机 1）。Linux 使用命名的打印机队列来区分打印机。队列还作为打印作业和发送到特定打印机的相关文件的临时存储区域。

![](img/5fe8f856723cde0b366f73584b9e64b8_42_1.png)

**图 2-5** 在 printconf-gui 中将打印机名称关联到打印机设备

在本文档中，我们假设打印机连接到电脑的并行端口。选择与打印机所连接的并行端口对应的设备——在大多数情况下，这将是 /dev/lp0，即 DOS/Windows LPT1 打印机端口的 Linux 等效项。单击 Next 继续。

第 10 课解释了 Linux 打印模型以及如何自定义 Red Hat Linux 以获得打印机的最佳效果。

在下一个对话框“选择打印驱动”中，如图 2-6 所示，向下滚动列表直到找到打印机的制造商，单击名称，然后选择您的打印机及相应的驱动文件。单击 Next 继续。最后一个对话框总结了您所做出的打印机配置（见图 2-7）。检查以确保其正确，然后单击 Finish（完成）以完成配置过程。

![](img/5fe8f856723cde0b366f73584b9e64b8_43_0.png)

![](img/5fe8f856723cde0b366f73584b9e64b8_43_1.png)

如果一切运行正常，您应该在 printconf-gui 的显示中看到您的打印机，如图 2-8 所示。

![](img/5fe8f856723cde0b366f73584b9e64b8_44_0.png)

*图 2-8* *新配置的打印机出现在 printconf-gui 的主对话框中。*

最后一步是打印测试页以确认打印机已正确配置。首先，从菜单栏中选择 Test→Print ASCII Test Page（测试→打印 ASCII 测试页）以确保简单文本正确打印，然后选择 Test→Print Postscript Test Page（测试→打印 Postscript 测试页）以确认图像和其他图形元素正确打印。

## 获取 Red Hat Linux 安装帮助

Red Hat Linux 在大多数具有受支持硬件的电脑上都能顺利安装。但是，如果您遇到文本模式或专家模式安装都无法解决的困难，经验丰富的帮助只需几次点击即可得到。实际上，即使您的安装运行完美无缺，您可能会发现以下一些链接和资源很有价值且信息丰富。

Red Hat 在网络上提供了完整的 manuals（手册）集合。对于这些前两课未解决的安装和初始配置问题，请务必查看以下一个或两个链接：

- [官方 Red Hat Linux x86 安装指南](http://www.redhat.com/support/manu...)：`http://www.redhat.com/support/manu...`
- [官方 Red Hat Linux 入门指南](http://www.redhat.com/support/manu...)：`http://www.redhat.com/support/manu...`

这两份指南是安装 Red Hat Linux 和基本自定义的权威参考。

位于 `http://www.redhat.com/apps/support/` 的 Red Hat 知识库是另一个丰富的信息来源。如果您遇到了问题，其他人很可能也遇到了，因此请使用知识库搜索解决方案。

第三个可能的信息来源是产品勘误和更新，位于 `http://www.redhat.com/apps/support/updates.html`。

最后，其他 Red Hat Linux 用户有时是最好的信息来源。Red Hat 邮件列表的存档包含大量有用信息（以及一些不太有用的信息）。

