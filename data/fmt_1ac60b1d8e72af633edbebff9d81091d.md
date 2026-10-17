
使用 `KPowersave`，您可以启动 `YaST` 电源管理模块并选择挂起到磁盘或内存（如果已在 `YaST` 中相应配置）。您可以更改 CPU 频率策略，这意味着您的系统要么在空闲时允许 CPU 频率下降并在需要更多 CPU 功率时动态调整（将 CPU 频率策略设置为“动态”），要么永久保持低 CPU 频率以节电（选择“节电”），或者永久保持高 CPU 频率以获得最大的 CPU 性能（选择“性能”）。如果您更改活动电源管理方案（“设置活动方案”），系统的所有组件都将成为节能工作的一部分。电源管理方案包括 CPU 频率缩放、节流、硬盘控制以及系统散热的设置。在 GNOME `kpowersave` 中通过“运行应用程序”终端启动此程序。

## 配置文件管理

您的系统需要适应用于移动计算的不断变化的环境。许多服务依赖于环境，且底层客户端必须重新配置。使用系统配置方案管理（`SCPM`）框架为您的机器使用的所有环境创建不同的配置方案。使用配置选择（`Profile Chooser`）更改活动配置。要修改 `SCPM` 设置，请选择“`YaST` 配置管理器模块”（`YaST Profile Manager Module`）并在提示时输入 root 密码。在 KDE 中通过主菜单启动配置选择。在 GNOME 中，在“运行应用程序”终端输入 `profile_chooser`。

### 1.10 使用 Shell

Linux 中的大多数任务可以通过图形用户界面方便地处理。某些任务（主要是系统管理员的任务）可以在终端或 shell 中通过命令行更有效地处理。这需要对 shell 如何工作有基本的了解，并掌握一些基本的命令行工具。请参阅第 245 页的第 19 章。

# Linux 软件

Linux 自丰富的应用程序，通常为您的特定问题提供多种解决方案。困难在于找到一个与您目前使用的 Windows 或 Mac 应用程序一样易用的程序。本章指出了重要的 Linux 应用程序，让您顺滑地过渡到新环境。

- 2.1 办公
- 2.2 网络
- 2.3 多媒体
- 2.4 图形
- 2.5 系统和文件管理
- 2.6 软件开发

接下来的几节将介绍常用 Windows 软件的一些强大的 Linux 替代品。每个节致力于特定的应用领域，并列出任务、Windows 应用程序和 Linux 等品。将详细讨论这些应用程序并提供更多信息的链接。此列表不完整，因为软件开发是一个演进过程，分钟都有新的应用程序产生。

## 2.1 办公

下节介绍了最流行的 Linux 办公和业务软件解决方案。这些包括办公套件、数据库、会计软件和项目管理软件。

表 2.1：Windows 和 Linux 办公软件

| 任务 | Windows 应用程序 | Linux |
|---|---|---|
| 办公套件 | MS Office, StarOffice, OpenOffice.org | OpenOffice.org, StarOffice |
| 文字处理器 | MS Word, StarOffice/OpenOffice.org Writer, WordPerfect | OpenOffice.org/StarOffice Writer |
| 电子表格 | MS Excel, StarOffice/OpenOffice.org Calc | OpenOffice.org/StarOffice Calc |
| 演示文片 | MS PowerPoint, StarOffice/OpenOffice.org | OpenOffice.org Impress, StarOffice Presentation |
| 数据绘图 | MS Excel, MicroCall Origin | OpenOffice.org Calc, Gnuplot |
| 本地数据库 | MS Excel, OpenOffice.org + MySQL | OpenOffice.org + MySQL, Rekall, knoda, PostgreSQL |
| 财务会计 | MS Money, Quicken, moneyplex | GnuCash, moneyplex |
| 项目管理 | MS Project | Planner, Taskjuggler |

思脑图工具 MindManager, Free Mind VYM (View Your Mind)

