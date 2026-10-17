
你在 shell 提示符下输入 Linux 命令。通过 *Linux 命令*，我的意思是 `bash` shell 理解的一些命令以及随 Linux 提供的命令行实用程序。在本节中，我介绍 Linux 命令的几个主要类别。

我无法在本章中涵盖每一个 Linux 命令，但我想通过向你展示常见的 Linux 命令，让你感受到命令的广度。表 3-2 按类别列出了常见的 Linux 命令。在开始记忆任何 Linux 命令之前，请浏览此表。

## 表 3-2 基本 Linux 命令

| Command Name | Action |
|---|---|
| **Finding help and abbreviations** |  |
| `apropos` | Finds online manual pages for a specified keyword. |
| `info` | Displays online help information about a specified command. |
| `man` | Displays online help information. |
| `whatis` | Searches for complete words only and finds the online manual pages. |
| `alias` | Defines an abbreviation for a long command. |
| `type` | Shows the type and location of a command. |
| `unalias` | Deletes an abbreviation defined with `alias`. |
| **Managing files and directories** |  |
| `cd` | Changes the current directory. |
| `chmod` | Changes file permissions. |
| `chown` | Changes the file owner and group. |
| `cp` | Copies files. |
| `ln` | Creates symbolic links to files and directories. |
| `ls` | Displays the contents of a directory. |
| `mkdir` | Creates a directory. |
| `mv` | Renames a file and moves the file from one directory to another. |
| `rm` | Deletes files. |
| `rmdir` | Deletes directories. |
| `pwd` | Displays the current directory. |
| `touch` | Updates a file's time stamp. |
| **Finding files** |  |
| `find` | Finds files based on specified criteria, such as name and size. |
| `locate` | Finds files by using a periodically updated filename database. (The database is created by the `updatedb` program.) |

(continued)

## 表 3-2（续）

| Command Name | Action |
|---|---|
| `whereis` | Finds files based in the typical directories where *executable* (also known as *binary*) files are located. |
| `which` | Finds files in the directories listed in the `PATH` environment variable. |
| Processing files |  |
| `cat` | Displays a file in standard output (can be used to concatenate several files into one big file). |
| `cut` | Extracts specified sections from each line of text in a file. |
| `dd` | Copies blocks of data from one file to another (used to copy data from devices). |
| `diff` | Compares two text files and finds any differences. |
| `expand` | Converts all tabs to spaces. |
| `file` | Displays the type of data in a file. |
| `fold` | Wraps each line of text to fit a specified width. |
| `grep` | Searches for regular expressions in a text file. |
| `less` | Displays a text file one page at a time. (Go backward by pressing `b`.) |
| `lpr` | Prints files. |
| `more` | Displays a text file one page at a time. (Goes forward only). |
| `nl` | Numbers all nonblank lines in a text file and prints the lines to standard output. |
| `paste` | Concatenates corresponding lines from several files. |
| `patch` | Updates a text file by using the differences between the original and revised copies of the file. |
| `sed` | Copies a file to standard output while applying specified editing commands. |
| `sort` | Sorts lines in a text file. |
| `split` | Breaks up a file into several smaller files with specified sizes. |
| `tac` | Reverses a file (last line first and so on). |
| `tail` | Displays the last few lines of a file. |
| `tr` | Substitutes one group of characters for another throughout a file. |
| `uniq` | Eliminates duplicate lines from a text file. |
| 命令名称 | 操作 |
|---|---|
| `wc` | 计算文本文件中的行数、单词数和字符数。 |
| `zcat` | 显示压缩文件（解压后）。 |
| `zless` | 一次一页地显示压缩文件。（按 `b` 向后移动。） |
| `zmore` | 一次一页地显示压缩文件。 |
| 归档和压缩文件 |  |
| `compress` | 压缩文件。 |
| `cpio` | 将文件复制到归档文件和从归档文件复制。 |
| `gunzip` | 解压缩使用 GNU Zip (`gzip`) 压缩的文件。 |
| `gzip` | 使用 GNU Zip 压缩文件。 |
| `tar` | 创建一个或多个目录中的文件的归档（最初用于磁带归档）。 |
| `uncompress` | 解压缩使用 `compress` 压缩的文件。 |
| 管理文件 |  |
| `bg` | 在后台运行被中断的进程。 |
| `fg` | 在前台运行进程。 |
| `free` | 显示系统中空闲和已使用的内存量。 |
| `halt` | 关闭 Linux 并停止计算机。 |
| `kill` | 向进程发送信号（通常用于终止进程）。 |
| `ldd` | 显示运行程序所需的共享库。 |
| `nice` | 以较低优先级运行进程（称为 nice 模式）。 |
| `ps` | 显示正在运行的进程列表。 |
| `printenv` | 显示当前环境变量。 |
| `pstree` | 显示父子进程关系。 |
| `reboot` | 停止 Linux 然后重新启动计算机。 |
| `shutdown` | 关闭 Linux。 |
