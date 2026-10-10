

这会根据指定的 I/O 地址和 IRQ 设置你的并行端口。然后你可以查看内核消息：

```bash
$ dmesg
```

```text
...
parport0: PC-style at 0x378, irq 7 [SPP,ECP,PCFPPS2]
```

这表明该端口已初始化。接下来，使用 insmod 加载 PLIP 支持并创建你的 PLIP 设备：

```bash
$ insmod plip timed=1
```

timed 选项指示 plip.o 避免使用其他正在使用的 I/O 地址或 IRQ。然后你可以检查内核输出，以查看设备是否已创建：

```bash
$ dmesg
```

```text
...
plip0: Parallel port at 0x378, using IRQ 7
```

注意返回的并行端口设备（在此例中为 plip0）。然后你可以使用 ifconfig 命令在每个计算机上启动 plip 接口（同时也可能设置设备子网掩码等）。例如，在 ComputerA 上，你可以使用以下命令：

```bash
$ ifconfig plip0 ComputerA pointopoint ComputerB up
```

而在 ComputerB 上，你可以使用以下命令：

```bash
$ ifconfig plip0 ComputerB pointopoint ComputerA up
```

然后你可以检查每个计算机上的接口：

```bash
$ ifconfig plip0
```

```text
plip0 Link encap:Ethernet HWaddr FC:PC:C0:A8:02:26 inet addr:192.168.2.38 P-t-P:192.168.2.30 Mask:255.255.255.255 UP POINTOPOINT RUNNING NOARP MTU:1500 Metric:1 RX packets:0 errors:0 dropped:0 overruns:0 frame:0 TX packets:0 errors:0 dropped:0 overruns:0 carrier:0 collisions:0 txqueuelen:10 Interrupt:7 Base address:0x378
```

然后你可以尝试 ping、telnet 或 ftp 到另一台计算机。你可能会遇到的问题包括线缆故障和不兼容的并行端口。要断开连接，请像这样使用 ifconfig 命令：

```bash
$ ifconfig plip0 down
```

## 红外（IrDA）网络

你也可以在笔记本电脑与其他笔记本电脑之间，或在配备红外（IrDA）"转接器"的桌面 PC 之间建立网络连接。请参阅 Linux IR-HOWTO 了解如何设置网络。访问 `http://home.snafu.de/wehe/IR-HOWTO.html`。速度将比使用串行或并行端口连接快得多。

## 设置交叉以太网连接

本节向你展示另一种极具成本效益的方法，用于将两台笔记本电脑，或一台桌面计算机和一台笔记本电脑进行网络连接。如果你想通过以太网连接一台笔记本电脑和一台桌面计算机，或者两台笔记本电脑，你不需要网络集线器！这种方法与串行和 PLIP 示例类似。我们将再次使用 `ifconfig` 命令来设置每台计算机的接口。

你需要确保每台计算机的 IP 地址和别名已输入到每台计算机的 `/etc/hosts` 文件中。插入网卡，并确保网卡已被识别和初始化。例如：

```text
# dmesg
...
eth0: NE2000 Compatible: io 0x300, irq 3, hw_addr 00:E0:98:06:84:C5
```

此示例表明 PC 网卡已被识别，并且 `eth0` 设备已创建。接下来，将 Cat 5 RJ-45 交叉线缆（而非普通跳线）连接到每个网卡的接口。这些线缆可以在大多数大型电脑商店找到。它们通过交换接收和发送线对来工作。有关自行制作的具体说明，请阅读 Paul Gortmaker 的 Ethernet-HOWTO（如果你在安装发行版时安装了文档，可以在你的 `/usr/doc/HOWTO` 目录下找到）。

连接线缆后，转到 ComputerA 并输入

```text
# ifconfig eth0 ComputerA pointopoint ComputerB up
```

然后，在 ComputerB 上输入

```text
# ifconfig eth0 ComputerB pointopoint ComputerA up
```

你应该查看网卡的指示灯以确认连接，然后使用 `ifconfig` 命令像这样检查每台计算机上的接口状态：

```text
# ifconfig eth0

eth0      Link encap:Ethernet  HWaddr 00:E0:98:06:84:C5
          inet addr:192.168.2.38  Bcast:192.168.2.255  Mask:255.255.255.0
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:0 errors:0 dropped:0 overruns:0 frame:0
          TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:100
          Interrupt:3 Base address:0x300
```

完成文件传输后，你可以使用 `ifconfig` 命令像这样断开连接：

```text
# ifconfig eth0 down
```

## 使用 Samba

如果你需要将笔记本电脑连接到 Windows 网络，你可以使用 Linux Samba 软件包中包含的多个实用工具来发送和检索文件。Samba 程序套件的其他部分支持从 Linux 共享文件，并支持向 Windows 打印或从 Windows 打印。本节介绍了一些基本步骤，涉及 Windows 端和 Linux 端的操作，以便你开始使用 Samba。然而，关于这个软件包的完整讨论超出了本书的范围。

