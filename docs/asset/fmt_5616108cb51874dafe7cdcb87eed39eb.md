
“`DNS`”选项卡负责决定网络中有多少客户端可以访问服务器。图 2-39 显示了 DNS 窗口。

![](img/aa463306f14dbdf30c3b9314551ee469_54_1.png)

此窗口显示主机名、主 DNS 和备用 DNS 等文本字段。主 DNS 显示您网络中服务器的 IP 地址。“Hosts”选项卡用于指定静态主机名到 IP 地址的映射。图 2-40 显示了网络配置窗口的 hosts 选项卡：

![](img/aa463306f14dbdf30c3b9314551ee469_55_0.png)

此窗口显示 hosts 的默认条目 `127.0.0.1`，它始终用于计算机本身。

## 使用红帽 GUI 包管理工具

如果您在 Linux 安装过程中没有安装所有软件包，可以使用红帽 GUI 包管理工具来安装软件包。红帽 GUI 包管理工具是一个图形化工具，帮助从 Linux 计算机上安装和删除软件包。它可以从本地安装和删除软件包。此外，您还可以使用红帽 GUI 工具远程安装或删除软件包。

### 安装 Linux

如果您想在您的计算机上安装或删除软件包，请执行以下步骤：

- 1. 选择主菜单 -> 系统设置 -> 网络来打开网络配置窗口，如下图：

![](img/aa463306f14dbdf30c3b9314551ee469_56_0.png)

- 2. 滚动滚动条找到“设备”部分，如下图：

图 2-42 设备部分

![](img/aa463306f14dbdf30c3b9314551ee469_56_1.png) (注：根据上下文修复，此处应为设备列表)

- 3. 点击右侧的“详情”链接打开“详情”窗口，如下图：

![](img/aa463306f14dbdf30c3b9314551ee469_57_0.png)

- 4. 取消勾选相关项并点击“关闭”按钮返回包管理窗口，如下图：

![](img/aa463306f14dbdf30c3b9314551ee469_57_1.png)

- 5. 如果您要在计算机上安装软件包，需要勾选相应的框。点击“更新”按钮显示“系统准备就绪”对话框：

![](img/aa463306f14dbdf30c3b9314551ee469_58_0.png)

- 6. 点击“继续”按钮显示“更新完成”对话框，如下图：

![](img/aa463306f14dbdf30c3b9314551ee469_58_1.png)

- 7. 点击“确定”按钮返回包管理窗口：

图 2-47 包管理窗口 (注：此处逻辑修复)

- 8. 点击“退出”按钮关闭包管理窗口并完成删除所需软件包的过程。

![](img/aa463306f14dbdf30c3b9314551ee469_61_0.png)

为了设置 Kickstart 配置窗口的选项，Prabhakar 需要执行以下任务：

- 设置基本配置选项
- 设置安装方法选项
- 设置引导程序（boot loader）选项
- 设置分区信息
- 设置网络配置选项
- 设置身份验证选项
- 设置防火墙配置选项
- 设置 X 窗口配置选项
- 设置软件包选择选项

## 设置基本配置选项

要设置基本配置（Basic Configuration）选项，请在基本配置屏幕上执行以下步骤：

- 在“Root Password”（根密码）和“Confirm Password”（确认密码）文本框中输入根密码，以设置根密码。例如，您输入 `redhatsys` 作为根密码。该密码用于以 root 用户身份登录系统。

b. 勾选 `Encrypt root password`（加密根密码）复框以加密根密码。

c. 从 Language Support（语言支持）列表框中选择 `English`（英语），以指定英语作为使用 Kickstart 配置工具的语言。

d. 确保勾选 `Reboot system after installation`（安装后重启系统）复框。选择此选项有助于在 kickstart 安装完成后自动重启电脑。

c. 如果你想以文本模式执行 kickstart 安装，请勾选 `Perform installation in text mode (graphical is default)`（以文本模式执行安装（默为图形模式））复框。默认情况下，安装将在图形模式下进行。

