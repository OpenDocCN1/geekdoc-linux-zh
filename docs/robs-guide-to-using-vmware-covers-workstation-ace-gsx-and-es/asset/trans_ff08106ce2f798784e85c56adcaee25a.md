
2. 在 Norton Ghost 2003 中，选择 Ghost Utilities 并点击 Norton Ghost Boot Wizard

![](img/25fe75b93b97a021effaba85db112a52_190_0.png)

图 16.1：使用 Norton Ghost Boot Wizard 创建启动软盘。

3. 在 Norton Ghost Boot Wizard 中，选择 Peer-to-Peer Network Boot Disk。

4. 在 Network Interface Cards 列表中，选择 AMD PCNet Family 适配器并点击 Next。

![](img/25fe75b93b97a021effaba85db112a52_190_1.png)

图 16.2：为您的计算机选择正确的网络适配器，或在虚拟机中使用时选择 AMD PCNet 适配器。

5. 在下一个屏幕中，选择要使用的 DOS 版本。只需选择默认列出的 PC-DOS 即可。

6. 向导现在会要求您输入 GHOST.EXE 文件的位置。您还可以在此处指定额外的参数，这些参数将在 Ghost 启动时使用。您可以指定 -TCPS 参数，该参数会自动启动 TCP/IP Peer-to-Peer 会话。

7. 在 Network Settings 屏幕中，输入 IP 地址或保留默认设置以使用 DHCP。

8. 您现在可以指定磁盘的位置。如有需要，格式化软盘。

9. 您现在可以查看 Summary 屏幕。如果一切正常，可以点击 Next 创建启动软盘。向导完成后，关闭 Ghost 并继续映像过程。

![](img/25fe75b93b97a021effaba85db112a52_191_0.png)

图 16.3：添加 -TCPS 参数以自动启动 Peer-to-Peer 会话。

此时您已使用 Ghost 启动文件创建了物理软盘或虚拟软盘映像。您需要将此软盘分配给将作为点对点映像操作的从机的虚拟机。下一步是准备您的主机 PC 并开始映像操作。

## 16.2 启动主计算机

您希望映像到虚拟机的当前操作系统的计算机，可以使用上一段中创建的同类软盘启动。与您的从机软盘的不同之处在于，您的主机 PC 很可能具有不同的网络适配器。然而，您也可以在不创建启动软盘的情况下自动启动 Ghost。您可以通过从 Ghost Advanced Menu 选项中选择 Peer-to-Peer 来实现此操作。

![](img/25fe75b93b97a021effaba85db112a52_192_0.png)

图 16.4：可以在没有软盘的情况下为主机计算机启动 Ghost。

您需要提供的信息与创建从机启动磁盘时使用信息相似。因此，我假设您不需要任何额外说明。

提示：如果您的网络适配器未自动检测到且未列出，您可以从 Network Interface Card 选择屏幕为您的 NIC 添加驱动程序。请确保下载网络卡的 NDIS2 驱动程序以将其添加到列表中。另外，在添加自定义驱动程序时，请确保将 PROTOCOL.INI 的正确参数输入到参数窗口中。

## 16.3 执行映像操作

当您将主机 PC 重启到 Ghost，并且使用 Ghost 启动磁盘启动了 VMware 客户机时，您可以开始点对点会话。如果 TCP/IP 协议栈成功初始化，点对点菜单选项将可用。选择 Peer-to-peer → TCP/IP → Slave 以在从机计算机上启动会话。

![](img/25fe75b93b97a021effaba85db112a52_193_0.png)

图 16.5：在从机计算机上启动 Peer-to-Peer 操作。

从机会开始连接到主机。在 Slave Connect 屏幕中，会显示此从机的 TCP/IP 地址。您必须在主机计算机中指定此地址。

![](img/25fe75b93b97a021effaba85db112a52_193_1.png)

图 16.6：从机会显示一条消息，其中包含要在主机中指定的 IP 地址。

