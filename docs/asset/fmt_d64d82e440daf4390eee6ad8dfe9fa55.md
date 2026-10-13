
接下来，你需要决定使用哪个脚本。下表可以告诉你：

## 表 8-1 LDAP 迁移

| 现有名称服务 | LDAP 是否运行？ | 使用此脚本： |
| :--- | :--- | :--- |
| `/etc`平面文件 | 是 | `migrate_all_on-line.sh` |
| `/etc` 平文件 | 否 | `migrate_all_of-fline.sh` |
| NetInfo | 是 | `migrate_all_net-info.sh` |
| NetInfo | 否 | `migrate_all_net-offline.sh` |
| NIS (YP) | 是 | `mi-grate_all_nis-on-line.sh` |
| NIS (YP) | 否 | `mi-grate_all_nis-of-fline.sh` |

根据你现有的名称服务运行相应的脚本。

`/usr/share/openldap` 中的 `README` 和 `migration-tools.txt` 文件提供了更多细节。

## 8.10 网络上的 LDAP

网上有很多关于 LDAP 的有用信息。在你的系统上设置 LDAP 之前，请查看 OpenLDAP 网站和 LDAP HOWTO。

- OpenLDAP: http://www.openldap.org
- 密歇根大学: http://www.umich.edu/~-dirsvcs/ldap
- SLAPD 和 SLURPD 管理员指南 http://www.umich.edu/~-dirsvcs/ldap/doc/guides/slapd
- Innosoft/Critical Angle: http://www.innosoft.com/ldapworld
- Jeff Hodges LDAP 路线和 FAQ: http://www.kingsmountain.com/ldapRoadmap.shtml
- PADL (nss_ldap, pam_ldap 和 yplldap): http://www.padl.com/
- auth_ldap: http://www.rudedog.org/auth_ldap/1.4/auth_ldap.html
- LDAP HOWTO: http://www.linuxdoc.org/HOWTO/LDAP-HOWTO.html
- Sendmail 8.89.使用 LDAP 进行地址查找: http://www.stanford.edu/~bense/Inst.html
- 使用个人 LDAP 服务器、Apache Web 服务器和 PHP 管理你的个人电子邮件通讯录: http://www.webtechniques.com/archives/1999/05/junk/junk.shtml

# 第二部分 安装相关参考

## 第 9.1 节：你应该知道的事

## 9 为文本模式安装做准备

### 9.1 你应该知道的事

在尝试安装 Red Hat Linux 之前，您应该收集一些系统信息，以防止安装过程中出现任何意外情况。您可以在系统随附的文档中，或从系统供应商或制造商处找到大部分此类信息。

Red Hat Linux 支持的最新硬件列表可以在 http://www.redhat.com/hardware 找到。在继续操作之前，检查您的硬件是否与此列表匹配是一个好主意。

> 注意
> 您可以按照本章以及第 10 节“通过文本模式安装 Red Hat Linux”中的说明，对 Red Hat Linux 6.2 进行文本模式安装。但是，如果你从 CD-ROM 安装，你可能更倾向于使用图形安装模式，它既提供了易用性，又提供了灵活的自定义安装模式。有关图形安装的更多信息，请参阅《官方 Red Hat Linux 安装指南》。

> 提示
> 在《官方 Red Hat Linux 安装指南》的“开始之前”章节末尾，有一张表格供您填写特定的系统要求，这将帮助您掌握安装过程中可能需要的任何信息。

## 第 9 章：为文本模式安装做准备

### 9.1.1 基础硬件配置

您应该对计算机中安装的硬件有一个基本的了解，包括：

- 硬盘 -- 具体来说，数量、大小和类型。如果你有多个硬盘，知道哪一个是第一个、第二个等将很有帮助。如果了解你的驱动器是 IDE 还是 SCSI 也是好的。如果你有 IDE 驱动器，应该检查计算机的 BIOS，查看你是否以线性模式访问它们。请参阅您的计算机文档以获取访问 BIOS 的正确键键。请注意，您的计算机 BIOS 可能会通过其他名称称为线性模式，例如“大磁盘模式”。再次，应咨询计算机文档以进行说明。
- 内存 -- 计算机中安装的 RAM 容量。
- CD-ROM -- 最重要的是单元的接口类型（IDE、SCSI 或其他接口），对于非 IDE、非 SCSI 的 CD-ROM，还需要其品牌和型号数字。IDE CD-ROM（也称为 ATAPI）是最近制造的 PC 计算机中最常见的类型。
- SCSI 适配器（如果有） -- 适配器的品牌和型号数字。
- 网卡（如果有） -- 显卡的品牌和型号数字。
- 鼠标 -- 鼠标的类型（串口、PS/2 或总线鼠标）、协议（Microsoft、Logitech、MouseMan 等）以及按钮数量；此外对于鼠标，还有它连接的串口。

