
在 Linux 中没有与此步骤等效的过程，因为在 Linux 中，用户本身并不像在 z/VM 中那样是一个完整的虚拟机。创建 Linux 用户时，其信息（用户 ID、密码）存储在系统文件中，并在`/home`目录中为其创建主文件夹。

## 登录并定制新的用户 ID

现在你应该能够登录到新的用户 ID 并格式化它的两个 minidisk：

+   1. 从 MAINT 注销，然后登录 LNXMAINT：

```
LOGON LNXMAINT
z/VM Version 5 Release 3.0, Service Level 0701 (64-bit),
built on IBM Virtualization Technology
There is no logmsg data
FILES: 0003 RDR,  NO PRT,  NO PUN
LOGON AT 05:41:34 EST THURSDAY 01/04/07
z/VM V5.3.0    2007-11-10 10:07
```

```
DMSACP112S A(191) device error
```

出现一条以 device error 结尾的错误消息。当 CMS 启动时，它会尝试将用户的 191 minidisk 作为文件模式 A 访问。191 minidisk 已定义给此用户 ID，但从未为 CMS 文件系统格式化⁹。

> 注意：仅用于保存 minidisk 的 DASD 不必格式化为 PERM 空间，因为其上的每个 minidisk 稍后都会被格式化。在这种情况下，格式化一个柱面并为其贴上标签就足够了。

⁹ 将 DASD 格式化为 PERM 存储与为 CMS 文件系统格式化用户 minidisk 是不同的。

## 创建 PROFILE EXEC

要创建一个简单的 PROFILE EXEC，以便每次此用户 ID 登录时运行：

+   1. 创建新文件并添加以下行。REXX EXEC 必须始终以 C 语言风格的注释开头。

```
==> x profile exec a
====> a 5
/* PROFILE EXEC */
'acc 592 e'
'cp set run on'
'cp set pf11 retrieve forward'
'cp set pf12 retrieve'
====> file
```

此 PROFILE EXEC 将 TCPMAINT 592 磁盘作为文件模式 E 访问，设置 CP run on（有关 RUN 参数的解释，请阅读第 60 页的“断开连接”部分），并按惯例设置检索键。

你可以向你的配置文件添加更多配置功能。虽然我们在这里没有提及，因为它们与安装步骤本身无关，但你可以在第 230 页的 5.2“运行系统”中看到它们。

+   2. 你可以通过注销并重新登录来测试更改。但是，键入命令 PROFILE 也能达到相同效果。默认情况下，CMS 会尝试将 191 磁盘作为 A 访问，将 192 磁盘作为 D 访问。此外，你应该已将 TCPMAINT 592 磁盘作为 E 访问。要查看你的 minidisk，请使用 QUERY DISK（`q disk`）命令：

```
==> profile
DMSACP7231 E (592) R/O
==> q disk
LABEL VDEV M STAT CYL TYPE BLKSZ FILES BLKS USED-(%) BLKS LEFT BLK TOTAL
LXM191 191 A R/W 120 i3390 4096 2 9-01 3591 3600
LXM192 192 D R/W 300 i3390 4096 0 11-00 53989 54000
TCM592 592 E R/O 167 i3390 4096 877 8167-68 3893 12060
MNT190 190 S R/O 100 i3390 4096 689 14325-80 3675 18000
MNT19E 19E Y/S R/O 250 i3390 4096 1010 26665-59 18335 45000
MNT191 120 Z R/O 175 i3390 4096 36 224-01 31276 31500
```

+   3. 验证你的 F11 和 F12 键已设置为 RETRIEVE 命令：

```
==> q pf11
PF11 RETRIEVE FORWARD
==> q pf12
PF12 RETRIEVE BACKWARD
```

## 获取 Linux 启动所需的文件

在第 183 页的“为 LNXMAINT 设置 minidisk 空间”一节中，你为 LNXMAINT 用户创建了两个磁盘：191 和 192 磁盘。191 磁盘将用于

用作 LNXMAINT 的主磁盘，其通用文件将存放在此。另一方面，192 磁盘将用于托管 Linux 虚拟机启动所需的所有文件。稍后，在第 193 页的“为 Linux 虚拟机设置通用配置文件”中，你将在 Linux 客户机中设置一个配置文件，该文件将以只读模式将其 191 磁盘链接到 LNXMAINT 的 192 磁盘。通过这样做，客户机的主磁盘可以通过从此链接的 LNXMAINT 磁盘读取来加载必要的 Linux 文件。

> **注意：** 要继续本节，请确保你已在 z/VM 中设置了 FTP 服务器，如第 163 页的“设置 FTP 服务器”中所述。再次强调，通过 FTP 发送文件是必需的，以确保传输保持内核和 ramdisk 文件的 80 字符记录长度。

你必须向你的 LNXMAINT 192 磁盘发送三个文件：

- Linux 内核

  - 在 SLES10 中，这是其第一张 DVD 或 CD 上的`/boot/s390x/vmrdr.ikr`文件

  - 在 RHEL5 中，这是其第一张 DVD 或 CD 上的`/images/kernel.img`文件

- Linux ramdisk

  - 在 SLES10 中，这是其第一张 DVD 或 CD 上的`/boot/s390x/initrd`文件

  - 在 RHEL5 中，这是其第一张 DVD 或 CD 上的`/images/initrd.img`文件

- 位于压缩文件中找到的 SWAPGEN 文件：

  `ftp://www.redbooks.ibm.com/redbooks/SG246695/`

> **注意：** 如果你的内核和 ramdisk 不是 80 字符记录长度，内核将无法加载。

作者获得了 SLES10SP2 和 RHEL5 U1 仓库的访问信息。由于我们必须选择一个作为此处示例的基础，我们决定使用 SLES。但是，当需要不同步骤或配置时，会突出显示 RHEL 系统的注释。

将这三个文件放在桌面上的同一目录中（你用于连接大型机的机器）并使用 FTP 客户端连接到服务器，如示例 4-10 所示。确保此时已注销 LNXMAINT，否则你的 FTP 客户端无法以读写模式访问磁盘。

### 示例 4-10 通过 FTP 将文件发送到 LNXMAINT 的 192 磁盘

```
# ftp <9.12.4.89> []
Connected to 9.12.4.89.
```

220-FTPSERVE IBM VM Level 530 at VMLINUX6.ITSO.IBM.COM, 16:33:09 EDT

THURSDAY 2008-05-15

220 Connection will close if idle for more than 5 minutes.

Name (9.12.4.89:root): lnxmaint 2a

331 Send password please.

Password:lnxmaint 2b

230 LNXMAINT logged in; working directory = LNXMAINT 191

Remote system type is z/VM.

ftp> cd lnxmaint.192 3

250 Working directory is LNXMAINT 192

ftp> put swapgen.exec 4

local: swapgen.exec remote: swapgen.exec

500 Unknown command, 'EPSV'

227 Data transfer will passively listen to 9,12,4,89,4,7

125 Storing file 'swapgen.exec'

100% |******************************************| 16750  14.60 MB/s

--:-- ETA

250 Transfer completed successfully.

16750 bytes sent in 00:00 (1.74 MB/s)

ftp> bin 5

200 Representation type is IMAGE.

ftp> site fix 80 6

200 Site command was accepted.

ftp> put vmrdr.ikr sles10s2.ikr 7
