
```
$ lq
Printer: lp@localhost
Queue: 2 printable jobs
Server: pid 4134 active
Unspoller: pid 4135 active
status: processing 'dfA133localhost.localdomain', size 467, format 'f'
IF filter 'filter' at 18:53:49.28
Status: waiting for subserver to exit at 18:54:05.230
Rank Owner/ID Class Job Files Size Time
root@localhost+133 A 133 /home/jake/prl 467 18:53:49
root@localhost+197 A 197 /home/jake/mydoc 23948 18:54:05
```

输出显示队列中有两个待处理的打印打印任务。（在这种情况下，它们没有打印，是因为打印机已关闭。）在 `Job` 列下，你可以看到与每个文档关联的作业编号。要删除第一个打印任务，请输入：

```
lprm 133
```

# 使用 `lpc` 控制打印机

`lpc` 命令允许你检查打印机状态、启用和禁用打印机，并更改队列中作业的安排。你对打印机执行的任何操作都可以针对单个打印机（通过指定打印机名称）或针对所有打印机（使用单词 `all`）。要禁用特定的打印机（例如，一个名为 `canyonsps` 的打印机），请使用 `disable` 选项并输入：

```
$ lpc disable canyonsps
Printer: canyonsps@localhost
kill server PID 4134 with User defined signal 1
canyonsps@localhost.localdomain: disabled
```

要启用已禁用的打印机（例如上一个示例中的打印机），请使用 `enable` 选项并输入：

```
$ lpc enable canyonsps
Printer: canyonsps@localhost
canyonsps@localhost.localdomain: disabled
```

当打印机被禁用时，它仍然可以继续接收打印任务并将其保留在队列中，直到打印机再次启用。如果你想完全防止任务被外存，请使用 `stop` 选项，如下：

```
$ lpc stop canyonsps
Printer: canyonsps@localhost
canyonsps@localhost.localdomain: stopped
```

要重新启动打印进程并恢复打印，请使用 `start` 选项，如下：

```
$ lpc start canyonsps
Printer: canyonsps@localhost
canyonsps@localhost.localdomain: stopped
```

要禁用打印机并杀死 `lpd` 守护进程（以便不再打印后续任务），请使用 `abort` 选项，如下：

```
$ lpc abort canyonsps
Printer: canyonsps@localhost
kill server PID 4134 with User defined signal 1
canyonsps@localhost.localdomain: aborted
```

# 配置打印服务器

连接到你的 Red Linux 系统的打印机可以通过不同的方式与其他计算机共享。你的计算机不仅可以作为 Linux 服务器，还可以向其他客户端显示为 NetWare 或 SMB。在将本地打印机添加到你的 Red Linux 系统且你的计算机连接到网络后，你可以使用本节中的操作程序。

## 在 `lpd.perms` 中配置共享的 Linux 打印机

在你的 Red Linux 计算机添加本地打印机后，让其他计算机可以使用它非常简单。如果共享打印机的计算机之间存在 TCP/IP 网络连接，你只需要向单独的主机授予权限。

来自计算机的用户对你的打印机的权限根据 `lpd.perms` 文件中的值确定。默认情况下，你应该能够从其他计算机打印到你的打印机。如果你想限制对打印机的访问，可以修改 `lpd.perms` 文件。

## 配置共享的 NetWare 打印机

Red Linux 提供的 NetWare 功能通过使用 `mars_nwe` 包提供。该包允许你从 Red Linux 进行文件和打印共享，就像共享资源来自 NetWare 服务器一样。虽然没有提供所有的 NetWare 功能，但 `mars_nwe` 包可以很好地处理基础的 NetWare 文件和打印共享。

![](img/176fece2d30daee750bc078e898ee4_651_0.png)

有关设置 `mars_nwe` 包的信息，请参考第 18 章。

