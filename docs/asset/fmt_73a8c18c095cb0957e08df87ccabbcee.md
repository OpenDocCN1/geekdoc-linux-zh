
# 72 第 2 章 软件组件

3. 要确定哪些应用程序运行在系统上，如果有必要，点击“应用历史”选项卡。

4. 检查列出的应用程序。

5. 要确定哪些进程正在运行并检查它们，点击“进程”选项卡。所有资源都列在左侧。

要查看进程选项卡中有关特定资源的信息，请点击资源标题。例如，你可以点击 CPU 列以按升序查看 CPU 使用情况的详情。再次点击列标题以按降序查看 CPU 使用情况。

![](img/290e46d5832f20e3707f4841e4e6d75a_91_0.png)

1. 点击性能选项卡。要检查所有进程和线程的利用率、速度、吞吐量，请检查图表底部的数据。

2. 要获取更详细的信息，点击窗口底部的“打开资源监视器”。如有必要，输入 `Pa$$wword` 继续并点击“是”。

3. 检查 CPU 窗中的进程，然后点击 CPU 箭头。

4. 要检查磁盘使用情况，点击“磁盘”箭头。检查磁盘使用情况后，再次点击“磁盘”箭头。

5. 要检查网络使用情况，点击“网络”箭头。检查网络使用情况后，再次点击“网络”箭头。

6. 要检查内存使用情况，点击“内存”箭头。检查内存使用情况后，再次点击“内存”箭头。

7. 关闭 Windows 10 虚拟机内的所有窗口。

8. 保持虚拟机登录状态以备后续活动使用。

## CentOS 7 系统监视器

你可以使用 PC 上的系统密集型任务。图 2-22 实时显示按 CPU 使用百分比排序的进程活动。要按 % CPU 列排序，点击其列标题。默认情况下，显示每五秒更新一次。

系统监视器包含比只有“进程”选项卡更多的表格。如图 2-22 和 2-23 所示，它还包含“资源”。图 2-22 显示了关于以下内容的实时信息：CPU 使用率、内存使用、磁盘使用和网络使用。图 2-23 显示了关于以下内容的实时信息：CPU 使用率、内存使用、磁盘使用和网络使用。

| 进程名称 | 用户 | % CPU | ID | 内存 |
| :--- | :--- | :--- | :--- | :--- |
| gnome-system-monitor | User01 | 1 | 26948 | 13 MB |
| gnome-shell | User01 | 1 | 22341 | 149.4 KiB |
| gnome-keyring-daemon | User01 | 1 | 22047 | 808.0 KiB |
| gnome-session | User01 | 0 | 22097 | 2.0 MB |
| dbus-launch | User01 | 0 | 22105 | 144.0 KiB |
| dbus-daemon | User01 | 0 | 22106 | 1.4 MB |
| gvsd | User01 | 0 | 22171 | 628.0 KiB |
| gvsd-fuse | User01 | 0 | 22175 | 2.7 MB |
| ssh-agent | User01 | 0 | 22243 | 572.0 KiB |
| at-spi-bus-launcher | User01 | 0 | 22269 | 568.0 KiB |
| dbus-daemon | User01 | 0 | 22273 | 616.0 KiB |
| at-spi2-registry | User01 | 0 | 22278 | 636.0 KiB |
| gnome-settings-daemon | User01 | 0 | 22287 | 10.1 MB |
| pulseaudio | User01 | 0 | 22307 | 2.8 MB |
| gsd-printer | User01 | 0 | 22325 | 1.5 MB |
| dbus-daemon | User01 | 0 | 22374 | 4.1 MB |
| dbus-conf | User01 | 0 | 22379 | 696.0 KiB |
| dbus-x11 | User01 | 0 | 22382 | 3.9 MB |
| gnome-shell-calendar-server | User01 | 0 | 22384 | 2.5 MB |
| evolution-source-registry | User01 | 0 | 22393 | 3.4 MB |
| mission-control-5 | User01 | 0 | 22402 | 3.5 MB |

