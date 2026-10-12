
理论上，你可以通过使用`Network Printer`模板而不是`Printer`模板来创建一个不占用本地端口的链接。遗憾的是，此过程存在 Bug——它与`Samba`服务器配合使用时会产生错误，导致打印机队列。可能`Samba`版本会解决这个 Bug，或者未来的`OS/2` FixPack 或更新版本的`OS/2`将修复此问题。在此，通过重定向的本地端口打印是可以行的，而且它具有可以在`DOS`、`Windows`程序以及`OS/2`程序运行的优势。

## 理解 OS/2 SMB/CIFS 特性

`OS/2`与大多数系统一样，在`SMB/CIFS`网络方面有一些特殊之处。在配置`Samba`和使用`OS/2`时，理解这些特性至关重要。虽然`Samba`的默认配置选项与`OS/2`配合良好，但你应该知道哪些选项是不应使用的。

### `OS` `OS2` 中的文件名和扩展属性 (EAs)

`OS/2`使用扩展属性（EAs）来存储某些类型的信息。`OS/2`处理大小写文件名的方式与`Windows` 9/2000 相同，`OS/2`保留大写和小写字符。高性能文件系统 (HPFS) 原生支持 EA，且`OS/2`在 FAT 分区上存储它们。遗憾的是，`SMB`不支持这些。

`OS/2`有一个特殊之处，它使用 EA 来存储某些信息。

## 附录 B 特定操作系统问题

这种方法确实存在某些缺点。缺点与`Windows`下遇到的相同。此外，在`OS/2`程序与`Windows`程序中，可能并不清楚哪个短文件名对应哪个长文件名。

### `Samba` 与 `BeOS`

`announce = Yes`，但这对带有`OS/2`系统的网络产生的影响不大。如果你希望你的`OS/2`系统能够在`OS/2`的`Windows`窗口中看到你的`Samba`服务器，则不应将`announce`设为`No`。

## Samba 与 BeOS

