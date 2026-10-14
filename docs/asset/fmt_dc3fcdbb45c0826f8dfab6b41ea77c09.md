
欢迎来到命令行世界——在这里，每次按键都能释放出无与伦比的控制。在本章中，我们将深入研究 Rocky Linux 中高效管理的核心命令行工具和技术。命令行不仅仅是一个工具，它是效率、自动化和精的门户——让新手和资深专业人士都能以极快的速度和手术般的精度与系统交互。

通过丰富的实践示例、实际用例和清晰的解释，我们将学习如何自信地导航终端、操作文件和目录、设置权限并精通地执行管理任务。但旅程并不仅于本地机器——我们还将探索云端 CLI 工作流，以便使用亚马逊云服务 (AWS) 等服务管理可扩展的基础设施。

无论我们是刚刚开始 Linux 之旅，还是在磨练 DevOps 技能，本章都提供了一个实操性的基础工具包，用于在本地服务器和云环境中高效工作。

## 结构

在本章中，我们将讨论以下主题：

- 基础终端命令
- 管理目录和文件
- 输出命令
- 文件权限与所有权
- `sudo` 命令
- 系统关机与重启
- AWS 云端 CLI 工作流导论

## 基础终端命令

终端，也称为命令行界面（CLI），不仅仅是一个工具——它是 Rocky Linux 9 系统管理的核心。与图形化用户界面（GUI）不同，终端提供了对系统的直接、低级访问，能够以无与伦比的效率实现快速配置、自动化和远程管理。

精通基础终端命令是任何 Linux 用户（尤其是系统管理员和开发者）最有价值的技能之一。这些基础命令使我们能够精确地在文件系统中导航、管理资源并执行关键任务。

在本节中，我们将探索一组每位管理员都应该掌握的核心 CLI 命令，并为每个提供清晰的解释和真实示例。无论我们是列出目录、在文件夹之间移动，还是为可重复的任务编写脚本，这些命令都构成了我们与 Rocky Linux 9 环境交互的主干。

### 理解终端环境

Rocky Linux 9 中的终端是一个基于文本的界面，允许用户与操作系统直接交互。它对系统进程提供精确的控制，对于系统配置、故障排除、脚本编写和远程管理等任务至关重要。

### 终端的关键组件

- 提示符 (Prompt)：这是我们输入命令的地方。它通常显示格式为：`user@hostname:~$`
- `Shell`：命令解释器（如 `Bash`），用于执行入的指令。`Shell` 处理我们的输入并管理输出、错误和环境。

**在 Rocky Linux 9 中打开终端：** 按 Ctrl + Alt + T，或者通过应用程序菜单访问。

**基础终端命令：** 这些基础命令对于导航和管理 Rocky Linux 9 系统至关重要。

- `pwd` - 打印工作目录：显示用户或管理员正在工作的目录的完整路径。

  ```bash
  pwd
  ```

  **示例输出：** `/home/username`

  使用此命令可以确认我们在复杂目录树中的当前位置。

- `ls` - 列出目录内容：列出当前（或指定）目录下的文件和文件夹。

  ```bash
  ls -l
  ```

  **实用标记：**

  - `-l`：长列表格式（显示权限、所有者、大小和日期）
  - `-a`：显示隐藏文件（以 `.` 开头的文件）

- `cd` - 切换目录：导航到文件系统中不同的目录。

  - `cd /etc` # 进入 `/etc` 目录
  - `cd ~` # 返回主目录
  - `cd ..` # 向上一个目录级

- `clear` - 清除终端屏幕：移除终端显示中之前的所有文本。

  ```bash
  clear
  ```

- `echo` - 显示消息或变量：在终端打印字符串。通常在脚本中用于消息或调试。

  `echo "Hello, Rocky Linux 9!"`

- `man` - 手册页：显示 Linux 命令的帮助文档。

  `man ls`

  按 **q** 退出帮助页。

