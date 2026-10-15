
shell 将为你提供以下列表：

```
m4 mesg mount_afp
mdNS metaflac mount_cd9660
mdNSResponder mibc2 mount_cddafs
mac mig mount_devfs
mach_init mk-and-map mount_fdesc
machine mkaafmmap mount_ftp
mail mkbom mount_hfs
mailq mkdep mount_msdos
maistat mkdir mount_ntfs
make mkextunpack mount_smbfs
makedbm mkfio mount_smbfs
makeinfo mkfile mount_synths
halloc_history mklocale mount_udf
man knod mount_volfs
manpath mksladfconf mount_webdav
md mktemp mountd
md5 mmroff msgs
md5sum more mtree
merge mount mv
```

shell 在尝试补全命令时只查找 `path` 变量中的目录。如果你安装了 Developer Tools 并希望 shell 也能使用 `/Developer/Tools/` 路径，你需要将其添加到你的 `path` 变量中。关于设置 `path` 变量的更多信息，请参阅第 16 章。

## 实践：查看所有可用命令列表

你好奇吗？你想获取一个可以在 Terminal 中运行的每一个命令列表吗？如果你使用 `bash`，在提示符处按下 Tab 键；你会看到：

```
Display all 1045 possibilities? (y or n)
```

按 `y` 列出所有命令，或按 `b` 退出。如果你想查看列表，`bash` 会一次显示一个屏幕，屏幕底部有 `--More--`。按下空格键查看下一页，或按下 Control-C 退出列表。

如果你使用 `tcsh`，按下 Control-X，Control-D。`tcsh` shell 并不礼貌；它没有给你机会为自己的错误后悔——事实上，你可能真的想看这个长列表。它会直接跳出 Terminal 中所有可用命令列表。

请注意，取决于你是否安装了额外的命令或 Developer Tools，你的命令可能多于或少于上面显示的 1,045 种可能性。

## 使用命令历史

你记得章节开头向你展示的那个长路径吗？它是这样的：

```
/Library/Preferences/ByHost/com.apple.SoftwareUpdate.033065c6ec5e.plist
```

假设你有这个文件路径，然后移动到其他几个目录并运行了一些命令，然后你再次需要它。你并不想重新输入一遍，尽管我们在上面所看到的，可以使用文件名补全让它变得更容易。

其实，在 Terminal 中工作时还有另一种节省时间的方法：被称为 `history`。

## BASH 和 TCSH 差异

虽然大多数历史功能的作用相同，但仍存在差异。在 `bash` 中，你可以使用 `!` 快捷键调用上一个命令，但在 `tcsh` 中你使用不同的语法。

假设你想拷贝一个文件；你输入以下命令：

```
$ cp /Users/kirk/Pictures/P101068.jpg /Users/shared
```

然后 Terminal 返回以下内容：

```
cp: /Users/kirk/Pictures/P101068.jpg: No such file or directory
```

但你确定该文件存在。当你进入目录进行检查时，你会发现确实有一个名字相似的文件，但你漏掉了一个 0，它应该是 P101068.jpg。使用命令历史记录，你可以按下上方向键，在提示符后就会显示相同的命令。使用左方向键将光标移动到你需要添加 0 的位置，输入 0，然后按回车键（你不需要将光标移回行末尾）。现在命令可以执行了。

你可以使用命令编辑来更改命令并在不同的文件上运行它们，例如。如果你在 Pictures 目录中有多个文件（如上所示），你可以使用上方向键重新显示上一个命令，更改文件名，并每次运行新命令。

```
$ cp /Users/kirk/Pictures/P101068.jpg /Users/shared
$ [up arrow; move cursor; change name]
```

使用左方向键移动光标，通过按下 Delete 键并输入新名称更改文件名，然后按 Enter。对每个文件重复此操作：

```
$ cp /Users/kirk/Pictures/P101053.jpg /Users/shared
$ [up arrow; move cursor; change name]
$ cp /Users/kirk/Pictures/P101047.jpg /Users/shared
$ [up arrow; move cursor; change name]
$ cp /Users/kirk/Pictures/P101026.jpg /Users/shared
```

在这个示例中，更改仅位于 .jpg 扩展名之前的两个字符，但你可以更改整个文件名。

你还可以使用命令编辑来更改命令的参数。使用上面的示例，我将一些图片拷贝到了我的 `/Users/shared` 目录。但我可以运行命令将其中一个文件拷贝到不同的位置，而无需重新输入整行：

```
$ cp /Users/kirk/Pictures/P101068.jpg /Users/shared
$ [up arrow]
```

在这里，你不需要移动光标，只需使用 Delete 键删除 `shared` 并将其替换为你的用户目录后加 Desktop：

```
$ cp /Users/kirk/Pictures/P101068.jpg /Users/kirk/Desktop
```

在第一行中我将一张图片拷贝到了 `/Users/shared` 目录，而在第二行中将文件的目标更改了桌面。

命令编辑也是更改命令中所发布选项的方法。假设你列出了一个目录中的文件，然后决定使用 `-l` 选项来显示长列表。也不需要重新输入命令。

