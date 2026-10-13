
这里，filename 是你想要获取更多信息的文件的名称。例如，命令：

```
$ file /bin/sh
```

将产生与以下类似的输出：

```
/bin/sh: ELF 32-bit MSB executable SPARC Version 1,
	statically linked, stripped
```

根据此输出，你可以判断文件 /bin/sh 是为基于 SPARC 的系统编写的可执行程序。你系统上的输出很可能不同。

## 链接

链接是一个指向系统上另一个文件的文件。链接对于在系统的多个位置维护文件的多个副本非常有用，而无需为副本使用存储空间。因为链接只是指向另一个文件，所以更改链接的内容会改变原始文件的内容。同样，改变原始文件的内容似乎也会改变链接的内容。

UNIX 支持两种类型的链接，硬链接和符号链接。

## 硬链接

硬链接是一个指向另一个文件的特殊目录项。硬链接有一些限制：

- 硬链接不能指向目录：它只能指向文件。
- 硬链接与它指向的文件无法区分：无法判断某个特定文件是硬链接还是原始文件。

硬链接可以使用 ln（link 的缩写）命令创建。其语法如下：
ln src target
这里 src 是 target 应该指向的路径名。例如，如果你想让硬链接 banana 指向文件 apple，可以按如下方式创建链接：
$ ln apple banana
如果创建硬链接时出现问题，ln 会显示错误消息；否则，不会显示任何输出。
当硬链接从一个目录移动到另一个目录时，它可以继续指向原始文件而不会出现任何问题。例如，考虑以下命令：
$ echo I drink lemonade in the summer > lemonade
$ cat lemonade
I drink lemonade in the summer

```
$ ln lemonade summer_drink
$ cat summer_drink
I drink lemonade in the summer
$ mv summer_drink ..
$ cat ../summer_drink
I drink lemonade in the summer
```

从输出中可以看到，即使文件 summer_drink 被移出创建它的目录，它仍然指向原始文件。

当硬链接被删除时，它指向的原始文件不受影响；只会删除链接。如果原始文件被删除，原始文件的条目会被移除，但其内容会保留在磁盘上，直到链接被删除为止。例如：

```
$ echo Pomegranates are very juicy > juicy
$ ln juicy pomegranate
$ cat pomegranate
Pomegranates are very juicy
$ rm juicy
$ cat pomegranate
Pomegranates are very juicy
cat: juicy: No such file or directory
```

正如你所见，即使文件 juicy 已被移除，文件 pomegranate 仍继续指向文件 juicy 的内容。

> 如果一个文件有多个硬链接到它，仅仅删除该文件不足以释放磁盘空间；你必须删除指向该文件的所有硬链接。

## 符号链接

符号链接或 symlink 是一个存储指向另一个文件路径名的特殊文件。当访问 symlink 时，系统会自动读取 symlink 中存储的路径名并访问对应路径名的文件，因此 symlink 可以指向系统上的任何文件。symlink 中存储的路径名可以是绝对路径或相对路径。如果存储的是相对路径名，则该路径名相对于链接所在的目录，而不是当前工作目录。

符号链接的 ls -l 输出看起来类似于以下内容：

```
lrwxrwxrwx 1 root root 9 Oct 23 13:58 /bin/ -> ./usr/bin/
```

symlink 是使用 ln 的 -s 选项创建的。语法如下：

```
ln -s src target
```

这里 src 是 target 应该指向的路径名。例如，如果你想创建指向文件 lime 的 symlink citrus，可以使用以下命令：

```
ln -s lime citrus
```

如果创建 symlink 时出现问题，ln 会显示错误消息；否则，不会显示任何输出。

如果使用相对路径创建 symlink，则在从创建的目录移动到另一个目录时可能无法正常工作。例如：

```
$ echo Persimmons are bitter until they ripen > persimmon
$ ln -s persimmon bitter
$ cat bitter
Persimmons are bitter until they ripen
$ mv bitter ..
$ cat ../bitter
cat: ../bitter: No such file or directory
$ ls -l ..
lrwxrwxrwx 1 root root 9 Jan 13 00:16 ../bitter@ -> persimmon
```

