

## 13 使用 CUPS 进行打印

### 本章内容

- 系统自动配置本地打印机 558
- 快速入门 I：使用 system-config-printer 配置打印机 558
- 快速入门 II：设置本地或远程打印机 560
- 使用 CUPS Web 界面 565
- CUPS Web 界面 567
- 命令行中的 CUPS 568
- 传统 UNIX 打印 573
- 从 Windows 打印 574
- 打印到 Windows 576

### 学习目标

阅读完本章后，您应该能够：

- 解释打印子系统的用途
- 描述 CUPS 的功能
- 定义 IPP 并解释其在 CUPS 中的作用
- 使用 system-config-printer 安装和管理本地及远程打印机
- 使用 CUPS Web 界面安装和管理本地及远程打印机
- 共享本地打印机
- 从 Windows 系统打印到 Linux 打印机
- 从 Linux 系统打印到 Windows 打印机
- 使用命令行工具提交、列出和取消打印任务
- 使用配额限制打印

打印系统负责处理从应用程序（或命令行）获取打印任务，通过适当的*过滤器*（第 1250 页）并进入适合打印机的队列，然后使其打印出来的任务。当打印机发生故障时，打印系统可以将任务重定向到其他类似的打印机。

## 简介

**LPD 和 LPR** 最初，UNIX 有两种打印系统：BSD LPD（行式打印机守护进程）和 System V LPR（行式打印机系统）。Linux 最初采用了这些系统，而 UNIX 和 Linux 都经历了这些系统的修改和替代。如今，CUPS 是 Linux 下的默认打印系统。

**CUPS** CUPS（通用 UNIX 打印系统）是一个跨平台的打印服务器，基于 IPP（下一节介绍）构建。CUPS 提供了许多打印机驱动，可以打印不同类型的文件，包括 PostScript。由于它是基于 IPP 构建并旨在保持可移植性，CUPS 可在许多操作系统下运行，包括 Linux 和 Windows。其他 UNIX 变体，包括 Mac OS X，也使用 CUPS。Windows 的近期版本包括打印到 IPP 打印机的功能。因此，CUPS 是异构环境中打印的理想解决方案。CUPS 提供 System V 和 BSD 命令行接口，除了 IPP 外，还支持 LPD/LPR、HTTP、SMB 和 JetDirect（套接字）协议等。

如果您正在配置的打印机位于未运行 CUPS 的较旧 Linux 系统或类 UNIX 操作系统上，该系统很可能运行 LPD/LPR。大多数将打印机直接连接到网络的设备都支持 LPR/LPD；有些支持 IPP。

**IPP** IPP 项目（Internet Printing Protocol；www.pwg.org/ipp）始于 1996 年，当时 Novell 和其他几家公司设计了一种通过 Internet 打印的协议。IPP 允许用户：

- 确定打印机的功能。
- 向打印机提交任务。
- 确定打印机的状态。
- 确定打印任务的状态。
- 取消打印任务。

IPP 是一种基于 HTTP 的客户端/服务器协议，其中服务器端可以是打印服务器或具备网络功能的独立打印机。

**网络打印机** 直接连接到网络的打印机在功能上等同于连接到运行打印服务器系统的打印机：它们监听与运行打印服务器系统相同的端口，并对任务进行排队。

**打印机和队列** 在计算系统上，当您“将任务发送到打印机”时，您实际上是将该任务添加到等待在某台打印机上打印的任务列表中。这个列表称为*打印队列*或简称为*队列*。短语*配置（或设置）打印机*通常用于指*配置（打印）队列*。本章互换使用这些短语。

**配置工具** 本章探讨了两种可用于配置打印队列的工具：**system-config-printer**（第 558 页）和 CUPS Web 界面（第 565 页），重点介绍前者。

使用 CUPS Web 界面与使用 **system-config-printer** 非常相似；因此，关于 **system-config-printer** 的许多讨论也适用于 CUPS Web 界面。然而，**system-config-printer** 是一个用 Python 编写的本地应用程序，而不是 Web 界面。

## 先决条件

请确保已安装以下软件包（大多数软件包随基础 Fedora/RHEL 系统安装）：

- **cups**
- **system-config-printer**（可选）
- **cups-pdf**（可选；设置虚拟 PDF 打印机）

CUPS Web 界面需要 X 服务器和 Web 浏览器。虽然这是一个较差的解决方案，但文本 Web 浏览器，如 **elinks**（**elinks** 软件包），也可以使用。

**启用并启动 cups** 运行 **systemctl** 使 **cups** 服务（**cupsd** 守护进程）在每次系统进入多用户模式时启动，然后启动 **cups** 服务。使用 **systemctl status** 命令确保服务正在运行。

```bash
# systemctl enable cups.service
# systemctl start cups.service
```

