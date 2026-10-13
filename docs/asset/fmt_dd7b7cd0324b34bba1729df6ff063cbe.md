
`/usr/xpg4/bin/egrep` 命令使用 `regex(5)` 手册页中“扩展正则表达式”（Extended Regular Expressions）部分描述的正则表达式。

### 注意事项

理想情况下，应该只有一个 `grep` 命令，但没有一种算法能跨越广泛的时空权衡。

行的限制仅限于可用虚拟内存的大小。

`/usr/xpg4/bin/egrep` 命令与 `/usr/xpg4/bin/grep -E` 相同（参见 `grep(1)`）。可移植应用程序应使用 `/usr/xpg4/bin/grep -E`。

### 选项

下面列出的选项受 `/usr/bin/egrep` 和 `/usr/bin/egrep` 支持，但 `-x` 选项除外，该选项仅适用于 `/usr/xpg4/bin/egrep` 命令。

- `-b` 在找到的每行之前加上其所在的块号。此选项对于通过上下文定位块号非常有用（第一个块为 0）。
- `-c` 打印包含模式的行数。
- `-e pattern-list` 搜索模式列表（以 `-` 开头的完整正则表达式）。
- `-f file` 从文件中读取正则表达式列表。
- `-h` 在搜索多个文件时抑制文件名的打印。
- `-i` 比较时忽略大小写区别。
- `-l` 仅打印一次匹配行的文件名，并用换行符分隔。当模式被发现多次时，不重复文件名。
- `-n` 在每行之前加上其在文件中的行号（第一行是 1）。
- `-s` 静默工作，即除错误消息外不显示任何内容。此选项对于检查错误状态非常有用。
- `-v` 打印所有包含模式的行。
- `-x` 仅考虑使用行中的所有字符来匹配整个固定字符串或正则表达式的匹配的行。此选项仅受 `/usr/xpg4/bin/egrep` 支持。

# egrep

### 操作数

`file`
要搜索模式的文件路径名。如果不指定文件操作数，则使用标准输入。

对于 `/usr/bin/egrep`，在搜索输入时指定一个要用的模式。

对于 `/usr/xpg4/bin/egrep`，指定一个或多个在搜索输入时要用的模式。此操作数被处理为指定了 `-e pattern-list`。

`pattern`

### 示例

假设你想在其中一个文件中找到包含 Michigan、Ohio 或 Indiana 单词的行。单个 `grep` 命令无法执行对多个模式的搜索。你可以使用 `egrep` 在文件或一组具有相似扩展名的文件组中搜索多个模式。

`egrep` 提供了以下功能：

- 在“或者”或“或”条件下同时搜索多个模式的能力。
- 搜索包含圆括号的文件作为其搜索基础的能力。
- 扩展的正则表达式元字符集。

`egrep` 比 `grep` 慢，但它可以执行更复杂的搜索。

> 注意 — 当使用 `egrep` 命令时，`\(`（反斜杠后跟左括号）或 `\)`（反斜杠后跟右括号）将括号作为字面文本匹配。左括号和右括号是分组部分的特殊字符。反之情况不成立，：

以下示例在当前目录下所有 `.doc` 扩展的文件中搜索包含 "Michigan|Ohio" 的行。

```
castle$ egrep "Michigan|Ohio" *.doc
```

以下示例强制 `egrep` 查找以 Michigan 和 Ohio 开头的行。`-i` 选项同时查找大小写。

```
castle$ egrep -i "Michigan|Ohio" *.doc
```

你可以将搜索模式包含在文件中，并将文件名作为 `egrep` 命令的参数。在开发不想在命令行中输入的复杂模式时，使用文件非常方便。

在以下示例中，名为 `pattern` 的文件包含行 `(Michigan|Ohio)`。

模式不需要引号，但需要圆括号。以下示例使用 `-f pattern.file` 作为 `egrep` 参数。

```
castle$ egrep -f pattern.file *.doc
```

以下示例在所有 `.doc` 扩展的文件中搜索包含 "Michigan|Ohio" 的行。

```
castle$ egrep "Michigan|Ohio" *.doc
```

## 310

# eject

## 别名路径 (Nickname Path)

