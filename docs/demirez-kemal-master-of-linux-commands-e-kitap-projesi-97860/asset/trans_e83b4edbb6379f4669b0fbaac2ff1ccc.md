

# 56 | Linux 命令精阶

```
root@kemal:/home# pushd /etc
etc /home
root@kemal:/etc# pushd
/home /etc
root@kemal:/home# pushd
/etc /home
root@kemal:/etc# pushd
/home /etc
root@kemal:/home# _
```

上面我们有两个简单的示例。可以使用 `pushd` 命令在持久目录之间进行切换，通过 `popd` 我们可以切换回其他目录并进行操作。

```
root@kemal:~# cd /home
root@kemal:/home# pushd /etc
etc /home
root@kemal:/etc# pushd /var
/var /etc /home
root@kemal:/var# popd
/etc /home
root@kemal:/etc# popd
/home
```

要列出打开打开的目录，可以使用 `dirs -v` 命令。

# ls 命令

```
root@kemal:~# cd /home
root@kemal:/home# pushd /etc
/etc /home
root@kemal:/etc# dirs -v
0 /etc
1 /home
root@kemal:/etc# 
```

要列出目录、文件夹和文件的子目录，请使用 `ls` 命令。我们可以带参数或不带参数使用此命令。不带参数将得到如下输出：

```
root@kemal:~# ls
Belgeler dwhelper Masaüstü Resimler Videolar
Downloads Genel Müzik Şablonlar
root@kemal:~# -
```

如果你使用 `ls -l`，我们将获得更详细的输出。此详细列表中提供了文件访问权限、所有者、创建日期等信息。

```
root@kemal:~# ls -l
toplam 36
drwxr-xr-x 2 root 4096 Agu 22 10:10 Belgeler
drwxr-xr-x 2 root 4096 Agu 22 10:10 Downloads
drwxr-xr-x 2 root 4096 Agu 22 12:21 dwhelper
drwxr-xr-x 2 root 4096 Agu 22 10:10 Genel
drwxr-xr-x 2 root 4096 Agu 22 17:34 Masaüstü
drwxr-xr-x 2 root 4096 Agu 22 10:10 Müzik
drwxr-xr-x 2 root 4096 Agu 22 10:10 Resimler
drwxr-xr-x 2 root 4096 Agu 22 10:10 Şablonlar
drwxr-xr-x 2 root 4096 Agu 22 10:10 Videolar
root@kemal:~# 
```

# 58 | Linux 命令精阶

如果想查看隐藏文件（隐藏文件以 `.` 开头），请使用 `ls -la` 命令。

```
root@kemal:~# ls -la
toplam 06
drwr-xr-x 2 root 4096 Agu 23 12:40 .
drwr-xr-x 2 root 4096 Agu 22 11:18 .
-rw------- 1 root 1714 Agu 23 10:42 .bash_history
-rw-r--r-- 1 root 3391 Agu 11 11:06 .bashrc
drwr-xr-x 2 root 4096 Agu 22 10:10 .Beliger
drwx------ 2 root 4096 Agu 22 12:22 .cache
drwr-xr-x 15 root 4096 Agu 22 18:48 .config
drwx------ 3 root 4096 Agu 23 10:10 .dbus
drwr-xr-x 2 root 4096 Agu 22 10:10 Downloads
drwr-xr-x 2 root 4096 Agu 22 12:21 dwhelper
drwx------ 3 root 4096 Agu 23 09:50 .gconf
drwr-xr-x 2 root 4096 Agu 22 11:35 .gnome2
-rw------- 1 root 1554 Agu 23 09:50 .iceauthority
drwx------ 3 root 4096 Agu 22 10:10 .local
```

我们还可以使用 `-R` 参数递归地列出目录的内容。

```
root@kemal:~# ls -R
.
Beleler dwhelper Masaüstü Resimler Videolar
Downloads Genel Müzik Şablonlar
./Belgeler:
./Downloads:
./dwhelper:
./Genel:
./Masaüstü:
Aproce Linux Komut Satırı.pdf LKS MATERYAL
```

要按行列出，我们应该使用 `ls -1` 命令。

```
root@kemal:~# ls -1
Belgeler
Downloads
dwhelper
Genel
Masaüstü
Müzik
Resimler
Şablonlar
Videolar
root@kemal:~#
```

其他可以使用的参数有：