修改 **cups** 配置文件后，再次执行第二个命令，将 **start** 替换为 **restart**，以使 **cups** 重新读取这些文件。

## 更多信息

**本地** CUPS 文档：当 CUPS Web 界面启动时（第 **567** 页），将本地浏览器指向 localhost:631/help

**网络** 关于 Linux 下打印机和打印的信息，包括论坛和文章：www.linuxfoundation.org/collaborate/workgroups/openprinting

包含许多打印机详细信息的支持数据库，包括备注和驱动程序信息：www.openprinting.org/printers

CUPS 主页：www.cups.org

IPP 信息：www.pwg.org/ipp

**HOWTO** SMB *HOWTO* 中有一个标题为“与 Linux 机器共享 Windows 打印机”的章节。

## 注意事项

**SELinux** 当 SELinux 设置为使用针对策略时，CUPS 受到 SELinux 保护。如有必要，您可以禁用此保护。更多信息请参阅第 **475** 页的“使用 **system-config-selinux** 设置针对策略”。

**防火墙** CUPS 服务器通常使用 TCP 端口 631 和 UDP 端口 631 进行 IPP 连接，并使用 TCP 端口 80 进行 LPR/LPD 连接。如果服务器接受远程系统的打印任务，并且正在运行防火墙或位于防火墙之后，您需要打开其中一个或两个端口。提供以下命令以在每次系统启动时（永久地）和运行中的系统上打开端口；有关 firewall-cmd 的信息，请参阅第 906 页。

![](img/243613168ac865b539f12460d966088e_614_0.png)

**图 13-1** 打印设置窗口

```bash
# firewall-cmd --add-port=631/tcp
# firewall-cmd --permanent --add-port=631/tcp
# firewall-cmd --add-port=631/udp
# firewall-cmd --permanent --add-port=631/udp
# firewall-cmd --add-port=80/tcp
# firewall-cmd --permanent --add-port=80/tcp
```

PDF 打印机 您可以通过安装 cups-pdf 软件包来设置虚拟 PDF 打印机，也可以手动设置此打印机。

## 系统自动配置本地打印机

在大多数情况下，当您连接打印机到本地系统并打开它时，系统会显示一条消息，此时它正在安装驱动程序。当驱动程序安装完成后，打印机即可使用。两个图形工具允许您添加和修改打印机，以及处理打印任务。您可以从设置窗口（第 107 页）中的打印机选项处理大多数与打印机相关的工作，并使用 system-config-printer（下一节）处理更复杂的打印机相关任务。使用其中一个工具来验证打印机是否已安装，向打印机发送测试页，并更改打印机的配置。

## 快速入门 I：使用 system-config-printer 配置打印机

打印设置窗口（图 13-1）允许您添加、移除和配置本地及远程打印机。通过从“输入命令”窗口（ALT-F2）或终端模拟器输入命令 system-config-printer 来打开此窗口。本快速入门

![](img/243613168ac865b539f12460d966088e_615_0.png)

解释了如何修改现有打印机的配置。有关设置新打印机的说明，请参阅第 560 页。

**默认打印机** 在打印设置窗口中高亮显示一个打印机，并从窗口菜单中选择 menubar: Printer->Set as Default，以指定高亮显示的打印机为默认打印机。如果打印设置窗口中仅显示一个打印机，则该打印机即为默认打印机；您无需将其设置为默认。图 13-1 中打印机上的对勾指示默认打印机。

**服务器设置** 从打印设置窗口中选择 menubar: Server->Settings，显示服务器设置窗口。此窗口顶部的两个复选框指定本地系统是否发布其共享的打印机（以便远程系统能够找到这些打印机）以及是否允许从 Internet 打印。如果您选择共享打印机，system-config-printer 会询问您是否希望调整防火墙以允许传入的 IPP 连接。当您单击“调整防火墙”时，system-config-printer 打开 TCP 端口 631 和 UDP 端口 631。您可以从打印机属性窗口的策略选择中控制是否共享特定打印机（下一节）。

### 配置选项卡

双击打印设置窗口中的打印机，或高亮显示一个打印机并选择 menubar: Printer->Properties，以显示该打印机的打印机属性窗口（图 13-2）。

本节描述在打印机属性窗口左侧框架中找到的六个选项卡。这些选项卡允许您配置在打印设置窗口中选择的打印机。

**设置** 图 13-2 显示了一台 Brother 打印机的设置选项卡。标记为“描述”和“位置”的文本框保存有助于用户识别打印机的信息。系统不使用此信息；您可以随意更改。例如，在标记为“位置”的文本框中填写打印机的物理位置（例如 Sam 的办公室）可能很有帮助。标记为“设备 URI”和“制造商和型号”的文本框指定打印机在计算机或网络上的位置以及打印机的类型。

