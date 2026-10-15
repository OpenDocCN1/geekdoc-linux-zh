
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

如果你想覆盖这种交互式选项，可以使用`-f`（强制）选项来覆盖选择，如下面的示例中`root`用户尝试将`hosts`文件重命名为已存在的`hosts2`文件，分别使用和不使用`mv`命令的`-f`选项：

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

创建目录、复制和移动文件是保留或创建硬盘数据的管理文件任务。要删除文件或目录，你必须使用`rm`命令或`rmdir`命令。

`rm`（删除）命令接受一个指定要删除的文件的绝对或相对路径名参数的列表。与大多数命令一样，可以使用通配符来简化指定要删除的多个文件。文件从文件系统删除后，无法恢复。因此，`rm`命令在`Red Hat Linux`中被别名为带有`-i`选项的`rm`命令，该选项交互式地提示用户选择是否继续删除。与`cp`和`mv`命令类似，`rm`命令也接受`-f`选项来覆盖此选择并立即删除文件。下面是一个示例，演示了使用`rm`和`rm -f`命令删除`current`和`hosts2`文件：

```
[root@server1 root]# ls -F
current@  Desktop/  hosts2  myprogram*  myscript2*  proj_files/
[root@server1 root]# rm current
rm: remove 'current'? y
```

### 删除文件和目录

```bash
[root@server1 root]# rm -f hosts2
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*  proj_files/
[root@server1 root]_
```

要删除目录，可以使用`rmdir`命令；但是，`rmdir`（remove directory）命令只有在目录不包含任何文件时才会将其删除。若要删除目录及其内部的文件，必须使用`rm`命令并指定要删除的是一个包含文件的目录（`-r`）。正如之前所述，在使用`cp`命令复制目录时，需要使用递归选项（`-r`）；同样，若要删除一个装满文件的目录，也可以使用`rm`命令的递归选项（`-r`）。例如，如果`root`用户希望删除`proj_files`子目录及其内部的所有文件，且不希望系统提示确认每个文件的删除，则她必须使用`rm -rf proj_files`命令，如下例所示：

```bash
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*  proj_files/
[root@server1 root]# rmdir proj_files
rmdir: `proj_files': Directory not empty
[root@server1 root]# rm -rf proj_files
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*
[root@server1 root]_
```

> **提示**
>
> 在大多数命令中，例如`rm`和`cp`，`-r`和`-R`选项的含义相同（递归）。
>
> **注意**
>
> 如果对要递归删除的目录中实际存在哪些文件不确定，`rm`命令的`-r`选项非常危险。因此，`rm`命令的`-r`选项常被称为`-resumé`选项；如果你误用该选项，可能需要准备你的简历了。

需要注意的是，前述的文件管理命令被 Linux 用户、开发人员和系统管理员普遍使用。表 5-2 总结了这些常见的文件管理命令。

表 5-2 常见的 Linux 文件管理命令

| 命令 | 描述 |
| :--- | :--- |
| `mkdir` | 创建目录 |
| `rmdir` | 删除空目录 |
| `mv` | 移动/重命名文件和目录 |
| `cp` | 复制文件和包含大量文件的目录（配合`-r`选项） |
| `alias` | 显示 `BASH` shell 别名 |
| `rm` | 删除文件和包含大量文件的目录（配合`-r`选项） |

### 查找文件

在使用前一节提到的文件管理命令之前，必须知道所涉及文件的位置。在 Linux 目录树中查找文件最快的方法是使用`locate`命令，它是`slocate`（或 `secure locate`）命令的快捷方式。例如，要查看根目录下所有文件名中包含单词“initab”（作为完整名称或一部分）的文件，只需在命令提示符下输入`locate initab`，其输出如下：

```bash
[root@server1 root]# locate initab
/usr/share/terminfo/a/ansi+initab
/usr/share/vim/vim62/syntax/initab.vim
/usr/share/man/ja/man5/initab.5.gz
/usr/share/man/pl/man5/initab.5.gz
/usr/share/man/it/man5/initab.5.gz
/usr/share/man/man5/initab.5.gz
/usr/share/man/fr/man5/initab.5.gz
/usr/share/man/ko/man5/initab.5.gz
/etc/initab
[root@server1 root]# _
```

通常情况下，`locate`命令返回的信息量过大，无法在屏幕上完全显示，因为它搜索的是文件系统上的所有文件。通常，可以使用`more`（或`less`）命令来暂停输出，例如`locate initab | more`，或者确保被搜索的单词非常具体。`locate`命令在一个预制的数据库中查找，该数据库包含系统上所有文件的列表。这个数据库的索引方式类似于教科书，以便于快速搜索，但随着文件的添加和移除（这是经常发生的情况），数据库可能会变得过时。因此，`locate`命令使用的数据库（`/var/lib/locate/locate.db`）每天会自动更新，也可以在命令提示符下通过运行`updatedb`或`slocate -u`命令手动更新。

一种较慢但更通用的文件定位方法是在文件系统上使用`find`命令。`find`命令不使用预制的文件索引，而是从特定目录开始，递归搜索目录树以找到满足特定条件的文件。`find`命令的格式如下：

```text
find <起始目录> -条件 <要查找的内容>
```

例如，要在`/etc`目录下方查找名为"inittab"的任何文件，可以使用命令`find /etc -name inittab`，输出如下：

```bash
[root@server1 root]# find /etc -name inittab
/etc/inittab
[root@server1 root]# _
```

也可以将通配符元字符与`find`命令一起使用；但是，这些通配符必须受到保护，以免被 shell 解释，因为它们只能由`find`命令解释。为此，确保任何通配符元字符都包含在引号字符内。以下是使用`find`命令配合通配符元字符查找`/etc`目录下所有以"host"开头的文件的示例输出：
