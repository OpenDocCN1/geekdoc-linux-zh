

![](img/75f39fc91296b889c0653851accdfd46_160_0.png)

图 3-7 /home/denise/krsort.dir.old

![](img/75f39fc91296b889c0653851accdfd46_160_1.png)

然后，我们可以创建一个名为 **krsort.dir.new** 的新目录，并将文件复制到该目录中，如图 3-8 所示：

![](img/75f39fc91296b889c0653851accdfd46_160_2.png)

```
$ mkdir ../krsort.dir.new
$ cp krsort ../krsort.dir.new
$ ls -l ../krsort.dir.new
total 68
-rwxr-xr-x  1 denise    users    34592 Oct 27 18:27 krsort
$
```

![](img/75f39fc91296b889c0653851accdfd46_160_3.png)

![](img/75f39fc91296b889c0653851accdfd46_161_0.png)

图 3-8 **/home/denise/krsort.dir.new**

![](img/75f39fc91296b889c0653851accdfd46_161_1.png)

现在让我们尝试 cp 的 -i 选项。如果我们试图将文件复制到已存在的文件名，系统会询问我们是否要覆盖目标文件。我们会收到提示，告知目标文件已存在，随后可以为我们要复制的文件选择一个新的名称，如图 3-9 所示：

![](img/75f39fc91296b889c0653851accdfd46_161_2.png)

![](img/75f39fc91296b889c0653851accdfd46_161_3.png)

```
$ pwd
/users/denise/krsort.dir.old
$ cp -i krsort ../krsort.dir.new
overwrite ../krsort.dir.new/krsort? (y/n) n
$ cp krsort ../krsort.dir.new/krsort.new.name
$ ls -l ../krsort.dir.new
total 136
-rwxr-xr-x 1 denise users 34592 Oct 27 18:27 krsort
-rwxr-xr-x 1 denise users 34592 Oct 27 18:29 krsort.new.name
$
```

![](img/75f39fc91296b889c0653851accdfd46_162_0.png)

图 3-9 已添加 **/home/denise/krsort.dir.new/krsort.new.name**

我们也可以在 **cp** 中使用通配符，将 **krsort.dir.old** 中的所有文件复制到 **krsort.dir.new**，如图 3-10 所示：

```
$ cp * ../krsort.dir.new
$ ls -l ../krsort.dir.new
total 236
-rwxr-xr-x  1 denise    users   34592 Oct 27 18:30 krsort
-rwxr-xr-x  1 denise    users   3234 Oct 27 18:30 krsort.c
-rwxr-xr-x  1 denise    users   32756 Oct 27 18:30 krsort.dos
-rwxr-xr-x  1 denise    users   34592 Oct 27 18:29
krsort.new.name
-rw-r--r--  1 denise    users   9922 Oct 27 18:30 krsort.q
-rwxr-xr-x  1 denise    users   3085 Oct 27 18:30 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_163_0.png)

图 3-10 所有文件已复制到 /home/denise/krsort.dir.new

## 使用 mv 命令

让我们从头开始，回到 **krsort.dir.new** 目录为空的点，如图 3-11 所示：

![](img/75f39fc91296b889c0653851accdfd46_164_0.png)

图 3-11 **空的 /home/denise/krsort.dir.new 目录**

现在，我们可以将文件 **krsort** 移动到 **krsort.dir.new** 目录，如图 3-12 所示：

```
$ mv krsort ../krsort.dir.new
$ ls -l ../krsort.dir.new
total 68
-rwxr-xr-x 1 denise users 34592 Oct 27 18:20 krsort
$
```

*   手册页：`mv - 3`
*   手册页：`ls - 2`

![](img/75f39fc91296b889c0653851accdfd46_165_0.png)

如果我们现在尝试使用 **-i** 选项将 **krsort** 移动到 **krsort.dir.new** 目录并覆盖文件 **krsort**，我们会得到以下结果：

![](img/75f39fc91296b889c0653851accdfd46_165_1.png)

```
$ mv -i krsort ../krsort.dir.new/krsort
overwrite ../krsort.dir.new/krsort? (y/n) n
$
```

由于我们对 **mv** 使用了 **-i** 选项，系统会询问我们是否允许在移动时覆盖文件。由于我们对这个问题回答了 *n*，文件未被覆盖。

我们也可以在使用 **mv** 命令时使用通配符，将 **krsort.dir.old** 目录中的所有文件复制到 **krsort.dir.new** 目录。如果没有 **-i** 选项，**krsort.dir.new** 目录中的任何文件将被同名文件覆盖，如图 3-13 所示：

```
$ mv * ../krsort.dir.new
$ ls -l ../krsort.dir.new
total 168
-rwxr-xr-x 1 denise users 34592 Oct 27 18:44 krsort
-rwxr-xr-x 1 denise users 3234 Oct 27 18:46 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 27 18:46 krsort.dos
-rw-r--r-- 1 denise users 9922 Oct 27 18:46 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 27 18:46 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_166_0.png)

