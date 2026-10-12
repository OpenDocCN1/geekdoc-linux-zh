
- **命令、别名或函数** — 如果文本以普通字符开头，Shell 会尝试将文本补全为命令、别名或函数名。
- **主机名** — 如果文本以 @ 符号开头，Shell 会从 /etc/hosts 文件中提取主机名来补全该文本。

> **提示：** 若要添加来自其他文件的主机名，您可以将 HOSTFILE 变量设置为该文件的名称。该文件必须与 /etc/hosts 文件格式相同。

以下是一些命令补全示例。（当您看到 <Tab> 时，意味着按键盘上的 Tab 键。）输入以下内容：

```bash
$ echo $0S<Tab>
$ cd -ro<Tab>
$ fing<Tab>
$ mailx root@loc<Tab>
```

第一个示例导致 $0S 被扩展为 $OSTYPE 变量。在下一个示例中，-ro 被扩展为 root 用户的主目录（~/root/）。接下来，fing 被扩展为 finger 命令。最后，root@loc 的地址被扩展为名为 localhost 的计算机（即本地计算机）。

当然，有时您输入的字符字符串会有多种可能的补全结果。在这种情况下，您可以在想要进行补全的位置按 Esc+? 来查看文本可能的扩展方式。以下是在 $P 处检查可能补全结果时会得到的结果示例。

```bash
$ echo $P<Esc+?>
$PATH $PPID $PS1 $PS2 $PS4 $PWD
$ echo $P
```

在这种情况下，有六个以 $P 开头的可能环境变量。显示这些可能性后，原始命令行会恢复，供您选择如何补全。

如果您试图补全的文本前面没有 $、- 或 @，您仍然可以尝试将文本补全为变量、用户名或主机名。按以下键组合来补全您的文本：

- Alt+~ — 将此点之前的文本补全为用户名。
- Alt+$ — 将此点之前的文本补全为变量。
- Alt+@ — 将此点之前的文本补全为主机名。
- Alt+! — 将此点之前的文本补全为命令名（按此顺序检查别名、保留字、Shell 函数、内建命令和文件名）。换句话说，使用您之前运行过的命令来补全此键序列。
- C+x+/ — 列出可能的用户名文本补全结果。
- C+x+$ — 列出可能的环境变量补全结果。
- C+x+@ — 列出可能的主机名补全结果。
- C+x+! — 列出可能的命令名补全结果。

# 额外的命令行补全

在 Red Hat Linux 7.3 中，有一套新的 Shell 补全规则可用。这些规则在 `/etc/bash_completion` 文件中定义。大多数规则允许您使用适合正在运行的命令的文件来补全命令行。

注意：必须安装 bash-completion 包才能使用本章中描述的补全功能。该包会在您登录后启动 bash Shell 时，从 `/etc/profile.d/bashopts.sh` 文件中激活（source）`/etc/bash_completion` 文件。如果这些功能不起作用，请在 Shell 中输入 `source /etc/bash_completion`。如果出现“没有那个文件或目录”的消息，您需要安装 bash-completion 包。如果 Red Hat Linux 发行版中未包含 bash-completion 包（他们曾在最后一刻考虑移除它），您可以通过在 Internet 上输入 `rpmfind bash-completion` 获取它。

以下是一个快速教程，您可以借此尝试一些 bash 补全功能：

1. 输入 `cd /tmp` 切换到 `/tmp` 目录。
2. 创建几个具有不同文件扩展名的文件。例如：

```bash
$ touch test.mp3 test.gz test.jpg
```

3. 在 `/tmp` 仍为当前目录时，输入 `ee` 命令，输入单词 `test`，并按 Tab 键，如下所示：

```bash
$ ee test<Tab>
```

应该会出现单词 `test.jpg`。这是因为 `ee` 命令（Electric Eyes）可以显示图像文件。因此，bash 补全会补全任何以 `.jpg`、`.gif`、`.png`、`.bmp`、`.xpm` 以及表明图像文件的几种其他扩展名结尾的文件。

4. 按 Ctrl+C 清除该行。然后输入 `gunzip` 命令，输入单词 `test`，并按 Tab 键，如下所示：

```bash
$ gunzip test<Tab>
```

应该会出现单词 `test.gz`。这是因为 `gunzip` 命令可以解压缩通常带有 `.gz`、`.Z`、`.tgz` 和 `.Gz` 文件扩展名的压缩文件。

5. 按 Ctrl+C 清除该行。然后输入 `xmms` 命令，输入单词 `test`，并按 Tab 键，如下所示：

```bash
$ xmms test<Tab>
```

应该会出现单词 test.mp3。这是因为 xmms 命令可以播放通常带有 .mp3、.MP3、.ogg、.pls 和 .OGG 文件扩展名的音频文件。

如果每个命令都能处理多种类型的文件，补全会停留在“test”并允许您再次按 Tab。在那时，您将看到所有与该命令支持的文件类型匹配的文件。例如：

