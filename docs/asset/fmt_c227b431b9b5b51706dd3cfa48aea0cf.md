
如果你要向可以访问 Samba 的人员列表中添加用户，请前往“首选项”并选择“Samba 用户”。你可以添加机器上存在的任何用户。你可以在图 22.5 中看到“添加用户”界面。重要的是你要意识到，你只能添加在此机器上拥有用户账户的用户，因此你首先需要为希望访问 Samba 共享目录的人添加一个用户账户。仔细想想，这完全合乎情理。如果一个人首先没有被授予对某台机器的访问权限，他就无法访问该机器上的目录。请记住，在前几章中，我们讨论了如何从 KDE 和 Shell 添加用户。

![](img/12d790664598bbf390261087fbe55bbc_438_0.png)

创建 Samba 共享目录并授予用户访问权限只需如此简单。共享打印机比你想象的要简单得多。回想起来，在本书早期，你被告知 Linux 将设备视为文件。对 Linux 来说，你的软盘驱动器实际上是 `/dev/fd0`。你的打印机也是一个设备文件。当你要共享打印机时，前往 `/dev` 文件夹并选择你的打印机即可！

与大多数应用程序一样，Samba 也可以配置。如果你前往“设置”并选择“Samba 设置”，你会看到如图 22.6 所示的界面。在此界面的第一个标签页上，你可以选择 Samba 运行所使用的工作组和用户名。还记得我们讨论 Apache Web 服务器时提到的吗？它也以一个特殊的用户账户运行。对于应用程序的用户账户（如 Samba 和 Apache 的账户），除非有迫切的原因，否则最好保留默认设置。

![](img/12d790664598bbf390261087fbe55bbc_438_1.png)

设置下还有第二个标签页，如图 22.7 所示。此标签页允许你设置安全选项。你可以选择如何验证登录尝试、是否加密传输等。

![](img/12d790664598bbf390261087fbe55bbc_439_0.png)

图 22.7：Samba 安全选项卡。

## 其他服务

虽然 Samba 是一个有趣且非常实用的服务，但它并不是 Linux 中唯一可用的服务。请记住，*service*（服务）和 *daemon*（守护进程）这两个词可以互换使用。这两个词都指代在后台运行并为系统提供某种服务的程序。以 Samba 为例，它提供的是对 Windows 机器的访问权限。

在*Server Settings*（服务器设置）下，你还会找到服务管理功能。该屏幕显示在**图 22.8**中。通过这个工具，你可以查看机器上正在运行的所有服务。你还可以启动或停止任何你想要的服务。但是，你无法从这个屏幕配置这些服务，只能启动或停止它们。

![](img/12d790664598bbf390261087fbe55bbc_440_0.png)

**图 22.8**：服务配置屏幕。

对于你的计算机来说，最重要的服务之一是打印。在讨论 Samba 时，我们提到你甚至可以与 Windows 用户共享你的打印机。很有可能明智的做法是确保你可以向 Linux 机器添加打印机。我们在前一章中简要讨论过这个问题，但没有深入展开。

如果你进入*Start*（开始）菜单，选择*System Settings*（系统设置），然后选择*Printing*（打印），你会看到类似**图 22.9**中那样的屏幕。该屏幕列出了打印队列中等待的所有文档以及打印机。正如你所见，此时我们没有连接任何打印机。

![](img/12d790664598bbf390261087fbe55bbc_440_1.png)

**图 22.9**：打印管理器。

让我们添加一个打印机。点击工具栏上的*New*（新建）按钮。你的计算机将花费几分钟时间查找任何已连接的打印机，然后启动向导以设置打印队列。在这个练习中，我们将设置一个实际的打印机。这并不是对该特定打印机型号的推荐。这是作者正在使用的机器上连接的打印机。打印队列向导的第一个屏幕，如**图 22.10**所示，告知你即将发生什么。

![](img/12d790664598bbf390261087fbe55bbc_441_0.png)

