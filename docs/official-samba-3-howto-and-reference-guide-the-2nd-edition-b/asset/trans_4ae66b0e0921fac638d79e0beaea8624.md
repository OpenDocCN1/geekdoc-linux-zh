

![](img/86d74c6cc862465e3a42e6dc3c90935a_445_0.png)

## 注意

一旦成功将 CUPS PostScript 驱动程序下载到客户端，您就可以按照第 20 章“经典打印支持”中所述的方法，轻松将所有打印机切换至此驱动程序。您可以运行打印机属性对话框来更改现有打印机的驱动程序，或者使用 `setdriver` 子命令配合 `rpcclient` 进行操作。

### 21.10.8 Windows CUPS PostScript 驱动程序与 Adobe 驱动程序的比较

您是否想了解 CUPS 和 Adobe PostScript 驱动程序之间的比较？就我们的用途而言，以下是在 CUPS 方面更有利的关键要点：

- 无需处理 Adobe 最终用户许可协议（EULA）。
- 无需担心“在哪里获取 ADOBE.* 驱动文件？”这一问题。
- Adobe 驱动程序（根据与其关联的打印机 PPD 的请求）经常在打印文件的主要 PostScript 部分之前添加 PJL 头部。因此，打印文件以 `<18>X-12345X` 或 `<escape><X-12345X` 开头，而不是 `%!PS`。这导致 CUPS 守护进程将传入文件自动识别为已准备好打印的文件，而不启动通过 `postscript` 过滤器的过程（从更技术的角度来说，它不被视为通用的 MIME 类型 `application/postscript`，而是被视为更特殊的 MIME 类型 `application/vnd.cups-postscript`），因此也导致 `/var/log/cups/page.log` 中的页面统计无法获取准确的页数：在标准设置中，记录的是虚假的页数“1”。
- Adobe 驱动程序有更多的选项来错误配置其生成的 PostScript（例如，无意中将其设置为“优化速度”而不是“优化可移植性”，这可能导致 CUPS 无法处理它）。
- 由 Windows 客户端发送到 CUPS 服务器的 CUPS PostScript 驱动程序输出，保证会自动识别为通用的 MIME 类型 `application/postscript`，从而通过 CUPS 的 `postscript` 过滤器，并在 `page.log` 中记录正确的页数用于统计和配额管理。
- CUPS PostScript 驱动程序支持由 Windows NT/2000/XP 客户端发送额外的标准（IPP）打印选项。这些额外的打印选项包括命名 CUPS 标准横幅页（或如果当时已安装自定义横幅页则使用自定义横幅页）、使用 CUPS 页面标签选项、设置作业优先级以及设置计划打印时间（并支持未来扩展其他有用的 IPP 作业属性）。
- CUPS PostScript 驱动程序支持在 PostScript 文件开头包含新的 `#cupsJobTicket` 注释（这在未来可用于 CUPS 侧的各种有益扩展，但不会干扰其他应用程序，因为它们会将其视为注释并简单地忽略它）。
- CUPS PostScript 驱动程序将是即将发布的完整功能 CUPS Windows NT/2000/XP IPP 客户端的核心（可能随 CUPS 1.2 的首个 beta 版本一起发布）。

### 21.10.9 以静默模式运行 cupsaddsmb

**cupsaddsmb** 命令将所需的文件复制到您的 `print$` 共享目录中。此外，与此打印机关联的 PPD 文件会从 `/etc/cups/ppd/` 复制到 `/print$`。在那里，这些文件等待通过“指向和打印”（Point'n'Point）方式进行方便的 Windows 客户端安装。在成功运行该命令之前，您需要确保我们可以向 Samba 进行身份验证。如果您有一个小型网络，您可能正在使用用户级安全性（`security = user`）。

以下是一个成功运行的 **cupsaddsmb** 命令的示例：

```bash
root# cupsaddsmb -U root infotec_IS2027
Password for root required to access localhost via Samba: ['secret']
```

若要共享*所有*打印机和驱动程序，请使用 `-a` 参数代替打印机名称。由于 **cupsaddsmb** 将打印机驱动程序“导出”到 Samba，因此显然它仅对与 CUPS 驱动程序关联的队列有效。

### 21.10.10 运行 cupsaddsmb 并显示详细输出

您或许希望查看正在发生的事情。使用 `-v` 参数可获得更详细的输出。下面的输出经过编辑以提高可读性：所有行尾的 `\` 表示我在这里插入了人为的换行符及缩进。

```bash
root# cupsaddsmb -U root -v infotec_2105
Password for root required to access localhost via GANDALF:
Running command: smbclient //localhost/print$ -N -U'root/secret' \
 -c 'mkdir W32X86; \\
 put /var/spool/cups/tmp/3e9bf2f4333b5 W32X86/infotec_2105.ppd; \\
 put /usr/share/cups/drivers/cupsdrv.dl1 W32X86/cupsdrv.dl1; \\
 put /usr/share/cups/drivers/cupsui.dll W32X86/cupsui.dll; \\
 put /usr/share/cups/drivers/cups.hlp W32X86/cups.hlp'
added interface ip=10.160.51.60 bcst=10.160.51.255 mask=255.255.252.0
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.7a]
NT_STATUS_OBJECT_NAME_COLLISION making remote directory W32X86
putting file /var/spool/cups/tmp/3e9bf2f4333b5 as W32X86/infotec_2105.ppd
putting file /usr/share/cups/drivers/cupsdrv.dl1 as W32X86/cupsdrv.dl1
putting file /usr/share/cups/drivers/cupsui.dll as W32X86/cupsui.dll
putting file /usr/share/cups/drivers/cups.hlp as W32X86/cups.hlp

