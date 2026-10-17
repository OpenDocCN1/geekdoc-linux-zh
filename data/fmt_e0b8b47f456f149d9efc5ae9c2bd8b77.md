
一旦你以错误的用户连接（例如，作为 `nobody`，这在设置了 `map to guest = bad user` 时经常发生），Windows 资源管理器将不接受再次以不同用户连接的尝试。将不会有任何字节传输到 Samba，但你仍会看到一个愚蠢的错误消息，让你认为 Samba 拒绝了访问。使用 `smbstatus` 检查活动连接。终止 PID。你仍然无法重新连接，当你尝试时，你会得到可怕的 `You can't connect with a second account from the same machine` 消息。并且你没有看到任何到达 Samba 的字节（查看日志；使用 `ethereal`）表明重新连接尝试。关闭所有资源管理器窗口。这会让 Windows 忘记其在内存中缓存的已建立连接。然后以正确的用户重新连接。最好的方法是使用 DOS 终端窗口并 `first do net use z: \\GANDALF\print$ /user:root.` 检查 `smbstatus` 以确认你是以不同账户连接的。现在打开 `Printers` 文件夹（在 Samba 服务器上的 `Network Neighorhood` 中），右键单击相关打印机，并选择 `Connect`......

### 21.19.7 避免以错误用户连接到 Samba 服务器

你通过 `smbstatus` 看到你是以用户 `nobody` 连接的，但你希望是 `root` 或打印机管理员。这可能是因为 `map to guest = bad user`，它在你提供（可能是意外）了错误的用户名时，静默地以访客账户连接了你。如果你想防止这种情况，请删除 `map to guest`。

### 21.19.8 从 Adobe 驱动升级到 CUPS 驱动

这些信息来自关于在 Microsoft Windows NT/200x/XP 客户端上从 Adobe 驱动升级到 CUPS 驱动时遇到的问题的邮件列表帖子。首先删除所有使用旧 Adobe 的打印机。然后删除所有旧的 Adobe 驱动。（在 Windows 200x/XP 上，在 `Printers` 文件夹的背景上右键单击，选择 `Server Properties`...，选择 `Drivers` 选项卡，并在此处删除）。

### 21.19.9 无法在使用作为 PDC 的 Samba 服务器上使用 "cupsaddsmb"

你使用“裸”的 root 用户名吗？尝试这样操作：`cupsaddsmb -U DO-\ MAINNAME\root -v printername>`（注意两个反斜杠：第一个用于“转义”第二个）。

### 21.19.10 删除的 Windows 200x 打印机驱动仍然显示

在客户端删除打印机不会删除驱动（要验证，右键单击 `Printers` 文件夹的白色背景，选择 `Server Properties`，然后点击 `Drivers` 选项卡）。当你尝试安装同名的打印机时，这些相同的旧驱动将重新显示。如果你想更新为新驱动，请先删除旧的。只有没有其他打印机使用相同的驱动时，删除才是可能的。

### 21.19.11 Windows 200x/XP 本地安全策略

本地安全策略可能不允许安装未签名的驱动程序（“本地安全策略”可能完全不允许安装打印机驱动程序）。

### 21.19.12 管理员无法为所有本地用户安装打印机

Windows XP 以“每用户”为基础处理 SMB 打印机。这意味着每个用户都需要自己安装打印机。要使打印机对每个人可用，你可能想要使用 Win XP 内置的 IPP 客户端功能。添加一个打印路径为 `http://cupsserver:631/printers/printername` 的打印机。我们仍在研究这个问题。也许登录脚本可以自动为所有用户安装打印机。

### 21.19.13 NT 客户端上的打印更改、通知功能

对于 NT++ 客户端的打印更改、通知功能。这些需要先运行 `Server` 服务（在 XP 中重命名为 `File & Print Sharing for MS Networks`）。

### 21.19.14 Win XP-SP1

