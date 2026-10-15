
```
rocket 46% cat /etc/passwd | grep ":10:"; cat /etc/passwd | grep "/hosts/planet"
gary:uIOeAFzcI:2111:220:Gary Daniels:/hosts/planet/usr/people/gary:/bin/csh
saturn:EBrqshw206Eu:1112:107:Saturn Watson:/hosts/planet/usr/people/saturn:/bin/csh
krier:qOrsddX1qeKm:1113:140:Kevin Riser:/user/krier:/bin/csh
```

执行一次 `grep` 获取组 10，然后是密码文件的另一部分，并从远程家目录进行 `grep`。你可以使用 `grep` 将这两个命令合并为一个命令。

```
rocket 47% egrep ':10\|/hosts/planet' /etc/passwd
gary:uIOeAFzcI:2111:220:Gary Daniels:/hosts/planet/usr/people/gary:/bin/csh
saturn:EBrqshw206Eu:1112:107:Saturn Watson:/hosts/planet/usr/people/saturn:/bin/csh
krier:qOrsddX1qeKm:1114:140:Kevin Riser:/user/krier:/bin/csh
```

`grep` 搜索括号内所有位置的模式，并用竖线 (`|`) 分隔每个模式列表。输出返回密码文件中所有属于组 10 或包含 `/hosts/planet` 的行。所有其他行将被丢弃。

可以执行命令并将其输出管道到 `grep` 以搜索特定模式。要显示系统中所有的 NFS 文件系统，你可以在命令中 `grep` NFS 硬挂载文件系统以及特定系统的名称。

| 文件系统类型 | kbytes | 使用 | 可用 | %使用 | 挂载在 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev /dev/dks023s7 | 20519316 | 1752436 | 299500 | 86 | / |
| saturn:/nfs | 16279916 | 1571004 | 56992 | 77 | /saturn2 |
| saturn:/patches | 8360424 | 5099859 | 3170565 | 62 | /tmp_mnt/hosts/saturn |
| pluto:/var | 966304 | 928110 | 38194 | 98 | /tmp_mnt/hosts/pluto/var |
| pluto:/disk2 | 2042828 | 1995226 | 50022 | 98 | /tmp_mnt/hosts/pluto/disk2 |

```
rocket 49% df -k | grep 'xfs saturn'
/dev /dev/dks023s7 20519316 1752436 299500 86 /
saturn:/nfs 16279916 1571004 56992 77 /saturn2
saturn:/patches 8360424 5099960 3260464 62 /tmp_mnt/hosts/saturn
```

# 第 6 章：文件管理：6.6 多重 grep

当执行 `df` 命令时，它会显示挂载的文件系统。当 `df` 将输出管道到 `grep` 时，它会显示所有包含 `xfs` 和 `saturn` 的行。使用单个 `grep` 命令为管理员提供了提取原本需要多个命令完成的所有数据的工具。

## 其他资源

帮助页：`cat`, `df`, `egrep`, `grep`

| UNIX 提示与技巧 | 索引 |
| :--- | :--- |
| 第 6 章：文件管理 | 上一章 / 下一章 |
| 本章章节： | |
| 6.1 使用时间戳复制文件 | 6.5 使用 grep 搜索文件 | 6.8 重命名文件组 | 11 分割文件 |
| 6.2 远程 grep | 6.7 使用 find 递归执行命令 | 6.9 帮助页 | 12 核心大小 |
| 6.3 grep 是工具吗？ | 6.6 多重 grep | 10 清理文件 | 13 编码解码 |
| 6.4 处理符号链接 | 上一节 / 下一节 |

# UNIX 提示与技巧 6.7 使用 find 递归执行命令

## 第 6 章：文件管理

本章章节：

- 6.1 使用时间戳复制文件
- 6.2 远程 grep
- 6.3 grep 是工具吗？
- 6.4 处理符号链接
- 6.5 使用 grep 搜索文件
- 6.6 多重 grep
- 6.7 使用 find 递归执行命令
- 6.1 分割文件
- 6.8 重命名文件组
- 6.9 帮助页
- 10 清理文件
- 12 核心大小
- 13 编码解码

### 6.7.1

`find` 命令遍历系统并显示所有文件，但 `find` 同时也通过 `grep` 在文件和子目录中执行搜索。

## 示例一：递归搜索

变体：AT&T, BSD

语法：

```
find [dir] -type f -print | xargs grep -il [pattern]
find [dir] -type f -exec grep -il [pattern] \;
```

有几种方法可以递归搜索子目录下的文件。当你寻找代码、记录或无法定位的信息时，这种方法非常有益。使用 `find` 结合 `grep` 可以遍历系统并搜索 `hostname` 的每一个出现。在这种情况下，如果将文件传递给 `xargs`，则会对文件运行 `grep`。如果文件中存在 `planet`，则会显示其路径。为了进一步缩短这个递归命令，可以将其添加到个人别列表中：

```
rocket 50% find / -type f -print | xargs grep -il planet
/etc/ethers
/etc/hosts
/etc/hostname
/usr/local/bin/sysinfo
/var/adm/messages
```

`find` 将遇到的任何文件管道到 `xargs`。`xargs` 命令接收参数并执行它。在这种情况下，作为文件传递给 `xargs`，会对文件运行 `grep`。为了进一步缩短这个递归命令，可以将其添加到个人别列表中：

```
alias grep='find . -type f -print | xargs grep -i $1'
```

## 文件管理：6.7 使用 find 递归执行命令

```
rocket 51% rgrep planet
/etc/ethers
/etc/hosts
/etc/hostname
/usr/local/bin/sysinfo
/var/admin/messages
```

通过输入 `grep` 和搜索模式，将在你执行命令的当前目录的所有文件和子目录中搜索该模式。

```
rocket 51% find / -type f -exec grep -il planet {}
/etc/ethers
/etc/hosts
/etc/hostname
/usr/local/bin/sysinfo
/var/admin/messages
```

为了显示执行相同任务的方法，此命令还会处理树或搜索区域。在这个版本，当找到每个文件时，会对文件执行对 *planet* 单词的 `grep`。如果找到了该单词，将显示文件名和路径。

可以为这种递归 `grep` 设置别名。这也允许管理员更快地输入命令并更快地获取结果。

```
alias grep='find -type f -exec grep -il {}'
```

## 示例二：删除旧文件

变体：AT&T, BSD

语法：

```
find [dir] -type f -atime +n -exec rm {} \;
```

为了清理文件，可以使用此命令清理旧且不必要的文件。当 `find` 到达一个 `n` 天未被访问的文件时，该文件将被删除。如果磁盘空间紧张且必须找到要清理的目录，你通常首先针对这些区域。用户仍然可能在该区域工作时放置文件。先删除旧文件更好。如果用户在 `n` 天内没有接触过某个文件，则被认为是可以删除的。

```
# find /disk/2tmp -type f -atime +10 -exec rm {} \;
```

此命令遍历 `disk/2tmp` 上的临时区域，并查找 10 天未被访问的文件。如果发现了它们，就会删除它们。如果发现了它们，显示器不会有任何输出。你应该注意到可用磁盘空间的增加。如果仍有大量文件填充空间，你可能需要缩回到七天删除一次。

你可能想通过发送定期通知来告知用户每七天删除一次文件。你可以在 `crontab` 中设置此，每七天删除一次临时区域的所有文件。
