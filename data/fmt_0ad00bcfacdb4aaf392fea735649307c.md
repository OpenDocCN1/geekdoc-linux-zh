
**图 9-4**：`history` 命令的输出。

## 恢复命令和参数
按下向上箭头允许你调回在终端上运行过的命令。先按 `Esc` 再按点 (`.`) 是调回参数的另一种方法。

## 如何执行基础 `Bash Shell` 操作

过程参考：使用通配符进行搜索

若要使用通配符进行搜索：

1. 以用户身份登录 `CLI`。
2. 执行基准操作。
    - 要列出所有匹配给定模式的内容，输入 `ls [wildcard] {wildcard}`
    - 要删除匹配给定模式的内容，输入 `rm [wildcard] {wildcard}`
    - 要打印所有匹配给定模式的内容，输入 `echo [wildcard] {wildcard}`

过程参考：使用通配符定位文件

若要使用通配符搜索文件：

1. 以 `root` 身份登录 `CLI` 并导航到相关目录。

## 使用通配符定位所需的文件。

过程参考：移动符合通配符模式的文件

若要移动符合通配符模式的文件：

1. 登录并导航到相关目录。
2. 要将符合搜索模式的文件移动到目标目录，输入 `mv *[search string] /(target directory)`。
3. 如有必要，要实文件是否已移动到目标目录，输入 `ls /(target directory)`。

过程参考：使用 `Tab` 键补全检测文件名

若要使用 `Tab` 键补全检测文件名：

1. 以用户身份登录 `CLI`。
2. 要补全命令名，输入命令名中的唯一字符并按下 `Tab` 键。
3. 要补全文件名，输入文件名中的唯一字符并按下 `Tab` 键。

过程参考：使用 `history` 命令查看最近使用的命令

若要使用 `history` 命令查看最近使用的命令：

1. 以用户身份登录 `CLI`。
2. 查看执行过的命令历史记录。
    - 要列出所有之前使用过的命令，输入 `history`。
    - 要从历史记录中执行特定命令，输入 `!{history number}`。
    - 要重复执行执行的命令，输入 `!!`。

过程参考：执行基础命令行扩展

若要执行基础命令行扩展：

1. 以用户身份登录 `CLI`。
2. 执行基础命令行扩展。
    - 当文件名或目录名包含公共字符串时，输入 `(command) {common string}{unique part of file 1, unique part of file 2}`。
    - 要打印字符串，输入 `(command) '{string}'`。
    - 要将一个命令的输出作为另一个命令的输入，输入 `{command 2} '{command 1}'`。

## 活动 9-1
使用通配符搜索文件

数据文件：
`Audit_File_2000.txt`, `Audit_File_2001.txt`, `Audit_File_2002.txt`, `Audit_File_2003.txt`, `Audit_File_2004.txt`, `Audit_File_2005.txt`, `Audit_File_2006.txt`, `Audit_File_2007.txt`, `Audit_File_2008.txt`, `Audit_File_2009.txt`, `Audit_File_2010.txt`。

开始之前：

1. 你已以 `root` 身份登录 `GUI`。
2. 终端窗口已显示。
3. 在终端窗口中，输入 `cp /085099Data/Working_with_Bash_and_shell_scripts/* /root.`。
4. 要覆盖 `Software_List.txt` 文件，输入 `y`。
5. 要覆盖 `Software_Rules.txt` 文件，输入 `y`。
6. 要切换到 `root` 目录，输入 `cd`。
7. 终端窗口已显示。
8. 切换到 `CLI`。
9. 登录。

场景：
你的组织采用了一种新的策略，要求你整理文件。你被要求创建目录结构并移动文件，以确保结构符合组织标准。需要组织的文件位于 `/root` 目录。

1. 创建一个以 `Audit_Reports` 为父目录的目录结构，包含四个子目录：`2007`、`2008`、`2009` 和 `2010`。
    a. 要创建 `Audit_Reports` 目录，输入 `mkdir Audit_Reports`
    b. 要切换到新创建的目录，输入 `cd Audit_Reports`
    c. 要创建多个目录，输入 `mkdir 2007 2008 2009 2010`
    d. 要列出目录，输入 `ls`
    e. 观察新创建的目录已列出。

2. 将与 `2007`、`2008`、`2009` 和 `2010` 年相关的文件移动到各自的目录中。

要将以“`2009`”结尾的文件移动到 `Audit_Reports/2009` 目录，输入 `mv *2009.txt Audit_Reports/2009`。

要验证文件已移动，输入 `ls Audit_Reports/2009`。

要将以“`2010`”结尾的文件移动到 `Audit_Reports/2010` 目录，输入 `mv *2010.txt Audit_Reports/2010`。

要验证文件已移动，输入 `ls Audit_Reports/2010`。

观察文件已列出，表明它们已经移动。清除终端屏幕。

## 3. 在不同位置为 `Audit_Reports` 目录创建备份。

- a. 要递归复制 `Audit_Reports` 目录中的所有文件到 `/Reports_Backup` 目录，输入 `cp -R Audit_Reports /Reports_Backup`
- b. 要验证备份目录已创建，输入 `ls /`
- c. 观察到备份已创建。

## 4. 将 `Reports_Backup` 目录重命名为 `Audit_Backup`。

- a. 要切换到父目录，输入 `cd ..`
- b. 要将 `Reports_Backup` 目录重命名为 `Audit_Backup`，输入 `mv Reports_Backup Audit_Backup`
- c. 要验证目录已重命名，输入 `ls`
- d. 观察到备份目录已重命名。
- e. 清除终端屏幕。

# 主题 B

## 编写 `Bash Shell` 脚本

在上一个主题中，你使用了基本的 `Bash Shell` 选项来执行各种任务。为了使用操作系统执行复杂任务，为相应的任务编写程序是至关重要的。在本主题中，你将编写一个基础 `Bash Shell` 脚本。

深入理解 `shell` 脚本对于理解 `Linux` 系统的运行所需的。作为 `Linux` 管理员，处理 `shell` 脚本对你至关重要，因为它们允许你自动化常规任务，节省时间和精力。

## Shell 脚本

`Shell` 脚本是一个包含命令列表的文件，由 `shell` 读取并执行。经常使用的命令可以存储在 `shell` 脚本中重复使用。每个 `shell` 脚本都以一行开头，该行指定操作系统执行该脚本的解释器。

```bash
root@localhost~

#!/bin/bash

echo "Good Morning $USER. Please fill in your timecard." 
```
