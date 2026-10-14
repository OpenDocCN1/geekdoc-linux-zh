
4. 选择 应用。
5. 选择 接受。
6. 关闭 YaST 控制中心。

## 第 IV 部分：启动 YaST 的 ncurses 接口

要启动 YaST 的 ncurses 接口，请执行以下操作：

1. 通过按 切换到第一个虚拟终端
   `Ctrl+Alt+F1`
2. 使用密码 `n0v3ll` 以 `root` 身份登录。
3. 通过输入 查看可用 YaST 模块列表
   `yast -l`
4. 要启动 YaST 的 ncurses 接口，输入
   `yast`

## 第 V 部分：查看系统文件的内容

要查看系统文件的内容，请执行以下操作：

1. 按向下箭头直到左侧框架中突出显示“杂项”；然后按 Enter。
2. 按向下箭头直到右侧框架中突出显示“查看系统日志”；然后按 Enter。
3. 按向下箭头直到选择 /proc/version；然后按 Enter。
4. 按两次 Tab 键突出显示“确定”；然后按 Enter。
5. 要退出 YaST，按 Alt+Q 选择“退出”。
6. 通过输入 `exit` 注销。
7. 通过按 切回图形界面
   `Ctrl+Alt+F7`

## 目标 3—了解 SuSEconfig 的作用

你可以将 YaST 视为各种其他程序的前端，例如 RPM（RPM Package Manager）软件管理、用户管理，或不同服务（例如邮件或 Web 服务器）的各种配置文件。

大多数情况下，YaST 会直接将配置更改写入最终配置文件。在其他情况下，您输入的信息首先写入 /etc/sysconfig/ 目录中的文件，然后再写入最终配置文件。

这个中间步骤就是 SuSEConfig 程序变得重要的地方。

SuSEConfig 是 SUSE Linux Enterprise Desktop 中使用的工具，用于根据 /etc/sysconfig/ 及其子目录中各种文件中设置的变量来配置系统。

这些文件包含诸如 `CUPSD_OPTIONS=""` 在 `/etc/sysconfig/cups` 中和 `SMTPD_LISTEN_REMOTE="no"` 在 `/etc/sysconfig/mail` 中的变量。

其中一些变量被直接使用（例如在某些启动脚本中）。例如，如果 `CUPSD_OPTIONS` 设置为“-c /path/cupsd.conf”，负责打印的 cups 守护进程将使用 `/path/cupsd.conf` 配置文件启动。

其他变量用于修改其他文件。例如，如果 `SMTPD_LISTEN_REMOTE` 设置为“yes”，脚本 `/sbin/SuSEConfig` 和 `/sbin/conf.d/` 中的脚本会将 `/etc/postfix/main.cf` 中的变量 `INET_INTERFACES` 设置为“all”。

SuSEConfig 充当 YaST 的后端，并在使用 YaST 模块时激活您所做的配置更改。

如果您使用编辑器修改 /etc/sysconfig/ 中的文件，您可能只需要重新启动服务即可使更改生效。但是，您可能还需要运行 SuSEConfig。

因此，我们建议在手动编辑 /etc/sysconfig/ 中的文件后运行 SuSEConfig。

SuSEConfig 使用 /sbin/conf.d/ 中的子系统特定脚本来配置各个子系统。例如，/etc/sysconfig/postfix 中的变量由脚本 /sbin/conf.d/SuSEconfig.postfix 评估。

![](img/9129877170834ca9d5fdac5319bf5f12_116_0.png)

## 摘要

- SLES 中的主要系统配置实用程序是 YaST。您可以在命令行终端中使用基于 ncurses 菜单的 YaST 接口，或在桌面环境中使用 Qt 图形 YaST 接口。
- 通过导航到 YaST 中的硬件信息模块，您可以查看有关计算机硬件的信息，这对于排除硬件设备故障很有用。
- YaST 还包含可用于配置 SUSE Linux 系统的时间、日期、语言和键盘设置的模块。
- YaST 通常将信息保存到 `/etc/sysconfig` 目录并使用 SuSEConfig 在系统上配置信息。因此，在修改 `/etc/sysconfig` 目录中的文件后，您应该运行 SuSEConfig。

## 关键术语

