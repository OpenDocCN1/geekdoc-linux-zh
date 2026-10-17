
`ifIndex` `InterfaceIndex`,

`ifDesc` `DisplayString`,

`ifType` `IANAifType`,

`ifMtu` `Integer32`,

`ifSpeed` `Gauge32`,

`PhysAddress` `PhysAddress`,

`ifAdminStatus` `INTEGER`,

`ifOperStatus` `INTEGER`,

`lastChange` `TimeTicks`,

```
ifInOctets             Counter32,
ifIncastPkts           Counter32,
ifInUCastPkts          Counter32, -- 已弃
ifInDiscards           Counter32,
ifInErrors             Counter32,
ifUnknownProtos       Counter32,
ifOutOctets            Counter32,
ifOutcastPkts          Counter32,
ifOutUCastPkts         Counter32, -- 已弃
ifOutDiscards          Counter32,
ifErrors               Counter32, -- 已弃
ifOutQLen              Gauge32,
ifSpecific             OBJECT IDENTIFIER -- 已弃
```

注意 `ifEntry` 和 `ifEntry` 的区别，一个是首字母大写，另一个不是。所有对象名称均为小写；例如 `ifTable` 和 `ifEntry`。因为 `ifEntry` 是首字母大写的，我们知道它是一个类型而不是一个对象。

`ifType` 类似于 C 语言中的 `struct`；它描述了表格每行的布局。小写的 `ifentry` 是 OID 树中的一个节点，列对象将定义在它的节点之下。因此，特定接口的描述将具有如下所示的 OID：

```
ifTable.ifEntry.ifDescr.x
```

其中 `x` 是行索引。

在条目类型定义之后将是构成该条目序列的对象的定义。你会在 MIB 定义中反复看到这种格式；许多 MIB 信息都是组织成表格。

# 定义新类型

虽然 SMI 中定义的数据类型已经足够，但有时更具体一些会更方便。例如，如果你的 MIB 重复使用这些限制值，你可能希望限制 `OCTET STRING` 中的可能值或 `Integer32` 覆盖范围，否则重复描述这些限制将变得繁琐。

RFC 1903 描述了文本约定（`textual convention`），这是一种允许你将说明绑定到一个新类型中的宏。以下文本约定取自 Net-SNMP（版本 5.0.8）分发的文件 `SNMPv2-TC.txt`。

```
Displaying ::= TEXTUAL-CONVENTION
DISPLAY-HINT "25a"
STATUS current
DESCRIPTION "代表来自 NVT ASCII 字符集的文本信息，如 RFC 854 第 4 页和第 10-11 页所示。
```

总结 RFC 854，NVT ASCII 集合规定：

- 使用字符代码 0-127（十进制）
- 图形字符（32-126）被解释为 US ASCII
- NUL, LF, CR, BS, HT, VT 和 FF 有 RFC 854 指定的特殊含义
- 其他 25 个代码没有标准解释
- 序列 'CR LF' 意味着换行
- 序列 'CR NUL' 意味着回车
- 前面没有 'CR' 的 'LF' 意味着到下一行的相同列。
- 对于除 LF 或 NUL 以外的 x，序列 'CR x' 是非法的。（注意，这意味着字符串可以以 'CR LF' 或 'CR NUL' 结尾，但不能以 CR 结尾。）

使用此语法定义的任何对象长度不得超过 255 个字符。

`SYNTAX STRING (o..255))`

这描述了一个名为 `DisplayString` 的类型，它可以占用最多 255 个字节，并限于可显示字符。`DISPLAY-hint` 显示了 `DisplayString` 可能出现的形式。`255a` 意味着它可以采取最多 255 个 ASCII 字符的形式。RFC 1903 描述了显示提示的完整语法。

# MIB 文件的结构

当你读取 MIB 文件时，你会注意到它在 `BEGIN` 和 `END` 语句之间命名并定义。它将描述它包含了其他哪些内容