Running command: rpcclient localhost -N -U'root/secret' \
 -c 'adddriver "WINDOWS NT x86"'
"infotec_2105:cupsdrv.dll:infotec_2105.ppd:cupsui.dll:cups.hlp:NULL: \\
RAW\"NULL"
cmd = adddriver "Windows NT x86" \\
"infotec_2105:cupsdrv.dll:infotec_2105.ppd:cupsui.dll:cups.hlp:NULL: \\
RAW\"NULL"
Printer Driver infotec_2105 successfully installed.
```

```bash
Running command: smbclient //localhost/print$ -N -U'root%secret' \\
-c 'mkdir WIN40'
put /var/spool/cups/tmp/3e98bf2d333b5 WIN40/infotec_2105.PPD; \\
put /usr/share/cups/drivers/ADFONTS.MFM WIN40/ADFONTS.MFM; \\
put /usr/share/cups/drivers/ADBEPS4.HLP WIN40/ADBEPS4.HLP; \\
put /usr/share/cups/drivers/ADBEPS4.DRV WIN40/ADBEPS4.DRV; \\
put /usr/share/cups/drivers/ADBEPS4.DRV WIN40/ADBEPS4.DRV; \\
put /usr/share/cups/drivers/DEFPTR2.PPD WIN40/DEFPTR2.PPD; \\
put /usr/share/cups/drivers/ICONLIB.DLL WIN40/ICONLIB.DLL; \\
put /usr/share/cups/drivers/PSMON.DLL WIN40/PSMON.DLL;'
added interface ip=10.160.51.60 bcast=10.160.51.255 mask=255.255.252.0
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.7a]
NT_STATUS_OBJECT_NAME_COLLISION making remote directory WIN40
putting file /var/spool/cups/tmp/3e98bf2d333b5 as \WIN40\infotec_2105.PPD
putting file /usr/share/cups/drivers/ADFONTS.MFM as \WIN40\ADFONTS.MFM
putting file /usr/share/cups/drivers/ADBEPS4.DRV as \WIN40\ADBEPS4.DRV
putting file /usr/share/cups/drivers/ADBEPS4.HLP as \WIN40\ADBEPS4.HLP
putting file /usr/share/cups/drivers/DEFPTR2.PPD as \WIN40\DEFPTR2.PPD
putting file /usr/share/cups/drivers/ICONLIB.DLL as \WIN40\ICONLIB.DLL
putting file /usr/share/cups/drivers/PSMON.DLL as \WIN40\PSMON.DLL
```

```bash
Running command: rpcclient localhost -N -U'root%secret' \\
-c 'adddriver "Windows 4.0"'
"infotec_2105:ADBEPS4.DRV:infotec_2105.PPD:NULL:ADBEPS4.HLP: \\
PSMON.DLL:RAW:ADBEPS4.DRV,ADBEPS4.HLP,ADFONTS.MFM,DEFPTR2.PPD, \\
ADFONTS.MFM,DEFPTR2.PPD,ICONLIB.DLL"'
cmd = adddriver "Windows 4.0" "infotec_2105:ADBEPS4.DRV: \\
infotec_2105.PPD:NULL:ADBEPS4.HLP:PSMON.DLL:RAW:ADBEPS4.DRV, \\
infotec_2105.PPD,ADBEPS4.HLP,PSMON.DLL,ADFONTS.MFM,DEFPTR2.PPD, \\
ICONLIB.DLL"
Printer Driver infotec_2105 successfully installed.
```

```bash
Running command: rpcclient localhost -N -U'root%secret' \\
-c 'setdriver infotec_2105 infotec_2105'
cmd = setdriver infotec_2105 infotec_2105
Successfully set infotec_2105 to driver infotec_2105.
```

> **警告**
>
> 您将在屏幕上看到 Samba 账户的 root 密码被打印出来。

如果您仔细查看，您会发现 root 密码未加密地在网络上传输，因此请小心！另外，如果您进一步查看，可能会发现输出中出现类似 `NT_STATUS_OBJECT_NAME_COLLISION` 的错误消息。当 `/print$` 驱动程序下载共享目录中已经存在 WIN40 和 W32X86 目录（由于之前的驱动程序安装）时，就会出现这种情况。这些是无害的警告消息。

### 21.10.11 理解 cupsaddsmb

发生了什么？ **cupsaddsmb** 做了什么？该过程分为五个阶段：

1. 通过 IPP 调用 CUPS 服务器，并请求指定名称打印机的驱动程序文件和 PPD 文件。
2. 将文件临时存储在本地的 TEMPDIR 中（如 `cupsd.conf` 中定义）。
3. 通过 smbclient 连接到 Samba 服务器的 `/print$/` 共享目录，并将文件放入共享目录的 WIN40（用于 Windows 9x/Me）和 W32X86（用于 Windows NT/200x/XP）子目录中。
4. 通过 rpcclient 连接到 Samba 服务器并执行带有正确参数的 **adddriver** 命令。
5. 再次通过 rpcclient 连接到 Samba 服务器并执行 **setdriver** 命令。

> **注意**
>
> 您可以使用参数运行 **cupsaddsmb** 实用程序，以指定一个远程主机作为 Samba 主机，另一个远程主机作为 CUPS 主机。特别是如果您想获得更深入的理解，这是一个好主意去尝试并更清楚地看到正在发生的事情（尽管在实际应用中，大多数人会将 CUPS 和 Samba 服务器运行在同一主机上）。
>
> ```bash
> root# cupsaddsmb -H sambaServer -h cupServer -v printer
> ```

