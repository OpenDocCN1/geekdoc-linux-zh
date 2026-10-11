
## 管理文件和目录

如前所述，使用 Linux 系统需要在多个目录之间导航并操作其中的文件。因此，高效的 Linux 用户必须了解如何按需创建目录、将文件或目录从一个位置复制或移动到另一个位置，以及删除文件和目录。这些任务通常被称为文件管理任务。

以下是在用户以 root 用户身份登录时目录列表的示例：

```
[root@server1 root]# pwd
/root

[root@server1 root]# ls -F
current@  myprogram*  project  project12  project2  project4
Desktop/  myscript  project1  project13  project3  project5
[root@server1 root]#
```

如上所示的输出中，只有一个目录（Desktop）、两个可执行文件（myprogram 和 myscript）以及几个项目相关文件（project*）存在。虽然这种目录结构并不杂乱，且在终端屏幕上以易于阅读的格式显示，但 Linux 系统上的典型主目录包含更多的文件；典型的 Linux 用户在其主目录中可能有超过 100 个文件。因此，根据文件用途将这些文件组织到子目录中是一个良好的实践。由于前面的输出中 root 用户的主目录下有几个项目文件，你可以创建一个名为 proj_files 的子目录来存放项目相关文件，从而减少目录列表的大小。为此，你需要使用 **mkdir（创建目录）命令**，该命令接受指定要创建的目录的绝对或相对路径名的参数。要在当前目录下方创建 proj_files 目录，你可以使用带有相对路径名的 mkdir 命令：

```
[root@server1 root]# mkdir proj_files
[root@server1 root]# ls -F
current@  myprogram*  project  project12  project2  project4  proj_files/
Desktop/  myscript*  project1  project13  project3  project5
[root@server1 root]#
```

现在，你可以使用 **mv（移动）命令** 将项目文件移动到 proj_files 子目录中。mv 命令至少需要两个参数：**源文件/目录和目标文件/目录**。如果需要移动多个文件，只需指定多个源参数；最后一个参数将成为目标目录。源和目的地都可以是绝对或相对路径名，如果移动多个文件，源还可以包含通配符。例如，要将所有项目文件移动到 proj_files 目录，你可以输入 mv 命令，源参数为 project*（以匹配所有以“project”开头的文件），目标参数为 proj_files（指向目标目录的相对路径名），如下面的输出所示：

```
[root@server1 root]# mv project* proj_files
[root@server1 root]# ls -F
current@  Desktop/  myprogram*  myscript*  proj_files/
[root@server1 root]# ls -F proj_files
project project1 project12 project13 project2 project3 project4 project5
[root@server1 root]#
```

在上面的输出中，当前目录列表不再显示项目文件，而 proj_files 子目录的列表表明它们已成功移动。

![](img/09bf13b782f71165e17bb3839040c96a_181_0.png)

如果目标是目录的名称，mv 命令会将这些文件移动到该目录。如果目标是某个目录中现有文件的文件名，且只有一个源文件，则 mv 命令会用源文件覆盖目标文件。如果目标是某个目录中不存在的文件的文件名，则 mv 命令会在目标目录中创建一个具有该文件名的新文件，并将源文件移动到该文件。

mv 命令的另一个重要用途是重命名文件，这仅仅是将文件移动到同一目录但使用不同的文件名。要将前面示例中的 myscript 文件重命名为 myscript2，你可以使用以下 mv 命令：

```
[root@server1 root]# ls -F
current@ Desktop/ myprogram* myscript* proj_files/
[root@server1 root]# mv myscript myscript2
[root@server1 root]# ls -F
current@ Desktop/ myprogram* myscript2* proj_files/
[root@server1 root]#
```

类似地，mv 命令也可以重命名目录。如果源是现有目录的名称，它将被重命名为指定为目标的那个目录名称。

mv 命令的工作方式类似于“剪切和粘贴”操作，即文件被复制到新目录并从源目录中删除。然而，有时需要保留源目录中的文件；这被称为复制文件，可以使用 cp（复制）命令来完成。与 mv 命令类似，cp 命令至少需要两个参数。第一个参数指定要复制的源文件/目录，第二个参数指定目标文件/目录。如果需要将多个文件复制到目标目录，只需指定多个源参数，命令行的最后一个参数将成为目标目录。每个参数都可以是绝对或相对路径名，并且可以包含通配符或特殊元字符“.”（表示当前目录）和“..”（表示父目录）。例如，要在当前目录（/root）中复制 /etc/hosts 文件的副本，你可以指定 /etc/hosts 文件的绝对路径名（/etc/hosts）以及指示当前目录的相对路径名（.）：

