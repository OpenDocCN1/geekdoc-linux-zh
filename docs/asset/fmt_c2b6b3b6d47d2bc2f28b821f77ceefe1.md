
如果 `temp` 不存在或存在但你没有权限读取其内容，命令会返回错误消息。如果 `temp.bak` 存在且你没有权限写入它，命令也会返回错误消息。下面的会话说明了这些情况。第一个错误消息报告是因为当前目录中不存在 `letter` 文件。第二个错误消息报告是因为你没有权限读取 `sample` 文件。最后一个命令报告错误消息是因为 `temp.bak` 存在且你没有写入权限。你可以通过使用 `-f` 选项来覆盖缺少写权限的情况，如下一个命令所示。`ls -l memo temp.bak` 命令用于显示复制确实已发生；也就是说，数据已被复制，但文件的时间戳为当前时间。如果你想同时复制源文件的数据和属性，你需要使用带有 `-f` 和 `-p` 选项的 `cp` 命令，如下面的最后一个 `cp` 命令所示。最后的 `ls -l memo temp.bak` 命令用于显示数据和文件属性（如时间戳）都已被复制。

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

下面的命令将你主目录中的 `.profile` 文件复制到你主目录中的 `sys.backups` 子目录下的 `.profile.old` 文件中。此命令无论你在运行命令时所在的目录如何都有效，因为路径名以你的主目录开头。你应该在更改 `~/.profile` 文件中指定的运行时环境之前执行此命令，以便在设置新环境时出现问题时，你拥有先前工作环境的备份副本。该命令在 `~/.profile` 不存在、你没有权限读取它、`~/sys.backups` 目录不存在或你没有对其执行（搜索）和写权限、或 `.profile.bak` 存在但你没有权限读取它时产生错误消息。

```
% cp ~/.profile ~/sys.backups/.profile.bak
%
```

下面的命令将当前目录中以字符串 `lab` 开头的所有文件复制到 `~/courses/ee446/backups` 目录。该命令还会在任何源文件已存在于 `backups` 目录中时提示你是否覆盖。在这种情况下（复制多个文件），如果 `backups` 不是目录或不存在，屏幕上会显示错误消息，告知目标必须是目录。

```
% cp -i lab* ~/courses/ee446/backups
%
```

如果你想将完整目录复制到另一个目录，你需要使用带有 `-r` 选项的 `cp` 命令。此选项递归地将文件和子目录从源目录复制到目标目录。这是一个有用的选项，你可以用它定期创建重要目录的备份。因此，下面的命令递归地将 `~/courses` 目录复制到 `~/backups` 目录。

```
$ cp -r ~/courses ~/backups
$
```

此命令创建 `~/courses` 目录的副本，包括 `~/courses` 目录下的所有文件和目录层次结构，并将其放置在 `~/backups` 目录下。图 6.2 显示了执行命令前后你的主目录（`~`）的状态。

### 6.3.2 移动文件

文件可以从文件结构中的一个目录移动到另一个目录。在 UNIX 中，此操作如果在同一文件系统上，也可能只是重命名文件。重命名

![](img/02e070097d401d3bf7de4bf1c470b267_260_0.png)

图6.2 执行 `cp -r ~/courses ~/backups` 命令前后当前目录的状态

移动操作相当于为文件创建一个硬链接（参见第8章），然后移除/删除（参见6.3.3节）原文件。如果源文件和目标文件位于不同的文件系统上，移动操作会将源文件物理复制到目标位置，然后移除源文件。移动文件的命令是 `mv`。下面是对该命令的简要说明。

```
语法
mv [选项] file1 file2
mv [选项] file-list directory

用途：第一种语法：将 file1 移动到 file2，或将 file1 重命名为 file2
第二种语法：将 file-list 中的所有文件移动到 directory

常用选项/特性：
- -f 忽略目标文件的权限，强制移动
- -i 在覆盖目标文件前提示用户
```

对于包含源文件（描述中的 `file1`）的目录，你必须具有写和执行访问权限，但不需要对该文件本身具有读、写或执行权限。同样，对于包含目标/目的文件（描述中的 `file2`）的目录，你必须具有写和执行权限；对于目标文件路径名中的每个目录，你必须具有执行权限；如果目标文件已存在，你还需要具有写权限。如果目标文件已存在，默认情况下它会直接被覆盖，而不会通知你。如果你使用 `-i` 选项，则在覆盖目标文件之前会提示你。

下面的命令将 `temp` 移动到 `temp.moved`。在这种情况下，`temp` 文件被重命名为 `temp.moved`。如果 `temp` 不存在，或者你对它所在的目录没有执行权限，`mv` 命令会返回一条错误消息。该命令

```
$ mv temp temp.moved
$
```

在 `temp.moved` 已存在而你没有写权限时，会提示你是否移动该文件。

下面的命令将 `temp` 作为 `temp.old` 文件移动到 `backups` 目录。图6.3展示了移动 `temp` 文件前后当前目录的状态。

```
$ mv temp backups/temp.old
$
```

下面的命令是强制移动；无论目标文件 `temp.moved` 的权限如何，你都可以使用它来强制移动。

```
$ mv -f temp temp.moved
$
```

下面的命令将 `dir1` 中的所有文件和目录（不包括隐藏文件）移动到 `dir2` 目录。如果 `dir2` 不是目录、不存在，或者你对它没有写和执行权限，命令会失败，并在屏幕上显示错误消息。

```
$ mv dir1/* dir2
$
```

命令执行后，`dir1` 中只包含隐藏文件。你可以使用 `ls -a` 命令确认 `dir1` 的状态。

![](img/02e070097d401d3bf7de4bf1c470b267_261_0.png)

图6.3 执行 `mv temp backups/temp.old` 命令前后当前目录的状态

## 6.3.3 移除/删除文件

当文件不再需要时，应将它们从文件结构中移除，以释放磁盘空间供新的文件和目录复用。UNIX 中用于移除（删除）文件的命令是 `rm`。下面是对该命令的简要说明。

```
语法
rm [选项] file-list

用途：从文件结构（和磁盘）中移除 file-list 中的文件
常用选项/特性：
- f 无论 file-list 的权限如何，强制移除
- i 在移除 file-list 中的文件之前提示用户
- r 递归移除作为参数传入的目录中的文件。这会移除该目录下的所有内容，因此在使用此选项之前请确保你确实想要这样做。
```

如果 `file-list` 中的文件是路径名，则你需要对路径名中的所有目录组件具有读和执行权限，并且对最后一个目录（包含要删除的文件）具有读、写和执行权限。你还必须对这些文件本身具有写权限，才能在你删除它们时不会提示你。如果你从终端运行该命令，并且对要删除的文件没有写权限，该命令会显示你对文件的访问权限，并提示你确认是否删除它。

```
$ rm temp
$ rm temp backups/temp.old
$ rm -f phones grades ~/letters/letter.john
$ rm ~/dir1/*
$
```

第一条命令从当前目录中移除 `temp`。第二条命令从当前目录中移除 `temp` 文件，并从当前目录的 `backups` 目录中移除 `temp.old` 文件。图6.4展示了该命令的语义。第三条命令移除 `phones`、`grades` 和 `~/letters/letter.john` 文件，无论它们的访问权限如何。第四条命令移除 `~/dir1` 目录中的所有文件，但目录本身不会被移除。
