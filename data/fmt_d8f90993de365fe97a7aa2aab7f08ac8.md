
浮点数有两种大小：`float`（单精度）和 `double`（双精度）。带有 CentOS 7 的 `g++` 编译器提供了表 A-14 列出的浮点大小。

| 类型 | 长度 | 最大 |
| :--- | :--- | :--- |
| `float` | 4 bytes | 3.40282E38 (7位) |
| `double` | 8 bytes | 1.79769E308 (15位) |

表 A-14 浮点大小

## 活动 A-10：提供数据类型

所需耗时：10 分钟
目标：给定示例数据，提供存储的数据类型。
描述：在此活动中，你通过完成表 A-15 来练习为示例数据指定数据类型。

| 数据示例 | 数据类型 |
| :--- | :--- |
| A | |
| 1024 | |
| 66 | |
| 1023.996 | |
| # | |
| -32700 | |
| -88888.778 | |
| 65000 | |
| -2,000,000,000 | |
| 777777789 | |

表 A-15 数据类型答案

# 使用 Hyper-V 虚拟化

## 开始使用 Hyper-V 虚拟化

许多版本的 Windows包含了 Hyper-V 虚拟化技术，它允许你在物理宿主机上运行虚拟化的计算机系统。你可以像使用物理计算机系统一样使用和管理这些系统；然而，它们存在于虚拟化且隔离环境中。Windows 10 中的此功能称为客户端 Hyper-V，它与 Windows Server 2012 Hyper-V 使用的技术相同。

X86 虚拟化允许多个操作系统同时安全、高效地共享资源。这种虚拟化用于模拟一个完整的硬件环境（即虚拟机），未修改的客户操作系统可以在其中运行。虚拟化于 2006 年添加到大多数 x86 处理器（Intel VT-x 或 AMD-V）中。

要使用虚拟化，必须在 BIOS 中启用 VT-x或 AMD-V选项。你可以在显示启动闪屏时按下相应的按键（F2 或 Delete）访问 BIOS 设置菜单。Intel VT 或 AMD-V 的 BIOS 设置通常位于 Chipset（芯片组）或 Security（安全）菜单中。

## 配置宿主机

为了使两台虚拟机能够连接互联网并彼此通信，你将安装 Hyper-V 体系程序和 Internet 连接共享（ICS）。接下来，将 Host01 计算机上的现有网络适配器连接到互联网。然后创建一个外部虚拟交换机，它与虚拟机有独立的连接。你将启用 ICS 以与内部交换机共享互联网连接。

按照以下步骤准备运行 Windows 10 的宿主机，以支持虚拟环境。

- 1. 以具有管理权限的用户身份登录到你的宿主机 PC。
- 2. 在任务栏的“搜索网络和 Windows”处输入 Windows Features（Windows 功能）。
- 3. 要安装 Hyper-V 体系程序，点击“启用或关闭 Windows 功能”，勾选“Hyper-V”，然后点击“确定”。
- 4. 等待 Windows 完成请求的更改，然后点击“立即重启”。

# 附录 B 使用超虚拟化

