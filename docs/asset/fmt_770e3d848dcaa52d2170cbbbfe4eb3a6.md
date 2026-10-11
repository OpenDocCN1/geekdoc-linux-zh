
```
/Intro_to_UNIX/chap04$ tail
total 36
rw-r--r-- 1 book 403 Feb 11 20:42 README
drwxr-xr-x 6 book 4096 Feb 11 20:42 courses
drwxr-xr-x 2 book 4096 Feb 10 18:00 examples
rw-r--r-- 1 book 3543 Feb 25 14:52 full_listing
drwxr-xr-x 1 book 40 Feb 11 20:42 greeting
drwxr-xr-x 2 book 4096 Feb 11 20:42 misc_files
rw-r--r-- 1 book 171 Feb 11 20:42 notes
drwxr-xr-x 2 book 4096 Feb 11 20:42 sample_home_dir
drwxr-xr-x 4 book 4096 Feb 11 20:42 work
```

图 4.33 使用 `tail` 查看文件的前几行。

```
/Intro_to_UNIX/chap04$ head -5
total 36
rw-r--r-- 1 book 403 Feb 11 20:42 README
drwxr-xr-x 6 book 4096 Feb 11 20:42 courses
drwxr-xr-x 2 book 4096 Feb 10 18:00 examples
rw-r--r-- 1 book 3543 Feb 25 14:52 full_listing
```

图 4.34 使用 `tail` 查看文件的最后几行。

```
/Intro_to_UNIX/chap04$ tail -5
total 36
drwxr-xr-x 2 book 4096 Feb 11 20:42 sample_home_dir
drwxr-xr-x 4 book 4096 Feb 11 20:42 work
```

# 86 UNIX/Linux 简介

```
//Intro_to_UNIX/chap04 echo "Hello, how are you?" > mymyfile
//Intro_to_UNIX/chap04$ cat mymyfile
Hello, how are you?
//Intro_to_UNIX/chap04$
```

图 4.37 利用 `echo` 创建文件。

请注意，如果你以这种方式使用 `echo` 命令指定一个已存在的文件，那么你在双引号中指定的内容将覆盖（或擦除）之前文件的内容。相反，如果你想保留文件的内容并在文件末尾输入信息，请使用 `echo` 的变体并配合 `>>` 运算符。（注意使用的是 `>` 和 `>>` 而不是一个）。第 5 章将更详细地解释 `>` 和 `>>` 的用法。

![](img/e3ac56d195b48617d5ae42cd57458af3_97_0.png)

在使用 `echo` 或任何其他跟随文件名的 `>` 命令时，请小心，因为该命令将覆盖该文件中的任何现有内容。然而，它会将内容添加到现有内容的末尾。

图 4.38 展示了如何使用 `>>` 发出 `echo` 命令。在这里，追加“I am fine”，然后显示其所有内容，其中包含原始内容和刚刚添加的内容。

```
//Intro_to_UNIX/chap04 echo "I am fine" >> mymyfile
//Intro_to_UNIX/chap04$ cat myfile
Hello, how are you
I am fine
//Intro_to_UNIX/chap04$
```

图 4.38 使用 `echo` 向现有文件添加（追加）内容。

创建文件的第三种方法涉及使用文件编辑器。通过这种方式，你可以创建一个包含所需内容的文件，甚至可以编辑这些内容。第 7 章解释了 UNIX 系统中一些常用编辑器的用法。

## 创建目录

当你向主目录创建并添加新文件时，你可能希望通过子目录来组织你的文件。为了方便使用子目录组织，UNIX/Linux 提供了根据需要创建或删除子目录的命令。你可以使用 `mkdir`（make directory）命令，后跟一个或多个子目录名称来创建子目录。

为了演示创建子目录，在当前工作目录 `-/Intro_to_UN/chap04` 中，按照图 4.39 所示的命令创建一个名为 `examples` 的子目录。该子目录将用于接下来的一些示例。在创建子目录之前列出该目录以显示其效果。

```
//Intro_to_UN/chap04 ls
README examples myfile notes work
courses full_listing misc_files mytouch sample_home_dir
//Intro_to_UN/chap04 mkdir examples
//Intro_to_UN/chap04 ls
README examples full_listing misc_files mytouch sample_home_dir
courses examples1 greeting myfile notes work
//Intro_to_UN/chap04
```

图 4.39 创建子目录。

为了证明你可以一次创建任意数量的子目录，请再创建三个子目录：`examples2`、`examples3` 和 `examples4`，并列出当前工作目录查看它们，如图 4.40 所示。

```
//Intro_to_UN/chap04 mkdir examples2 examples3 examples4
//Intro_to_UN/chap04 ls
README examples1 examples4 misc_files notes
courses full_listing myfile sample_home_dir
examples examples3 greeting mytouch work
//Intro_to_UN/chap04
```

图 4.40 创建多个子目录。

## 删除空目录

作为组织文件和子目录的一部分，你有时需要删除目录。为了完成此操作，你可以利用 UNIX/Linux 的 `rmdir`（for remove directory）命令来删除空子目录。为了演示，利用图 4.41 所示的 `rmdir` 来删除刚刚创建的 `examples4` 子目录。与 `mkdir` 类似，你可以用 `rmdir` 指定多个子目录，以便一次性删除你想要的任意数量的空子目录。

```
//Intro_to_UN/chap04 rmdir examples4
//Intro_to_UN/chap04 ls
README examples1 full_listing myfile sample_home_dir
courses examples2 greeting mytouch work
examples examples3 misc_files notes
//Intro_to_UN/chap04
```

图 4.41 删除空子目录。

作为安全措施，`rm` 仅删除空子目录，这样你就不会意外删除子目录内可能存在的任何文件或子目录。有一种方法可以删除包含文件和/或其他子目录的目录，即使用另一个工具 `rm`，它将在本章稍后讨论。

## 复制文件和目录

有时，你可能想要创建一个文件的副本。例如，你可能想要一个文件的工作副本，并将其作为创建和编辑新文件的基础。在这种情况下，你可以将原始文件内容复制到新文件中并修改新文件，同时保持原始完整。

另一个原因是，修改某些文件（特别是重要的文件）时，你可能希望先创建一个文件的备份，以便在必要时参考原始内容。虽然这种备份方法是有效的，但其他复杂的备份技术将在第 5 章解释。

要复制文件，请使用 UNIX/Linux 的 `cp`（copy 的缩写）命令。在最形式的形式，`cp` 接受两个参数：原始或源文件，随后是生成的副本或目标文件。为了演示，假设你想为文件 `notes` 创建备份，并将备份文件命名为 `notes.bak`。如图 4.42 所示，你可以将源文件名和目标文件名作为 `cp` 的两个参数。图 4.42 还列出了当前目录以显示复制的效果，即文件 `notes.bak` 的存在。

```
//Intro_TO_UNIX/chap04$ cp notes.bak
//Intro_TO_UNIX/chap04$ ls
README example1 full_listing myfile notes.bak
courses example2 greeting sample_home_dir
examples example3 misc_files notes work
//Intro_TO_UNIX/chap04$ _
```

图 4.42 复制文件。
