
```
Desktop emmett filethree junk2 questions
TestPro errors filetwo sample brio example myfile sample the world
dulaney example2 numbers simplesimon
eRRors fileone junk1 snapshot.gif
```

列表总是按字母顺序排列，大写字母在小写字母之前。该命令有许多选项，最常用的是 `-F`，它会显示条目的类型：

```
Desktop emmett filethree junk2 questions
TestPro errors filetwo sample brio example myfile sample the world
```

没有结尾字符的项是标准文件。带有 `/` 的项是目录。带有星号 `*` 的项是执行文件。符号链接用 `@` 符号表示。

另一个实用的选项是 `-a`，它会显示所有文件。默认情况下，`ls` 不显示隐藏文件。隐藏文件的第一个字符是点 `.`：

```
.Desktop emmett filethree junk2 questions
TestPro errors filetwo sample brio example myfile sample the world
.bash_history dulaney example2 numbers simplesimon
.file. junk1 snapshot.gif
```

> 注意：点可以出现在文件名的任何位置，并出现任意次数。只有当它们是第一个字符时才有意义。如果你用 `-A` 代替 `-a`，将忽略隐藏条目。无疑，最有用的选项是 `-l`，它会显示详细列表。条目看起来如下：

```
drwx------ 5 root 1024 Aug 30 11:12
-rw-r---- 1 root 548 Aug 23:01
-rw-r---- 1 root 28 Aug 22:26
```

基本上有七列，划分如下：

- 1. 权限。虽然全文讨论了权限，但现在重要的是识别条目的类型。`-` 表示文件，而 `d` 表示目录。

- 2. 链接数。如果是目录，它等于其下方的条目数；如果是文件，它等于引用它的方式数。

- 3. 创建（或拥有）该实体的所有者名称。

- 4. 该文件的组。

- 5. 文件的大小。

- 6. 创建或修改的日期。

- 7. 名称。

表 3.3 提供了 `ls` 的其他选项及其用途。

表 3.3 `ls` 命令选项

| 选项 | 用途 |
| --- | --- |
| -c | 按最后修改/修改顺序列表而非字母顺序 |
| -d | 列出目录 |
| -G | 与 -l 配合时不显示组 |
| -i | 显示每个条目的 inode 号（指针） |
| -n | 用数值显示所有者和组 |
| -o | 与 -l 相同 |
| -r | 反转显示顺序 |
| -R | 递归显示子目录中的条目 |
| -S | 排序 |
| -u | 按最后访问排序 |
| -w | 指定屏幕宽度 |
| -x | 显示行而非列 |
| -X | 按扩展名排序 |

### 应用 `touch`

文件或条目本质上有三个日期：创建、修改和访问。使用 `touch` 工具，你可以更改文件相关的访问和修改时间：

```
$ ls -l brio
-rw-r---- 1 root root 28 Aug 22 10:26 brio
$ touch brio
ls -l brio
-rw-r---- 1 root root 28 Aug 30 16:01 brio
```

`touch` 工具也可以使用几个选项，总结如下表所示：

| 选项 | 用途 |
| --- | --- |
| -a | 仅更改访问时间 |
| -m | 仅更改修改时间 |
| -r | 使用引用文件的时间/日期进行更改，而不是当前时间/日期 |

后者的示例如下：

```
$ ls -l tuesday wednesday
-rw-r--r- 1 root root 85 Aug 22 10:26 tuesday
-rw-r--r- 1 root root 85 Aug 29 13:08 wednesday
$ touch tuesday -r wednesday
ls -l tuesday wednesday
-rw-r--r- 1 root root 85 Aug 29 13:08 tuesday
-rw-r--r- 1 root root 85 Aug 29 13:08 wednesday
```

> 如果你使用 `touch` 工具处理一个不存在的文件名，它将创建一个具有当前日期和时间且大小为零的文件。

### 复制与移动

涵盖的课程目标

- 4. 在命令行执行命令 (3036)
- 5. 常见的命令行任务 (3036)
- 9. 复制和移动文件及目录 (3036)
- 10. 创建目录 (3036)
- 11. 删除文件和目录 (3036)

如果东西永远不移动或改变，系统管理将会容易得多。不幸的是，很少有东西保持不变，变化以不停的速度发生着。Linux 提供了两个用于复制和移动文件的强大工具：分别是 `cp` 和 `mv`，以及第三个工具 `dd`——它结合了后者的功能。

## 基础 GNU 和 Unix 命令

# 第 3 章

```
$ ls -l fileone onefile
ls: onefile: No such file or directory
-rw-r--r-- 1 root root 85 Aug 22 10:26
->onefile
```

```
$ cp fileone onefile
ls -l fileone onefile
-rw-r--r-- 1 root root 85 Aug 22 10:26
->onefile
-rw-r--r-- 1 eduelaney users 85 Aug 30 16:16
->onefile
```

注意原始条目（源）保持不变，但现在有了第二个条目（目标）。在第二个条目中，内容是相同的，但日期和时间是当前的（执行 `cp` 时的时间），而不是源文件的时间。同样注意，新文件的所有者和组将变为执行命令的用户。这与你完全从开始创建目标文件时的情况是相同的。

> 要能复制文件——创建一个内容与另一个文件相同的新实体——你只需要对源文件读取权限。

`-p` 选项可以强制尽可能多的旧变量保持不变。它保留了属性方面可以保留的内容：

```
$ ls -l filenextfile
ls: nextfile: No such file or directory
-rw-r--r-- 1 root root 85 Aug 22 10:26
->fileone
```

```
$ cp -p fileone nextfile
ls -l fileone nextfile
-rw-r--r-- 1 root root 85 Aug 22 10:26
->fileone
-rw-r--r-- 1 eduelaney users 85 Aug 22 10:26
->nextfile
```

注意与源相关的日期和时间被保留了，但所有者和组仍然更改。

# Novell 认证 Linux 专业学习指南

当你执行复制操作时，实用程序首先检查源文件是否存在。如果存在，将创建指定为目标的文件（大小为 0），并复制源的内容。重点在于目标总是会被创建的——无论它之前是否存在。以下是一个示例：

```
$ ls -l fileone filetwo
--r--r---- 1 root root 85 Aug 22 10:26
>fileone
--r--r---- 1 root root 16432 Aug 28 13:43
>filetwo
$
$ cp fileone filetwo
$ ls -l fileone filetwo
--r--r---- 1 root root 85 Aug 22 10:26
>fileone
--r--r---- 1 eduelaney users 85 Aug 30 16:18
>filetwo
$
```

`filetwo` 的原始内容已经丢失（除非有备份带版本），因为 `filetwo` 被创建为 `fileone` 的副本。有一个 `-i`（询问为 inquire）选项，可用于询问如果目标文件已存在，你是否真的想删除目标文件的内容：

```
$ ls -l fileone filetwo
--r--r---- 1 root root 85 Aug 22 10:26
>fileone
--r--r---- 1 root root 16432 Aug 28 13:43
>filetwo
$
$ cp -i fileone filetwo
cp: overwrite 'filetwo?'
```

在提示符处，你可以输入 "y" 执行操作，或输入任何其他内容停止操作。

你可以将多个文件从一个目录复制到另一个目录，只要最后一个项目是存放这些文件的有效目录：
