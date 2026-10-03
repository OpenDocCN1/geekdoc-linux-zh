
- 9. 显示文件 `a.out` 的权限。

```
$ ls -l a.out
-rw-rw-rw- 1 users 23951 Jan 08 13:02 a.out
```

*(注：原文示例第9步输出为 `-rw-rw-rw` 疑似漏了一位，此处按逻辑翻译并保持与原文一致)*

以及写入权限，而组和其他用户只有读取权限。验证权限已按照你的要求设置。

## 解决方案

```
$ chmod 755 groupfile
$ ls -l groupfile
-rxr-xr-x 1 you users 268 Jan 09 08:43 groupfile
$ chmod 111 groupfile
$ ls -l groupfile
---x----x 1 you users 268 Jan 09 08:43 groupfile
$ chmod 644 groupfile
$ ls -l groupfile
-rw-r--r-- 1 you users 268 Jan 09 08:43 groupfile
```

# 移动和重命名文件

## 概述

`mv` 命令将文件从一个文件名重命名另一个，或者将文件从一个目录移动到另一个目录。

`mv` 命令的格式为：

```
mv file file2 or mv file ... directory
```

## 使用 mv 命令

当使用 `mv` 命令移动或重命名文件时，如果新文件位于同一个文件系统中，磁盘上的文件本身不会被移动或复制。相反，指向文件的指针会被更改。

当 `mv` 命令将文件从一个文件系统移动到另一个文件系统时，它会将文件复制到新的文件系统并从原始工作目录中删除。

- 将文件 `mail.lst` 移动到当前工作目录下的子目录 `personal`

  - `$ mv mail.lst personal`

- 同时将文件 `res` 和 `skills` 移动到工作目录下的子目录 `personal`

  - `$ mv res skills personal`

- 将当前工作目录下的文件 `mail.lst` 重命名为 `mail`

  - `$ mv mail.lst mail`

- 将文件 `res` 移动到工作目录下的子目录 `intro` 并将其重命名为 `resume`

  - `$ mv res intro/resume`

- 将 `personal` 目录中的所有文件移动到 `intro` 目录，并保持文件名。此命令将清空 `personal` 目录。

  - `$ mv personal/* intro`

## 安全移动文件

当你将文件移动到一个已存在的文件时，原始文件将被覆盖。如果你已经有一个名为 `chores` 的文件并输入以下命令：

```
$ mv todo chores
```

`chores` 文件的原始内容将会丢失。

在 `mv` 命令中使用 `-i` 选项，会在文件可能被覆盖时提示你确认。输入 `y` 继续复制或输入 `n` 取消复制。

```
$ mv -i todo chores
overwrite chores? y
```

## 试一下！

- 1. 在你的主目录中，将主目录下的文件列表存入名为 `listing` 的文件中。（提示：使用 `>` 符号重定向 `ls` 命令的输出。）

- 2. 将文件 `listing` 重命名为 `dir.list`。

- 3. 在主目录中创建一个名为 `temp` 的子目录。仅使用一条命令，将 `dir.list` 重命名为 `listing` 并将其移动到 `temp`。

- 4. 将工作目录更改到 `temp` 并列出该目录的文件。你应该看到一个名为 `listing` 的文件。然后返回你的主目录。

## 解决方案

```
$ ls > listing
$ mv listing dir.list
$ mkdir temp
$ mv dir.list temp/listing
$ cd temp
$ ls
listing
$ cd
```

# 复制文件

## 概述

有时你可能想创建一个文件的副本，而不是重命名它。在对文件进行任何重大修改之前，始终为文件创建一个备份副本。

`cp`（复制）命令执行此功能。当你使用 `cp` 命令复制文件时，系统会创建一个具有新名称的文件副本，并保持原始文件完整。`cp` 命令的格式为：

```
cp filename new-filename
```

## 使用 cp 命令

- 在在工作目录中创建一个名为 `memo` 的 `mail` 文件的副本：

  `$ cp mail memo`

- 在 `pers` 目录中创建一个名为 `skills` 的 `resume` 文件的副本：

  `$ cp resume pers/skills`

工作目录中的原始文件保持不变。

## 安全复制文件

如果你将文件复制到已存在的文件中，旧文件将被覆盖并丢失。`-i` 选项会在覆盖文件之前要求你进行确认。只有当你的回答为 `y` 或 `yes` 时，文件才会被覆盖。

```
$ cp -i mail memo
overwrite memo? y
$
```

## 复制子目录

使用 `-R` 选项将整个目录（包括子目录）复制到指定的路径。

以下示例将目录 `/usr/users/jonah/whales` 复制到 `/usr/users/noah/animals`。整个 `whales` 目录（包括所有文件）将成为 `/usr/users/noah/animals` 的子目录。

```
$ cp -R /usr/users/jonah/whales /usr/users/noah/animals
```

### 现在试一下！

- 1. 将工作目录更改为你的主目录。

- 2. 将文件 `/etc/passwd` 复制到你的工作目录并命名为 `pass1`。

