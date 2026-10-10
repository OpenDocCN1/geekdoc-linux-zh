
- 名称：`oompa`
- 值：`loompa`

此蠕虫创建以下临时文件：
- `/tmp/pic.gz`
- `/tmp/pic`
- `/tmp/latestpics`
- `/tmp/latestpics.tar`
- `/tmp/latestpics.tar.gz`
- `/tmp/latestpics.tgz`
- `/tmp/apphook` 下的若干文件

## Inqtana.A：F-Secure 蠕虫

基于 Java 的 Inqtana.A 蠕虫通过蓝牙传播，影响未受保护的 Mac OS X 10.4 系统。此蠕虫以 OBEX 推送请求的形式到达，需要用户接受传输的数据。一旦传输完成，蠕虫便利用目录遍历漏洞复制其文件。然后，该蠕虫在重启时激活。激活的蠕虫会搜索接受 OBEX 推送传输的设备，并将自身发送到这些设备上。文件 `com.openbundle.plist` 和 `com.pwned.plist` 被放置在一个系统启动时可以被调用的位置。`openbundle.plist` 文件解压蠕虫组件，而 `com.pwned.plist` 执行蠕虫。

## 针对 OS X Inqtana.A 的预防措施

OS X/Inqtana.A 仅影响 Mac OS X 10.4。为了在 OS X 10.4 中保护系统免受此蠕虫的侵害，请执行以下步骤：
1. 通过安装 Apple 的更新来修补系统。
2. 删除以下已被蠕虫入侵的文件：
   - `/Users/worm-support.tgz`
   - `/Users/InqTest.class`
   - `/Users/com.openbundle.plist`
   - `/Users/com.pwned.plist`
   - `/Users/libavetanaBT.jnilib`
   - `/Users/javax`
   - `/Users/ld`
   - `/Users/[username]/Library/LaunchAgents/com.pwned.plist`
   - `/Users/[username]/Library/LaunchAgents/com.openbundle.plist`

## Mac 中的病毒：宏病毒

宏病毒对 Macintosh 用户构成了巨大危险。第一个真正的宏病毒攻击了 Microsoft Word 文件，随后宏病毒迅速流行起来。即使随着用户意识的提高，由于 Microsoft 软件的普遍性，这些病毒仍继续造成巨大损害。宏病毒被创建用于攻击其他 Microsoft 应用程序，如 Excel、Visio、PowerPoint 和 Access，但 Microsoft Word 病毒是最流行的。宏病毒是一个真实的威胁，因为它们在不同平台上都有效；它们可以破坏 Macintosh 和 Windows 系统。

针对 Microsoft Word 文件的宏病毒使用诸如 `AutoOpen`、`AutoClose`、`AutoExec` 和 `AutoExit` 等命令。这些命令在处理文件时发生事件时执行。当文件被打开和执行时，它们会传播。宏病毒在打开文件时复制到活动模板（通常是“Normal”模板）。如果模板未打开，该文件会将自己复制到后台打开的模板中。宏病毒可能在系统中造成严重破坏，破坏文件，更改文件类型和部分菜单项，或者使得模板无法编辑。然后，病毒复制到从受损模板打开或保存的新文件中。宏病毒破坏或删除文件，甚至隐藏某些应用程序。通过删除活动模板（在大多数情况下是默认“Normal”模板）和受损文件，可以移除此类病毒。

## Mac OS X 中的防病毒应用

### VirusBarrier

`VirusBarrier`（图 2-2）是一种非侵入式防病毒软件程序，通过不断检查它读取和写入的所有文件，保护 Mac 免受包括宏病毒和针对操作系统病毒在内的所有类型病毒的侵害。它还巡逻以检测可能表明病毒正在作用于应用程序或其他文件的可疑活动。它可以修复或隔离受感染的文件，并显示警报。`VirusBarrier` 可以按需或在正常操作期间在后台扫描。它有一个选项，可以跳过自上次扫描以来未更改的文件。

`VirusBarrier` 的一些其他功能包括以下方面：
- 启发式和行为分析
- 指定的“信任区域”，在此区域内可禁用对选定文件或文件夹的后台扫描
- 改进日志记录以更好地分析扫描
- 扫描可安排多个时间点
- 当卷被挂载或病毒定义更新时，扫描可自动启动
- 用于远程扫描的命令行控制
- 可通过归档类型激活归档扫描
- 扫描文件中的 Windows 病毒（可禁用）
- 阻止病毒执行
- 接收和发送邮件时扫描电子邮件
- 由 Intego 病毒监控中心进行文件分析
- 用于快速扫描的上下文菜单
- 完整日志可以保存和导出
- 用于程序和更新状态的 Intego 小部件
- 用于更快扫描的 Turbo Mode 技术
- 警报选择（语音、对话框或电子邮件）
- 从 Dock 进行文件分析

