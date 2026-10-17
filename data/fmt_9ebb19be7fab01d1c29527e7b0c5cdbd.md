
```ini
[hpdj]
path = /var/spool/samba
user = lucille, ricky
print ok = Yes

[lexmark]
path = /var/spool/samba
user = larry, lucille
print ok = Yes
```

在此配置中，只有 `larry`、`moe` 和 `curly` 可以使用打印机 `canon`，而只有 `lucille` 和 `ricky` 可以使用打印机 `hpdj`。`lexmark` 打印机则可由可以访问另外两台打印机中的每一台的两个用户访问，即 `larry` 和 `lucille`。正如你所见，共享级安全性在控制对特定打印机的访问能力方面极其灵活。另一方面，它也相当难以维护，因为随着网络上的用户发生变化，你必须频繁地在多个共享中添加和删除用户。这种访问方式还会减慢身份验证速度，特别是当共享的用户很多时，因为 Linux 在此方案中通过将提供的密码逐一与共享的授权用户进行比对来验证用户。

另一种应用共享级安全性的方式是为每个共享或一组共享创建特殊的 Linux 账户，然后将该账户的密码分发给需要访问相关共享的每个人。当然，这意味着单个密码将被广泛知晓，因此你必须格外谨慎地控制该账户在除其预期共享之外的其他方面的可访问性。（例如，黑客如果获知了密码和账户名，可能会通过 `telnet` 登录并尝试进一步捣乱。）更改密码也可能成为噩梦，因为你随后需要通知数个人密码已更改。

## 使用 Linux /etc/printcap 组控制

第 15 章“与其它 UNIX 系统共享打印机”描述了一种基于 Linux 组 membership 的打印机访问控制方法。具体来说，你可以在打印机 `/etc/printcap` 条目中添加一行，类似于以下内容：

`:rg=layout:\`

有效地限制对打印机的访问。事实上，你可以用这种方式为前面示例中的 `canon`、`hpdj` 和 `lexmark` 打印机实现完全相同的控制，这些打印机由 `larry`、`moe`、`curly`、`lucille` 和 `ricky` 使用。

## 使用 hosts allow 和 hosts deny 参数

你可以在单个共享的定义中使用 `hosts allow` 和 `hosts deny` 参数，按客户端控制对打印机的访问。例如，假设你的 Linux 计算机托管三台共享的打印机。打印机 `hp4000` 应可供你内部网上的所有计算机访问，而 `epson1520` 仅应可供艺术部门访问，`okidata` 仅应可供前台工作人员访问。如果艺术部门的计算机全部具有 `192.168.5.x` 范围的地址，而前台工作人员的计算机全部位于 `192.168.7.x` 范围内，那么你可以这样做：

```ini
[hp4000]
    path = /var/spool/samba
    print ok = Yes

[epson1520]
    path = /var/spool/samba
    hosts allow = 192.168.5.
    print ok = Yes

[okidata]
    path = /var/spool/samba
    hosts allow = 192.168.7.
    print ok = Yes
