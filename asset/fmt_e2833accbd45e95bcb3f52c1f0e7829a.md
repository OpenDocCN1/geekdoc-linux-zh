
关于文件共享，SAMBA 是解决方案的关键部分。由于 Windows 系统并不特别喜欢使用外来协议，因此翻译的负担主要落在 Unix 系统的身上，通过 SAMBA 实现。

你将看到如何管理 Linux 主机系统中供 Windows 客户端打印机。接下来是一个在 Windows 主机上执行此操作的简要示例。最后，你将看到如何通过 Unix 客户端系统安装 SAMBA 来使用这些共享。

注意：由于在 Unix 客户端上使用 SMB 共享，如果你的系统没有自带 SAMBA，你需要获取并安装它；VMware Workstation 不包含它。

# 10.5.1 配置 SAMBA 打印机共享 (Linux)

本节将告诉你如何从 Linux 主机系统共享打印机供 Windows 客户端使用。当你按照第 10.1 节所述通过 `smb-conf.pl` 配置 SAMBA 时，生成的配置已经包含了对打印机共享的支持。具体来说，你的 `smb.conf` 文件中的 `[printers]` 部分所示：

```
[printers]
comment = All printers
path = /var/lpd
browable = no
guest = no
writable = no
printable = yes
```

由于 Unix 安装中的打印机配置差异巨大，你可能需要更改上述行中 `smb.conf` 文件的几处。你可能需要更改的第一项是 `path` 参数，它指定了在 spbd 将文件发送到打印机打印系统之前，中间文件（缓存文件）存放的位置。

由于 Unix 打印程序需要对该缓存目录的写权限，大多数打印系统将此目录设置为 world可写，以便所有进程都能访问它。然而，你的系统上可能不存在 `/var/lpd`，导致其变得不可写。因此，如果前者不起，可以将 `/var/lpd` 更改为 `/tmp`。

## 特定打印机的设置

你可能希望更改某个特定打印机的选项以获得更精细的控制。你可以像这样在 `smb.conf` 文件中为打印机指定设置：

```
[someprinter]
comment = one particular printer
printer name = someprinter
path=/var/spool/lpd/someprinter
guest ok = yes
browable = yes
printable = yes
printer driver = HP LaserJet 4M
```

这里的参数区分了共享目录和非共享目录是否可打印。`smb.conf` 中的所有打印机共享条目必须将此选项设置为 `yes`。将 `guest ok` 和 `browseable` 参数设置为你喜欢的任何值。注意，此示例包含了可选的 `printer driver` 参数：如果 Windows 客户端能够将此字符串与它已知的打印机驱动程序匹配，当你设置网络打印机时，它会自动选择驱动程序。

## 打印子系统

Linux 有多个打印子系统。常用的有三种：Berkeley LPD、`LPRng` 和 PLP。为了让 Windows 客户端操作系统能够正常打印，你必须告诉 SAMBA 使用哪一个。你 `smb.conf` 文件中的 `print` 参数用于选择打印系统。此示例指定了 LPRng：

```
printing = LPRng
```

对于 PLP，请使用 PLP 代替 LPRng。默认使用 Berkeley LPD。

## 登录和密码要求

VMware 的 `smb.conf` 文件通过设置 `guest ok no` 规定只有拥有登录和密码的用户才能打印。如果你打印频繁，这可能会很麻烦，你可以通过以下命令进行更改：

```
guest ok = true
guest only = true
```

## Windows 客户端打印机驱动程序

在你的 Windows 客户端系统中，你应该将打印机驱动程序设置为支持 PostScript 的激光打印机，无论你的主机系统实际连接的是什么种打印机。HP LaserJet 5M (PS) 和 Apple LaserWriter IIINTX 是两个可以驱动程序。

其原因是 Linux 打印服务器期望看到 PostScript 输入，因为大多数 Unix 程序都会产生 PostScript 输出。即使你的打印机不理解 PostScript，你的打印系统也可能会产生你的打印机可以理解的 PostScript 输入。

# 10.6 Windows 主机打印机共享

如果你的主机操作系统是 Windows，你可以通过 SMB 共享获取网络打印机访问。此服务包含在所有基于 Windows NT 的系统中。