你可以通过向 `/etc/nwserv.conf` 文件添加条目使你的 Red Linux 打印机作为 NetWare 打印机可用。此文件用于配置大多数 `mars_nwe` 信息。对于添加打印机，特别感兴趣的是队列部分（21节）。通过将每行识别为21节，可以将 Red Linux 打印机识别为 NetWare 打印队列。例如：

```
21 PRSPRINT SYS:/PRINT/PRSPRINT 1pr -Pprint
```

数字 `21` 标识为 NetWare 打印队列。`PRSPRINT` 是队列名称。队列目录标识为 `SYS:/PRINT/PRSPRINT`。注意队列目录与 `lpd` 缓存目录不同。最后，条目的最后部分是打印提交到此队列的文档的 `lpr` 命令。

## 配置共享的 Samba 打印机

可以通过 Samba SWAT（Samba Web 管理工具）程序将你的 Red Linux 打印机配置为共享 SMB 打印机。要使用 SWAT，你需要安装 Samba 包并配置服务以便在浏览器窗口中打开 SWAT。你还需要在你与使用打印机的客户端计算机之间建立 TCP/IP 连接。

### 第 17 章 ♦ 设置打印服务器

第 18 章描述了如何配置 Samba 和 SWAT 以便在浏览器中使用。

配置好 SWAT 后，你可以通过在本地计算机上打开 Netscape 并在位置框中输入以下地址打开该程序：

```
http://localhost:901/
```

从 Samba SWAT 主界面，点击打印机（Printers）图标。会出现打印机参数（Printer Parameters）页面。你的打印机可能已经作为共享 SMB 打印机可用。点击选择打印机（Choose printer）按钮旁边的复框。你应该看到一个可用打印机列表。弹出列表中名称前带有星号的打印机将自动加载为共享打印机。

要创建一个新打印机，在创建打印机（Create Printer）框中输入名称并点击创建打印机（Create Printer）。然后，填写打印机信息（路径、安全选项、打印选项、浏览选项和杂项选项）。完成后，点击更改（Changes）。要了解如何从 Linux 设置 SMB 打印机，请参阅本章较早之前的“添加 SMB 打印机”部分。

很有可能如果你在 Red Hat Linux 计算机上配置 SMB 打印机，你会想要将其与 Windows 95/98/2000 或 NT 客户端共享。客户端计算机可以通过网络访问你，找到并使用你的打印机应该是相当简单的。

客户端计算机查找你的共享 SMB 打印机的第一个地方是网络邻（Network Neighborhood，Windows 2000 为“我的网络位置”My Network Places）。从 Windows 95/98 桌面，双击“网络邻”图标。（对于 Windows 2000，双击“我的网络位置”图标。）你的主机计算机名称（NetBIOS 名称，也是你的 TCP/IP 名称）应该出现在屏幕上或屏幕上的组文件夹中。打开代表你计算机的图标。打开的窗口应显示你的共享打印机和文件夹。

如果你的计算机图标没有出现在“网络邻”中，请尝试使用查找（Find:）：从 Windows 95 开始，点击“开始” -> “计算机”。在“命名”（Named）框中输入你的计算机名称并点击“立即查找”（Find Now）。如果窗口找到了你的计算机，双击它。。会出现一个显示你计算机共享打印机和文件夹的窗口，如图 17-2 所示。

当你的共享打印机出现在窗口中后，客户端可以通过打开（双击）打印机图标来配置指向该打印机的指针。你会看到一条消息，告诉你在使用打印机之前必须对其进行设置。点击“是”（Yes）继续为本地使用配置打印机。出现添加打印机向导（Add Printer Wizard）。回答有关你打算如何使用打印机的问题，并添加适当的驱动程序。完成后，打印机将出现在你的打印机窗口中。它现在可以被选择为 Windows 95/98 中任何程序的打印机。

![](img/176fafece2d30daee750bc078e898ee4_652_0.png)

# 第四部分 + Red Hat Linux 网络和服务器设置

![](img/176fafece2d30daee750bc078e898ee4_653_0.png)
