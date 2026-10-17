
USB 驱动器有一个常见的设计缺陷：在串行电可擦只读存储器（EEPROM）中不当地存储密码值。USB 设备由一个带有 USB 支持的微处理器、外部内存和胶合电路组成。内存是 EEPROM，它只需要极少的电路和读写；主要用于工程行业。然而，它是不安全的，不能为其所使用的设备提供安全性。因此，设备编程器通过攻击使用安全 EEPROM 的设备，通过限制不当访问来提供安全性。

由于这个缺陷，攻击者可以使用电气攻击（在物理访问 USB 设备板时对 USB 驱动器执行攻击）来提取所有数据，包括私有信息。攻击者的目标是偷取存储在设备上的私有数据，这些数据本应受合法用户的 PIN 和密码保护。攻击后，存储在 EEPROM 中的密码值会被更改，数据可以被轻易地提取。攻击完成后，攻击者将密码重置为原始值，确保 USB 设备的所有者察觉到任何可疑活动。

## 软件攻击

软件攻击是一种非破坏性攻击。在这种攻击中，USB 设备不会被篡改或损坏。相反，软件攻击利用设备的正常条件，其目的是寻找该产品中软件或固件实现中的缺陷。

## 病毒和蠕虫

供应商提供的软件开发包由源代码、头文件以及关于 USB 设备设计和结构的信息组成。这些信息存储在设备的串行 EEPROM 中，由于设计缺陷，允许了访问私有信息。通过启动软件攻击，攻击者尝试使用自定义设备驱动程序和 USB 协议分析仪来检查 USB 设备与主机计算机之间的通信通道，从而获取这些信息。攻击者可以使用这些信息来分析并确定成功攻击的可能性，然后使用以下方法之一：

- 尝试暴力破解密码：通过分析和确定管理员的 `MKEY` 值或原始密码或 PIN 来访问 USB 驱动器。
- 向 USB 驱动器发送错误且已知的错误 USB 数据包：由于设计缺陷，USB 驱动器可能允许传输受保护区域的内容。

一旦攻击完成，结果可以复制到其他设备。

## Windows 缓冲区溢出攻击

插入到带有 Windows 32 位操作系统（如 Windows Vista、XP 和 2000）的计算机上的 USB 设备面临另一种类型攻击的危险。USB 驱动程序中的缓冲区溢出漏洞允许攻击者绕过安全设置并获得对主机的管理权限。知道这些漏洞的攻击者可以使用 USB 驱动器伪装成创建漏洞驱动程序的设备。

一旦完成此操作，攻击者将驱动器插入系统，当有缺陷的驱动程序加载时，攻击者将获得默认 PIN 和存储在设备串行 EEPROM 中的合法用户凭据。攻击者可以使用这些信息来利用系统并访问被锁的工作站。

这些攻击需要对系统的物理访问，可以通过使用 USB 安全工具来防止，这些工具可以识别 USB 设备何时插入主机计算机或网络，并防止漏洞被利用。

这些章节解释了一些影响 USB 设备的病毒和蠕虫。

## 病毒：W32/Mad-Fam

`W32/Mad-Fam` 是一种通过可移动驱动器影响 Windows 系统的病毒。它通过修改驱动器上的 `autorun` 文件或在插入驱动器时将其代码注入系统来传播。它还会修改 Windows 注册表以确保在重启后仍然存在。

## 蠕虫：W32/Hasnot-A

`W32/Hasnot-A` 是一种通过 USB 设备影响 Windows 系统的蠕虫。它通过利用 USB 驱动程序的漏洞或将自身复制到连接的驱动器上来传播。它还可以获得对主机的管理权限。

## 蠕虫与病毒：W32/Fujacks-AK

`W32/Fujacks-AK` 蠕虫和病毒影响 Windows 平台。它通过可用的网络共享和可移动存储设备传播到其他网络计算机。该蠕虫以 `GameSetup.exe` 和 `setup.exe` 为文件名复制自己，并复制 `Autor.inf` 文件以确保 `setup.exe` 执行。它可以访问互联网并通过 HTTP 与远程服务器通信。当该蠕虫首次运行时，它会将自己复制到以下文件：

```
<System>drivers\spocsv.exe
```

```
<Root>setup.exe
```

```
<Root>AutorRun.inf
```

在 `setup.exe` 上创建了以下注册表项：

`HKCU\Software\Microsoft\Windows\CurrentVersion\share = <System>drivers\spocsv.exe`