### McAfee VirusScan for Mac

`McAfee VirusScan for Mac`（图 2-3）防范所有类型的病毒和恶意代码，包括可能影响 OS X 的新兴和未知威胁及新兴恶意软件。`VirusScan for Mac` 保护系统免受病毒、蠕虫、木马和其他可能感染系统的恶意代码的侵害。`VirusScan for Mac` 提供对多个文件、目录或卷（包括网络计算机上的卷）的策略执行。在 McAfee 产品中，按需扫描和后台扫描都是可选项。`VirusScan` 可以扫描压缩文件，并使用高级启发式和通用检测，保护系统免受新病毒和其他威胁的侵害。

### Sophos Endpoint Security and Control

`Endpoint Security and Control` 通过自动电子邮件警报警告网络中的爆发风险。它是一个防病毒、反间谍软件和客户机防火墙。Sophos 可以保护 Windows、Mac 和 Linux 机器，并为台式机、笔记本电脑、文件服务器和移动设备提供跨平台的安全性和控制。它保护系统免受病毒、间谍软件和广告软件的侵害，并控制 VoIP、IM、P2P 和游戏。当新计算机加入网络时，安全策略会自动执行。这消除了未受保护的计算机破坏安全策略的风险。`Endpoint Security and Control` 包含独特的 Behavioral Genotype 保护功能，防范新的、不可预见的病毒、蠕虫和其他威胁。

![](img/0c79e6db97822eb68322dfe40d8564fe_73_0.png)

**图 2-2** 此屏幕显示 ViruBarrier 服务器管理员选项。

![](img/0c79e6db97822eb68322dfe40d8564fe_73_1.png)

**图 2-3** 此屏幕显示 DropScan 的扫描和清理选项。

### Norton Internet Security

`Norton Internet Security`（图 2-4）提供防病毒保护、互联网蠕虫保护、个人防火墙、隐私保护和 parental 控制。它自动检测并移除来自互联网下载和电子邮件附件中的病毒、木马和蠕虫。NIS 的一些其他功能包括以下方面：
- 个人防火墙允许用户控制所有传入和传出互联网流量。
- 隐私控制防止信息在未获用户许可的情况下被发送。
- 自动阻止黑客和身份窃贼。
- 父母控制阻止用户不希望其孩子访问的网站。
- 通过删除不需要的 cookie 和缓存文件来保护隐私并节省磁盘空间。

## Mac OS X 安全工具

### MacScan

`MacScan` 使用高级检测方法隔离和卸载可能危害安全的程序。黑客使用的远程管理程序允许远程访问计算机。这些程序通常未被检测到，因为防病毒软件通常不保护免受间谍软件侵害。使用远程访问，黑客可以使用击键记录器监控用户活动、操纵文件或锁定合法用户。`MacScan` 可以黑名单跟踪 cookie 以阻止这些黑客，并通知用户任何可能正在活动的间谍软件应用程序。`MacScan` 定期更新间谍软件定义，以保护系统免受最新间谍软件的侵害。它还审计和保护系统免受可能无意中遗留或安装的远程管理程序的侵害。图 2-5 显示了 `MacScan` 应用程序屏幕。

### ClamXav

`ClamXav` 是一款用于 Mac OS X 的病毒检查器。`ClamXav` 基于免费的 `ClamAV` 开源命令行防病毒引擎构建。该软件具有在计算机上移动文件的能力；因此，完整的安全……

在运行 `ClamXav` 之前，会先对任何重要数据执行备份。`ClamXav` 运行于 PPC Mac 的 10.3 和 10.4 版本，以及 Intel Mac 的 10.4 版本。它通过 Apple 安装的 `ClamAV` 引擎在 OS X Server 上运行。其他功能包括将结果记录到文件中、将受感染文件移入隔离区，以及监控文件夹内容变化。图 2-6 展示了 `ClamXav` 检测到的蠕虫。

![](img/0c79e6db97822eb68322dfe40d8564fe_75_0.png)

![](img/0c79e6db97822eb68322dfe40d8564fe_75_1.png)

## IPNetSentryX
