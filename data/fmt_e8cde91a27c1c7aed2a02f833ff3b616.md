
```bash
debugfs: <14803>
      Mode [0644]
      User ID [503]
      Group ID [100]
      Size [6065]
      Creation time [833201524]
      Modification time [832708049]
      Access time [826012887]
      Deletion time [833201524] 0
      Link count [0] 1
      Block count [12]
      File flags [0x0]
      Reserved [0]
      File acl [0]
      Directory acl [0]
      Fragment address [0]
      Fragment number [0]
      Fragment size [0]
      Direct Block #0 [594810]
      Direct Block #1 [594811]
      Direct Block #2 [594814]
      Direct Block #3 [594815]
      Direct Block #4 [594816]
      Direct Block #5 [594817]
      Direct Block #6 [0]
      Direct Block #7 [0]
      Direct Block #8 [0]
      Direct Block #9 [0]
      Direct Block #10 [0]
      Direct Block #11 [0]
      Indirect Block [0]
      Double Indirect Block [0]
      Triple Indirect Block [0]
```

# 486

# 目录

也就是说，我将行号设置为 `0`，链接计数设置为 `1`，并对其他每个字段都按了回车键。诚然，如果你有大量文件需要恢复，这可能有点繁琐，但我认为你可以应付来。如果你很有缘的话，你本该使用带有漂亮“回收站”的图形化“操作系统”了。

顺便说一下：`mi` 的输出指的是 `inode` 中的一个“创建时间”（Creation time）字段。这是个谎言！（或者至少是误导性的）。事实真相是，你无法在 `UNIX` 文件系统中判断一个文件是何时创建的。`struct stat` 结构体 `st_ctime` 成员指的是“inode 更改时间”（inode change time），即 `inode` 细节最后更改的时间。今天的索引到此结束。

注意，较新版本的 `debugfs`（我正在使用的版本）可能不包含上述列表中的某些字段（特别是 `Reserved` 和（部分或？）fragment 字段）。

一旦你修改了 `inode`，你就可以使用 `debugfs` 并执行：

```
# efsck -f /dev/sda5
```

其意图是，任何被删除的文件在字面上都已未删除删除，但它们都没有出现在目录目中。`debugfs` 程序可以检测到这一点，并为文件系统中 `/lost+found` 目录下的每个文件添加一个目录目。（如果该分区通常挂载在 `/usr` 上，这些文件现在将出现在 `/lost+found`。）剩下的工作就是根据内容推算出每个文件的名称，并将其返回到文件系统树中的正确位置。

当你运行 `efsck` 时，你会得到一些信息性输出，以及一些关于修复什么的的问题。对于所有涉及“摘要信息”（summary information）或你修改过的 `inode` 的问题，请回答“yes”。其他任何事情由你决定，对所有问题说“yes”是件好主意。`efsck` 完成后你需要移除文件系统。

实际上，有一种让 `efsck` 不需要将文件留在 `/lost+found` 的替代方案：你可以使用 `debugfs` 在文件系统中创建一个指向 `inode` 的链接。在修改 `inode` 之后，在 `debugfs` 中使用 `link` 命令：

```
debugfs: link <148003> foo.txt
```

这会在 `debugfs` 认为的当前目录下创建一个名为 `foo.txt` 的文件，`foo.txt` 将是你的文件。你需要运行 `efsck` 来修复摘要信息和块计数等。

## 12 未来这会变得更容易吗？

是的。事实上，我相信它已经变容易了。`2.1.x` 系列开发的内核在六多个月前就已经是零间接块了。`1996` 年 `12` 月初，`linux-kernel` 邮件列表上讨论过制作另一个 `2.0x` 生产级内核，该内核在删除时也会保持间接块完好。截至内核 `2.0.31` 的预发布版本，这还没有发生，我怀疑这是可行的。一旦我（以及）其他内核黑客克服了生产级内核中的这一局限性，我手动修改 `inode` 这种技术的许多选项将会消失。最晚，这应该在 `2.2.x` 内核系列的发布时发生（根据历史内核开发时间表，这应该在 `1998` 年第一季某个时候发生）。当这项工作被修正后，在 `debugfs` 中使用 `dump` 命令处理长文件也将是可能的。

