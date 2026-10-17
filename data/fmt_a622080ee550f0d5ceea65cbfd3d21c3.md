
## 步步通 Linux：三合一

这些命令可以帮助你操作 Linux 命令行并简化各种任务的执行。但是 `man` 命令和 `help` 命令之间有什么区别呢？

`man` 命令（源自“manual”，手册）用于获取 Linux 中特定命令或程序的帮助。它会显示命令的完整描述，包括可用选项、参数、用法示例和其他有用信息。

相反，`help` 命令是一个内置 shell 命令，用于获取有关内置 shell 命令或内置编程语言函数（例如 `Bash`）的简要信息。该命令提供的详细程度不如 `man` 命令，且不适用于外部命令。

因此，`man` 和 `help` 的区别在于：`man` 提供关于外部命令的详细帮助，而 `help` 用于获取有关内置 shell 命令的简要信息。

使用 `man` 命令获取帮助的语法如下：

```
man [options] command_name
```

其中 `options` 是 `man` 命令的额外参数，可以影响帮助信息的输出，`command_name` 是你需要获取帮助的命令名称。

使用 `help` 命令获取帮助的语法取决于你正在使用的 shell。在标准的 `Bash` shell 中，语法如下：

```
help [command_name]
```

其中 `command_name` 是你需要获取帮助的命令名称。如果未指定 `command_name`，则将显示该 shell 中所有可用命令的列表。

如果你在不同的 shell 中工作，语法可能会有所不同，但通常 `help` 命令用于获取内置 shell 命令的帮助。

## 第 III 章 在 Linux 命令行中操作的命令

### 英文 III.2.3 管理 Linux 中文件和文件夹的命令

Linux 的“管理文件和文件夹”部分包含了允许你在命令行处理文件和目录的函数和命令。一些最重要的函数见表 3.6。

表 3.6 - Linux“管理文件和文件夹”部分中的命令

| 命令 | 说明 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `cd` | 切换目录 | | `cd directory`, `cd ..`, `cd /` |
| `ls` | 显示目录内容 | `-a`: 显示隐藏文件，`-l`: 显示文件的额外信息（以列表形式） | `ls`, `ls -a`, `ls -l`, `ls -al` |
| `dir` | 列出目录内容 | `-a` (显示隐藏文件) | `dir`, `dir -a`, `dir /home/docs` |
| | `dir` 是 Windows 操作系统中使用的命令。`dir` 命令也可以在 Linux 上使用，但它不是标准命令，不建议用来替代 `ls` 命令。当用户在 Linux 上输入 `dir` 命令时，通常会导致带特定参数执行 `ls` 命令。 | | |
| `mkdir` | 创建目录 | `-p`: 创建目录及所有中间目录 | `mkdir directory`, `mkdir -p directory/sub` |
| `rmdir` | 删除空目录 | | `rmdir directory` |
| `rm` | 删除文件和目录 | `-r`: 递归删除目录及其内容，`-f`: 不经确认删除 | `rm file`, `rm -r directory`, `rm -rf directory` |

## 步步通 Linux：三合一

| 命令 | 说明 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `mv` | 移动或重命名文件和文件夹 | `-i`: 覆盖前确认，`-v`: 显示移动过程的详细信息 | `mv file.txt folder/`, `mv file.txt newname.txt` |
| `touch` | 创建空文件或更新修改时间 | `-a`: 仅更新访问时间, `-m`: 仅更新修改时间 | `touch file.txt`, `touch -a file.txt`, `touch -m file.txt` |
| `file` | 文件类型 | | `file file.txt` |
| `ln` | 为文件创建硬链接或符号链接 | `-s`: 创建符号链接，`-i`: 覆盖前确认 | `ln file.txt link.txt`, `ln -s file.txt link.txt` |
| `cp` | 复制文件和文件夹 | `-r`: 递归复制, `-i`: 覆盖前确认，`-v`: 显示复制过程的详细信息 | `cp file.txt folder/`, `cp file.txt newfile.txt` |
| `find` | 通过各种标准搜索文件和文件夹 | `-name`: 按文件名搜索，`-type`: 按类型搜索, `-exec`: 对找到的文件执行命令 | `find /home/user/ -name "*.txt"`, `find /home/user/ -type f -exec chmod 644 {} ;` |
| `locate` | 在数据库中快速搜索文件 | | `locate file.txt` |

