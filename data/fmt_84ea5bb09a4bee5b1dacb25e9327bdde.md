
观察到命令 `binary` 被推后台运行。在操作命令时，你可以将光标移动到命令的任何部分。使用一些快捷键将节省大量时间。例如，按 `Ctrl+A` 到行首，按 `Ctrl+E` 到行尾。是的，在遍历命令时，你可以向前或向后移动。使用 `Ctrl+右箭头` 每次移动光标单词，或使用 `Ctrl+左箭头` 向后移动单词。

在没有 `root` 的情况下有杀死运行命令的快捷键吗？

```
$ find = /name
$ find /home/user Permission denied
$ find /root Permission denied
$ find /bin Permission denied
$ find /root/ Permission denied
```

如你在上面的示例所示，我们正在使用 `find` 命令搜索文件。每个人都知道 `clear` 命令可以清除屏幕，但这并不会停止提示符中运行的命令。如果你想停止正在运行的命令，使用 `Ctrl+L` 清除屏幕并返回提示符。使用鼠标进行复制粘贴操作并不总是可能的。在行上进行快速编辑可以确保你的光标位于文本开头，然后可以使用 `Ctrl+V` 进行粘贴。你可能想运行你最近执行的一个复杂/长命令。通常我们使用鼠标向下和向上滚动。要搜索命令，按 `Ctrl+R` 并开始输入你正在查找的命令名称。如果你仍然没有得到结果，尝试按 `Ctrl+R` 循环查找（`img/42a435dd97fa37bf0839d8abe967b91b_52_0.png`）。

## 常见问题 (FAQ)
## 使用命令行

名为 `abc`，但由于无法访问系统上的位置，它给了 `permission denied` 错误。现在，要用 `root` 权限重新运行此命令，可以使用以下快捷键：

```bash
$ sudo
$ sudo find "abc"
```

所以你可以看到使用 `sudo` 将允许运行命令。这在命令复杂或很长时很有用。

我想了解更多关于我的 `Linux` 系统。如何获取详细信息？我正在学习带有各种选项的 `uname` 命令。这里是：

使用 `-r` 选项获取内核版本：

```bash
$ uname -r
3.8.0-generic
```

使用 `-v` 选项获取编译日期：

```bash
$ uname -v
May 29...
```

使用 `-m` 选项获取硬件架构：

```bash
$ uname -m
x86_64
```

使用 `-o` 选项获取操作系统：

```bash
$ uname -o
Linux
```

使用 `-a` 选项获取显示所有信息：

```bash
$ uname -a
Linux-3.8.0-generic #1 SMP x86_64 May 29...
```

问题 7：有时我从命令行启动一个程序，提示符会被阻塞，直到我关闭它。每当你在 `Linux` 中运行命令时，在命令完成之前命令行提示符都不会释放。一个命令可能需要几分钟，取决于你正在操作的内容。例如，如果你尝试运行一个大型文件系统，耗的时间可能比尝试查找简单目录要长得多。与高质量电影相比，一个小文本文件会很快完成。

现在，要检查它是否在后台运行，请使用 `jobs` 命令。

问题 2：如何在后台运行命令？

```
$ jobs
& running
& binary
```

问题 5：如何加快我在 `Linux` 中的工作？

观察显示 `binary` 及其状态的输出。要将其带回前台，使用 `fg` 命令。

这里有几个命令行快捷键：在操作命令时，你可以将光标移动到命令的开头或结尾。传统方法在这些情况下非常慢。替代方案是按 `Ctrl+A` 回到命令开头或按 `Ctrl+E` 回到命令末尾。

```
/binary
```

所以，你可以看到命令执行回到了前台。

在命令行中为现有文件或目录输入名称可以使用 `Tab` 键来加速。只需输入前几个字符并按 `Tab` 键，它就会补全名称。如果有多个同名文件，按两次 `Tab` 键显示所有选项。

有时用户可能不想在后台运行命令以继续在终端进行其他工作。有多种方法可以实现这一点：

-   使用 `&` 执行你的命令以便在后台运行。

-   要将后台命令带回前台，使用 `fg`。

-   将后台命令置于后台，使用 `bg`。

