
当我们删除最后一个硬链接时，文件内容才会消失：

```
[me@linuxbox playground]$$ rm link2 link3
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
```

意识到硬链接是非常重要的，因为你可能会偶尔遇到它们，但现代实践更倾向于使用符号链接，我们接下来将介绍。

## 符号链接

符号链接是为了克服硬链接的局限性而创建的。它们通过创建一个特殊类型的文件来工作，该文件包含一个指向被引用文件或目录的文本指针。在这方面，它们的操作方式与 Windows 快捷方式相似，尽管它们早于 Windows 的这一功能多年。

被符号链接指向的文件和符号链接本身是无法区分的。例如，如果你向符号链接写入内容，内容会被写入所指向的文件。然而，当你删除符号链接时，删除的只是链接，而不是文件。如果在删除符号链接之前删除了文件，链接将继续存在但指向空值。在这种情况下，该链接被称为“断开的”。在许多实现中，`ls` 命令将用不同的颜色（如红色）显示断开的链接以显示它们的存在。

链接的概念可能看起来很混乱，但请坚持。我们将尝试所有这些内容，理想情况下它们会变得清晰。

## 构建一个实验场

由于我们要进行一些真实的文件操作，让我们建立一个安全的地方来“玩”我们的文件操作命令。我们需要一个目录来工作。我们将在家目录下创建一个并将其命名为 `playground`。

## 创建目录

`mkdir` 命令用于创建目录。为了创建我们的 `playground` 目录，我们首先确保位于主目录下，然后创建新目录。

```
[me@linux ~]$ cd
[me@linuxbox ~]$ mkdir playground
```

为了让我们的实验场更有趣，让我们在里面创建两个名为 `dir1` 和 `dir2` 的目录。为了做到，我们将当前工作目录切换到 `playground` 并执行另一个 `mkdir`。

```
[me@linuxbox ~]$ cd playground
[me@linuxbox playground]$ mkdir dir1 dir2
```

注意，`mkdir` 命令接受多个参数，允许我们通过单个命令创建多个目录。

## 复制文件

接下来，让我们向实验场中放入一些数据。我们将通过复制文件来实现。使用 `cp` 命令，我们将从 `/etc` 目录将 `passwd` 文件复制到当前工作目录。

```
[me@linuxbox playground]$$ cp /etc/passwd .
```

注意我们如何使用当前工作目录的简写，即结尾的单点 `.`。所以现在如果我们执行 `ls`，就会看到我们的文件。

```
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
--rw-r--r-- 1 me 1650 2018-01-10 16:07 passwd
```

现在，为了好玩，让我们使用 `-v`（详细模式）选项重复复制，看看它的作用。

```
[me@linuxbox playground]$$ cp -v /etc/passwd
/etc/passwd -> './passwd'
```

`cp` 命令再次执行了复制，但这次显示了一条简短的消息，指示它正在执行的操作。注意 `cp` 在没有任何警告的情况下覆盖了第一次复制的文件。同样，这是 `cp` 假设我们自己在做什么的情况。为了获取警告，我们将包含 `-i`（交互模式）选项。

```
[me@linuxbox playground]$$ cp -i /etc/passwd
cp: overwrite "./passwd"?
```

通过输入 `y` 响应提示会导致文件覆盖；任何其他字符（例如 `n`）将导致 `cp` 保持文件不变。

## 移动和重命名文件

现在 `passwd` 这个名字看起来并不好玩，而且这里是实验场，让我们把它改成别的。

```
[me@linuxbox playground]$$ mv passwd fun
```

让我们通过将重命名后的文件移动到每个目录中再移动回来来增加点趣味性。以下操作首先将其移动到目录：

```
[me@linuxbox playground]$$ mv fun dir1
```

接下来的操作将其从 `dir1` 移动到 `dir2`：

```
[me@linuxbox playground]$$ mv dir1/fun dir2
```

最后，此命令将它带回当前工作目录：

```
[me@linuxbox playground]$$ mv dir2/fun .
```

接下来，让我们看看 `mv` 对目录的影响。首先我们将数据文件移动到 `dir1`，如下所示：

```
[me@linuxbox playground]$$ mv fun dir1
```

然后我们将 `dir1` 移动到 `dir2` 并用 `ls` 确认：

```
[me@linuxbox playground]$$ mv dir1 dir2
[me@linuxbox playground]$$ ls -dir2
total 4
drwxr-xr-x 2 me 4096 2018-01-11 16:06 dir1
``` (注：原文此处为 `ls -dir2` 疑似有误))total 4

drwxr-xr-x 2 me 4096 2018-01-11 16:06 dir1

注意，在删除 `passwd` 之前，`dir2` 已经存在了，所以 `mv` 会覆盖它。

## 创建硬链接

让我们在实验场中尝试一些硬链接。首先我们为文件创建一些硬链接：

```
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
--rw-r--r-- 1 me 1650 2018-01-10 16:07 passwd
```

现在，我们为 `passwd` 创建一些硬链接：

```
[me@linuxbox playground]$$ ln passwd link1
[me@linuxbox playground]$$ ln passwd link2
[me@linuxbox playground]$$ ln passwd link3
```

让我们看看 `ls` 显示的这些硬链接的数量：

```
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
--rw-r--r-- 4 me 1650 2018-01-10 16:07 passwd
--rw-r--r-- 4 me 1650 2018-01-10 16:07 link1
--rw-r--r-- 4 me 1650 2018-01-10 16:07 link2
--rw-r--r-- 4 me 1650 2018-01-10 16:07 link3
```

我们注意到数字 `4` 是指向该文件的硬链接数量。当我们删除其中一个链接时，这个数字会减少：

```
[me@linuxbox playground]$$ rm link1
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
--rw-r--r-- 3 me 1650 2018-01-10 16:07 passwd
--rw-r--r-- 3 me 1650 2018-01-10 16:07 link2
--rw-r--r-- 3 me 1650 2018-01-10 16:07 link3
```

当我们删除最后一个硬链接时，文件内容才会消失：

```
[me@linuxbox playground]$$ rm link2 link3
[me@linuxbox playground]$$ ls -1
total 12
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir1
drwxrwx-x 2 me 4096 2018-01-10 16:40 dir2
```

意识到硬链接是非常重要的，因为你可能会偶尔遇到它们，但现代实践更倾向于使用符号链接，我们接下来将介绍。

## 符号链接