## 第 III 章 在 Linux 命令行中操作的命令

| 命令 | 说明 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `du` | 确定文件或文件夹的大小（字节） | `-h`: 以易读格式显示大小 | `du file.txt`, `du -h folder/` |
| `df` | 确定可用磁盘空间 | `-h`: 以易读格式显示 | `df -h` |
| `tar` | 创建或提取 `tar` 归档包 | `-c`: 创建归档包, `-x`: 提取归档包, `-v`: 显示过程 | `tar -cvf archive.tar file.txt...`, `tar -xf archive.tar` |
| `gzip`/`gunzip` | 压缩和解压 `gzip` 文件 | | `gzip file.txt`, `gunzip file.txt` |
| `zip` | 在 Linux 操作系统中创建 ZIP 格式归档包 | `-r` 递归归档文件夹及其内容 | `zip [options] archive.zip -r directory/` |
| `unzip` | 在 Linux 操作系统中解压 ZIP 格式的归档包 | `-d` (目录) 允许指定解压目录 | `unzip [options] archive.zip`, `unzip archive.zip -d /path/to/` |

例如，要从当前目录的所有文件和文件夹创建一个名为“my_archive.zip”的归档包，请使用命令：`zip my_archive.zip *`

使用 `zip` 命令的示例：

1. 为多个文件创建归档包：`zip my_archive.zip file1.txt file2.txt file3.txt`
2. 为整个目录创建归档包：`zip -r my_archive.zip directory/`
3. 在当前目录解压归档包：`unzip my_archive.zip`
4. 将归档包解压到指定的目录：`unzip my_archive.zip -d /path/to/`
5. 从归档包中解压特定文件：`unzip my_archive.zip file.txt`

# 第三章。LINUX 命令行操作命令

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `chown` | 更改文件/目录的所有者或组 | - | `chown user:group file.txt` |
| `chgrp` | 更改文件/目录的组 | - | - |
| `dd` | 复制/转换数据块 | `if` (输入文件), `of` (输出文件), `bs` (块大小) | `dd if=/dev/zero of=file.txt bs=1M count=10` |
| `df` | 显示空闲磁盘空间信息 | `-h` (以人类可读的格式显示) | `df`, `df -h` |
| `du` | 显示已用磁盘空间信息 | `-h` (以人类可读的格式显示) | `du`, `du -h` |
| `mount` | 挂载文件系统 | - | `mount /dev/sdb1 /mnt/usb` |
| `umount` | 卸载文件系统 | - | `umount /mnt/usb` |

# 挂载（mount）是什么意思？

在操作系统中，挂载意味着将文件挂载到目录树中的特定挂载点。当文件系统被挂载时，它就可以在该挂载点上使用，用户可以像处理其他文件一样在该文件系统上读写文件。挂载可以在系统启动时自动发生，也可以根据用户请求手动进行。

需要注意的是，在“或”（`or`）操作符的条件下，不仅可以使用命令，还可以使用任何可以评估为真或假的其他表达式。

# 逐步进阶 Linux：三合一

# 英文版 III.2.4 Linux 中管理网络和文件系统的命令

要从命令行在 Linux 中管理网络，你需要了解某些命令。这些命令将允许你更深入地配置和管理网络。一些最重要的命令在表 3.7 中。

表 3.7 – Linux 网络管理命令

| 命令 | 描述 | 重要参数 | 示例 |
| --- | --- | --- | --- |
| `ping` | 检查与另一个主机的连接 | | `ping yandex.ru` |
| `ifconfig` | 显示网卡接口信息 | | `ifconfig` |
| `ip` | 为接口分配 IP 地址、路由、管理、隧道管理 | `addr`, `route`, `link` | `ip addr show` |
