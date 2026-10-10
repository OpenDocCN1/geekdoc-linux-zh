
I/O 请求包 (`IRP`) 描述了对设备的 I/O 请求。它的许多字段在你完成本章节后面的实验时将变得重要。一些显著字段包括 `AssociatedIrp.SystemBuffer` 字段，它通常包含请求的输入和或输出缓冲区，以及 `Tail.Overlay.CurrentStackLocation` 字段，它包含与被调用设备相关的信息。当前位置 (`_IO_STACK_LOCATION`) 中的重要信息包括 `MajorFunction` 字段（它是当前请求的主函数）以及 `Parameters` 字段（这是一个巨大的联合体，根据调用的主函数包含不同的信息）。在 I/O 控制的情况下，`MajorFunction` 将是 `IRP_MJ_DEVICE_CONTROL` (14)，`Parameters` 字段将描述调用的 I/O 控制 (`IOCTL`) 代码以及输入输出缓冲区。对于大多数 `IOCTL` 调用，输入和或输出缓冲区位于 `_IRP` 的 `AssociatedIrp.SystemBuffer` 字段中。有关 `IOCTL` 代码的更多信息，请参 Windows 文档。

在本章的实验中，你将逆向工程并调试内核驱动程序，以定位其创建的设备，确定注册的主函数处理程序，学习如何从用户态调用主函数处理程序模式，并最终编写利用程序来执行本地权限提升 (`LPE`)。

## 内核调试

用户态（ring 3）调试器仅能够调试运行在内核之上的单个程序。调试内核则需要内核态（ring 0）调试器。内核调试通常在两个系统之间进行：一台系统运行调试器，另一个系统是被调试的系统。之所以需要两个系统，是因为与 ring 3 调试器中挂起单个程序不同，停止整个内核将导致你无法与系统进行交互以运行命令或恢复运行！有一个被称为“本地”内核调试的例外，它允许对当前运行的系统内核进行便利调试。内核调试的主要缺点是无法停止正在运行的系统，这意味着你无法设置或注入任何断点，无法在崩溃时进行调试，而且由于系统一直在运行，内存中的值可能会迅速变化。

Windows 唯一官方支持（因此也是推荐的）ring 0 调试器是 `WinDbg`，通常读音为 win-dee-bee-gee、wind-bag 或 win-dee-bug。它由微软开发并维护，作为开发工具包的一部分包含在。`WinDbg` 提供了多种不同的传输方式来调试内核。网络调试是内核调试中最可靠、最高效且一致的设置。可以通过安装 Windows SDK、WDK 或从微软商店下载 `WinDbg Preview` 来获取 `WinDbg`。较新的 `WinDbg Preview` 与 `WinDbg` 相同，但具有类似 Metro 的界面。本节的实验将使用 `WinDbg Preview`。如果你更偏好命令行，可以使用 `kd.exe` 连接到目标系统。它随 SDK 和 WDK 中的 `WinDbg` 一起。`WinDbg` 的所有变体都有 `DbgEng` 支持，`DbgEng` 成了 `WinDbg` 的核心功能。微软在 Windows SDK 中包含了与 `DbgEng` 交互的头文件和库，以便开发者能够编写使用支持 `WinDbg` 程序库的工具。

## 实验 14-1：设置内核调试

要开始，你需要两个 Windows 10 虚拟机以及你选择的虚拟化软件（`VMware`、`VirtualBox`、`Parallels` 等）。如果你有 Windows 11 的副本，也可以使用，因为过程和结果应该是相同的。如果你已经有了 Windows 许可证并设置好了虚拟机，那太好了！如果你没有微软提供的任何 Windows 10 ISO，可以使用 Windows 试用版，或者前往 Windows 开发者资源下载旧版的 Internet Explorer 开发虚拟机。请查看“延伸阅读”部分获取链接。在本文编写时，微软仍提供该镜像，尽管可能会发生变化！

![](img/0add480ffb73b6bc89b65d99f7d6b37a_498_0.png)

**注意**：这些虚拟机可以用于实验，但如果你打算将 Windows 作为你的操作系统使用或用于商业目的，则需要购买许可证。偷窃是不对的！

一旦你设置好了一个满意的 Windows 10 虚拟机，请创建一个完整克隆或链接克隆。一台虚拟机将作为调试机，你将在上面安装 `WinDbg`，另一台作为调试目标。可以从微软商店安装 `WinDbg Preview`，并从 Windows SDK 安装 `WinDbg Classic`。要安装 `WinDbg Classic`，请下载 Windows SDK 并在安装程序中选择“Windows 调试工具”。