- **/etc/sysconfig** — 存储 YaST 存储的配置信息的目录。
- **/sbin/conf.d** — 存储 SuSEConfig 使用的脚本的目录。
- **date command** — 用于在 Linux 系统上设置系统时间的命令。
- **hwclock command** — 用于修改系统 BIOS 时间的命令。
- **ncurses** — Linux 中的基于文本的菜单界面。
- **Qt** — 用于在 Linux 系统上创建图形应用程序的工具包。YaST 包含图形 Qt 模式。
- **su command** — 用于在登录到 Linux 终端时切换用户帐户的命令。

**SuSEConfig**  一个使用 `/etc/sysconfig` 目录中条目配置系统的软件实用程序。

**YaST**  SUSE Linux 中的主要配置工具。它代表 Yet another Setup Tool，可以在图形或文本（ncurses）模式下运行。

**yast command**  用于启动 YaST 的 ncurses 接口的命令。

**yast2 command**  用于启动 YaST 的 Qt 和 ncurses 接口的命令。

**YaST Control Panel**  YaST 中列出可用 YaST 模块的主对话框屏幕。

### 复习问题

1. 在桌面环境中的命令行提示符下，您会键入什么命令来启动基于文本的 YaST 接口？ ____________

2. 更改 `/etc/sysconfig` 目录中的内容后应运行什么实用程序？
   a. YaST
   b. SuSEConfig
   c. uname
   d. KDE System Guard

3. 您可以使用什么命令快速查看 YaST 模块列表？

4. 以下哪些可用于直接启动 YaST 模块？（选择所有适用项。）
   a. `yast modulename`
   b. `yast~i modulename`
   c. `yast2~i modulename`
   d. `yast2 modulename`

5. SuSEConfig 实用程序在进行系统配置更改时处理哪个目录？ ____________

### 发现练习

![](img/9129877170834ca9d5fdac5319bf5f12_117_0.png)

### 查看您的系统硬件配置文件

了解您的系统硬件对于做出有关系统使用的未来决策非常重要。随着时间的推移，您可能会选择向特定 Linux 服务器添加服务，该服务器具有足够的硬件来充分支持软件。或者，您可能会选择在添加服务之前升级 Linux 服务器的硬件。

使用 YaST 的硬件信息模块查看您的系统硬件配置文件。保存或打印结果以供以后使用。

## YaST 模块

为了有效地管理 Linux 系统，您应该熟悉 YaST 中用于系统配置的各种模块。使用 yast --list 命令查看系统上可用的 YaST 模块。直接使用 yast 命令启动每个模块并注意其用途。

## 了解 SuSEconfig

SuSEconfig 实用程序通过配置 YaST 在 /etc/sysconfig 中保存的信息为 YaST 提供后端。检查 /etc/sysconfig 目录的内容并查看其中的一些文件。使用 Internet 和本地文档，检查 SuSEconfig 实用程序的目的。最后，在您的系统上运行 SuSEconfig。

![](img/9129877170834ca9d5fdac5319bf5f12_118_0.png)

![](img/9129877170834ca9d5fdac5319bf5f12_120_0.png)

## 第 5 节

## 管理网络配置

在本节中，您将了解 YaST 网络卡模块以及其他网络相关主题。这些包括用于测试网络的命令行工具、SUSE 防火墙和远程访问。

## 目标

- 目标 1—从 YaST 管理网络配置信息
- 目标 2—使用命令行工具测试网络连接
- 目标 3—使用 SuSEfirewall2
- 目标 4—使用 NetworkManager 配置网络
- 目标 5—提供远程访问

## 目标 1—从 YaST 管理网络配置信息

用于配置网络卡和网络连接的 YaST 模块可以从 YaST 控制中心访问。参见图 5-1。

要激活网络配置模块，请选择 **网络设备 > 网络卡**。

![](img/9129877170834ca9d5fdac5319bf5f12_121_0.png)

**图 5-1**

YaST 首先想知道网络设置方法：

- *由 NetworkManager 控制的用户*—普通用户可以使用桌面小程序管理所有网络接口的连接。这在笔记本电脑在有线和无线连接之间切换时特别有用。
- *使用 ifup 的传统方法*—传统方法使用 `ifup` 命令。您会在服务器上或在不太可能更改网络连接的桌面上使用此方法。