从输出中可以看到，只要两个文件位于同一目录，链接 bitter 就能正确指向文件 persimmon。当 bitter 被移动后，链接停止工作，因为在 bitter 的新目录中不存在名为 persimmon 的文件。可以通过在创建 symlink 时使用绝对路径来避免此问题。

当 symlink 被删除时，它指向的文件不受影响。当 symlink 指向的文件被删除或移动到其他位置时，symlink 将无法正常工作。例如：

```
$ echo Plums were plentiful this year > plums
$ ln -s plums plentiful
$ cat plentiful
Plums were plentiful this year
$ rm plums
$ cat plentiful
cat: plentiful: No such file or directory
$ ls -l plentiful
lrwxr-xr-x 1 ranga wheel 5 Jan 13 00:25 plentiful -> plums
```

从输出中可以看到，即使该文件已被删除，链接 plentiful 仍指向文件 plums。这导致了 cat 的错误消息。

## 常见错误

创建链接时遇到的两个常见错误发生在

- target 已存在。
- target 是一个目录。

如果 target 是文件，ln 将不会创建请求的链接。例如，如果当前目录中存在文件 .exrc，则以下命令：

```
$ ln -s /etc/exrc .exrc
```

会产生以下错误消息：

```
ln: cannot create .exrc: File exists
```

如果 target 是目录，ln 会在该目录中创建链接，文件名与 src 相同。例如，如果当前目录中存在目录 pub，则以下命令：

```
$ ln -s /home/ftp/pub/ranga pub
```

会创建链接 pub/ranga，而不是抱怨目标是目录。

忘记这种行为是 shell 脚本中问题的常见来源。

## 设备文件

在 UNIX 中，设备，如硬盘、键盘和打印机，是通过设备文件访问的。有两种类型的设备文件：字符特殊文件和块特殊文件。

设备文件通常位于 /dev 目录中。

## 字符特殊文件

字符特殊文件提供了一种逐字符与设备通信的机制。通常字符设备代表“原始”设备。对字符特殊文件执行 ls -l 的输出如下所示：

```
crw------- 1 ranga users 4, 0 Feb 7 13:47 /dev/tty0
```

输出中的第一个字母 c 表示这是一个字符特殊文件。日期前的两个额外数字称为主设备号和次设备号。UNIX 使用这两个数字来识别连接到字符特殊文件的设备驱动程序。

## 块特殊文件

块特殊文件提供了一种通过传输大量数据块而不是单个字符与设备通信的机制。块特殊文件通常用于

访问硬盘和可移动介质。对块特殊文件执行 ls -l 的输出如下所示：

```
brw-rw---- 1 root disk 8, 0 Feb 7 13:47 /dev/sda
```

输出中的第一个字母 b 表示该文件是块特殊文件。文件的主设备号和次设备号标识连接到块特殊文件的设备驱动程序。

## 命名管道

UNIX 的一个重要特性是，你可以用很少的工作将一个程序的输出重定向到另一个程序的输入。例如，以下命令：

```
$ who | grep ranga
```

将 who 命令的输出作为 grep 命令的输入。在命令行上，使用临时匿名管道，但有时程序需要对通信通道有更多控制。命名管道是充当命令行上临时匿名管道的文件。

命名管道可以使用 mkfifo 命令创建。其语法如下：

```
mkfifo file
```

这里 file 是你想赋予管道的文件名。例如，以下命令创建名为 mypipe 的命名管道：

```
$ mkfifo mypipe
```

此命名管道的 ls -l 输出将类似于以下内容：

```
prw-r--r-- 1 ranga wheel 0 Nov 22 17:39 mypipe
```

第一个字符 p 表示该文件是命名管道。

## 所有者、组和权限

文件权限和文件所有权是 UNIX 的重要组成部分，因为它们提供了一种安全的文件存储方法。UNIX 中每个文件都有以下属性：

- 所有者权限
- 组权限
- 其他（世界）权限

所有者的权限决定文件所有者可以对文件执行哪些操作。组的权限决定作为该组成员的用户可以