- 3. 使用 `mkdir` 命令在你的主目录下创建一个名为 `practice` 的目录。

- 4. 在不更改工作目录的情况下，将文件 `pass1` 复制到 `practice` 目录。

- 5. 将工作目录更改为 `/usr/users/you/practice` 并列出该目录的文件。你应该看到 `pass1` 文件。

- 6. 再次将文件 `/etc/passwd` 复制到你的工作目录并命名为 `passl`。这次使用 `-i` 选项确认你是否想要继续复制该文件。在提示覆盖现有文件时输入 `y`。

## 解决方案

```
$ cd
$ cp /etc/passwd passl
$ mkdir practice
$ cp passl practice
$ cd practice
$ ls
passl
$ cp -i /etc/passwd passl
overwrite passl? y
```

# 删除文件和目录

## 概述

当你不再需要某些文件或目录时，可以使用 `rm` 和 `rmdir` 命令删除它们。

## 使用 rm 命令

`rm`（删除）命令可以删除单个文件或多个文件。

`rm` 命令的格式为：

```
rm filename...
```

- 从工作目录删除名为 `book` 的文件：

  `$ rm book`

- 从工作目录删除名为 `book` 和 `intro` 的两个文件：

  `$ rm book intro`

以下示例显示了列出工作目录中的文件并删除 `dead.letter`、`a.out`、`mail.help` 和 `core` 的命令。

**示例 6-7: 使用 rm 删除文件**

```
$ ls
calendar dead.letter intro mbox
$ rm dead.letter a.out mail.help core
$ ls
calendar intro
```

## 安全删除文件

`-i` 选项会在删除指定的文件之前要求确认。只有当你的回答为 `y` 或 `yes`时，文件才会被删除。

```
$ rm -i dead.letter a.out mail.help core
rm: remove dead.letter? y
rm: remove a.out? y
rm: remove mail.help? y
rm: remove core? y
```

## 注意

非常小心。一旦文件被删除，无法恢复。养成在使用 `rm` 命令时使用 `-i` 选项的习惯。

## 使用 rm -r 删除文件和目录

`rm` 命令的 `-r` 选项允许你同时删除文件和目录。

使用 `rm -r` 命令的格式为：

```
rm -r pathname
```

指定的路径是你想删除的目录名称。如果你想删除 `/usr/users/you/test` 目录中的文件以及 `test` 目录本身，请输入：

```
$ rm -r /usr/users/you/test
```

你可以将 `-r` 选项与 `-i` 选项结合，如下例所示。

### 示例 6-8: 删除文件和目录

```
$ rm -ri /usr/users/you/practice
rm: remove files in directory /usr/users/you/practice? y
rm: remove /usr/users/you/practice/pass? y
rm: remove /usr/users/you/practice/ls.out? y
rm: remove /usr/users/you/practice/report.old? y
rm: remove /usr/users/you/practice? y
$
```

## 使用 rmdir 命令

你可以使用 `rmdir` 命令删除系统中不再需要的空目录。如果目录为空，它会警告你。

`rmdir` 命令的格式为：

```
rmdir directory-name...
```

此示例在 `personal` 目录为空时，从当前工作目录删除名为 `personal` 的目录。

```
$ rmdir personal
```

此示例当 `proj1`、`proj2` 和 `proj3` 目录为空时，从工作目录删除这三个目录。

```
$ rmdir proj1 proj2 proj3
```

### 现在试一下！

- 1. 在你的主目录下创建两个名为 `practicel` 和 `practice2` 的目录。

- 2. 将你的工作目录更改到 `practicel`。

- 3. 使用 `cat` 命令创建一个名为 `friends` 的文件，其中包含一些朋友的名字。

- 4. 创建 `friends` 文件的三个副本，分别命名为 `friends1`、`friends2` 和 `friends3`。

- 5. 删除名为 `friends2` 文件。

- 6. 使用带有 `-i` 选项的 `rm` 命令删除名为 `friends3` 文件。在提示时输入 `y`。然后返回主目录。

- 7. 现在使用带有 `-r` 和 `-i` 选项的 `rm` 命令删除 `practicel` 及其内部的文件。

## 解决方案

```
$ mkdir practicel practice2
$ cd practicel
$ cat > friends
Clark
Marion
Linda
<Ctrl/D>
$ cp friends friends1
$ cp friends friends2
$ cp friends friends3
$ rm friends2
$ rm -i friends3
rm: remove friends3? y
$ cd
$ rm -ri practicel
rm: remove practicel/friends? y
rm: remove practicel/friends1? y
rm: remove practicel? y
```

# 链接文件

## 概述

链接提供了一种共享文件的机制。

- 链接允许多个用户访问相同的数据。
- 链接是一个引用文件的目录条目。
- 一个文件可以有多个链接。

## 关于 Inode

*inode* 是一种文件系统数据结构，包含有关文件的信息，例如：