它还设置了以下注册表项：

```
HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Advanced\Folder\HiddenSHOWALLCheckedValue = 0
```

每当该蠕虫发现 EXE 文件时，它会尝试感染包括管理员共享在内的它们。如果成功，该蠕虫会通过在驱动器上创建一个隐藏文件 `Autor.inf` 将自己复制到包括软磁盘和 USB 驱动器在内的移动驱动器上。该 AutoRun.inf 设计在可移动设备连接到受感染系统时启动蠕虫。

## 蠕虫与病毒：W32/Fujacks-E

`W32/Fujacks-E` 是一种具有后门功能的病毒，影响 Windows 平台。它针对弱密码的网络，通过将自己复制到本地和映射的网络驱动器通过可移动设备传播。它使用 `GameSetup.exe` 和 `setup.exe` 文件名进行复制。它创建 `Autor.inf` 文件以确保 `setup.exe` 执行。该蠕虫持续运行，提供供攻击者访问和控制系统的后门。此外，该蠕虫可以访问互联网并通过 HTTP 与远程服务器通信并更改 HTML 文件。

当该蠕虫首次运行时，它复制到 `<System>drivers\spocsv.exe`。蠕虫为 `setup.exe` 创建了以下注册表项：

```
HKLM\SOFTWARE\Microsoft\CurrentVersion\share = <System>drivers\spocsv.exe
```

它还设置了以下注册表项：

`HKLM\SOFTWARE\Microsoft\CurrentVersion\Explorer\Advanced\Folder\HiddenSHOWALLChecked = 0`

## 病毒：W32/Dzan-C

`W32-Dzan` 是一种影响 Windows 平台的病毒。该病毒通过软磁盘等可移动存储设备传播。它在所有驱动器中搜索 EXE 文件。当发现 EXE 文件时，它会将自己的病毒附加到执行文件中，使其大小增加 66048 字节。每当执行该文件时，后门就会激活。该蠕虫持续运行，提供供攻击者访问和控制系统的后门。

当系统被此病毒感染时，会创建文件：

- `<System>inetinfo.exe`
- `<System>1021\services.exe`

文件 `<System>1021\services.exe` 被注册为一个系统服务。它的显示名称为“Themes and Play”，并在系统启动时自动执行。该病毒在 `HKLM\SYSTEM\CurrentControl\Services` 下创建注册表项以注册该服务。

## 第7 章

## 蠕虫：W32/SillyFD-AA

`W32/SillyFD-AA` 是一种通过软磁盘和 USB 设备等可移动设备传播影响 Windows 平台的蠕虫。它尝试在可移动设备上创建一个名为 `Autorun.inf` 的隐藏文件，并将自己复制到可移动设备上的 `<Root>handdriver.exe`。`Autorun.inf` 设计在设备连接到受感染系统时启动蠕虫。蠕虫将自己复制到下列表的位置：

- `<Roots>\kernel32.exe`
- `<Windows>\regedit.exe`
- `<Windows>\ipchache\helpctr\msconfig.exe`
- `<System>\systeminit.exe`
- `<System>\wininit.exe`
- `<System>\winsystem.exe`
- `<System>\cmd.exe`
- `<System>\taskmgr.exe`

设置以下启动注册表项：

- `HKLM\SOFTWARE\Microsoft\CurrentVersion\Winlogon\Userinit = <System>\userinit.exe`
- `HKLM\SOFTWARE\Microsoft\CurrentVersion\Run = <System>\wininit.exe`

还设置了以下注册表项：

- `HKCU\Software\Microsoft\Internet\Main\Window Title = Hacked by 1BYTE`
- `HKCU\Software\Microsoft\ServicePack = 1.2`
- `HKCU\Software\Microsoft\CurrentVersion\Explorer\SearchHidden = 0`
- `HKCU\Software\Microsoft\CurrentVersion\Explorer\SearchSystemDirs = 0`
- `HKCU\Software\Microsoft\CurrentVersion\Policies\Explorer\NoFolderOptions = 1`
- `HKCU\Software\Microsoft\CurrentVersion\Policies\System\DisableRegEdit = 1`
- `HKCU\Software\Microsoft\CurrentVersion\Policies\System\DisableTaskManager = 1`
- `HKCU\Software\Microsoft\Flag = 1`
- `HKCU\Software\Microsoft\CurrentVersion\Explorer\Advanced\Hidden = 1`
- `HKCU\Software\Microsoft\CurrentVersion\Explorer\Advanced\HideFileExt = 1`
- `HKCU\Software\Microsoft\CurrentVersion\Explorer\Advanced\ShowHidden = 0`
- `HKCU\Software\Microsoft\CurrentVersion\Policies\Explorer\NoDriveAutoRun = 0`
- `HKCU\Software\Microsoft\CurrentVersion\Policies\Explorer = 0`
- `HKLM\System\CurrentControlSet\SharedAccess\Start = 1`