## 13 有什么工具可以自动化这个过程吗？

碰巧的是，有的。遗憾的是，我相信它们面临与手动修改 `inode` 技术相同的问题：间接块是无法恢复的。然而，由于很快可能不再是一个问题的概率很大，现在查看这些工具是非常值得的。

## 14 Colophon（后记）

由 `Scott Heaver` 提到的 `lde`。老实说，我不推荐将其作为自动化文件恢复的工具。它更像是一个全屏调试而不是其他东西，尽管它确实具有一些功能，例如扫描某些类型的文件或某些文件内容的能力。它还可以与 `xia`（真的有人用过它吗？）和 `minix` 文件系统一起工作，我想只是现在没人在卖这些了。版本 `2.3.4` 可以在 `Sunite` `<http://sunite.unac.edu.au/pub/linux/Linux/system/Filesystems/lde-2.3.4.tar.gz>` 和镜像中找到（尽管有一个比这更近的版本！）我从一个 `8` 个月前的 `CD-ROM` 存档中找到了那一个。`lde` 对基本文件系统概念提供了一些相当实用的文档，以及关于如何使用它恢复被删除文件的文档。虽然我没有用过它，但我怀疑我的方法更好。

听起来像是在使用 `GNU Midnight Commander`，这是一个全屏文件管理工具，据我所知（`AFAIK`），它基于某些被称为 `'NC'` 的 `MS-DOS` 程序。`MC` 在 `Linux` 控制台和 `xterm` 中支持更多功能，并提供了虚拟文件系统，允许 `cd` 进入一个 `tar` 包。它的虚拟文件系统之一就是用于 `ext2` 撤销删除。这听起来非常方便，尽管我自己从未用过该程序——我更偏好老派式的 `shell` 命令。显然，我必须用 `--with-ext2undeleion` 选项配置程序：我还需要随 `sprofgs` 包一起的开发库和头文件。我推测一旦程序构建完成，你就可以告诉它 `cd undel /dev/hda5/`，并获取被删除文件的列表。

最新的非开发版本是 `4.0`；对于内核本身，不建议使用开发版本。

## 14 Colophon（后记）

由 `Scott Heaver` 提到的 `lde`。老实说，我不推荐将其作为自动化文件恢复的工具。它更像是一个全屏调试而不是其他东西，尽管它确实具有一些功能，例如扫描某些类型的文件或某些文件内容的能力。它还可以与 `xia`（真的有人用过它吗？）和 `minix` 文件系统一起工作，我想只是现在没人在卖这些了。版本 `2.3.4` 可以在 `Sunite` `<http://sunite.unac.edu.au/pub/linux/Linux/system/Filesystems/lde-2.3.4.tar.gz>` 和镜像中找到（尽管有一个比这更近的版本！）我从一个 `8` 个月前的 `CD-ROM` 存档中找到了那一个。`lde` 对基本文件系统概念提供了一些相当实用的文档，以及关于如何使用它恢复被删除文件的文档。虽然我没有用过它，但我怀疑我的方法更好。

听起来像是在使用 `GNU Midnight Commander`，这是一个全屏文件管理工具，据我所知（`AFAIK`），它基于某些被称为 `'NC'` 的 `MS-DOS` 程序。`MC` 在 `Linux` 控制台和 `xterm` 中支持更多功能，并提供了虚拟文件系统，允许 `cd` 进入一个 `tar` 包。它的虚拟文件系统之一就是用于 `ext2` 撤销删除。这听起来非常方便，尽管我自己从未用过该程序——我更偏好老派式的 `shell` 命令。显然，我必须用 `--with-ext2undeleion` 选项配置程序：我还需要随 `sprofgs` 包一起的开发库和头文件。我推测一旦程序构建完成，你就可以告诉它 `cd undel /dev/hda5/`，并获取被删除文件的列表。

最新的非开发版本是 `4.0`；对于内核本身，不建议使用开发版本。

## 15 Credits and Bibliography（致与参考文献）

“我之所以看得远，是因为我站在了巨人的肩膀上。”（艾萨·牛顿）
