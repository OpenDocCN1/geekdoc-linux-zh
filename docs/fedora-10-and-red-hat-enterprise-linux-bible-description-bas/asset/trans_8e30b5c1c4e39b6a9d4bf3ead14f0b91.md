

# 第 5 章：访问和运行应用程序

系统主要用于 Web 浏览和电子邮件。通过 Linux，部署了数百甚至数千个系统的企业可以对员工系统中的安全性和功能拥有极大的控制力。此外，可以使用 `ssh` 进行远程 Linux 管理，`ssh` 提供了加密和身份验证，并具有 Linux 终端壳的所有优点。

从长远来看，随着 Linux 系统对病毒和恶意软件变得更具可利用性，学习使用软件、文件所有权/权限以及监控系统资源的良好实践将变得更加重要。然而，此类工具（包括病毒扫描器，如 `clamav` 和 `clamscan`）对于任何选择包含它们的 Linux 系统来说已经可用了。（欲了解更多信息，请参阅 http://www.clamav.net 和 http://clamav.sourceforge.net。）

- 一个庞大的开发社区正在开发开源应用程序以满足社区的需求。如果你觉得有公司为你的关键任务应用程序提供支持会更有安全感，为 Red Hat 系统提供了一些商业化软件产品（http://www.redhat.com/apps/isv_catalog）。

底线是，对于大多数人来说，完全放弃 Microsoft Windows 操作系统仍需要付出一些努力。如果你致力于将 Fedora 作为你唯一的应用程序平台，有几种方法可以缓解这种过渡。仿真程序可以让你运行许多为其他操作系统创建的程序。转换程序可以帮助将其他格式的图形和文字处理数据文件转换为 Linux 应用程序支持的格式。

> 交叉引用：请参见第 6 章有关导入和导出文字处理和图形文件的信息。

如果你在 PC 上运行 Linux，那么你很可能已经为 Microsoft Windows 95, 98, ME, XP, NT, 2000 或 Vista 操作系统付过费。你可以在与运行 Windows 不同的 PC 上运行 Linux，也可以在同一块硬硬盘的不同分区上同时拥有 Windows 和 Linux。后者要求你在每次切换操作系统时都要重新启动。（请参见第 2 章获取有关设置 Linux/Windows 双启动系统的信息。）最近增加了第三种选择，即你可以在 Linux 桌面面上运行虚拟的 Windows 系统（见本章后文关于 `Xen` 和 `KVM` 的描述）。

本节介绍了在 Fedora 中运行的应用程序，你可以使用它们来替换以前使用的 Windows 应用程序。

## 在 Linux 中寻找常见的桌面应用程序

如果你打算将 Linux 作为桌面计算机系统，你将需要编写文档、处理图形和计算数字。你可能还有其他喜欢的应用程序，如音乐播放器、Web 浏览器和电子阅读器。

## 第二部分：使用 Fedora 和 RHEL

> 注意：利用 `WINE` 技术，`Codeweavers, Inc.` 的人员提供了一种 `CrossOver` 产品，让你可以在 Linux 中安装和运行 Microsoft Office。参见本章中的“带有 WINE 的 Windows 应用程序”部分。

为了让你了解有哪些桌面应用程序可用，表 5-3 列出了热门 Windows 应用程序、等效的 Linux 应用程序以及在哪里找到这些 Linux 应用程序。尽管这些应用程序许多尚未达到其 Windows 对应品的复杂程度，但它们可以作为高性价比的替代方案。

## 表 5-3：Windows 等效 Linux 应用程序

| Windows 应用程序 | Linux 应用程序 | 获取 Linux 应用程序的地方 | 费用 |
| --- | --- | --- | --- |
| Microsoft Office (办公效率套件) | OpenOffice (openoffice.org) | 包含在 Fedora DVD 中 | 免费 |
| | Office | 包含在 Fedora DVD 中 | 免费 |
| | StarOffice | www.sun.com/staroffice | $69.95 |
| Microsoft Word (文字处理器) | OpenOffice.Writer | 包含在 Fedora DVD 中 | 免费 |
| | AbiWord | 包含在 Fedora DVD 中 | 免费 |
| | kword | 包含在 Fedora DVD 中 | 免费 |
| Microsoft Excel (电子表格) | OpenOffice.Calc | 包含在 Fedora DVD 中 | 免费 |
| | gnumeric | 包含在 Fedora DVD 中 | 免费 |
| | kspread | 包含在 Fedora DVD 中 | 免费 |
| Microsoft PowerPoint (演示文片) | OpenOffice.Impress | 包含在 Fedora DVD 中 | 免费 |
| | kpresenter | 包含在 Fedora DVD 中 | 免费 |
| Microsoft Internet Explorer (浏览器) | firefox | 包含在 Fedora DVD 中 | 免费 |
| | seamonkey | 包含在 Fedora DVD 中 | 免费 |
| | epiphany | 包含在 Fedora DVD 中 | 免费 |
| | konquer | www.opera.com | 免费 |
| Microsoft Outlook (邮件阅读器) | evolution | 包含在 Fedora DVD 中 | 免费 |
| | kmail | 包含在 Fedora DVD 中 | 免费 |
| | thunderbird | 包含在 Fedora DVD 中 | 免费 |
| | Seamonkey Mail | 包含在 Fedora DVD 中 | 免费 |
| | Mozilla Lightning | www.mozilla.org | 免费 |

| Windows 应用程序 | Linux 应用程序 | 获取 Linux 应用程序的地方 | 费用 |
| --- | --- | --- | --- |
| Adobe Photoshop (图像编辑器) | Gimp | 包含在 Fedora DVD 中 | 免费 |
| Microsoft Expression (HTML 编辑器) | NX | 包含在 Fedora DVD 中 | 免费 |
| Quickicker (个人财务) | gnash | 包含在 Fedora DVD 中 | 免费 |
| AutoCAD (计算机辅助设计) | LinuxCad | www.linuxcad.com | $89 |
| | ProEngineer | www.siemens.com/automation | 免费 |
| | | www.ptc.com/proengineer/ | 免费 |

以下章节介绍了在 Fedora 中运行的应用程序，你可以使用它们来替换你以前使用的 Windows 应用程序。

## 在 Linux 中寻找常见的桌面应用程序

如果你打算将 Linux 作为桌面计算机系统，你将需要编写文档、处理图形和计算数字。你可能还有其他喜欢的应用程序，如音乐播放器、Web 浏览器和电子阅读器。

## 第二部分：使用 Fedora 和 RHEL

> 注意：利用 `WINE` 技术，`Codeweavers, Inc.` 的人员提供了一种 `CrossOver` 产品，让你可以在 Linux 中安装和运行 Microsoft Office。参见本章中的“带有 WINE 的 Windows 应用程序”部分。

为了让你了解有哪些桌面应用程序可用，表 5-3 列出了热门 Windows 应用程序、等效的 Linux 应用程序以及在哪里找到这些 Linux 应用程序。尽管这些应用程序许多尚未达到其 Windows 对应品的复杂程度，但它们可以作为高性价比的替代方案。