## 蠕虫：W32/SillyFD-BC

`W32/SillyFD-BC` 是一种通过可移动设备传播的蠕虫。执行时，该蠕虫会将自己复制到 `<Root>\rag.exe` 并在 `<Root>\Autorun.inf` 创建文件。`Autorun.inf` 设计在设备连接到受感染系统时执行蠕虫。该蠕虫还设置了启动注册表项：

`HKLM\SOFTWARE\Microsoft\CurrentVersion\Run"K" = <Windows>\rag.exe`

## 蠕虫：W32/Liar-A

`W32/Liar-A` 影响 Windows 平台。它通过软磁盘和 USB 驱动器等可移动存储设备传播。它将自己复制到设备的根目录并添加 `Autorun.inf` 文件。`Autorun.inf` 文件设计在可移动设备挂载时启动蠕虫。此文件不会对你的电脑做出任何有害更改。此文件不会干扰你电脑或优盘（USB）上的任何数据或文件。所以不要害怕，会快乐的！此蠕虫将自己复制到以下位置：

- `<Open>\Folder=exe`
- `<Root>\Boot.exe`
- `<Root>\log.exe`
- `<Windows>\ErrorReport`
- `<Windows>\Monitor`
- `<Windows>\Setup.exe`
- `<Windows>\WinSystem`
- `<Windows>\Windows.exe`
- `<System>\WindowsProtection.exe`

此蠕虫还会创建以下文件：

- `<System>\oem`
- `<System>\oem`

此蠕虫可能创建以下注册表项：

- `HKCR\shell\Command<Root>\windows\Monitor.run`
- `HKCR\Folder\shell<Root>\windows\Monitor.run`
- `HKCR\Folder\shellCommand<Root>\windows\Monitor.run`
- `HKCU\Software\Kyrent`

## 蠕虫：W32/Hairy-a

`W32/Hairy-a` 是一种影响 Windows 平台的蠕虫，它通过软磁盘和 USB 设备等可移动设备传播。它在可移动设备上创建一个名为 `Autorun.inf` 的隐藏文件，并将自己复制到可移动设备上的 `<Root>handdriver.exe`。`Autorun.inf` 设计在设备连接到受感染系统时启动蠕虫。当系统被此蠕虫感染时，会创建文件：

- `<Root>\HarryPotter-TheDeathallows.doc`
- `<Root>\AutoRun.inf`
- `<Root>\harry potter.txt`
- `<Windows>\Tempt`

以下注册表项用于启动 `talk.bat`：

`HKLM\SOFTWARE\Microsoft\CurrentVersion\Run = <Windows>\Tempt\talk.bat`

该蠕虫通过修改以下注册表项影响 Microsoft Internet Explorer：

- `HKCU\Software\InternetExplorer\Main`
- `HKCU\SOFTWARE\InternetExplorer\MainStartPage`
- `HKLM\SOFTWARE\InternetExplorer\Main\StartPage`

通过设置以下注册表项影响网络安全：

通过设置以下注册表项禁用系统：

- `HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System\DisableTaskMgr = 1`
- `HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\System\DisableRegistryTools = 1`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DisableTaskMgr = 1`

`lhxl.bat` 是一个干净的文件，可以被删除。在 `System\jusodl.dll` 文件中检测到 `Troj/QQRob-ACM`，`Autorun` 文件被检测为 `W32/QQRob-ADN`。

该病毒尝试通过修改 HOSTS 文件来阻止对安全相关文件的访问。此外，为了在启动时运行 `jusodle.exe` 和 `server`，它创建了以下注册表项：

- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\pnvif" = "System\jusodle"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run\pnvif" = "System\server.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\360Safe.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\EGHOST.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\Icesword.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\KRegEx.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\KV-MonXP.kvp,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\KVDetect.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\KXP.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\MagicSet.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\NOD32.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\PFW.exe,Debugger" = "System\drivers\pnvif.exe"`
- `HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Image Execution Options\PFWLive-Update.exe,Debugger" = "System\drivers\pnvif.exe"`
