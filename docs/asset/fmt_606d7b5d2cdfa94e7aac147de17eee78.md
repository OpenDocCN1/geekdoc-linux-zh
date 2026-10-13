
```text
$ pwd
/users/pat/bin                         pat’s program directory
$ ls -l
total 4
-rwxr-xr-x  1 pat      DP3822     1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 pat      DP3822      504 Apr 21 18:30 xtr
$ ln /users/steve/wb .                link wb to pat’s bin
$ ls -l
total 5
-rwxr-xr-x  1 pat      DP3822     1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 steve    DP3725       89 Jun 25 13:30 wb
-rwxr-xr-x  1 pat      DP3822      504 Apr 21 18:30 xtr
$
```

注意，即使在查看 `pat` 的目录内容时，`wb` 的所有者仍然显示为 `steve`。这是合理的，因为实际上该文件只有一份副本，而它的所有者是 `steve`。

关于链接文件的唯一限制是，对于普通链接，要被链接在一起的文件必须位于同一个文件系统上。如果不在同一个文件系统上，当你试图链接它们时，`ln` 会返回一个错误。（要确定系统上的不同文件系统，可以执行 `df` 命令。输出中每行的第一个字段就是一个文件系统的名称。）

要在不同文件系统（或不同网络系统）上的文件之间创建链接，可以使用 `ln` 命令的 `-s` 选项。这会创建一个符号链接。符号链接的行为与普通链接非常相似，区别在于符号链接指向原始文件；如果原始文件被删除，符号链接将不再有效。

让我们看看符号链接在之前的例子中是如何工作的：

```text
$ rm wb
$ ls -l
total 4
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$ ln -s /users/steve/wb ./symwb                 Symbolic link to wb
$ ls -l
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
lrwxrwxr-x  1 pat     DP3822      15 Jul 20 15:22 symwb -> /users/steve/wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$
```

注意，`symwb` 的所有者列的是 `pat`，并且 `ls` 输出中第一个字符显示的文件类型为 `l`，表示这是一个符号链接。这个符号链接的大小是 15（该文件实际上包含字符串 `/users/steve/wb`），但如果尝试访问该文件的内容，看到的却是它所链接到的文件 `/users/steve/wb` 的内容：

```text
$ wc symwb
       5           9          89 symwb

$
```

`ls` 命令的 `-L` 选项可以与 `-l` 选项一起使用，以获取符号链接所指向文件的详细信息列表：

```text
$ ls -Ll
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
-rwxr-xr-x  1 steve   DP3725      89 Jun 25 13:30 wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$
```

删除符号链接所指向的文件会使符号链接失效（因为符号链接是以文件名形式维护的），但并不会删除符号链接本身：

```text
$ rm /users/steve/wb                         Assume that pat can remove this file
$ ls -l
total 5
-rwxr-xr-x  1 pat     DP3822    1358 Jan 15 11:01 lcat
lrwxrwxr-x  1 pat     DP3822      15 Jul 20 15:22 symwb -> /users/steve/wb
-rwxr-xr-x  1 pat     DP3822     504 Apr 21 18:30 xtr
$ wc symwb
Cannot open wb: No such file or directory
$
```

这种类型的文件被称为*悬空符号链接*；除非你有特殊理由保留它（例如，你打算替换被删除的文件），否则应将其删除。

在结束这个话题之前，还有最后一点需要注意：`ln` 命令与 `cp` 和 `mv` 遵循相同的一般格式，也就是说，你可以使用如下格式在特定目标目录中为一组文件创建链接：

```text
ln files directory
```

## 删除目录：`rmdir` 命令

你可以使用 `rmdir` 命令删除目录。不过，为了防止你意外删除几十甚至上百个文件，`rmdir` 只有在指定目录完全没有任何文件和子目录时才会允许你继续操作。

要删除目录 `/users/pat`，可以使用以下命令：

```text
$ rmdir /users/pat
rmdir: pat: Directory not empty
$
```

呼！那本来会是个错误！相反，让我们删除你之前创建的 `misc` 目录：

```text
$ rmdir /users/steve/misc
$
```

同样，上述命令只有在 `misc` 目录中不包含任何文件或目录时才会生效；否则，就会出现下面的情况，正如前面也展示过的那样：

```text
$ rmdir /users/steve/misc
rmdir: /users/steve/misc: Directory not empty
$
```

如果你仍然想删除 `misc` 目录，你必须先删除该目录中的所有文件，然后再重新执行 `rmdir` 命令。

作为删除目录及其内容的另一种方法，你可以使用 `rm` 命令的 `-r` 选项。格式很简单：

```text
rm -r dir
```

其中 `dir` 是你要删除的目录的名称。`rm` 会删除指定目录及其中的所有文件（包括目录），所以使用这个功能强大的命令时要小心。

想直接全速运转？加上 `-f` 标志即可，它会强制执行，而不会逐条命令提示你确认。然而，如果你不小心，它可能会彻底摧毁你的系统，因此许多管理员干脆完全避免使用 `rm -rf`！

## 文件名替换

### 星号

Unix 系统中由 shell 处理的其中一个强大特性就是*文件名替换*。假设你的当前目录中有以下文件：

```text
$ ls
chap1
chap2
chap3
chap4
$
```

假设你想一次显示它们的内容。很简单：`cat` 允许你显示命令行上指定的任意数量文件的内容。就像这样：

```text
$ cat chap1 chap2 chap3 chap4
    ...
$
```

但这很繁琐。相反，你可以利用文件名替换，只需输入：

```text
$ cat *
    ...
$
```

`shell` 会自动把当前目录中与模式 `*` 匹配的所有文件的名称替换进去。当然，如果你把 `*` 与其他命令一起使用，也会发生同样的替换。`echo` 呢？

```text
$ echo * *
chap1 chap2 chap3 chap4 : chap1 chap2 chap3 chap4
$
```

这里的 `*` 再次被替换为当前目录中所有文件的名称，`echo` 命令只是把这个列表显示给你。

只要 `*` 出现在命令行上的任意位置，`shell` 就会执行替换：

```text
$ echo * *
chap1 chap2 chap3 chap4 : chap1 chap2 chap3 chap4
$
```

实际上，`*` 是一种丰富的文件替换语言的一部分，它还可以与其他字符组合使用，以限制匹配哪些文件名。

例如，假设你的当前目录中不仅有 `chap1` 到 `chap4`，还有文件 `a`、`b` 和 `c`：

```text
$ ls
a
b
c
chap1
chap2
chap3
chap4
$
```

若只显示以 `chap` 开头的文件内容，你可以输入：

```sh
$ cat chap*
    .
    .
    .
$
```

`chap*` 匹配任何以 `chap` 开头的文件名。在指定命令被调用之前，所有匹配的文件名都会被替换到命令行上。

`*` 并不限于文件名的末尾；它同样可以用于文件名的开头或中间：

```sh
$ echo *t1
chap1
$ echo *t*
chap1 chap2 chap3 chap4
$ echo *x
*x
$
```
