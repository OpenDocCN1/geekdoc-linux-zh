
```
[root@server1 root]# pwd
/root
[root@server1 root]# ls -l
total 548
lrwxrwxrwx 1 root root     9 Apr  7 09:56 current -> project12
drwx------ 3 root root  4096 Mar 29 10:01 Desktop
-rwxr-xr-x 1 root root 519964 Apr  7 09:59 myprogram
-rwxr-xr-x 1 root root     20 Apr  7 09:58 myscript
-rw-r--r-- 1 root root     71 Apr  7 09:58 project
-rw-r--r-- 1 root root     71 Apr  7 09:59 project1
-rw-r--r-- 1 root root     71 Apr  7 09:59 project12
-rw-r--r-- 1 root root      0 Apr  7 09:56 project13
-rw-r--r-- 1 root root     71 Apr  7 09:59 project2
-rw-r--r-- 1 root root     90 Apr  7 10:01 project3
-rw-r--r-- 1 root root     99 Apr  7 10:01 project4
-rw-r--r-- 1 root root    108 Apr  7 10:01 project5
[root@server1 root]#
```

在前面的示例中列出的每个文件都有八个信息组件，按从左到右的列列出：

- **文件类型字符**
  - `d` 字符代表目录。
  - `l` 字符代表符号链接文件（在第 5 章“Linux 文件系统管理”中讨论）。
  - `b` 或 `c` 字符代表特殊设备文件（在第 6 章中讨论）。
  - `n` 字符代表命名管道。
  - `s` 字符代表套接字。
  - `–` 字符代表所有其他文件类型（文本文件、二进制数据文件）。
- 2. 文件的权限列表（也称为文件的模式）
- 3. 硬链接计数（在第 5 章中讨论）
- 4. 文件的所有者（在第 5 章中讨论）
- 5. 文件的所有组（在第 5 章中讨论）
- 6. 文件大小
- 7. 文件的最近修改时间
- 8. 文件名（某些文件是通往其他文件的快捷方式或指针，如前述输出中名为 `current` 的文件，使用箭头 `->` 表示；这些被称为符号链接，并在第 5 章中讨论）

对于前面示例中名为 `project` 的文件，你可以看到，由于该文件的长列表以 `-` 字符开头，因此它是一个常规文件；该文件的权限为 `rw-r--r--`，硬链接计数为 1，文件的所有者是 `root` 用户，文件的所有组是 `root` 组，文件大小为 71 字节，且该文件最近一次修改时间为 4 月 7 日上午 9:58。

#### 注意

> 在大多数 Linux 系统中，可以使用 `ls` 命令的快捷方式来显示与 `ls -l` 命令相同的列信息。一些用户更喜欢使用这种快捷方式，通常称为别名，当用户在命令提示符下输入 `ll` 时调用。这被称为 `ll` 命令。

`ls -F` 和 `ls -1` 命令对于希望显示文件类型的用户很有价值；然而，这两个命令都无法使用特殊字符显示所有文件类型。要显示任何文件的文件类型，你可以使用 `file` 命令；只需给 `file` 命令提供一个参数，指定要分析的文件。你也可以将多个文件作为参数传递，或使用 `*` 元字符来表示当前目录中的所有文件。在 `root` 用户的家庭目录中使用 `file` 命令的示例如下：

```
[root@server1 root]$ pwd
/root
[root@server1 root]$ ls
current myprogram project project2 project3 project4
Desktop myscript project1 project3 project4 project5
[root@server1 root]$ file Desktop
Desktop: directory
[root@server1 root]$ file project Desktop
project:    ASCII text
Desktop:    directory
[root@server1 root]$ file *
Desktop:    directory
current:     symbolic link to project12
myprogram: ELF 32-bit LSB executable, Intel 80386, version 1, dynamically linked (uses shared libs), stripped
myscript:    Bourne-Again shell script text executable
project:     ASCII text
project1:    ASCII text
project12:   ASCII text
project13: empty
project2:    ASCII text
project3:    ASCII text
project4:    ASCII text
project5:    ASCII text
[root@server1 root]#
```

如前述示例所示，`file` 命令还可以识别不同可执行文件类型之间的差异。`myscript` 文件是一个包含可执行命令的文本文件（也称为 shell 脚本），而 `myprogram` 文件是一个编译后的 32 位可执行程序。`file` 命令还能识别像前一个示例中的 `project13` 这样的空文件。

每个用户家庭目录中的一些文件名代表重要的配置文件或程序目录。由于这些文件很少由用户编辑，并且可能会使文件列表杂乱无章，因此在使用 `ls` 和 `file` 命令时，它们通常会被隐藏。请记住，隐藏文件的文件名以点字符（`.`）开头。要查看它们，只需将 `-a` 选项传递给 `ls` 命令。`root` 用户家庭目录中常见的几个隐藏文件如下所示：

```
[root@server1 root]# ls
current  myprogram  project    project12  project2  project4
Desktop  myscript   project1   project13  project3  project5
[root@server1 root]# ls -a
.                        .gimp-1.2            project
..                       .gnome               project1
.bash_history           .gnome-desktop      project12
.bash_logout            .gnome_private      project13
.bash_profile           .gtkrc               project2
.bashrc                 .ICAuthority        project3
.cshrc                  .kde                 project4
current                  .moc                 project5
.DCOP_server_server1_0  .DCOP-random-seed  .sane
Desktop                  .mocpp               .sawfish
.first_start_kde         .mozilla             .tcshrc
.galeon                  myprogram            .Xauthority
.gconf                  myscript             .Xresources
.gconfd                 .nautilus          .xsession-errors
[root@server1 root]#
```

#### 查看文件和目录

如前所述，`.` 字符指的是当前工作目录，而 `..` 字符指的是相对于你在目录树中当前位置的父目录。在使用 `ls -a` 命令时，每个这样的指针都被视为一个特殊（或虚构的）文件，因为每个都以点开头。

你通常可以在命令行上为大多数命令同时指定多个选项，从而获得所有选项的组合功能。例如，要查看所有隐藏文件及其文件类型，你可以输入：
