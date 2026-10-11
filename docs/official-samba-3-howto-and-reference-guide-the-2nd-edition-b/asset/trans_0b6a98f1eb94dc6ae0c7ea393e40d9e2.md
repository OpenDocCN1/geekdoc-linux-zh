
# 注意

![](img/86d74c6cc862465e3a42e6dc3c90935a_378_0.png)

在 Windows 2000 和 Windows XP 上，较新的驱动程序被安装在“3”子目录中，而不是“2”中。在 Windows NT 中使用的版本 2 的驱动程序是在内核模式下运行的。Windows 2000 改变了这一点。虽然它仍然可以使用内核模式驱动程序（如果由管理员启用），但其对打印机驱动程序的默认模式是用户模式执行。这需要为此目的设计的驱动程序。这些类型的驱动程序安装到“3”子目录中。

## 20.6.2.2 从 Windows 客户端 *[print$] 共享* 获取驱动程序文件

现在我们需要收集上一步中确定的所有驱动程序文件。我们从哪里获取它们？嗯，为什么不从我们在上一步中调查文件的那个 PC 和同一个 *[print$]* 共享中检索它们呢？我们可以使用 **smbclient** 来做到这一点。我们将使用由 **getdriver** 泄露给我们的路径和名称。列表经过编辑，加入换行符以提高可读性：

```bash
root# smbclient //TURBO_XP/print$ -U'Danka%xxxx' -c 'cd W32X86/2; \get HD*.de.* hd*ppd HD*.de.* Hddm*dl l HDN*Aux .DLL'
added interface ip=10.160.51.60 bcast=10.160.51.255 nmask=255.255.252.0
Got a positive name query response from 10.160.50.8 ( 10.160.50.8 )
Domain=[DEVELOPMENT] OS=[Windows 5.1] Server=[Windows 2000 LAN Manager]
Get file Hddm91cl.de.ABD? n
Get file Hddm91cl.de.def? y
getting file \W32X86\2\Hddm91cl.de.def of size 428 as Hddm91cl.de.def
Get file Hddm91cl.de.DLL? y
getting file \W32X86\2\Hddm91cl.de.DLL of size 876544 as Hddm91cl.de.DLL
[...]
```

此命令完成后，文件位于我们当前的本地目录中。你可能已经注意到，这次我们向 *-c* 参数传递了多个命令，用分号分隔。这确保了所有命令都在远程 Windows 服务器上按顺序执行，然后 **smbclient** 才会退出。

