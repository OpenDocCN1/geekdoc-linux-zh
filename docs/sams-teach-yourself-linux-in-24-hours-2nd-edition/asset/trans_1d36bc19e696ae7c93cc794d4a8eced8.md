
> OpenLinux 不允许你尝试选择一个超过 Linux 分区可用空间的安装大小。你必须选择一个较小的安装。如果有硬盘空间，你可以通过按后退按钮返回安装对话框来创建更大的 Linux 分区，或稍后创建额外的 Linux 分区。

9. OpenLinux 现在显示一个对话框并要求你选择键盘型号和布局。滚动键盘列表，然后单击你的型号。接下来，选择一个键盘布局（例如 U.S. English）。要测试所选键盘，请在“Test here”字段中单击并输入一些文本。完成后，单击“Next”按钮继续。另外，请注意，在你继续配置过程的同时，软件包安装仍在向你的 Linux 分区复制文件！

10. OpenLinux 现在要求你选择视频卡，如图 2.3 所示。这是安装过程中的关键步骤，可确保你能以计算机视频卡和显示器最佳可能的分辨率运行 X Window System。查看“Card Type”字段，确认计算机的视频卡是否已正确列出。接下来，单击视频卡上安装的视频 RAM 数量（例如 2MB）。即使视频卡已正确列出，也请单击“Probe”按钮以获取更准确的信息。这会运行 XF86_SVGA X11 服务器来探测图形卡以获取设置信息。

### 图 2.3
OpenLinux 应能自动检测你的视频卡，但你可以单击“Probe”按钮以获得更具体的设置。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_48_0.png)

- 11. 单击“Probe”按钮后，会出现一个对话框，要求你确认探测。单击“Probe”按钮继续，或单击“Abort”按钮取消探测。
- 12. 如果探测成功，你的屏幕会变黑并出现一个带有“OK”按钮的对话框。单击“OK”关闭对话框，然后单击“Next”继续配置 X Window System。
- 13. 你现在会看到一个“Select Monitor”对话框，其中列出了显示器以及水平和垂直同步范围，如图 2.4 所示。滚动显示器列表，然后单击与系统一起使用的型号。如果列表中没有你的显示器，请在滚动列表下方输入显示器的名称和同步范围。单击“Monitor name”字段，然后输入名称。通过单击上下箭头输入低和高水平同步范围，然后对低和高垂直同步范围执行相同操作。完成后，单击“Next”按钮。

### 图 2.4
滚动显示器列表，然后选择特定显示器，或输入有关计算机显示器的详细信息。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_49_0.png)

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_49_1.png)

> 请务必为显示器输入正确的同步值！错误的设置可能会损坏你的显示器！你已被警告！

14. 下一个对话框要求你选择首选视频模式，如图 2.5 所示。单击所需的分辨率，例如 800×600，表示显示器上可用的像素数（横向和纵向）。不要选择超出显示器能力的分辨率！接下来，从屏幕右上角的列表中单击所需的显示深度。完成后，单击“Test This Mode”按钮测试你的设置。

### 图 2.5
“Select Video Mode”对话框用于为显示器和显卡选择最佳分辨率和颜色深度。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_50_0.png)

15. 会出现一个确认对话框。单击“OK”继续。屏幕变清，并出现一个代表性的 X11 显示，持续约 10 秒，如图 2.6 所示。当安装对话框重新出现时，单击“Next”按钮继续。

### 图 2.6
在 X11 配置期间，OpenLinux 允许你测试显卡和显示器，以确保设置正确。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_50_1.png)

16. OpenLinux 现在要求你设置 root 密码。这是系统管理员——也就是你！的密码。输入密码，然后按 Enter，再次输入。不要忘记此密码！你需要在 OpenLinux 会话期间执行重要配置任务时使用此密码。完成后，单击“Next”按钮。

> 好的密码至少有八个字符，并包含字母和数字的混合。

