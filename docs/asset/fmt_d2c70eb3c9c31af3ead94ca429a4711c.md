
上一个示例展示了关于 `cp` 的一个你需要知道的重要知识点。在“使用通配符复制文件”示例中，你将三张 `libby_on_floor` 图片复制到了 `libby` 目录中；在上一个示例中，你再次将这些相同的 `libby_on_floor` 复制到 `libby` 目录中。你复制了已经存在的文件，但 `cp` 并没有警告你，这就是 Linux 的工作方式：它并不知道你在做什么，所以除非你要求它这样做，否则它不会警告你正在覆盖文件。在用 `cp` 命令覆盖文件之前，你应该得到警告，请使用 `-i` 选项（或 `--interactive`）。如果你现在这次尝试使用 `-i` 选项复制相同的文件，你将得到一个不同的结果。

```
$pwd
/home/scott/libby
$ ls ~/pix
arrowck.jpg by_pool_03.jpg on_floor_03.jpg
by_pool_01.jpg on_floor_01.jpg on_floor_04.jpg
by_pool_02.jpg on_floor_02.jpg
$ ls
arrowck.jpg libby_on_couch.jpg on_floor_02.jpg
libby.jpg on_floor_01.jpg on_floor_03.jpg
$ cp -i ~/pix/on_floor_01[1-3].jpg
cp: overwrite './.on_floor_01.jpg'?
```

# 第一部分：入门

砰！`cp` 命令停了下来，询问你是否想要覆盖它正尝试覆盖的第一个文件 `libby_on_floor_01.jpg`。如果你想继续复制该文件，输入 `y`；否则，输入 `n`。如果你选择了 `n`，这并不意味着 `cp` 完全停止；你会被询问下一个文件，接下一个，依此类推。通过输入 `n` 来取消整个进程的唯一方法是按下 `Ctrl+c`。同样，没有办法提前对所有问题说是，如果你想将 1000 个文件复制到另外 1000 个同名文件，并且打算使用 `-i` 选项，请确保你有充足的时间坐在那里与 shell 交互，因为你会被询问 1000 次你是否真的想覆盖你的文件。

> **注意**
>
> 对于普通用户来说，`-i` 通常不是必要的。但对于 `root` 用户来说，它几乎是必须的，因为 `root` 用户可以轻松复制任何关键系统文件，导致灾难。出于如此，在 `root` 用户的 `.bashrc` 文件中创建一个别名是一个好主意，确保 `cp` 实际上是 `cp -i`。

```
alias cp='cp -i'
```

### 复制目录

#### `cp -R`

到目前为止你查看了复制文件，但有时你也想复制目录。不过，你不能直接输入 `cp 源目录 目标目录`，因为那样不会按你预期的方式工作；目录会复制，但它内部的文件不会。

```
$pwd
/home/scott
$ cp libby libby_bak
cp: omitting directory 'libby'
```

如果你想复制目录，需要包含 `-R` 选项（或 `--recursive`），你应该从 `ls` 命令中记得这个选项。添加 `-R` 意味着目录及其内容都会被复制。

```
$pwd
/home/scott
$ ls -l
drwxr-xr-x 328 2005-10-17 14:42 documents
drwxr-xr-x 240 2005-10-20 17:16 libby
$ cp -R libby_bak
$ ls -l
drwxr-xr-x 328 2005-10-17 14:42 documents
drwxr-xr-x 240 2005-10-20 17:16 libby
drwxr-xr-x 240 2005-10-20 17:17 libby_bak
```

### 作为目录复制文件

#### `cp -a`

你可能认为 `cp` 对备份文件很有用，这确实如此（尽管有更好的程序，我们会查看其中一个）。通过几行 `bash` 脚本，`cp` 可以是备份文件和目录的有效方法。在这种情况下最有用的选项是 `-a`（或 `--archive`），它等同于组合了多个选项：`-dp`（或 `--no-dereference recursive`）。另一种理解方式是 `-a` 确保 `cp` 不跟踪符号链接（这可能会导致复制膨胀），保留文件所有者和时间戳并递归处理子目录。

```
$pwd
/home/scott
$ ls
drwxr-xr-x 216 2005-10-21 11:31 libby
drwxr-xr-x 216 2005-09-29 23:17 music
$ ls -LR
libby:
total 312
-rw--r-- 73786 2005-10-20 12:12 arrowck.jpg
-rw--r-- 18034 2005-04-19 00:57 libby.jpg
-rw--r-- 198557 2005-04-19 00:57 on_couch.jpg
drwxr-xr-x 218 2005-10-21 11:31 on_floor
libby/on_floor:
total 764
-rw--r-- 218849 2005-10-20 16:11 on_floor_01.jpg
-rw--r-- 200024 2005-10-20 16:11 on_floor_02.jpg
-rw--r-- 358986 2005-10-20 16:11 on_floor_03.jpg
$ cp -a libby libby_bak
$ ls -l
drwxr-xr-x 216 2005-10-21 11:31 libby_bak/
drwxr-xr-x 216 2005-10-21 11:31 libby_bak/
drwxr-xr-x 216 2005-09-29 23:17 music
$ ls -LR
lib_bak:
total 312
-rw--r-- 73786 2005-10-20 12:12 arrowck.jpg
-rw--r-- 18034 2005-04-19 00:57 libby.jpg
-rw--r-- 198557 2005-04-19 00:57 on_couch.jpg
drwxr-xr-x 218 2005-10-21 11:31 on_floor
```

> **注意**
>
> 是的，你可能已经发现了，但让我确认一下：`Libby` 是我的狗，一只可爱的西西，最终以某种方式出现在我写的每个地方。想看她，请访问 `http://www.granneman.com/go/libby`。

### 移动并重命名文件

#### `mv`

复制文件。看起来足够简单，但移动文件呢？沿着移除命令中不必要元元的类似思路，我们有 `mv` 命令，`move` 的缩写。

你会很快发现，你为 `cp` 学的大多数选项与 `mv` 使用的选项非常相似。这应该不会感到惊讶；毕竟，`mv` 执行了 `cp -a`，然后移动它成功复制的文件。

简单来说，`mv` 将文件从你的一个位置移动到另一个位置。

```
$ pwd
/home/scott/libby
$ ls
libby_arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_03.jpg
libby_on_floor_02.jpg libby_on_floor_04.jpg
$ mv ~/pix/dogs/libby_on_floor_04.jpg libby_on_floor_04.jpg
$ ls
libby_arrowck.jpg libby.jpg libby_on_floor_04.jpg
libby_bak.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_02.jpg libby_on_floor_03.jpg
```

就像你用 `cp` 时做的一样，如果你不想输入文件名，可以使用点来表示当前目录。

```
$pwd
/home/scott/libby
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_03.jpg
libby_on_floor_02.jpg libby_on_floor_04.jpg
$ mv ~/pix/dogs/libby_on_floor_04.jpg .
$ ls
arrowck.jpg libby_bak.jpg libby.jpg libby_on_couch.jpg on_floor
libby_on_floor_04.jpg
$ ls ~/pix/dogs
libby_on_floor_01.jpg libby_on_floor_02.jpg libby_on_floor_03.jpg
```

如果你正在将一个文件移动到目录并想保留相同的文件名，你只需要指定目录。文件名保持不变。
