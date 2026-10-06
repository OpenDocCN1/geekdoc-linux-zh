

-   -s 以 1,024 字节为块显示每个文件的大小。大小位于名称之前。使用 -l 选项时，此选项将大小显示在第 1 列，并将其他所有项向右移动。你可以包含 -h 选项使文件更易读。

--format=word 默认情况下文件按垂直方向排序。此选项根据单词对文件进行排序：跨列 (-x)、逗号分隔 (-m)、水平方向 (-x)、长格式 (-l)、单列 (-n)。

--sort=word 默认按 ASCII 顺序显示文件。此选项根据单词对文件进行排序：文件名扩展名 (-X)、无 (-U)、文件大小 (-S)、访问时间 (-u)、修改时间 (-t)，详情请参见 --time。

--time=word 默认情况下时间是文件的修改时间。将单词设为 atime 以显示访问时间（或使用 -t 选项），或设置为 ctime 以显示创建时间。当您使用 --sort=time 选项时，将按单词列出文件。

ls long (--format=long 或 -l 选项) 显示第 119 页图 4-12 中所示的七列。第一列包含 11 个字符，按照后续段落进行进行划分。第一个字符描述文件类型，如表 III-20 所示。有关文件类型的更多信息，请参考第 103 页和第 968 页。

# 第一个字符

| 第一个字符 | 表 III-20 |
|---|---|
| - | 普通文件 |
| b | 设备 |
| c | 字符设备 |
| d | 目录 |
| p | FIFO（命名管道） |
| l | 符号链接 |

第一列的后续九个字符代表文件相关的所有访问权限。这九个字符分为三组三个字符。

前三个字符代表所有者的访问权限。如果所有者对文件具有读取权限，则第一个位置出现 r。如果不允许所有者读取该文件，则该位置出现连字符 -。接下来的两个位置代表所有者的写入和执行权限。如果允许所有者写入文件，则在第二个位置出现 w，如果允许所有者执行文件，则在第三位置出现 x。第三位置的 s 表示文件设置了权限（setuid/setgid）且具有执行权限。连字符表示所有者不具有与字符位置相关的访问权限。

同样，第二组和第三组三个字符代表用户组和其他用户的访问权限。第二组字符第三位置的 s 表示文件设置了权限且具有执行权限，而 T 表示设置了权限但没有执行权限。

如果设置了粘滞位（sticky bit）且具有执行权限，最后一个字符为 t；如果没有执行权限，则为 T。有关如何更改访问权限的信息，请参考第 1103 页的 chmod。

第二列指示文件的硬链接数。有关链接的更多信息，请参考第 123 页。

第三、四列显示文件所有者的名称和文件所属组的名称。

第五列指示以字节为单位的文件大小，如果显示的是设备文件，则显示大小和次设备号。对于目录，该数字是目录的大小，而不是目录内项文件的大小。（使用 du 显示目录中所有文件的大小和。）包含 -h 选项以千字节、兆字节或吉字节显示文件大小。

最后两列分别显示文件最后修改的日期、时间和文件名。

# 注意事项

参考第 157 页使用 ls 处理模糊文件引用的示例。

通过 --color 选项，ls 可以以不同颜色显示各种类型文件的文件名。默认情况下，可执行文件为绿色，目录文件为蓝色，符号链接为青色，存档和压缩文件为红色，普通文本文件为黑色。ls 为不同文件类型上色的方式在 /etc/DIR_COLORS 文件中指定。如果你的系统中不存在此文件，ls 将不会为文件名上色。你可以修改 /etc/DIR_COLORS 在系统范围内更改默认的颜色/文件类型映射。为了个人使用，你可以将 /etc/DIR_COLORS 复制到主目录下的 ~/.dir_colors 文件并修改 ~/.dir_colors。对于你的登录，~/.dir_colors 会覆盖 /etc/DIR_COLORS 中建立的系统颜色。更多信息请参阅 dir_colors 和 dircolors 手页。

# 示例

第一个命令显示了带有 -x 选项的 ls 实用。你会看到工作目录下文件名的字母顺序列表：

```
$ ls -x
bin c calendar
execute letters shell
```

-F 选项对目录文件显示斜杠 (/)，对可执行文件显示星号 (*)，对符号链接显示 @ 符号 (@)：

```
$ ls -Fx
bin/ c/ calendar
execute* letters/ shell@
```

-l (long) 选项显示长列表。文件仍然按字母排序：

```
$ ls -l
total 8
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
```

-a (all) 选项列出所有文件，包括隐藏文件：

```
$ ls -a
.profile c execute shell
bin calendar shell
```

结合 -a 和 -l 选项显示工作目录下所有文件（包括隐藏文件）的列表列表。此列表仍然按字母排序：

```
$ ls -al
total 12
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .
drwxrwx-- 26 root 816 Jun 6 14:45 ..
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
-rw-r--r 1 jenny pubs 85 May 6 08:27 execute
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
```

当在命令行中添加 -r (reverse) 选项时，ls 会按反字母顺序生成列表：

```
$ ls -alr
total 12
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
```

-rw-rw-r-- 1 jenny pubs 85 May 6 08:27 execute
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrwx-- 26 root 816 Jun 6 14:45 ..
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .

使用 -t -l 选项列出文件，使最近修改的文件位于顶部：

```
drwxrxr-x 16 jenny pubs 1296 Jun 6 17:33 shell
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
```

-rw-rw-r-- 1 jenny pubs 85 May 6 08:27 execute
-rw-r--r 1 jenny pubs 104 May 28 11:44 calendar
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrwx-- 26 root 816 Jun 6 14:45 ..
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .

结合 -r -t 选项将按最不常修改的文件列在列表顶部：

```
drwxrxr-x 2 jenny pubs 32 Oct 6 22:56 letters
```

使用使用 -r -t 选项将文件文件文件的顶部：

```
drwxrxr-x 2 jenny pubs 144 Mar 26 11:59 c
drwxrxr-x 2 jenny pubs 80 May 20 09:17 bin
-rw-r--r 1 jenny pubs 161 Jun 6 17:15 .profile
drwxrwx-- 26 root 816 Jun 6 14:45 ..
drwxrxr-x 2 jenny pubs 480 Jun 6 17:42 .
```

你可以使用以下 bash 命令来显示你主目录下所有隐藏文件（以点开头）的文件名。这是列出主目录下所有初始化文件的方便方法：

```
ls -d ~.*
```