```
[root@server1 root]# cp /etc/hosts .
[root@server1 root]# ls -F
current@ Desktop/ hosts myprogram* myscript2* proj_files/
[root@server1 root]#
```

你也可以在相同目录中创建文件的副本。要在当前目录中创建名为 hosts2 的 hosts 文件的副本，请键入以下命令：

```
[root@server1 root]# cp hosts hosts2
[root@server1 root]# ls -F
current/  Desktop/  hosts  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]#
```

除了用途之外，mv 和 cp 命令之间的一个显著区别在于它们对目录的处理方式不同。mv 命令只是重命名目录，而 cp 命令会创建目录及其内容的完整新副本。要在 Linux 中复制整个充满文件的目录，你必须告诉 cp 命令该复制将是**递归**的（涉及文件和子目录），方法是使用 -r 选项。以下示例演示了复制 proj_files 目录及其所有内容到 /home/user1 目录，分别使用和不使用 -r 选项：

```
[root@server1 root]# ls -F
current/  Desktop/  hosts  myprogram*  myscript2*  proj_files/
[root@server1 root]# ls -F /home/user1
Desktop/
[root@server1 root]# cp proj_files /home/user1
cp: omitting directory `proj_files'
[root@server1 root]# ls -F /home/user1
Desktop/
[root@server1 root]# cp -r proj_files /home/user1
[root@server1 root]# ls -F /home/user1
Desktop/  proj_files/
[root@server1 root]#
```

在复制或移动文件时，如果目标是一个存在的文件，mv 和 cp 命令会警告用户目标文件将被覆盖，并询问是否继续。这不是命令通常调用时的功能，而是 Red Hat Linux 中默认配置的功能，因为 Red Hat Linux 中的 BASH shell 包含了指向 cp 和 mv 命令的别名。

> **注意**
> 
> 别名是内存中指向命令的特殊变量；关于它们的完整讨论请参见第 8 章，“使用 BASH Shell”。

当你键入 mv 时，实际上运行的是带有 -i 选项的 mv 命令，该选项交互式地提示用户选择如果目标文件在执行命令时已经存在，是否要覆盖现有文件；这被称为**交互模式**。类似地，当你键入 `cp` 命令时，运行的是 `cp -i` 命令，以执行相同的功能。要查看当前 shell 中存在的别名，只需键入 `alias`，如下面的输出所示：

```
[root@server1 root]# alias
alias cp='cp -i'
alias l='\ls -d . --color=tty'
alias ll='\ls -l --color=tty'
alias ls='\ls --color=tty'
alias mc='../usr/share/mc/bin/mc-wrapper.sh'
alias mv='mv -i'
alias rm='rm -i'
alias vi='vim'
alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --show-tilde'
[root@server1 root]#
```

如果你想覆盖这种交互式选项，可以使用 `-f`（强制）选项来覆盖选择，如下面的示例中 root 用户尝试将 hosts 文件重命名为已存在的 hosts2 文件，分别使用和不使用 `mv` 命令的 `-f` 选项：

```
[root@server1 root]# ls -F
current@  Desktop/  hosts  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]# mv hosts hosts2
mv: overwrite 'hosts2'? n
[root@server1 root]# mv -f hosts hosts2
[root@server1 root]# ls -F
current@  Desktop/  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]#
```

创建目录、复制和移动文件是保留或创建硬盘数据的管理文件任务。要删除文件或目录，你必须使用 `rm` 命令或 `rmdir` 命令。

`rm`（删除）命令接受一个指定要删除的文件的绝对或相对路径名参数的列表。与大多数命令一样，可以使用通配符来简化指定要删除的多个文件。文件从文件系统删除后，无法恢复。因此，`rm` 命令在 Red Hat Linux 中被别名为带有 `-i` 选项的 `rm` 命令，该选项交互式地提示用户选择是否继续删除。与 `cp` 和 `mv` 命令类似，`rm` 命令也接受 `-f` 选项来覆盖此选择并立即删除文件。下面是一个示例，演示了使用 `rm` 和 `rm -f` 命令删除 current 和 hosts2 文件：

```
[root@server1 root]# ls -F
current@  Desktop/  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]# rm current
rm: remove 'current'? y
```

