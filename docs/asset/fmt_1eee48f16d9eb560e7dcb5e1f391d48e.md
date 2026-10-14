
## CHOOSE A ROOT PASSWORD

安装完成后启动 Linux 时，你将使用用户名 root 和你选择的密码登录。如果你计划让他人使用你的 Linux 系统，请确保选择的 root 密码不是他们容易猜到的（图 1-13）。选一个好密码，并在 **Root Password** 和 **Confirm** 框中输入。

由于 root 用户（也称为超级用户）可以完全访问 Linux 系统上的所有内容，你应仅将此选项用于系统管理任务，例如安装新软件和配置系统服务。你也可以在此屏幕上为日常任务添加额外的用户账户。如果家庭或办公室有多个人会使用 Linux，请为每个人创建各自的账户。

## CONFIGURE X WINDOWS

此时，安装程序启动`Xconfigurator`（X Windows 配置程序），它将探测你的系统以确定你拥有的显示器和显卡类型，并安装合适的 XFree86 服务器。XFree86 是 X Windows 系统在 PC 兼容处理器上的免费实现，是 GNU 项目的一部分。

![](img/3137cdda7122042e86dbeafe9840d4ed_54_0.png)

图 1-12：配置系统时钟

![](img/3137cdda7122042e86dbeafe9840d4ed_54_1.png)

图 1-13：选择 root 密码

## DEFINING YOUR MONITOR

在选择显卡后，如果`Xconfigurator`能够自动检测到你的显示器，则会显示该设备的名称。如果不能，`Xconfigurator`会显示一个显示器列表供你选择。如果你的显示器在列表中，请选择它。如果不在列表中且你有制造商的技术规格，请选择 Custom，`Xconfigurator`将提示你选择显示器的特性。但要小心——如果你选择了一个“相似”的显示器，而你的显示器无法处理某种显示模式，则可能损坏显示器。更安全的选择是 Generic Monitor 或 Generic Multisync。

## DEFINING YOUR VIDEO CARD

如果`Xconfigurator`能识别出你的显卡以及安装了多少显存，它会在显示卡名称的屏幕中显示这些信息（图 1-14）。只需按 ENTER 继续即可。

![](img/3137cdda7122042e86dbeafe9840d4ed_55_0.png)

图 1-14：视频探测结果

如果`Xconfigurator`无法自动检测你的显卡，它会显示一个显卡列表供你选择。如果你的显卡不在列表中，Linux 可能不支持它。然而，如果你有显卡的技术文档，你可以选择 Unlisted Card 并尝试通过将显卡的视频芯片组与`Xconfigurator`提供的选项紧密匹配来配置它。

`Xconfigurator`可能会询问你的显卡安装了多少显存。如果你不知道，请查阅文档。猜错也不会有坏处，但 X Windows 可能无法正确启动。如果所选显卡可能具有视频时钟芯片，`Xconfigurator`会列出时钟芯片。推荐选择是 No Clockchip 设置，因为 Linux 在大多数情况下可以检测到正确的时钟芯片。

## CUSTOMIZING THE X CONFIGURATION

如果选择 Customize X Configuration 复选框并按下 Next，`Xconfigurator`随后会提示你选择希望使用的视频模式。对大多数人来说，800 by 600 分辨率配合 16 位颜色就足够好了。如果你的显示器和显卡支持更高分辨率，也可以选择。 如果你选择了多个视频模式，在运行 X Windows 时可以通过按 CTRL-ALT-PLUS 在模式间切换。

完成后，`Xconfigurator`会将你的所有配置选择记录在`/etc/X11/XF86Config`文件中。你可能会觉得浏览此文件很有趣，但除非你真的知道自己在做什么，否则不要对其进行任何更改。

使用 Test Configuration 按钮验证你的 X 配置是否有效。如果无法启动 X Windows，或显示效果不佳（过大、过小、颜色错误等），你可以在安装后再次运行`Xconfigurator`命令，并稍后尝试不同的设置选项。

## START X WINDOWS AT BOOT TIME?

