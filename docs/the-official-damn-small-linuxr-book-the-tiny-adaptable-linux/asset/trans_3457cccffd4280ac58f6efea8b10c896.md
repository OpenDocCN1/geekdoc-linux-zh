

2. 在下载完这些软盘映像文件后，使用常规工具将它们写入软盘。对于 Windows，这通常意味着使用 rawwrite。适用于 Windows 的 rawwrite 程序可以在这里找到：
http://www.chrysocome.net/rawwrite

在将软盘映像写入软盘后，取出该磁盘，以便在目标机器上使用它来安装 DSL。（稍后，当指示从这两种软盘中的任意一个启动时，请确保已更改系统的 BIOS 设置，使软盘成为第一个启动设备。）

## DSL 安装在 Windows 9x 或 DOS 分区上

假设你有一台带有调制解调器或 Internet 访问的 Windows 9x 或 DOS 系统，并且你想尝试 DSL。你不想干扰你的 Windows 安装。你尤其不想重新分区硬盘。要在不影响当前系统的情况下安装 DSL，请按照以下步骤操作：

NOTE
本节需要 Internet 访问。对于没有 Internet 访问的系统的方法将在本章下一节中讨论。

- 1. 启动你想要安装 DSL 的机器进入 Windows 或 DOS。
- 2. 将 DSL 的嵌入版下载到 C:\。我们不会尝试运行第 7 章中讨论的虚拟化。嵌入版以 Zip 文件提供，因此对于 DOS 和 Windows 系统来说解压非常容易。
- 嵌入版，我称之为 DSL 的 Zip 文件版，可以在这里找到：
ftp://ibiblio.org/pub/Linux/distributions/damnsmalllinux/current/dsl-embedded.zip
- 3. 如果你的 Windows 系统上已有 unzip 程序，将此 Zip 文件解压到工作目录——例如，c:\work。
如果没有 unzip，你可以重新启动计算机使用 DSL Utilities 启动软盘，你会找到 unzip 和我们将要使用的其他实用程序。

我现在将重点放在使用 DSL FreeDOS Utilities 软盘上。这样可以提供一个共同的基础来继续。如果你已经有 unzip 并且熟悉它，我相信仍然很容易跟随。

### NOTE

如果你使用的是 Windows XP，FreeDOS 启动软盘实用程序将无法工作。对于 XP，你已经有 unzip；因此不需要它。

从实用程序软盘启动，然后执行以下操作：
A:\> C:
C:\> unzip dsl-33-1.zip KNOPPIX/KNOPPIX

### NOTE

DSL Zip 文件名因 DOS 8.3 文件名限制而被修改。使用 FreeDOS 时，你可以输入几个字符并按 Tab 键，修改后的文件名将被自动补全。如果使用 Windows，你可能能够看到并使用完整的 Zip 文件名。

- 4. 用 DSL 启动软盘替换 DSL Utilities 软盘，并使用 DSL 启动软盘重新启动系统。
- 5. 在 DSL 启动提示符下，输入以下内容：
boot: dsl 2 legacy frugal
在从 DSL 启动软盘启动时，如果出现错误或系统挂起，你可能需要使用额外的启动选项。DSL 启动选项在第 2 章中有讨论。
- 6. 当你看到系统提示符 # 时，输入以下内容：
# mkdoss swapfile
再次重新启动，你就完成了 Poorman's 安装。
恭喜！你现在正在 Windows 或 DOS 格式分区内运行 DSL Poorman's 安装。

## DSL 安装在现有的 Linux 分区上

Poorman's 方法也可以在现有的传统 Linux 安装中使用。你可能有另一个 Linux 发行版并且想尝试 Poorman's 安装方法。步骤与前面基本相同：

- 1. 下载 DSL 的嵌入版（Zip 文件）。
- 2. 解压以仅提取 KNOPPIX/KNOPPIX 文件作为 Linux 分区上的第一级目录。
- 3. 从 DSL 启动软盘启动你的系统。

在启动期间，你的分区将被扫描以查找 KNOPPIX/KNOPPIX 文件并开始启动 DSL。同样，你可能需要指定额外的启动参数，就像从 DSL CD-ROM 启动时一样。

## 在 Windows 9x 或 DOS 上进行 FRUGAL DSL 安装

请回顾前面对 Frugal 的定义：Frugal 安装是一种无需软盘且无需在每次启动时输入额外启动选项的 Poorman's 安装。接下来讨论的程序适用于 DOS、Windows 95 和 Windows 98。仅支持可以启动到 DOS 原生模式的系统。Windows ME 可以被修补以启动 DOS 原生模式，但这超出了本讨论的范围。如果你有 Windows XP，你可能想使用第 7 章中讨论的虚拟化。

在尝试这些程序之前，你应该成功完成前一节中的 Poorman's 安装。事实上，如果你发现需要额外的启动参数，你应该将它们写下来。此处的目标是无需软盘并且在每次启动时都不必输入额外的启动参数。

### 使用 LinLd 从原生 DOS 模式启动 DSL

linld 启动加载器是一个微小的 DOS COM 文件。使用 linld，你可以在 DOS 命令行上输入所有启动信息，类似于 DSL 启动提示符，或者你可以使用一个简单的 DOS 文本文件来存储启动选项。

有关 LinLd 的更多信息，请参阅

http://www.lwn.net/Articles/102210/

让我们继续从我们的 Poorman's 方法开始。你需要有 Poorman's 设置（换句话说，你应该在 C:\KNOPPIX\KNOPPIX 中有该文件，并且 Zip 文件仍驻留在 C:\ 上）。然后，从 DSL FreeDOS Utilities 软盘启动并执行以下操作：

```
A:\> C:
C:\> unzip dsl-33-1.zip linux24
C:\> unzip dsl-33-1.zip minirt24.gz
```
