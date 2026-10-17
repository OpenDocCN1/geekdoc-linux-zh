
Solstice Domain Manager 满足了网络管理的大多数需求。然而，有超过 300 个应用程序运行在 Solstice Site Manager 和 Domain Manager 上，提供了额外的网络管理能力和数据分析功能。

## Solstice 协作控制台 (Cooperative Consoles)

Cooperative Consoles 产品作为 Solstice Site Manager 和 Solstice Domain Manager 的一部分提供。Site Manager 版本具有局限性，它只能向另一个管理控制台发送信息；它无法接收信息并充当域管理器。Solstice Domain Manager 版本包含了完整发布版的 Cooperative Consoles，允许它从其他管理控制台发送和接收信息。

Solstice Domain Manager 的真正威力在于可以灵活配置多个域管理器来共享信息。每个控制台都可以配置为点对点控制台，允许每个控制台对对方具有平等的访问权限，从而监控和控制对方的资源，例如多个 Solstice Site Manager 控制台。或者，可以将 Domain Manager 控制台配置为接收多个管理控制台的输入，但不向它们发送信息，使其成为一个超级网络管理控制台。

![](img/20459f772e7361286cec3e76e3bd26b4_283_0.png)

**图 14.8** 超级网络管理控制台从中心位置提供企业的网络管理。

## Sun 网络管理产品 267

该设施特别适用于那些站点在工作时间内可能自行管理自己的网络，但在非工作时间交由中央网络管理控制台进行监控和管理的场景。非工作时间的控制台可以作为多个站点的主机，但不会向任何其他控制台返回其自身活动的信息。

## Solstice 企业管理器 (Solstice Enterprise Manager)

这是一款用于管理大型企业和复杂网络的产品。它直接面向电信和互联网服务提供商 (ISP)。除非在这些特定的业务领域工作，否则 Solaris 系统管理员可能不会预期看到这款产品。

这里提到 Enterprise Manager 是因为使用 Cooperative Consoles 软件，它促进了将 Solstice Domain manager 控制台和 Solstice Site manager 控制台连接到 Solstice Enterprise Manager，以进行大规模网络和系统管理。Enterprise Manager 用于隔离复杂的系统或网络问题，从而更快速地解决问题并为客户提供高可用性维护。

## Solstice Site/Domain Manager 的定制

许多组织对 Solstice Site 和 Domain Manager 提供的功能非常满意，但可以进行一些定制以增强产品的实用性，并使其更具体地针对业务需求进行定制。

我曾使用 SunNet Manager（Solstice Domain 和 Site Manager 的基础）来定义自定义对象。新创建的对象随后被视为一个单元，例如，可以在此指定类型的每个系统上启动一个单的事件和数据请求。此外，我还在“工具 (Tools)”菜单中添加了额外功能，以便能够从同一个中央管理位置执行清理和管理任务。SunNet Manager 已成功实施，用于管理和维护 15 台大型服务器和 300 多个工作站客户端。

默认情况下，进行这些添加的文件是 `/opt/SUNconn/snm/struct/elements.schema`。该文件定义了所有已知的对象类型，以及从这些对象可以执行的命令和用于识别它们的图标。可以使用标准的文本编辑器（如 `vi`）编辑 `elements.schema` 文件。

要添加新对象，你必须编辑文件中的三个部分：一个用于为组件创建新记录，一个用于指定使用的图标，一个用于声明可以运行的命令。

`elements.schema` 文件相关部分的简略示例如列表 14.1 所示，展示了添加 DB-server 新数据对象类型时需要进行的更改。

### 第268 页 第14 章 网络管理工具

列表 14.1 `elements.schema` 文件的简略版本，显示了默认类型 `sun-server` 和新类型 `DB-server` 的值

```
####################
# COMPONENTS
#nrecord component.sun-server (  # 通用 sun 器
  string[64] Name
  string[40] IP_Address
  string[40] User
  string[40] Location
  string[80] Description
  string[40] SNMP_RdCommunity
  string[40] SNMP_WrCommunity
  string[64] SNMP_Vendor_Proxy
  int SNMP_Timeout
  string[256] Sys_ObjectId
  string[40] Physical_Address
  string[60] Created_by_cc
  string[64] _groupId_Layout
)
```

```
record component.DB-server (  # 数据库服务器
  string[64] Name
  string[40] IP_Address
  string[40] User
  string[40] Location
  string[80] Description
  string[40] SNMP_RdCommunity
  string[40] SNMP_WrCommunity
  string[64] SNMP_Vendor_Proxy
  int SNMP_Timeout
  string[256] Sys_ObjectId
  string[40] Physical_Address
  string[60] Created_by_cc
  string[64] _groupId_Layout
)
```

```
instance elementCommand (
  (component.sun-server  "Remote login..." $SNMPHOME/bin/snm_cmtool login
%Name")
  (component.sun-server  "Telnet to Host..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.sun-server  "DB..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.sun-server  "FS check..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.sun-server  "USER check..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.sun-server  "Start Backup..." $SNMPHOME/bin/snm_cmtool
%Name")
)
```

### Sun Network产品 269

```
(component.DB-server  "Remote login..." $SNMPHOME/bin/snm_cmtool login
%Name")
  (component.DB-server  "Telnet to Host..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.DB-server  "DB..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.DB-server  "FS check..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.DB-server  "USER check..." $SNMPHOME/bin/snm_cmtool
%Name")
  (component.DB-server  "Start Backup..." $SNMPHOME/bin/snm_cmtool
%Name")
)
```

*(注：由于原文示例中 `elementCommand` 部分似乎存在不完整或占位符，此处保持了逻辑结构的对齐翻译)*

## 组件的图标

```
instanceGlyph(
(component.sun-server sun.icon)
(component.DB-server DB.icon)
```

图 14.9 显示了 Solstice 屏幕上新创建的对象以及现在可以执行的命令。

![](img/20459f772e7361286cec3e76e3bd26b4_286_0.png)

图 14.9 启动工具是可配置的，可以添加其他应用程序或隐藏现有的应用程序。

## Solstice 带宽管理器 (Solstice Bandwidth Manager)
