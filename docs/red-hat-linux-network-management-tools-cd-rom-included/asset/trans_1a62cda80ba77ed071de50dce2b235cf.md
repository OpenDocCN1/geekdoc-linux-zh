
```
system.sysLocation.0 = Graphics_Lab
system.sysServices.0 = 72
```

主机 **nrcidemo** 运行着 UCD SNMP 代理，上面的输出仅显示了系统组的一部分。在此示例中，我们可以确认 sysContact、sysName 和 sysLocation 对象已根据 **snmpconf** 配置文件进行了更新。

**snmpconf** 软件提供了几种指定所需配置文件的方法。首先，文件名可以在命令行中给出，如前例所示；**snmpconf** 将检查当前目录以查找文件。接下来，可以使用完全限定路径名提供文件。最后，如果环境变量 **SNMPCONF_LIB** 已设置，软件将搜索该变量指定的目录。

**snmpconf** 工具提供了一些基本错误检查，并在出现问题时显示有用的信息。然而，很难确定某些类型问题的根本原因。例如，如果提供了错误的 community 字符串或设备当前不在网络上，则会显示相同的错误消息。因此，命令

```
# snmpconf didymus private config1
# snmpconf monet public config1
```

产生相同的错误，如下所示，但原因不同：

```
#
# Setup standard system group information
#
UNABLE to set display string ‘system contact’ to Susan-Maxwell
UNABLE to set display string ‘system name’ to host.dt.com
UNABLE to set display string ‘system location’ to Graphics_Lab
Done.
3 errors encountered.
```

第一个命令尝试在系统 **didymus** 上设置 MIB 对象，该系统目前在网络上无法访问；也就是说，在运行此命令时该设备已断电。第二个命令使用了错误的 community 字符串。在此情况下，正确的 community 字符串是 **private**，而不是 **public**。正如你所见，该工具对宕机的系统和错误的 community 没有不同的响应，使得你难以确定特定错误的根本原因。然而，通过谨慎，你可以通过在执行 **snmpconf** 之前发出 **ping** 命令来解决此问题。这样可以避免这种歧义并适当处理各自的问题。

**snmpconf** 软件提供了两个命令行选项。第一个，**-version**，显示 **snmpconf** 工具本身以及 CMU 支持库的版本信息。第二个，**-quiet**，指示 **snmpconf** 在执行时抑制消息。

## Tkmib 工具

tkmib 实用程序为许多 Linux SNMP 工具提供了 GUI 前端，包括 **snmpget**、**snmpgetnext**、**snmpwalk** 和 **snmptable**。该软件被称为“MIB 浏览器”，可用于查询 SNMP 代理关于特定 MIB 对象及其关联值的信息。要调用此工具，请在 UNIX shell 中发出 **tkmib** 命令。启动软件后，它会显示一个相当大的窗口，其中包含多个菜单、面板和按钮，如图 8.4 所示。

窗口包含四个主要面板：MIB 树视图面板、MIB 对象定义面板、MIB 描述面板和 MIB 值面板。

使用该软件查询代理非常简单：在顶部面板中找到所需的 OID 字符串，在目标主机文本框中输入主机名或 IP 地址，然后单击适当的 SNMP 操作按钮之一。

按钮 **stop**、**get**、**getnext** 和 **walk** 的功能应该很容易理解。不幸的是，**graph** 功能似乎不能正常工作；调用时会产生大量错误消息。剩下的按钮 **table** 需要更详细的解释。此按钮提供了一种查看 SNMP 表的绝佳方式。我们之前讨论过 **snmptable** 命令的功能，该命令显示 MIB 表。该工具的主要功能之一是能够将数据格式化为其他应用程序和程序的输入。它还显示表的格式。**tkmib** 中的 **table** 按钮主要用于查看 MIB 表，并且在格式化特定表的元素方面比 **snmptable** 命令做得更好。

![](img/f265c9d1f2610aca197c430cbfcd51f5_490_0.png)

MIB 树视图

OID
MIB 信息
MIB 定义
信息

对象
描述

目标
主机

MIB 对象及
关联值

SNMP 操作按钮

**Figure 8.4** tkmib 主窗口。