- 1. 等待更改应用。
- 2. 以具有管理权限的用户账户登录 Windows 10 桌面。
- 3. 要启动 Hyper-V 管理器，在开始屏幕的“搜索网络和 Windows”处输入“Hyper-V 管理器”。
- 4. 双击“Hyper-V 管理器”。
- 5. 点击 Hyper-V 管理器下的宿主机名称。
- 6. 要为虚拟机创建网络连接，点击“操作”窗格中的“虚拟交换机管理器”。
- 7. 创建虚拟交换机。在“新建虚拟交换机”处输入“外部网络连接”。点击“确定”。点击“是”。
- 8. 等待更改应用。
- 9. 要为虚拟机连接启用增强会话模式，点击右窗格中的“Hyper-V 设置”，点击“增强会话模式策略”，然后点击“允许增强会话模式”。在“用户”下，点击“增强会话模式”，然后选择“使用增强会话模式”。点击“确定”。
- 10. 保持 Hyper-V 管理器窗口打开以便后续操作。
- 11. 要配置 ICS，点击任务栏上的网络图标，点击“打开网络和共享中心”，然后点击“更改适配器设置”。右键点击以网适配器，选择“属性”，点击“共享”选项卡，然后点击“允许其他用户通过此计算机连接”。点击“确定”。关闭“网络”窗口。
- 12. 要为 `.iso` 操作系统文件创建文件夹，点击“开始”，点击“文件资源管理器”，点击“此电脑”，双击“本地磁盘 (C:”；右键点击空白处，指向“新建”，“文件夹”，在“新建文件夹”处输入“ISOFiles”，然后按回车键。

> 请参考书籍的前言以查找操作系统文件的来源。例如，如果你从 DreamSpark 下载了 Windows 10 `.iso` 文件，请将 `.iso` 文件复制到 `C:\`

![](img/290e46d5832f20e3707f4841e4e6d75a_621_0.png)

- 13. 要为虚拟机文件创建文件夹，点击任务栏上的文件资源管理器图标，双击“本地磁盘 (C:)”；右键点击空白处，指向“新建”，“文件夹”，在“新建文件夹”处输入“VirtualMachines”，然后按回车键。关闭文件资源管理器窗口。
- 14. 要在此宿主机上创建 TextShare 文件夹，点击“开始”，点击“计算机”，双击“本地磁盘 (C:)”；注意你的操作系统驱动器可能有不同的名称。右键点击右窗格中的空白处，指向“新建”，“文件夹”，输入“Text-Share”，并按回车键。右键点击 TextShare，点击“属性”，点击“共享”选项卡，并点击“共享”。输入 everyone，点击“添加”，点击“共享”，点击“完成”。当询问是否要对所有公共网络启用网络发现和文件共享时，点击“是”，然后点击“关闭”。关闭“本地磁盘 (C:)”窗口。
- 15. 要共享 Host01 计算机上的打印机，右键点击“开始”，点击“控制面板”，点击打印机图标并选择“小图标”。点击“设备和打印机”，点击“添加打印机”，

# 在 Hyper-V 中安装操作系统

如果我需要的打印机未列在列表中，点击“使用手动设置添加打印机或网络打印机”，并连续两次“下一步”。滚动制造商列表，点击“Generic”，点击“Generic/Text Only”，然后点击“下一步”。在“打印机名称”框中输入 SharedPrinter，连续两次“下一步”，然后点击“完成”。点击“设备和打印机”窗口。

访问 www.cengagebrain.com 并

![](img/290e46d5832f20e3707f4841e4e6d75a_622_0.png)

21. 要添加步骤 5–7 中创建的硬盘，点击 SCSI 控制器（SCSI Controller），然后点击添加（Add）。

22. 点击浏览（Browse），点击 Windows (C:\)，滚动并双击 VirtualVirtualMachines，点击 Windows 10 – Disk1.vhdx，然后点击打开（Open）。点击应用（Apply）。

23. 对 Windows 10 – Disk2.vhdx 重复步骤 21 和 22。

24. 要添加 Windows 10 `.iso` 文件，点击 SCSI 控制器（SCSI Controller），点击 DVD 驱动器（DVD Drive），然后点击添加（Add）。点击映像文件（Image File）。

25. 点击浏览（Browse），导航至 `C:\ISOFiles`，点击 Windows 10 `.iso` 文件，然后点击打开。点击应用。

> 参考书的前言以查找您正在使用的特定 `.iso` 文件名。如果您是从 DreamSpark 下载的 `.iso` 文件，文件名为 `en_windows_10_education_x64_6848120.iso`。

![](img/290e46d5832f20e3707f4841e4e6d75a_624_0.png)

26. 要更改启动顺序，点击固件（Firmware），点击 DVD 驱动器（DVD Drive），并点击向上移动（Move Up），直到 DVD 驱动器成为第一个项目。点击网络适配器（Network Adapter），然后点击向下移动（Move Down），直到网络适配器成为最后一个。

27. 验证固件是否将 DVD 驱动器列为启动顺序中的项。

28. 要添加客户服务（Guest services），点击集成服务（Integration Services），点击客户服务，然后点击确定。

29. 保持 Hyper-V 管理器（Hyper-V Manager）窗口打开以便后续操作。

## 安装 Windows 10

在虚拟机上安装 Windows 10 与在物理机上安装没有本质区别。执行以下步骤安装 Windows 10 虚拟机，以确保您的虚拟环境与整个过程中使用的环境保持一致。

- 1. 如必要，使用具有管理员权限的用户帐户登录到您的主机 PC。
- 2. 如必要，在开始屏幕的“搜索网络和 Windows”上输入 Hyper-V Manager。双击 Hyper-V Manager。
- 3. 要连接到 Windows 10 虚拟机，右键点击 Hyper-V Manager 中间面板中的 Windows 10。点击连接（Connect）。
- 4. 要启动 Windows 10 虚拟机，点击操作（Action）菜单并点击启动（Start）。在虚拟机连接窗口中点击。
- 5. 当出现“按任意键从 CD 或 DVD ”时，立即按下空格键。
- 6. 根据需要验证并修正语言和其他设置，然后点击下一步（Next）。
- 7. 要继续安装 Windows 10，在提示时点击安装（Install）按钮。
- 8. 等待安装程序启动。
- 9. 当出现“输入密钥以激活 Windows”屏幕时，输入密钥并点击下一步。

## 附录 B 使用 Hyper-V 虚拟化

- 10. 当出现许可条款时，我接受许可条款，然后点击下一步。
- 11. 当被要求选择您喜欢的安装类型时，点击自定义（Custom (advanced)），点击驱动器 0 未分配空间（Drive 0 Unallocated Space），然后点击下一步。
- 12. 等待文件被复制并扩展。
- 13. 当出现“快速开始”（Get going fast）窗口时，点击“使用快速设置”（Use Express settings）。
- 14. 当提示为您的账户选择用户名时，点击“谁将使用此电脑”框中的 Admin01。
- 15. 在“密码 password”处输入 Pa$$word，按 Tab 键，在“重新输入密码”处输入 Pa$$word，在“密码提示”处输入 It’s a Microsoft password，然后点击下一步。
- 16. 等待 Windows 设置桌面。
- 17. 要释放 Windows 10 `.iso` 文件，点击媒体（Media）菜单，点击 DVD 驱动器，然后点击检出（Eject）。
- 18. 要更改计算机名称，在“搜索网络和 Windows”文本框中输入 control，点击控制面板，点击系统和安全，点击点击系统，点击更改设置链接，点击更改，然后在计算机名称处输入 Windows10。双击确定，点击关闭，然后立即重启。
- 19. 要以 Admin01 身份登录，点击操作（Action）菜单，然后点击 Ctrl-Alt-Delete。点击左下角的 Admin01，输入 Pa$$word 作为密码，然后按回车。
- 20. 等待设置完成。
- 21. 要扩展脚本的环境变量，在“搜索网络和 Windows”文本框中输入 control，然后点击控制面板。点击系统和安全，点击点击系统，点击高级系统设置，然后点击环境变量。点击 Path 然后点击编辑。按右方向键，输入 Scripts\，然后点击三次确定。
- 22. 验证 Path 环境变量已正确添加，在“搜索网络和 Windows”文本框中点击命令提示符，输入 ECHOCHO %PATH%，然后按回车。
- 23. 关闭 Windows 10 虚拟机中打开的窗口。
- 24. 要将脚本下载到 Windows 10 虚拟机，使用您的学生帐户登录 www.cengagebrain.com。在“输入 ISBN、作者或标题”处输入 caswell，然后点击放大镜状搜索栏。点击《Guide to Parallel Operating Systems with Windows 10 and Linux》，点击免费材料（Free Materials）标签页。

- 4. 检查“开始之前”（Before You Begin）页面。点击“下一步”三次。
-- 5. 在“New Virtual Hard Disk.vhdx”处输入 CentOS7 – sda。点击“浏览”（Browse），点击 Windows (C:\)，滚动并点击 VirtualMachines，然后点击“选择文件夹”（Select Folder）两次两次。
- 6. 点击“完成”（Finish）。
- 7. 为学生使用创建一个虚拟硬盘，点击“操作”（Actions）窗格中的“新建”（New）。点击“硬盘”（Hard Disk）。
- 8. 检查“开始之前”（Before You Begin）页面。点击两次“下一步”，点击“固定大小”（Fixed Size），然后点击“下一步”。
- 9. 在“New Virtual Hard Disk.vhdx”处输入 CentOS7 – sdb。点击“浏览”（Browse），点击 Windows (C:\)，滚动并点击 VirtualMachines，然后点击“选择文件夹”（Select Folder）。输入大小为 4，然后点击“完成”（Finish）。
- 10. 对 CentOS7– sdc 重复步骤 7 至 9。
- 11. 要创建一个虚拟机，点击“操作”（Actions）窗格中的“新建”（New）。点击“虚拟机”（Virtual Machine）。
- 12. 检查“开始之前”（Before You Begin）页面。点击“下一步”。
- 13. 在“虚拟机”（Virtual Machine）处输入 CentOS 7。点击“浏览”（Browse），点击 Windows (C:\)，滚动并点击 VirtualMachines，点击“选择文件夹”（Select Folder），然后点击两次“下一步”。
- 14. 指定内存，为启动内存输入 1024，勾选“此虚拟机使用动态内存”（Use Dynamic Memory for this virtual machine），然后点击“下一步”。
- 15. 配置网络，点击连接箭头，然后点击“外部网络连接”（External Network Connection）。点击“下一步”。
- 16. 要延迟虚拟硬盘的连接，点击“稍后附加虚拟硬盘”（Attach a virtual hard disk later）。点击“下一步”。
- 17. 检查摘要并点击“完成”（Finish）。
- 18. 等待虚拟机创建。
- 19. 要查看虚拟机设置，点击中间窗格中的 CentOS 7，然后点击“操作”（Actions）窗格中的“设置”（Settings）。
- 20. 要添加步骤 3–6 创建的硬盘，点击“IDE 控制器 0”（IDE Controller 0），点击“硬盘”（Hard Drive），然后点击“添加”（Add）。
- 21. 点击“浏览”（Browse），点击 Windows (C:\)，滚动并双击 VirtualMachines，点击 CentOS7– sda.vhdx，然后点击“打开”（Open）。点击“应用”（Apply）。
- 22. 要添加步骤 7–9 创建的硬盘，点击“SCSI 控制器”（SCSI Controller），然后点击“添加”（Add）。
- 23. 点击“浏览”（Browse），点击 Windows (C:\)，滚动并双击 VirtualMachines，点击 CentOS7– sdb.vhdx，然后点击“打开”（Open）。点击“应用”（Apply）。
- 24. 对 CentOS 7– sdc.vhdx 重步骤 22 和 23。
- 25. 添加 CentOS 7 `.iso` 文件，点击“IDE 控制器 1”（IDE Controller 1），点击“DVD 驱动器”（DVD Drive），然后点击“映像文件”（Image File）。
- 26. 点击“浏览”（Browse），导航到 `C:\ISOFiles`，点击 CentOS 7 `.iso` 文件，然后点击“打开”（Open）。点击“应用”（Apply）。
- 27. 要添加客户服务（Guest services），点击“集成服务”（Integration Services），点击“客户服务”（Guest services），然后点击“确定”（OK）。
- 28. 保持 Hyper-V 窗口打开以便后续操作。

# 安装 CentOS 7

在虚拟机上安装 CentOS 7 从本质上与在物理机上安装没有区别。执行以下步骤安装 CentOS 7 机器，以确保你的虚拟环境与文中使用的环境一致。

- 1. 如必要，以用户 user01 登录你的宿主机 PC，密码为 P@ssword。
- 2. 如必要，在开始屏幕的“搜索网络和 Windows”处输入 Hyper-V Manager。双击 Hyper-V Manager。
- 3. 要连接到 CentOS 7 虚拟机，在 Hyper-V 管理器的中心窗格中右键点击 CentOS 7。点击“连接”（Connect）。
- 4. 要启动 CentOS 7 虚拟机，点击“操作”（Action）菜单，点击“启动”（Start）。在“虚拟机连接”窗口中点击。
- 5. 当下一个窗口提示你安装或测试时，按向上箭头选择 CentOS 7。按回车。
- 6. 当“欢迎 CentOS 7”窗口出现时，确认选择了 English (United States)。
- 7. 在下一个窗口，点击“安装目标”（DESTINATION）。
- 8. 点击 GNOME 桌面并点击“完成”（Done）。
- 9. 指定 GNOME 桌面，点击“软件选择”（SOFTWARE SELECTION）。在左侧点击应用程序（Applications）、办公套件（Office Suite）、开发工具（Development Tools）和安全工具（Security Tools）。
- 10. 设置日期和时间，点击“日期和时间”（Date and Time）设置时区。点击“完成”。
- 11. 点击右下角的“开始安装”（Begin Installation）。
- 12. 设置 root 密码，点击“密码”（PASSWORD），输入 P@ssword，按 Tab 键，输入密码并点击两次“完成”。
- 13. 创建用户，点击“用户创建”（USER CREATION）。输入 User01 作为全名（Full Name），输入 User01 作为用户名（User Name）。创建此用户。输入两次密码。
- 14. 点击两次“完成”（Done）。
- 15. 安装可能需要一小时。完成后，点击“重启”（Reboot）。
- 16. 如果安装再次启动，点击“操作”（Action），然后点击两次“关闭”（Off）。点击“文件”（File），检查启动顺序，确保 IDE 是第一。

# 附录 B 使用 Hyper-V 进行工作

- 17. 系统重启时，输入 1、2，然后输入 c 接受许可协议。登录页面出现，可以选择用户 (user01)。
- 18. 以密码 Password 登录 CentOS 7 用户 User01。

# 完成 CentOS 7 配置

执行以下步骤完成 CentOS 7 虚拟机，确保你的虚拟环境与文中使用的环境一致。你将分区并格式化两个硬盘 sdb 和 sdc。

- 1. 如必要，以用户 User01 登录你的宿主机 PC，密码为 Password。
- 2. 如必要，在桌面上双击 Virtual Machines。
- 3. 以密码 Password 登录 CentOS 7 用户 User01。
- 4. 确认选择了 English 语言并点击“下一步”。
- 5. 使用 Linux。关闭窗口。
- 6. 验证以太网适配器可用，点击屏幕右上角的箭头。如果显示关闭（Off），点击箭头选择“连接”（Connect）。
- 7. 禁用屏幕保护，点击“应用程序”（Applications），点击“系统工具”（System Tools），点击“电源”（Power），点击“从不”（Never）。关闭窗口。
- 8. 要打开终端，右键点击桌面并点击“终端”（Terminal）。
- 9. 输入 sudo install samba，输入 sudo密码。在任何提示处输入 y，然后按回车。
- 10. 开始分区 sdb 磁盘，输入 `sudo fdisk /dev/sdb` 并按回车。输入密码。
- 11. 忽略警告。
- 12. 在 sdb 上创建第一个主分区，等待“Command (m for help)”出现，输入 n 并按回车，输入 1 并多次回车。
- 13. 检查分区并写入分区表，输入 p 并按回车，然后输入 w 并按回车。
- 14. 将分区格式化为 Ext4，输入 `sudo mkfs /dev/sdb1` 并按回车。输入密码。
- 15. 为分区标记，输入 `sudo label /dev/sdb1 Ext4` 然后按回车。如必要，输入密码。
- 16. 开始分区 sdc 磁盘，输入 `sudo fdisk /dev/sdc` 并按回车。如必要，输入密码。
- 17. 忽略警告消息。
- 18. 在 sdc 上创建第一个主分区，等待“Command (m for help)”出现，输入 n 并按回车，输入 p 并按回车，输入 1 并多次回车。
- 19. 检查分区并写入分区表，输入 p 并按回车，然后输入 w 并按回车。
- 20. 格式化分区，输入 `sudo mkfs -t vfat /dev/sdc` 并按回车。输入密码。
- 21. 为分区标记，输入 `sudo label /dev/sd1 Fat` 并按回车。如必要，输入密码。
- 22. 将分区置于 /mnt 目录，输入 `cd /mnt` 并回车。
- 23. 为 sdb1 创建目录，输入 `sudo mkdir sdb1` 并按回车。如必要，输入密码。
- 24. 挂载 sdb1 分区，输入 `sudo mount /dev/sdb1 -t ext4 /mnt/sdb1` 并按回车。如必要，输入密码。
- 25. 为 sdc1 创建目录，输入 `sudo mkdir sdc1` 并按回车。如必要，输入密码。
- 26. 挂载 sdc1 分区，输入 `sudo mount /dev/sd1 -t vfat /mnt/sdc1` 并按回车。如必要，输入密码。
- 27. 返回根目录，输入 `cd ..` 并回车。
- 28. 打开 /etc/fstab 文件进行编辑，输入 `sudo nano /etc/fstab` 并按回车。输入密码。
- 29. 将箭头移动到新行。
- 30. 为 sdb1 添加挂载行，输入以下内容并回车：
  `/dev/sdb1 /mnt/sdb1 ext4 defaults 0 0`
- 31. 为 sdc1 添加挂载行，输入以下内容并回车：
  `/dev/sd1 /mnt/sd1 vfat defaults, dmask=000, fmask=111 0 0`
- 32. 将文件写入磁盘，按 Ctrl+O
- 33. 退出 nano，按 Ctrl+X。
- 34. 重新标记设备，输入 `sudo mount -a` 并回车。如必要，输入密码。
- 35. 验证挂载是否成功，回到桌面，点击“位置”箭头，点击“计算机”，双击 mnt，验证 sdb1 和 sdc 文件夹是否出现，并关闭打开的窗口。

38. 下载完成后，右键点击 tar.gz 文件，点击“打开文件所在文件夹”，并验证文件已下载到“Downloads”（下载）目录。

39. 要打开终端窗口，右键点击桌面并点击“在终端中打开”。

40. 输入 `cd Downloads`，然后按回车。

41. 要将文件解压到 /mnt/sdb1/ 目录，输入以下行并按回车。如有必要，输入密码 Pa$$word 并按回车。

```