`OpenOffice.org` 是 MS Office 的开源解决方案。它是一个强大的办公套件，包含一个文字处理器（Write）、电子表格和数据库管理器（Calc）、演示文稿（Impress）以及绘图程序（Draw）。熟悉 MS Office 系列应用程序的用户会发现非常相似的应用界面以及他们习惯的功能。由于 `OpenOffice.org` 能够从 MS Office 应用程序导入数据，因此这两个套件之间的切换非常轻松。`OpenOffice.org` 甚至存在 Windows 版本，允许 Windows 用户在继续使用 Windows 的同时切换到开源替代方案。可以在 http://www.openoffice.org/ 查找更多关于 `OpenOffice.org` 的信息，并阅读第 109 页的第 6 章了解 `OpenOffice.org` 的介绍以及从一个办公软件迁移数据的简短指南。

`StarOffice` `StarOffice` 是由 Sun Micros 分发的 `OpenOffice.org` 专有版本。它适用于 Windows 和 Solaris 在内的多个平台。它包含了免费版（OpenOffice）不具备某些功能。可以在 http://www.sun.com/software/star/staroffice/ 查找更多关于 `StarOffice` 的信息。

`Gnuplot` `Gnuplot` 是一款非常强大且可移植的命令行控制绘图软件。它也适用于 MacOS 和 Windows 平台。`Gnuplot` 创建的图表可以导出多种格式，如 PostScript、PDF、SVG 等，允许您轻松地处理这些图表。可以在 http://www.gnuplot.info/index.html 查找更多关于 `Gnuplot` 的信息。

`Recall` `Recall` 是一个操作数据库的工具。支持的数据库包括 MySQL、PostgreSQL、带有 XBase 的 IBM DB2 以及 ODBC。使用 `Recall` 生成各种报告和表单、设计数据库查询，或将数据导入导出到各种格式。可以在 http://www.thecompany.com/products/recall/ 查找更多关于 `Recall` 的信息。

`knoda` `knoda` 是一个针对不同类型数据库的前端。它支持与 MySQL、PostgreSQL、SQLite 和 ODBC 数据库服务器连接。`knoda` 可用于操作表数据、创建和存储查询以及导入和导出 CSV 格式的数据。可以在 http://www.knoda.org/ 查找更多关于 `knoda` 的信息。

![](img/0d7086818d63bf06d3da42b908c48b45_52_0.png)

SUSE LINUX 33

`PostgreSQL` 是一个对象关系数据库管理系统，支持 SQL 标准的扩展子，包括事务、外键、子查询、触发器以及用户定义类型和函数。可以在 http://www.postgresql.org/ 查找更多关于 `PostgreSQL` 的信息。

`GnuCash` `GnuCash` 是一款用于控制个人和业务财务的软件工具。使用这一套软件跟踪收支，并管理您的银行账户和股票组合。可以在 http://www.gnucash.org 了解更多关于 `GnuCash` 的信息。

`moneyplex` `moneyplex` 是一个控制您财务状况的工具。从管理入资源和支出、监控投资组合到通过 HCIBC 标准进行在线交易，所有任务都由 `moneyplex` 处理。使用各种分析选项随时间跟踪您的财务交易。该工具也适用于 Windows，用户可以非常容易地迁移，而无需学习新的应用程序界面。可以在 http://www.matrica.de 找到更多关于 `moneyplex` 的信息。

`Planner` `Planner` 是一个项目管理工具，旨在为 Windows 下使用的项目管理工具提供功能。其各种功能包括甘特图表功能、任务和资源的各种视图等。可以在 http://www.imendo.com/projects/ 查找更多关于 `Planner` 的信息。

`Taskjler` `Taskjler` 是一款精简但非常强大的项目管理软件。通过甘特图功能生成各种报告（XML、HTML 或 CSV 格式）来控制和跟踪您的项目。不习惯通过命令行控制应用程序的用户可以使用 `Taskjler` 的图形前端。可以在 http://www.taskjler.org 查找更多关于 `Taskjler` 的信息。