```

#### NOTE

> 此配置假定 `192.168.5.x` 范围内的所有计算机都属于艺术部门，并且 `192.168.7.x` 范围内的所有计算机都在前台。如果不是这样，你可以使用更复杂的 `hosts allow` 语句，例如添加 `EXCEPT` 子句以排除特定主机，如 `hosts allow = 192.168.7. EXCEPT gingko`

有关如何在 `hosts allow` 和 `hosts deny` 中指定计算机的详细信息，请参见第 11 章。

## 为打印配置 Windows

当然，要发挥作用，你的 Linux 打印服务器必须有客户端。这些客户端通常是 Windows 计算机，但也可以是 DOS、OS/2，甚至是本身运行 Samba 的 UNIX 或 Linux 计算机。（本章后面的“从 Linux 打印到远程 SMB/CIFS 打印机”部分提供了如何配置 Linux 以打印到 Windows 或 Samba 服务器的概述。）

## 安装合适的驱动程序

打印到 Samba 服务器最棘手的问题之一是确定要安装什么驱动程序。每个安装都是独特的，无论是硬件还是网络用户的需求，因此不可能给出始终适用的绝对指导。在某些情况下，你可能需要尝试几种配置才能找到满意的配置。

## 打印机队列配置

如第 14 章所述，你可以以多种方式配置 Linux 打印机队列：

- PostScript 打印机——如果你有一台打印机本身支持 PostScript，你可能希望使用 PostScript 打印机的标准过滤器来配置 Linux 打印机队列。然而，如果打印机同时支持 PostScript 和其他协议，你可能希望设置一个原始队列，将其输入直接馈送到打印机而不进行处理。这种原始队列解决方案允许你在客户端操作系统之间在两个驱动程序之间无缝切换。

- 通过 Ghostscript 的非 PostScript 打印机——你可以配置一台非 PostScript 打印机，例如使用 Hewlett-Packard 的 PCL 或 Epson 的 ESC/P2 的打印机，使其在客户端操作系统看来表现得像 PostScript 打印机一样。

- 通过原始队列的非 PostScript 打印机——如果你设置了一个不以任何方式处理其输入的队列，你可以使用客户端操作系统的原生驱动程序来打印该打印机，由操作系统或打印机制造商提供。

当你打印到原始队列时，无论使用 PostScript 还是非 PostScript 打印机，最好使用针对你所使用特定打印机型号的客户端操作系统驱动程序。这种做法可以让你最好地访问打印机的特定功能，例如内置字体、分辨率选项、纸张进纸器等。在许多情况下，对于通过普通 Linux 打印机队列馈送的 PostScript 打印机也是如此；但在某些情况下，Linux 的过滤器会误解模式更改代码或 Control-D 字符，并将 PostScript 代码转换为 ASCII 文本，从而产生无法使用的打印输出。这种情况下有三种可能的解决方案：

- 选择一个与你实际使用的打印机不同的 PostScript 打印机客户端驱动程序。

- 在 `/etc/smb.conf` 中为相关共享设置 `postscript = true` 选项。

- 在 Linux 服务器上设置一个原始队列并使用它来代替你之前使用的过滤队列。

并非所有这些选项在所有情况下都适用。例如，最后一种方法仅在你使用 PostScript 打印机或为你使用的特定打印机切换到客户端操作系统的原生驱动程序时才有效。

## 选择驱动程序

当你通过在 Linux 过滤器中使用 Ghostscript，利用客户端操作系统 PostScript 驱动程序向非 PostScript 打印机打印时，你会面临一个困境：在客户端操作系统上应选择哪种特定型号的 PostScript 驱动程序？由于你实际使用的打印机不是 PostScript 型号，你在可用的 PostScript 打印机列表中找不到它。相反，你必须选择另一种型号的 PostScript 打印机，或选择一个通用的 PostScript 选项，如果有的话。然而，你应选择与实际打印机功能尽可能匹配的 PostScript 打印机，特别是分辨率、可用的纸张尺寸和颜色支持方面。当然，你也可以为 Linux 服务器选择一个支持这些功能的 Ghostscript 驱动程序。

总体而言，我发现 Apple LaserWriter 驱动程序在使用 Ghostscript 驱动的黑白打印机时往往能产生良好的结果。较旧型号的驱动程序，例如 LaserWriter II 系列，与 300dpi 喷墨打印机和较旧的激光打印机配合良好。新型号的驱动程序，例如 LaserWriter 630，与 600dpi 打印机配合良好。

对于彩色打印机，我的建议是首先尝试 QMS magicolor 的驱动程序。这是一款 600dpi 彩色打印机，其驱动程序通常能与通过 Linux 下的 Ghostscript 驱动的彩色喷墨打印机配合得相当好。

如果你有具有特殊功能，例如超大纸张处理能力的打印机，你可能需要进一步寻找合适的驱动程序。许多此类高端打印机都有 PostScript 选项，因此你可以尝试制造商的网站，看看是否有为配备此类选项的打印机提供的驱动程序。

#### NOTE

> 尽管为某些打印机销售的计算机托管 PostScript 解释器在 Linux 下没有用处，但制造商为使用基于主机的解释器的打印机提供的 PostScript 驱动程序可能有用。从概念上讲，Ghostscript 取代了基于主机的解释器，并且从客户端使用打印机与从同一客户端使用同一打印机非常相似，只是打印机连接到运行制造商解释器的 Windows 计算机。

大多数客户端操作系统都附带一系列 PostScript 驱动程序，因此你不应为在 Ghostscript 队列中使用而找不到驱动程序。对于 PostScript 打印机，你也可以向打印机制造商咨询。你也可以为某些操作系统找到其他 PostScript 驱动程序，但使用前应检查许可条款。例如，Adobe 提供 PostScript 驱动程序，但它们仅许可用于使用正版 Adobe PostScript 的打印机，因此你不应将这些驱动程序与 Ghostscript 驱动的打印机或使用 PostScript 克隆解释器的打印机一起使用。

## 将驱动程序指向 Linux 服务器

你应按照随驱动程序或操作系统提供的说明在客户端计算机上安装驱动程序。在某个时候，操作系统会要求你定位打印机。例如，图 16.3 显示了 Windows NT 4.0 连接到打印机对话框，提示输入远程打印机的名称。根据操作系统和驱动程序的不同，你可能能够通过指向和点击的方式找到打印机，也可能需要输入 NetBIOS 风格的标识。在图 16.3 中，例如，打印机被标识为 `\\SPEAKER\escp2`，因为它是服务器 `SPEAKER` 上的 `escp2` 打印机。

![](img/5d4d3092919d1d16884788127447cc6d_421_0.png)

## FIGURE 16.3

此处显示的 Windows NT 4.0 连接到打印机对话框让你可以图形化地选择打印机，尽管并非所有操作系统都提供此便利。

## TIP

某些网络会出现服务器未出现在浏览列表中的问题，但它们仍然可用。你通常可以通过手动输入其名称来访问此类计算机上的打印机，即使你无法通过浏览找到它们。

完成客户端打印机队列的配置后，应进行测试打印。许多客户端操作系统都会提示你执行此操作。不过要做好准备——如果配置有误，打印机可能会开始吐出印满乱码的纸张。你可能需要在 Linux 中取消打印作业（使用 `lprm` 命令，如第14章所述）。你可能还需要在打印机本身上取消作业（大多数打印机都有前面板控制装置，请查阅你的手册）。

**提示**

从打印机中取出所有纸张，只留下一张，这样即使出现问题，也不会浪费大量纸张。你可能仍然需要取消打印作业，但至少不会在解决问题时看着纸张以最快速度从打印机中出来！

## 打印文件

配置好队列后，就可以像打印到本地队列一样向它打印。例如，图16.4显示了一个 Windows NT 4.0 打印对话框，配置为将作业打印到连接到名为 `speaker` 的服务器的 Epson Stylus Color 400 打印机。你可以选择其他打印队列、调整打印机属性，并在开始打印作业前调整其他打印选项，就像打印机是本地打印机一样。你可以查阅操作系统或打印机驱动程序的文档，了解可供你使用的更多选项。

![](img/5d4d3092919d1d16884788127447cc6d_422_0.png)

**图16.4**

打印对话框因操作系统而异，甚至因打印机驱动程序而异。

**注意**

如果你使用 PostScript 驱动程序打印到 Ghostscript 驱动的打印机，客户端操作系统中的某些选项可能无效，或者会导致意外情况发生。这是因为 PostScript 驱动程序可能期望硬件具有某些不存在的功能，例如进纸器或彩色打印能力。在某些情况下，硬件可能存在，但你仍然可能无法访问它。例如，Ghostscript 不了解打印机的进纸器选项，因此即使 PostScript 驱动程序允许你控制进纸器，你也可能无法使用这些选项。在许多情况下，你可以配置多个 Linux 打印机队列来重新获得这些“丢失”的功能，如第14章所述。

如果你经常从 Windows 下运行的 DOS 程序进行打印，你可能希望将共享打印机分配给本地打印机端口，以允许 DOS 程序打印。在 Windows 95 或 98 中，你可以通过右键单击打印机图标，然后从弹出的菜单中选择“属性”来执行此操作。选择“详细信息”选项卡，然后单击“捕获打印机端口”，这会打开“捕获打印机端口”对话框（见图16.5）。在“设备”字段中选择要用于打印机的端口，并在“路径”字段中输入端口的网络路径。（你可能需要手动输入此路径。如果你从要连接的打印机开始操作，可以从打印机的“属性”对话框中复制信息。）如果你希望此连接在重新启动计算机时仍然存在，请选中“登录时重新连接”。

![](img/5d4d3092919d1d16884788127447cc6d_423_0.png)

**图16.5**

“属性”对话框因打印机而异，但通常都有一个“详细信息”选项卡，其中的选项允许你将 DOS 可访问的端口链接到网络打印机。

完成端口捕获配置后，就可以从 DOS 程序打印到捕获的端口。不过，DOS 输出不会由 Windows 驱动程序处理。如果你以这种方式捕获了由 PostScript 或 Ghostscript 驱动的 Linux 共享，DOS 程序应输出 PostScript 以获得最佳效果，尽管某些队列可能也能处理原始 ASCII。如果你捕获的是原始队列，则需要在 DOS 程序中为所使用的打印机安装驱动程序。

## 从 Linux 打印到远程 SMB/CIFS 打印机

在某些情况下，你可能希望从 Linux 打印到 Windows 计算机或其他支持 SMB/CIFS 的系统上的远程打印机。为什么要这样做？以下是一些可能的原因：

- 你在对等网络上使用 Linux 计算机，而该网络上的 Windows 系统有一台你想使用的打印机。
- 你在客户端/服务器网络上使用 Linux 客户端，并且有 Windows 打印服务器。
- 你在客户端/服务器网络上使用 Linux 客户端，并且有 Linux 打印服务器，该服务器已配置为通过 Samba 共享打印机。打印服务器的管理员不想在该系统上配置 UNIX 风格的打印机共享。
- 你的 Linux 计算机充当 Macintosh 网络和 Windows 网络之间的转换器。你希望 Macintosh 计算机能够打印到 Windows 打印机，因此你设置了一个打印到 Windows 打印机的 Linux 打印机队列，并将该队列导出给 Macintosh 计算机。（这种情况与第15章中的图15.3类似。）

## 使用 printtool 配置打印队列

Red Hat Linux 直接支持 SMB/CIFS 打印配置。在 `printtool` 实用程序中，如果你在“添加打印机条目”对话框中选择了“SMB/Windows 95/NT 打印机”，Linux 将允许你使用图16.6所示的“编辑 SMB/Windows 95/NT 打印机条目”对话框来配置 SMB/CIFS 打印机。

除了本地打印机所需的信息之外，要使用 SMB/CIFS 队列，还必须填写以下字段：

- 打印服务器的主机名——服务器的 NetBIOS 名称。
- 服务器的 IP 号——你可以输入服务器的 IP 地址，以代替 NetBIOS 名称，或作为其补充。通常你不需要输入此信息。
- 打印机名称——服务器上打印机的名称。如果你要打印到另一个 Samba 系统，这是 Samba 共享的名称，可能与服务器 `/etc/printcap` 文件中的名称不同。

## FIGURE 16.6

配置 SMB/CIFS 打印机需要输入的信息比配置其他类型的本地或网络打印机更多。

![](img/5d4d3092919d1d16884788127447cc6d_425_0.png)

- User—所有 Samba 打印任务都通过一个用户名进行。您必须在此输入该用户名。这是服务器上的用户名，而不是本地机器；您在此输入的用户名不必与本地系统的用户对应。
- Password—您必须输入服务器上授权打印的用户的密码。

## CAUTION

正如 `printtool` 实用程序所警告的那样，当您通过 SMB/CIFS 队列打印时，Linux 会以未加密的形式将远程系统的用户名和密码存储在本地硬盘上。该文件名为 `.config`，位于 `/var/spool/lpd/printername` 目录中。不幸的是，该文件的权限为 `-rw-r--r--`，这意味着系统上的任何人都可以读取该文件。如果您限制权限，则只有 root 能够打印。因此，这对打印服务器来说是一个潜在的重大安全问题。您可以通过在服务器上创建一个专用仅打印账户来降低问题的严重性。如果服务器使用共享级安全性，那么用户名无关紧要，密码仅用于访问打印机共享，前提是服务器为所有服务配置了不同的密码。

- Workgroup—服务器所在的域或工作组的名称。

当您完成打印机队列的定义后，您可以像使用任何 Linux 打印机队列一样打印到它。您可以使用 `lp` 命令打印文档，如 `lp fly.ps`；或者您可以使用所用应用程序中的打印命令进行打印。打印机队列是 Samba 队列没有任何提示，它只是与您可能在系统上定义的任何其他本地或远程打印机队列一起存在（假设应用程序列出可用队列；并非所有应用程序都这样做）。

## Configuring a Queue Manually

如果您没有使用 Red Hat Linux，您应该查阅发行版的文档以获取配置 Samba 打印机队列的信息。如果您的文档缺少此信息，请按照以下步骤操作：

1. 以您通常的方式创建一个打印机。
2. 将 `/etc/printcap` 中的 `lp=` 条目更改为指向 `/dev/null`。
3. 在打印机 spool 目录（`/var/spool/lpd/printername`）中创建一个名为 `.config` 的文件，并在该文件中输入以下行：
   ```
   server=servername
   service=printername
   password=password
   ```
   您当然应该用适当的字符串替换 `servername`、`printername` 和 `password`。

#### Note

> 标准 `smbprint` 脚本文件将服务器的名称作为用户名传递。如果服务器设置为共享级安全性，这无关紧要，但如果服务器设置为用户级安全性，则服务器必须有一个以其自身命名的账户，并且密码在 `.config` 文件中指定。或者，您也可以修改 Linux 客户端上的 `smbprint` 脚本。

4. 将 `/etc/printcap` 中的 `if=` 行更改为指向 `smbprint` 脚本。该脚本可能位于 `/usr/bin`、`/usr/local/bin` 或其他位置，具体取决于您的发行版。
5. 更改 `/etc/printcap` 中的 `af=` 行，或在必要时添加该行以创建会计文件。这可以是 spool 目录中的一个文件。它的名称无关紧要，只要它不覆盖现有文件即可。例如 `af=/var/spool/lpd/printername/afile` 应该就足够了。
6. 重新启动打印机队列。

新的队列现在应该可以工作，但有一个主要警告：步骤 4 替换了您的过滤器文件，如果您已配置打印机队列使用智能过滤器将 PostScript 处理成打印机可理解的内容，那么您现在就失去了这种能力。因此，您可能希望创建一个新脚本，该脚本既调用旧的打印过滤器又调用 `smbprint`。然后您可以将此新脚本作为队列的新过滤器文件输入。如果服务器是具有自己的 Ghostscript 队列的 Linux 计算机，那么当然您可以将 PostScript 打印到远程系统，远程系统将执行 Ghostscript 处理。PostScript 处理也发生在远程

如果打印机是 PostScript 型号，当然，无论它托管在 Linux 还是 Windows 系统上。

> NOTE
> 
> 你可能会发现将打印服务器配置为接受 UNIX 风格的打印作业更容易。Linux 当然可以做到这一点，Windows NT 也可以。

## Summary

在你配置了 Linux 打印机队列并为文件共享设置了 Samba 之后，与 DOS、Windows 和 OS/2 机器共享打印机，只需在 `/etc/smb.conf` 文件中为打印机添加一个条目即可。该条目与文件共享条目非常相似，这是有原因的：Samba 打印机共享的工作方式与文件共享非常相似。客户端计算机打开一个共享并向其写入文件，Samba 随后将该共享定向到标准的 Linux 打印机队列。

在此场景中最大的复杂性来自于需要选择合适的打印机驱动程序集，既在 Linux 中（如果打印到非 PostScript 打印机，则用于 Ghostscript），也在客户端操作系统中（以匹配 Ghostscript 以及通过 Ghostscript 的打印机功能）。因此，在某些情况下，使用原生客户端操作系统驱动程序和原始队列进行打印可能更简单易配置。

也可以反向进行此过程，从 Linux 打印到 Windows 打印机。然而，你应该意识到这样做的安全影响，因为此配置要求服务器的密码以未加密的形式存储在客户端硬盘上，可供所有用户读取。

## Netatalk: Sharing Printers with Macintoshes

### CHAPTER
17

### IN THIS CHAPTER

- An Overview of Macintosh-Style Printer Sharing 408
- Setting Up Remote Access 411
- Configuring MacOS for Printing 415
- Printing from Linux to Macintosh Printers 419
- Summary 422

Linux 的打印机共享功能如果没有对 Macintosh 的支持就不算完整，而 Linux 在这方面也不令人失望。然而，Red Hat 6.0 并未随附必要的软件 Netatalk，因此它包含在本書附带的 CD-ROM 的 `sams-extras/netatalk` 目录中。Netatalk 结合 Linux 内核中对 Apple Datagram Delivery Protocol (DDP; p. 293) 的支持，使 Linux 能够参与 Apple 原生的网络“对话”。

本章不讨论 Netatalk 的基本配置。关于这一点，你应该阅读第 12 章“Netatalk: Sharing Files with Macintoshes”，尤其是标题为“Compiling AppleTalk Support into Your Kernel”和“The atalkd Daemon”的部分。在你启动了基本的 Netatalk 服务后，你可以阅读本章学习如何使你的打印机可供 Macintosh 使用。

Linux 可以成为 Macintosh 的出色打印服务器，部分原因在于 Macintosh 与网络 PostScript 打印机配合良好，但与大多数廉价喷墨打印机配合不佳，而使用 Linux 你可以将 PostScript 转换为喷墨打印机可理解的格式。你可以通过在 Linux 中配置 Ghostscript 程序自动作为打印过滤器的一部分来做到这一点。因此，你可以设置一台 Linux 计算机为一组 Macintosh 工作组提供两到三台廉价彩色喷墨打印机。即使包括 Linux 服务器的成本（它可以做的不止是提供打印机），你也可能比购买更昂贵的网络 PostScript 彩色打印机节省资金。Macintosh 也能自行共享其非 PostScript 彩色打印机，但这会占用服务器计算机，意味着你必须将计算机专用于服务器（在这种情况下，Linux 计算机和 PC 硬件更便宜），或者服务器计算机的用户在任何人想要打印作业时必须忍受性能下降。

### An Overview of Macintosh-Style Printer Sharing

一些最早的 Macintosh 使用 AppleTalk over LocalTalk 网络打印到最早的 LaserWriter（随后是其他 PostScript 打印机）。事实上，共享昂贵的 LaserWriter 打印机是大多数早期 AppleTalk 网络的主要功能。

由于早期的 Apple 激光打印机是 PostScript 型号，Apple 的网络打印模型高度以 PostScript 为中心。如今 PostScript 打印机种类繁多，因此 Apple 的 PostScript 驱动程序使用一个描述 PostScript 打印机功能的文件。这种方法允许单个 Macintosh 打印机驱动程序处理功能各异的各种打印机。

了解协议和打印机描述两者将有助于你处理 Macintosh 打印并配置 Netatalk 以服务 Macintosh，因此相关信息在此呈现。

## Macintosh 打印协议

Macintosh 使用打印机访问协议（PAP；第 293 页）进行打印，因此处理 Macintosh 打印请求的 Netatalk 组件称为 `papd`。PAP 在 DDP 及其他 Macintosh 网络协议之上运行，并且不通过 TCP/IP 工作。这与 UNIX 风格的 `lpd` 打印或 Samba 的 SMB/CIFS 实现不同，后两者都通过 TCP/IP 工作（尽管 Windows 计算机可以通过 NetBEUI 实现 SMB/CIFS，而 NetBEUI 与 TCP/IP 分开）。Netatalk——更准确地说，Adrian Sun 更新的 Netatalk 版本——可以通过 TCP/IP 在 AppleTalk 上共享文件，但不能以这种方式共享打印机。Netatalk 只能通过 DDP 共享打印机。虽然这听起来像是一个缺点，但并非 universally 如此。使用 DDP 作为 Macintosh 打印机共享的底层协议的主要优点之一是 DDP 不能作为一个整体通过互联网传输——至少不是在没有额外协议对其进行封装的情况下。这意味着 Netatalk 打印机共享不会受到外部来源的黑客攻击。另一方面，Netatalk 打印机共享不需要用户名或密码，因此在本地控制对打印机的访问是困难的。此外，如果你打印非常大的文件，像 UNIX 风格的 `lpd` 打印这样的基于 TCP/IP 的协议可能比 PAP 共享更快。

#### Note

诸如 `lpr` 和 `DAVE` 之类的程序允许 Macintosh 使用非 Macintosh 打印机协议进行打印，例如 `lpd` 和 SMB/CIFS。

## 理解 PPD 文件

根据你与谁交谈，PPD 代表 PostScript 打印机描述或打印机页面描述。过去，PPD 文件被称为打印机描述文件（PDFs），但当 Adobe 发布其便携式文档格式（PDF；也称为 Acrobat）文件时，使用 PDF 指代打印机描述文件变得过于混乱。

无论全称如何，PPD 文件都包含有关打印机确切功能的信息，例如其分辨率、是否为彩色打印机以及包含哪些字体。这些信息使 Macintosh 打印机驱动程序能够为打印机提供合理的选项，并生成不应过度负担打印机的输出——例如，在只能处理 8.5"×11" 纸张的打印机上不要使用 11"×17" 页面描述。

你必须在 Macintosh 和 Linux Netatalk 服务器上都指定一个 PPD 文件。最好在连接的两端使用相同的文件。我遇到过 PPD 文件不匹配导致打印失败的情况。同样，在两台计算机上选择错误的 PPD 文件也可能导致打印失败。

那么，你可以在哪里找到正确的 PPD 文件呢？一个答案是向你的打印机制造商查询。如果打印机是 PostScript 型号，或具有 PostScript 选项——即使是用于基于主机的 PostScript 解释器——制造商应该有该打印机的 PPD 文件。另一个选择是检查 `http://www.adobe.com/prodindex/printerdrivers/macppd.html` 上的 PPD 文件。

