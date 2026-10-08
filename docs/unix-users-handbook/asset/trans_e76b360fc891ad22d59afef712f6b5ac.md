

![](img/75f39fc91296b889c0653851accdfd46_155_0.png)

在创建目录 level1 并执行 ls 命令后，我们可以看到 level2 确实位于 level1 之下，而 level3 位于 level2 之下。

![](img/75f39fc91296b889c0653851accdfd46_155_1.png)

### mkdir - 创建指定的目录。

选项：
- -m 指定目录的模式（权限）。
- -p 创建中间目录以实现完整路径。如果您想创建多层目录，请使用 **-p**。

## rm

![](img/75f39fc91296b889c0653851accdfd46_155_2.png)

**rm** 命令用于从目录中删除一个或多个文件，也可以用于删除目录本身。回顾我们之前关于权限的讨论，您必须对目录拥有 *写入* 和 *执行* 权限，才能从中删除文件。如果您拥有要删除文件所在的目录的所有权，那么您通常可以从中删除文件。但是，如果您对目录没有适当的权限，则**删除**文件会失败。

与我们之前介绍的其他一些命令类似，您可以使用 **-i** 选项，该选项会在删除每个文件时要求您进行确认。这意味着，如果您被询问是否确实要删除某个文件并回答 *n*，则该文件不会被删除。如果您回答 *y*，则文件会被删除。

您还可以使用 **-r**（或 **-R**）选项递归删除目录的内容，然后删除目录本身。这意味着您可以递归删除指定的文件和目录。如果您心中对是否要递归删除文件和目录有任何疑问，请结合使用 **-i** 选项和 **-r**。

您可以使用 -f 选项来删除文件和目录，该选项在执行删除操作时不会要求您进行确认。

以下示例对目录 **krsort.dir.new** 执行长列表显示，交互式地提示用户查看他或她是否想要删除该目录中的文件，然后再次列出该目录的内容，显示所有文件均未删除，因为用户回答了 *n*：

```
$ ls -l krsort.dir.new
total 168
-rwxr-xr-x 1 denise users 34592 Oct 27 18:44 krsort
-rwxr-xr-x 1 denise users 3234 Oct 27 18:46 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 27 18:46 krsort.dos
-rw-r---- 1 denise users 9922 Oct 27 18:46 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 27 18:46 krsortorig.c
$ rm -i krsort.dir.new/*
../krsort.dir.new/krsort: ? (y/n) n
../krsort.dir.new/krsort.c: ? (y/n) n
../krsort.dir.new/krsort.dos: ? (y/n) n
../krsort.dir.new/krsort.q: ? (y/n) n
../krsort.dir.new/krsortorig.c: ? (y/n) n
$ ls -l krsort.dir.new
total 168
-rwxr-xr-x 1 denise users 34592 Oct 27 18:44 krsort
-rwxr-xr-x 1 denise users 3234 Oct 27 18:46 krsort.c
-rwxr-xr-x 1 denise users 32756 Oct 27 18:46 krsort.dos
-rw-r---- 1 denise users 9922 Oct 27 18:46 krsort.q
-rwxr-xr-x 1 denise users 3085 Oct 27 18:46 krsortorig.c
$
```

请注意，对于是否应删除文件的询问，所有情况下的回答都是 *n*。这意味着没有文件被移除。对任何问题的 *y* 回答都会导致该文件从目录中被移除。要交互式删除目录，请结合使用 **rm** 命令的选项 *-i* 和 *-r*。但是，如果您没有删除目录中的每个文件，在使用 *-i* 选项时，该目录不会被移除。以下示例的第一部分显示了从目录 **krsort.dir.new** 中移除了除 **krsort** 文件之外的所有文件。由于该文件仍然存在，目录未被删除。当在此示例的第二部分中删除该文件时，目录本身随后被删除：

![](img/75f39fc91296b889c0653851accdfd46_157_0.png)

![](img/75f39fc91296b889c0653851accdfd46_157_1.png)

```
$ rm -ir krsort.dir.new
directory krsort.dir.new: ? (y/n) **y**
krsort.dir.new/krsort: ? (y/n) **n**
krsort.dir.new/krsort.c: ? (y/n) **y**
krsort.dir.new/krsort.dos: ? (y/n) **y**
krsort.dir.new/krsort.q: ? (y/n) **y**
krsort.dir.new/krsortorig.c: ? (y/n) **y**
krsort.dir.new: ? (y/n) **y**
rm: directory krsort.dir.new not removed.  Directory not
empty
```