```
$ ls /etc/periodic
daily weekly; move cursor;
$ [up arrow; monthly; type option]
```

按下上方向键后，将光标向左移动并添加 `-l`：

```
$ ls -l /etc/periodic
total 0
drwxr-xr-x 4 root wheel      136 Jul 14 13:33 daily
drwxr-xr-x 3 root wheel      102 Jul 14 13:33 monthly
drwxr-xr-x 3 root wheel      102 Jul 14 13:33 weekly
```

shell 现在以列表形式显示目录内容。

# 哎！忘记加 sudo 了？

有很多命令在没有 root 权限的情况下无法运行；你的计算机上也有许多区域在没有这些权限的情况下无法访问的。如果你拥有计算机的管理员权限，可以使用 `sudo` 命令来提示你输入密码以运行这些命令或访问这些文件或目录（更多关于 `sudo` 的信息请参见间插 7，“sudo”）。

但输入一个长命令后却只得到 Terminal 回复“Permission denied”（拒绝访问），这可能会很恼人：

```
$ periodic daily weekly monthly
/usr/sbin/periodic: /var/log/daily.out: Permission denied
/usr/sbin/periodic: /var/log/weekly.out: Permission denied
/usr/sbin/periodic: /var/log/monthly.out: Permission denied
```

如果你忘记在命令前缀加 `sudo`，可以使用快捷键再次运行它：

```
$ sudo !!
```

这是一个命令历史操作符，告诉 shell 运行上一个命令。通过在它前面添加 `sudo`，你告诉 shell 以 `sudo` 身份运行上一个命令。Terminal 显示如下：

```
$ sudo !!
sudo periodic daily weekly monthly
```

Password:
在提示符处输入你的密码，然后按 Enter，命令将作为 `sudo` 运行，无需你重新输入命令。

# 显示命令历史

你可以随时通过运行以下命令检查历史记录中有哪些命令：

```
$ history
```

Terminal 显示历史列表中的命令列表；它看起来像这样：

```
$ history
1 10:13 ls
2 10:13 cd ..
3 10:13 ls
4 10:13 cd kirk
5 10:13 ls
6 10:13 cd Pictures
7 10:13 ls
8 10:13 ls -l
9 10:24 history
```

你可以看到它显示了命令的编号（从第一个到最后一个）、你运行命令的时间以及你输入的命令。它包含了你运行的命令，无论它们是否成功。这意味着错误的或拼写错误的命令也包含在历史中。

`history` 命令默认显示整个历史列表；但根据你的 shell 设置，它可以限制命令的数量。当这个列表变得非常长时，最好不要显示整个列表。有几种方法可以只显示部分历史。在大多数情况下，你想查看最近的命令。一种方法是运行 `history` 并带上你想显示的命令数量参数：

```
$ history
329 10:47 locate walden
330 10:49 history
331 10:49 ls
332 10:49 cd ..
333 10:49 ls -a
```

这告诉 shell 显示历史列表中的最后五个命令。你可以输入任何数字作为 `history` 命令的参数；如果历史列表比该数字短，shell 将显示整个列表：

```
$ history 10
1 11:12 cd /
2 11:12 ls -a
3 11:12 cd
4 11:12 ls
5 11:12 history
```

# 从历史中运行特定命令

我们看到，你可以通过方向键在历史列表中向上或向下移动。这是重新运行最近执行命令的最简单方法。但如果命令在列表中靠得后，还有其他方法指定要运行哪个命令。

如果你显示了历史列表，其中一部分如下：

```
328 10:44 history
329 10:47 locate walden
330 10:49 history
331 10:49 ls
332 10:49 cd ..
333 10:49 ls -a
334 10:49 history
335 10:50 cd /
336 10:50 ls -a
337 10:50 history
```

你将知道想要运行的命令。只需输入：

`!329`

叹号 `!` 是历史列表中命令的快捷方式；如果你在后面输入一个数字（中间没有空格），它会运行该绝对对应的命令。另一种指定之前的命令的方法是使用列表末尾的相对数字。如果你想运行倒五个命令，输入：

`!-5`

你还可以告诉 shell 运行以特定字符串开头的最后一个命令。再次使用上面的历史，你可以通过输入以下内容（同样在叹号后没有空格）运行 `locate walden`：

`!loc`

你可以在叹号后输入任意数量的字符，但 shell 会停止在第一个匹配处。在上面的示例中，由于没有其他以这些字母开头的命令，我可以输入 `!loc`。但如果我只输入 `!1`，它将运行命令 337，即第一个匹配。

# bash 的命令历史

到目前，我提供的命令历史信息对于 `bash` 和 `tcsh` 都是相同的。这一节将介绍一些 `bash` 特有的历史命令和技术。事实上，`bash` 让你处理命令历史的方式是使用 `bash` 的一个理由。它提供了更大的灵活性，并让你工作快得多，为最近的命令提供了大量的快捷方式。

`bash` 中实用的历史功能之一是可以运行以特定字符串开头的命令。假设你几小时前运行了以下命令：

