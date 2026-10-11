
在提示时，输入 `root` 用户名和密码。

现在，显示了管理界面，设置打印机的方法如下：

1. 点击添加打印机（Add Printer）按钮。出现“添加打印机”屏幕。
2. 为打印机输入名称（Name）、位置（Location）和描述（Description），并点击继续（Continue）。
3. 选择连接打印机的设备。打印机可以直接连接到计算机上的并行、SCSI 或 USB 口。或者，你可以为 Apple 打印机选择网络连接类型（appSocket/JetDirect）、互联网打印协议（http 或 ipp），或 Windows 打印机（使用 SAMBA 或 SMB）。
4. 更多信息，你可能需要描述到打印机的连接。例如，你可能需要为串口服务器输入波特率和校验位，或者你可能是 IPP 或 Samba 打印机的网络地址。
5. 选择打印机驱动程序的名称（如果你不知道列出的打印机制造商，为 PostScript 打印机选择 PostScript，或为 PCL 打印机选择 HP）。对于列出的制造商，你将可以选择特定的型号。
6. 如果打印机添加成功，下一页将显示指向该打印机描述的链接。点击该链接。在新的打印机页面上，你可以打印测试页或修改打印机配置。

当你能够从 CUPS 打印时，可以返回 CUPS 基于 Web的管理页面并处理你的打印机。以下是你可以执行的一些示例：

- 打印任务 — 点击“任务”（Jobs）查看当前为此服务器配置的任何打印机上正在运行的任务。点击“显示已完成的任务”（Show Completed Jobs）查看已打印任务的信息。
- 创建打印机类— 点击“类”（Classes）；然后点击“添加类”（Add Class）并为打印机指定名称和位置。点击“继续”（Continue）。然后，从服务器上配置的打印机列表中选择要放入此类的打印机。
- 查看打印机 — 你可以点击任何 CUPS 基于 Web 管理页面顶部的“打印机”（Printers）来查看你配置的打印机。对于出现的每个打印机，你可以点击“停止打印机”（Stop Printer，停止打印机打印但仍接受队列中的打印任务）、“拒绝任务”（Reject Jobs，暂时不接受任何后续任务）或“打印测试页”（Print Test Page，打印一页）。图 26-2 显示了打印机页面。

### 图 26-2

从“打印机”页面打印测试页或临时停止打印。

![](img/d7f79c91d15076e71790c1b4e1d072d0_732_0.png)

## 使用 Red Hat 打印机配置窗口

如果你使用的是 Fedora、RHEL 或其他 Red Hat 赞助的系统，你可以使用打印机配置窗口来设置打印机。事实上，我建议你使用它而不是 CUPS Web 管理，因为生成的打印机文件是为配合 Red Hat 系统定制的。

要在 Fedora 的 GNOME 桌面上安装打印机，请通过选择系统（System）-> 管理（Administration）->（对于 Fedora 8，选择系统->打印）或以 `root` 用户身份输入 `system-config-printer` 来打开打印机配置窗口。此工具允许你添加和删除打印机属性。它还允许向打印机发送测试页以确保它们正常工作。

这里的关键在于你正在配置由你的打印守护进程（CUPS 服务的 `cupsd`）管理的打印机。配置打印机后，你可以在本地系统可以使用它。你可以

## 运行打印服务器

参考“配置打印服务器”部分来了解如何让网络上其他计算机的用户可以使用服务器。

你设置的打印机可以连接到你的计算机（如并行端口）或连接到网络上的另一台计算机（例如，来自另一个 UNIX 系统或 Windows 系统）。

## 在 Fedora 中配置本地打印机

使用以下步骤通过打印机配置窗口添加本地打印机（换句话说，连接到你的计算机的打印机）。如果你没有打印机，请查看侧边栏“选择打印机”）。

> 提示：在启动此程序之前连接你的打印机。这将使打印机软件自动检测打印机的位置，并在添加它时立即测试打印机。

## 选择打印机

PostScript 语言一直是 Linux 和 UNIX 打印的优选格式，且已多年。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。SUSE、Debian 和 UNIX 系统支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。SUSE、Debian 和 UNIX 系统支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。运行在 Fedora、SUSE、Debian 和 UNIX 系统上的主要文字处理产品都支持 PostScript。

## 运行打印服务器

5. 如果检测到您想要配置的打印机，只需选择它即可。如果没有检测到，请选择打印机连接的设备（LPT #1 和 Serial Port #1 是第一个并行端口和串行端口）并点击“下一步”。有关远程打印机的信息，请参阅下一个步骤。）

6. 选择“从数据库选择打印机驱动程序”（并选择制造商）或选择“提供 PPD 文件”（并选择驱动程序）。点击“下一步”为您的打印机选择特定的驱动程序（您可能有多个选择）。

如果您有一台在 Windows 中可以工作但在 Linux 中无法工作的打印机，请参阅随打印机一起安装的磁盘（可能是 CD）。选择“提供 PPD 文件”，并在磁盘上查找 PPD 文件以为 Linux 选择驱动程序。

![](img/d7f79c91d15076e71790c1b4e1d072d0_735_0.png)

