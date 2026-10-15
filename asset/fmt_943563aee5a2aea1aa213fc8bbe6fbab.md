
绝对路径包含了从文件系统的任何地方到达 `Reports` 所需的所有信息。缺点是它非常繁琐。

第二个示例（`cd Reports`）输入起来简单得多。这是一个**相对路径**的示例。相对路径较短，但它们只相对于你当前的位置才有意义。考虑这个类比：我正在你家里拜访。你告诉你的朋友住在隔壁。我会理解那个位置，因为它是相对于我当前位置的。但如果你在电话里告诉我，我将无法找到你朋友的房子。你需要给我具体的街道地址。

## 特殊相对路径

Linux 为我们提供了在导航时缩短路径的方法。要显示第一个特殊路径，我们输入带有 `-a` 标志的 `ls` 命令。该标志会修改 `ls` 命令，使其列出所有路径和目录，包括隐藏文件和目录：

```
user@hostname ~/Documents/Reports $ ls -a
..
report2018.txt
```

> 注意：你可以参考 `ls` 的帮助页面（man page）来理解 `-a` 的作用。

## Linux 基础（版本 1.6） | 主题 2：在 Linux 系统中找到路

此命令显示了两个额外结果：这些是特殊路径。它们不代表新文件或目录，而是代表你已经知道的目录：

- `.` 表示*当前位置*（在此情况下，是 `Reports`）。
- `..` 表示*父目录*（在此情况下，是 `Documents`）。

通常没有必要对当前位置特殊相对路径。输入 `report2018.txt` 比输入 `./report2018.txt` 更容易且更易理解。但 `.` 有你将在未来章节中学习到的用途。现在，我们将关注父目录的相对路径：

```
user@hostname ~/Documents/Reports $ cd ..
user@hostname ~/Documents $ pwd
/home/user/Documents
```

使用 `..` 代替绝对路径，`cd` 的示例要简单得多。此外，我们可以结合这种模式快速地在文件树向上导航。

```
$ user@hostname ~/Documents $ cd ../
$ pwd
/home
```

### 引导式练习

1. 对于以下每个路径，识别它们是**绝对**的还是**相对**的：

| `/home/user/Downloads` | 绝对 |
| `../Reports` | 相对 |
| `/var` | 绝对 |
| `docs` | 相对 |
| `/` | 绝对 |

2. 观察以下文件结构。注意：当使用带有 `-F` 选项调用 `tree` 时，目录以斜杠（`/`）结尾。你需要权限才能在根（`/`）目录上运行 `tree` 命令。以下是示例输出，并不代表完整的目录结构。使用它来回答以下问题：

```
$ sudo tree -F /
├── etc/
│   ├── network/
│   │   └── interfaces
│   ├── systemd/
│   │   └── resolved.conf
│   ├── system/
│   │   └── system.conf
│   └── user/
│       └── user.conf
└── udev/
    ├── rules.d/
    └── udev.conf
└── home/
    ├── lost+found/
    ├── user/
        └── Documents/
12 个目录，5 个文件
```

使用此结构回答以下问题：

用户输入了以下命令：

## Linux 基础 | 主题 2：在 Linux 系统中找到路

```
$ cd /udev
$ ls -a
```

`ls -a` 命令的输出是什么？

- 3. 为以下各项输入最短的命令：
- 你的当前位置是根目录（`/`）。进入 `lost+found` 目录（示例）：
- 你的当前位置是根目录（`/`）。进入名为 `/etc/` 的目录。
- 你的当前位置是 `/home/user/Documents/`。进入名为 `/etc/` 的目录。
- 你的当前位置是 `/etc/systemd/system/`。进入名为 `/home/user`。

```
$ cd home/lost+found
```

- 4. 考虑以下命令：
`$pwd`
`/etc/udev/rules.d`
`$ cd ../systemd/user`
`$ cd ..`
`$pwd`

最后一个 `pwd` 命令的输出是什么？

### 探索性练习

1. 假设用户输入了以下命令：

```
$ mkdir "this is a test"
$ ls
this is a test
```

输入 `cd this` 后按下 TAB 键，现在提示符上显示什么？

这是自动补全的示例，它不仅可以节省时间，还是防止拼写错误的重要工具。

3. 尝试创建一个包含 `\` 字符的目录。使用 `ls` 显示目录名称并删除该目录。

### 总结

在本节中，你学习了：

- Linux 文件系统的基础知识
- 父目录和子目录的区别
- 绝对文件路径和相对路径的区别
- 特殊相对路径 `.` 和 `..`
- 使用 `cd` 导航文件系统
- 使用 `pwd` 显示当前位置
- 使用 `ls -a` 列出所有文件和目录

本节讨论了以下命令：

```
cd
```

更改当前目录。

```
pwd
```

打印当前目录的路径

```
ls
```

列出目录内容并显示文件的属性

```
mkdir
```

创建一个新目录

```
tree
```

显示目录树的层次级列表。

## Linux 基础 (版本 1.6) | 主题 2：在 Linux 系统中寻找路径

```
$ cd /etc/udev
$ ls -a
```

`ls -a` 命令的输出是什么？

```
.. rules.d udev.conf
```

3. 请为以下每个项目输入最短的命令：

- 你的当前位置是 root (`/`)。进入家目录目录下的 `lost+found` 目录的命令（示例）：

```bash
$ cd home/lost+found
```

- 你的当前位置是 root (`/`)。进入名为 `network` 的目录的命令：

```bash
$ cd etc/network
```

- 你的当前位置是 `Documents`。进入名为 `etc` 的目录：

```bash
$ cd /etc
```

- 你的当前位置是 `system`。进入名为 `user` 的目录：

```bash
$ cd /home/user
```

4. 考虑以下命令：

```bash
$ pwd
/etc/udev/rules.d
$ cd ../../systemd/user
$ cd ..
$ pwd
```

最后一个 `pwd` 命令的输出是什么？

```
/etc/systemd
```

### 探索性练习答案

1. 假设用户输入了以下命令：

```bash
$ mkdir "this is a test"
$ ls
this is a test
```

哪个 `cd` 命令允许你进入此目录？

```bash
$ cd this\is\ a\ test
```

2. 再次尝试，但在输入 `cd this_` 后按下 TAB 键。现在提示符上显示了什么？

```bash
$ cd this\is\ a\ test
```

这是自动补全的示例，它不仅是一个节省时间、还能防止拼写错误的宝贵工具。

3. 尝试创建一个包含 `\` 字符的目录。使用 `ls` 显示目录名称并删除该目录。

你可以使用另一个反斜杠 (`\\`) 来转义反斜杠，或者在整个目录名称周围使用双引号：

```bash
$ mkdir my\dir
$ ls
'my\dir'
$ rmdir 'my\dir'
```

# Linux 专业协会 (LPI)

## 2.3 第 2 节

| 证书: | Linux Essentials |
|---|---|
| 版本: | 1.6 |
| 主题: | 2 在 Linux 系统中寻找路径 |
| 目标: | 2.3 使用目录和列出文件 |
| 课程: | 2 / 2 |

### 引言

Unix 操作系统最初是为 20 世纪 60 年代的主机设计的。这些计算机由许多用户共享，他们通过终端访问系统资源。这些基本理念延续到了今天的 Linux 系统。我们仍然谈论使用“终端”在 shell 中输入命令，而且每个 Linux 系统的组织方式都使得在单个系统上创建许多用户变得很容易。

### 目录

这是 Linux 中一个普通文件系统的示例：

```
$ tree -L 1 / /
|├── bin
├── boot
├── cdrom
├── dev
└── etc
```
