
```
缺点是与 `locate` 命令关联的数据库可能不是最新的。正如我们在本章后面将看到的，它默认在每天早上 4:02 更新。
```

### 读取文件

大多数 Linux 服务通过文本文件进行配置。有许多方法可以快速查看你选择的文件。你可以使用五个基本命令之一来浏览文本文件：`cat`、`more`、`less`、`head` 和 `tail`。

#### cat

`cat filename` 将文件名的内容发送到屏幕上。例如，以下命令读取你的基本密码数据库文件内容：

```
$ cat /etc/passwd
```

你还可以连续读取几个文件；例如，以下命令会连续滚动 `/etc/passwd` 和 `/etc/group`。

```
$ cat /etc/passwd /etc/group
```

#### more and less

`more` 和 `less` 命令相似。它们允许你逐行或按屏查看较长的文本文件。`more filename` 命令非常直观；它允许你按屏或逐行查看文件内容。

```
$ more /etc/samba/smb.conf
```

按行滚动按 `Enter` 键；按屏滚动按空格键。遗憾的是，使用 `more` 命令时，你只能向前滚动。如果想向后滚动，可以使用 `less` 命令。

```
$ less /etc/samba/smb.conf
```

你可以使用方向键上下滚动。按 `q` 退出 `less` 命令。

#### head and tail

`head` 和 `tail` 命令相似。它们允许你查看文件的开头或结尾。`head filename` 命令显示文件的前几行。例如：

```
$ head -n 5 /etc/samba/smb.conf
```

`tail filename` 命令显示文件的最后几行。例如：

```
$ tail -n 5 /etc/samba/smb.conf
```

### 创建和删除文件

为了管理文件，你需要学会如何创建和删除它们。命令包括 `touch`、`cp`、`mv` 和 `rm`。

#### touch

`touch` 命令创建一个空文件。例如，以下命令创建一个名为 `quota` 的文件：

```
$ touch home/quota
```

#### cp

`cp` 命令几乎 `ls` 一样灵活。自然地，你可以通过以下命令将一个文件的内容复制到另一个：

```
$ cp file1 file2
```

你可以将一个或多个文件复制到目录。例如，如果你想将当前目录下的所有文件复制到名为 `backup` 的目录，运行以下命令：

```
$ cp * backup
```

如果文件已存在，系统会提示你是否要覆盖副本。例如，如果你运行 `cp backup` 命令，你将尝试覆盖已复制的文件。`shell` 会警告此问题，如 `cp/file1?`

你可以回答 `y` 或 `n`。或者，你可以使用 `-f` 开关自动覆盖现有文件。

#### mv

`mv` 命令用于移动或重命名文件。例如，将 `file1` 重命名为 `file2`，请使用：

```
$ mv file1 file2
```

你还可以将文件或目录移动到另一个位置。例如，将 `file1` 和 `file2` 移动到 `backup` 目录，使用：

```
$ mv file1 file2 backup/
```

#### rm

`rm` 命令用于删除文件。例如，删除名为 `file1` 的文件，请使用：

```
$ rm file1
```

使用 `rm` 命令时要小心，因为删除的文件是永久的。要删除目录及其内容，请使用 `-r` 开关：

```
$ rm -r directory/
```

### 第 8 章：管理与维护

#### mv

在 Linux 中，如果你重命名一个文件，实际上是将其从一个文件名移动到另一个文件名。因此，Linux 的重命名命令是 `mv`。例如，如果你运行以下命令：

```bash
# mv file1 file2
```

`mv` 命令会创建 `file2`，将 `file1` 的内容复制到 `file2`，然后删除 `file1`。`mv` 命令的选项与 `cp` 命令的选项相似。我在表 4 中说明了一些相关示例。

**表 4. `mv` 命令示例。**

| 命令 | 解释 |
| :--- | :--- |
| `mv file1 file2` | 建立一个名为 `file2` 的新文件，将 `file1` 的内容复制到 `file2`，然后删除 `file1`。 |
| `mv file1 file2 file3 dir1` | 在 `dir1` 子目录中创建新文件 `file1`、`file2` 和 `file3`，然后删除当前目录下的 `file1`、`file2` 和 `file3`。 |
| `mv -i file1 file2` | 将 `file1` 的内容复制到 `file2`。如果 `file2` 已经存在，`mv -f` 命令将自动覆盖它。然后删除 `file1`。 |
| `mv -i file1 file2` | 将 `file1` 的内容复制到 `file2`。如果 `file2` 已经存在，`mv -i` 命令在覆盖前会请求确认。然后删除 `file1`。 |

