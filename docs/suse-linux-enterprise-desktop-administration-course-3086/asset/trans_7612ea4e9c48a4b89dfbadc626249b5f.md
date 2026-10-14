

**GConf** 用于配置 GNOME 首选项的系统软件。
**gconf** GConf 守护进程。
**gconf-editor command** 用于调用图形化 GConf 编辑器的命令。
**gconftool-2 command** 用于调用基于终端的 GConf 编辑器的命令。
**GNOME Control Center** 一个图形化实用程序，可用于配置 GNOME 桌面环境的行为。
**GNOME Volume Manager** 一个软件系统，用于挂载并管理对可移动媒体设备（如 CD-ROM、DVD 和 USB 设备）的访问。
**gnome-volume-manager command** 用于调用 GNOME Volume Manager 的命令。
**gnome-Xgl-settings command** 用于在 GNOME 桌面环境中启动桌面特效工具的命令。
**Keys** 包含 GConf 使用的值的配置参数。
**kwin** KDE 桌面环境中的默认窗口管理器。
**lsmod command** 列出当前已加载内核模块的命令。
**Metacity** GNOME 桌面环境中的默认窗口管理器。
**OpenGL** 用于定义 2D 和 3D 图形图像的工业标准应用程序编程接口。
**OpenOffice.org** 目前在 Linux 系统上常用的功能齐全的办公生产力套件。
**sabayon** 桌面配置文件编辑器的软件包名称。
**sax2 command** 用于在 SUSE Linux 系统上启动 X 配置实用程序的命令。
**template** 用于在程序中创建新文档的示例结构，例如 OpenOffice.org。
**udev** 用于创建和管理系统设备设备文件的 Linux 软件系统。
**window manager** 控制 X 中应用程序和对话框窗口外观的软件组件。
**X** 用于在 Linux 系统上绘制图形图像的系统。
**Xgl** 一种基于 OpenGL 的软件架构，可与 X 一起使用。
**xnest** 一个 X 服务器，其输出显示在现有 X 会话中的一个窗口内。

## Review Questions

+   1. 如果你在 GNOME 桌面环境中激活 Compiz 窗口管理器，它将替换哪个窗口管理器？
+      a. kwin
+      b. kde
+      c. Metacity
+      d. Enlightenment
+   2. 如果你当前没有运行 X 服务器，可以使用什么命令从命令行配置 X 设置，例如显卡和显示器类型？ ________

3. 可以使用什么键组合展开 Compiz 立方体？
a. Ctrl+Alt+Left
b. Ctrl+Alt+Shift+Left
c. Pause
d. Ctrl+Alt+Down

4. 你已使用 GConf 编辑器修改了 Nautilus 的 GNOME 桌面设置。你知道这些设置存储在 %gconf.xml 文件中。应检查哪个目录以找到包含你的 Nautilus 设置的文件？
a. /opt/gnome/nautilus
b. ~/.gconf/apps/nautilus
c. ~/.gconf/nautilus
d. /opt/gconf/nautilus

5. 可以使用哪些命令编辑 GConf 配置文件？（多选。）
a. gconf-editor
b. gconf-config
c. gconftool-2
d. vim

6. 你正尝试使用 gconftool-2 更改系统范围的 GNOME 默认值，但无法做到。你必须做什么？ __________

7. GConf 可用于锁定 GNOME 桌面，使用户无法修改某些桌面设置。你可以配置什么来锁定桌面设置？（多选。）
a. 在 GConf 编辑器中设置强制性首选项值。
b. 创建用户配置文件。
c. 在桌面配置文件编辑器中选择 编辑 > 锁定。
d. 在 GConf 编辑器中选择 桌面 > GNOME > 锁定。

8. 你已使用桌面配置文件编辑器为特定用户创建了配置文件，并希望验证其在文件系统上的位置。哪个文件包含用户的桌面配置文件？ __________

9. 你已为 Firefox 创建了一个自定义配置文件，希望将其提供给系统上将要创建的新用户。你应该怎么做？ __________

10. 以下哪种限制用户访问可移动媒体的方法最有效？
a. 使用 GConf 防止自动挂载程序挂载可移动媒体
b. 在 /etc/fstab 文件中添加“noauto”