使用 `man` 学习新命令，或为管理员已知的命令探索额外选项。

### `ls` - 列出目录内容

`ls` 命令允许我们显示目录的内容。

```bash
[cesarserver@RockyLinux ~$] ls
Desktop Documents Downloads Music Pictures Public Templates Videos
[cesarserver@RockyLinux ~$]
```

> **图 2.1：输出**

`ls` 命令是 Linux 中用于列出目录最常用的命令之一。在图 2.1 中，我们可以看到在特定目录下执行 `ls` 命令时生成的输出。此输出提供了该目录内包含的文件和子目录的概览。默认情况下，`ls` 以列的形式出文件名，但各种选项（如 `ls -a` 显示隐藏文件）可以修改显示。理解 `ls` 命令及其选项对于 Linux 系统中的文件导航和管理是基础性的。

列出当前位置的文件和目录。

选项：

- `ls -a`：包含隐藏文件（以 `.` 开头的文件）。
- `ls -l`：提供详细信息，包括权限、所有权和大小。
- `ls -h`：以人类可读的格式显示文件大小。

```bash
[cesarserver@RockyLinux ~$] ls -lah
total 44K
drwxr-xr-x 2 cesarserver cesarserver 4096 Oct 24 10:00 ..
drwxr-xr-x 2 cesarserver cesarserver 4096 Oct 24 10:00 .
-rw-r--r-- 1 cesarserver cesarserver 38 Oct 24 10:00 .bash
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Desktop
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Documents
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Downloads
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Music
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Pictures
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Public
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Templates
drwxr-xr-x 4 cesarserver cesarserver 4096 Oct 24 10:00 Videos
```

`ls` 命令是 Linux 中列出目录内容最常用的命令之一。在图 2.1 中，我们可以看到在特定目录下执行 `ls` 命令时生成的输出。此输出提供了该目录内包含的文件和子目录的概览。默认情况下，`ls` 以列的形式出文件名，但各种选项（如 `ls -a` 显示隐藏文件）可以修改显示。理解 `ls` 命令及其选项对于 Linux 系统中的文件导航和管理是基础性的。

*（注：原文后续部分存在大量重复内容，已根据要求“不要重复输出原文”进行处理）*

### 复制文件和目录

`cp -r dir1/ dir2/`

**有用选项：**

- `-r`：递归，复制所有子目录及其内容。
- `-v`：详细，显示正在复制的内容。

在运行 `cp -rv dir1/ dir2/` 后：

在命令行界面中，将显示类似以下的内容：

- `file1.txt` -> `dir2/dir1/file1.txt`
- `file2.txt` -> `dir2/dir1/file2.txt`
- `dir1/subdir` -> `dir2/dir1/subdir`
- `dir1/subdir/file3.txt` -> `dir2/dir1/subdir/file3.txt`

### 移动或重命名文件和目录

- `mv`：移动或重命名文件和目录

```bash
重命名文件：mv oldname.txt newname.txt
将文件移动到另一个目录：mv file.txt /home/user/Documents/
```

### 删除文件和目录

- `rm`：删除文件或目录

删除文件：`rm unwanted.txt`

删除目录及其内容：`rm -r old_folder/`

**有用选项：**

- `-r`：递归，删除目录及其内容。
- `-f`：强制，跳过确认提示。

请谨慎使用此命令：`rm -rf /`

此命令将删除系统上的所有内容，绝对不要运行。

### 检查文件和元数据

- `stat`：查看文件信息

显示元数据，如文件大小、访问和修改时间以及权限。

`stat example.txt`

### 识别文件类型

- `file`：确定文件类型

用于确认文件是否为脚本、文本文件、二进制文件、图像等。

`file script.sh`

通过这些工具，管理员现在能够任在任何 Rocky Linux 9 环境中高效地处理文件和目录管理。接下来，我们将探索文件权限和所有权——这是保护系统的关键。
