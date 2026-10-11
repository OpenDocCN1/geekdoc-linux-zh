
| 名称 | 公司 | 版本 | 构建 |
| :--- | :--- | :--- | :--- |
| Microsoft Office OSM UX MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Office 共享安装元数据 MUI | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Excel MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft PowerPoint MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Publisher MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Outlook MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Groove MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Word MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Office 校对 (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Office 共享组件 MUI (English) 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Office 校对工具 2016 – Microsoft 校对工具 Outils de vérification linguistique 2016 | Microsoft Corporation | 16.0.4266.1001 | |
| Microsoft Visual C++ 2017 x86 附加组件 | Microsoft Corporation | 14.12.25810 | |
| FortiClient | Fortinet Inc | 5.2.3.0633 | |
| Python 2.7.7.14 | Python Software Foundation | 2.7.14150 | |
| VMware Tools | VMware, Inc. | 10.3.10.1240696 | |
| Microsoft Visual C++ 2017 x86 最小配置 | Microsoft Corporation | 14.12.25810 | |
| Microsoft Visual C++ 2008 可再发行组件 | Microsoft Corporation | 9.0.30729.4148 | |

*列表 535 - 列出 Windows 上安装的所有应用程序*

关于已安装应用程序的信息可能有助于我们寻找特权提升攻击。

同样，更重要的是，*wmic* 还可以通过查询 *Win32_QuickFixEngineering* (*qfe*)[^472] WMI 类来列出系统范围的更新。

```bash
c:\Users\student>wmic qfe get Caption, Description, HotFixID, InstalledOn
```

| 标题 | 描述 | HotFixID | 安装日期 |
| :--- | :--- | :--- | :--- |
| http://support.microsoft.com/?kbid=4088785 | 安全更新 | KB82693643 | 4/7/2018 |
| http://support.microsoft.com/?kbid=4090914 | 更新 | KB4088785 | 3/31/2018 |
| http://support.microsoft.com/?kbid=4088776 | 安全更新 | KB4999914 | 3/31/2018 |
| http://support.microsoft.com/?kbid=4088776 | 更新 | KB4088776 | 3/31/2018 |

*列表 536 - 列出 Windows 上安装的所有安全补丁*

*HotFixID* 和 *InstalledOn* 信息的组合可以为我们提供目标 Windows 操作系统安全状态的精确指示。根据此输出，该系统最近未进行更新，这可能会使其更容易被利用。

基于 Linux 的系统使用多种包管理器。例如，基于 Debian 的 Linux 发行版使用 *dpkg*[^473]，而基于 Red Hat 的系统使用 *rpm*[^474]。

要列出在 Debian 系统上已安装（通过 dpkg）的应用程序，我们可以使用 `dpkg -l`。

```bash
student@debian:~$ dpkg -l
Desired=Unknown/Install/I
Remove
/Purge/Hold
| Status=Not/Inst/Conf-files
/Unpacked/half-cnf/half-inst/trig-aWait/Trig-pend
| / Err?= (none)/Reinst-required
(Status,Err:
uppercase=bad)
|| Name Version Architecture Description
+++=
=============
==========================
==========
======
=
=
===
=
i i acl 2.2.52-3+b1 i386 Access control list utilities
```

[^472]: (Microsoft, 2018). https://docs.microsoft.com/en-us/windows/win32/cimwin32prov/win32-quickfixengineering

[^473]: (Linux.die.net, 2003). https://linux.die.net/man/1/dpkg

[^474]: (Marc Ewing, 2003). https://linux.die.net/man/8/rpm

| | | | | |
|---|---|---|---|---|
| ii aduser | 3.1.15 | all | 添加和删除用户及组 | |
| ii adwaita-icon-theme | 3.22.0-1+deb9u1 | all | GNOME 默认图标主题 | |
| ii alsa-utils | 1.1.3-1 | i386 | 用于配置和 ... 的工具 | |
| ii anacron | 2.3-24 | i386 | 类似 cron 但不要求 ... 的程序 | |
| ii ant | 1.9.9-1 | all | 类似于 ma 的基于 Java 的构建工具 | |
| ii ant-optional | 1.9.9-1 | all | 类似于 ma 的基于 Java 的构建工具 | |
| i1 apache2 | 2.4.25-3+deb9u4 | i386 | Apache HTTP 服务器 | |
| ii apache2-bin | 2.4.25-3+deb9u4 | i386 | Apache HTTP 服务器 (模块 a ... | |
| ii apache2-data | 2.4.25-3+deb9u4 | all | Apache HTTP 服务器 (公共 fi ... | |
| ii apache2-utils | 2.4.25-3+deb9u4 | i386 | Apache HTTP 服务器 (实用程序 p ... | |
| | | | ... | |

*列表 537 - 列出 Debian Linux 操作系统上已安装的所有软件包*

这证实了我们之前的预期：Debian 机器实际上正在运行一个 Web 服务器。在这种情况下，它运行的是 Apache2。

### 18.1.1 9 枚举可读/可写的文件和目录

正如我们之前提到的，访问限制不足的文件可能会创建漏洞，从而可能使攻击者获得提权。这种情况最常发生在攻击者能够修改在特权账户上下文下执行的脚本或二进制文件时。

此外，非特权用户可读的敏感文件可能包含重要信息，例如数据库或服务账户的硬编码凭据。

由于手动检查每个文件和目录的权限是不现实的，我们需要尽可能自动化这一任务。

有许多实用程序和工具可以在 Windows 平台上帮助我们自动化这一任务。来自 SysInternals 的 AccessChk[^475] 可能是为此目的最知名且经常使用的工具。

在接下来的示例中，我们将演示如何使用 AccessChk 在 **Program Files** 目录中找到具有不安全文件权限的文件。请注意，目标二进制文件仅为演示此练习的目的而创建。

具体而言，我们将枚举 **Program Files** 目录，以查找允许 *Everyone*[^476] 组拥有写入权限的任何文件或目录。

我们将使用 **-u** 来抑制错误，**-w** 来搜索写入访问权限，并 **-s** 来执行递归搜索。由于该工具非常有用，其他选项也值得探索。

```text
c:\Tools\privilege_escalation\SysinternalsSuite>accesschk.exe -uws "Everyone" "C:\Program Files"

Accesschk v6.12 - Reports effective permissions for securable objects
Copyright (C) 2006-2017 Mark Russinovich
Sysinternals - www.sysinternals.com

Rw C:\Program Files\TestApplication\testapp.exe
```

[^475]: (Microsoft, 2017). https://docs.microsoft.com/en-us/sysinternals/downloads/accesschk

[^476]: (Microsoft, 2019). https://docs.microsoft.com/en-us/windows/win32/secauthz/well-known-sids

*列表 538 - 列出指定目标中所有可写的文件和目录*

在上面的列表中，AccessChk 成功识别了一个可全局写入的可执行文件。如果此文件由特权用户或服务账户执行，我们可以尝试用我们选择的恶意文件（例如反向 shell）覆盖它，以提升我们的权限。我们将在本模块的后文展示一个类似的工作示例。

我们也可以使用 PowerShell 实现相同的目标。这在某些情况下非常有用，例如当我们可能无法在目标系统上传输和执行任意二进制文件时。

PowerShell 命令本身（如下在列表 539 中所示）可能看起来有点复杂，因此我们将逐步介绍这些选项。

我们要使用的主要 cmdlet 是 **Get-Acl**，它检索给定文件或目录的所有权限。然而，由于 Get-Acl 不能递归运行，我们还使用 **Get-ChildItem** cmdlet 先枚举 **Program Files** 目录下的所有内容。这将有效地检索目标目录中的每个对象及其所有相关访问权限。带有 **-match** 标志的 **AccessToString** 属性将结果缩小到我们正在寻找的特定访问属性。在我们的情况下，我们正在搜索任何可以被 Everyone 组成员修改 (Modify) 的对象。

```powershell
PS C:\Tools\privilege_escalation\SysinternalsSuite>Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\sModify"}
```

Directory: C:\Program Files\TestApplication

| 路径 | 所有者 | 访问 |
|---|---|---|
| **testapp.exe** | BUILTIN\Administrators | Everyone Allow Modify, Synchronize... |

*列表 539 - 使用 PowerShell 列出指定目标中所有可写的文件和目录*

在这种情况下，输出与 AccessChk 的输出相同。此命令序列允许额外的格式选项。

在 Linux 操作系统中，我们可以使用 **find**[^477] 来识别具有不安全权限的文件。

在下面的示例中，我们正在搜索目标系统上当前用户可写的每个目录。我们搜索整个根目录 (*/*) 并使用 **-writable** 参数来指定我们感兴趣的属性。我们还使用 **-type d** 来定位目录，并使用 **2>/dev/null** 来过滤错误：

```bash
student@debian:~$ find / -writable -type d 2>/dev/null
/usr/local/james/bin
/usr/local/james/bin/lib
/proc/16195/task/16195/fd
/proc/16195/fd
/proc/16195/map_files
/home/student
/home/student/.gconf
```

[^477]: (Linux man-pages project, 2019), http://man7.org/linux/man-pages/man1/find.1.html
