

[hpdj]
path = /var/spool/samba
user = lucille, ricky
print ok = Yes

[lexmark]
path = /var/spool/samba
user = larry, lucille
print ok = Yes

在此配置中，只有 larry、moe 和 curly 可以使用打印机 canon，而只有 lucille 和 ricky 可以使用打印机 hpdj。lexmark 打印机则可由可以访问另外两台打印机中的每一台的两个用户访问，即 larry 和 lucille。正如你所见，共享级安全性在控制对特定打印机的访问能力方面极其灵活。另一方面，它也相当难以维护，因为随着网络上的用户发生变化，你必须频繁地在多个共享中添加和删除用户。这种访问方式还会减慢身份验证速度，特别是当共享的用户很多时，因为 Linux 在此方案中通过将提供的密码逐一与共享的授权用户进行比对来验证用户。

另一种应用共享级安全性的方式是为每个共享或一组共享创建特殊的 Linux 账户，然后将该账户的密码分发给需要访问相关共享的每个人。当然，这意味着单个密码将被广泛知晓，因此你必须格外谨慎地控制该账户在除其预期共享之外的其他方面的可访问性。（例如，黑客如果获知了密码和账户名，可能会通过 telnet 登录并尝试进一步捣乱。）更改密码也可能成为噩梦，因为你随后需要通知数个人密码已更改。

## 使用 Linux /etc/printcap 组控制

第 15 章“与其它 UNIX 系统共享打印机”描述了一种基于 Linux 组 membership 的打印机访问控制方法。具体来说，你可以在打印机 /etc/printcap 条目中添加一行，类似于以下内容：

:rg=layout:\

有效地限制对打印机的访问。事实上，你可以用这种方式为前面示例中的 canon、hpdj 和 lexmark 打印机实现完全相同的控制，这些打印机由 larry、moe、curly、lucille 和 ricky 使用。

## 使用 hosts allow 和 hosts deny 参数

你可以在单个共享的定义中使用 hosts allow 和 hosts deny 参数，按客户端控制对打印机的访问。例如，假设你的 Linux 计算机托管三台共享的打印机。打印机 hp4000 应可供你内部网上的所有计算机访问，而 epson1520 仅应可供艺术部门访问，okidata 仅应可供前台工作人员访问。如果艺术部门的计算机全部具有 192.168.5.x 范围的地址，而前台工作人员的计算机全部位于 192.168.7.x 范围内，那么你可以这样做：

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

### NOTE

> 此配置假定 192.168.5.x 范围内的所有计算机都属于艺术部门，并且 192.168.7.x 范围内的所有计算机都在前台。如果不是这样，你可以使用更复杂的 hosts allow 语句，例如添加 EXCEPT 子句以排除特定主机，如 hosts allow = 192.168.7. EXCEPT gingko

有关如何在 hosts allow 和 hosts deny 中指定计算机的详细信息，请参见第 11 章。

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

- 在 /etc/smb.conf 中为相关共享设置 postscript = true 选项。

