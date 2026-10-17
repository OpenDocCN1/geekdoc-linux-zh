
```
    int latching;          // 如果报警应锁存

    int input;             // 报警的最新输入

    int alarm;             // 如果报警为1

    int count;             // 报警计数器

}
ZONE;
```

图 14-1 显示了它在编辑器中的器貌。

| id | name | enabled | latching | alarm | count |
|---|---|---|---|---|---|
| 1 | 车库门 | 1 | 0 | 1 | 7 |
| 2 | 运动检测器 | 1 | 0 | 0 | 228 |
| 3 | 大门 | 1 | 0 | 1 | 0 |
| 4 | 厨房窗 | 1 | 0 | 1 | 0 |
| 5 | 冰箱 | 1 | 1 | 0 | 0 |

图 14-1：编辑器中的 `ZONE` 结构体。

稍微跳跃一下，当我们设计和实现我们的 MIB 时，相同的信息在我们的 SNMP 接口中看起来如下：

```
$ snmptable -c public -v2c application ladAlarmTable ladAlarmCount

SNMP table: lad-MIB::ladAlarmTable
```

| ladAlarmZoneName | ladAlarmenable | ladAlarmLatching | ladAlarmState | ladAlarmCount |
|---|---|---|---|---|
| 车库门 | true | 0 | 0 | 7 |
| 运动检测器 | true | 0 | 0 | 228 |
| 大门 | true | 0 | 0 | 0 |
| 厨房窗 | true | 0 | 0 | 0 |
| 冰箱 | true | true | 0 | 0 |

在本章和下一章的任务是向你展示如何从 `ZONE` 结构体逐步变为上述 SNMP 接口。完成后，你应该应该理解如何在自己的应用程序中做同样的事情，并从此 MIB 中进行大量的剪粘贴。

# 你的企业编号

你可能注意到，我们没有在 SNMP 表格视图包含 `id`、`edge` 和 `input` 列。这并不是疏忽。由 MIB 设计师（或者任何接口设计者）根据接口的预期用途决定什么是合理的。在我们的案例中，我们认为 `edge` 和 `input` 信息硬件特定性太强，在该接口没有必要。`id` 列不由我们的 SNMP 代理返回，但需要访问特定行时它将作为报警表的索引使用。

现在你的兴趣被激起了，我们将为那些实际上正在建立一家小公司来告知你的设备的人通过一个小绕路来增加悬念。你可能还记得上一章在我们用 SNMP 识别打印机时关于企业编号的简短讨论。每个 MIB 都必须挂载到全局命名空间，如果你正在设计私有 MIB，你需要一个自己的企业编号。这些编号由 IANA（互联网分配编号机构）分配。每家公司或组织只需要一个企业编号，IANA 授予管理你编号下方树的权限。

从 IANA 获取企业编号可能需要一段时间，所以你应该开始行动起来。一旦你申请，IANA 会告诉你该过程大约需要一个月。在 IANA 处理你的请求期间，你可以设计并实现你的 MIB。

过程非常简单。只需使用你喜爱的浏览器访问 IANA 网站 (`http://www.iana.org`) 并点击菜单中的“Application Forms”。在下一页，选择“Private Enterprise Numbers (SNMP)”。你将看到一个需要填写的在线表。

在网页底部，有一个指向当前注册编号列表的链接。你可能想检查一下谁在列表上。你会发现在开头有一些熟悉的名字；公司从 SNMP 游戏之初就参与了；IBM 的是 2。思科有 9。惠尔士-普罗有 11。你可以滚动到最后查看当前最大的编号是多少。你可能还会识别条目 23528。它是我们将在本章中开发的 Laddie MIB 挂载的子树起始。

正如你在查看当前列表时可能注意到的，在线仅列出了企业编号、公司名称、联系人姓名和联系人邮箱地址。在这里最好使用你通用邮箱地址的其他地址，因为垃圾机器人可能会采集它。为此目的使用一个独立的地址非常方便，这是一个通用的地址，你可以将其转发给未来任何负责你 SNMP 工作的人。

只需在表单中输入你的信息并点击提交（Submit）按钮。

## MIB 文件

IANA 授予了你管理自己子树的权限，但要将其做好取决于你自己。为成功做好计划，不要把这台设备看作终点——为扩展留出空间。你可能想在一个单独文件中定义你的企业编号，可以在那里放入所有 MIB 通用的信息。（顺便说一下，阅读他人的 MIB 是非常好的主意。你会发现哪些是通用用法，并可能发现你喜欢的风格。）

以下是本章我们将创建的两个文件：

- `LADDIE-GROUP-SMI.txt`

这是我们将定义 Laddie 企业编号和产品标识 OID 的文件。¹

- `LADDIE-MIB.txt`

此文件将包含 Laddie MIB。该 MIB 将锚定在 `LADDIE-GROUP-SMI.txt` 文件定义的 OID 上。

我们将通过 Net-SNMP 提供的工具运行这些文件，以为我们的 MIB 实现生成骨架代码。你还需要将这些文件放在任何运行管理应用程序（`snmpget`, `snmpset`, `snmpwalk` 等）或解释陷阱（traps）和通知（informs）的系统中。

你正在使用的网络管理系统决定了这些文件的位置。Net-SNMP 管理应用程序希望它们位于 `/usr/local/share/snmp/mibs` 目录，尽管你可以修改它，并且取决于你所使用的操作系统分发版的偏好。对于我们的设备，我们将它们放在 `/opt/snmp/share/snmp`。

## LADDIE-GROUP-SMI

该文件描述了我们将用于组织 Laddie 企业子树的顶层结构。它包含了我们的企业编号和产品标识 OID。这个文件很小，让我们看看全文，然后讨论它的结构。（地址、电话号码和传真号码是为了保护 Bob 的隐私的虚造信息，但你会明白大致的意思。）

¹用于识别产品的 OID 作为 MIB-2 中 `sysObjectId` 的值返回。

```
LADDIE-GROUP-SMI DEFINITIONS ::= BEGIN
```

```
IMPORTS

    MODULE-IDENTITY,

    enterprises

    FROM SNMPv2-SMI
```

```
;laddieGroup MODULE-IDENTITY

LAST-UPDATED "200502220000Z"

ORGANIZATION "The Laddie Group"

CONTACT-INFO

    "Contact: Bob Smith

```

```
Postal: 221B Baker Street

Santa Clara, California, USA 12345

```

```
Phone: 408-555-1138

FAX: 408-555-1234

```

```
Web: www.runtimeaccess.com

Email: bsmith@linuxtoys.org

```

# DESCRIPTION

"The Laddie MIB"
Copyright 2005 The Laddie Group
保留所有权利。

此 MIB 模块指定了 Laddie Group MIBs 的锚点以及这些 MIB 通用的定义。

```

REVISION "200502220000Z"

DESCRIPTION

::= 1.0 - Initial Document.

::= { enterprises 23528 }
```

```
-- MIBs are defined here:

laddieMgmt OBJECT IDENTIFIER ::= { laddieGroup 1 }
```

```
-- Products are registered here:

laddieProducts OBJECT IDENTIFIER ::= { laddieGroup 2 }

laddieAppliance OBJECT IDENTIFIER ::= { laddieProducts 1 }

END
```