#### NOTE

这是 Adobe 网站上 Macintosh PPD 的 URL。这是因为 Macintosh PPD 文件包含创建者和类型信息以及 Macintosh 使用文件所需的资源分支数据。Netatalk  however 可以使用 PPD 的数据分支部分。因此最好在 Macintosh 上获取 PPD 文件并使用 Macintosh 实用程序提取它们。然后你可以使用 Netatalk 将文件复制到 Linux 并将其移动到 Netatalk 配置的方便位置，如本章后面“准备 PPD 文件”中所述。

Adobe 的 Windows PostScript 驱动程序也使用 PPD 文件，因此你通常可以找到 Windows PPD 文件。我建议在整个过程中使用 Macintosh PPD 文件以保持一致性，但你可能会发现在使用 Linux 时使用 Windows 文件，在 Macintosh 上使用 Macintosh 文件在某些情况下效果很好。

不过应该使用哪个 PPD 文件呢？如果你使用的是 PostScript 打印机，尝试为你的型号找到 PPD 文件。如果你使用的是由 Ghostscript 驱动的非 PostScript 打印机，我建议你尝试一些简单的。Apple LaserWriter PPD 通常与 Ghostscript 配合良好，而且还有一个额外的优点，即随 MacOS 一起提供，因此你不必四处寻找。我曾使用适用于 Hewlett Packard DeskJet 1200C 和 QMS magicolor 2 的 PPD 文件与彩色喷墨打印机配合使用，效果相当不错。