+   c. 防止在系统初始化时加载 usb_storage 内核模块
+    d. 物理移除或限制对 CD-ROM 驱动器、DVD-ROM 驱动器和 USB 端口的访问

## Discovery Exercises

![](img/9129877170834ca9d5fdac5319bf5f12_597_0.png)

### Creating a Lockdown Security Profile

安全规划在规划组织内锁定计算机时至关重要。有效的安全规划可确保有缺陷设计中的安全漏洞在实施前被检测出来。

你即将实施多个供个人浏览公司目录的公共访问亭。该目录在互联网上提供，并将通过亭中的 Firefox 访问。亭用户应仅限于使用 Firefox 应用程序，并且不应访问桌面或可移动媒体的其他区域。此外，他们不应能够自定义 Firefox 或更改其默认主页。管理员用户账户应具有完全访问系统的权限以执行系统维护。

编写一份简短的摘要，说明执行此锁定所需的步骤。包括所涉及的技术和工具名称以及如何使用它们来锁定亭。如果有多种方法可用于锁定特定区域，请提供所选方法的理由。

### Locking Down Computers

假设你的 PC 是一个公共访问亭，并使用你在前一个发现练习中创建的摘要配置 GConf 以锁定它。测试你的结果以确保锁定有效。

### Researching Lockdown Utilities

锁定 Linux 计算机已成为十多年的标准做法。因此，除了 GConf 之外，还有许多软件包可用于限制对各种 Linux 组件的访问或锁定整个 Linux 桌面。使用互联网研究三个锁定软件包。对于每个软件包，描述其功能和基本配置。接下来，将每个锁定软件包与 GConf 进行比较。总结你的发现在一份简短备忘录中。

## Deploy SUSE Linux Enterprise Desktop 10

本节解释如何部署 SUSE Linux Enterprise Desktop 10。你选择的部署方法在很大程度上取决于你想要部署的工作站数量。安装数百台机器需要不同于安装几台机器的方法。

## Objectives

+   - Objective 1—Installation Options and Deployment Strategies
+   - Objective 2—Autoinstallation Basics
+   - Objective 3—The Configuration File for AutoYaST
+   - Objective 4—Installation Server: Setup and Use
+   - Objective 5—Automated Installation

## Objective 1—Installation Options and Deployment Strategies

如果你安装一台机器，使用安装 DVD 进行手动安装是最好的选择。但是，当你计划安装的机器数量增加时，需要替代方案。

你可以使用 *SUSE Linux Enterprise Desktop 10* DVD、启动磁盘或 PXE 兼容网络卡启动安装。安装源可以是 DVD 或网络中的安装服务器。访问安装服务器上存储库所支持的协议为 NFS、HTTP、FTP 和 SMB/CIFS。

为了找到网络的最佳解决方案，你需要了解以下内容：

+   - Installation Options
+   - Deployment Strategies

### Installation Options

在决定如何安装 *SUSE Linux Enterprise Desktop 10* 之前，你需要考虑以下内容：

+   - Boot Media
+   - Installation Source
+   - Configuration

### Boot Media

要安装机器，你必须选择一个启动介质来启动机器：

+   - *Installation DVD*—安装 DVD 可启动，可用于启动安装或启动救援系统。如果默认参数有问题，可以设置不同的内核参数。例如，可以禁用 ACPI 或本地 APIC，或使用安全设置。
+   - *Floppy disk*—要创建可启动软盘，请启动 YaST 并选择 系统 > 启动或救援软盘。
+   - *PXE-capable network card*—如果机器配备了 PXE 兼容网络卡，它可以从网络中的 TFTP 服务器加载启动映像。如果网络卡还支持 Wake on LAN，则可以实现完全远程安装。

### Installation Source

你可以使用不同的安装源：

+   - Installation DVD
     安装 DVD 包含安装 *SUSE Linux Enterprise Desktop 10* 所需的所有文件。
+   - Installation Server
     所需的安装文件可以存储在网络中的服务器上。可用的协议为 HTTP、FTP、NFS 或 SMB/CIFS。SLP 可用于在网络中广告安装服务器。