f. 如果你想以交互模式执行 kickstart 安装，请勾选 `Perform installation in interactive mode`（以交互模式执行安装）复框。在交互模式下，kickstart 安装程序会要求您确认创建 kickstart 文件时指定的设置。

下面的图显示了执行上述任务后更新的基本配置屏幕：

![](img/aa463306f14dbdf30c3b9314551ee469_62_0.png)

## 设置安装方法选项

要设置安装方法（Installation Method）选项，请从 Kickstart 配置窗口左侧窗格列表中选择 `Installation Method` 选项。选择 Installation Method 选项后会出现安装方法屏幕。请在安装方法屏幕上执行以下步骤：

a. 选择 `Perform new installation`（执行新安装）单选按钮以执行新的 安装。如果你想升级已有的 Linux 系统，可以选择 `Upgrade an existing installation`（升级现有安装）单选按钮。

b. 从 Choose Installation Method（选择安装方法）类别中选择 `NFS` 单选按钮，以使用 NFS 进行安装。你也可以选择使用 `CD-ROM`、`FTP`、`HTTP` 或硬盘进行安装。

c. 分别在 `NFS Server`（NFS 服务器）和 `NFS Directory`（NFS 目录）文本框中选择 NFS 服务器地址和 NFS 目录名称。

接的图显示了执行上述任务后更新的安装方法屏幕：

![](img/aa463306f14dbdf30c3b9314551ee469_63_0.png)

## 设置引导程序选项

要设置引导程序（Boot Loader）选项，请从 Kickstart 配置窗口左侧窗格列表中选择 `Boot Loader Options` 选项。选择 Boot Loader Options 选项后会出现引导程序选项屏幕。请在引导程序选项屏幕上执行以下步骤：

a. 选择 `Install new boot loader`（安装新引导程序）单选按钮以安装新的引导程序。

b. 选择 `Use GRUB`（使用 GRUB）单选按钮将 GRUB 作为引导程序。

c. 勾选 `Use GRUB password` 复框以设置 GRUB 密码。

d. 在 `Password`（密码）和 `Confirm Password`（确认密码）文本框中输入密码以指定 GRUB 密码。

e. 勾选 `Encrypt GRUB password`（加密 GRUB 密码）复框以加密 GRUB 密码。

f. 选择 `Install boot loader on Master Boot Record (MBR)`（在主引导记录上安装引导程序）单选按钮以在 MBR 上安装引导程序。如果 MBR 已经包含了引导程序，你也可以选择 `Install boot loader on the first sector of the boot partition`（在引导分区第一个扇区安装引导程序）单选按钮。

g. 如果你想在系统启动时向内核传递某些内核参数，请输入内核参数名称。例如，如果有一个 IDE CD-ROM，你可以通过输入 `hdd=ide-scsi` 作为内核参数，指定内核在使用 `cdd record` 之前必须加载 SCSI 仿真驱动程序（其中 `hdd` 是 CD-ROM 设备）。

接的图显示了更新的引导程序选项屏幕：

### 图 2-51 引导程序选项屏幕

![](img/aa463306f14dbdf30c3b9314551ee469_64_0.png)

## 设置分区信息

要设置分区信息（Partition Information），请从 Kickstart 配置窗口左侧窗格列表中选择 Partition Information 选项。选择 Partition Information 选项后会出现分区信息屏幕。请在分区信息屏幕上执行以下步骤：

- 选择 `Clear Master Boot Record`（清除主引导记录）单选按钮在创建分区之前清除 MBR 上的信息。
- 选择 `Remove all existing partitions`（移除所有现有分区）单选按钮移除所有现有分区。
- 点击 `Initialize the disk`（初始化磁盘）按钮在安装时初始化磁盘标签。下面的图显示了更新的分区信息屏幕：

图 2-52 分区信息屏幕

![](img/aa463306f14dbdf30c3b9314551ee469_65_0.png)

点击 `Add` 按钮显示分区对话框。在分区对话框中执行以下操作：