#### rm

要删除 Linux 中的一个文件，你可以使用 `rm` 命令将其从系统中移除。像系统上的任何删除命令一样，如果使用不当，它可能是危险的。例如，如果你想删除当前目录下所有以 `a` 开头的文件，可以运行以下命令：

```bash
# rm a*
```

一旦在 Linux 中删除了一个文件，就没有“撤销删除”功能来恢复它。例如，Red Hat 进行了了项配置，要求 `root` 用户在删除文件之前必须进行确认。例如，如果你以 `root` 用户身份运行 `rm*`，你会收到类似下面的信息：

```bash
rm: remove regular file 'abcd'
```

这种现象是因为 Linux 的*别名（aliases）*概念，即用一个命令替换另一个命令。默认情况下，Red Hat 在标准的 Red Hat `.bashrc` 配置中为 `root` 用户包含了别名：

```bash
# 用户特定别名和函数

alias rm='rm -i'

alias cp='cp -i'

alias mv='mv -i'
```

如果你以 `root` 用户身份登录，可能想用一个命令删除一组文件和目录。例如，如果你想删除 `/tmp/orbit-tr` 目录下的文件和目录，可以运行以下命令：

```bash
# rm -rf /tmp/orbit-tr
```

`-r` 和 `-f` 选项的作用与 `cp` 和 `mv` 等其他类似命令相同。换句话说，它们 (`-f`) 强制删除指定的文件而不进行提示，并且是递归地 (`-r`)，这意味着 `/tmp/orbit-tr` 的子目录也会被自动删除。

`rm` 命令可能非常危险。如果你作为 `root` 用户，不小心在第一个斜杠后包含了一个空格，结果产生的命令将删除你计算机上的所有文件，包括根目录；然后它会尝试删除 `/tmp/orbit-tr` 子目录中的所有文件：

```bash
# rm -rf / /tmp/orbit-tr
```

请极度小心地运行 `rm -rf`。一个简单的错误就会删除你 Linux 计算机上的每一个文件。

表 5 说明了 `rm` 命令的一些示例。

**表 5. `rm` 命令示例。**

| 命令 | 解释 |
| :--- | :--- |
| `rm file1 file2` | 删除 `file1` 和 `file2`。 |
| `rm file1 file2 file3 dir1` | 在 `dir1` 子目录中创建新文件 `file1`、`file2` 和 `file3`，然后删除当前目录下的 `file1`、`file2` 和 `file3`。 |
| `rm -f file1 file2` | 如果你设置了别名 `rm='rf'`，`-f` 将强制删除 `file1` 和 `file2` 而不提示。 |
| `rm -r dir1` | 递归删除 `dir1` 目录的内容；`dir1` 中的子目录和文件也会被删除。 |

#### mkdir 和 rmdir

在 Linux 中，目录是一种特殊类型的文件。你可以使用 `mkdir` 和 `rmdir` 命令创建和删除这些特殊文件。在两种情况下，你都可以使用 `-p` 选项来创建或删除多级目录。例如，以下命令允许你创建目录 `DirA` 和 `DirB` 作为当前目录的子目录，其中 `DirB` 是 `DirA` 的子目录：

```bash
$ mkdir -p DirA/DirB
```

只要目录是空的，你就可以相同的方式删除目录：

```bash
$ rmdir -p DirA/DirB
```

如果其中任一目录包含文件，命令将被拒绝并显示以下消息：

```bash
rmdir: 'DirA/DirB/: Directory not empty
```

### 向文件末尾添加信息

这里有一个示例，你可以使用 `cat` 命令将之前描述的别名添加到用户的 `.bashrc` 配置文件中。一旦添加，这些别名可以帮助防止意外的文件覆盖。

如果你想将之前的别名应用到用户的家目录，请以 `mj` 或 `root` 运行以下命令：

```bash