### 为 Samba 进行设置

在正确安装和配置 Windows 计算机中的网卡后，你应该启用文件和打印共享访问。然后你应该拥有计算机名称、工作组和卷名（计算机名称和工作组信息可通过"网络"控制面板的"标识"选项卡获取）。

在你的笔记本电脑上，以 root 操作员身份登录。将 Windows 计算机的 IP 地址添加到系统的 /etc/hosts 文件中。保存文件，退出编辑器，然后使用 `ping` 命令测试连接。在 Windows 计算机上，从开始菜单运行 MS-DOS 提示符应用程序，并使用 `ping` 命令测试到你笔记本电脑的连接。

从你的 Linux 计算机，使用 `smbclient` 命令及其 -L 选项列出 Windows 机器上可用的资源：

```text
# smbclient -L stinky
Added interface  ip=192.168.2.38  bcast=192.168.2.255  nmask=255.255.255.0

Password:

        Sharename   Type   Comment
        ---------   ----   -------
        C           Disk    stinky's laptop drive
```

系统会要求你输入在 Windows 计算机上设置共享时分配的文件共享密码。`-L` 选项方便地列出了计算机上可用的服务。如前例所示，该 Windows 计算机是一台笔记本电脑。

## 传输文件

启用共享后，你可以使用 smbclient、计算机的 Windows 名称、共享卷名、`-I` 选项和 IP 地址（或 Windows 计算机的主机名），以及 `-u` 选项和用户名（在 Windows 计算机上）从 Linux 访问此硬盘：

```text
# smbclient '//stinky/c' -I stinky -U bhsall
Added interface ip=192.168.2.38 bcast=192.168.2.255 mask=255.255.255.0
Password:
smb: \>
```

输入文件共享访问密码并按 Enter 后，你可以使用问号 (?) 或 help 关键字获取 smbclient 内置命令的列表：

```text
smb: \> help
```

```text
ls          dir         du        lsd         cd
pwd         get         mget      put         mput
rename      more        mask      del         open
rm          mkdir       md        rmdir       rd
prompt:     recurse     translate lowercase print
printmode   queue       cancel    quit        q
exit        never       archive   tar         blocksize
          setmode     help
```

使用 `cd` 命令更改目录到 Windows 桌面，然后使用 `ls` 命令列出文件：

```text
smb: \> cd windows/desktop
smb: \windows/desktop\> ls
```

```text
D 0 Wed Jun 9 21:12:34 1999
D 0 Wed Jun 9 21:12:34 1999
RingCentral Fax.lnk A 364 Sat Jul 31 10:15:54 1999
cerols.DKN A 816 Tue Dec 7 12:15:06 1999
Register.lnk A 363 Tue Dec 7 11:51:46 1999
My Briefcase DR 0 Wed Jun 9 21:12:46 1999
Netscape Navigator.lnk A 583 Tue Dec 7 12:22:18 1999
Rio Manager.lnk A 403 Wed Jun 9 23:05:00 1999
MusicMatch Jukebox.lnk A 493 Wed Jun 9 23:05:30 1999
Netscape Communicator.lnk A 583 Wed Jun 9 23:54:56 1999
AOL Instant Messenger (TM).lnk A 586 Wed Jun 9 23:55:06 1999
RealPlayer G2.lnk A 421 Wed Jun 9 23:55:38 1999
explore2fs-1.00-pre2.zip D 325902 Sat Nov 13 11:24:08 1999
vmc D 0 Wed Nov 10 04:08:04 1999
WinZip.lnk A 385 Wed Nov 10 11:07:26 1999
eBowl.exe A 1130496 Thu Nov 18 17:05:52 1999
ext2fs D 0 Sat Nov 13 11:13:10 1999
Shortcut to dball on Green.lnk A 274 Sun Jan 16 11:39:36 2000
linuxdir_167.exe A 7213 Tue Nov 30 23:54:54 1999
fase.snd A 684032 Wed Jan 26 17:46:46 2000
ar D 0 Tue Dec 14 17:16:44 1999
mail.1.14.00 D 0 Sun Jan 16 11:40:16 2000

65505 blocks of size 32768; 18814 blocks available

smb:\\windows\desktop>
```

使用 `mget` 命令后跟一个文件名，从 Windows 桌面检索文件到当前 Linux 目录：

```text
smb:\\windows\desktop> mget explore2fs*
Get file explore2fs-1.00-pre2.zip? y
getting file explore2fs-1.00-pre2.zip of size 325902 as explore2fs-1.00-pre2.zip
(298.559 kb/s) (average 298.559 kb/s)
smb:\\windows\desktop>
```

使用 `mput` 命令后跟当前 Linux 目录中的文件名，将其发送到 Windows 桌面：

```text
smb:\\windows\desktop> mput Linuxdocument.txt
Put file Linuxdocument.txt? y
putting file Linuxdocument.txt as \\windows\desktop\Linuxdocument.txt (13.0673 kb/s)
(average 13.0673 kb/s)
```

