

该动作是根据系统的消息目录进行解释的，而不是根据 **find** 自身的消息翻译。

TZ

影响 **-printf** 和 **-fprintf** 中某些与时间相关的格式指令所使用的时区。

## BINARIES

findutils 源代码发行版包含两种不同的 **find** 实现。旧版实现递归遍历文件系统，而新版实现使用 **fts(3)**。两者通常都会安装。

如果向 **configure** 传递了选项—**without-fts**，则递归实现被安装为 **find**，而基于 fts 的实现被安装为 **ftsfind**。否则，基于 fts 的实现被安装为 **find**，而递归实现被安装为 **oldfind**。

## EXAMPLES

**find /tmp -name core -type f -print | xargs /bin/rm -f**

在目录 `/tmp` 及其下级目录中查找名为 **core** 的文件并删除它们。请注意，如果文件名中包含换行符、单引号、双引号或空格，此操作将不正确。

**find /tmp -name core -type f -print0 | xargs -0 /bin/rm -f**

在目录 `/tmp` 及其下级目录中查找名为 **core** 的文件并删除它们，并以这种方式处理文件名，使得文件名或目录名中包含单引号、双引号、空格或换行符的情况能够被正确处理。**-name** 测试位于 **-type** 测试之前，以避免对每个文件都调用 **stat(2)**。

**find . -type f -exec file '{}' \;**

对当前目录及其下级目录中的每个文件运行 `file`。请注意，大括号被单引号包围，以保护它们不被解释为 shell 脚本标点符号。分号也通过反斜杠加以保护，尽管在这种情况下也可以使用单引号。

**find / \( -perm -4000 -fprintf /root/suid.txt '%#m %#p\n' \) \( -size +100M -fprintf /root/big.txt '%-10s %p\n' \)**

仅遍历文件系统一次，将 setuid 文件和目录列出到 `/root/suid.txt` 中，将大文件列出到 `/root/big.txt` 中。

**find $HOME -mtime 0**

搜索主目录中在过去二十四小时内被修改过的文件。此命令的工作原理是：将自文件上次修改以来的时间除以 24 小时，并丢弃任何余数。这意味着，为了匹配 **-mtime 0**，文件的修改时间必须少于 24 小时前。

**find /sbin /usr/sbin -executable \! -readable -print**

搜索可执行但不可读的文件。

**find . -perm 664**

搜索所有者和组具有读和写权限，而其他用户只有读权限而没有写权限的文件。如果满足这些标准但设置了其他权限位（例如，如果某人可以执行该文件）的文件，则不会匹配。

**find . -perm -664**

搜索所有者和组具有读和写权限，且其他用户可以读的文件，而不考虑是否存在任何额外的权限位（例如可执行位）。这将匹配例如权限模式为 0777 的文件。

**find . -perm /222**

搜索任何人都可以写（所有者、组或其他任何人）的文件。

**find . -perm /220**

**find . -perm /u+w,g+w**

**find . -perm /u=w,g=w**

这三个命令都做同样的事情，但第一个命令使用文件模式的八进制表示，而其他两个使用符号形式。这些命令都搜索其所有者或组可以写的文件。文件不需要既对所有者又可写又对组可写才能匹配；任意一方可以写即可。

find . -perm -220

find . -perm -g+w,u+w

这两个命令做同样的事情；搜索其所有者和组都可以写的文件。

find . -perm -444 -perm /222 ! -perm /111

find . -perm -a+r -perm /a+w ! -perm /a+x

这两个命令都搜索对每个人都可读（-perm -444 或 -perm -a+r）、至少设置了一个写位（-perm /222 或 -perm /a+w）但对任何人不可执行（分别为 ! -perm /111 和 ! -perm /a+x）的文件。

cd /source-dir

find . -name .snapshot -prune -o \( \! -name *~ -print0 \) | cpio -pmd0 /dest-dir

