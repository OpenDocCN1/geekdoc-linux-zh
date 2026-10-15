
## 7.2 我如何访问 Windows Terminal 服务？

图 7.4 使用 Power Term 的键盘映射。

| 键盘映射 | 确定 | 取消 | 默认 | 帮助 |
| :--- | :--- | :--- | :--- | :--- |
| VT 键盘 | | | | |
| F4 | F5 | F6 | F7 | F8 | F9 | F10 | F11 | F12 | F13 | F14 | 帮助 | F17 | F18 | F19 | F20 |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | - | x | 查找 |  | 执行 | F21 | F22 | F23 | F24 |
| t | h | q | w | e | r | t | u | i | o | p | | 选择 | 下一个 全部 | F25 | F26 | F27 | F28 |
| Ctrl | c | a | s | o | t | g | h | j | k | | | | | F29 | F30 | F31 | F32 |
| Shift | z | x | c | v | b | n | m | | | | | | | F33 | F34 | F35 | F36 |
| 空格 | | | | | | | | | | | | | | | | | | |
| PC 键盘 | | | | | | |
| F1 | F2 | F3 | F4 | F5 | F6 | F7 | F8 | F9 | 0 | - | | 插入 | 查找 | 打印 | Pct1 | Pct2 | Pct3 | Pct4 |
| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 0 | - | | | | | | | | Pct5 | Pct6 | Pct7 | Pct8 |
| t | a | s | d | f | g | h | j | k | l | | | | | | | Pct9 | Pct10 | Pct11 | Pct12 |
| Super | u | e | r | t | y | i | o | p | | | | | | | Pct13 | Pct14 | Pct15 | Pct16 |
| Shift | z | x | c | v | b | n | m | | | | | | | | Pct17 | Pct18 | Pct19 | Pct20 |
| Ctrl-1 | | | | | | | | | | | | | | | | | | | |
| 终端键 | | | | | | | | | | | | | | PC 键 |

### 7.2.1 RHEL 8位版本

`up2date rdesktop`

### 7.2.2 适用于此版本的系统 v1.3.1

```
tar -xzf rdesktop-1.3.1.tgz

cd rdesktop-1.3.1

./configure

make

make install
```

Mandrake/SLES9/RHEL4/Fedora 已经是操作系统的一部分。

在使用 `rdesktop` 时，当我们坐在 Windows 机器上时，会弹出一个与示例相似的登录框。使用的每个 `rdesktop` 命令都会启动一个新的登录会话；虽然没有方法将 `rdesktop` 作为共享工具，但一旦登录，所有标准的桌面共享工具都可以供你使用。`rdesktop` 无法规避连接时对终端服务器许可证的需求，因为终端服务器正运行在你的 Microsoft Windows 平台上。

## 7.3 我如何访问 Citrix Metaframe 服务器？

图 7.5 新的 `rdesktop` 登录界面。

![](img/a063699af5597deead6a12a449cc2aa3_132_0.png)

使用 Citrix 提供的免费 Metaframe 客户端可以很容易地访问 Citrix Metaframe 服务器。你可以在 http://www.citrix.com 找到该客户端，它的行为与在 Windows 上相同。如果客户端已集成到现有的发行版中（如 RHEL3 所示），可以从系统菜单访问。

### 7.3.1 RHEL

`up2date ICAClient`

启动从 Red Fedora->Internet->Citrix ICA Client 菜单项开始。首次启动时，你需要同意许可协议。一旦同意许可，就可以像在 Windows 上一样完全使用该客户端。图 7.6 显示了第一个 Citrix 窗口。

## 7.4 成本

![](img/a063699af5597deead6a12a449cc2aa3_133_0.png)

终端服务器客户端涉及有趣的许可问题，例如，使用 `rdesktop` 时，你仍然需要终端服务器许可证客户端才能连接，Citrix Metaframe 客户端也是如此。对于 Citrix，这是在 Citrix Metaframe 许可证之外的额外。在 Windows 上，使用 Citrix 并不需要额外的终端服务器许可证。使用这些工具可能比其他选项稍贵一些。

除了使用 PowerTerm 这样的工具外，所演示客户端没有其他相关费用。

## 7.5 支持

每个供应商都为 PowerTerm 和 Citrix 提供支持。对于 xterm，支持通过 Linux 发行版供应商提供；对于 a-terminal emulator，支持取决于所使用的哪种客户端。成本显示在表 7.2 中。

### 表 7.2 Linux 服务的替代品的成本

| 软件 | 支持级别 | 费用 |
| :--- | :--- | :--- |
| VMware | 基于 Web/电话 | $199（免费90天，之后仍需购买） |
| Xterm | 通过 Linux 供应商，如果 | NA |
| PowerTerm | 基于 Web/电话 | $89（一年的价格的15%） |
| Client | 电话 | 仅限服务器（如果使用 Linux，你还需要证书） |
| tn20 | 各不相同 | 仅限服务器 |

## 家庭工具

本章将讨论在家庭桌面常用的工具，但在公司桌面也能找到。我们将展示将 Palm 或手持设备连接到桌面的解决方案，并讨论同步 PDA 数据的机制。具体而言，我们将查看照片和文档的数字同步解决方案。

## 我的 PDA 与 Linux 同步吗？

如果你有桌面支持和客户端，同步 Palm OS 设备到 Linux 非常简单。大多数并非所有这些工具都可以直接从每个发行版获取；然而，有几个子集将解决这个问题。需要注意的是，较新的 Palm 设备可能需要修改内核模块才能正常工作（此修改通常是对源目录中的文件）。参考 http://www.palm.org 获取内核模块的更新。至少需要以下程序来同步 Palm 设备：

### 8.1.1 RHEL

```
up2date palmlink

up2date gnome-evolution
```

Palmink 提供了同步 Palm 设备的基本工具，而其他工具为系统增加了功能，包括自动同步、日历和地址。有了所有工具，同步 Palm 设备到 Linux 变得非常直观。然而，找到正确的端口并不总是简单的，有一些通用规则：第一是 Palm 设备使用 `/dev/ttyUSB0` 且并不总是准确，对于 Sony 设备，它们可能是反的。还需要注意 USB 端口并不对应物理设备。

### 8.1.2 为你的 Palm 寻找正确的端口

`dpsh` 命令允许你打印关于 Palm 设备的信息。这些信息可以用于验证连接性，并提供一个获取 palm 上存储文件的方便命令界面。当设备要求你按 HotSync 按钮时，如果你选择了正确的设备，就会连接。由于我正在同步 Palm Tungsten 设备，我选择使用 `/dev/ttyUSB1`，并在 HotSync 后连接成功。有时在运行 `dpsh` 之前需要按 HotSync。尝试两种方法，并使用 `df` 命令从 Palm 设备读取数据并验证其准确性。涉及的设备将是 `/dev/ttyS0` 或 `/dev/ttyS1`，取决于 Palm 插入了哪个设备。

```
dpsh -p /dev/ttyUSB1

正在监听端口: /dev/ttyUSB1

现在按 HotSync 按钮...

欢迎来到 DLP Shell

输入 'help' 获取更多信息
```
`dpsh>` `df`
文件系统      k-blocks     已用      可用      总计
Card0:ROM       16515072            n/a 16515072      n/a 16128k
Card0:RAM       66060288    39241776 26813112     59% 64512k
总计 (ROM + RAM) 82753660    55762248              n/a n/a 806409k

![](img/a063699af5597deead6a12a449cc2aa3_138_0.png)