```bash
$ gunzip test<Tab>.<Tab>
test.gz      test.Gz      test.tgz      test.Z
$ gunzip test.
```

因为，在这个示例中，当前目录中有四个与 gunzip 支持类型匹配的不同文件，所以在第二次按 Tab 后显示了这四个文件。然后原始命令行返回，供您输入更多字母以选择文件或尝试再次匹配。

表 3-4 展示了几个可以使用 bash 补全来匹配特定用于各命令的文件的命令。

## 表 3-4：使用 bash 文件名称补全的命令

| 命令类型 | 命令 | 文件扩展名 |
| :--- | :--- | :--- |
| 文件压缩 | bunzip, bcat, bzcmp, bzdiff, bzegrep, bzfgrep, bzgrep | .bz2 |
| | unzip | .zip, .ZIP, .jar, .JAR, .exe, .EXE, .ppk3 |
| | uncompress | .Z |
| 图形 | ee, xv, qiv, display | .gif, .jpg, .jpeg, .tif, .tiff, .png, .pbm, .pgm, .ppm, .bmp, .xpm, .Gif, .JPG, .JPEG, .TIF, .TIFF, .PNG, .PBM, .PGM, .PPM, .BMP, .XMP |
| | gv, ggv | .eps, .ps, .EPSI, .PSI, .eps-gv, .ps.gz, .pdf, .PDF |
| | xfig | .xfig |
| 文档 | xdvi | .dvi, .DVI, .gz, .Z, .bz2 |
| | acroread, xpdf | .pdf, .PDF |
| | makeinfo, texi2dvi, texi2html | .texi |
| | tex, latex, slutex, jadetex, pdfjadetex, pdftex, pdfetex | .tex, .TEX |
| 音频/视频 | mpg123 | .mp3, .MP3 |
| | mplayer | .mpg, .mpeg, .avi, .asf, .vob, .bin, .vcd, .ps, .pes, .fli, .viv, .rm, .ram, .yuv, .mov, .wmv |
| | aviplayer | .avi, .asf |
| | xanim | .mpg, .mpeg, .avi, .mov |
| | ogg123 | .ogg, .OGG |
| | xmms, gqmpeg, freeamp | .mp3, .MP3, .ogg, .OGG, .pls |

还有其他命令，它们不匹配文件名称，而是期望从配置文件或命令输出中获取信息作为参数。表 3-5 展示了期望此类信息（如用户名、组名和运行任务参数）的命令，这些参数可用于 bash 补全。

## 表 3-5：使用来自配置信息的 bash 补全的命令

| 命令类型 | 命令 | 从...获取信息 |
| :--- | :--- | :--- |
| 操作用户 | finger, su, usermod, userdel, passwd | /etc/passwd 文件 |
| 操作组 | groupmod, groupdel | /etc/group 文件 |
| 操作停止的进程 | bg | jobs -s |
| 操作后台进程 | fg, jobs, disown | jobs |
| 操作变量 | readonly, unset | Shell 变量 |
| | set, shopt | set 选项 |
| 显示帮助文本 | help | help 选项（即有可用帮助文本的 Shell 内建命令） |
| 取消别名 | unalias | 设置了别名的命令（输入 alias 查看已设置的别名） |
| 定位命令 | type | 路径目录中的命令名称 |

> **提示：** 如果您按 Tab 但没有补全任何内容，请尝试再次按 Tab。很可能存在多种补全可能性。再次按 Tab 将显示这些可能性。

有关命令行补全的更详细信息，您可以阅读 `/etc/bash_completion` 文件的内容。如果愿意，您甚至可以添加自己的补全定义。以下是来自 `/etc/bash_completion` 文件的定义示例。

```bash
complete -f -X '!*.@(mp3|MP3)' mpg123
```

此定义表明，如果您使用 mpg123 播放器，所有具有 `.mp3` 或 `.MP3` 后缀的文件都应匹配进行补全。要添加自己的定义，您可以复制此行并将 `mpg123` 替换为您使用的应用程序名称，然后将 `mp3` 和 `MP3` 替换为您希望该应用程序匹配的文件后缀。（添加多个管道字符以添加更多后缀。）

# 命令行调用

输入命令行后，整个命令行会保存在您的 Shell 历史记录列表中。该列表存储在一个历史文件中，您可以从中调用任何命令再次运行。调用后，您可以如前所述修改命令行。

要查看历史记录列表的内容，请使用 `history` 命令。您可以输入不带选项的命令，或者在命令后跟随一个数字以列出该数量的最近命令。以下是一个示例：

```bash
$ history 8
382 date
383 ls /usr/bin | sort -a | more
384 man sort
385 cd /usr/local/bin
386 man more
387 useradd -m /home/chris -u 101 chris
388 passwd chris
389 history 8
```

列表中的每个命令行前都有一个数字。有几种方法可以立即从此列表中运行命令，包括：

