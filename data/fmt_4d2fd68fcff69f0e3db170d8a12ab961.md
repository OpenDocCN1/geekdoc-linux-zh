
### 使用 `cat` 命令创建

`cat` 命令允许你创建短文本文件：

```
$ cat > newfile
```
执行此命令时不会显示任何内容。系统等待你输入。完成后按 Ctrl+d 保存输入到名为 `newfile` 的文件中。

### 使用 `vi`、`vim` 或 `nano` 命令创建

这些是 Linux 文本工具。最常用 `vi` 编辑器，但可以使用其中任何一个来创建和修改文本文件。参考第 4 章“编辑器和处理器”详细了解 `vi` 编辑器。第 4 章介绍了 `vim` 和 `nano`。

### 使用 `mkdir` 命令创建

`mkdir` 命令用于创建目录。以下示例显示如何在 `user1` 的家目录 (`/home/user1`) 下创建一个名为 `scripts` 的新目录：

```
$ cd
$ pwd
/home/user1
mkdir scripts
```

> 你必须具有创建目录的权限；否则会收到权限不足的错误。

你可以使用 `mkdir` 命令的 `-p` 选项创建子目录层次。在示例中，`mkdir` 创建了 `scripts2` 的子目录 `perl` 以及 `perl` 下的子目录 `perl5`。

```
$ mkdir -p scripts2/perl/perl5
```

## 列出文件和目录 (Listing Files and Directories)

要列出文件和目录，请使用 `ls` 或 `ll` 命令。以下示例以 `user1` 的身份在其家目录下运行 `ll`：

```
total 12
-rw-rw-r-- 1 user1 user1 0 Nov 26 file1
-rw-rw-r-- 1 user1 user1 6 Nov 26 newfile
drwxr-xr-x 2 user1 user1 4096 Nov 26 scripts1
drwxr-xr-x 2 user1 user1 4096 Nov 26 scripts2
```

注意输出中有九列，包含：

- 第 1 列：第一个字符告诉文件类型。接下来的 9 个字符表示权限。文件权限在第 3 章“文件和目录权限”中详细解释。
- 第 2 列：显示文件或目录有多少个链接。
- 第 3 列：显示文件或目录的所有者名称。
- 第 4 列：显示文件或目录所属的组名。
- 第 5 列：字节大小。对于目录，此数字反映了目录存储内容信息所使用的块数。
- 第 6、7 和8 列：列出文件或目录创建或最后访问/修改的月份、日期时间和。
- 第 9 列：文件或目录的名称。

## 显示文件内容 (Displaying File Contents)

Linux 提供了几个命令来显示文件内容。目录内容简单来说是其中的文件和子目录。如前所述，使用 `ll` 或 `ls` 命令查看目录内容。

`cat`, `more`, `less`, `head`, `tail`, `view`, `vi`, `vim`, `nano` 和 `strings` 命令可用于文件内容。下文解释了其中每一个命令。

### 使用 `cat` 命令

`cat` 命令显示文本文件的内容。在下面的示例中，使用 `cat` 命令显示 `user1` 家目录下的 `.bash_profile`：

```
$ cat /home/user1/.bash_profile
## .bash_profile
# Get the aliases and functions
if [ -f ~/.bashrc ]; then
  ~/.bashrc
fi
# User specific environment and startup programs
PATH=$PATH:$HOME/bin
export PATH
```

### 使用 `more` 命令

`more` 命令从头到尾一次一页显示长文本文件的内容。在下面的示例中，使用 `more` 命令显示了 `/etc/profile`。该命令会显示最后一行中已查看的文件的百分比。

```
$ more /etc/profile
#etc/profile
# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc
...
if [ "$SEUID" = "0" ]; then
--More-(45%)
```

当使用 `more` 查看查看大文件时，表 2-1 中列出的导航键将非常有帮助。

| 键 | 用途 |
| :--- | :--- |
| 空格键 / f | 滚动到下一页。 |
| 回车 | 一次滚动一行。 |
| b | 滚动到上一页。 |
| d / u | 向下/向上滚动半页。 |
| h | 显示帮助信息。 |
| q | 退出并返回 shell 提示符。 |
| /string | 向前搜索字符串。 |
| ?string | 向后搜索字符串。 |
| n / N | 查找字符串的下一个/上一个出现处。 |

### 表 2-1 使用 `more` 进行导航

### 使用 `less` 命令

`less` 命令与 `more` 命令相反。在下面的示例中，使用 `less` 命令显示了 `/etc/profile`：

```
$ less /etc/profile
#etc/profile
# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc
if [ "$SEUID" = "0" ]; then
/etc/profile
```

当使用 `less` 查看大文件时，表 2-1 中列出的导航键将非常有帮助。

### 使用 `head` 命令

`head` 命令显示文本文件的前几行。默认显示前 10 行。以下示例显示了 `/etc/profile` 文件的前 10 行：

```
$ head /etc/profile
## /etc/profile
# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc
pathmunge {
    if echo $PATH | /bin/egrep -q "(^|:)(\$1)(:)"; then
        if [ "$2" = "after" ]; then
PATH=$PATH:$1
    else
```

在命令后提供一个数字作为参数可以查看不同数的行。以下示例显示了 `/etc/profile` 文件的前三行：

```
$ head -3 /etc/profile
## /etc/profile
# System wide environment and startup programs, for login setup
```

### 使用 `tail` 命令

`tail` 命令显示文件的最后几行。默认显示最后 10 行。以下示例显示了 `/etc/profile` 文件的最后 10 行：

```
$ tail /etc/profile
export PATH USER LOGNAME MAIL HOSTNAME HITSIZE INPUTRUTC
for i in /etc/profile.d/*.sh; do
    if [ -r "$i" ]; then
        $i
    fi
done
unset i
unset pathmunge
```

你可以指定一个数值来查看不同的行。以下示例显示了 `/etc/profile` 的最后 8 行：

```
$ tail -8 /etc/profile
for i in /etc/profile.d/*.sh; do
    if [ -r "$i" ]; then
        $i
    fi
done
unset i
unset pathmunge
```

当你希望在日志文件更新时查看它，`tail` 命令证明非常有用。`-f` 选项启用此功能。以下示例显示了如何以这种方式查看 RHEL 系统日志文件 `/var/log/messages`。尝试在你的系统上运行此命令并观察其行为。

```
$ tail -f /var/log/messages
```

## 使用 `vi` 和 `vim` 命令

这些命令在 `vi` 编辑器中打开指定的字符串。以下是如何运行它们来打开 `.bashprofile`：

```
$ vi ~/.bashprofile
$ vim ~/.bashprofile
```

参见第 2-4 节获取关于 `vi` 和 `vim` 编辑器的详细信息。

## 使用 `nano` 命令

许多系统管理员和用户倾向于使用菜单式文本编辑器（如 `nano`）。以下是使用运行它来打开 `/etc/profile` 的方法：

```
$ nano /etc/profile
```