```
IF-MIB DEFINITIONS ::= BEGIN
```

`IMPORTS`

`MODULE-IDENTITY`, `Counter32`, `Gauge32`,

`Integer32`, `TimeTicks`,

`SMI`,

```
```

= { mib-2 31 }

```

这描述了 `ifmib`，它占用 `m` 地址。组织和联系信息清晰可见，随后是按时间倒序排列的先前版本描述。时间和日期看起来很晦涩，但它们只是 GMT（由 Z 表示 Zulu 时间）的年、月、日的拼接。因此，最近的修订（`200006140000Z`）是在 2000 年 6 月 14 日做的。接下来，你将看到 MIB 对象实际结构的定义，以及任何属于此 MIB 的文本约定。

```

END

```
然后是模块的定义。

```

ifMIB-MODULE-IDENTITY

LAST-UPDATED "200006140000Z"

ORGANIZATION "IETF MIB Working Group"

CONTACT-INFO

    Keith McChrie

    Cisco Systems, Inc.

    170 Tasman Drive

    San Jose, CA 95134-1706

    kmlogh@cisco.com

```

`DESCRIPTION` "描述通用对象的 MIB 模块。此 MIB 是 MIB-II 的更新版本，并包含了 RFC 1229定义的扩展。"

`REVISION` "200006140000Z"
`DESCRIPTION` "Interfaces MIB WG 同意的澄清，并已发布为 RFC 2863。"

`REVISION` "199602281555Z"
`DESCRIPTION` "Interfaces MIB WG 的修订，并发布在 RFC 2233 中。"

`REVISION` "199311082155Z"
`DESCRIPTION` "初始修订，作为 RFC 1573 的一部分发布。"

![](img/a28f80056348678270f2ea0cfefd7891_348_0.png)

# 安装帧缓冲区驱动程序

![](img/a28f80056348678270f2ea0cfefd7891_348_1.png)

在本附录中，我们将涵盖以下主题：

- 为你的显卡查找帧缓冲区设备驱动
- 配置帧缓冲区设备驱动

## 为你的显卡查找帧缓冲区设备驱动

要找到显显卡的可用设备驱动，请使用 Laddie CD 启动你的 PC。

如果 Laddie CD 成功为你的显卡找到了驱动，它将启动 Laddie 帧缓冲区 UI（如图 C-1 所示）。否则，它将在登录提示符之前显示消息 *The framebuffer (/dev/fb0) is unavailable*（帧缓冲区 /dev/fb0 不可用）。

![](img/a28f80056348678270f2ea0cfefd7891_349_0.png)

图 C-1：Laddie 帧缓冲区 UI

现在，我们假设帧缓冲区驱动已成功加载。要确定加载了哪种驱动，首先按 ESC 键退出帧缓冲区 UI。然后在命令提示符处输入以下内容：

```
laddie:~$ dmesg | grep fb
```

`dmesg` 命令显示内核启动产生的消息缓冲区，而 `grep` 命令选择那些可能与帧缓冲区相关的消息。

### vesafb 驱动

Laddie CD 首先尝试加载 `vesafb` 驱动，因为对于未知显卡这最可能的候选者。`vesafb` 驱动将视频电子标准协会（VESA）开发的接口转换为 VESA BIOS 扩展（VBE）。该驱动依赖 BIOS，因此必须在系统启动时进行配置。这意味着 `vesafb` 驱动必须编译进内核，而不是作为一个独立的模块。Laddie 设备使用启动提示符配置驱动，我们将对此进行描述。

这是我们一个成功安装了 `vesafb` 驱动的系统输出示例：

```
vesafb: framebuffer=0x88000000, mapped to 0xf8880000, using 600k, total 32768k

vesafb: mode=640x480, linewidth=640, pages=11

vesafb: mode=protected interface info at c000:f003

vesafb: scrolling:redraw

vesafb: Pseudocolor:size=8:8:8, shift=0:0:0

vesafb: Mode is VGA compatible
```
