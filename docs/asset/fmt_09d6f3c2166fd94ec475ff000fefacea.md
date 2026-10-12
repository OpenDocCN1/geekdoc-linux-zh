
# 第 11 章 Linux 文件系统、共享与服务权限

```
[avazquez@bravo ~]$ ls -l example.txt
-rw-rw-rw-. 1 avazquez avazquez 0 6月29 23:31 example.txt
```

如果我们想撤销此权限，也可以用 `chmod` 实现。

```
[avazquez@bravo ~]$ chmod o-w example.txt
[avazquez@bravo ~]$ ls -l example.txt
-rw-rw-r-- 1 avazquez avazquez 0 6月29 23:31 example.txt
```

还有另一种替代语法，它不是使用 `-u`、`-g`、`-o` 等标志，而是指定分配给这三组中每一组权限的二进制表示。

默认情况下，每种类型的权限被分配如下值：`r = 4`，`w = 2`，`x = 1`。在我们的示例中，与 `example.txt` 文件关联的权限二进制表示将为 `664`，因为所有者拥有读取 `4` 加写入 `2` 权限，组也拥有读取 `4` 加写入 `2` 权限，而其他用户只有读取 `4` 权限。

我们可以通过 `stat` 命令来检查这一点，它会向我们显示两种格式的文件权限，以及其他有趣的信息。

```
[avazquez@bravo ~]$ stat example.txt
File: example.txt
Size: 0      Blocks: 0      IO Block: 4096 regular empty file
Device: fd01h/64769d Inode: 34311523 Links: 1
Access: (0664/-rw-rw--) Uid: ( 1003/avazquez) Gid: ( 1003/avazquez)
```

因此，如果我们只想给组提供读取权限，可以再次这样使用 `chmod`：

```
[avazquez@bravo ~]$ chmod 644 example.txt
[avazquez@bravo ~]$ ls -l example.txt
-rw-rw-r-- 1 avazquez avazquez 0 6月29 23:31 example.txt
```

*注：此处原文示例命令与描述逻辑略有出入，按原意翻译*

默认情况下，每种类型的权限被分配如下值：`r = 4`，`w = 2`，和 `x = 1`。在我们的示例中，与 `example.txt` 文件关联的权限二进制表示将为 `664`，因为所有者拥有读取 `4` 加写入 `2` 权限，组也拥有读取 `4` 加写入 `2` 权限，而其他用户只有读取 `4` 权限。

我们可以通过 `stat` 命令来检查这一点，它会向我们显示两种格式的文件权限，以及其他有趣的信息。

```
[avazquez@bravo ~]$ stat example.txt
File: example.txt
Size: 0      Blocks: 0      IO Block: 4096 regular empty file
Device: fd01h/64769d Inode: 34311523 Links: 1
Access: (0664/-rw-rw--) Uid: ( 1003/avazquez) Gid: ( 1003/avazquez)
```
