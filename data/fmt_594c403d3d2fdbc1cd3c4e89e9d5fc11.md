
在使用 `rm` 指定要删除的文件时要小心。虽然删除文件是必要的，但在 UNIX/Linux 中没有标准的“删除”或“回收站”功能可以撤销文件删除。因此，请确保你指定了实际要删除的文件。

你可以使用前面描述的通配符指定要删除的文件名或文件名。为了演示这一点，首先如图 4.51 所示创建空文件。

```
//Intro_to_UNIX/chap04$ pwd
/home/book/Intro_to_UNIX/chap04
//Intro_to_UNIX/chap04$ cd examples3
//Intro_to_UNIX/chap04$ ls
newnotes.bak othernotes.bak
//Intro_to_UNIX/chap04$ rm newnotes.bak
//Intro_to_UNIX/chap04$ ls
othernotes.bak
//Intro_to_UNIX/chap04$ rm othernotes.bak
```

```
//Intro_to_UNIX/chap04$ pwd

/home/book/Intro_to_UNIX/chap04/examples3

//Intro_to_UNIX/chap04/examples3$ touch file1 file2 file3 file4 file5 file6 newnotes.bak

//Intro_to_UNIX/chap04/examples3$ ls

file1 file2 file3 file4 file5 file6 newnotes.bak

//Intro_to_UNIX/chap04/examples3$ []
```

**图 4.51** 为删除创建空文件。

使用共同名称“file”和针对 1、3、6 的通配符删除 `file1`、`file2`、`file3` 和 `file6`。图 4.52 演示了这种删除形式并显示了效果。

```
//Intro_to_UNIX/chap04/examples3$ rm file[136]

//Intro_to_UNIX/chap04/examples3$ ls

file4 file5 newnotes.bak

//Intro_to_UNIX/chap04/examples3$ []
```

**图 4.52** 使用通配符范围删除多个文件。

图 4.53 显示了你如何使用多重通配符在共同短语“notes”的前后删除 `newnotes` 和 `newnotes.bak` 文件。

```
//Intro_to_UNIX/chap04/examples3$ rm *notes*

//Intro_to_UNIX/chap04/examples3$ ls

file4 file5

//Intro_to_UNIX/chap04/examples3$ []
```

**图 4.53** 使用通配符删除多个文件。

记得 `rmdir` 允许你删除空子目录——即没有文件或子目录的目录。为了防止误删包含其他文件和/或子目录的子目录。如果你确定要删除子目录及其所有内容，UNIX/Linux 允许通过指定 `rm` 的 `-r`（递归选项）来覆盖此保护。这种方法不仅可以轻松删除目录的内容，还可以删除目录本身。

你可以轻松地使用递归方法指定删除一个或多个目录。为了演示，清理当前的 `examples` 并首先删除一个目录 `examples3` 及其内容，如图 4.54 所示。通过显示当前目录、确保你在要删除的目录中，并返回父目录（当前工作目录）。在删除前后列出父目录以说明效果。

```
//Intro_to_UNIX/chap04/examples3$ pwd

/home/book/Intro_to_UNIX/chap04/examples3

//Intro_to_UNIX/chap04/examples3$ ls

file4 file5

//Intro_to_UNIX/chap04/examples3$ cd ..

README examples3 misc_files notes work

courses examples1,bak full_listing mynewfile notes.bak

examples examples2 greeting mytouch sample_home_dir

//Intro_to_UNIX/chap04/examples3$ rm -rf examples3

//Intro_to_UNIX/chap04/examples3$ ls

README examples1 full_listing mynewfile notes.bak

courses examples1,bak greeting mytouch sample_home_dir

examples examples2 misc_files notes-work

//Intro_to_UNIX/chap04/examples3$ []
```

**图 4.54** 删除目录及其内容。

为了显示可以一次删除多个目录，请同时删除 `examples1` 和 `examples2.bak` 子目录，如图 4.55 所示。你也可以将这些子目录指定为 `examples[1-2]`。

```
//Intro_to_UNIX/chap04$ rm -rf examples1 examples2 examples1,bak

//Intro_to_UNIX/chap04/examples3$ ls

README greeting mynewfile notes sample_home_dir

courses full_listing misc_files mytouch notes.bak work

//Intro_to_UNIX/chap04$ []
```

**图 4.55** 删除多个目录及其内容。

## 重命名文件和目录

如果你需要更改文件或目录的名称，可以使用 UNIX/Linux 的 `mv` (move) 命令。为了演示这一效果，创建一个名为 `mv_examples` 的子目录，并将笔记复制到该目录并命名为 `notes.bak`。然后进入该子目录，将文件 `notes.bak` 重命名为 `newname`。最后，列出子目录的内容显示重命名结果。

```
//Intro_to_UNIX/chapter04$ mkdir mv_examples

//Intro_to_UNIX/chapter04$ cp -ip notes mv_examples/notes.bak

//Intro_to_UNIX/chapter04$ cd mv_examples/

//Intro_to_UNIX/chapter04/mv_examples$ ls

notes.bak

//Intro_to_UNIX/chapter04/mv_examples$ mv notes.bak newname

//Intro_to_UNIX/chapter04/mv_examples$ ls

newname

//Intro_to_UNIX/chapter04/mv_examples$ []
```

**图 4.56** 移动和重命名文件。

你也可以使用 `mv` 将一个或多个文件（甚至是目录）移动到另一个目录。要这样做，请指定要移动的文件和或目录的名称，随后是目标目录的绝对或相对路径。图 4.57 展示了这一操作：首先通过将 `newname` 复制为 `newname.bak` 来创建第二个文件。然后你在 `mv_examples` 中创建一个名为 `newdir` 的子目录，并将文件和 `newname.bak` 移动到该子目录。你可能希望执行目录列表操作来显示结果。

```
//Intro_to_UNIX/chapter04/mv_examples$ cp newname, newname.bak

//Intro_to_UNIX/chapter04/mv_examples$ mkdir newdir

//Intro_to_UNIX/chapter04/mv_examples$ ls

newdir newname, newname.bak

//Intro_to_UNIX/chapter04/mv_examples$ mv newname, newname.bak newdir

//Intro_to_UNIX/chapter04/mv_examples$ ls

newdir

//Intro_to_UNIX/chapter04/mv_examples$ ls newdir

newdir newname.bak

//Intro_to_UNIX/chapter04/mv_examples$ []
```
