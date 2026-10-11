

然而，目前 CUPS 驱动程序仅支持 Windows NT、2000 和 XP。如果你需要支持 Windows 95、98 和 Me 客户端，还需要获取相应的 Adobe 驱动程序部分。

## 21.10.2 为 cupsaddsmb 准备 smb.conf

在运行 **cupsaddsmb** 之前，你需要按照示例 21.10.1 中所示设置 `smb.conf` 中的配置。

### 示例 21.10.1 用于 cupsaddsmb 的 smb.conf

```text
[global]
    load printers = yes
    printing = cups
    printcap name = cups
[printers]
    comment = All Printers
    path = /var/spool/samba
    browseable = no
    public = yes
# 设置取决于你的需求
    guest ok = yes
    writable = no
    printable = yes
    printer admin = root
[print$]
    comment = Printer Drivers
    path = /etc/samba/drivers
    browseable = yes
    guest ok = no
    read only = yes
    write list = root
```

## 21.10.3 CUPS “Windows NT/200x/XP 的 PostScript 驱动程序”

CUPS 用户可以从 `http://www.cups.org/software.html` 获取完全相同的软件包。它是基于 CUPS 的软件文件的独立软件包，标记为 CUPS 1.1.x Windows NT/200x/XP Samba 打印机驱动程序 (tar.gz, 192k)。需要下载的文件名为 `cups-samba-1.1.x.tar.gz`。解压和解压后，将显示以下文件：

```bash
root$ tar xvfz cups-samba-1.1.19.tar.gz
cups-samba.install
cups-samba.license
cups-samba.readme
cups-samba.remove
cups-samba.ss
```

这些文件是使用 ESP 元打包软件 EPM 打包的。`*.install` 和 `*.remove` 文件是简单的 shell 脚本，它们解开 `*.ss`（`*.ss` 只不过是一个 tar 归档文件，也可以用 "tar" 解开）。然后将内容放入 `/usr/share/cups/drivers/`。这些内容包含三个文件：

```bash
root# tar tv cups-samba.ss
cupadrvr.dll
cupsui.dll
cups.hlp
```

`cups-samba.install` shell 脚本很容易处理：

```bash
root# ./cups-samba.install
[...]
Installing software...
Updating file permissions...
Running post-install commands...
Installation is complete.
```

该脚本应将驱动程序文件自动放入 `/usr/share/cups/drivers/` 目录中：

```bash
root# cp /usr/share/drivers/cups.hlp /usr/share/cups/drivers/
```

> **警告**
>
> 由于一个 bug，最近的某个 CUPS 版本将 `cups.hlp` 驱动程序文件放置到了 `/usr/share/drivers/` 而不是 `/usr/share/cups/drivers/`。为了解决这个问题，请手动复制/移动该文件（在运行 `./cups-samba.install` 脚本后）到正确的位置。

这个新的 CUPS PostScript 驱动程序目前仅提供二进制形式，但免费使用。尚未提供完整的源代码。原因是它是借助 Microsoft DDK 开发并使用 Microsoft Visual Studio 6 编译的。驱动程序开发人员不允许将整个源代码作为自由软件分发。然而，CUPS 开发人员在 GPL 下发布了源代码的“差异部分”，因此任何拥有 Visual Studio 和 DDK 许可证的人都可以自行编译。

## 21.10.4 识别不同的驱动程序文件

CUPS 驱动程序不支持旧的 Windows 95/98/Me，仅支持 Windows NT/2000/XP 客户端。

Windows NT、2000 和 XP 由以下文件支持：

- cups.hlp
- cupadrvr.dll
- cupsui.dll

Adobe 驱动程序也适用于旧的 Windows 95/98/Me 以及 Windows NT/2000/XP 客户端。不同平台的文件集是不同的。

Windows 95、98 和 ME 由以下文件支持：

- ADFONT5.MFM
- ADOBEPS4.DRV
- ADOBEPS4.HLP
- DEFFPRTR2.PPD
- ICONLIB.DLL
- PSMON.DLL

Windows NT、2000 和 XP 由以下文件支持：

- ADOBEPS5.DLL
- ADOBEPSU.DLL
- ADOBEPSU.HLP

![](img/86d74c6cc862465e3a42e6dc3c90935a_442_0.png)

