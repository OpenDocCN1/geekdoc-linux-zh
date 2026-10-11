
```bash
# vparstatus -v

[Virtual Partition Details]
Name:			cable1
State:			Up
Attributes:		Dynamic,Manual
Kernel Path:		/stand/vmunix
Boot Options:

[CPU Details]
```

## 最小/最大：1/3

**受用户[路径]限制：**

**受监控[路径]限制：** 33

**未绑定[路径]：**

**[I/O 详情]**

0.0

0.0.1.1.2.0 BOOT <--- cable1 的启动磁盘

**[内存详情]**

指定[基地址 /范围]：

(字节) (MB)

总内存 (MB)：1024

**[虚拟分区详情]**

名称：cable2

状态：已启动

属性：动态，手动

内核路径：`/stand/vmunix`

启动选项：

**[CPU 详情]**

最小/最大：1/3

**受用户[路径]限制：**

**受监控[路径]限制：** 37

**未绑定[路径]：**

**[I/O 详情]**

0.8.0.0.8.0.5.0.0.0, BOOT <--- cable2 的启动磁盘

0.10

**[内存详情]**

指定[基地址 /范围]：

(字节) (MB)

总内存 (MB)：1024

`cable1` 从位于 `0.0.1.1.2.0` 的内部磁盘启动，`cable2` 从位于 `0.8.0.0.8.0.5.0.0.0` 的外部磁盘启动。

在使用虚拟分区时，你需要对系统的硬件有良好且扎实的了解，包括总线适配器和磁盘。在撰写本文时，所有与 vPar 相关的工作都在命令行中进行。了解构成你系统的硬件以及如何在命令行中查询这些信息至关重要。

如果你以前未接触过相关设备，可能需要回顾本章末尾的备份材料，以便熟悉设备及相关主题。

### 虚拟分区与处理器

在第 2 章中分配处理器时，我们可以选择将其设为`未绑定`或`绑定`。`绑定` CPU 专属于某个 vPar，不能动态地从 vPar 中移除或添加。`绑定` CPU 处理 I/O 中断，因此应与 I/O 密集型应用程序配合使用。`未绑定` CPU 可以从 vPar 中动态添加和移除。`未绑定` CPU 不处理 I/O 中断，因此应与 CPU 密集型应用程序配合使用。处理处理器稍显复杂，因为你有很多选项，其中一些只能在创建 vPar 时执行，其他一些则要求在执行前将 vPar 停止，因此让我们看一下 `vpstatus` 手册页（表 5-2）中的一个表格：

![](img/eff8b9287a5f38c5adf538f24aacf29e_351_0.png)

**表 5-2 添加、删除和修改资源**

| 命令 | 描述 | 在 vPar 运行时完成？ |
| :--- | :--- | :--- |
| 添加资源使用：（如果在运行 `vparmodify`，则相对于现有内容添加组件） | `-a` `cpu`:num | 否 |
| | `-a` `cpu`:num | 是 - 相对值 |
| | `[-a` `cpu`:num `[-a` `cpu`: [min] [:max]] `[-a` `cpu`:path]] `vparcreate` 专用 | |
| | `[-a` `mem`:size | 否 |
| | `-a` `io`:path [:attr] [,attr2,...]] | 否 |
| 删除资源使用： | `-d` `cpu`:path | 否 |
| | `-d` `cpu`:num | 是 - 相对值 |
| | `-d` `io`:path [:attr] [,attr2,...]] | 否 |
| | `-d` `mem`:size | 否 |
| | `-d` `mem`:base:range | 否 |
| 修改资源使用：（这是将修改为绝对数值而非相对值。） | `-m` `cpu`:num | 是 - 绝对值 |
| | `-m` `cpu`: [min [:max] | 否 |
| | `-m` `io`:path [:attr] [,attr2,...]] | 否 |
| | `-m` `mem`:size | 否 |

表 5-2 表明，在添加、删除和修改与虚拟分区相关的资源时，你有很多选项。虚拟分区提供的灵活性是使用该技术时最令人期望的特性之一。然而，它也是最令人困惑的特性之一。