在完成所有必要的安装后，在目标虚拟机的管理员 shell 中使用 `bcdedit` 启用网络内核调试：

```
PS C:\WINDOWS\system32 bcdedit.exe /debug on
操作已成功完成。
PS C:\WINDOWS\system32 bcdedit.exe /debugsettings hostip:1.1.1.1:port=50000
Key=jz2hly1bcrc.2j4zht8k2xwm.10xxohgb127k.2tm20duys53h5i
```

`hostip` 可以是你通过 `WinDbg Preview` 连接的任何内容，或者在 `WinDbg Classic` 连接字符串中指定目标变量；否则，将其设置为调试器虚拟机的 IP。将返回的密钥复制到你的调试机，因为你需要它进行远程连接。重启目标虚拟机进入调试模式。

通过进入 File | Attach to kernel 并在 Net 标签上输入所需信息连接 `WinDbg Preview`。对于 `WinDbg Classic` 或 `kd.exe`，在命令行使用 `-k` 标志并输入以下连接字符串，将括号中的值替换为你特定环境的值：

```
windbg.exe -k tcp:target=<target IP>,port=<target port>,key=<key> from bcdedit
```

如果连接成功，你应该会在位于内核地址（以 0xffffff 开头）的断点（int 3）处获得一个活动提示符。命令行也将处于活动状态。如果你无法连接，请检查目标的 IP 地址，确保两个虚拟机都能通过网络连接，并尝试关闭两台机器上的 Windows 防火墙。一旦连接成功，尽管尝试一些命令。`WinDbg` 初看起来非常让人眼花，但不要担心，通过练习会变得容易。

内核调试设置完成后，你现在准备好开始识别内核攻击的目标了！

## 选择目标

在所有漏洞研究中，最迫切且相关的问题之一是“我该如何选择目标？”虽然我们可能无法回答，但从尝试在内核本身寻找漏洞可能有些困难。一个更容易、更易上手的切入点是已知漏洞的驱动程序。如果你想进入内核利用领域，从哪里开始？从微软开发的驱动程序开始可能会令人沮丧。

在 8 月的 DEFCON 27 上，来自 Elysium Labs 的研究人员展示了许多带有漏洞的驱动程序，凸显了这个问题。在本文时，他们的列表中有39 个驱动程序允许任意虚拟和物理读写、任意读写执行内核内存分配以及任意模型特定寄存器（MSR）读写。这些功能本身并不是漏洞，因为特权应用程序如 BIOS 升级程序需要它们才能正常运行，但利用它们所需的访问才是关键。这些驱动程序可以从系统的用户模式访问。在某些情况下，即使是低或不可信完整级别的进程也可以调用它们。这意味着任何具有执行权限的人都可以将其权限提升到 SYSTEM。

2021年5月，Sentinel Labs 研究员 Kasif Dekel 发表了一篇文章，详细介绍了一个与 Elysium 驱动列表问题相似的广泛发布的 Dell 驱动程序。该驱动程序的有趣之处在于其范围——几乎400个平台受此问题影响。该驱动名为 `DBUtil_2.sys`，自2009以来一直包含在 Dell 和 Alienware 的更新工具中。它由 Dell 的第三方 SPC 签名，未经过或提交给微软。由于这是一个近期漏洞且范围如此大，它是学习内核利用的完美目标。

## 实验 14-2：获取目标驱动程序

Dell 的公告说漏洞影响“更新工具包，包括 BIOS 更新工具、Thunderbolt 更新工具、TPM 固件更新工具和扩展坞固件更新工具”。根据此，前往 Dell 网站开始查找可能受影响的更新。包含该驱动程序的更新之一是 Dell Latitude 7204 Rugged BIOS 更新 A16。在编写本文时，该更新是该系统的最新版本，且它仍然会将漏洞驱动程序写入磁盘。作为一个额外的练习，尝试寻找另一个包含该漏洞驱动程序的更新。如果你在此过程中发现了其他驱动程序，请保存它们以备后续进行逆向工程练习。上述更新程序和目标驱动程序的副本可以在书籍的 GitHub 仓库中找到。

在 Windows 系统上运行 BIOS 更新程序（或你选择的更新），并检查 `C:\Users\your user\AppData\Local\Temp` 下名为 `DBUtil_2_3.sys` 的文件。如果找不到该文件，请查看 `C:\Windows\Temp`。你也可以启动 Sysinternals Process Monitor 并设置过滤器“Path, Ends With, DBUtil_2_3.sys”，以便驱动程序何时写入磁盘或被调用。

## 实验 14-3：驱动程序的逆向工程