如果服务器上当前同时安装了支持 Windows NT/200x/XP 的 Adobe 驱动程序文件和 CUPS 驱动程序文件，Adobe 文件将被忽略，而会使用 CUPS 文件。如果你出于任何原因更喜欢仅使用 Adobe 驱动程序，请移开这三个 CUPS 驱动程序文件。Windows 9x/Me 客户端在任何情况下都使用 Adobe 驱动程序。

## 21.10.5 获取 Adobe 驱动程序文件

对于许多用户来说，获取 Adobe 驱动程序文件似乎意外地困难。它们不作为单个文件在 Adobe 网站上提供，自解压和/或自安装的 `Windows-.exe` 也不容易找到。你可能需要使用附带的原生安装程序并在某个客户端上运行一次安装过程。这将在客户端本地安装驱动程序（和一个通用的 PostScript 打印机）。安装完成后，共享该通用 PostScript 打印机。之后，客户端的 *`/print$`* 共享将包含 Adobe 文件，你可以从 CUPS 主机使用 smbclient 获取这些文件。

## 21.10.6 ESP Print Pro Windows NT/200x/XP PostScript 驱动程序

ESP Print Pro 软件用户可以安装 ESP 打印驱动程序包作为 Adobe PostScript 驱动程序的替代方案。为此，请从 Easy Software 网站上的 ESP Print Pro 软件的常规下载区域获取驱动程序文件。你需要在 **Download Printer Drivers for ESP Print Pro 4.x** 区域中找到标记为 “SAMBA” 的链接并下载该包。安装完成后，你可以通过在打印机管理器 GUI 中高亮显示打印机并从菜单中选择 **Export Driver...** 来准备任何驱动程序。当然，你需要事先配置好 Samba 以处理驱动程序文件；也就是说，设置 *`/print$`* 共享等。ESP Print Pro 软件包还包括 CUPS 驱动程序文件以及一套（许可的）用于 Windows 95/98/Me 客户端系列的 Adobe 驱动程序。

## 21.10.7 需要考虑的注意事项

一旦你运行了安装脚本（并可能手动将 `cups.hlp` 文件移动到 `/usr/share/cups/drivers/`），驱动程序即可放入 Samba 的 *`/print$`* 共享（该共享通常映射到 `/etc/samba/drivers/`，并包含具有 **WIN40** 和 **W32X86** 分支的子目录树）。你通过运行 **cupsaddsmb** 来完成此操作（另请参阅自 1.1.16 版本起 CUPS 的 **man cupsaddsmb**）。

![](img/86d74c6cc862465e3a42e6dc3c90935a_443_0.png)

**提示**
你可能需要通过运行 **smbpasswd** 将 root 添加到 `smbpasswd` 文件中：如果你第一次执行整个流程并且不在一个已配置 *单点登录* 到 Windows 域控制器的环境中工作，这一点尤为重要。

一旦驱动程序文件位于 *`/print$`* 共享中并进行了初始化，Windows NT/200x/XP 客户端就可以下载并安装它们了。

<http://www.easyws.com/software.html>

> **注意**
>
> Win 9x/Me 客户端不能与 CUPS PostScript 驱动程序一起工作。对于这些客户端，你仍然需要使用之前提到的 ADOBE*.\* 驱动程序。

> **注意**
>
> 如果你在 /usr/share/cups/drivers/ 目录中仍保留有之前安装的 ADOBE*.\* 驱动程序文件，这不会造成危害。新的 cupsaddsmb（自 1.1.16 版本起）如果同时发现两者，会自动优先使用它自己的驱动程序。

> **注意**
>
> 如果你的 Windows 客户端已经安装了用于 Adobe PostScript 驱动程序的旧 ADOBE*.\* 文件，那么新 CUPS PostScript 驱动程序针对 Windows NT/200x/XP 的下载和安装最初会失败。你需要先清除客户端上的旧驱动程序。仅仅“删除”打印机是不够的，因为驱动程序文件仍会被客户端保留，并如果你在尝试重新安装打印机时会被重新使用。为了真正清除客户端上的 Adobe 驱动程序文件，请打开打印机文件夹（可能通过 开始 -> 设置 -> 控制面板 -> 打印机），右键单击文件夹背景，并选择服务器属性。当新对话框打开时，选择驱动程序选项卡。在列表中选择一个要删除的驱动程序并单击删除按钮。只有在该驱动程序没有留下任何使用它的打印机的情况下，这才能生效。你需要先删除打印机文件夹中所有使用此驱动程序的打印机。你需要管理员权限才能执行此操作。

