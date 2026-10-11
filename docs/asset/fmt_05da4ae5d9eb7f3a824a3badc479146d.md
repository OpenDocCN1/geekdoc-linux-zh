
该文件的所有者是 `carol`，组也是 `carol`。现在，让我们将拥有文件的组改为另一个组，比如 `students`：

```bash
$ chown carol:students text.txt

$ ls -l text.txt

-rw-rw---- 1 carol 1881 Dec 10 15:57 text.txt
```

请记住，文件的所有者不需要属于拥有该文件的组。在上面的示例中，用户 `carol` 不需要是 `students` 组的成员。

然而，为了将文件的组所有权转移到该组，她必须是该组的成员。

如果你不想更改用户或组，可以省略它们。因此，如果只想更改文件的组，可以使用 `chown :students text.txt`。如果只想更改用户，命令应为 `chown carol text.txt`。或者，你也可以使用命令 `chgrp students text.txt` 来仅更改组。

除非你是系统管理员 `root`，否则你无法更改属于其他用户或你不所属的组的文件的所有权。如果你尝试这样做，你将得到错误信息 `Operation not permitted`（不允许的操作）。

## 查询组

在更改文件所有权之前，了解系统上存在哪些组、哪些用户是组的成员以及一个用户属于哪些组可能会有用。这些任务可以通过两个命令完成：`groups` 和 `groupmems`。

要查看系统中存在哪些组，只需输入 `groups`：

```bash
$ groups

carol students cdrom sudo dip plugdev ladmin sambashare
```

如果你想知道一个用户属于哪些组，请将用户名作为参数：

```bash
$ groups carol

carol : carol students cdrom sudo dip plugdev ladmin sambashare
```

要反过来操作，显示哪些用户属于一个组，请使用 `groupmems`。参数 `-g` 指定组，`-l` 将列出其所有成员：

```bash
$ sudo groupmems -g cdrom -l

carol
```

`groupmems` 只能以 `root`（系统管理员）身份运行。如果你当前不是以 `root` 登录，请在命令前添加 `sudo`。

## 特殊权限

除了用户、组和其他人的读、写、执行权限外，每个文件还可以有三个特殊权限，这些权限可以更改目录的工作方式或程序的运行方式。它们可以用符号模式或数字模式指定，如下所示：

### 粘滞位 Sticky Bit

粘滞位也称为限制删除标记，其八进制值为 `1`，在符号模式下用“其他用户”权限中的 `t` 表示。它只适用于目录，在 Linux 上，它可以防止用户在不拥有该文件或目录的情况下，从目录中删除或重命名该文件。

带有粘滞位的目录在 `ls -l` 的输出中，其他用户的权限 `x` 会替换为 `t`：

```bash
$ ls -ld Sample_Directory/

drwxr-xr-t 2 carol 4096 Dec 20 21:25 text.txt
```
（在数字模式下，此处应为目录）
```bash
$ ls -ld Sample_Directory/

drwxr-xr-t 2 carol 4096 Dec 20 21:25 text.txt
```

### 组 ID 位 GID

组 ID 位也称为 `SGID`，其八进制值为 `2`，在符号模式下用组权限中的 `s` 表示。当应用于目录时，它允许在该目录下创建的文件继承父目录的组所有权。在 `ls -l` 的输出中显示如下：

```bash
$ ls -ld Sample_Directory/

drwxr-xr-s 2 carol 4096 Dec 20 21:25 text.txt
```

### 用户 ID 位 UID

用户 ID 位也称为 `SUID`，其八进制值为 `4`，在符号模式下用用户权限中的 `s` 表示。它主要适用于文件，并允许程序以文件所有者的权限运行。在 `ls -l` 的输出中显示如下：

```bash
$ ls -l test.sh

-rws-xr-x 1 carol 33 Dec 11 10:36 test.sh
```

### 引导练习

1. 使用 `mkdir` 命令创建一个名为 `emptydir` 的目录。现在，使用 `ls` 列出该目录的权限。

