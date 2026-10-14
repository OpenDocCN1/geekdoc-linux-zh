

```
-rw-r--r-- 1 me me 15738 2012-10-14 07:15 foo.txt
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 3230 2012-10-14 07:15 foo.txt.gz
[me@linuxbox ~]$ gunzip foo.txt
[me@linuxbox ~]$ ls -l foo.*
-rw-r--r-- 1 me me 15738 2012-10-14 07:15 foo.txt
```

在此示例中，我们从目录列表创建了一个名为 foo.txt 的文本文件。接下来，我们运行 gzip，它用压缩版本 foo.txt.gz 替换了原始文件。在 foo.* 的目录列表中，我们可以看到原始文件已被压缩版本替换，并且压缩版本的大小约为原始文件的五分之一。我们还可以看到压缩文件具有与原始文件相同的权限和时间戳。

接下来，我们运行 gunzip 程序来解压缩文件。之后，我们可以看到文件的压缩版本已被原始文件替换，权限和时间戳同样得以保留。

gzip 有许多选项。表 18-1 列出了其中几个。

## 表 18-1：gzip 选项

| 选项 | 描述 |
|---|---|
| -c | 将输出写入标准输出并保留原始文件。也可使用 --stdout 和 --to-stdout 指定。 |
| -d | 解压缩。这会使 gzip 像 gunzip 一样工作。也可使用 --decompress 或 --uncompress 指定。 |
| -f | 强制压缩，即使原始文件的压缩版本已存在。也可使用 --force 指定。 |
| -h | 显示使用信息。也可使用 --help 指定。 |
| -l | 列出每个已压缩文件的压缩统计信息。也可使用 --list 指定。 |
| -r | 如果命令行上的一个或多个参数是目录，则递归压缩其中包含的文件。也可使用 --recursive 指定。 |
| -t | 测试压缩文件的完整性。也可使用 --test 指定。 |
| -v | 在压缩时显示详细消息。也可使用 --verbose 指定。 |
| -number | 设置压缩量。number 是 1 到 9 之间的整数，1 表示最快、压缩率最低，9 表示最慢、压缩率最高。值 1 和 9 也可分别表示为 --fast 和 --best。默认值是 6。 |

让我们再次回顾之前的示例：

```
[me@linuxbox ~]$ gzip foo.txt
[me@linuxbox ~]$ gzip -tv foo.txt.gz
foo.txt.gz:         OK
[me@linuxbox ~]$ gzip -d foo.txt.gz
```

这里，我们用压缩版本 foo.txt.gz 替换了文件 foo.txt。接下来，我们使用 -t 和 -v 选项测试了压缩版本的完整性。最后，我们将文件解压缩回原始形式。gzip 也可以通过标准输入和输出以有趣的方式使用：

```
[me@linuxbox ~]$ ls -l /etc | gzip > foo.txt.gz
```

此命令创建了一个目录列表的压缩版本。gunzip 程序用于解压缩 gzip 文件，它假定文件名以扩展名 .gz 结尾，因此无需指定它，只要指定的名称不与现有未压缩文件冲突即可：

```
[me@linuxbox ~]$ gunzip foo.txt
```

如果我们的目标只是查看压缩文本文件的内容，我们可以这样做：

```
[me@linuxbox ~]$ gunzip -c foo.txt | less
```

或者，gzip 提供的程序 zcat 等同于带 -c 选项的 gunzip。它可以像 cat 命令一样用于 gzip 压缩文件：

```
[me@linuxbox ~]$ zcat foo.txt.gz | less
```

注意：还有一个 zless 程序。它执行与上述管道相同的功能。

## bzip2—以速度为代价获得更高压缩率

Julian Seward 编写的 bzip2 程序与 gzip 类似，但使用不同的压缩算法，在压缩速度的代价下实现了更高的压缩率。在大多数方面，它的工作方式与 gzip 相同。用 bzip2 压缩的文件以扩展名 .bz2 表示：

```
[me@linuxbox ~]$ ls -l /etc > foo.txt
[me@linuxbox ~]$ ls -l foo.txt
-rw-r--r-- 1 me me 15738 2012-10-17 13:51 foo.txt
[me@linuxbox ~]$ bzip2 foo.txt
[me@linuxbox ~]$ ls -l foo.txt.bz2
-rw-r--r-- 1 me me 2792 2012-10-17 13:51 foo.txt.bz2
[me@linuxbox ~]$ bunzip2 foo.txt.bz2
```