**图 2-21** CentOS 7 系统监视器中的进程活动

来源：Red Hat CentOS 7/系统监视器

![](img/290e46d5832f20e3707f4841e4e6d75a_93_0.png)

**图 2-22** CentOS 7 系统监控的资源选项卡

来源：Red Hat CentOS 7/System Monitor

| 设备 | 目录 | 类型 | 总计 | 可用 | 已用 |
| --- | --- | --- | --- | --- | --- |
| `/dev/mapper/` | | | 18.7 GB | 13.0 GB | 5.7 GB |
| `/dev/sdb1` `/boot` | xfs | 520.8 MB | 312.0 MB | 208.8 MB | 40 % |
| `/dev/sdb1` `/mnt/sdb` | xfs | 2.1 GB | 2.1 GB | 33.8 MB | 1 % |
| `/dev/sdc1` `/mnt/sdc1` | vfat | 2.1 GB | 2.1 GB | 4.1 kb | 0 % |

**图 2-23** CentOS 7 系统监控的文件系统选项卡

来源：Red Hat CentOS 7/System Monitor

## 活动 2-4：使用 CentOS 7 系统监控

![](img/290e46d5832f20e3707f4841e4e6d75a_93_1.png)

**所需时间：** 15 分钟

**目标：** 使用 CentOS 7 系统监控查看虚拟机的性能。

描述：在本次活动中，你将在 CentOS 7 中打开系统监控。通过按 CPU 使用率百分比排序来定位活动进程。使用其他选项卡查看有关系统的重要信息。如果你想查看进程和虚拟机的性能，此活动将非常有用。

- 1. 如必要，使用活动 1-1 中的相应指令启动你的虚拟机。
- 2. 要打开系统监控，点击“应用程序”`Applications`，“系统工具”`System Tools`，然后点击“系统监控”`System Monitor`。
- 3. 要查看进程，点击“进程”`Processes`选项卡。
- 4. 要确定最活跃的进程，点击 `% CPU` 按钮，直到人向箭头指向下方。
- 5. 要查看系统资源的图表，点击“资源”`Resources`选项卡。
- 6. 要确定可用磁盘空间量，点击“文件系统”`File Systems`选项卡。
- 7. 关闭系统监控窗口。

保持虚拟机登录状态以备后续活动使用。

## 应用程序

你在个人电脑上使用许多应用程序，包括文字处理器、电子表格、演示文稿软件、Web 浏览器、电子邮件客户端、游戏和图形软件。应用程序由许多协同工作的小程序组成，这并不稀奇。应用程序是人们使用计算机的原因。

Microsoft Office 是一套为 Windows 操作系统开发的程序包。它的组件包括：

- `Microsoft Word`—一个文字处理器，被认为是 Office 2013 中的主程序；它在文字处理市场占据主导地位。其专有的 DOC 格式是事实标准，尽管其最新版本也支持基于 XML 的格式。
- `Microsoft Excel`—一个电子表格程序；与 Microsoft Word 一样，它拥有着主导的市场份额。它最初是 Lotus 1-2-3 的竞争对手，但最终成为了事实标准。
- `Microsoft PowerPoint`—一个流行的演示文稿程序；它用于创建由文本、图形、电影和其他对象组成的幻灯片。幻灯片可以显示在屏幕上或打印在透明片或灯片上。

### LibreOffice

LibreOffice 是由非营利组织 The Document Foundation 开发的免费开源办公软件套件。它于 2010 年基于 OpenOffice.org 构建。LibreOffice 显著提升了将 Microsoft 文档导入 Linux 的能力。所有 Linux 发行版默认都包含了它。它的组件包括：

- `Writer`—一个与 Microsoft Word 具有相似外观和感受的文字处理器，并提供了大量重叠的功能和工具。它可以保存为 `.docx`（这是从 Office 2007 开始保存 Word 文档的默认格式）。`Writer` 允许你在无需额外软件的情况下创建或导出为 PDF 文件。