考虑 tcpConnTable 表，其中每个索引由 IP 地址和端口对构造。乍一看，很难理解此表的组织方式。然而，在 tkmib 工具的帮助下，表更容易理解。图 8.5 显示了从 IP 地址为 10.0.2.201 的设备检索到的 tcpConnTable 的视图。要获得此列表，选择了 tcpConnTable 表（来自 MIB-II 组）并单击了表按钮。

图中所示的底部面板包含一个滚动条，用于列出表的所有列。这些包括 tcpConnIndex、tcpConnLocalAddress、tcpConnLocalPort 等。还请注意 Index 列，其中包含表中每一行的索引。

**Figure 8.4** tkmib 主窗口。

![](img/f265c9d1f2610aca197c430cbfcd51f5_491_0.png)

**Figure 8.5** 表按钮显示。

### 菜单项

tkmib 工具提供了三个主要菜单：File、Mib 和 Options。File 菜单包含一个项目 Quit，其含义不言自明。下一个菜单 Mib 包含三个项目：Find a MIB Node、Load a New MIB File 和 Load a New MIB Module。子项目 Find a MIB node 可以搜索现有 MIB 以查找特定对象或组。例如，假设我们正在搜索 `udpInDatagrams` MIB 对象。首先，从 `Mib` 菜单中选择 `Find a mib node` 子菜单以显示图 8.6 所示的对话框窗口。

![](img/f265c9d1f2610aca197c430cbfcd51f5_491_1.png)

**Figure 8.6** 搜索节点对话框窗口。

输入 `udpInDatagrams` 对象名称并单击 `OK` 按钮。如果能找到该对象，MIB 树面板将更新以显示所需对象。否则，将显示错误对话框，说明找不到该对象。其他菜单项将额外的 MIB 模块和文件加载到 `tkmib` 中。

新 MIB 文件可以直接导入到 `tkmib` 工具中，以便 OID 对象使用标准名称字符串显示。要加载新 MIB，请选择 `Load a New MIB File` 菜单项。会出现一个新的对话框窗口，如图 8.7 所示。

![](img/f265c9d1f2610aca197c430cbfcd51f5_492_0.png)

在底部文本框中输入名称，或从右侧面板中选择代表应加载的 MIB 的文件名。在此示例中，将导入一个名为 `CISCO-6400-CHASSIS-MIB.my` 的 Cisco MIB。该 MIB 包含用于描述基于机箱的 Cisco 交换机和路由器产品的元素。选择后，树视图面板将被重绘并显示默认树项。要确定 MIB 文件是否按预期导入，请导航到 MIB 对象应开始的位置。

在此示例中，已从 `enterprises` 分支创建了一系列 Cisco 相关组。图 8.8 显示了顶部树视图面板的快照，其中仅包含 MIB 视图，显示在 Cisco 分支下定义的新 MIB 组。如果加载了不同的厂商特定 MIB，厂商特定名称也应在此列表中出现。

![](img/f265c9d1f2610aca197c430cbfcd51f5_493_0.png)

**Figure 8.8** Cisco 分支的树视图。

剩余的菜单包含四个项目：`Display`、`Time between graph polls`、`Port number` 和 `Community Name`。`Display` 子菜单控制在对象描述面板中显示的每个 MIB 对象属性。子菜单包含多个复选框，每个 MIB 属性一个。当其中一个框未选中时，相应的 MIB 属性将从对象面板中移除。

时间间隔图轮询菜单选项控制在图中使用的 MIB 对象每次检索之间经过的时间。默认值为五秒。端口号子菜单项定义查询 SNMP 目标代理时使用的 TCP 端口。默认值为标准端口 161。要更改默认值，请选择端口号项，并在显示新的对话框框时（如图 8.9 所示），输入所需端口并单击 Ok 按钮。

![](img/f265c9d1f2610aca197c430cbfcd51f5_493_1.png)

**Figure 8.9** 端口号对话框窗口。

community 字符串密码也可以更改。默认值设置为 public。要更改默认值，请选择 Community Name 子菜单项，并在显示的新对话框窗口中输入新值，如图 8.10 所示。

不幸的是，Options 菜单中任何项目的更改在应用程序终止时都不会永久保存。