## 深入挖掘 rm 和 rmdir 命令

在 UNIX 世界中，最令人望而生畏的命令（我可能会说是有充分理由的）是 **rm** 命令。**rm** 随时可以删除任何你想要的东西，除非你使用 -i 选项，否则不会询问任何问题。

想立即摧毁你的系统吗？**rm** 会很乐意帮你。作为一个普通用户，而不是系统管理员，你通常没有权限这样做。然而，知道这种可能性是存在的，让人感到不安。此外，你很可能有权限删除你自己所有的文件和目录。只需简单地在 rm 命令中使用 -i 选项，就可以轻松避免所有这些。

![](img/75f39fc91296b889c0653851accdfd46_167_0.png)

让我们假设 **krsort.dir.new** 和 **krsort.dir.old** 是相同的目录，如图 3-14 所示：

![](img/75f39fc91296b889c0653851accdfd46_167_1.png)

**图 3-14** /home/denise/krsort.dir.old 和 /home/denise/krsort.dir.new (相同)

要从 **krsort.dir.new** 交互式地删除文件，请执行以下操作：

```
$ rm -i ../krsort.dir.new/*
../krsort.dir.new/krsort: ? (y/n) n
../krsort.dir.new/krsort.c: ? (y/n) n
../krsort.dir.new/krsort.dos: ? (y/n) n
../krsort.dir.new/krsort.q: ? (y/n) n
../krsort.dir.new/krsortorig.c: ? (y/n) n
$ ls -l ../krsort.dir.new
total 168
-rwxr-xr-x  1 denise  users  34592 Oct 27 18:44 krsort
-rwxr-xr-x  1 denise  users   3234 Oct 27 18:46 krsort.c
-rwxr-xr-x  1 denise  users  32756 Oct 27 18:46 krsort.dos
-rw-r--r--  1 denise  users   9922 Oct 27 18:46 krsort.q
-rwxr-xr-x  1 denise  users   3085 Oct 27 18:46 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_167_2.png)

显然，这导致没有从 **krsort.dir.new** 中删除任何东西，因为我们在被询问是否要删除文件时回答了 *n*。

现在让我们继续向 **krsort.dir.new** 添加一个以“.”开头的文件。*touch* 命令正是做这个的，创建一个没有内容的文件，如图 3-15 所示：

```
$ touch ../krsort.dir.new/.dotfile
$ ls -al ../krsort.dir.new
total 172
drwxr-xr-x 2 denise users 1024 Oct 27 18:54 .
drwxrwxr-x 4 denise users 1024 Oct 27 18:40 ..
-rw-r--r-- 1 denise users 0 Oct 27 18:56 .dotfile
-rwxr-xr-x 1 denise users 34592 Oct 27 18:44 krsort
-rwxr-xr-x 1 denise users 3234 Oct 27 18:46 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 27 18:46 krsort.dos
-rw-r--r-- 1 denise users 9922 Oct 27 18:46 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 27 18:46 krsortorig.c
$
```

![](img/75f39fc91296b889c0653851accdfd46_168_0.png)

![](img/75f39fc91296b889c0653851accdfd46_168_1.png)

如果我们现在尝试使用之前发出的相同 `rm` 命令来删除文件，我们会看到以下结果，如图 3-16 所示：

```
$ rm -i ../krsort.dir.new/*
../krsort.dir.new/krsort: ? (y/n) y
../krsort.dir.new/krsort.c: ? (y/n) y
../krsort.dir.new/krsort.dos: ? (y/n) y
../krsort.dir.new/krsort.q: ? (y/n) y
../krsort.dir.new/krsortorig.c: ? (y/n) y
$ ls -al ../krsort.dir.new
total 4
drwxr-xr-x     2 denise     users        1024 Oct 27 18:57 .
drwxrwxr-x     4 denise     users        1024 Oct 27 18:40 ..
-rw-r--r--     1 denise     users           0 Oct 27 18:56 .dotfile
```

![](img/75f39fc91296b889c0653851accdfd46_169_0.png)

与 `rm` 命令一起使用的通配符 `"*"` 没有删除文件 `.dotfile`。该目录中的文件 `.dotfile` 阻止了 `rmdir` 命令删除 `krsort.dir.new`。在 **rmdir** 命令成功删除 **krsort.dir.new** 之前，必须先删除该文件。

```
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
rmdir: ../krsort.dir.new: Directory not empty
$ rm ../krsort.dir.new/.dotfile
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
$
```

![](img/75f39fc91296b889c0653851accdfd46_170_0.png)

![](img/75f39fc91296b889c0653851accdfd46_170_1.png)

**rmdir** 现在成功删除了 **krsort.dir.new**，因为 **.dotfile** 已消失，如图 3-17 所示：

![](img/75f39fc91296b889c0653851accdfd46_170_2.png)

图 3-17 **rmdir** 删除 /home/denise/krsort.dir.new