17. 下一个对话框要求你至少向 OpenLinux 系统添加一个新用户，如图 2.7 所示。首先单击“Real Name”字段并输入你的姓名。按 Enter，然后输入“Login name”。按 Enter，然后输入密码。按 Enter，然后再次输入密码。接下来，单击 bash、tcsh 或 zsh 以选择“Login Shell”。完成后，单击“Add User”按钮。要继续，请单击“Next”按钮。

### 图 2.7
“Set Login Name(s)”对话框用于在 OpenLinux 安装期间创建新用户。（安装后也可以添加或删除其他用户。）

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_51_0.png)

> 登录名通常是个人姓名的首字母，后跟姓氏。例如，Julie Lewis 的登录名是 jlewis，Jeff Goldfarb 的登录名是 jgoldfarb。

18. 你现在可以在图 2.8 所示的对话框中设置网络。如果你的计算机已连接到网络并且已安装网络卡，请输入网络的 IP 地址（例如 192.168.1.2）、主机名（例如 wishbone.erols.com）、Netmask 和 Gateway。如果你的网络有域名服务器，请输入其 IP 地址。如果没有网络卡，请单击“Next”按钮继续。

### 图 2.8
如果已安装网络卡，请使用“Set Up Networking”对话框输入网络信息，例如计算机的 Internet 协议或 IP 地址号码。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_52_0.png)

> 如果你跳过此步骤，稍后仍可以添加和配置网络卡。有关详细信息，请参阅第 3 小时“Post-Installation Issues”。

19. 为了确保 OpenLinux 准确跟踪时间，现在要求你选择时区。滚动区域列表，然后单击你的时区。如果计算机的硬件时钟设置为本地时间，请单击“Hardware Clock Runs in Local Time”项，然后单击“Next”继续。

20. 现在放松一下！是时候玩一个熟悉的下落方块游戏了，同时 OpenLinux 继续将文件复制到硬盘。单击“New Game”开始游戏。使用光标键旋转、移动或放置方块。在你玩游戏的同时，屏幕底部的进度条可帮助你监控安装进度。当安装完成时，单击“Finish”按钮。

## 完成你的 Linux 安装
恭喜！坚持住，因为你几乎完成了 OpenLinux 的安装！单击“Finish”后，OpenLinux 会重新启动计算机到 K 桌面环境的 K 显示管理器登录屏幕（如图 2.9 所示）。

### 图 2.9
你在 K 显示管理器中首次看到 OpenLinux，在那里你必须登录 Linux。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_53_0.png)

虽然你现在如果想的话可以登录，但安装中仍有一个重要的步骤！如果你想启动到 Linux，必须先关闭、重新启动，然后从 Windows 安装 BootMagic。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_53_1.png)

> 有经验的 Linux 用户可能想使用 LILO，但应知道此时与之前的 OpenLinux 安装不同，LILO 已被安装，并且默认的 /etc/lilo.conf 配置文件已配置为从根 Linux 分区启动 LILO。这可能不是你想要的，但这是支持商业引导加载程序（如 System Commander 或包含的 Boot Magic 版本）的正确配置。虽然有经验的 LILO 用户可能会使用引导软盘或将 LILO 安装到 DOS 分区的 Master Boot Record，但 MBR 是 Boot Magic 所需的。此时你必须决定是否使用 BootMagic 或 LILO。如果你决定使用 LILO，以 root 身份登录 OpenLinux，然后编辑 /etc/lilo.conf 以指向 MBR，并插入一个支持启动 DOS 的条目。（默认情况下没有包含，并且你可能已经注意到安装过程不会提供配置 LILO 的机会。）如果你决定不单独使用 LILO，BootMagic 然后使用 LILO（安装在你的 Linux 分区上）来启动 OpenLinux。有关更多信息，请参阅 /usr/doc/lilo 目录下的 README 文件。

单击“Shutdown”按钮，然后选择“Shutdown”，并重新启动以重新启动到 Windows。当 Windows 桌面出现时，从“开始”菜单的 OpenLinux 文件夹中单击“Post Install Boot Magic”菜单项。确保你的 OpenLinux CD-ROM 已插入计算机。BootMagic 设置窗口会出现，如图 2.10 所示。
