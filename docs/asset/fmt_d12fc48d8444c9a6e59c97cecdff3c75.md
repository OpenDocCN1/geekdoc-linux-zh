
如果你发现某个设置很有用，可以将其输入 `/etc/sysctl.conf` 文件。其格式如下，请使用以下示例：

```
net.ipv4.tcp_retries 2=20
```

对于内核黑客来说，`sysctl` 比对普通用户更有意义，它是一个具有强大功能的工具，并且持续持续开发和编写文档。

> 相关的 FEDORA 核心和 LINUX 命令

在 Fedora Linux 中管理内核及其模块时，你将使用到以下命令：

- `gcc`—GNU 编译器系统
- `make`—GNU 项目和文件管理命令
- `mkbootdisk`—Fedora Core 的启动盘创建工具
- `sysctl`—运行时操作内核变量的接口
- `mkinitrd`—为启动加载创建 RAM 磁盘文件系统

## 参考

`http://www.kernel.org/`—Linux 内核存档。Linux 内核所有开发讨论的来源。

`http://kt.zork.net/kernel-traffic/`—Linux 内核流量。每周生成的 Linux 内核列表的摘要版本和评论。

`http://www.gnu.org/`—自由软件基金会。整个内核编译过程中使用的手册和软件程序的来源。像 `make` 和 `gcc` 等工具在这里有它们的官方文档。

`http://slashdot.org/article.pl?sid=01/08/22/1453228&mode=thread`—来自 Alan Cox 的著名的 AC 补丁，这些补丁是他的

`http://www.tldp.org/LDP/tlk/`—Linux 内核。关于 2.2 内核的在线书籍，描述了 Linux 内核的。

`http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Kernel-HOWTO.html`—内核 HOWTO；配置、编译和故障排除。

`http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/KernelAnalysis-HOWTO.html`—内核分析 HOWTO。描述了内核的神秘工作机制。

`http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Module-HOWTO.html`—内核模块 HOWTO。包含了关于未解析符号的良好讨论。

`http://www.ibiblio.org/pub/Linux/docs/HOWTO/other-formats/html_single/Modules.html`—Linux 模块安装 HOWTO；一份讨论重新编译内核模块的旧文档。

`http://www.tldp.org`—Linux 文档项目。所有 Linux 文档的圣地。HOWTO 文档、FAQ 以及在线书籍的极佳来源，全部关于 Linux。

`http://www.minix.org`—非官方的 minix 网站。它包含了一些指向 minix 信息的链接以及一个指向实际主页的链接。尽管 minix 仍受版权保护，所有者已向所有人授予了无限权利。亲自查看用于开发 Linux 的操作系统。

`http://jungla.dit.upm.es/-jmseysas/kernel/hackers-docs.html`—一个包含 Linux 内核文档、书籍、黑客工具以及其他对初学者和经验丰富的内核及内核模块开发者有用信息的链接的网页。如果你安装了 Fedora Core 内核源码，在该列表中位于文件 `/usr/src/linux-2.4/Documentation/kernel-docs.txt` 中。

`http://kerneltrap.org/node/view/799#comment`—如何升级到 2.6 内核；还包含一些关于该过程的活跃讨论和更新。

`http://www.fearthecow.net/kernel.html`—将 RH9 升级到 2.6.0-test4；关于让程序运行良好的良好信息。

`http://thomer.com/linux/migrate-to-2.6.html`—迁移到 Linux 内核 2.6；更新模块工具的良好 HOWTO。

# 第 25 章 生产力应用

当今的现代企业开始学习丰富的 Linux 用户多年来一直知道：使用 Linux 和免费的生产力软件具有巨大的成本效益。跳出许可和升级的轮训将有助于增加底线。本章提供了有关 Fedora Core Linux 包含和可用的流行生产力软件的一些信息。尽管少数科技行业专家持反对意见，但通过仔细选择和安装可选的生产力软件软件包，Fedora Core Linux 可以用于支持业务环境下的桌面操作。Fedora Core Linux 有大量有用、可靠且免费的软件可用。

生产力客户端包括用于创建文档以及调度、组织和计算的免费办公套件和工具。