该表格中嵌入了许多选项。让我们谈谈在创建 vPar 时分配 CPU，因为大多数与 CPU 相关的问题都发生在创建 vPar 时。在撰写本文时，`num` 在某些文档中使用，而 `total` 在其他文档中使用，因此就本讨论而言，`num` 和 `total` 是可以互换的。

`path` 允许你指定用于 vPar 的特定处理器。使用 `path` 会自动分配`绑定`处理器。要将硬件路径 45 处的处理器添加到 vPar，你会使用以下命令：

```bash
-a cpu:45
```

`min` 指的是`绑定` CPU 的最小数量。只有在创建 vPar 并指定 `min` 时，你才能获得 `min` 数量的 CPU，系统会分配`绑定` CPU 的硬件路径。以下命令将为你提供两个`绑定` CPU，其硬件路径由系统定义：

```bash
-a cpu:::2
```

`max` 是`绑定` + `未绑定` CPU 的潜在数量。例如，你可以有两个 `min` 和四个 `max` CPU，这将为你提供两个`绑定`（由 `min` 2 指定）和最多两个`未绑定`（由 `max` 4 指定）。如果有未使用的 CPU，它们将被分配给你的 vPar，从而使总数达到四个。以下命令将提供此数量：

```bash
-a cpu::2:4
```

`num` 是当前`绑定` + `未绑定` CPU 的数量。这与 `max` 描述的潜在数量不同。要通过 `num` 指定总共三个 CPU，其中三个通过 `min` `绑定`，一个在硬件路径 45 通过 `path` 指定，你会使用以下命令：

```bash
-a cpu::3 -a cpu::3 -a cpu:45
```

此命令的一个有趣细节是，要删除我们指定的硬件路径，我们需要按相反顺序发出选项。硬件路径将首先出现，然后是 `min`，最后是 `num`。

在我的 vPar 工作中，最常见的愿望是在所有 vPar 中拥有一定数量的`绑定` `min` CPU，然后根据 vPar 中应用程序的需要移动`未绑定` CPU。例如，当运行 `vparcreate` 时，我们将指定以下内容：

```bash
vparcreate -p cable1 -a cpu:::1:3 -a cpu::1
```

在创建时，`cable1` 将只有一个`绑定` CPU，因为我们指定了 `min` 为 1 且 `num` 为 1。`num` 是`绑定` + `未绑定` CPU 的总数，由于我们为 `num` 指定了 1，我们将获得一个`绑定` CPU。由于 `max` 为 3，我们留出了添加最多两个额外`未绑定` CPU 的空间。如果我们系统中有两个`未绑定` CPU，我们可以使用 `vparmodify` 根据需要将其在 vPar 之间移动。要从 `cable2` 移除两个`未绑定` CPU 并将其添加到 `cable1`，我们将发出以下两个 `vparmodify` 命令：

```bash
vparmodify -p cable2 -m cpu::1        # 将 cable2 从 3 减少到 1
vparmodify -p cable1 -m cpu::3        # 将 cable1 从 1 增加到 3
```

我们首先从 `cable2` 移除两个`未绑定` CPU，然后将其添加到 `cable1`。如果两个`未绑定` CPU 未分配给任何 vPar，我们在将其添加到 `cable1` 之前就不必从 `cable2` 中移除它们。在撰写本文时，`未绑定` CPU 可以在 vPar 启动或停止时移动，但`绑定` CPU 只能在 vPar 停止时移动。

尽管你在指定和修改 CPU 方面有很多选择，但你不需要使用所有这些选择。vPars 就像其他任何系统管理任务一样；保持简单。

让我们现在查看系统中的一些处理器。以下列表显示了在本书中一些早期示例中使用的 L-Class 系统在将其分配给任何 vPar 之前的总 CPU 数量：

```bash
evhdcon> # ioscan -f | grep proc
 processor   0   33   processor CLAIMED     PROCESSOR   Processor
 processor   1   37   processor CLAIMED     PROCESSOR   Processor
 processor   2   97   processor CLAIMED     PROCESSOR   Processor
 processor   3  101   processor CLAIMED     PROCESSOR   Processor
```
