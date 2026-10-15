

将你的网络连接到 Internet。如果你使用 NetBEUI，这个问题也会减少，因为 NetBEUI 无法通过 TCP/IP 路由器。如果您担心这些问题，您应该咨询您组织的网络人员或您的 ISP，以确定您的计算机如何连接到 Internet。

## SMB 协议

在 Windows 网络协议的顶层，控制着一切的是 *Server Message Block*（SMB）协议，该协议已被重新命名为 *Common Internet File System*（CIFS）。事实上，Samba 的名称就源于 SMB 的缩写。图 11.2 显示了 SMB、NetBIOS、NetBEUI、IPX 和 TCP/IP 之间的关系。

![](img/5d4d3092919d1d16884788127447cc6d_280_0.png)

**图 11.2**
*Samba 仅支持通过 TCP/IP 的 SMB，尽管 Windows 也支持通过 NetBEUI 和 IPX 的 SMB。*

NetBIOS 提供基本功能——事实上，NetBIOS 中的 B 代表 basic。SMB 提供更高级别的工具。这类似于控制硬盘的驱动程序或 BIOS 与磁盘文件系统之间的关系。SMB 就像 UNIX 的 Network Filesystem（NFS）一样，是用于网络的文件系统。然而，与硬盘的 BIOS 不同，在 Windows 文件共享的情况下，NetBIOS 之下还有另一层协议——即 Samba 的情况为 TCP/IP。

## 何时使用 Samba

NetBIOS 和 SMB/CIFS 是为 DOS 的网络以及后来的 Windows 和 OS/2 而设计的。这些协议为 DOS、Windows 和 OS/2 程序期望文件系统提供的特定功能提供支持。其他网络协议，如 NFS，则支持不同的功能集。因此，当客户端操作系统为 DOS、Windows 或 OS/2 时，使用 SMB/CIFS 是最佳选择。

请注意，使用 Samba 在 Linux 上意味着 Samba 必须将 SMB 支持的文件系统功能转换为 Linux 可以处理的形式。基本功能，如文件读写，并不是问题；诸如隐藏属性等功能，Linux 不支持，具体取决于 Samba 的配置，可能会导致困难。在大多数情况下，Samba 已经克服了这些困难，因此 Samba 服务器可以相当无缝地集成到

现有的 Windows 网络中。事实上，如果您小心地正确配置系统，您可以用运行 Samba 的 Linux 计算机替换 Windows 服务器，而您的用户可能根本察觉不到区别！

由于 SMB 不提供 UNIX 计算机期望的权限或所有权信息，而 NFS 提供了这些信息，因此通常最好不要使用 Samba 在 Linux 或 UNIX 计算机之间进行文件共享。您可能在某些有限的情况下这样做，例如当您只需要提供对用户数据文件的访问，而不是程序文件，或者如果用户需要快速访问远程文件，这些文件通常不需要从 Linux 访问，但需要从 Windows 访问。作为一般规则，我建议仅在您有令人信服的理由这样做时才使用 Samba 与 Linux 或 UNIX 客户端进行文件共享，例如希望限制服务器支持的文件共享协议数量。

同样，Macintosh 希望其文件系统支持某些独特功能，例如存在独立的资源和数据分支。Samba 不支持此功能，Macintosh 的 SMB/CIFS 软件，例如 Thursby 的 DAVE，必须模拟它。DAVE 也是收费的，而 Linux 的 Netatalk AppleTalk 服务器包是免费的，因此不使用 Samba 与 Macintosh 有经济激励。另一方面，Samba 比 Netatalk 更完善，因此您可能会发现 Samba 和 DAVE 的组合在某些情况下更好。

## 设置 Samba 选项

在使用 Samba 提供文件服务之前，您必须配置该软件。随着您使用 Samba，您会发现它提供极其广泛的配置选项，使您能够比使用 Windows 服务器更精细地控制 Linux 服务器的行为。您需要花时间学习这些选项的作用。

> Tip
> 
> 当您创建 /etc/smb.conf Samba 配置文件时，您可能希望使用 testparm 实用程序。此程序检查文件是否包含任何明显的错误。尝试在 /etc/smb.conf 上运行它，然后在另一个不相关的文件上运行，例如 /etc/fstab。testparm 会为后者显示许多错误，但不应为前者显示。程序在进行测试后还会转储 /etc/smb.conf 文件服务的摘要，此摘要可能相当长。

