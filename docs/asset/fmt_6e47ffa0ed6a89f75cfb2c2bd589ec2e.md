
要查找可执行文件的功能，请输入：
`whatis mkdir`

要将标准输出 (STDOUT) 显示在终端并同时写入文件，请输入：
`ls -l | tee file_name.ext`

要创建多个具有顺序命名的空文件（例如 file1, file2, file3 等），请输入：
`touch file_name{1..100}`

或—
`touch file_name{a..z}`

**示例输出：**
```
user@localhost:~$ touch file_name{1..100}
user@localhost:~$ ls -l
-rw-rw-rw-1 jane root 0 May 13 21:22 file_name1
-rw-rw-rw-1 jane root 0 May 13 21:22 file_name2
-rw-rw-rw-1 jane root 0 May 13 21:22 file_name3
...
```

**注意：** 大括号 `{}` 扩展允许你扩展一组字符。例如，`{1..100}` 将 1 到 100 之间的数字递增地添加到字符串或文件名中。例如，`{ a..z }` 将 A 到 Z 之间的字母递增地添加到字符串或文件名中。其他大括号扩展的示例，输入：
```
echo {0,1}{0..9}
echo {home\*,/root}/.\profile
```

在当前目录下所有文件中搜索字符串 `search_pattern`（末尾的 `*` 是搜索所有文件的通配符），请输入：
`grep -RnisI search_pattern *`

将长文件（即段落）重新格式化为短行，请输入：
`fmt file_name.txt`

**示例输出：**
```
user@localhost:~$ cat text_file.txt
Lorem ipsum dolor sit amet, consectetur adipiscing elit. In quis metus facilisis aliquam quis non nisl.
user@localhost:~$ fmt text_file.txt
Lorem ipsum dolor sit amet, consectetur adipiscing elit. In quis metus facilisis aliquam quis non nisl.
```

显示文件的详细统计信息和属性，请输入：
`stat file_name.ext`

**示例输出：**
```
user@localhost:~$ capture.jpg
File: 'capture.jpg' Size: 5278 Blocks: 16 IO Block: 512 regular file Device: 2h/2d
Inode: 83035118129644079 Links: 1
Access: (0666/-rw-rw-rw-) Uid: (1000/jane) Gid: (1000/jane)
Access: 2018-03-29 19:39:11.953837000 -0700
Modify: 2018-03-29 19:39:11.958023900 -0700
Change: 2018-05-13 21:05:23.751088300 -0700
Birth: -
```

将文件移动到特定目录，请输入：
`mv file_name1 path/to/directory`

Linux 没有特定的文件重命名命令，你必须使用 MV 来更改文件名，请输入：
`mv file_name1 file_name2`

显示关于文件类型的信息，请输入：
`file file_name.ext`

**示例输出：**
```
user@localhost:~$ capture.jpg
capture.jpg: JPEG image data, JFIF standard 1.01, resolution (DPCM), density 66x66, segment length 16, baseline, precision 8, 120x120, frames 3
```

更改文件的所有者，请输入：
`chown user1 path/to/file_name`

文件权限，请输入：
`chmod 644 path/to/file_name`

**注意：** 权限部分：所有者、所有组和其他其它（例如 754，`owner` = 所有，`group` = 读+执行，`world` = 读）。文件权限为：读 = 4，写 = 2，执行 = 1（例如，读(4)+写(2) = 6）

**提示：** 将 file2 的权限更改为与 file1 相同，输入：
`chmod --reference file_name1 file_name2`

递归更改当前路径下所有文件的权限，并忽略目录，请输入：
`find ./ -type f -exec chmod 777 {} \;`

显示目录占用了多少存储空间，请输入：
`du -sh /directory`

## 基础网络命令

这些命令和工具用于执行基础网络管理功能。例如，管理网络连接、显示网络信息等。Linux 有一套非常强大的命令支持网络。

如果你想查看系统的基本网络配置（如 IP 地址、子网掩码、MAC 地址等），请输入：
`ifconfig`

要查看数据包到达远程主机的传输路径（即必须经过的路由器和交换机），请输入：
`traceroute example.com`

**注意：** 关于 `IFCONFIG` 和 `TRACOUTE` 这两个弃用命令，请参见后续章节“弃用命令与替代工具”

检查远程地址是否可访问，请输入：
`ping example.com`

或 `ping 209.67.208.202`（按 Ctrl+C 命令）

**提示：** 当 IP 地址存活时，播放提示音，输入：
`type -a mkdir`

**提示：** 此命令的替代方案是，输入：
`type -a mkdir`

有一个比 vi 更新且改进的版本称为 vim，它是“Vi IM Improved”的缩写。它于1991年在 Amiga 计算机上首次公开发布。它与 vi 向后兼容，并包含了若干增强。

**注意：** 某些发行版仅包含 vim，并将 vi 的别名别了它。

## 启动程序

以下是启动文本编辑器的命令，更多选项可以在帮助文件中找到（例如 `man vim`）：

- `vi file` 编辑或创建文件（如果指定了则创建一个新文件）。
- `vi -r` 显示恢复的文件。
- `vi -r file` 恢复一个已恢复的文件。
- `vi +n file` 编辑文件并将光标置于第 (n) 行。

## 插入模式和命令模式

vi 有两种主要模式：插入模式和命令模式。本节包含了用到的核心概念，理解这两种模式之间的区别至关重要。

编辑器以命令模式启动，在此模式下可以进行光标移动以及文本的粘贴和删除。当激活插入模式（在命令模式下按下 "i" 或 "I" 键）时，用户可以进入并修改文件中的文本。按下 ESC 键（在插入模式下）将编辑器返回到命令模式（例如，通过输入 :x 可以保存并退出）。

在命令模式下，大多数命令在输入后立即执行，但“冒号”命令（例如 :q!）除外，它们在你按下回车键后执行。

## 退出程序

这些命令用于退出程序，并保存文件更改或放弃更改。

- `:x` 退出并保存更改
- `:wq file` 退出程序（如果指定了则创建一个新文件）
- `:q!` 退出（强制，即使未保存）
- `:qa!` 退出所有（强制，即使未保存）

## 插入文本

这些命令用于通过插入、追加和替换来修改文本。你必须在命令模式下才能使用这些功能。

- `i` 在光标前插入
- `I` 在行首插入
- `a` 在光标后追加
- `A` 在行尾追加
- `o` 在当前行之后开启新行
- `O` 在当前行之前开启新行
- `r` 替换一个字符
- `R` 替换多个字符

## 光标移动

这些命令用于在屏幕和文档中移动光标。你必须在命令模式下才能使用这些功能。

- `h` 光标向左移动
- `j` 光标向下移动
- `k` 光标向上移动
- `l` 光标向右移动
- `w` 下一个单词
- `W` 下一个空白分隔的单词
- `b` 单词开头
- `B` 空白分隔单词的开头
- `e` 单词结尾
- `E` 空白分隔单词的结尾（上一个句子）
- `;` 句子向前移动
- `{` 段落后退
- `}` 段落向前移动
- `0` 行首
- `$` 行尾
- `1G` 文件开头
- `G` 文件末尾
- `nG` 文件的第 (n) 行
- `:n` 文件的第 (n) 行
- `fc` 向前到 (c)[字符]
- `Fc` 回到 (c)[字符]
- `tc` 向前到 (c)[字符] 之前
- `Tc` 回到 (c)[字符] 之前
- `H` 屏幕顶部
- `M` 屏幕中部
- `L` 屏幕底部
- `%` 移动到关联的 ( ), { }, [ \]

## 删除文本
