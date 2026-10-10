
让那些没有商业版 IDA 的用户能够完成练习。列表中唯一活跃维护的工具是 `Diaphora` 和 `BinDiff`。这每种工具的作者都应该受到赞誉，因为他们提供了如此出色的工具，为我们节省了无数寻找代码更改的尝试次数。

## BinDiff

如前所述，Google 在 2011 年初收购了德国软件公司 `Zymamics`，该公司的研究负责人由声名显赫的研究员 `Thomas Dullien`（也称为 `Halvar Flake`）担任。`Zymamics` 因其开发的 `BinDiff` 和 `BinNavi` 两个工具而广为人知，这两款工具都有助于反向工程。在收购后，Google 大幅降低了这些工具的价格，仅为原价的十分分之一，使其变得更易获得。2016 年 3 月，Google 宣布从今起，`BinDiff` 将免费提供。该项目由 `Christian Blichmann` 活跃维护，`BinDiff 7` 是其最新版本。`BinDiff` 经常被誉为同类中最好的工具之一，能够对块和代码更改提供深度分析。截至 2021 年年中，`BinDiff` 对 `Ghidra` 以及另一个优秀的反汇编器 `Binary Ninja` 的支持处于测试阶段。

`BinDiff 7` 以 Windows 安装包 `(.msi)`、`Debian` 软件包 `(.deb)` 或 Mac OS X 磁盘映像 `(.dmg)` 的形式提供。安装仅需几次点击、一个授权版的 `IDA Pro` 以及所需的 `Java` 运行时环境特定版本。要使用 `BinDiff`，你必须允许 `IDA` 对你想要比较的两个文件进行自动分析并保存 `IDB` 文件。完成后，在 `IDA` 内部打开其中一个文件，按下 `CTRL-6` 弹出 `BinDiff` GUI 界面，如图所示：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_637_0.png)

下一步是点击 `Diff Database` 按钮并选择另一个 `IDB` 文件进行对比。根据文件的大小，可能需要一到两分钟才能完成。一旦对比完成，`IDA` 中会出现一些新标签，包括 `Matched Functions`（匹配函数）、`Primary Unmatched`（主要未匹配）和 `Secondary Unmatched`（次要未匹配）。`Matched Functions` 标签包含存在于两个文件中的函数，这些函数可能包含也可能包含更改。每个函数在 `Similarity`（相似性）列中都有 0 到 1.0 之间的评分，如下所示。数值越低，表示函数在两个文件之间的更改越大。正如 `Zynatics/Google` 在关于 `Primary Unmatched` 和 `Secondary Unmatched` 标签时所述：“第一个显示包含在当前打开的数据库中且与对比数据库中的任何函数关联的函数，而 `Secondary Unmatched` 子视图包含对比数据库中但未与第一个数据库中的任何函数关联的函数。”¹1

| similarity | confidence | change | EA primary | name primary | Primary Unmatched | Secondary Unmatched | Hex View-A |
|---|---|---|---|---|---|---|---|
| 0.90 | 0.95 | GE-E---- | 00000000D64F0 | EcSpPolicyParseP | 00000000169BE8 | EcSpPolicyParseP@20 | |
| 0.90 | 0.95 | GE-E---- | 00000000E0D68 | TcbProcessConnect... | 00000000C50F7 | TcbProcessConnectionWonFailure4 | |
| 0.90 | 0.94 | I-E------ | 0000000000000 | WfsSignapiDecryptC... | 000000006758E8 | TcbConnectionToControlEndPoint | |
| 0.90 | 0.93 | I-E------ | 00000000E2F0C2 | TGcToConnect... | 00000000200668 | WfsSignapiDecryptInternal@20 | |
| 0.90 | 0.92 | I-E------ | 00000000A3CB99 | TcbWbsAllBoundOut... | 0000000001B8EE | TcbWbsAllBoundEstimation@4 | |
| 0.90 | 0.85 | GE-I------ | 00000000A4F9C | AppAddOrDeletePeri... | 000000000B0D96 | AppAddOrDeletePersistentRoots | |
| 0.90 | 0.94 | I-E------ | 00000000B02A8 | NShmFillRef$Egdfe | 00000000003C9 | NShmFillRefEgdfe@80 | |
| 0.90 | 0.92 | I-E------ | 00000000E3028 | TcbWbsStubInbound... | 0000000013345 | TcbWbsStubInboundEstimation | |
| 0.90 | 0.91 | I-E------ | 00000000B4B00 | QmClearEcProfileFrom... | 00000000C4A69 | QmClearEqProfileFrom | |

![](img/0add480ffb73b6bc89b65d99f7d6b37a_641_0.png)

![](img/0add480ffb73b6bc89b65d99f7d6b37a_641_1.png)

# 实验 18-1: 我们的第一次差异 (Diff)

> 注意：从书籍仓库的 `Lab1` 中复制 `name` 和 `name2` 两个 ELF 二进制文件，并将它们放置在 `C:\grayhat\app_diff` 文件夹中。你需要创建一个 `app_diff` 子文件夹。如果你没有 `C:\grayhat` 文件夹，可以现在创建一个，或者使用其他位置。