如果你需要支持 Windows 9x/Me/XP 客户端，请记住针对 WIN40 架构重复此过程。也要记住，这些架构的文件位于 **WIN40/0/** 子目录中。完成后，我们可以运行 **smbclient** ... *put* 将收集的文件存储到 Samba 服务器的 *[print$]* 共享中。

## 20.6.2.3 将驱动程序文件安装到 [print$]

我们现在要将驱动程序文件定位到 [print$] 共享中。请记住，该共享的 UNIX 路径已在你的 smb.conf 文件中之前定义。你还为想要支持的不同 Windows 客户端类型创建了子目录。例如，如果你的 [print$] 共享映射到 UNIX 路径 /etc/samba/drivers/，那么你的驱动程序文件现在应该放在这里：

- 适用于所有 Windows NT、2000 和 XP 客户端：/etc/samba/drivers/W32X86/，但不要（还）放在 2 子目录中。
- 适用于所有 Windows 95、98 和 Me 客户端：/etc/samba/drivers/WIN40/，但不要（还）放在 0 子目录中。

我们再次使用 smbclient 通过网络传输驱动程序文件。我们指定由针对原始 Windows 安装运行 getdriver 泄露给我们的相同文件和路径。然而，现在我们要将文件存储到 Samba/UNIX 打印服务器的 [print$] 共享中。

```bash
root# smbclient //SAMBA-CUPS/print$ -U'root/xxxx' -c \
'cd W32X86; put HDNISI01_de.DLL; \
put Hddm91c1_de.ppd; put HDNISI01_de.dll;   \
put HDNISIOU_de.HLP; put Hddm91c1_de.dll;    \
put Hddm91c1_de.INI; put Hddm91c1KMIN.DLL;   \
put Hddm91c1_de.dat; put Hddm91c1_de.dat;     \
put Hddm91c1_de.def; put Hddm91c1_de.hre;     \
put Hddm91c1_de.vnd; put Hddm91c1_de.hlp;     \
put Hddm91c1_de_reg.HLP; put HDNISOIAux.dll;  \
put HDNISI01_de.NTf'
```

```bash
added interface ip=10.160.51.60 bcast=10.160.51.255 netmask=255.255.252.0
Got a positive name query response from 10.160.51.162( 10.160.51.162)
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.7a]
putting file HDNISI01_de.DLL as W32X86/HDNISI01_de.dll
putting file Hddm91c1_de.ppd as W32X86/Hddm91c1_de.ppd
putting file HDNISIOU_de.dll as W32X86/HDNISIOU_de.dll
putting file HDNISIOU_de.HLP as W32X86/HDNISIOU_de.HLP
putting file Hddm91c1_de.dll as W32X86/Hddm91c1_de.dll
putting file Hddm91c1_de.ini as W32X86/Hddm91c1_de.ini
putting file Hddm91c1KMIn.dll as W32X86/Hddm91c1KMIn.dll
putting file Hddm91c1_de.dat as W32X86/Hddm91c1_de.dat
putting file Hddm91c1_de.dat as W32X86/Hddm91c1_de.dat
putting file Hddm91c1_de.def as W32X86/Hddm91c1_de.def
putting file Hddm91c1_de.hre as W32X86/Hddm91c1_de.hre
putting file Hddm91c1_de.vnd as W32X86/Hddm91c1_de.vnd
putting file Hddm91c1_de.hlp as W32X86/Hddm91c1_de.hlp
putting file Hddm91c1_de_reg.HLP as W32X86/Hddm91c1_de_reg.HLP
putting file HDNISOIAux.dll as W32X86/HDNISOIAux.dll
putting file HDNISO1_de.NTF as \W32X86\HDNISO1_de.NTF
```

呼——那真是敲了很多键！大多数驱动程序要小得多——许多只有三个通用的 PostScript 驱动程序文件加上一个 PPD。虽然我们确实从 Windows 机器上的 w32x86 目录的 2 子目录中检索了文件，但我们（暂时）不将它们放到 Samba 机器上的同一个子目录中。这次重新定位将由 addriver 命令自动完成，我们稍后就会运行该命令（如果需要，也不要忘记将 Windows 9x/Me 架构的文件放到 \WIN4O\ 子目录中）。

## 20.6.2.4 使用 smbclient 确认驱动程序安装

目前我们验证文件是否在那里。这也可以通过 **smbclient** 完成（当然，你也可以通过 SSH 登录并通过标准 UNIX shell 访问来做到这一点）：

```bash
root# smbclient //SAMBA-CUPS/print/$ -U 'root/xxxxx' \
-c 'cd W32X86; pwd; dir; cd 2; pwd; dir'
added interface ip=10.160.51.60 bcast=10.160.51.255 nmask=255.255.252.0
Got a positive name query response from 10.160.51.162 ( 10.160.51.162 )
Domain=[CUPS-PRINT] OS=[UNIX] Server=[Samba 2.2.8a]

Current directory is \\ SAMBA-CUPS \ print$ \ W32X86\ :
D 0 Sun May 4 03:56:35 2003
. D 0 Thu Apr 10 23:47:40 2003
.. D 0 Sun May 4 03:56:18 2003
2 D 0 Sun May 4 03:56:18 2003
HDNISO1Aux.dll A 15356 Sun May 4 03:58:59 2003
Hdcm91c1KMW.in.DLL A 46966 Sun May 4 03:58:59 2003
HDNISO1_de.DLL A 434400 Sun May 4 03:58:59 2003
HDNISO1_de.NTF A 790404 Sun May 4 03:58:35 2003
Hddm91c1_de.DLL A 876544 Sun May 4 03:58:59 2003
Hddm91c1_de.INI A 101 Sun May 4 03:58:59 2003
Hddm91c1_de.dat A 5044 Sun May 4 03:58:59 2003
Hddm91c1_de.def A 428 Sun May 4 03:58:59 2003
Hddm91c1_de.hlp A 37699 Sun May 4 03:58:59 2003
Hddm91c1_de.lpr A 323584 Sun May 4 03:58:59 2003
Hddm91c1_de.ppd A 26373 Sun May 4 03:58:59 2003
Hddm91c1_de.vnd A 45056 Sun May 4 03:58:59 2003
HDNIS01U_de.DLL A 165888 Sun May 4 03:58:59 2003
HDNIS01U_de.HLP A 19770 Sun May 4 03:58:59 2003
Hddm91c1_de_reg.HLP A 228417 Sun May 4 03:58:59 2003
40976 blocks of size 262144. 709 blocks available

Current directory is \\ SAMBA-CUPS \ print$ \ W32X86 \ 2\ :
D 0 Sun May 4 03:56:18 2003
. D 0 Sun May 4 03:56:35 2003
.. A 434400 Sat May 3 23:18:45 2003
ADOBEPS5.DLL A 434400 Sat May 3 23:18:45 2003
```

注意到 2 子目录中已经存在驱动程序文件（可能来自以前的安装）。一旦新驱动程序的也存在，你仍然还需要几步才能在客户端上使用它们。目前你唯一能做的就像从文件共享中检索普通文件一样，通过 Windows 资源管理器打开 print$ 来从客户端检索它们。但这不会按打印安装它们。原因是 Samba 尚不知道这些文件是特殊的东西，即打印机驱动程序文件，并且它也不知道这些驱动程序文件属于哪些打印队列。

## 20.6.2.5 运行带有 adddriver 的 rpcclient

接下来，你必须告诉 Samba 你刚刚上传到 [print$] 共享中的文件的特殊类别。这是通过 adddriver 命令完成的。它会让 Samba 将驱动程序文件注册到其内部 TDB 数据库文件中。以下命令及其输出为了可读性经过编辑：

```bash
root# rpcclient -Uroot%xxxx -c 'adddriver "Windows NT x86" '
"dm9110:HDNIS01_de.DLL: \
Hdmm91c1_de.ppd:HDMI5O1U_de.DLL:HDMI5O1U_de.HLP: \
NULL:RAV:Hdmm91c1_de.DLL,Hdmm91c1_de.INI,
Hdmm91c1_de.dat,Hdmm91c1_de.def,Hdmm91c1_de.bre,
Hdmm91c1_de.vnd,Hdmm91c1_de.hlp,Hdmm91c1KMmin.DLL,
HDNI5O1Aux.dll,HDNI5O1_de.NTF,
Hdmm91c1_de_reg.HLP' SAMBA=CUPS
cmd = adddriver "Windows NT x86" 
"dm9110:HDMI501_de.DLL:Hdmm91c1_de.ppd:HDMI5O1U_de.DLL:
HDMI5O1U_de.HLP:NULL:RAV:Hdmm91c1_de.DLL,Hdmm91c1_de.INI,
Hdmm91c1_de.dat,Hdmm91c1_de.def,Hdmm91c1_de.bre,
Hdmm91c1_de.vnd,Hdmm91c1_de.hlp,Hdmm91c1KMmin.DLL,
HDNI5O1Aux.dll,HDNI5O1_de.NTF,Hdmm91c1_de_reg.HLP"
Printer Driver dm9110 successfully installed.
```

在此步骤之后，驱动程序应被打印服务器上的 Samba 识别。输入命令时需要非常小心。不要交换字段的顺序。某些更改会导致 NT_STATUS_UNSUCCESSFUL 错误消息。这些变得明显。其他更改可能会成功安装驱动程序文件，但使驱动程序无法工作。所以要小心！adddriver 命令的语法提示在 man 页面中，如果你需要，它提供了更详细的描述。