在主机计算机上，选择 Peer-to-peer → TCP/IP → Master 以启动映像会话。系统会要求您输入从机的 IP 地址。当主机连接到从机时，从机计算机将显示一条已连接的消息。主机将返回到原始菜单，您可以在其中选择映像操作（disk to disk，或单个分区）。最简单的转换可以通过选择 disk-to-disk 选项来实现，以将整个 PC 复制到虚拟机中。但是，您也可以在分区级别执行此操作。

## 接下来的步骤

根据您正在恢复的操作系统，您可能需要修改驱动程序等。详细说明见第 21 章：“Modify your restored operating system to work with VMware”。

## 17 其他点对点或多播网络解决方案

Norton Ghost 是一款广泛可用的映像工具，我已在上一章中选择讨论此主题。还有其他产品，我想简要提及。

### Portlock Storage Manager

该应用程序在 NetWare 环境中经常使用，但功能多样。Storage Manager 支持 NetWare 的 NSS 文件系统，但也支持 FAT、NTFS、EXT2、EXT3 和 ReiserFS。该应用程序支持从硬盘和可移动媒体（如可写 CD 和 DVD）进行本地映像操作，以及通过 TCP/IP 网络进行网络映像操作。

对于 NetWare 环境，这是最佳工具，因为它支持 NSS 文件系统，这使其能够映像服务器上的特定卷。另一个好处是它使用 NetWare 的常规 LAN 和存储驱动程序，因为该应用程序作为 NLM 运行。对于您的虚拟机目标，您必须使用带有 NetWare TCP/IP 协议栈的 DOS 软盘。可在以下位置下载带有 DOS、LAN 驱动程序和 TCP/IP 协议栈的虚拟软盘：www.robbastiaansen.nl。

有关 Portlock Storage Manager 的更多信息，请访问：www.portlocksoftware.com

### Novell ZENworks imaging

许多拥有 Novell NetWare 环境的用户也拥有 Novell ZENworks for desktop 产品。它包含一个支持 Windows 文件系统的映像组件。它可用于与映像服务器之间的映像操作，但您也可以通过将一台工作站设置为多播主机，另一台设置为多播从机来进行点对点映像。

### Altiris Client Management Suite

该管理套件非常流行于工作站管理，也包含点对点映像功能。

## 18 通过网络使用 Acronis True Image 基于文件的映像

上一章中描述的 Symantec Ghost 点对点选项是最容易使用的，因为它直接将映像发送到另一台计算机。此解决方案并不总是有效，要么是因为 Ghost 的限制，我已在点对点部分中解释过，要么是因为网络带宽的限制。然而，您可以使用 Acronis True Image 将映像文件直接存储在服务器卷或另一台 PC 上。这允许您从该位置恢复该映像文件，或将映像复制到其他位置。这种方法的一个优点是您可以多次使用映像文件，而点对点映像操作是一次性操作。

我决定使用 Acronis 的 True Image 软件，因为该软件可以在 Windows 中创建映像，并且还提供非常强大的恢复 CD。

注意：对于 Windows Server 产品，您需要 Acronis True Image 的服务器版本。服务器版本比普通工作站版本更昂贵。不仅仅是 Acronis 有特殊的服务器版本。Symantec 也销售其 DriveImage 软件的特定服务器版本。对于 Linux，如果您想在运行的 Linux 机器上运行映像软件，则需要 True Image Server for Linux 软件。使用恢复 CD，您可以在使用该 CD 重启机器时创建任何机器的映像。

使用 True Image 创建映像有两种方法。第一种是在 Windows 或 Linux 环境中安装完整的 Acronis 应用程序。第二种是使用 True Image 救援 CD 启动机器，以便从常规操作系统之外执行操作。

当您使用第一个选项时，您实际上是从正在运行的操作系统创建映像。这与迄今为止所有其他映像方法相矛盾，在这些方法中，我们需要创建操作系统已关闭的机器的映像。那么，在运行的服务器上执行映像操作安全吗？

我添加了以下来自 Acronis 支持页面的文字，以阐明此问题：

> 我在服务器上运行着 Microsoft SQL Server、Oracle 或 Microsoft Exchange 等复杂应用程序。我计划创建映像，但不确定这些应用程序在映像过程中是否可以运行。我该怎么办？
