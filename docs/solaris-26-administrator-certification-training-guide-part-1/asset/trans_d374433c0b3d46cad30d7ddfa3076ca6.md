
## 表 9-3 Solaris 2.6 打印软件包

| 包实例 | 包名 |
|---|---|
| SUNWpcr | SunSoft Print - 客户端 |
| SUNWpcu | SunSoft Print - 客户端 |
| SUNWpsr | SunSoft Print - LP 服务器 |
| SUNWpsu | SunSoft Print - LP 服务器 |
| SUNWpsf | PostScript 过滤器 |
| SUNWscplp | SunSoft Print - 源兼容性 |

Solaris 2.5 软件包不再在软件分发中找到：

| 包实例 | 包名 |
|---|---|
| SUNWlpr | LP 打印服务 |
| SUNWlpu | LP 打印服务 - 客户端 |
| SUNWlps | LP 打印服务 - 服务器 |

打印客户端发出打印命令，使打印客户端能够发起打印请求。打印命令定位打印机和打印机配置信息。

当打印作业从打印客户端发送时，用户发出 SystemV 风格的 lp 命令或 BSD 风格的 lpr 命令。表 9-4 中显示的任何一种样式都可以使用。

## 表 9-4 有效打印样式

| 样式 | 描述 |
|---|---|
| 原子样式 | 打印命令和选项后跟打印机名称或类；例如：`lp -d neptune filename` |
| POSIX 样式 | 打印命令和选项后跟 server:printer；例如：`lpr -P galaxy:neptune filename` |
| 上下文样式 | 在《联邦命名服务编程指南》中定义；例如：`lpr -d thisdept/service/printer/printer-name filename` |

如果用户在有效样式中未指定打印机名称或类，命令会检查用户的 PRINTER 或 LPDEST 环境变量以获取默认打印机名称。这些变量可以在用户的启动文件中设置以指定要使用的默认打印机。如果未定义默认打印机的任一环境变量，命令会检查用户主目录中的 .printers 文件中的 _default 打印机别名。如果命令在 .printers 文件中找不到 _default 打印机别名，则会检查打印客户端的 /etc/printers.conf 文件以获取配置信息。如果在 /etc/printers.conf 文件中找不到打印机，命令会检查名称服务（NIS 或 NIS+），如果有的话。

## 为 Solaris 打印机配置软件

打印客户端软件和 Solstice AdminSuite 中的打印机管理器应用程序为在网络上设置和管理打印机提供了一种图形化解决方案。打印客户端软件的优点是它支持名称服务（NIS 或 NIS+），使您能够为网络集中管理打印。您还可以在命令行上使用 lpadmin 命令来配置单个系统上的打印机。Admintool 提供了在 Solaris 环境中安装打印机的替代方法。Admintool 为表 9-2 中列出的 lp 命令提供图形界面。本节介绍如何使用 Admintool 设置打印机软件。

您必须在已连接打印机的系统上运行 Admintool，因为 Admintool 不允许您对远程系统进行更改。

设置打印机时，Admintool 会在系统的 /etc/printers.conf 和 /etc/lp 目录中进行适当的更改。

> **注意。** 如果您坐在 systemA 上并且想要将打印机连接到 systemB，您不需要开车到该位置在 systemB 上运行 Admintool。从 systemA， simply rlogin 到 systemB 并输入

```
admintool -display local_systemA:0.0
```

SystemB 的 Admintool 现在应该在 systemA 上显示，就好像您坐在 systemB 一样。

使用以下步骤通过 Admintool 配置打印机。

- 1. 输入 admintool 以调出 Admintool 菜单。Admintool 窗口出现。
- 2. 单击工具栏中位于的 Browse 按钮并从弹出菜单中选择 Printers，如图 9-1 所示。

### 图 9-1

使用 Admin 工具选择打印机。

![](img/85737305a4c9aeecbcadd9986d604c02_177_0.png)

图 9-2 所示的打印机配置菜单出现，窗口中显示任何现有打印机。

### 图 9-2

打印机配置窗口。

![](img/85737305a4c9aeecbcadd9986d604c02_177_1.png)

- 3. 单击 Edit，Add。

- 4. 如果您正在配置打印客户端并且打印服务器位于网络另一侧，物理连接到另一系统，请从弹出菜单中选择 Access to Printer（参见图 9–3）。

### 图 9–3

Printers 窗口弹出菜单。

![](img/85737305a4c9aeecbcadd9986d604c02_178_0.png)

Add Access to Printer 窗口出现，如图 9–4 所示。

### 图 9–4

Add Access to Printer 窗口。