#### NOTE

一些 PPD 文件有一种奇怪的效果，即打印出来的页面是倒置的。（页面完全可读；只是先打印底部而不是通常的先打印顶部。）如果你在信笺纸上打印，这种特殊情况可能很重要。倒置打印如果你的意图是使用 Macintosh “打印”到磁盘文件并从 PostScript 文件生成 Adobe Acrobat PDF 文件，也可能是一个严重问题。如果倒置打印是一个问题，你可能需要尝试多个 PPD 文件，直到找到一个能产生可接受结果的文件。

## 设置远程访问

配置 Netatalk 以导出 Linux 打印机涉及编辑单个文件，但你可能需要找到其他文件来使 Netatalk 本身正常工作，并可能调试问题。如果一切顺利，你可能很快就能从联网的 Macintosh 打印机打印。如果不顺利，你可能会发现自己深入研究 PPD 文件和 Ghostscript 的奥秘。

> Tip
> 
> 在开始配置 Netatalk 进行打印之前，请确保你能从 Linux 打印 PostScript 文件。如果你使用的是 Red Hat 或 Mandrake Linux 系统，可以使用 `printtool` 来测试打印队列打印 PostScript 文件的能力，如第 14 章“准备共享打印机”中所述。如果你使用的是其他 Linux 发行版，请尝试使用 `lpr` 命令打印 PostScript 测试文件，例如 Ghostscript 示例目录中的文件（在 Red Hat 6.0 系统上为 `/usr/share/ghostscript/5.10/examples/`）。如果无法从 Linux 计算机本身打印 PostScript，那么从 Macintosh 打印的可能性也不大。

## 准备 PPD 文件

如本章前面所述，在你能够从 Macintosh 打印之前，必须找到 PPD 文件。由于你很可能有一台连接到与 Linux 机器相同网络的 Macintosh，因此你应该能够毫无问题地从你找到的任何来源在 Macintosh 上提取 PPD 文件。然后你可以将文件传输到 Linux 计算机。最终，你希望 PPD 文件位于一个方便的目录中。我喜欢使用 `/etc/atalk/ppds`，但如果你愿意也可以选择其他位置。不过现在不要复制该文件，因为你可能首先需要转换文件的换行符。

如果在不调整换行符的情况下复制 PPD 文件，你的打印机可能无法正常工作。幸运的是，一对简单的实用程序可以帮助进行此转换：`unix2mac` 和 `mac2unix`。你可以从随本书附带的 CD-ROM 上的 `sans-extras/unix2mac` 目录安装它们。你可以将这些文件复制到硬盘路径上的位置，例如 `/usr/local/bin`。如果你愿意，也可以从源代码重新编译这些实用程序，源代码位于书籍 CD-ROM 上的 `sans-extras/unix2mac/source` 目录中。

你可以通过键入其名称、输入文件名和输出文件名来调用任一实用程序。例如，你可能会使用以下命令：