在 Windows NT、2000 和 XP 下共享打印机，请遵循以下步骤：

- 1. 从设置子菜单打开“打印机”文件夹。
- 2. 右键点击你想要共享的打印机并从菜单中选择“属性”。出现打印机属性窗口。
- 3. 点击“共享”选项卡并选择“共享”选项。
- 4. 如需限制对打印机的访问，请使用“安全”选项卡。
- 5. 点击“确定”。

# 第 10 章：网络服务

为了让打印机共享生效，你的 Windows 主机上必须有一个活动的 Server 服务。

# 10.7 Unix 打印

接下来的几节描述了如何通过 VMware 网络从客户端操作系统（Linux、FreeBSD、NetBSD 或 OpenBSD）打印。以下是关于 Unix 打印的几点基础：

- Unix 打印客户端发送 PostScript 输出。如果连接的打印机不支持 PostScript，Unix 打印子系统会将其从 PostScript 翻译为该打印机理解的任何格式。
- Unix 打印系统守护进程是 `lpd`。然而，有三种 LPD 版本：Berkeley LPD、`LPRng` 和 PLP。书中的示例兼容这三种。
- Unix 系统上的主打印配置文件是 `/etc/printcap`。
- 一致性不是 Unix 打印的优势。

## 10.7.1 从 Unix 客户端打印到 Unix 主机

让 Unix 客户端系统将打印作业发送到 Unix 主机相当：

- 1. 设置客户端系统的 `/etc/printcap` 文件。此示例假设使用主机主机网络或 NAT 网络，主机 IP 为 `172.16.144.1`。主机上的打印机名称为 `myprinter`。

```
lp|host|hostprinter:Host System Printer:\n:lp=-d=/var/ spool/lpd/host:\n:mx0=rm=172.16.144.1:rp=myprinter:
```

- 2. 在客户端创建一个名为 `/var/spool/lpd/host` 的缓存目录，并确保打印进程（通常以 daemon 用户运行）可以写入该目录。
- 3. 在主机系统的 `/etc/hosts.lp` 文件中添加客户端主机名或 IP 地址。

## 10.7.2 从 Unix 客户端打印到 Windows 主机

遗憾的是，从 Unix 客户端打印到 Windows 主机可能困难。你必须克服两个障碍：需要通过 SMB 发送打印作业，以及可能需要在目标打印机的语言中处理 PostScript 文件。如果你能通过并行端口连接到主机的打印机并对其进行配置，情况会变得简单。发送作业是容易的。要这样做，你需要 SAMBA 以及第 10.4 节描述的 `sambclient` 程序。发送作业，使用如下命令：

```
smbclient '\\SERVER\PRINTER' password -U user -N
```

在这里，`SERVER` 是服务器（在这种情况下），`PRINTER` 是打印机名称，`user` 和 `password` 是你的用户名和密码，`file` 是你想打印的文件。

如果你的打印机操作系统理解 PostScript，这就是你所需要的。最简单的方法是创建一个运行上述命令的脚本，然后使用它。注意：如果你的打印机不支持 PostScript，你可以测试通过 VMware 网络向主机发送作业。在主机系统上，将文档打印到文件而不是打印机。

## 处理打印驱动程序

如果你的打印机不支持 PostScript，那么如果你想从 Unix 客户端通过网络到 Windows 主机，你需要配置正确的打印驱动程序。驱动程序将化 PostScript 信息，这意味着作业中的 PostScript 代码将生成位图图像发送到打印机。

`Ghostscript` 是将 PostScript 输入转换为其他类型打印机理解的标准 Unix 程序。`Ghostscript` 几乎带有所有的 Linux 发行版；其可执行文件为 `gs`。你所需要是在运行 `sambclient` 之前在管道中插入 `gs` 命令。困难的部分是获取适用于打印机的正确参数。关于 `Ghostscript` 的完整指南超本书的范围，但这里有一些提示。你需要从标准输入使用 PostScript 文件并将渲染后的结果输出到标准输出。有两种主要的驱动样式。实用方法如下：这里是你想打印的 PostScript 文件，`args` 是上一节的 `sambclient` 参数。因为这是一个很复杂的命令，如果你需要使用它，应该将其放在脚本中——例如：