7. 如果您的打印机没有出现在列表中，但支持 PCI（HP 打印机控制语言），请选择其中一个打印机（如 HP LaserJet）。如果您的打印机支持 PostScript，请从列表中选择 PostScript 打印机。选择“原始打印队列”允许您向打印机发送已针对该打印机类型格式化过的文档。

7. 点击模型框中的您的打印机型号，并为您的打印机选择驱动程序。

![](img/d7f79c91d15076e71790c1b4e1d072d0_735_1.png)

8. 如果您点击“打印机”、“驱动”或“PPD”按钮。在很多情况下，您将看到来自 Linux 打印数据库的信息，有关您的打印机如何配置以及如何进一步调整。点击“下一步”继续。

9. 如果信息看起来正确，点击“应用”为您的打印机创建条目。

打印机出现在主打印机配置窗口中。如果您想让该打印机成为默认打印机，点击“设为默认打印机”按钮。添加其他打印机时，可以通过选择它并点击“设为默认打印机”来更改默认打印机。

10. 此时打印应该可以工作了。为了确保，从左列选择您刚刚添加的打印机。然后点击“打印机测试页”按钮。（如果您想与网络上的其他计算机共享打印机，请参阅本章的“配置打印服务器”部分。）

## 在 Fedora 中编辑本地打印机

选择您想要配置的打印机后，从以下选项卡中更改其配置：

- 设置 — Settings — 您之前创建的描述、位置、设备 URI 和模型信息将显示在此选项卡上。除了添加的原始选项外，以下内容说明了如何更改其他选项：
- 状态 — State — 勾选框以指示打印机是否会打印队列中的作业（启用）、接受新的打印作业（接受作业）或是否可以与与您的计算机通信的其他计算机共享（共享）。
- 设为默认打印机 — Make Default Printer — 选择此选项卡将打印机设置为默认打印机。
- 策略 — Policies — 点击“策略”选项卡。从此选项卡，您可以设置以下项目：
- 横幅 — Banner — 在任务的开始或结束添加横幅页。对于多人共享的打印机，这是一个良好的做法。横幅页可以帮助您分类谁获取了哪个任务。标准横幅页显示打印作业的 ID、文件、请求打印作业的用户以及与之相关的任何计费信息。
- 策略 — Policies — 以防发生错误，选择“停止打印机”将取消向该打印机的所有打印。您也可以选择在发生错误情况时丢弃作业（中止作业）或重试作业（重试作业）。
- 访问控制 — Access control — 如果您的打印机是共享打印机，您可以选择此选项卡创建一个列表，要么允许用户访问打印机（拒绝所有其他），要么拒绝用户访问打印机（允许所有其他）。
- 打印机选项 — Printer Options — 点击打印机选项设置与打印机驱动程序相关的详细信息。可用取决于打印机而异。许多选项可以在有人打印文档时进行覆盖。
- 横幅 — Watermark — 有若干横幅设置允许您在页面上添加横幅。默认情况下，横幅和覆盖关闭的（无）。通过选择横幅（文本之后）或覆盖（文本之上），您可以设置横幅以确定如何执行横幅。横幅可以出现在所有页面（全部）或仅第一页（仅第一页）。

选择横幅文本以选择用于横幅或覆盖的文字（草稿、副本、机密、最终等）。

然后您可以选择横幅或覆盖的字体类型、大小和强度。

- 分辨率增强 — Resolution Enhancement — 您可以使用打印机的当前设置或选择开启或关闭增强。
- 页面大小 — Page Size — 默认是信纸，但您也可以要求打印机打印法律、信封、ISO A4 标准或其他页面大小。
- 介质源 — Media Source — 选择打印纸盒。选择手动1 以手动插入纸张。
- 灰阶 — Levels of Gray — 选择使用打印机当前的灰阶或增强的标准灰阶。
- 分辨率 — Resolution — 选择默认打印分辨率（例如 300、600 或 1200 dpi）。分辨率越高质量越好，但耗时越长。
- 经济模式 — EconoMode — 您可以使用打印机的当前设置或选择开启或关闭增强。

## 运行打印服务器

- 服务器（Server）——计算机的 BIOS 名称或 IP 地址，其可能与 TCP/IP 名称不相同。为了将此名称转换为访问 SMB 主机所需的地址，Samba 会检查多个可能将名称分配给 IP 地址的地方。Samba 会按照所示顺序检查以下位置直到找到匹配项：本地的 `/etc/hosts` 文件、本地的 `/etc/mhosts` 文件、网络上的 WINS 服务器以及对本地网络接口广播响应的响应。
- 共享（Share）——打印机与远程计算机共享时的名称。它可能与 SMB 打印机本地用户识别打印机时的名称不同。
- 用户（User）：SMB 服务器系统用于授予访问 SMB 打印机的用户名。如果你是基于共享级而非用户级访问控制对打印机进行验证，则不需要用户名。在共享级访问中，你可以为每个共享打印机或文件添加密码。
- 密码（Password）：与 SMB 服务器或共享资源相关，取决于所使用的访问控制类型。

注意 当你为 SMB 输入用户和密码时，这些信息将以未加密的形式存储在 `/etc/cups/printers.conf` 文件中。请确保该文件对 `root` 用户保持可读。

以下是一个你可以添加到 SMB:: 框中的 SMB URI 示例：

```