-   如果有多个命令在后台运行，你可以使用 `jobs` 命令（列在 `jobs` 的输出中）将特定命令带回前台。

-   如果你想停止正在运行的命令，按 `Ctrl+Z` 挂起它然后使用 `fg` 或 `bg` 将其推到后台。例如，如果一个名为 `binary` 的可执行文件无限运行：

```
$binary
```

现在，要将此命令推到后台，使用 `bg` 命令。

```
$bg
& binary
```

观察到命令 `binary` 被推后台运行。在操作命令时，你可以将光标移动到命令的任何部分。使用一些快捷键将节省大量时间。例如，按 `Ctrl+A` 到行首，按 `Ctrl+E` 到行尾。是的，在遍历命令时，你可以向前或向后移动。使用 `Ctrl+右箭头` 每次移动光标单词，或使用 `Ctrl+左箭头` 向后移动单词。

在没有 `root` 的情况下有杀死运行命令的快捷键吗？

```
$ find = /name
$ find /home/user Permission denied
$ find /root Permission denied
$ find /bin Permission denied
$ find /root/ Permission denied
```

如你在上面的示例所示，我们正在使用 `find` 命令搜索文件。每个人都知道 `clear` 命令可以清除屏幕，但这并不会停止提示符中运行的命令。如果你想停止正在运行的命令，使用 `Ctrl+L` 清除屏幕并返回提示符。使用鼠标进行复制粘贴操作并不总是可能的。在行上进行快速编辑可以确保你的光标位于文本开头，然后可以使用 `Ctrl+V` 进行粘贴。你可能想运行你最近执行的一个复杂/长命令。通常我们使用鼠标向下和向上滚动。要搜索命令，按 `Ctrl+R` 并开始输入你正在查找的命令名称。如果你仍然没有得到结果，尝试按 `Ctrl+R` 循环查找（`img/42a435dd97fa37bf0839d8abe967b91b_52_0.png`）。

## 常见问题 (FAQ)

## 使用命令行

名为 `abc`，但由于无法访问系统上的位置，它给了 `permission denied` 错误。现在，要用 `root` 权限重新运行此命令，可以使用以下快捷键：

```bash
$ sudo
$ sudo find "abc"
```

所以你可以看到使用 `sudo` 将允许运行命令。这在命令复杂或很长时很有用。

我想了解更多关于我的 `Linux` 系统。如何获取详细信息？我正在学习带有各种选项的 `uname` 命令。这里是：

使用 `-r` 选项获取内核版本：

```bash
$ uname -r
3.8.0-generic
```

使用 `-v` 选项获取编译日期：

```bash
$ uname -v
May 29...
```

使用 `-m` 选项获取硬件架构：

```bash
$ uname -m
x86_64
```

使用 `-o` 选项获取操作系统：

```bash
$ uname -o
Linux
```

使用 `-a` 选项获取显示所有信息：

```bash
$ uname -a
Linux-3.8.0-generic #1 SMP x86_64 May 29...
```

## 使用命令行

您的常见问题

## 常见问题解答

```bash
$/usr/bin/dicolors
$ ls -b
$ >> while line
$ ls --color=auto
$ ls -la --color=auto
$ grep --color=auto
$ grep --color=auto
$ grep --color=auto
```

这将会保持输出，直到你继续按下键盘上的 `Enter` 键。

要退出输出，请按 `Q`。

```bash
/boot/abi-3.8.0-19-generic
/boot/abi-3.8.0-23-generic
/boot/grub/i386-pc/search.mod
/sbin/acpi_available
/sbin/edid
/sbin/e2label
/sbin/ntfs-3
/sbin/iptables-save
/sbin/iptables-restore
/boot/vmlinuz...
```

Q12: 如果我想读取文件的前或最后几行怎么办？

你可以使用 `head` 和 `tail` 命令来

```bash
$ tail -5 output
$ /etc/tty-nabc.txt
$ /etc/tty-small.txt
$ /etc/tty-v2-abi_basic.txt
$ /etc/media/adjab.sh
$ /etc/fstab
```

`tail` 命令显示输出的最后几行。

你也可以使用 `-c` 显示最后数量的字节数。

```bash
$ tail -c 100
$ /etc/shadow
```

要取消颜色，请在命令行上运行以下命令：
