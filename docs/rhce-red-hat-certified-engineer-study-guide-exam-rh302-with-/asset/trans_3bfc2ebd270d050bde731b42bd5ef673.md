

## 使用 linuxconf 215

你可以点击“Add”（添加）添加一个新的 Linux 启动镜像。要编辑或删除现有的 Linux 启动镜像，请选择该镜像并按回车。将出现启动配置界面。要删除启动镜像，点击“Delete”（删除）按钮。要编辑启动镜像，进行所需的更改并点击“Accept”（接受）。该界面提供了上一节描述的 LILO 启动镜像选项以及一些不常用的选项。

## 配置非 Linux 启动菜单

要添加、更改或删除非 Linux 分区，请从 linuxconf 树中选择 Config（配置） ➤ Boot Mode（启动模式） ➤ LILO ➤ Configure LILO Other OS Configurations（配置 LILO 其他操作系统配置）。将出现 LILO 其他操作系统配置界面；图 9.10 显示该界面的图形化版本。

图 9.10 LILO 其他操作系统配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_236_0.png)

你可以点击“Add”添加一个新的非 Linux 启动镜像。要编辑或删除现有的非 Linux 启动镜像，请选择该镜像并按回车。将出现操作系统设置界面。要删除启动镜像，点击“Delete”按钮。要编辑启动镜像，进行所需的更改并点击“Accept”。其他操作系统设置界面提供了上一节描述的 label1 和其他选项。标记为“Partition to Boot”（启动分区）的文本对应于其他选项。

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com

## 配置默认启动镜像

要指定默认启动镜像，请从 linuxconf 菜单中选择 Config（配置）▷ Boot Mode（启动模式）▷ LILO ▷ Change Default Boot Configuration（更改默认启动配置）。将出现默认启动配置界面；图 9.11 显示该界面的图形化版本。

图 9.11 默认启动配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_237_0.png)

要指定不同的默认启动镜像，点击对应所需镜像的单选按钮，然后点击“Accept”。

## 配置启动选项

你可以使用 linuxconf 配置启动选项。要这样做，请从 linuxconf 菜单中选择 Config（配置）▷ Boot Mode（启动模式）▷ Mode（模式）▷ Default Boot Mode（默认启动模式）。将出现启动模式配置界面；图 9.12 显示该界面的图形化版本。

## 图 9.12 启动模式配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_238_0.png)

你可以使用此界面启用或禁用 LILO 的启动菜单，并指定启动延迟和提示超时。后两个选项在 LILO Defaults（默认）界面也可用。你还可以使用启动模式配置界面指定系统是以文本模式（runlevel 3）还是图形模式（runlevel 5）启动。

## 配置网络

你可以使用 `linuxconf` 配置基本和高级网络选项。本节解释了如何配置基本选项；后续章节——特别是第 15 章——解释了如何配置高级选项。

## 配置主机名

要配置主机名，请从 `linuxconf` 菜单中选择 Config（配置） ➤ Networking（网络） ➤ Client Tasks（客户端任务） ➤ Basic Host Information（基本主机信息）。将出现主机基本配置界面；图 9.13 显示该界面的图形化版本。

## 图 9.13 主机基本配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_239_0.png)

图形化的主机基本配置界面包含多个标签页，允许你从各种窗口之间进行选择。如果图形界面中没有显示 Host Name（主机名）界面，请点击 Host Name 标签。要指定主机名，将其输入文本框中并点击“Accept”。

## 配置网络适配器

要配置网络适配器，请从 linuxconf 菜单中选择 Config（配置） > Networking（网络） > Client Tasks（客户端任务） > Basic Host Information（基本主机信息）。将出现主机基本配置界面。图形界面包含多个标签页，允许你在各种窗口之间进行选择。如果图形界面中没有显示 Adapter 1（适配器 1）界面，请点击 Adapter（适配器）标签。将出现 Adapter 1 界面；图 9.14 显示该界面的图形化版本。

如果你使用的是文本版本的 linuxconf，只需滚动查看主机基本配置界面中与 Adapter 1 关部分。linuxconf 程序提供了多达 5 个网络适配器的配置选项访问。

## 图 9.14 适配器界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_240_0.png)

使用 Adapter I 界面或其他适配器界面，你可以启用或禁用适配器，并指定其配置是静态的还是通过 DHCP 或 OTP 获取。如果配置是静态的，你可以使用标记为“Primary Name + Domain”（主名 + 域）的文本框指定完全限定域名 (FQDN)。你还可以指定 IP 地址、子掩码和其他选项，包括设备选项。点击“Accept”保存你的更改。

## 配置域名服务器

要配置域名服务器，请从 linuxconf 菜单选择 Config（配置） > Networking（网络） > Clients（客户端） > Name Server Specification（域名服务器规范）。将出现 Resolution（解析）界面；图 9.15 显示该界面的图形化版本。

## 图 9.15 解析器配置界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_241_0.png)

Copyright©2000 SYBEX, Inc., Alameda, CA www.sysex.com

如果正常运行不需要 DNS，请禁用“DNS Is Required for normal operation”（正常运行需要 DNS）。否则，指定最多两个搜索域。点击“Accept”保存你的更改。

## 配置默认网关

要配置默认网关，请从 linuxconf 菜单树选择 Config（配置） > Networking（网络） > Client Tasks（客户端任务） > Routing（路由） > Set Defaults（设置默认）。将出现 Defaults（默认）界面；图 9.16 显示该界面的图形化版本。

图 9.16 默认界面

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_242_0.png)

指定默认网关的 IP 地址。如果你让此系统充路由器，请开启 Routing。有关配置路由的更多信息，请参阅第 29 章，“配置路由器”。

## 激活更改

如前所述，当使用 linuxconf 更改选项时，该更改可能会立即发生，也可能保持挂起状态直到更改被激活。虽然配置文件会立即更新，但大多数服务在重启之前不会检测到更改。当你指示 linuxconf 激活挂起的更改时，会重启已更改配置的服务。

如果你想知道有哪些挂起的更改，点击“Preview What Has Done”（预览已完成）。linuxconf 将显示挂起的更改。要激活更改，点击“Activate”。要在不激活任何挂起的更改的情况下退出状态界面，点击“Quit”。

你应该在退出 linuxconf 之前激活挂起的更改。如果你忽略了这一点，linuxconf 将提示你确认要在不激活更改的情况下退出。

## 总结

在本章中，你学习了如何配置安装时的选项。涵盖了最重要的主题：

- **键盘**：安装完成后，你可以使用 kbdconfig 程序配置键盘。
- **鼠标**：安装完成后，你可以使用 mouseconf 程序配置鼠标。
- **时区**：安装完成后，你可以使用 timeconf 程序配置时区。
- **音频**：安装完成后，你可以使用 sndconfig 程序配置音频。
- **默认运行级别**：安装完成后，你可以使用 linuxconf 程序配置默认运行级别。
- **身份验证**：安装完成后，你可以使用 `pwconv` 或 `punconv` 程序配置影子密码，或使用 `linuxconf` 程序更改 `root` 密码。
- **LILO 选项**：安装完成后，你可以使用 `linuxconf` 程序配置 LILO 选项。
- **网络**：安装完成后，你可以使用 `linuxconf` 程序配置网络。

## 关键术语

在进入下一章之前，请确保熟悉以下术语：

Runlevel（运行级别）

## 更多信息来源

如果你想进一步了解本章介绍的主题，你应该查阅以下资源：

字体 官方 Red Hat Linux 参考指南
- 本章描述的程序和工具的手页 (man pages)

