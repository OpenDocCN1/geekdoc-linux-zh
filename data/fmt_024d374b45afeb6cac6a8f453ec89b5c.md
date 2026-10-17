
现在让我们再次详细地过一遍这个文件。我们将先向你展示 MIB 文件的一个部分，然后进行讨论。阅读此内容的内容的方法是简要扫描 MIB 文本，然后阅读引用 MIB 文本的描述。

## LADDIE-GROUP-SMI DEFINITIONS ::= BEGIN

这一行给 MIB 赋予了一个名称，并告诉读者（人类或程序）这是我们对该 MIB 定义的开始。在文件底部寻找匹配的 `END` 标记以告诉读者所有定义都已完成。

## IMPORTS

- `MODULE-IDENTITY`,
  `enterprises` FROM `SNMPv2-SMI`

`Imports`（导入）部分相当于 C 程序中的 `#include` 部分——它告诉你在哪里可以找到此 MIB 中使用了但未在此定义的术语。我们包含了 `MODULE_IDENTITY` 宏和 `enterprises` 以供后续使用。接下来，我们定义了 `laddieGroup` 模块：

- `laddieGroup` `MODULE-IDENTITY`
`LAST-UPDATED` "200502220000Z"
`ORGANIZATION` "The Laddie Group"
`CONTACT-INFO`

"这里告诉用户你是谁以及如何联系你的地方。"

`DESCRIPTION`
"这里是你描述此 MIB 通用用途的地方。这也是你想要放置版权声明的地方。"

`REVISION` "200502220000Z"
`DESCRIPTION`
" 1.0 - Initial Document."

- { `enterprises` 23528 }

我们将 `laddieGroup` 锚定到此模块，并定义其值为 23528。完整的 OID 看起来如下：

```
1.3.6.1.4.23528
```

`LAST-UPDATED` 和 `REVISION` 行中的时间字符串指定了年、月、日、小时和分钟。Z 代表格林威治标准时间（GMT）。

```
"200502220000Z" 意味着 2005年2月22日00:00。
```

```
-- MIBs are defined here:

laddieMgmt OBJECT IDENTIFIER ::= { laddieGroup 1 }
```

这里我们锚定了它。

```
-- Products are registered here:

laddieProducts OBJECT IDENTIFIER ::= { laddieGroup 2 }

laddieAppliance OBJECT IDENTIFIER ::= { laddieProducts 1 }
```

LaddieProducts 部分是定义我们产品 OID 的地方。

`END`

这是 SMIie.txt 文件的结束。

## 创建 LAD-MIB

在本节中，我们将创建我们的设备 MIB。在跟随开发 MIB 时，请参考图 14-2 中的图片以获得更好的理解。LAD-MIB 分为三个部分：

- LaddTraps，包含陷阱的定义
- LaddieInfo，包含信息的定义
- laddSystem，包含

让我们开始详细的回顾。同样，我们将通过对所展示内容的讨论来展示一行或多行。
我们将从 `BEGIN` 语句和 MIB 的定义开始：

```
LAD-MIB DEFINITIONS ::= BEGIN
```

希望这看起来很熟悉。如果没有，请再次查看 LADDIE-GROUP-SMI.txt 文件的开头。`BEGIN` 行表示我们开始定义 LAD-MIB，这是我们为设备 MIB 起的名字。

接下来，我们将从其他文件导入将使用的外部定义类型和宏：

```
IMPORTS

NOTIFICATION-TYPE,

MODULE-IDENTITY,

OBJECT-TYPE,

Counter32,

Integer32,

Gauge32

FROM SNMPv2-SMI

DisplayString,

TrueValue

FROM SNMPv2-TC

laddieMgmt

FROM LADDIE-GROUP-SMI
```

SNMPv2-SMI 和 SNMPv2-TC MIB 定义随 Net-SNMP 软件包一起提供。当你在第 13 章在系统上安装 Net-SNMP 时，这些文件可能被放置在 `/usr/share/snmp/mibs` 或 `/usr/local/share/snmp/mibs` 中。请寻找 `SNMPv2-TC.txt` 文件。

# 模块定义