| 别名 | 路径 |
| --- | --- |
| diskette0 | /dev/diskette0 |
| diskettel | /dev/diskettel |
| rdiskette | /dev/rdiskette |
| rdiskette0 | /dev/rdiskette0 |
| diskettel | /dev/diskettel |
| floppy | /dev/rdiskette |
| floppy0 | /dev/rdiskette0 |
| floppy1 | /dev/diskettel |

不要从包含挂载文件系统的设备上物理弹出介质。`eject` 会自动搜索设备上的任何已挂载文件系统，并在弹出介质之前尝试卸载它们（参见 `mount(1M)`）。如果 `eject` 操作失败，`eject` 将打印警告信息并退出。你可以使用 `-f` 选项在设备包含挂载分区的情况下强制 `eject`；此选项仅在卷管理程序（Volume Management）未运行时才有效。

如果你插入了软盘，在弹出介质之前必须使用 `vol(1)`，以通知卷管理程序软盘的存在。

# 缺陷 (Bugs)

应该有一种方法可以按用户更改默认设置。如果卷管理程序未运行，可以弹出当前已挂载的卷（参见 `mount(1M)`）。例如，如果你在 `/dev/dsk/c0t3ds2` 有一个 CD-ROM 驱动器挂载在 `/mnt` 上，以下命令（在卷管理程序未运行时）将弹出 CD-ROM 驱动器，因为切片 s0 和 s2 都引用了整个 CD-ROM 驱动器。

```
castle# eject /dev/dsk/c0t3ds0
```

# 选项 (Options)

- `-d` 显示要弹出的默认设备名称。
- `-f` 即使设备正忙（且卷管理程序未运行），也强制设备弹出。
- `-n` 显示别名到设备名称的翻译表。
- `-p` 不尝试调用 `eject_popup` 程序。
- `-q` 查询以查看介质是否存在。

# 操作数 (Operands)

| device | 通过 `/dev` 目录中的名称指定要弹出的设备 |
| nickname | 通过此命令已知的别名指定要弹出的设备 |

# 示例 (Example)

以下示例使用 `-d` 选项找到默认的弹出设备。在第一个示例中，软盘或 CD-ROM 驱动器中都没有介质。在第二个示例中，软盘驱动器中有软盘，并使用 `volcheck` 命令让系统知道它的存在。第三个示例中，CD-ROM 驱动器中有 CD，而软盘驱动器中没有任何东西。

```
castle% eject -d
Default device is: nothing inserted
castle% volcheck
castle% eject -d
Default device is: /vol/dev/rdiskette0/unnamed_floppy
castle% eject -d
Default device is: /vol/dev/rdsk/c0t6d0/jumpingjavascript
castle% eject
```

以下示例在卷管理程序运行时从其驱动器中弹出 CD（假设仅有一个 CD-ROM 驱动器）。

```
castle% eject cdrom0
castle%
```

以下示例无论卷管理程序是否运行，都会弹出软盘。

```
castle% eject floppy0
castle%
```

以下示例在卷管理程序未运行的情况下，弹出路径为 `/dev/dsk/c0t3d0s` 的 CD-ROM 驱动器。

```
# eject /dev/dsk/c0t3d0s2
#
```

> 注意 — 在卷管理程序未运行时，你必须拥有超级用户权限才能挂载、卸载和弹出 CD-ROM。

# 退出状态 (Exit Status)

- `0` 操作成功，或在带有 `-q` 选项时，介质在驱动器中。
- `1` 操作失败，或在带有 `-q` 选项时，介质不在驱动器中。
- `2` 你指定了无效选项。
- `3` `ioctl()` 请求失败。
- `4` 手动可弹出的介质现在可以移除了。

有关显示信息的完整描述，请参阅《链接器与库指南》（Linker and Libraries Guide）。

# elfdump 313

# 选项 (Options)

- `-c` 导出段段头部信息。
- `-C` 解混 C++ 符号名。Solaris 8 版本中新增。
- `-d` 导出 `.dynamic` 节的内容。
- `-e` 导出 ELF 头部。
- `-G` 导出 `.got` 节的内容。
- `-h` 导出 `.hash` 节的内容。
- `-i` 导出 `.interp` 节的内容。
- `-k` 计算 elf 校验和。Solaris 8 版本中新增：`elf_checksum()`。
- `-m` 导出 `.note` 节的内容。Solaris 8 版本中新增。
- `-n` 导出 `.note` 节的内容。
