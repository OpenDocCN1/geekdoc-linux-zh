
```bash
$ grep -i | mft.body | grep FILE_NAME | cut -d|f2
[MFT FILE_NAME] WINDOWS\system2\confidential3.pdf (Offset: 0xc692750)
[MFT FILE_NAME] WINDOWS\system2\confidential4.pdf (Offset: 0xd694b80)
[MFT FILE_NAME] WINDOWS\system2\w.exe (Offset: 0xd8cb80)
[MFT FILE_NAME] WINDOWS\system2\confidential5.pdf (Offset: 0x10acc88)
[MFT FILE_NAME] WINDOWS\system2\systemf.txt (Offset: 0x15938800)
[MFT FILE_NAME] WINDOWS\system2\g.exe (Offset: 0x15938c00)
[MFT FILE_NAME] WINDOWS\system2\p.exe (Offset: 0x18229000)
[MFT FILE_NAME] WINDOWS\system2\r.exe (Offset: 0x18229400)
[MFT FILE_NAME] WINDOWS\system2\sysmon.exe (Offset: 0x18229800)
[MFT FILE_NAME] WINDOWS\system3\$system1 (Offset: 0x1b2d4400)
```

# 网络存活

通过工具整理 `mftparser` 输出，你可以确定以下 Prefetch 文件是在 `SWING-MECHANICS.DOC1.EXE-01CEA10.pf` 之后创建的。这一证据表明攻击者正在进行网络侦察以获取系统。

```text
[MFT FILE_NAME] WINDOWS\Prefetch\IPCONFIG.EXE-239F53B0.pf (Offset: 0x10c5800)
[MFT FILE_NAME] WINDOWS\Prefetch\NET.EXE-01A53C2F.pf (Offset: 0xd3e5d800)
[MFT FILE_NAME] WINDOWS\Prefetch\PING.EXE-31216D26.pf (Offset: 0x11b0f400)
```

# WinRAR 存档外泄

此外，如果你查看输出结果，可以看到攻击者可能已经将用户的 PDF 文件归档为 RAR 文件。具体而言，在 `r.exe` 执行后，Application Data 目录中创建了一个 WinRAR 文件夹。众所周知，WinRAR 在系统上首次运行时创建此文件夹。在这些痕迹出现后，`ftp.exe` 程序运行：

```text
ftp r.exe
[MFT FILE_NAME] WINDOWS\system32\system1\confidential13.pdf (Offset: 0xd6927500)
[MFT FILE_NAME] WINDOWS\system32\system1\confidential4.pdf (Offset: 0xd6948b00)
[MFT FILE_NAME] WINDOWS\system32\system1\confidential5.pdf (Offset: 0xd0a1cc88)
[MFT FILE_NAME] WINDOWS\system32\system1\r.exe (Offset: 0x18229400)
[MFT FILE_NAME] WINDOWS\Prefetch\R.EXE-192B4F9B.pdf (Offset: 0xleeb2a400)
[MFT FILE_NAME] WINDOWS\Documents and Settings\binge\Application Data\WinRAR\(Offset: 0xd6b4000)
[MFT FILE_NAME] WINDOWS\Prefetch\FTP.EXE-0FFBA53.pdf (Offset: 0xd1b10000)
```

为了验证 `r.exe` 程序，你可以使用 `dump` 程序（本文稍后会讨论）将其提取并使用 `strings` 工具对其进行分析。以下输出显示了如何比较：

```bash
$ python vol.py -f grrcoon.raw dumps | grep -i r.exe$
Volatility Foundation Volatility Framework 2.4
[snip]
0x0000000021be7a0 1 R--r-d
\Device\Harddisk\Volume1\WINDOWS\system32\systems\r.exe
[snip]

$ mdk output
$ python vol.py -f grrcoon.raw dumps -Q 0x0000000021be7a0 -D output
Volatility Foundation Volatility Framework 2.4
ImageSectionObject 0x021be7a0 None
\Device\Harddisk\Volume1\WINDOWS\system32\systems\r.exe
DataSectionObject 0x021be7a0 None
\Device\Harddisk\Volume1\WINDOWS\system32\systems\r.exe
```

`dump` 提取了一个文件：

```bash
$ ls output/
file.None.0x82137f10.img
```

如果你在 Linux 上使用 `strings` 工具，你需要进行两次扫描，一次针对 ASCII，一次针对 Unicode：

```bash
$ strings -a file.None.0x82137f10.img > r.exe_strings
$ strings -a el file.None.0x82137f10.img >> r.exe_strings
```

之后，你就可以检查输出。如果你向下滚动，会发现一条帮助信息。该信息属于 WinRAR（参见 <https://discussions.apple.com/thread/4114488?tstart=0>），它证明了攻击者使用 WinRAR 创建了文件存档：

```text
$ less r.exe_strings
[snip]
o[+|-]      设置覆盖模式
oc               设置 NTFS 压缩属性
ol               将符号链接保存为链接而非文件
or               自动重命名文件
os               保存 NTFS 流
ow             保存或恢复文件所有者组
p[password]      设置密码
[snip]
s-               禁用固化压缩
sc+chr:[obj]    指定字符集
sfx[name]      创建 SFX 存档
si[name]      从标准输入 (stdin) 读取数据
```

```text
[snip]
ERROR: Bad archive %s
#Enter password (将不会显示)
Enter password
Reenter password:
[snip]
```

# MFT 驻留数据

由于攻击者脚本足够小，可以驻留于 MFT 中，因此运行开启详细模式的 `mftparser` 插件以提取任何可能存在的脚本是值得的。在这种情况下，`mftparser` 插件的详细输出提取了攻击者的一个脚本 (`f.txt`)。该脚本使用用户名 `jack` 和密码 `2awsome` 连接到 `66.32.119.38`，切换到释放文件所在的系统目录，并将该目录下的文本文件上传到远程系统的 `/home/jack` 目录：

```text
[snip]
Full Path: WINDOWS\system32\systems\.txt
```
