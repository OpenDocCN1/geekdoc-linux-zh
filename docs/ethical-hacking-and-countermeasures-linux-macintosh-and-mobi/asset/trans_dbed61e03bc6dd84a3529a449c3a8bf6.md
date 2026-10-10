
在Windows操作系统中选择一个选项，以避免蠕虫自动运行的可能性，并防止其重复该过程以进一步传播。

## 破解USB设备简介

本章专注于破解USB设备。首先，它介绍了USB设备的一般概述及其工作原理。然后，讨论了针对USB设备发起的不同类型攻击。本章还涵盖了黑客用于攻击USB设备的工具，以及管理员可用于保护这些设备的工具。最后，它列举了用户可以采取的一些对策来保护其设备。

## USB设备简介

USB（通用串行总线）设备是一种外设（物理输入/输出设备），可插入USB端口。USB端口是一种即插即用硬件接口，用于将这些外设（如磁盘驱动器、打印机、记忆棒、鼠标、键盘和游戏手柄）连接到计算机。它提供了一种单一、标准化的方法将设备连接到计算机，并允许这些设备与主机计算机通信。USB外设通常是热插拔的，这意味着可以在不重新启动或关闭计算机的情况下连接和断开它们。

当USB设备连接到计算机时，系统会确定USB设备的速度，并自动识别和配置该设备。支持的数据传输速率将在下面部分进行说明。

### USB传输速率

不同版本的USB支持不同的数据传输速率。USB 1.1只能以最大12 Mbit/s的速率传输数据，而USB 3.0可以以4.8 Gbit/s的速率传输数据。USB支持的数据传输速率如下：

- 低速（1.1, 2.0）：以1.5 Mbit/s（187 kB/s）的速率传输数据。
- 全速（1.1, 2.0）：以12 Mbit/s（1.5 MB/s）的速率传输数据。
- 高速（2.0）：以480 Mbit/s（60 MB/s）的速率传输数据。
- 超速（3.0）：以4.8 Gbit/s（600 MB/s）的速率传输数据。

### USB攻击

有几种类型的USB攻击。本节将解释电气攻击、软件攻击和Windows缓冲区溢出攻击。

#### 电气攻击

USB驱动器存在一个常见的设计缺陷：在串行电可擦除可编程只读存储器（EEPROM）中不当存储密码值。USB设备由一个支持USB的微处理器、外部存储器和粘合电路组成。存储器是EEPROM，其读写所需的最小电路；因此，它主要用在工程行业。然而，它是不安全的，并且没有为使用它的设备提供安全性。因此，设备 programmers 被附加到使用串行EEPROM的设备上，通过限制不当的访问来提供安全性。

由于这个缺陷，攻击者可以使用电气攻击，这种攻击是在物理访问设备电路板时对USB驱动器进行的，以提取所有数据，包括私人信息。攻击者的目标是窃取存储在设备上的私人数据，这些数据本应由合法用户的PIN和密码保护。在攻击过程中，存储在EEPROM中的密码值被更改，数据很容易被提取。黑客完成后，攻击者将密码重置为原始密码，从而确保USB设备的所有者不会察觉到任何可疑活动。

#### 软件攻击

软件攻击是一种非侵入式攻击。在这种攻击中，USB设备不会被篡改或损坏。相反，软件攻击利用设备的正常操作条件，其目的是找到产品中软件或固件实现的缺陷。

供应商提供的软件开发工具包包括源代码、头文件以及关于USB设备设计和结构的信息。这些信息存储在设备的串行EEPROM上，由于设计缺陷，允许访问私人信息。在发起软件攻击时，攻击者试图通过使用自定义设备驱动程序和商用USB协议分析器来检查USB设备与主机计算机之间的通信通道，从而获取这些私人信息。攻击者可以使用这些信息来分析和确定成功攻击的可能性，然后使用以下方法之一：

- *尝试暴力破解密码：* 通过分析并确定管理员的MKEY值或真正的用户密码或PIN来访问USB驱动器。
- *向USB驱动器发送错误且已知的错误USB数据包：* 由于设计缺陷，USB驱动器可能会允许传输受保护内存区域的内容。

攻击完成后，结果可以复制到其他设备。

## Windows缓冲区溢出攻击