在本章中，我们将检查 Fedora Core 提供的默认办公生产力应用。你将看到将员工迁移到 Linux 桌面是多么简单，因为有类似的应用程序可以利用现有的 Microsoft 格式数据文件。你将了解到 Fedora Core Linux 提供的替代应用程序，以及一些你可以自己安装的应用程序。本章描述了如何安装、配置和启动这些应用程序；有关使用这些应用程序的信息仅为了让你了解与使用它们相关的特殊问题。

## 适用于 Fedora Core 的办公套件

大多数办公套件都包含生产力应用，例如文字处理器、电子表格程序、计算器和绘图工具。

### 本章内容

- 适用于 Fedora Core 的办公套件
- PDA 连接
- Fedora Linux 扫描应用程序
- Web 设计
- 传真软件
- Fedora Linux 包含的其他生产力工具
- 为 Windows 创建的生产力应用
- 参考

### 生产力应用

供 Linux 使用。其中许多是免费的，但也有一些商业产品。Fedora Core 没有开发自己的办公套件，但它提供了一套默认应用程序。主要组件 `OpenOffice.org` 和 `GNOME Office` 套件包含书中。在接下来的章节中，你将学习这些软件包中的应用程序，并了解其他免费或购买的办公套件。

### 使用 OpenOffice.org

如果你需要实现与私有格式的兼容，`OpenOffice.org` 套件是满足你需求的先驱。Microsoft 文件格式在业务环境中很常用，兼容性是大多数选择套件的企业的主要考虑。`OpenOffice.org` 包含的应用程序与 Microsoft 文件格式大部分兼容，但无法提供 100% 的兼容性。这种兼容性对于 GNU 公许可证 (`GPL`) 应用程序是不可能的，因为文件格式是私有的，导入/导出过滤器必须经过逆向工程。可能某些特殊的格式导入或导出效果很好——你只能通过对自己的文件进行测试来判断——但所有基本功能都能正常工作。

许多家庭用户更喜欢 `OpenOffice.org`，因为它的界面与他们过去使用的 Microsoft 应用程序相似（但并不完全相同）。对于从 Microsoft Office 迁移过来的人，这种熟悉感是一个重要点。

`OpenOffice.org` 识别并打开近 120 种不同的格式和文档类型，从流行的办公套件到各种图形格式，并能够导出 70 种文档。

### OpenOffice.org 中有什么

`OpenOffice.org` 包含许多生产力应用，用于创建文本文档、准备电子表格、组织演示文稿、管理项目等。以下组件包含在 Red Hat Linux 包中：

- `Writer`—此文字处理程序允许你编写、格式化和组织文本文档。如果你习惯使用 Microsoft Word，`OpenOffice.org Writer` 的功能你会感到熟悉。然而，这些功能在应用程序中的呈现方式与 Microsoft Word 有不同，因此你必须寻找熟悉的功能。拼写检查、同义词、宏、样式和帮助功能内置在 `OpenOffice.org Writer` 中，其工作方式与其他文字处理器和应用程序一致。

- `OpenCalc`—此电子表格程序允许你以电子表格格式处理数字。它支持除最冷门的 Excel 函数外的所有函数，这意味着通过对 Excel 用户进行电子表格培训将会成功。`OpenCalc` 提供了一些有限的兼容性，但那些宏通常需要重写。`OpenCalc` 还支持数据交换格式，例如 Data Interchange 格式和 dBASE 格式。

- `Impress`—此演示文程序类似于 Microsoft PowerPoint，允许你创建包含图表、图解和其他图形的幻灯片。它与 PowerPoint 文件配合良好。当打开它时，`OpenOffice.org` 会启动一个向导，引导你创建新的演示文、让你使用现有的模板（尽管未提供），或允许你打开现有的演示文。

- `Math`—此公式编辑器允许你使用多种字体和符号编写数学公式，并纳入文字处理文档中。这些符号高度专业化，不容易包含在文字处理器的基本功能中。它对数学和科学写作人员非常有吸引，但 `Math` 对于任何需要在文本中包含复杂公式的人来说都大有帮助。