最新的主流操作系统之一是`BeOS`，它同时适用于`Intel.x86`和摩托罗拉`PowerPC` (PPC) 电脑。该系统的 5.0 版本由`Be` (<http://www.be.com>) 以有限（但免费）的形式提供，并以“专业版”（`Professional`）的形式在`CD-ROM`光盘上提供。后者包含一个名为`World O' Networking` (WON) 的`SMB/CIFS`客户端和服务器软件，尽管`WON`默认并不安装。你也可以从`ftp://.be.com/pub/experimental/r5/apps/WON/`获取`WON`。本节的其余部分假设你正在使用`BeOS` 5.0 的专业版。

> **警告** `WON`被认为是实验性软件。这意味着它在质量上本质上是 beta 甚至是 alpha 级。`WON`运行缓慢或完全无法运行并不罕见。我强烈建议你在安装`WON`之前备份任何`BeOS`系统，并准备好面对一些沮丧的体验。

## 在 BeOS 中安装 SMB/CIFS 支持

遗憾的是，`WON`远非一个完善的产品。在`BeOS` 5.0 的全新默认安装中，安装程序无法正常工作，导致系统没有任何任何类型的支持。在`BeOS`中让`SMB/CIFS`网络运行的最佳方法是在系统安装期间开始：

### 附录

#### 附录 B 特定于系统的问题

**图 B.11** `BeOS` `WON` 设置框允许你输入常用的内核`SMB/CIFS`参数。

![](img/d9a4a3fb0f0756635ea9aafdf129ae4f_600_0.png)

1. 在此对话框中输入你的域或工作组名称、用户名和密码，然后点击`Done`（完成）。`BeOS`提示你必须重启网络。确认此操作。
2. 从`CD-ROM`上的`WON`目录将`Netscript.CIFS`文件复制到`/boot/bees/system/boot`目录，并将其重命名为`Netscript`。（此操作可以规避`WONSet`程序中的错误。）
3. 重启`BeOS`。

如果运气好，结果应该是一个可以运行的`BeOS`系统，桌面上配有`World O' Networking`。（在操作系统其余部分启动后，这可能需要几秒钟才会出现。）你可以使用此图标浏览并使用网络资源，也可以使用命令行工具挂载远程文件系统。

## 从 BeOS 使用 Samba 服务器

从`BeOS`使用`Samba`服务器最简单的方法是使用`World O' Networking`图标。双击此图标会产生一个与`Windows`的“我的网络”（`Neighborhood`）或`OS/2`的“连接”（`Connections`）类似的网络视图。你可以使用此功能浏览工作组、服务器和共享。然而，与`DOS`、`Windows`和`OS/2`客户端不同，`BeOS`的`World O' Networking`在显示基本网络信息之前不会获取用户名和密码信息。这了两个两个结果：

- 你可能比使用其他客户端更频繁被要求用户名和密码，且时间不同。
- 因为没有与客户端关联的用户名，你不会在`World O' Networking`中看到带有你用户名的主目录。如果你在`[homes]`共享中省略`browseable=No`参数，你将在`World O' Networking`列表中看到一个名为`Homes`的共享。

如果你愿意，可以使用类似于`DOS`、`Windows`和`OS/2` `NET`命令或`Samba`的`smbmount`命令的命令行工具。此命令称为`cifsmount`，其语法如下：

```
cifsmount \\SERVER\\SHARE USERNAME PASSWORD mountpoint
```

**提示** 注意在`cifsmount`命令中输入正确数量的反斜杠（`\\`）。如果你漏掉了一个，你将收到一条有关该程序正确用法的消息。

`cifsmount`参数的意义应该是显而易见的。`mountpoint`（挂载点）的作用就像`Linux`挂载点——它必须客户端文件系统上的目录（通常是空目录），例如`/cifs/mystuff`。

要从`BeOS`使用`Samba`打印机，请遵循以下指令：

1. 从任务栏选择`BeOS` > `Preferences`（首选项） > `Printers`（打印机）。这将产生如 B.12 所示的对话框（尽管打印机区域可能没有任何项目）。

**B.12** 你可以从`BeOS`打印机对话框添加并控制打印机。

![](img/d9a4a3fb0f0756635ea9aafdf129ae4f_601_0.png)

2. 点击打印机对话框中的`Add`（添加）按钮。`BeOS`询问你想添加本地打印机还是网络打印机。
3. 选择网络打印机选项并点击`Continue`（继续）。`BeOS`显示如图 B.13 所示的`Add a Network Printer`（添加网络打印机）对话框。

**图 B.13** 添加网络打印机对话框允许你指定打印机的名称和网络位置。

![](img/d9a4a3fb0f0756635ea9aafdf129ae4f_602_0.png)

4. 在`Printer Name`（打印机名称）字段中输入打印机名称。
5. 在`Printer Type`（打印机类型）选择框中，选择你定义的打印机通用类别（`PostScript`、`PCL`等）。如果你使用`Ghostscript`驱动的打印机，请选择`PostScript`。
6. 点击`Browse`（浏览）查找打印机。结果如图 B.14。

**图 B.14** `BeOS`的`AppleTalk`与`Samba`链接。

![](img/d9a4a3fb0f0756635ea9aafdf129ae4f_603_0.png)

7. 浏览网络，找到打印机，选择`Samba`。`BeOS`现在询问你是否要删除。
8. 在打印机对话框中点击`Add`。`BeOS`现在显示制造商。
9. 如果你删除文件，打印机将出现在。
10. 如果你右键点击文件并选择`Move to Trash`（移到垃圾桶），`BeOS`提供了。

## BeOS 文件系统特性

与所有操作系统一样，`BeOS`在大小写敏感方面有自己的特性。为了确保你不会遇到问题（例如你可能想设置`case = Yes`），`BeOS`的原生文件系统更像`Linux`而不是`DOS`、`Windows`或`OS/2`。因此，对于`Samba`，归档、系统和隐藏位的设置并不重要。尽管`BeOS`文件系统支持`Unix`风格的所有者权限，但`BeOS` 5.0 版本并没有实现这种安全机制。`BeOS`因此并不尝试使用`Windows`风格的`ACL`来访问`Linux`功能。

与`OS`不同，`BeOS`使用额外的文件系统信息。由于`SMB/CIFS`未对此类数据提供支持，这些信息无法存储在`Samba`服务器上。对于许多文件，`BeOS`的属性可能会被`Samba`服务器损坏。遗憾的是，`BeOS`为文档实现了一个“垃圾桶”。`BeOS`提供了直接删除文件的。你也可以通过`bash` shell 中的`rm`命令删除文件。

## Samba 与 MacOS

`Apple`的`MacOS`有自己的`AppleTalk`文件和打印机共享协议。`Linux`通过`Netatalk`服务器直接支持`AppleTalk`。你可能希望使用`Netatalk`为`Macintosh`提供服务。当你想要为`Macintosh`系统使用`SMB/CIFS`时：