Win XP-SP1 引入了 Point and Print 限制策略（此限制不适用于“Administrator”或“Power User”组的用户）。在组策略对象编辑器中，转到 `User Configuration -> Administrative Templates -> Control Panel -> Printers`。策略自动设置为 `Enabled`，并且 `Users` 只能 `Point and Print` 到 `their Forest` 中的 `machines`。你可能需要将其更改为 `Disabled`，或者 `Users` 只能 `Point and Print` 到这些服务器，以使得从 Samba 下载驱动程序成为可能。

### 21.19.15 无法在 Windows 200x/XP 上为所有用户设置打印选项

你是怎么做到的？我敢打赌你是用错了方法（尽管很难找到正确的方法）。有三种不同的方式可以引导你进入一个*看似*能设置所有选项的对话框。这三个对话框*看起来*是一样的，但只有其中一个能做到你意图中的事情。你需要具有 `管理员` 或 `打印管理员` 权限才能为所有用户执行此操作。以下是我在 XP 上的操作方法：

- `A 第一种错误方法：`

  - (a) 打开 `打印机` 文件夹。

  - (b) 右键单击打印机（`remoteprrinter on cupshost`），并在上下文菜单中选择 `打印首选项`…

  - (c) 仔细查看此对话框并记住它的样子。

- `B 第二种错误方法：`

  - (a) 打开 `打印机` 文件夹。

  - (b) 右键单击打印机（`remoteprrinter on cupshost`），并在上下文菜单中选择 `属性`。

  - (c) 单击 `常规` 选项卡。

  - (d) 单击 `打印首选项`…按钮。

  - (e) 打开一个新对话框。保持此对话框打开状态，并返回到父级对话框。

- `C 第三种也是正确的方法：`

  - (a) 打开 `打印机` 文件夹。

  - (b) 单击 `高级` 选项卡。（如果所有内容都是“灰色的”，则说明你未以具有足够权限的用户登录。）

  - (c) 单击 `打印默认值`…按钮。

  - (d) 在两个新选项卡中的任意一个上，单击 `高级`…按钮。

  - (e) 打开一个新对话框。将此对话框与步骤“B,5”或“A,3”中外观相同的其他对话框进行比较。

你看到区别了吗？我也没看到。然而，只有最后一个，即通过步骤“C,1 到 C,6”到达的对话框，才会永久保存任何设置，并成为新用户的默认设置。如果你希望所有客户端都获得相同的默认值，你需要在客户端下载驱动程序之前，以*管理员*身份（在 `smb.conf` 中为*打印机管理员*）执行这些步骤（客户端随后可以按照*A*或*B*步骤设置自己的*每用户默认值*）。

### 21.19.16 Windows 客户端驱动程序设置中最常见的错误

不要使用*针对速度进行优化*，而应使用*针对可移植性进行优化*（Adobe PS 驱动程序）。不要使用*页面独立性*：否。始终选择*页面独立性：是*（Microsoft PS 驱动程序和用于 Windows NT/200x/XP 的 CUPS PS 驱动程序）。如果字体有问题，请使用*作为软字体下载到打印机*（Adobe PS 驱动程序）。对于 TrueType 下载选项，选择*轮廓*。如果你在使用非 PS 打印机时遇到问题并且有选择的话，请使用 PostScript Level 2。

### 21.19.17 cupaddsmmb 无法与新安装的打印机一起工作

`症状：` `cupaddsmmb` 的最后一条命令未成功完成。如果 `cmd` = `smdriver printername printername` 的结果为 `NT_STATUS_UNSUCCESSFUL`，则可能是 Samba 尚未识别该打印机。它是否显示在“网上邻居”中？它是否显示在 `rpcclient hostname -c 'enumprinters’` 中？重启 `smbd`（或向 `smbstatus` 列出的所有进程发送 `kill -HUP`），然后重试。

### 21.19.18 /var/spool/samba/ 上的权限在每次重启后都会重置
