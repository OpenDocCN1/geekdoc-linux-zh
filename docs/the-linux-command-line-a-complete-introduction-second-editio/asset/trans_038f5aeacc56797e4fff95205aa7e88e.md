

## 构建一个游乐场

由于我们将进行一些实际的文件操作，让我们建立一个安全的地方来“玩”我们的文件操作命令。首先我们需要一个工作目录。我们将在主目录中创建一个并命名为 playground。

## 创建目录

mkdir 命令用于创建目录。为了创建我们的 playground 目录，我们将首先确保位于主目录中，然后创建新目录。

```
[me@linuxbox ~]$ cd
[me@linuxbox ~]$ mkdir playground
```

为了让我们的游乐场更有趣一些，让我们在其中创建几个名为 dir1 和 dir2 的目录。为此，我们将把当前工作目录更改为 playground 并执行另一个 mkdir。

```
[me@linuxbox ~]$ cd playground
[me@linuxbox playground]$ mkdir dir1 dir2
```

请注意，mkdir 命令会接受多个参数，使我们能够使用单个命令创建两个目录。

## 复制文件

接下来，让我们将一些数据放入我们的游乐场。我们将通过复制文件来实现这一点。使用 cp 命令，我们将把 /etc 目录中的 passwd 文件复制到当前工作目录。

```
[me@linuxbox playground]$ cp /etc/passwd .
```

请注意我们如何使用当前工作目录的简写，即单个尾随句点。现在如果我们执行 ls，就可以看到我们的文件。

```
[me@linuxbox playground]$ ls -l
total 12
drwxrwxr-x 2 me me 4096 2018-01-10 16:40 dir1
drwxrwxr-x 2 me me 4096 2018-01-10 16:40 dir2
-rw-r--r-- 1 me me 1650 2018-01-10 16:07 passwd
```

现在，为了好玩，让我们使用 -v 选项（详细）重复复制操作，看看它会做什么。

```
[me@linuxbox playground]$ cp -v /etc/passwd .
`/etc/passwd' -> `./passwd'
```

cp 命令再次执行了复制，但这次显示了一条简洁的消息，说明它正在执行的操作。请注意 cp 在没有任何警告的情况下覆盖了第一次复制。同样，这也是 cp 假设我们知道自己在做什么的情况。为了得到警告，我们将包含 -i（交互式）选项。

```
[me@linuxbox playground]$ cp -i /etc/passwd .
cp: overwrite `./passwd'?
```

通过输入 y 回复提示将导致文件被覆盖；任何其他字符（例如 n）将导致 cp 不动文件。

## 移动和重命名文件

现在，名称 passwd 似乎不太好玩，而这是一个游乐场，所以让我们把它改成其他名称。

```
[me@linuxbox playground]$ mv passwd fun
```

让我们把 fun 传来传去，通过将重命名后的文件移动到每个目录中再移回来。以下命令首先将其移动到目录 dir1：

```
[me@linuxbox playground]$ mv fun dir1
```

以下命令然后将其从 dir1 移动到 dir2：

```
[me@linuxbox playground]$ mv dir1/fun dir2
```

最后，此命令将其带回当前工作目录：

```
[me@linuxbox playground]$ mv dir2/fun .
```

接下来，让我们看看 mv 对目录的影响。首先我们将把数据文件再次移入 dir1，如下所示：

```
[me@linuxbox playground]$ mv fun dir1
```

然后我们将 dir1 移入 dir2 并用 ls 确认。

```
[me@linuxbox playground]$ mv dir1 dir2
[me@linuxbox playground]$ ls -l dir2
total 4
drwxrwxr-x 2 me me 4096 2018-01-11 06:06 dir1
[me@linuxbox playground]$ ls -l dir2/dir1
total 4
-rw-r--r-- 1 me me 1650 2018-01-10 16:33 fun
```

请注意，因为 dir2 已经存在，mv 将 dir1 移入了 dir2。如果 dir2 不存在，mv 就会将 dir1 重命名为 dir2。最后，让我们把所有东西都放回去。

```
[me@linuxbox playground]$ mv dir2/dir1 .
[me@linuxbox playground]$ mv dir1/fun .
```

## 创建硬链接

现在我们来试试链接。我们将首先创建一些指向我们数据文件的硬链接，如下所示：

```
[me@linuxbox playground]$ ln fun fun-hard
[me@linuxbox playground]$ ln fun dir1/fun-hard
[me@linuxbox playground]$ ln fun dir2/fun-hard
```

所以现在我们有四个 fun 文件的实例。让我们看看我们的游乐场目录。

```
[me@linuxbox playground]$ ls -l
total 16
drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir1
drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir2
-rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun
-rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun-hard
```

我们注意到的一件事是，fun 和 fun-hard 的列表中第二个字段都包含一个 4，这就是该文件现在存在的硬链接数。请记住，一个文件至少总有一个链接，因为文件名称是由链接创建的。那么，我们如何知道 fun 和 fun-hard 确实是同一个文件呢？在这种情况下，ls 并没有太大帮助。虽然我们可以看出 fun 和 fun-hard 的大小相同（第 5 个字段），但我们的列表没有办法确定。为了解决这个问题，我们必须深入挖掘一些。

在思考硬链接时，有助于想象文件由两部分组成。

- 包含文件内容的数据部分
- 存放文件名称的名称部分

当我们创建硬链接时，我们实际上是创建了额外的名称部分，它们都指向相同的数据部分。系统会将一系列磁盘块分配给称为 inode 的对象，然后与名称部分关联。因此，每个硬链接都引用包含文件内容的特定 inode。

ls 命令有一种方法可以显示此信息。它使用 -i 选项调用。

```
[me@linuxbox playground]$ ls -li
total 16
12353539 drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir1
12353540 drwxrwxr-x 2 me me 4096 2018-01-14 16:17 dir2
12353538 -rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun
12353538 -rw-r--r-- 4 me me 1650 2018-01-10 16:33 fun-hard
```

在此版本的列表中，第一个字段是 inode 编号，正如我们所见，fun 和 fun-hard 共享相同的 inode 编号，这证实它们是同一个文件。

