# Linux 命令初学者指南：用简单方法学习 Linux 命令、标志和选项



![](img/image_rsrc1F6.jpg)
![](img/image_rsrc1F7.jpg)


## 关于作者
你好，我叫 Rajdeep Singh。我编写这本书是因为我经常在 Linux 命令标记（flags）或选项上遇到困惑。我开始访问网站、阅读书籍以及一些提供信息的文章，但那些文章都太老了。于是，我意识到了这个问题，找到了资源，并开始编写一本关于 Linux 命令行标记的书。我对这本书的梦想是：清晰清晰，每个人都能为这本书贡献力量并改进它。这本书免费供大家阅读和改进。

### 了解更多关于作者：
* [https://medium.com/officialrajdeepsingh/my-learning-path-biology-to-computer-science-70bec32db8ea]
* [https://officialrajdeepsingh.medium.com/]
* [https://www.officialrajdeepsingh.dev/]

### 联系作者：
* [https://www.officialrajdeepsingh.dev/contact-me/]
* officialrajdeepsingh@gmail.com

## 如何贡献
### 如何贡献？
如果你想为开源书籍做出贡献，请确保你有自己的 GitHub 账户并提供你的电子邮件（用于认证）。如果你参与贡献，请确保你有自己的 GitHub 账户并需要电子邮件（用于认证）。

## 法律声明
版权所有。未经出版者许可，不得得以任何形式（电子、机械、复印、扫描或其他方式）复制、存储或传输本书的任何部分。这样做属于违法行为，风险自担。作者对可能造成的损害不承担任何责任。

## 引言
### 什么是 Linux？
Linux 是一个开源类 Unix 操作系统，由 Linus Torvalds 于 1991 年 9 月发布。它是最流行的平台，用于 Android 系统和服务器。

### 谁在使用 Linux？
Linux 无处不在，包括 Windows、macOS 和 iOS。

### 参考文献
* [en.wikipedia.org/wiki](https://en.wikipedia.org/wiki)
* [linux.com/what-is-linux](https://linux.com/what-is-linux)

### 内容简介
本书涵盖了 Linux 命令和标记。如果你想学习更多，请查看示例和内容。作者试图在书中许多标记。

### 为什么要写这本书？
查看 YouTube 播放列表：
* [`www.youtube.com/playlist?list=PLUzr48G11X_S_S_S_S_S_S_S_S_S_S_S`](https://www.youtube.com/playlist?list=PLUzr48G11X_S_S_S_S_S_S_S_S_S_S_S) (保持链接结构不变)

## 第一章：Linux 终端快捷键
### 终端快捷键：
* `Ctrl + L`: 清除屏幕。
* `Ctrl + S`: 停止输出。
* `Alt + Tab`: 切换窗口。
* `Ctrl + A`: 回到首。
* `Ctrl + E`: 回到行尾。
* `Ctrl + F`: 光标向前移动一个字符。
* `Ctrl + B`: 光标向后移动一个字符。
* `Alt + F`: 光标向前一个单词。
* `Alt + B`: 光标向后一个单词。
* `Ctrl + U`: 将字符转换为大写。
* `Alt + l`: 将字符转换为小写。
* `Alt + T`: 交换单词。
* `Alt + D`: 删除光标到行尾的内容。
* `Ctrl + K`: 剪切从当前位置到行尾的内容。
* `Ctrl + W`: 删除光标前的单词。
* `Ctrl + Y`: 粘贴上次剪切的内容。
* `Ctrl + D`: 逐字符删除。
* `Ctrl + T`: 删除空白字符。
* `Shift + Ctrl + W`: 关闭标签页。
* `Shift + Ctrl + Q`: 关闭整个终端。
* `Shift + Ctrl + N`: 打开新窗口。
* `Shift + Ctrl + T`: 在窗口中打开新标签页。
* `Shift + Ctrl + C`: 复制终端内文本。
* `Shift + Ctrl + V`: 粘贴终端内文本。
* `Shift + Ctrl + +`: 放大。
* `Shift + Ctrl + -`: 缩小。
* `Shift + Ctrl + )`: 重置比例。
* `Shift + Ctrl + I`: 为每个打开的标签页添加名称。

## 第二章：基础文本编辑器命令
### nano
`nano` 是命令行中一个小且友好的编辑器。
`nano [options] [file ..]`

## 第三章：基础操作命令
### vim
`vim` 是一个文本编辑器。它可以编辑各种编程语言。它在命令行中编辑时特别有用。
`vim [options] [file ..]`

### whatis
`whatis` 命令有助于显示帮助页的简短描述。
`whatis [CommandName...]`




`which` : `which` 帮助定位你笔记本中的命令存储位置。`which` 命令主要用于你的 bash 脚本。

Syntax: `which [CommandName...]`

## Chapter 4 pwd Command

`pwd` : 显示当前目录。
`pwd --help` : 显示关于 `pwd` 命令的帮助文档。
`pwd --version` : 打印 `pwd` 命令版本。
`pwd -man` : 使用 `-man` 命令读取 `pwd` 手册页。

## Chapter 5 man Command

`man` : `man` 命令提供一个接口，该接口帮助你在终端上阅读手册页参考。

Syntax: `ls [OPTION]... [COMMANDS]...`

配合命令使用的选项：
`man -w` : 此标志不会显示任何手册页，但会打印命令在你的笔记本中的存储位置。
`man -f` 或 `man –whatis` : 如果描述可用，此标志将向你显示手册页的简短描述。
`man man` : 为你提供命令手册页信息。

仅适用于 man 命令的选项：
`man --help` : 此标志为你提供关于 `man` 命令的帮助文档。
`man --usage` : 提供关于命令的短用法消息。
`man -V` 或 `man --version` : 打印 `man` 命令版本。

注意：
- `Man` 命令提供了许多选项，我们建议你访问命令手册页以获取更多信息。
- 退出 `man` 简单使用 `q` 或 `Exit` 命令。
- 键盘方向键用于滚动页面：`↑` 向上滚动，`↓` 向下滚动。

关于 `man` 命令的测验

Q.1 如何检查 `mkdir` 命令的手册页参考？
Ans. `pi@raspberrypi:~ $ man mkdir`
Q.2 如何将命令手册页信息保存到笔记本的 txt 文件中。
Ans. `pi@raspberrypi:~ $ man ls > lsManPages.txt`

## Chapter 6 ls Command

`ls` : 提供目录内存在文件的信息。默认按字母顺序提供当前目录信息。

Syntax: `lsOPTION]... [FILE]...`

命令选项：
`ls -a` : 在终端内显示所有文件。
`ls -A` : 意味着几乎所有文件，但不显示 `.` 和 `..` 文件。
`ls -l --author` : 此命令配合 `-l` 标志或选项工作，并打印每个文件的作者信息。
`ls -b` : `ls` 命令提供了一个选项 - 当使用时会对不可打印字符打印 C 风格的转义字符。
`ls --block-size=SIZE` : 此标志将你的文件转换为不同的大小。例如兆字节、字节等。
- `ls -l --block-size=K` : 将文件转换为字节。
- `ls -l --block-size=M` : 将文件转换为兆字节。
`ls -c` : 此标志为你提供输出，显示你最近修改的文件，此选项永远不会与 `-l` 标志配合工作。
`ls --color[=WHEN]` : 用彩色显示输出。默认始终为自动。如果你停止此项，你将永远不会使用。
- `ls –color=never`
- `ls –color=auto`
`ls -G` : 在不带组名打印列表。
`ls -h` 或 `ls --human-readable` : 配合 `-l` 和 `-s` 打印输出。在 CMD 中显示类似 1K 234M 2G 的文件大小。
`ls -i` 或 `ls --inode` : 打印你的命令中每个文件的索引号。
`ls -k` 或 `ls --kibibytes` : 此标志显示每个文件的块大小。默认每个块大小为 1024 字节.--k` 标志配合 `-s` 标志工作。
`ls -l` : 在你的命令中打印长列表信息格式模式。
`ls -m` : `m` 标志显示逗号分隔的文件项列表。
`ls -n` 或 `ls --numeric-uid-gid` : 显示数字用户和组 ID。
`ls -N` : `-N` 标志打印不带逗号分隔或引号（`,`）的文件名。
`ls -o` : 不带组信息打印信息。
`ls -p` 或 `ls --indicator-style=slash` : 在你的目录文件名后附加斜杠 `/`。

注意：指示-style 的工作方式相同，或 `--indicator-style` 参数有：
- ‘none’
- ‘slash’
- ‘file-type’
- ‘classify ’
`ls -Q` 或 `ls --quote-name` : 用双引号显示你的文件名。
`ls --quoting-style="escape"` : 样式化你终端内的引号。更多参数有：
- ‘literal’
- ‘shell’
- ‘shell-always’
- ‘shell-escape’
- ‘shell-escape-always’
- ‘c’
- ‘c-maybe’
- ‘escape’
- ‘Locale’
- ‘clocale’
`ls -r` 或 `ls --reverse` : 逆序打印你的文件（z 到 a）。
`ls -R` 或 `ls --recursive` : 打印你的所有文件以及子目录文件。
`ls -s` 或 `ls --size` : 以块形式打印每个文件的大小。
`ls -S` : 按文件大小排序，最大的在前。
`--sort='none'` : 根据时间和大小等参数排序你的文件。更多有效的参数有：
- ‘none’
- ‘time’
- ‘size’
- ‘extension’
- ‘version’
`ls -t` : 根据修改时间排序你的文件，最新创建的在前。
`ls -X` : 按字母顺序排序你的文件。
`ls -1` : 每行打印一个文件列表。
`ls --help` : 显示关于 `ls` 命令的文档。
`ls --version` : 打印 `Ls` 命令版本。
`ls -man` : 使用 `-man` 命令检查你的手册页。

关于 `ls` 命令的测验

Q1. 如何在 `ls` 命令中列出多个目录？
Ans. `pi@raspberrypi:~ $ ls Blog Documents`
Q2. 如何访问目录内的隐藏文件？
Ans. `pi@raspberrypi:~ $ ls -a`
Q3. 如何打印文件的长列表格式？
Ans. `pi@raspberrypi:~ $ ls -l`
Q4. 逆序打印目录（z 到 a）
Ans. `pi@raspberrypi:~ $ ls -r`
Q5. 如何阅读 `ls` 手册页？
Ans. `pi@raspberrypi:~ $ man ls`

## Chapter 7 mkdir Command

`mkdir` : `mkdir` 命令帮助创建新目录。如果目录已经存在，则不会创建新目录并在终端内给出警告消息。

Syntax: `mkdir [OPTION]... DIRECTORY...`

命令选项：
`mkdir -m=Mode` linuxBook: `-m` 选项帮助为文件分配新权限（类似于 `chmod`）。模式选项有：
- `rwx` : 对此文件的读、写、执行权限
- `wx` : 仅对此文件的写、执行权限
- `rx` : 仅对此文件的读、执行权限
`mkdir -p` 或 `mkdir --parents` : -p 选项如果文件存在则不显示错误。不覆盖你的文件。
`mkdir -v` 或 `mkdir --verbose` : 在每个创建的目录后打印消息--help` : 显示此帮助并退出--version` : 输出 `mkdir` 命令信息。 `man mkdir` : 在你的工具中打印 `mkdir` 手册页信息。

关于 `mkdir` 命令的测验

Q1. 如何使用 `mkdir` 创建多个目录？
Ans. `pi@raspberrypi:~ $ mkdir linux linuxBook`
Q2. 创建一个新的 Linux 目录并添加一些读执行权限？
Ans. `pi@raspberrypi:~ $ mkdir m='rx' linux`
Q3. 打印 `mkdir` 命令手册页？
Ans. `pi@raspberrypi:~ $ man mkdir`

## Chapter 8 rmdir Command

`rmdir` : `rmdir` 命令帮助删除你笔记本中的空目录。你不会删除文件。

Syntax: `mkdir [OPTION]... DIRECTORY...`

命令选项：
`rmdir --ignore-fail-on-non-empty` : 此选项在删除多个目录时有用。我们不确定哪些文件为空。在这种情况下，此标志会忽略非空目录且不显示“目录为空”的错误。
`rmdir -p` 或 `rmdir --parents` : 默认 `rmdir` 命令可以使用子目录文件夹，如 `rmdir a/b/c/d`，此时 `rmdir` 只删除 d 文件夹。如果你使用 `-p` 或 `--parents` 标志，你会删除整个子目录。
`rmdir -v` 或 `rmdir --verbose` : 为每个目录过程在终端内打印诊断结果--help` : 显示此帮助并退出--version` : 输出 `mkdir` 命令信息。 `man rmdir` : 在你的工具中打印 `rmdir` 手册页。

关于 `rmdir` 命令的测验

Q1. 如何删除 Linux 空目录？
Ans. `pi@raspberrypi:~ $ rmdir linux`
Q2. 最近我创建了一个包含 test.txt 文件的 Linux 目录。现在告诉我 `rmdir` 命令是否工作以及为什么。
Ans. 不工作。因为 `rmdir` 命令只删除空目录
Q3. 打印 `mkdir` 命令手册页？
Ans. `pi@raspberrypi:~ $ man mkdir`

## Chapter 9 rm Command




# rm 命令

`rm` 命令帮助你删除文件或目录。

**语法：**
`rm [OPTION]... [FILE]...`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `rm -f` 或 `rm --force` | 此标志在不询问提示权限的情况下删除所有文件或目录。 |
| `rm -i` | 此命令选项首先通过提示来询问你是否有权限删除文件。你输入输入 Yes，则会删除该文件。 |
| `rm -I` | 仅在有提示时询问一次权限。然后删除所有文件。 |
| `rm -r` 或 `rm -R` 或 `rm --recursive` | 此标志用于递归地删除目录、子目录和文件及其内容。 |
| `rm -d` 或 `rm --dir` | 此标志仅删除空目录。 |

*   `rmdir -v` 或 `mkdir –verbose`: 解释正在执行的操作。
*   `rmdir --help`: 显示此帮助信息并退出。
*   `rmdir –version`: 输出 `mkdir` 命令的版本信息。
*   `man rmdir`: 在你的命令行工具中打印 `rmdir` 手页信息。

### 关于 rm 命令的测试

**Q1. 在不提示权限的情况下删除 `test.txt` 文件？**
答。`pi@raspberrypi:~$ rm -f test.txt`

**Q2. 如何删除多个文件？**
答。`pi@raspberrypi:~$ rm -f test.txt test2.txt`

**Q3. 在不提示权限的情况下删除我的子目录和文件？**
答。`pi@raspberrypi:~$ rm -r test`

**Q4. 如何删除一个空的 Linux 目录？**
答。`pi@raspberrypi:~$ rm -d Linux`

## 第 10 章 cp 命令

`cp`: 使用 `cp` 命令帮助你拷贝电脑内部的文件和目录。

**语法：**
`cp [OPTION]... SOURCE... DIRECTORY`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `cp -i` 或 `cp --interactive` | 此标志在覆盖你的文件之前通过提示询问你权限。 |
| `cp -R` 或 `cp -r` 或 `cp –recursive` | 此标志用于拷贝包含所有文件的目录。 |

*   `rmdir -v` 或 `mkdir –verbose`: 在终端内打印正在执行操作的说明信息。
*   `rmdir --help`: 显示此帮助信息并退出。
*   `rmdir –version`: 输出 `mkdir` 命令的版本信息。
*   `man rmdir`: 在你的命令行工具中打印 `rmdir` 手页信息。

**注意：** 阅读 Man 手页以获取关于 `cp` 命令的所有信息。

### 关于 cp 命令的测试

**Q.1 如何拷贝 `js` 目录中包含所有文件的整个 Javascript 目录？**
答。`pi@raspberrypi:~ $ cp -r javascript js`

**Q.2 如何打开 `cp` 手页文档？**
答。`pi@raspberrypi:~ $ man cp`

## 第 11 章 wc 命令

`wc`: `wc` 命令为每个文件提供字数和字节数。

**语法：**
`wc [OPTION]... [FILE]...`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `wc -c` 或 `wc –bytes` | 此标志帮助以字节为打印文件大小。 |
| `wc -m` 或 `wc --chars` | 此标志打印文件的字符数。 |
| `wc -l` 或 `wc --lines` | 打印文件的总行数。 |
| `wc -L` 或 `wc –max-line-length` | 打印文件中最长的一行。 |
| `wc -w` 或 `wc --words` | 打印文件的总字数。 |
| `wc --help` | 显示此帮助信息并退出。 |

*   `wc –version`: 输出 `wc` 命令的版本信息。
*   `man wc`: 在你的命令行工具中打印 `wc` 手页信息。

### 关于 wc 命令的测试

**Q.1 如何统计文件行数？**
答。`pi@raspberrypi:~ $ wc -l manCommand.txt`

**Q.2 如何统计文件字数？**
答。`pi@raspberrypi:~ $ wc -w manCommand.txt`

**Q.3 在多个文件上运行 `wc` 命令？**
答。`pi@raspberrypi:~ $ wc ls.txt test.txt`

**Q.4 如何在 `wc` 命令中查找文件大小？**
答。`pi@raspberrypi:~ $ wc -c ls.txt`

## 第 12 章 cd 命令

`cd`: `cd`（切换目录）命令用于在 Linux 中更改当前工作目录。`cd` 不是一个命令，它默认内置在你的 shell 中。这是必要的，因为你当前的工作目录是由名为 `pwd` 的环境变量控制的，该变量源自 `pwd` 或“打印工作目录”命令。

**语法：**
`cd [DIRECTORY]`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `cd` | 回到用户主目录。 |
| `cd ~` | 回到主目录。 |
| `cd ..` | 返回上一级目录。 |
| `cd -` | 回到上一个目录。 |

### 关于 cd 命令的测试

**Q.1 如何切换到包含 `js` 目录的所有主目录？**
答。`pi@raspberrypi:~ $ cd ~`

**Q.2 如何进入上一级目录？**
答。`pi@raspberrypi:~ $ cd ..`

**Q.3 如何返回上一个目录？**
答。`pi@raspberrypi:~ $ cd -`

## 第 13 章 mv 命令

`mv`: `mv` 命令用于移动或重命名文件。

**语法：**
`mv [OPTION]... SOURCE... DEST`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `mv -f` 或 `mv --force` | 此标志在不询问提示权限的情况下强制移动现有文件。 |
| `mv -i` 或 `mv --interactive` | 此标志在覆盖你的文件之前通过提示询问你权限。 |
| `mv -v` 或 `mv --verbose` | 显示正在执行什么操作。 |

### 关于 mv 命令的测试

**Q.1. 在不提示权限的情况下移动 `test.txt`？**
答。`pi@raspberrypi:~$ mv -f test.txt /tmp/`

**Q.2. 如何重命名文件？**
答。`pi@raspberrypi:~$ mv oldname.txt newname.txt`

**Q.3. 如何移动我的子目录和文件且不提示？**
答。`pi@raspberrypi:~$ mv test /home/user/`

## 第 14 章 cat 命令

`cat`: `cat` 命令连接并显示文件。

**语法：**
`cat [OPTION]... [FILE]...`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `cat -A` 或 `cat --show-all` | 显示所有隐藏字符。 |
| `cat -b` 或 `cat --number` | 对非空行进行行号。 |
| `cat -E` 或 `cat --show-ends` | 在行尾显示 `$` 符号。 |
| `cat -n` 或 `cat --number` | 对所有行进行行号。 |
| `cat -T` 或 `cat --show-tabs` | 将制表符显示为 `^I`。 |
| `cat -S` 或 `cat --squeeze-tabs` | 压缩连续的空格。 |
| `cat -v` 或 `cat --help` | 显示不可打印字符。 |

### 关于 cat 命令的测试

**Q.1. 如何查看 `test.txt` 的内容？**
答。`pi@raspberrypi:~$ cat test.txt`

**Q.2. 如何带行号显示文件？**
答。`pi@raspberrypi:~$ cat -n file.txt`

**Q.3. 如何合并多个文件？**
答。``pi@raspberrypi:~$ cat file1.txt file2.txt > combined.txt`

## 第 15 章 touch 命令

`touch`: `touch` 更新时间戳并创建空文件。

**语法：**
`touch [OPTION]... FILE`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `touch -a` 或 `touch --access` | 仅更改访问时间。 |
| `touch -c` 或 `touch --no-create` | 如果文件不存在则不创建任何空文件。 |
| `touch -d` 或 `touch --date="STRING"` | 此标志帮助为文件分配自定义的时间和日期。 |
| `touch -m` | 仅更改修改时间。 |
| `touch -t [[CC]YY]MMDDhhmm[.ss]` | 使用时间格式设置时间。 |

### 关于 touch 命令的测试

**Q.1. 如何使用 touch 命令创建一个空文件？**
答。`pi@raspberrypi:~$ touch newfile.txt`

**Q.2. 如何修改文件的日期？**
答。`pi@raspberrypi:~$ touch -d="2023-01-01" file.txt`

## 第 16 章 head 命令

`head`: `head` 命令输出文件的开头部分。

**语法：**
`head [OPTION]... [FILE]...`

| 命令选项（标志） | 描述 |
| :--- | :--- |
| `head -n NUMBER` 或 `head --lines=NUMBER` | 输出前 NUMBER 行。 |
| `head -c NUMBER` 或 `head --bytes=NUMBER` | 输出前 NUMBER 字节。 |

### 关于 head 命令的测试

**Q.1. 如何查看文件的前 10 行？**
答。`pi@raspberrypi:~$ head file.txt`

**Q.2. 如何查看文件的前 5 行？**
答。`pi@raspberrypi:~$ head -n 5 file.txt`





# head 命令

`head` : 默认打印每个文件的前 10 行。你可以对两个以上的文件使用 `head` 命令。

### 语法
`head [OPTION]... [FILE]...`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `head -n` | 该标志帮助打印文件的特定行，或每个文件多于 10 行。示例：`pi@raspberrypi:~ $ head -20 cat.txt` |
| `head --lines=NUM` | 该标志也打印文件的特定行或每个文件多于 10 行。示例：`pi@raspberrypi:~ $ head --lines=30 cat.txt` |
| `head -v` 或 `head --verbose` | 该标志在顶部打印文件名，并在打印头信息后再次打印。 |
| `head --help` | 显示此帮助信息并退出。 |
| `head --version` | 输出 `head` 命令的版本信息。 |
| `man head` | 在你的命令行工具中打印 `head` 命令的帮助页信息。 |

### 关于 head 命令的测试
**Q.1** 如何打印 `linux.txt` 文件的前 20 行？
答。`pi@raspberrypi:~ $ head -20 cat.txt`

**Q.2** 如何打印两个以上文件的文件头信息？
答。`pi@raspberrypi:~ $ head cat.txt ls.txt mv.txt`

## 第 17 章：tail 命令

`tail` : 打印每个文件的最后 10 行。你可以对两个以上的文件使用 `tail` 命令。

### 语法
`tail [OPTION]... [FILE]...`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `tail -n` | 该标志帮助打印文件的特定行，或每个文件多于 10 行。示例：`pi@raspberrypi:~ $ tail -20 cat.txt` |
| `tail --bytes=NUM` | 该标志也根据文件大小打印。示例：`pi@raspberrypi:~ $ tail --bytes=300 cat.txt` |
| `tail -v` 或 `tail --verbose` | 该标志在顶部打印文件名，并在打印 tail 头信息后再次打印。 |
| `tail --help` | 显示此帮助信息并退出。 |
| `tail --version` | 输出 `tail` 命令的版本信息。 |
| `man tail` | 在你的命令行工具中打印 `tail` 命令的帮助页信息。 |

### 关于 tail 命令的测试
**Q.1** 如何打印 `linux.txt` 文件的最后 30 行？
答。`pi@raspberrypi:~ $ tail -30 cat.txt`

**Q.2** 如何打印两个以上文件的文件头信息？
答。`pi@raspberrypi:~ $ tail cat.txt ls.txt mv.txt`

## 第 18 章：find 命令

`find` : 用于在目录层次结构中搜索文件。

### 语法
`find [Directory] [Option] [Expression]`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `find -name` | 该标志帮助通过名称查找文件。 |
| `find -size` | 根据文件大小查找文件，连同大小标准传递 `-size` 参数。你可以以下后缀来指定文件大小：<br>● `b` : 512 字节块（默认）<br>● `c` : 字节<br>● `w` : 双字节字<br>● `k` : 千字节 (KB)<br>● `M` : 兆 (MB)<br>● `G` : 吉字节 (GB) |
| `find -atime n` | 该标志显示最后访问的文件。示例：`pi@raspberrypi:~ $ find . -atime 1` |
| `find -cmin n` | 该标志显示在最后一分钟内状态变化的文件。 |
| `find -ctime n` | 该标志显示在 24 小时内变化的状态。 |
| `find -mtime n` | 可以指定数字参数：<br>● `+n` : 大于 `n`<br>● `-n` : 小于 `n`<br>● `n` : 恰等于 `n` |
| `find --help` | 显示此帮助信息并退出。 |
| `man find` | 在命令行工具中打印 `find` 帮助页信息。 |

### 关于 find 的测试
**Q.1** 如何在根目录下查找所有 txt 文件？
答。`pi@raspberrypi:~ $ find /`

**Q.2** 如何查找 `.txt` 文件？
答。`pi@raspberrypi:~ $ find .txt`

## 第 19 章：echo 命令

`echo` : 用于显示作为参数传递的行。

### 语法
`echo [OPTION] [STRING]`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `echo -n` | 该标志不输出换行符。 |
| `echo -e` | 该标志启用反斜杠转义解释：<br>● `b` : 删除空格。<br>● `r` : 添加回车。<br>● `n` : 添加换行。<br>● `t` : 添加水平制表。<br>● `v` : 添加垂直制表。 |
| `echo --help` | 显示此帮助信息并退出。 |
| `echo --version` | 输出版本信息。 |
| `man echo` | 打印 `echo` 帮助页。 |

### 关于 echo 的测试
**Q.1** 如何启用反斜杠转义？
答。`pi@raspberrypi:~ $ echo -e "My\nName"`

**Q.2** 如何禁用反斜杠转义？
答。`pi@raspberrypi:~ $ echo "My\nName"`

## 第 20 章：进程命令

`pidof` : 查找当前运行程序的进程 ID。

### 语法
`pidof [programName]`

`ps` : 显示当前工作进程的快照。

### 语法
`ps [options]`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `ps -ux` | 该标志显示笔记本上所有的工作进程。 |
| `ps -e` | 该标志显示所有工作进程的简要描述。 |

`top`: `top` 命令将显示运行进程列表以及每个进程使用的 CPU 情况。它提供了系统的动态实时视图。

### 语法
`top [OPTIONS]`
注意：所有进程命令都有自己的选项或标志。请使用 `man` 命令阅读帮助页。

## 第 21 章：Kill 命令

`kill`: 有时程序没有响应，你可以通过使用 `kill` 命令手动终止进程。

### 语法
`kill [options] [pid...]`

### 命令选项 (Flag)
| Flag | 描述 |
| :--- | :--- |
| `kill [pid]` | 该标志杀死指定或进程列表。示例：`pi@raspberrypi:~ $ kill 2345` |
| `kill -9 -1` | 该标志杀死笔记本或电脑上当前运行的所有进程。 |
| `kill -9` | 当进程无法通过 `kill` 命令终止时，该标志很有帮助。使用 `-9` 标志可以轻松杀死进程。 |
| `kill -Kill` | 该标志的作用与 `-9` 标志相同。 |

### 关于 Kill 命令的测试
**Q.1** 如何通过 kill 命令杀死多个进程？
答。`pi@raspberrypi:~ $ kill 2326 2349`

**Q.2** 如何杀死笔记本上当前运行的所有进程？
答。`pi@raspberrypi:~ $ kill -9 -1`





## 日期
`date` 命令打印系统日期和时间。

语法：`date [OPTION]... [FORMAT]...`

### 命令选项(标志)
### 
- `date -r` 或 `date --reference=FILE` : 此标志用于显示 `FILE` 的最后修改时间
- `date -s` 或 `date --set=STRING` : 此标志用于设置或更改笔记本电脑或电脑上的系统日期
- `date -u` 或 `date --utc` 或 `date --universal` : 此标志打印协调世界时 (UTC)
- `date --help` : 显示此帮助信息并退出
- `date --version` : 输出版本信息并退出
- `man date` : 此命令帮助你打印帮助页信息。

### 格式选项
- `+%a` : 打印星期简写（例如 Sun）
- `+%A` : 打印本地区域的完整星期名称（例如 Sunday）
- `+%b` : 打印本地区域的月份缩写（例如 Jan）
- `+%B` : 打印本地区域的完整月份名称（例如 January）
- `+%c` : 打印本地区域的日期和时间（例如 Thu Mar 3 23:05:25 2005）
- `+%C` : 打印年份后两位（例如 20）
- `+%d` : 打印月份中的几（例如 01）
- `+%D` : 打印格式与 `%m/%d/%y` 相同的日期
- `+%e` : 打印日期（例如 1-31）
- `+%F` : 打印与 `%Y-%m-%d` 相同的完整日期
- `+%g` : ISO 周数年份的后两位（参见 `%G`）
- `+%G` : ISO 周数的年份（参见 `%V`）；通常只配合 `%V` 使用
- `+%h` : 与 `%b` 相同
- `+%H` : 小时（00..23）
- `+%I` : 小时（01..12）
- `+%j` : 一年中的第（001..366）
- `+%m` : 月份（01..12）
- `+%M` : 分（00..59）
- `+%n` : 添加换行符
- `+%N` : 打印纳秒（000000000..999999999）
- `+%p` : 打印本地区域对应的 AM 或 PM；如果未知则留空
- `+%P` : 类似于 `%p`，但小写
- `+%r` : 本地区域的 12 小时制时间（例如 11:11:04 PM）
- `+%R` : 24 小制时分；与 `%H:%M` 相同
- `+%s` : 自 1970-01-01 00:00:00 UTC 以来的秒
- `+%S` : 秒（00..60）
- `+%t` : 打印制表符
- `+%T` : 打印与 `%H:%M:%S` 相同的时间
- `+%u` : 星期（1..7）；1 是周一
- `+%U` : 年周，以星期日为一周的第一天（00..53）
- `+%V` : ISO 周数，以周一为一周的第一天（01..53）
- `+%w` : 星期（0..6）；0 是星期日
- `+%W` : 年周，以周一为一周的第一天（00..53）
- `+%x` : 本地区域的日期表示（例如 12/31/99）
- `+%X` : 本地区域的时间表示（例如 23:13:48）
- `+%y` : 年份的后两位（00..99）
- `+%Y` : 打印完整年份
- `+%Z` : 时区缩写（例如 EDT）

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

### 关于 date 命令的测试
Q1. 如何使用 `date` 命令设置自定义日期？
答：`pi@raspberrypi:~ sudo date -s "12/17/2020 05:26"`
Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

（注：原文中的重复测试部分已合并以保持清晰度）

---

## cal 命令
`cal` 命令显示日历。

Q1. 如何使用 `cal` 命令查看日历？

### 格式选项
### 描述
- `+%D` : 打印格式与 `%m/%d/%y` 相同的日期

Q2. 如何使用格式打印带有 AM/PM 的完整日期和时间？
答：`pi@raspberrypi:~ $ date '+A'`

---

## tar 命令
`tar` 命令用于文件归档。

### 描述
- `-c` : 创建新归档
- `-x` : 从归档中提取文件
- `-v` : 详细输出
- `-f` : 使用归档文件
- `-z` : 使用 gzip 压缩
- `-j` : 使用 bzip2 压缩
- `-n` : 在后添加换行
- `-u` : 更新归档中的文件
- `-t` : 列出归档中的文件
- `-r` : 向归档追加文件
- `-W` : 提取后列出文件
- `-P` : 不提取领先斜杠

---

## groups 命令
`groups` 显示用户所属的组。

### 描述
- `groups` : 列出当前用户的组

---

## groupadd 命令
`groupadd` 命令创建一个新组。

字体 选项
- `-r` : 创建系统组
- `-f` : 即使组存在也强制创建
- `-g` : 指定 GID
- `-o` : 允许非唯一的 GID
- `-p` : 设置加密密码
- `-K` : 覆盖 GID_MIN 和 GID_MAX 设置

---

## groupdel 命令
`groupdel` 命令删除现有组。

### 选项
- `-R` : 在根目录下应用更改

---

## group 命令
`group` 命令提供组数据库的信息。

---

## useradd 命令
`useradd` 命令用于在系统中创建新用户。





## userdel 命令

`userdel`: Linux 系统中的 `userdel` 命令用于删除用户账户及相关文件。

### 语法
`userdel [OPTIONS] UserName`

### 命令选项(标志)
| 选项 | 描述 |
| :--- | :--- |
| `userdel -r` 或 `userdel --remove` | 使用 `-r` 标志强制 `userdel` 同时删除用户的家目录。 |
| `userdel -h` 或 `userdel --help` | 显示帮助信息并退出。 |
| `userdel -f` 或 `userdel --force` | 此选项强制删除用户账户，即使该用户仍登录登录。它还会强制 `userdel` 删除用户的家目录和邮件邮箱，即使有其他用户正在使用该家目录，或者该邮件邮箱的所有者不是指定的该用户。 |

## sudo 命令

`sudo`: `sudo` (Super User DO) 命令允许你以另一个用户（默认是 root 用户）的安全权限运行程序。`sudo` 是你会非常频繁地使用的命令之一。

### 语法
`sudo [OPTION] [COMMAND]`

### 命令选项(标志)
| 选项 | 描述 |
| :--- | :--- |
| `sudo -V` 或 `sudo --version` | 该选项打印 Sudo 命令的版本。 |
| `sudo -l` | `-l` 选项将打印允许的命令列表。 |
| `sudo -h` 或 `sudo --help` | `-h` (help) 选项打印简短帮助信息并退出。 |
| `sudo -v` | 如果给出 `-v` (validate) 选项，`sudo` 将更新用户的时间戳，必要时提示用户输入密码。这会将 `sudo` 的超时时间延长 5 分钟（或在 sudoers 中指定的时间），但不会运行命令。这不会产生任何输出。 |
| `sudo -k` | `sudo` 的 `-k` (kill) 选项使用户的时间戳失效。因此下次运行 `sudo` 时需要密码。此选项不需要密码，添加目的是允许用户从注销文件中撤销 sudo 权限。 |
| `sudo -K` | 与 `-k` 选项类似，`-K` (sure kill) 选项用于完全移除用户的时间戳。同样，此选项不需要密码。 |
| `sudo -b` | `-b` (background) 选项告诉在后台运行指定的命令。注意，无法使用 shell 作控制来操作由 sudo 启动的后台进程。大多数交互式命令在后台将无法正常工作。 |
| `sudo -p` | `-p` (prompt) 选项允许你覆盖默认密码提示并使用自定义提示。 |

## apt-get 命令

`apt-get`: `apt-get` 是处理 Debian Linux 系统内部软件包的命令行工具。Debian 使用 `dpkg` 软件包系统。软件包系统是一种提供程序和应用程序安装的方式。`APT` (高级软件包工具) 是与此软件包系统交互的命令行工具。你可以用它查找并安装新包、升级包、清理包等。

### 语法
`sudo apt-get [options] command`

### 命令
| 命令 | 描述 |
| :--- | :--- |
| `update` | `update` 命令用于更新你笔记本电脑的软件包索引。`update` 命令是从源处重新同步软件包索引文件。可用软件包的索引是从 `/etc/apt/sources.list` 中指定的位置获取的。此命令帮助更新你笔记本电脑或电脑内部的软件包。 |
| `upgrade` | 此命令用于安装用户系统中当前安装的软件包的最新版本。 |
| `install` | `install` 命令后跟一个或多个在系统中想要安装或升级的软件包。系统中的每个包都通过其包名进行安装。 |
| `remove` | 此命令类似于 `Install` 命令，但主要区别是它移除软件包而不是安装它们。它不会移除由软件包创建的任何配置文件。 |
| `purge` | 此命令移除软件包，并同时移除与软件包相关的任何配置文件。 |
| `check` | 此命令用于更新软件包缓存并检查损坏的依赖关系。 |
| `download` | 此命令用于在当前目录下载指定的二进制包。 |
| `autoremove` | 有时，为了满足其他包的依赖而自动安装的包可能不再需要。`autoremove` 命令用于移除此类包。 |

### 命令选项(标志)
| 选项 | 描述 |
| :--- | :--- |
| `apt-get -q` 或 `apt-get --quiet` | 当指定此选项时，`apt-get` 产生的输出适用于日志记录。 |
| `apt-get -V` 或 `apt-get --verbose-versions` | 显示已升级和已软件包的完整版本。 |
| `apt-get --reinstall` | 重新安装已安装且为最新版本的软件包。 |
| `apt-get -h` 或 `apt-get --help` | 此命令显示简短的使用摘要。 |
| `apt-get -v` 或 `apt-get --version` | 此命令在你的 CMD 中显示程序版本。 |

*注意。我们涵盖了一些命令或选项，请阅读手册页以获取更多更新。*

## grep 命令

`grep`: `grep` 命令是一种基于 Linux 的命令行工具，用于在指定文件中搜索字符串和模式。

### 语法
`grep [OPTION...] PATTERNS [FILE]`

### 命令
| 命令 | 描述 |
| :--- | :--- |
| `grep --help` | 输出用法信息并退出。 |
| `grep -V` 或 `grep --version` | 输出 grep 版本并退出。 |
| `grep -i` 或 `grep --ignore-case` | 此标志用于区分大小写敏感和不区分大小写。 |
| `grep -c` | 仅打印匹配的行数。 |
| `grep -h` | 显示匹配的行，但不显示文件名。 |
| `grep -i` 或 `grep --ignore-case` | 此标志用于区分大小写敏感和不区分大小写。 |
| `grep -l` | 显示文件名列表。 |
| `grep -n` | 显示匹配的行及其行号。 |
| `grep -v` | 打印所有不匹配的行。 |
| `grep -e` | 指定表达式。可以使用多次。 |
| `grep -f` | 从文件读取模式，每行一个。 |
| `grep -E` | 将模式视为扩展正则表达式 (ERE)。 |
| `grep -w` | 匹配整个单词。 |
| `grep -o` | 仅打印匹配的部分，每个部分单独占一行输出。 |

*注意：阅读手册页查看所有选项。*

## chmod 命令

`chmod`: 我们可以使用 `chmod` 命令，意为“更改模式”。使用该命令，我们可以为文件/目录设置权限（读、写、执行）。

### 语法
`chmod [Option]... [Permissions] fileName`

三个数字定义了用户、组和其他人的的权限。
- `r`: 读取文件的权限。
- `w`: 写入（或删除）文件的权限。
- `x`: 执行文件的权限。

### 权限示例
| 符号 | 进制 | 描述 |
| :--- | :--- | :--- |
| `rwx` | 111 | 读、写、执行 |
| `rw-` | 110 | 读、写 |
| `r-x` | 101 | 读、执行 |
| `r--` | 100 | 仅读 |
| `-wx` | 011 | 写、执行 |
| `-w-` | 010 | 仅写 |
| `--x` | 001 | 仅执行 |
| `---` | 000 | 无 |

### 命令选项(标志)
| 选项 | 描述 |
| :--- | :--- |
| `chmod -R` 或 `chmod --recursive` | 递归地更改文件和目录 |
| `chmod --help` | 显示此帮助并退出 |
| `chmod --version` | 输出版本信息并退出 |

`man chmod`: 此标志用于阅读手册页。