此命令将 /source-dir 的内容复制到 /dest-dir，但省略名为 .snapshot 的文件和目录（以及它们的内容）。它还省略名称以 ~ 结尾的文件或目录，但不省略它们的内容。结构 -prune -o \( ... -print0 \) 非常常见。这里的想法是，-prune 之前的表达式匹配要修剪的内容。然而，-prune 动作本身返回真，因此后续的 -o 确保仅在那些未被修剪的目录上评估右侧。被修剪目录的内容甚至不会被访问，因此其内容无关紧要。-o 右侧的表达式仅用括号包围以清晰表示。它强调了 -print0 动作仅对未应用 -prune 的对象发生。由于测试之间的默认 `and` 条件绑定比 -o 更紧密，这本来就是默认情况，但括号有助于展示正在发生的事情。

```
find repo/ -exec test -d {}/.svn \; -o \
            -exec test -d {}/.git \; -o \
            -exec test -d {}/CVS \; \
| -print -prune
```

给定以下项目目录及其相关的 SCM 管理目录，执行对项目根目录的高效搜索：

```
repo/project1/CVS
repo/gnu/project2/\.svn
repo/gnu/project3/\.svn
repo/gnu/project3/src/\.svn
repo/project4/\.git
```

在此示例中，-prune 防止不必要地深入已经发现的目录（例如，由于我们已经找到 project3/.svn，所以不再搜索 project3/src），但确保同级目录（project2 和 project3）被发现。

## EXIT STATUS

**find** 如果在所有文件成功处理的情况下以状态 0 退出，如果发生错误则大于 0。这是一个刻意非常宽泛的描述，但如果返回值非零，你不应该依赖 **find** 结果的正确性。

当发生某些错误时，**find** 可能会立即停止，而不完成所有指定的动作。例如，一些起点可能尚未检查，或者一些待执行的 `-exec ... {} +` 或 `-execdir ... {} +` 程序调用可能尚未执行。

## SEE ALSO

+   **locate(1), locatedb(5), updatedb(1), xargs(1), chmod(1), fnmatch(3), regex(7), stat(2), lstat(2), ls(1), printf(3), strftime(3), ctime(3)**

**find** 的完整文档作为 Texinfo 手册维护。如果 **info** 和 **find** 程序在你的站点上正确安装，命令 **info find** 应该能让你访问完整的手册。

## HISTORY

从 findutils-4.2.2 开始，用于文件名模式的 shell 元字符（例如 ‘*’、‘?’ 或 ‘[]’）将匹配前导的 `.`，因为 IEEE POSIX 解释 126 要求如此。

从 findutils-4.3.3 开始，-perm /000 现在匹配所有文件，而不是没有文件。

纳秒级分辨率的时间戳在 findutils-4.3.3 中实现。

从 findutils-4.3.11 开始，当 -delete 动作失败时，它将 find 的退出状态设置为非零值。然而，find 不会立即退出。以前，find 的退出状态不受 -delete 失败的影响。

| 功能 | 添加于 | 也存在于 |
|---|---|---|
| -newerXY | 4.3.3 | BSD |
| -D | 4.3.1 | |
| -O | 4.3.1 | |
| -readable | 4.3.0 | |
| -writable | 4.3.0 | |
| -executable | 4.3.0 | |
| -regextype | 4.2.24 | |
| -exec … + | 4.2.12 | POSIX |
| -execdir | 4.2.12 | BSD |
| -okdir | 4.2.12 | |
| -samefile | 4.2.11 | |
| -H | 4.2.5 | POSIX |
| -L | 4.2.5 | POSIX |
| -P | 4.2.5 | BSD |
| -delete | 4.2.3 | |
| -quit | 4.2.3 | |
| -d | 4.2.3 | BSD |
| -wholename | 4.2.0 | |
| -iwholename | 4.2.0 | |
| -ignore_readdir_race | 4.2.0 | |
| -fls | 4.0 | |
| -ilname | 3.8 | |
| -iname | 3.8 | |
| -ipath | 3.8 | |
| -iregex | 3.8 | |

语法 .B -perm +MODE 已在 findutils-4.5.12 中移除，改为 .B -perm /MODE。+MODE 语法自 2005 年发布的 findutils-4.2.21 起已被弃用。