- `ls -r`: 反序显示列表。
- `ls -S`: 按文件大小排序。
- `ls -F`: 根据文件类型排序。
- `*`: 可执行文件。
- `@`: 符号链接。
- `/`: 目录。
- `ls -i`: 列出索引节点（inode number）。
- `ls -lh`: 以人类易读格式列出大小。
- `ls -lt`: 按修改日期排序文件。

| 列 | 值 |
| :--- | :--- |
| 1562 | Belgeler |
| 1561 | Genel |
| 1564 | Resimler |
| 1559 | Downloads |
| 1558 | Masaüstü |
| 1560 | Şablonlar |
| 1555 | dwhelper |
| 1563 | Müzik |
| 1565 | Videolar |

现在让我们讨论 `ls` 命令的其他形式。例如，如果我们只想查看目录中的隐藏文件，应该使用什么命令？答案是 `ls -d`。

```
root@kemal:~# ls -d
.bashrc .dbus .cache .gconf .bash_history .config .gnome2 .local .mozilla
```

如果你不想列出目录的内容，那么应该使用 `ls -d`。即使没有名为 `test` 的文件，我们的命令也会被创建并保存到指定短语创建的文件中。

```
root@kemal:/var/log/apache2# ls ..
backups cache local opt
```

# 浏览器

作为提醒，我想在这里添加一些额外信息。你可以使用浏览器列出文件、在目录之间切换等。例如，在根目录下命令行输入 `/` 并回车。你将看到如下内容：

img/aa6ce54db8ffe9ef8c674064_0

当你使用浏览器列出目录时，输入 `../` 切换到上级目录，你可以切换到 `/root/Desktop`：

img/aa6ce54db8ffe9ef8c674064_1

# 62 | Linux 命令精阶

从桌面目录到上级目录，在上面的图中输入 `../` 并回车，将进入上级目录，浏览器将显示如下：

img/aa6ce54db8ffe9ef8c674064_0

当然，要查看目录中的文件，你也可以使用浏览器浏览目录外的帮助页。例如，在命令行输入 `cat`，将出现帮助屏幕。

img/aa6ce54db8ffe9ef8c674064_1

# 第5章

## 文件操作

在本章中，我们将讨论创建文件、复制、查看内容、重定向命令输出到文件等。在这里处理的文件通常是文本文件。

我们的主题顺序如下：在需要的地方提供命令示例，这样可以提供更高效的处理。我认为叙述风格会更好。

# Touch

创建文本文件最简单的方法之一是 `touch` 命令。例如，通过 `touch` 命令，我们可以创建一个名为 `test` 的文本文件（如果你愿意，可以命名 `test.txt`）。

```
root@kemal:~/zeyno# touch test
root@kemal:~/zeyno# ls
test
```

此命令不仅用于创建文本文件，你还可以用它更新现有文件的时间戳。

```
root@kemal:~# -l users.txt
-rw--w--r-- 1 root 144 May 18 02:09 users.txt
root@kemal:~# touch users.txt
root@kemal:~# -l users.txt
-rw--w--r-- 1 root 144 Jan 6 00:34 users.txt
```

# Cat

“cat” 用于从终端屏幕读取文件内容，也用于写入文本文件。例如，要写入一个空 `test` 文件，输入 `cat > test` 命令（注意 `>` 运算符的使用），输入我们想要的短语并用 `CTRL + D` 结束文本。因此，我们在控制台上写的内容将注册到我们的文件中。要读取文件内容，我们可以使用 `cat` 命令。

```
root@kemal:~zeyno# cat > test
Kali Linux 2.0 (Kali Sana)
root@kemal:~zeyno# cat > test
Kali Linux 2.0 (Kali Sana)
root@kemal:~zeyno# _
```

在上面的示例中，我们将我们的文本写入了现有文件。即使没有名为 `test` 的文件，我们的命令也会被创建并保存到指定短语创建的文件中。

如果你再次检查上面的示例，我们使用 `>` 运算符，我们称之为重定向运算符。该运算符用于生成的文件。该运算符有许多不同的用法。给定的表达式、命令输出等可以重定向到文件，也可以将文件的内容作为参数。

我们稍后会提供关于这些示例。现在我们只讨论 `>` 和 `>>` 运算符。向现有文件写入任何内容时，该文件必须是空的。如果不为空，它将删除旧内容并写入新内容。当然，这是使用 `>` 运算符的情况。