2. 使用 `touch` 命令创建一个名为 `emptyfile` 的空文件。现在，使用符号模式 `chmod` 为文件所有者添加执行权限，并移除所有人的执行权限。仅使用一个 `chmod` 命令完成。

3. 使用 `chmod 754 text.txt` 后，`text.txt` 的权限是多少？

4. 假设名为 `test.sh` 的文件所有权如下：

```bash
-rwxr-sr-x 1 carol root      33 Dec 11 10:36 test.sh
```

- 文件所有者的权限是什么？
- 如果用户 `john` 运行此脚本，它将以哪个用户的权限运行？
- 使用数字表示法，`chmod` 的语法应该是什么以取消该文件的特殊权限？

5. 考虑此文件：

```bash
ls -l /dev/sdb1

br-rw---- 1 root disk 8, 17 Dec 21 18:51 /dev/sdb1
```

`sdb1` 是什么类型的文件？谁可以向它写入数据？

6. 考虑以下 4 个文件：

```
drwxr-xr-t 2 carol carol 4,0K Dec 20 18:46 Another_Directory
----rr--r-- 1 carol carol 0 Dec 11 10:55 foo.bar
-iw-rw-r-- 1 carol carol 1,2G Dec 20 18:22 HugeFile.zip
drwxr-sr-x 2 carol users 4,0K Jan 18 17:26 Sample_Directory
```

使用 4 位数字表示法写出每个文件和目录对应的权限。

#### Another_Directory

#### foo.bar

#### HugeFile.zip

#### Sample_Directory

### 探索性练习

1. 在终端上尝试此操作：创建一个名为 `emptyfile` 的空文件。现在使用 `chmod 000 emptyfile` 将该文件的权限“清零”。如果你在数字模式下仅为 `chmod` 一个值来更改 `emptyfile` 的权限，例如 `chmod 4 emptyfile`，会发生什么？如果使用两个值，例如 `chmod 44 emptyfile` 呢？我们从 `chmod` 读取数值的方式中可以学习什么？

2. 你可以执行一个你拥有执行权限但没有读取权限 `--x` 的文件吗？为什么或者为什么不行？

3. 考虑 Linux 系统上临时目录 `/tmp` 的权限：

```
$ ls -l /tmp

drwxrwxrwt 1 root root 16K Dec 21 18:58 tmp
```

用户、组和其他用户都拥有完全权限。但普通用户可以删除此目录内的任何文件吗？为什么？

4. 一个名为 `test.sh` 的文件具有以下权限：`-rwsr-xr-x`，这意味着设置了 `SUID` 位。现在，运行以下命令：

```
$ chmod u-x test.sh
$ ls -l test.sh

-rwSr-xr-x 1 carol carol 33 Dec 11 10:36 test.sh
```

我们做了什么？大写的 `$` 代表什么？

5. 你将如何创建一个名为 `Box` 的目录，其中所有文件都自动属于组 `users`，并且只能由创建它们的的用户删除？

### 总结

作为一个多用户系统，Linux 需要一种方法来跟踪谁拥有每个文件以及谁可以访问它。这是通过三级权限系统实现的，在本节中，我们学习了它的所有工作原理。

在本节中，你学习了如何使用 `ls` 获取文件权限信息，如何使用 `chmod` 控制或更改谁可以创建、删除或修改文件（使用符号表示法），以及如何使用 `chown` 和 `chgrp` 更改文件的所有权。

本节讨论了以下命令：

`ls`

- 列出文件，可选地包括权限等详细信息。

`chmod`

更改文件或目录的权限。

`chown`

更改文件或目录的所有者和/或所属组。

`chgrp`

更改文件或目录的所属组。

### 引导性练习答案

- 1. 使用命令 `mkdir emptdir` 创建名为 `emptdir` 的目录。现在，使用 `ls` 列出 `emptdir` 目录的权限。

给 `ls` 添加 `-d` 参数以查看目录的属性，而不是列出其内容。因此答案是：

```
ls -l -d emptdir
```