- 文件的类型和访问模式
- 文件的所有者
- 组访问标识符
- 指向文件的链接数
- 文件的大小（字节为字节）
- 文件使用的物理块数
- 文件创建、访问或修改的时间
- 指向磁盘数据块的指针

你可以使用 `ls -i` 命令显示 inode 节点。

## 使用 ln 命令

两种类型的链接——硬链接和符号链接（软链接）都是使用 `ln` 命令生成的。默认情况下，`ln` 创建硬链接。

`ln` 命令的格式为：

```
ln [-fns] source_file target_file
```

*source_file* 是已存在的文件。*target_file* 是链接文件名。常用的链接选项有：

- `-f`：在链接前强制删除已存在的目标路径。
- `-n`：如果目标文件已存在，则不覆盖其内容；`-f` 会覆盖此选项。
- `-s`：创建一个符号链接。

## 关于硬链接

建立硬链接后，它与原始文件无法区分。如果原始文件被删除，链接文件仍然存在，并包含相同的数据。

硬链接：

- 不能引用目录。
- 不能跨文件系统（必须与原始文件在同一个文件系统中）。
- 节省磁盘空间，因为只存在一份数据。
- 共享 inode。

## 生成硬链接

以下示例展示了如何为 Smif 的贷款程序创建一个硬链接。同时也显示了源文件和目标文件的 `ls -il` 命令结果。

### 示例 6-9：创建硬链接

```
$ pw
$ /usr/users/you
$ ln /usr/users/smif/mortgage mortgage-hlink
$
$ ls -il mortgage-hlink
17028 -rwxr-xr-x 2 smif users 39772 Apr 06 10:40 mortgage-hlink
$
$ ls -il /usr/users/smif/mortgage
17028 -rwxr-xr-x 2 smif users 39772 Apr 06 10:40 mortgage
```

## 硬链接与文件的关系

下图显示了硬链接与其引用的文件之间的关系。

### 图 6-5：硬链接

![](img/8295751dfa37c5d3eb4d16a30f79fb_199_0.png)

## 尝试一下

1. 将 `/etc/passwd` 到主目录下名为 `dummy` 的文件中。

2. 使用 `ls -il dummy` 命令获取你创建的 `dummy` 文件的目录列表。在此处记录结果。

3. 为 `dummy` 文件创建一个名为 `hard_link` 的硬链接。

4. 使用 `ls -il` 获取原始文件和链接文件的目录列表。在此处记录结果。

5. 原始文件的列表有变化吗？如果有，变化是什么？比较链接文件和原始文件的目录列表。哪些目录条目是相同的？为什么？

6. 删除 `dummy` 文件。

7. 使用 `cat hard_link` 或 `more hard_link` 显示文件。在删除原始文件后还能显示该文件吗？为什么？

8. 删除链接文件 `hard_link`。

9. 尝试为 `/etc/passwd` 创建名为 `hard_link` 的硬链接。发生了什么？

10. 如果上一个命令失败，为 `/usr/users` 下另一个用户的文件（或你主目录所在的任何文件）创建一个硬链接 `hard_link`。

11. 使用 `ls -1` 获取你工作目录的目录列表。`hard_link` 有什么异常？

12. 删除 `hard_link` 文件。如果你对文件所在的目录有写权限，就可以删除一个没有写权限的文件。

## 解决方案

1. `$ cp /etc/passwd dummy`

2. `$ ls -il dummy`

```
80537 -rw-r-- 1 you users 2623 Dec 23 13:01 dummy
```

3. `$ ln dummy hard_link`

4. `$ ls -il hard_link`

```
80537 -rw-r-- 2 you users 2623 Dec 23 13:01 hard_link
```

5. 链接数从 1 增加到 2。inode 节点、链接数、所有者、组、大小和日期都是相同的。唯一的区别是文件名本身。

6. `$ rm dummy`

7. `$ cat hard_link`

## 摘要

### 切换目录

由于 UNIX 文件结构是层次化的，所有文件或目录都是通过在目录链中跟踪路径直到到达目标目录来访问的。

要理解如何使用 `cd` 命令，你必须首先理解主目录（home directory）、工作目录（working directory）和路径名的概念。

主目录通常由包含用户名作为最后一个部分的路径名来标识。你的主目录永远不会改变。

你的工作目录定义为你在目录树中的当前位置。

### 列出文件

系统记录你所有文件的名称。你可以使用 `ls` 命令查看目录中所有文件的名称列表。

### 查找文件

有时你需要在系统上定位文件，但你并不确定定位它们所需的所有信息。`whereis` 和 `find` 命令在这些情况下非常有用。

### 查看文件

UNIX 提供了许多方法在终端屏幕上显示文件内容。提供此种功能的命令有：

| 命令 | 说明 |
| :--- | :--- |
| `cat` | 文件文本滚动显示 |
| `more` | 文件每次显示一页 |
| `head` | 屏幕上显示文件的前 10 行 |
| `tail` | 屏幕上显示文件的后 10 行 |

### 创建文件

可以使用 `cat` 命令通过 `>` 或 `>>` 符号重定向输出来创建文件。