```
$ rm -ir krsort.dir.new
directory krsort.dir.new: ? (y/n) **y**
krsort.dir.new/krsort: ? (y/n) **y**
krsort.dir.new: ? (y/n) **y**
$ 
```

**rm** - 删除文件和目录。

选项：
- -i		交互式删除，提示您确认是否要删除现有文件。
- -f		强制删除文件。
- -r (-R)	递归删除目录内容，然后删除目录本身。

## rmdir

![](img/75f39fc91296b889c0653851accdfd46_157_2.png)

![](img/75f39fc91296b889c0653851accdfd46_157_3.png)

**rmdir** 命令用于删除一个或多个目录。目录必须是空的才能被删除。您也可以指定要删除的多个目录。回顾我们之前关于权限的讨论，您必须对被删除目录的父目录拥有 *写入* 和 *执行* 权限，才能删除该目录。

与我们之前介绍的其他一些命令类似，您可以使用 **-i** 选项，该选项会在删除每个目录时要求您进行确认。这意味着，如果您被询问是否确实要删除某个目录并回答 *n*，则该目录不会被删除。如果您回答 *y*，则目录会被删除。

您指定要删除目录的顺序很重要。如果您要删除一个目录及其子目录，必须先指定要删除的子目录。如果您先指定要删除父目录而不是其子目录，父目录的删除操作将失败，因为它不是空的。

您可以使用 **-f** 选项强制删除目录，该操作在执行删除时 *不会* 要求您进行确认。

以下示例对目录 **krsort.dir.new** 执行长列表显示，表明该目录中包含一个名为 **.dotfile** 的文件。当我们试图使用 **rmdir** 删除该目录时，会显示一条消息，告知我们该目录不是空的。该目录中的文件 **.dotfile** 阻止了 **rmdir** 命令删除 **krsort.dir.new**。在删除 **.dotfile** 后，我们便可以使用 **rmdir** 删除该目录：

```
$ ls -al ../krsort.dir.new
total 4
drwxr-x-x 2 denise users 1024 Oct 27 18:57 .
drwxrwxr-x 4 denise users 1024 Oct 27 18:40 ..
-rw-r--r- 1 denise users 0 Oct 27 18:56 .dotfile
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
rmdir: ../krsort.dir.new: Directory not empty
$ rm ../krsort.dir.new/.dotfile
$ rmdir -i ../krsort.dir.new
../krsort.dir.new: ? (y/n) y
$
```

**rmdir** 现在已成功删除了 **krsort.dir.new**，**.dotfile** 也已被移除：

![](img/75f39fc91296b889c0653851accdfd46_158_0.png)

![](img/75f39fc91296b889c0653851accdfd46_158_1.png)

![](img/75f39fc91296b889c0653851accdfd46_159_0.png)

### rmdir - 删除目录。

选项：
- -i	交互式删除，提示您确认是否要删除目录
- -f	强制删除目录。
- -p	如果删除目录后，父目录为空，则也将其删除。此操作将持续进行，直到遇到一个不为空的父目录为止。

## 使用命令

### 使用 cd, pwd, ls, mkdir, 和 cp 命令

既然我们已经“孤立”地介绍过其中一些命令，让我们把一些命令组合起来使用。

![](img/75f39fc91296b889c0653851accdfd46_159_1.png)

让我们从查看 *denise* 主目录下名为 **krsort.dir.old** 的目录层次结构开始，如 3-7 图所示：

![](img/75f39fc91296b889c0653851accdfd46_159_2.png)

```
$ cd /home/denise/krsort.dir.old
$ pwd
/home/denise/krsort.dir.old
$ ls -1
total 168
-rw-r--x     1 denise     users        34592 Oct 27 18:20 krsort
-rwxr-xr-x     1 denise     users         3234 Oct 27 17:30 krsort.c
-rwxr-xr-x     1 denise     users        32756 Oct 27 17:30 krsort.dos
-rw-r--     1 denise     users         9922 Oct 27 17:30 krsort.q
-rwxr-xr-x     1 denise     users         3085 Oct 27 17:30 krsortorig.c
```

![](img/75f39fc91296b889c0653851accdfd46_159_3.png)

