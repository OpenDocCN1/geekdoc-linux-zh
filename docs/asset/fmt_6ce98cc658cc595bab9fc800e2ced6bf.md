
^468 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/api/msdk/wmic

^469 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/wmisdk/wmi-start-page

^470 (Microsoft, 2015) https://docs.microsoft.com/en-us/previous-versions/windows/desktop/legacy/aa394378(v=vs.85)

^471 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/msi/windows-installer-portal

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

同样，更重要的是，`wmic` 还可以通过查询 `Win32_QuickFixEngineering` (`qfe`)[^472] WMI 类来列出系统范围的更新。

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

`HotFixID` 和 `InstalledOn` 信息的组合可以为我们提供目标 Windows 操作系统安全状态的精确指示。根据此输出，该系统最近未进行更新，这可能会使其更容易被利用。

基于 Linux 的系统使用多种包管理器。例如，基于 Debian 的 Linux 发行版使用 `dpkg`[^473]，而基于 Red Hat 的系统使用 `rpm`[^474]。

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