**图 22.10**：打印队列向导屏幕一。

下一个屏幕，见**图 22.11**，要求你为该打印机命名并提供简短描述。名称是绝对必需的。这是你在各种应用程序中引用打印机时使用的标识。描述是可选的。

![](img/12d790664598bbf390261087fbe55bbc_441_1.png)

**图 22.11**：打印队列向导屏幕二。

第三个屏幕，如**图 22.12**所示，是最重要的。在这里，你看到的是 Linux 能够检测到的所有本地连接打印机列表。在这种情况下只有一个。你还可以使用顶部的下拉菜单，将查找本地控制的打印机更改为查找网络打印机。点击你想使用的打印机一次，然后点击前进按钮。

![](img/12d790664598bbf390261087fbe55bbc_442_0.png)

图 22.12：选择打印机。

如果你了解关于打印机的技术细节，你可以从图 22.13 所示的列表中选择打印机的类型。但是，如果你不确定，或者你的打印机规格不在列表中，请选择通用打印机选项。

![](img/12d790664598bbf390261087fbe55bbc_442_1.png)

图 22.13：打印机类型。

一旦你选择了特定的打印机型号和类型，你就可以完成向导。然后系统会询问你是否想打印测试页。通常这样做是个明智的主意。正如你所见，在 Linux 中设置打印机并非一项困难的任务。

## 总结

本章涵盖了几个非常重要的主题。我们讨论了 Samba，如果你的 Linux 机器需要能够被 Windows 机器访问，这是一个关键的实用工具。Samba 使你可以运行混合环境，结合 Windows 和 Linux 机器。我们还讨论了服务配置实用工具。这对于了解哪些服务已启动，以及根据需要停止或启动它们非常有用。

我们通过讨论添加打印机结束了本章。在某个时间点，大多数人都会希望从计算机打印。使用打印队列向导，你应该可以将大多数打印机连接到你的 Linux 机器而不会遇到麻烦。

## 复习题

- 1. 什么是 Samba？
- 2. 什么是 SMB？
- 3. 什么是 IPC？
- 4. 如何从服务配置屏幕配置一个服务？

### 答案

- 1. 它是一个允许 Windows 用户访问 Linux 目录的实用工具。
- 2. 服务器消息块（Server Message Block），一种微软网络协议。
- 3. 进程间通信（Inter Process Communication）。
- 4. 你无法配置。你只能启动或停止服务。

# 附录 A：其他资源

本附录旨在帮助你进一步学习本书中介绍的任意内容。显然，一本书无法涵盖所有内容，因此这些资源旨在为你提供帮助。我挑选了我认为最能提供优质、扎实 Linux 信息的资源。

## 通用 Linux 链接

- **Linux Online:** http://www.linux.org/
- **Linux.com:** http://www.linux.com/
- **The Linux Journal:** http://www.linuxjournal.com
- **Linux Today:** http://linuxtoday.com/
- **Linux World:** http://www.linuxworld.com/

## 发行版

- Red Hat Linux: http://www.redhat.com/
- Debian Linux: http://www.debian.org/
- Mandrake Linux: http://www.mandrakelinux.com/en/
- SuSE Linux: http://www.suse.com/index_us.html
- Slackware: http://www.slackware.com/

## Linux 教程

- Linux Online: http://www.linux.org/
- Linux Planet: http://www.linuxplanet.com/linuxplanet/tutorials/
- Linux Guru's: http://www.linuxguruz.com/z.php?id=2

## Linux 软件

- **Open Office:** http://www.openoffice.org/
- **Star Office:** http://wwws.sun.com/software/star/staroffice/6.0/
- **Opera Web Browser:** http://www.opera.com/
- **Mozilla Web Browser:** http://www.mozilla.org/
- **Netscape Web Browser:** http://www.netscape.com/
- **VS FTP Server:** http://vsftpd.beasts.org/
- **Apache Web Server:** http://www.apache.org