插入装有32位Windows操作系统（如Windows Vista、XP和2000）的计算机的USB设备面临另一种攻击的危险。USB设备驱动程序中的缓冲区溢出漏洞可能允许攻击者绕过Windows安全并获取主机机器上的管理员访问权限。了解这些漏洞的攻击者可以编程一个USB驱动器，使其伪装成使用易受漏洞影响的驱动程序的设备类型。

完成此操作后，攻击者将设备插入主机系统，当有缺陷的驱动程序被加载时，攻击者将获取存储在设备串行EEPROM上的默认PIN和合法用户的凭据。攻击者可以使用这些信息利用系统并访问锁定的工作站。

这些攻击需要对系统的物理访问，可以通过使用USB安全工具来预防，这些工具可以识别当USB设备插入主机计算机或其网络时，并阻止利用。

## 病毒和蠕虫

以下部分介绍影响USB设备的一些病毒和蠕虫。

### 病毒：W32/Madang-Fam

W32/Madang-Fam是一类感染Windows平台的病毒，可以通过可移动存储设备进行传播。这些病毒搜索所有驱动器和连接的网络共享以定位带有EXE或SCR扩展名的文件。这些病毒连接到远程网站并下载其他恶意代码。这些文件中的某些可能会将感染病毒的Serverx.exe文件放入Windows系统文件夹中。这些病毒通过创建以下注册表项来修改系统注册表，以便在启动时运行Serverx.exe文件：

```
"Serverx" = <System>\Serverx.exe
```

这些病毒还可能试图运行<System>\setupx.exe和<System>\Update.exe文件，或者将自己注入内核或当前正在运行的其他进程中。

### 蠕虫和病毒：W32/Hasnot-A

W32/Hasnot-A是一种针对Windows平台的蠕虫和伴随病毒，通过共享网络文件和可移动存储设备（包括USB驱动器）进行传播。该蠕虫试图将自己复制到可访问受感染机器的可写设备中。它通过将自己作为副本附加到文件或文件夹的原始名称来隐藏文件和文件夹。它将自己复制到根驱动器文件夹作为Skynet.exe，并添加一个Autorun.inf文件。一旦驱动器被挂载，Autorun.inf文件被设计为运行Skynet.exe，从而传播蠕虫。当首次运行时，此蠕虫将自己复制到以下文件：

- <Root>\Dokumente und Einstellungen.exe
- <Root>\Documenti e Impostazioni.exe
- <Root>\Documents and Settings.000.exe
- <Root>\Documents and Settings.exe
- <User>\Application Data\Explorer.exe
- <User>\Application Data\Microsoft\WinNT.com
- <Favorites>\svchost.exe
- <Root>\Games.exe
- <Root>\Mijn Documenten.exe
- <Root>\My Downloads.exe
- <Root>\My Music.exe
- <Root>\My Shared Folder.exe
- <Root>\Program Files.exe
- <Root>\Programma's.exe
- <Root>\Programme.exe
- <Root>\Programmi.exe
- <Root>\Programs.exe
- <Root>\SkyNet.exe
- <Root>\System Volume Information.exe
- <Root>\Temp.exe
- <Root>\Tmp.exe
- <Root>\WinNT.exe
- <Root>\inetpub.exe
- <Root>\install.exe
- <Root>\recycled.exe
- <Root>\windows.exe
- <Windows>\_default.pif
- <Windows>\svchost.exe
- <System>\Explorer.exe

创建以下注册表项，以便在启动时运行WinNT.com和_default.pif：

- HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run\"WinNT" = <User>\Application Data\Microsoft\WinNT.com
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\Run\"Graphics" = <Windows>\_default.pif

设置以下注册表项以禁用系统软件：

- HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System\"DisableTaskMgr" = 1
- HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System\"DisableRegistryTools" = 1
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\"DisableTaskMgr" = 1
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\system\"DisableRegistryTools" = 1

W32/Hasnot-A还设置以下注册表项：

- HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\"NoFolderOptions" = 1
- HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Non Enum\"{6DFD7C5C-2451-11d3-A299-00C04F8E6FAF}" = 1
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Explorer\"NoFolderOptions" = 1
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\Hidden\SHOWALL\"CheckedValue" = 1
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\policies\Non Enum\"{6DFD7C5C-2451-11d3-A299-00C04F8E6FAF}" = 1