我们首先定义一个名为 `ladProject` 的模块来包含我们的设备的 MIB。在这里我们放置版权信息、修订历史、联系信息以及该模块包含内容的通用描述。

```
ladProject MODULE-IDENTITY

LAST-UPDATED "200505280000Z"

ORGANIZATION "The Laddie Group"

CONTACT-INFO

"Here we put contact information."
```

`DESCRIPTION`

"The LAD MIB."

此 MIB 模块指定了 Linux 设备设计演示应用程序（一个报警系统监控器）中的可轮和可设置对象。该 MIB 还描述了与此演示设备相关的陷阱（traps）。

+ `REVISION` "200505280000Z"
`DESCRIPTION`
" 1.1 - 根据 trapInfo 部分添加了陷阱。

+ `REVISION` "2005052220000Z"
`DESCRIPTION`
" 1.0 - 初始文档。"

```
:= { laddieMgmt 1 }
```

`MODULE-IDENTITY` 部分相当于一句话长度。第一行和最后一行结合在一起表示 ladProject 是在下方命名空间中定义的模块，其 OID 为 `laddieMgmt.1`。以下是该 OID：

`.1.3.6.1.4.1.3382.1`

在上一节讨论了 LADDIE-SMI 之后，`MODULE-IDENTITY` 的其余部分应该非常清晰。你可能会注意到我们在第 1 行和第 2 行列出了两个 `REVISION` 子句。如果你将来对 MIB 进行了更改，你需要添加修订子句来解释你做了什么。惯例是将修订子句按逆 chronological排列（即最近的更改出现在最顶部）。这并不意味着你可以随心所欲地对 MIB 进行任何更改；如果你更改了 MIB 中已定义的任何内容（名称、OID 等），将给你的客户带来困扰。你可能会发现需要根据客户需求的新信息来增强你的 MIB，或者帮助管理将添加到设备中的新功能。你可以添加新结构，但不要更改现有的结构！

显然，你的 `LAST-UPDATED` 时间戳将与你最近的修订子句匹配，我们的也是如此。

下一组行定义了我们将详细说明的部分：

```
-- LAD MIB 的顶层 MIB 标题

ladTraps OBJECT IDENTIFIER ::= { ladProject 0 }

ladSystem OBJECT IDENTIFIER ::= { ladProject 1 }

ladTrapInfo OBJECT IDENTIFIER ::= { ladProject 2 }
```

将所有的部分标题 OID 放在顶部（正如我们在这里做的那样），这是一种风格选择，我们认为这有助于传达 MIB 其他部分的结构。我们明确了将有一个部分用于定义陷阱，一个部分用于系统信息（我们将报警表放在那里），以及另一个部分用于仅通过陷阱发送的非轮询信息。

SNMP 中的编号通常从 1 开始，而不是 0，但你可能已经注意到我们给上面的陷阱部分分配了 `ladProject 0` 的 OID。我们这样做的原因可以追溯到 SNMP2（SNMP 版本 2）的早期，当时正在构建与 SNMPv1（SNMP 版本 1）的兼容性。更多详细信息，你可能需要阅读 RFC 1908：Coexistence Version 1 and Version 2 of the Internet-Standard Network Management Framework。

我们将通过 `ladSystem` 部分继续审查 MIB，并将陷阱留到以后考虑。这样我们就可以在讨论陷阱之后，紧接着讨论 `ladTrapInfo` 部分。

```
-- LAD 系统信息

ladSystemScalars OBJECT IDENTIFIER ::= { ladSystem 1 }

ladSystemTables OBJECT IDENTIFIER ::= { ladSystem 2 }
```

我们进一步将 `ladSystem` 细分为标量（scalars）部分和另一个表（tables）部分。标量只是不是表中列的实例。经验告诉我们，要将标量和表分开，以避免在 MIB 随着时间演变时，标量散落在各个表中。

# 区域的版本和数量

接下来，我们将在 `ladSystemScalars` 部分中定义一些标量。

+ - LAD 系统标量

```
ladVersion OBJECT-TYPE

SYNTAX      DisplayString

MAX-ACCESS  read-only
```