![](img/85737305a4c9aeecbcadd9986d604c02_178_1.png)

- 5. 按如下方式填写窗口中的信息：

  - **打印机名称**—输入您想要访问的远程系统上打印机的名称。
  - **打印服务器**—输入打印机所连接的系统的名称。
  - **描述**—如果愿意，输入打印机的简要描述。
  - **选项**—如果您想将此设为系统默认打印机，请选中此选项。

- 6. 单击 OK 按钮。窗口关闭，信息被添加到适当的 LP 打印系统文件中。

- 7. 如果您正在配置打印服务器，并且打印机将连接到本地系统，请从图 9-3 所示的弹出菜单中选择 Local Printer。显示图 9-5 所示的窗口。

- 8. 按如下方式填写字段：

  - **打印机名称**—输入您想要为此打印机指定的名称。
  - **描述**—如果愿意，输入打印机的简要描述。
  - **打印机端口**—单击按钮并选择打印机所连接的端口。
    - `/dev/term/a` 是串行端口 A。
    - `/dev/term/b` 是串行端口 B。
    - `/dev/bpp0` 是并行端口。
    - 如果您已连接具有其他设备名称的 SBUS 卡，请选择 Other。
  - **打印机类型**—单击按钮以选择与打印机匹配的打印机类型。

这里的打印机类型对应于 `/usr/share/lib/terminfo` 目录中列出的打印机。您选择的打印机类型必须对应于 terminfo 数据库中的一个条目。UNIX 与 PostScript 打印机配合效果最佳，因为从 CDE 内部的文本和图形分页格式是针对 PostScript 打印机的。如果您想选择 PostScript 打印机，您的打印机必须能够支持 PostScript。如果您使用的是 HP LaserJet 打印机，请选择 hplaserjet 作为打印类型，除非 LaserJet 打印机支持 PostScript。

  - **文件内容**—单击按钮以选择将发送到打印机的文件的格式。
  - **故障通知**—单击按钮以选择在打印机错误情况下如何通知超级用户。
  - **选项**—选择打印横幅或将此设为默认打印机。

> 注意。系统可以识别一个默认打印机。如果用户在打印时未指定特定打印机，作业将发送到默认打印机。

### 图 9-5

Add Local Printer 窗口。

![](img/85737305a4c9aeecbcadd9986d604c02_180_0.png)

用户访问列表—如果愿意，输入允许打印到此打印机的系统的名称。如果未输入任何名称，则所有客户端都允许访问。

- 9. 填写所有字段后，单击 OK 按钮。窗口关闭，新的打印机名称出现在图 9-2 所示的 Printer 窗口中。

## 使用打印机类型菜单中未列出的打印机

Print Manager 窗口中列出的打印机类型对应于 /usr/share/lib/terminfo 目录中列出的打印机。如果您要添加的打印机类型不可用，您可能需要在 /usr/share/lib/terminfo 数据库中添加一个条目。每个打印机在 terminfo 数据库中都由一个简短名称标识；例如，HP LaserJet 打印机在 /usr/share/lib/terminfo/h 目录下列为 hplaserjet。PostScript 打印机的条目位于 /usr/share/lib/terminfo/P 中。目录中找到的名称是在设置打印机时您指定的打印机类型。

如果您找不到打印机的 terminfo 条目，您可以尝试选择类似类型的打印机；但是，您可能难以在每次打印请求时保持打印机处于正确的模式。如果您的打印机类型没有 terminfo 条目并且您希望保持打印机处于正确的模式，您可以自定义与打印机一起使用的接口程序或向 terminfo 数据库添加条目。您将在 /etc/lp/interfaces 目录下找到打印机接口程序。编辑接口文件或在 terminfo 数据库中添加条目超出了本培训指南的范围。terminfo 数据库中的打印机条目包含并定义了数百个项目。请参阅《Solaris 系统管理员指南》以获取执行此任务的信息。

## 管理打印机

管理打印系统涉及监控 lp 系统并找出系统可能无法正常工作的原因。其他常规任务包括取消打印作业以及在打印机维护期间启用或禁用打印机。本节提供有关您将执行的日常任务的说明，以管理打印机和打印调度程序。以下所有命令都需要超级用户访问权限。

### 删除打印机和打印机访问

使用 Admintool 从系统中删除打印机。在 Admintool 的打印管理器窗口中，突出显示您要删除的打印机并选择 Edit，Delete，如图 9-6 所示。打印机队列将从系统中删除。

### 图 9-6

删除打印机。

![](img/85737305a4c9aeecbcadd9986d604c02_181_0.png)
