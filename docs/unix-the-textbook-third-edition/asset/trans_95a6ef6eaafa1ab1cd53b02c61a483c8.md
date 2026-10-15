

# 练习 6.4

给出显示 student_records 文件的开头七行和最后七行的命令。

## 6.3 复制、移动和删除文件

在本节中，我们描述了在文件结构中对文件执行复制、移动/重命名和删除/移除操作的命令。讨论的命令是 cp、mv 和 rm。

### 6.3.1 复制文件

UNIX 中复制文件的命令是 cp。以下是该命令的简要说明。

```
SYNTAX
cp [options] file1 file2

Purpose: Copy file1 to file2. If file2 is a directory, make a copy of file1 in this directory.
Commonly used options/features:
-f Force copying if there is no write permission on file2
-i If file2 exists, prompt before overwriting
-p Preserve file attributes such as owner ID, group ID, permissions, and modification times
-r Recursively copy files and subdirectories
```

你必须有读取源文件（file1）的权限，并且有执行（搜索）包含 file1 和 file2 的目录的权限。此外，如果目标目录中尚不存在 file2，你必须对包含 file2 的目录具有写权限。如果 file2 已存在，你不需要对包含它的目录具有写权限，但你必须对 file2 具有写权限。如果目标文件（file2）存在，默认情况下，如果你有权限写入该文件，它将被覆盖而不会通知你。若要在覆盖现有文件前提示你，需要使用 -i 选项。如果你没有权限写入目标文件，你将被告知此事。如果你没有权限读取源文件，屏幕上会出现错误消息。

下面的 cp 命令行将 temp 的副本制作到 temp.bak 中。ls 命令显示了执行 cp 命令前后的当前目录状态。图 6.1 以图形形式显示了相同的信息。

```
$ ls
memo  sample      temp
$ cp temp temp.bak
$ ls
memo  sample      temp  temp.bak
$
```

![](img/02e070097d401d3bf7de4bf1c470b267_258_0.png)

# 图 6.1 temp 文件被复制到 temp.bak 之前和之后的当前目录状态。

如果 temp 不存在或存在但你没有权限读取其内容，命令会返回错误消息。如果 temp.bak 存在且你没有权限写入它，命令也会返回错误消息。下面的会话说明了这些情况。第一个错误消息报告是因为当前目录中不存在 letter 文件。第二个错误消息报告是因为你没有权限读取 sample 文件。最后一个命令报告错误消息是因为 temp.bak 存在且你没有写入权限。你可以通过使用 -f 选项来覆盖缺少写权限的情况，如下一个命令所示。ls -l memo temp.bak 命令用于显示复制确实已发生；也就是说，数据已被复制，但文件的<|message|>
时间戳为当前时间。如果你想同时复制源文件的数据和属性，你需要使用带有 -f 和 -p 选项的 cp 命令，如下面的最后一个 cp 命令所示。最后的 ls -l memo temp.bak 命令用于显示数据和文件属性（如时间戳）都已被复制。

```
% ls -l
total 3
-rw-r----- 1 sarwar faculty 371 Aug 28 07:01 memo
--wxx----- 1 sarwar faculty 164 Jul 25 12:35 sample
-r-xr----- 1 sarwar faculty 792 Aug 28 07:01 temp
-r-xr----- 1 sarwar faculty 792 Aug 28 07:05 temp.bak
% cp letter letter.bak
cp: letter: No such file or directory
% cp sample sample.new
cp: sample: Permission denied
% cp memo temp.bak
cp: temp.bak: Permission denied
% cp -f memo temp.bak
% ls -l memo temp.bak
-rw-r----- 1 sarwar faculty 0 Aug 28 07:01 memo
--wxx----- 1 sarwar faculty 0 Aug 28 07:22 temp.bak
% cp -fp memo temp.bak
% ls -l memo temp.bak
```

```
-rwxr---- 1 sarwar faculty 0 Aug 28 07:01 memo
-rwxr---- 1 sarwar faculty 0 Aug 28 07:01 temp.bak
%
```

下面的命令将你主目录中的 .profile 文件复制到你主目录中的 sys.backups 子目录下的 .profile.old 文件中。此命令无论你在运行命令时所在的目录如何都有效，因为路径名以你的主目录开头。你应该在更改 ~/.profile 文件中指定的运行时环境之前执行此命令，以便在设置新环境时出现问题时，你拥有先前工作环境的备份副本。该命令在 ~/.profile 不存在、你没有权限读取它、~/sys.backups 目录不存在或你没有对其执行（搜索）和写权限、或 .profile.bak 存在但你没有权限读取它时产生错误消息。

```
% cp ~/.profile ~/sys.backups/.profile.bak
%
```

下面的命令将当前目录中以字符串 lab 开头的所有文件复制到 ~/courses/ee446/backups 目录。该命令还会在任何源文件已存在于 backups 目录中时提示你是否覆盖。在这种情况下（复制多个文件），如果 backups 不是目录或不存在，屏幕上会显示错误消息，告知目标必须是目录。

```
% cp -i lab* ~/courses/ee446/backups
%
```

如果你想将完整目录复制到另一个目录，你需要使用带有 -r 选项的 cp 命令。此选项递归地将文件和子目录从源目录复制到目标目录。这是一个有用的选项，你可以用它定期创建重要目录的备份。因此，下面的命令递归地将 ~/courses 目录复制到 ~/backups 目录。

```
$ cp -r ~/courses ~/backups
$
```

此命令创建 ~/courses 目录的副本，包括 ~/courses 目录下的所有文件和目录层次结构，并将其放置在 ~/backups 目录下。图 6.2 显示了执行命令前后你的主目录（~）的状态。

### 6.3.2 移动文件

文件可以从文件结构中的一个目录移动到另一个目录。在 UNIX 中，此操作如果在同一文件系统上，也可能只是重命名文件。重命名