```
$ pico /Volumes/Backup/Texts/Walden.txt
```

如果你想再次运行它，可以滚动历史列表，发现它是 20 个命令之前的，找到它的编号，然后使用之前提到的 `history` 快捷键调用它。或者，你可以使用 `bash` 的方法。如果你在 `.bash_profile` 文件中添加以下两行，你就设置了一个强大的历史快捷键：

```bash
bind '*M-[A]': history-search-back
bind '*M-[B]': history-search-forward
```

完成这些操作后，退出 shell 并打开一个新的 Terminal 窗口。要找到你运行的以特定字符串开头的之前的命令，你可以使用这些方向键快捷键：输入 `pico`，然后按下上方向键。这会提示你运行的以 `pico` 开头的命令。如果你运行了许多以 `pico` 开头的命令，只需按下上方向键查看你运行的所有命令。或者你可以在按下上方向键之前输入更多。对于上面的命令，你可以输入 `pico /Vol` 然后按下上方向键，如果你知道你没有运行过其他以 `pico` 和 `path` 开头的文件的命令。你还可以通过输入 `cd` 并按下上方向键使用这种技术回到另一个目录（如果你指定了完整路径）。你可以将其用于任何运行过的命令，只要输入它的开头字母。

# 快速搜索你的命令历史

还有另一种方法找到存储在历史文件中最近运行的命令。在 `bash` 中，按下 Control+R 调出反向提示。当你这样做时，会显示：

```
(reverse-i-search)—
```

输入几个字符——你正在查找的命令的开头——shell 会自动填充剩余部分。如果显示的命令是你想要的，按 Enter 运行它。如果不是，按 Control+R 遍历以相同字符串开头的其他命令。这与之前技术中按下上方向键相同。

# FC 命令

`bash` 特有的一个命令是 `fc` 命令。这个内置命令（它是 shell 的一部分，而不是一个独立的命令）让你以多种方式编辑和交互历史记录。

首先，`fc -1` 列出历史文件中最后 16 条目。这与运行 `history 16` 相同，所以它并不特别：

```
$ fc -1
500 exit
501 bash
```

```
502 history 10
503 ls
504 ls
505 ls | wc
506 history
507 ls
508 man bash
509 history -10
510 history 10
511 man fc
512 fc
513 man fc
514 fc
515 man fc
516 fc -l
```

当你使用 `fc` 命令来编辑之前的命令时，它会变得更有价值。
你输入了类似这样的命令：

```
$ tr -d '01-5' < Walden.txt | awk 'BEGIN { RS = ""; OFS = " " }\n{ $1 = $1; printf "%s\r", $0 } > Walden.txt
```

上面的命令（全部在一行中运行）似乎很容易导致输入错误。假设你在命令、文件名或某个参数引用或引号中犯了错误。
编辑此命令有多种方法，包括如本章前面介绍的那样，只需按向上方向键将其带回提示符并进行修改。但 `fc` 命令允许你在喜喜欢的文本编辑器中编辑命令，对于复杂的命令，在编辑器中编辑比在命令行中要简单得多。
当你不带参数运行 `fc` 命令时，它会在你的文本编辑器中打开上一个命令。你可以进行任何更改、保存并退出文本编辑器。然后 shell 将运行你编辑后的命令。
你也可以带参数运行 `fc` 命令，例如数字（`fc` 加载历史列表中编号为该数字的命令）或字符串（`fc` 加载你以该字符串开头运行的命令）。

## 实际上手：设置 FCEDIT 变量

`fc` 命令使用你通过 `EDITOR` 变量设置的文本编辑器，或者如果你想为 `fc` 使用不同的编辑器，可以使用 `FCEDIT` 变量。例如，如果你想使用 `pico`，请在你的 `.bash_profile` 文件中输入以下内容：
```bash
FCEDIT=/usr/bin/pico
```

如果你已经设置了 `EDITOR` 变量并想使用相同的文本编辑器，那么就不设置 `FCEDIT` 变量，但这允许你在执行 `fc` 命令时使用更简单的编辑器，而对其他文本处理使用另一个。

## 设置命令历史变量

命令历史可以记录几乎无限数量的命令。根据你如何使用终端，你可能希望历史记录大量的命令，或者只记录少数几个。有几个变量可以让你选择历史文件的大小，以及 shell 是否保存重复项。

## 在 BASH 中设置历史变量

shell 默认记录你的历史；与 `tcsh` 不同，你不需要设置变量来记录历史，这是自动完成的。默认情况下，这个历史文件包含你最后运行的 500 条命令。
但你可能并不想存储 500 条命令：你可能只想保存最后几十条命令，或者可能想存储数千条。你可以通过设置 `HISTSIZE` 变量来更改这一点。
要做到这一点，请向你的 `.bash_profile` 文件中添加以下行：

```bash
export HISTSIZE=n
```

其中 `n` 是你想保存的命令数量。
你还可以选择历史忽略重复命令，或者至少忽略连续的重复命令。要做到这一点，请向你的 `.bash_profile` 文件中添加以下行：

```bash
export HISTCONTROL=ignoredups
```
