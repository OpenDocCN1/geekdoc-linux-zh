
除了用途外，`mv` 和 `cp` 命令之间的一个显著区别是它们都可以作用于目录。`mv` 命令仅仅是重命名目录，而 `cp` 命令则会创建目录及其内容的新副本。在 Linux 中复制包含许多文件的目录时，必须使用 `-r` 选项告诉 `cp` 命令将进行递归操作（包含文件和子目录）。以下示例演示了使用 `-r` 选项将 `proj_files` 目录及其所有内容复制到 `/home/user` 目录：

```bash
[root@localhost root]# ls -F

current@ Desktop/hosts myprogram* myscript2* proj_files/

[root@localhost root]# ls -F /home/user

Desktop/

[root@localhost root]# cp proj_files /home/user

cp: omitting directory 'proj_files'
```

# 第 5 章 Linux 文件系统管理

```bash
[root@localhost]# ls -F /home/user

Desktop/

[root@localhost]# cp -r proj_files /home/user

[root@localhost]# ls -F /home/user

Desktop/proj_files/

[root@localhost]# _
```

在复制或移动文件时，如果目标是一个已存在的文件，`mv` 和 `cp` 命令将警告用户文件将被覆盖并询问是否继续。这并不是命令在正常调用时的功能，而是 Red Hat Linux 默认配置的一个特性，在其中 Bash Shell 包含了 `cp` 和 `mv` 命令的别名（aliases）。别名是内存中指向命令的特殊变量；我们将在第 8 章详细讨论它们。当你输入 `mv` 时，你实际上运行的是带有 `-i` 选项的 `mv` 命令，它会在命令执行时目标已存在时交互式地提示用户选择是否覆盖现有文件。同样，当你输入 `cp` 命令时，`cp -i` 命令只是输入了别名。要查看当前 shell 中存在的别名，请看下面的输出：

```bash
[root@localhost]# alias

alias cp='cp -i'

alias ls='ls -d [a-zA-Z]* --color=tty'

alias ll='ls -l --color=tty'

alias ls='ls --color=tty'

alias mv='mv -i'

alias rm='rm -i'

alias which='alias | /usr/bin/which --tty-only --read-alias --show-dot --tilde='

[root@localhost]# _
```

如果你希望覆盖此交互式选项，可以使用 `-f`（强制）选项来覆盖选择，如下例所示，用户尝试将 `hosts` 文件重命名为已存在的 `hosts2`，且没有给 `mv` 命令添加 `-f` 选项：

```bash
[root@localhost]# ls -F

current@ Desktop/ hosts2 myprogram* myscript*

proj_files/ [root@localhost]# mv hosts2

mv: overwrite 'hosts2?' n

[root@localhost]# mv -f hosts2

[root@localhost]# ls -F

current@ Desktop/ hosts2 myprogram* myscript*

proj_files/ [root@localhost]# _
```

创建目录、复制文件和移动文件都是在硬盘上保留或创建数据的文件管理任务。若要删除文件或目录，你必须使用 `rm` 命令或 `rmdir` 命令。

`rm` 命令接受一组参数列表，指定要删除的文件的绝对路径或相对路径。与大多数命令一样，可以使用通配符来简化多个要删除文件的操作。一旦文件从文件系统中删除，它将无法恢复。

# 查找文件 195

```
/usr/lib/linuxconf/help.ro/inittab-msg-1.25r7.ro
/usr/lib/linuxconf/help.ru_SU/inittab-msg-1.25r7.ru_SU
/usr/lib/linuxconf/help.se/inittab-msg-1.25r7.se
/usr/lib/linuxconf/help.sk/inittab-msg-1.25r7.sk
/usr/lib/linuxconf/images/inittab.xpm
/usr/lib/linuxconf/images/mini-inittab.xpm
/usr/lib/linuxconf/install/inittab.redhat-4.0
/usr/lib/linuxconf/install/inittab.debian
/usr/lib/linuxconf/install/inittab.redhat
/usr/lib/linuxconf/modules/so.1.25.7
/usr/share/doc/vim-common-5.8~/syntax/inittab.vim
/usr/share/man/man5/inittab.5gr
/usr/share/terminfo/ansi/inittab
/usr/share/vim/vim58/inittab.vim
/usr/include/linuxconf/module_apis/inittab_apidef.h
/usr/include/linuxconf/module_apis/inittab_api.h
[root@localhost root]#
```

通常情况下，`locate` 命令返回的信息远超屏幕显示范围，因此你可以使用 `more` (less) 命令来暂停输出，例如 `locate inittab | more`，否则你必须确保搜索的词非常具体。

`locate` 命令在预先的数据库中查找，该数据库包含了系统中所有文件的列表。该数据库像教材一样被索引以便快速搜索，但由于文件会被定期索引并从系统中移除，该数据库可能会过期。因此，`locate` 命令的数据库 (`/var/lib/locate/slocate.db`) 每天会自动更新，也可以通过在命令提示符处运行 `updatedb` 或 `locate -u` 命令手动进行更新。

在文件系统中查找文件的另一种较慢但更通用的方法是使用 `find` 命令。`find` 命令会从特定目录开始递归遍历树，查找符合特定标准的文件。`find` 命令的格式为：

```
find <start directory> -criteria <what to find>
```

例如，要在 `/etc` 目录下查找任何名为 `inittab` 的文件，你可以使用命令 `find /etc -name inittab` 并获得以下输出：

```
[root@localhost root]# find /etc -name inittab
/etc/inittab
[root@localhost root]#
```

你也可以在 `find` 命令中使用通配符元字符；然而，通配符必须被 `find` 命令正确解释。为了做到这一点，请确保任何通配符元字符都包含在引号内。以下是使用 `find` 命令配合通配符元字符查找 `/etc` 目录下所有以 `host` 字母开头的文件输出示例：

```
[root@localhost root]# find /etc -name "host*"
/etc/host.conf
/etc/hosts.allow
/etc/hosts.deny
/etc/ups/hosts.conf
/etc/hosts
[root@localhost root]#
```

虽然按名称搜索是 `find` 命令最常用的标准，但还有许多其他标准也可以可以使用。要查找从 `/var` 目录开始的尺寸大于 1024K（字节）的文件，你可以使用以下命令：

```
[root@localhost root]# find /var -size +1024k
/var/lib/rpm/Packages
/var/lib/rpm/Basenames
/var/lib/slocate/slocate.db
/dev/log/cron
/dev/cache/man/whatis
/dev/ftp/lib/libc-2.2.4.so
[root@localhost root]#
```

此外，如果你只想查找 `/dev` 目录下的所有目录，你可以输入以下命令：

```
[root@localhost dev]# find /dev -type d
/dev
/dev/pts
/dev/ataraid
/dev/cciss
/dev/compaq
/dev/dri
/dev/i2o
/dev/ida
/dev/inet
```