在许多较新的系统中，安装程序能够自动识别大多数硬件。然而，为了起起见，收集这些信息仍然是一个好习惯。

### 使用 Windows 了解你的硬件

如果你的计算机已经在运行 Windows 9x，可以使用以下步骤获取额外的配置信息：

## 图 9–1 Windows 系统属性

![](img/a62cd8edb5919f938a546de403f602c6_198_0.png)

在此时，您可以双击图标（或单击加号+）来详细查看每个条目。请查看以下图标下的内容以获取更多信息：

## 图 9–2 Windows 95 下的设备管理器

![](img/a62cd8edb5919f938a546de403f602c6_198_0.png)

## 第 10 章：通过文本模式安装 Red Hat Linux

图 10–2，“磁盘德鲁士（Disk Druid）”中的安装程序小部件展示了你将看到的屏幕。

图 10–1 “配置 TCP/IP”中的安装程序小部件

![](img/a62cd8edb5919f938a546de403f602c6_205_0.png)

复选复选框 (Check Box)

### 第 10.1 节：安装程序用户界面

图 10–2，“磁盘德鲁士（Disk Druid）”中的安装程序小部件

![](img/a62cd8edb5919f938a546de403f602c6_206_0.png)

- 窗口 (Window) -- Windows（在本手册中通常称为对话框）在整个安装过程中显示在你的屏幕上。有时，一个窗口可能会覆盖另一个窗口；在这种情况下，你只能与顶部的窗口进行交互。当在该窗口中操作完成后，它将会消失，允许你继续在下面的窗口中工作。
- 文本输入 (Text Input) -- 文本输入行是你输入安装程序所需的文本信息的地方。当光标停留在文本输入行上时，你可以在该行上输入和/或编辑信息。
- 复选框 (Check Box) -- 复选框允许你选择或取消选择某项功能。框中显示星号（已选择）或空格（未选择）。当光标在复选框内时，按 [Space] 键可以选择一个未选的功能或取消选择已选的功能。
- 文本小部件 (Text Widget) -- 文本小部件是用于显示文本的屏幕区域。有时，文本小部件可能包含其他小部件，例如复选框。如果文本小部件包含的信息超过其预留空间的显示范围，则会出现滚动条；如果你将光标置于文本小部件内，就可以使用 [Up] 和 [Down] 方向键滚动查看所有可用信息。你的当前位置通过 # 字符显示在滚动条上，随着你的滚动，该字符会在滚动条上移动。
- 按钮小部件 (Button Widget) -- 按钮小部件是与安装程序交互的主要方法。你通过使用 [Tab] 和 [Enter] 键导航这些按钮，从而推进安装程序的窗口。按钮在高亮时可以被选中。
- 光标 (Cursor) -- 虽然光标不是小部件，但它用于选择（并交互）特定的小部件。当光标在小部件之间移动时，可能会导致小部件改变颜色，或者你只看到光标位于小部件内部或其旁边。在图 10–1，“*配置/IP 中的安装程序小部件*”中，光标位于 OK 按钮上。图 10–2，“*磁盘德鲁士中的安装程序小部件*”显示光标位于 Edit（编辑）按钮上。

### 10.1.1 使用键盘导航

通过安装拨盘的导航通过一组简单的按键完成。移动光标，请使用 [Tab]、[Right]、[Up] 和 [Down] 方向键。使用 [Tab] 和 [Alt-Tab] 在屏幕上的每个小部件之间循环向前或向后切换。大多数屏幕底部都会显示可用光标定位键的摘要。

要按下按钮，将光标移动到按钮上（例如使用 [Tab]）并按 [Space] 或 [Enter]。要从列表中选择一个项目，将光标移动到你想要选择的项目并按 [Enter]。要选择带有*复选框*的项，将光标移动到复选框并按 [Space] 键选择项目。要取消选择，再次按 [Space] 键。

按下 [F12] 会接受当前值并继续到下一个对话框；它等同于按下 **OK** 按钮。

### 第 10.2 节：启动安装程序

> 注意：
> 除非对话框正在等待你的输入，否则在安装过程中不要按任何键（这样做可能会导致不可预知的行为）。

### 10.2 启动安装程序

有几种方法可以启动安装。你可以：

- 将随包装盒装附带的软磁盘（或你创建的 PCMCIA 启动盘或网络磁盘）插入主磁盘并重启计算机
- 如果你的计算机可以从 CD-ROM 驱动器启动，将 Red Hat Linux CD 插入驱动器并重启
- 启动 MS-DOS，并在 Red Hat Linux CD 的 `dosutils` 目录下启动名为 `autoboot.bat` 的程序（这仅在 DOS 下有效；它在从 Windows 启动的 DOS 窗口中无效）

当安装程序加载时，信息将在屏幕上滚动。当安装程序加载完成后，会出现此提示符：