如果你想要完全的图形界面，请在按下 Next 按钮前勾选 Use Graphical Login 按钮，你的系统在启动时会进入 X Windows 模式。如果你不选择图形登录，启动时将出现文本模式 shell 提示符。登录后，你可以使用`startx`命令启动 X Windows。

## INSTALLING PACKAGES

完成 X Configuration 步骤后，你会看到一个显示 About to Install 的屏幕。按下 Next 按钮，安装程序

## 关机和重启

当你看到 **Congratulations** 屏幕时，你几乎已经到达终点线。如果你选择的是无分区安装方法，请将启动盘留在软盘驱动器中——否则现在将其取出。按下 **Exit** 按钮继续，然后会有一堆消息显示各种系统正在关闭。然后你将启动进入你宏伟而辉煌的新 Linux 系统。你必须在系统重启前 **取出安装光盘**，否则你可能会发现自己重新运行安装程序。

如果你为启动选项选择了文本模式 shell 提示符，会出现类似这样的提示：

```
[root@localhost /root] #
```

如果你熟悉 Linux 命令，可以在井号（#）提示符处输入它们。否则，使用`startx`命令启动 GNOME 图形界面，然后继续阅读第 2 章，“The Linux GUI。”

## 安装后：配置

成功安装 Linux 后，你需要采取几个步骤来让所有硬件与 Linux 正常工作。在本节中，你将学习如何配置你的打印机、声卡和 CD-ROM 驱动器。

### 配置打印机

要配置打印机，从 shell 提示符输入`printtool`命令，或点击 **Gnome Foot • System • Control Panel**，然后选择打印机图标。当 **Print System Manager** 窗口出现时，点击 **Add** 按钮（图 1-16）。

Linux 会询问打印机如何连接到你的计算机；最可能的响应是 **Local Printer**，这意味着它直接插入计算机的背面。如果你的打印机在网络上，请向管理员询问配置 Linux 所需的信息。按下 **OK** 继续。

在 **Edit Local Printer Entry** 屏幕（图 1-17）上，保留默认值，然后按下 **Select** 按钮继续。

![](img/3137cdda7122042e86dbeafe9840d4ed_59_0.png)

*Figure 1-16: Adding a printer definition*

![](img/3137cdda7122042e86dbeafe9840d4ed_59_1.png)

*Figure 1-17: Configuring a printer*

在 Configure Filter 屏幕（图 1-18）上，选择最接近你的打印机，然后选择合适的纸张尺寸和分辨率。

![](img/3137cdda7122042e86dbeafe9840d4ed_60_0.png)

*Figure 1-18: Specifying printer model and specs*

按两次 OK 返回 Print System Manager 窗口，然后选择 lpd • Restart lpd 以激活你的打印机。完成后，选择 PrintTool • Quit 退出。

### 配置声卡

要配置声卡，从 shell 提示符输入`sndconfig`命令。当 Sound Configuration Utility 屏幕出现（图 1-19）时，按下 OK 探测你的系统。如果探测找到可以自动配置的声卡，它将进行配置。否则你必须从列表中选择你的声卡并输入端口、IRQ 和 DMA 信息。你从 Windows 设备管理器获得的信息在这里会有所帮助。做出选择后，`sndconfig`会播放声音和音乐片段并询问你是否能听到它们。如果不能，请返回并尝试不同的设置。

![](img/3137cdda7122042e86dbeafe9840d4ed_61_0.png)

将音乐 CD 插入驱动器，**GNOME CD Player** 应该会弹出并开始播放它。如果你无法让声卡工作，请阅读安装光盘上`/doc/HOWTO`目录中的`SOUND-HOWTO`文件。

## 访问 CD-ROM 上的文件

发出`mount`命令后，列出 CD-ROM 上的文件以查看挂载是否成功，使用以下命令：

- `cd /mnt/cdrom`    切换到 CD 目录。

- `ls`    列出 CD 上的文件。

如果你在`mount`命令中尝试设备名并收到错误，或你的`ls`命令没有显示任何文件，只需选择另一个设备名再试一次——这样不会造成任何损害。
