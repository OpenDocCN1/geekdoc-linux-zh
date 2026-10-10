

### gzip 命令的常用选项

| 选项 | 描述 |
| :--- | :--- |
| -# | 指定压缩的彻底程度，其中 # 可以是 1~9 之间的数字。选项 -1 表示快速压缩，压缩耗时较短，但压缩率较低。选项 -9 表示彻底压缩，耗时较长，但压缩率较高。 |
| -\best | 结果产生更高的压缩率；等同于 -9 选项。 |
| -C<br>-\stdout<br>-\to-stdout | 与 gunzip 命令配合使用时，将压缩文件的内容显示到标准输出（功能等同于 zcat 命令）。 |
| -d<br>-\decompress<br>-\uncompress | 与 gzip 命令配合使用时，解压缩指定的文件（等同于 gunzip 命令）。 |
| -f<br>-\force | 与 gzip 命令配合使用时，压缩符号链接。与 gunzip 命令配合使用时，不询问用户直接覆盖任何已存在的文件。 |
| -\fast | 结果产生较低的压缩率；等同于 -1 选项。 |
| -h<br>-\help | 显示 gzip 和 gunzip 命令的语法及可用选项。 |
| -l<br>-\list | 列出使用 gzip 压缩过的文件的压缩率。 |
| -n<br>-\no-name | 不允许 gzip 和 gunzip 保留文件的原始修改时间和访问时间。 |
| -q<br>-\quiet | 抑制所有警告消息。 |
| -r<br>-\recursive | 指定递归压缩或解压缩指定目录中的所有文件。 |
| -S .suffix<br>-\suffix .suffix | 在压缩或解压缩文件时，指定除 .gz 以外的文件后缀。 |
| -t<br>-\test | 与 gunzip 命令配合使用时，执行测试解压缩，以便用户在解压缩前查看任何错误消息；它不解压缩文件。 |
| -v<br>-\verbose | 在压缩和解压缩期间显示详细输出（压缩率和文件名）。 |

与 compress 和 gzip 一样，只有使用 -f 选项时，符号链接才会被压缩，并且可以使用 -v 选项来显示压缩率。此外，在压缩过程中，文件的所有权、修改时间和访问时间会被保留。

使用 bzip2 压缩的文件，其文件名扩展名为 .bz2。要压缩 samplefile 和 samplefile2 文件并查看它们的压缩率和文件名，你可以使用以下命令：

```bash
[root@server1 ~]# bzip2 -v samplefile samplefile2
samplefile: 2.637:1, 3,034 bits/byte, 62.08% saved, 20239 in, 7675 out.
samplefile2: 1.483:1, 5.394 bits/byte, 32.58% saved, 574 in, 387 out.
[root@server1 ~]$ ls -l
total 16
drwx------ 3 root root 4096 Jul 21 08:15 Desktop
-rw-rw-r-- 1 root root 387 Jul 21 08:18 samplefile2.bz2
-rw-r--r-- 1 root root 7675 Jul 21 08:15 samplefile.bz2
[root@server1 ~]$
```

由于压缩算法与 **compress** 和 **gzip** 使用的不同，你必须使用 **bcat** 命令将压缩文件的内容显示到标准输出，如下面的示例所示：

```bash
[root@server1 ~]$ bcat samplefile2.bz2
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 ~]$
```

![](img/c27875544958897d817484d558c208c8_509_0.png)

你还可以使用 **bmore** 和 **bless** 命令逐页查看 bzip2 压缩文件的内容。

要解压缩文件，你可以使用 **bunzip2** 命令后跟要解压缩的文件名；与 **compress** 和 **gzip** 不同，在解压缩文件时必须包含文件名扩展名。要解压缩之前创建的 samplefile 和 samplefile2 文件并查看结果，你可以使用以下命令：

```bash
[root@server1 ~]$ bunzip2 -v samplefile.bz2 samplefile2.bz2
samplefile.bz2: done
samplefile2.bz2: done
[root@server1 ~]$
```

如果即将有文件被覆盖，**bunzip2** 命令会提示用户确认。要跳过此确认，你可以包含 *-f* 选项。表 11-3 列出了 **bzip2** 实用程序的其他常用选项。

### bzip2 实用程序的常用选项

| 选项 | 描述 |
| :--- | :--- |
| -# | 指定压缩时使用的块大小；-1 表示块大小为 100KB，而 -9 表示块大小为 900KB。 |
| -c <br> --stdout | 与 bunzip2 命令配合使用时，将压缩文件的内容显示到标准输出。 |
| -d <br> --decompress | 与 bzip2 命令配合使用时，解压缩指定的文件（等同于 bunzip2 命令）。 |
| -f <br> --force | 与 bzip2 命令配合使用时，压缩符号链接。与 bunzip2 命令配合使用时，不询问用户直接覆盖任何已存在的文件。 |
| -k <br> --keep | 在压缩期间保留原始文件；创建一个扩展名为 .bz2 的新文件。 |
| -q <br> --quiet | 抑制所有警告消息。 |
| -s <br> --small | 在压缩期间最小化内存使用。 |
| -t <br> --test | 与 bunzip2 命令配合使用时，执行测试解压缩，以便用户在解压缩前查看任何错误消息；它不解压缩文件。 |
| -v <br> --verbose | 在压缩和解压缩期间显示详细输出（压缩率）。 |

# 系统备份

定期创建文件和目录的备份副本并将其存储在备用位置是个好主意。然后，你可以将这些备份副本分发到其他计算机，或使用它们来恢复因系统故障而丢失的文件。整个过程被称为**系统备份**，文件和目录的备份副本被称为**归档**。

你可以在许多不同类型的介质上创建归档，例如磁带、CD、DVD 或硬盘。传统上，磁带用于备份数据。如今，大型备份通常使用单独的硬盘执行。较小的备份使用 CD 或 DVD 执行，这需要稍后本章中描述的特殊烧录软件。

表 11-4 列出了用于不同磁带设备的一些常见设备文件。

典型的 Linux 系统可以包含数十万个文件，但你不必将所有文件都包含在归档中。例如，你不必包含 /tmp 和 /var/tmp 目录中的临时文件，也不需要包含每个用户主目录下 .mozilla 目录中（如果你使用 Mozilla Firefox Web 浏览器）发现的任何缓存 Internet 内容。

作为一条经验法则，你应该备份主目录中的用户文件以及重要的系统配置文件，如 /etc/passwd。除此之外，你可能还想备份系统服务使用的文件。例如，如果 Linux 计算机用作 Web 服务器，你需要备份网站文件。像 grep 和 vi 这样的程序不需要备份，因为在系统故障时，可以从原始安装介质中恢复它们。

![](img/c27875544958897d817484d558c208c8_510_0.png)

### 常见的磁带设备文件

| 设备文件 | 描述 |
| :--- | :--- |
| /dev/st0 | 第一个 SCSI 磁带设备（回卷） |
| /dev/st1 | 第二个 SCSI 磁带设备（回卷） |
| /dev/st2 | 第三个 SCSI 磁带设备（回卷） |
| /dev/nst0 | 第一个 SCSI 磁带设备（不回卷） |
| /dev/ht0 | 第一个 ATAPI IDE 磁带设备（回卷） |
| /dev/nht0 | 第一个 ATAPI IDE 磁带设备（不回卷） |
| /dev/ftape | 第一个软盘磁带设备 |

在选定用于系统备份的文件后，你可以使用备份实用程序将文件复制到适当的介质上。有几种备份实用程序可供 Linux 管理员使用。最常见的是以下这些：

- 磁带归档 (tar)
- 复制进/出 (cpio)
- dump/restore
- 光盘烧录软件

# 使用磁带归档 (tar)

磁带归档 (tar) 实用程序是最古老、使用最广泛的备份实用程序之一，并通过 **tar** 命令执行。它可以在文件系统上的文件中或直接在设备上创建归档。

与前面讨论的压缩实用程序类似，**tar** 命令接受选项来确定归档的位置以及对归档执行的操作。指定给 **tar** 命令的任何参数都列出了要放入归档的文件。表 11-5 描绘了与 **tar** 命令一起使用的一些常用选项列表。

![](img/c27875544958897d817484d558c208c8_511_0.png)

由于 **tar** 是一个广泛使用的实用程序，表 11-5 中显示的选项也常用于其他类似命令。一个例子是 **jar** 命令，它归档 Java 编程语言使用的可复用类文件。

要创建一个名为 **/backup.tar** 的归档，其中包含当前目录的内容并查看结果，你可以使用以下命令：

```bash
[root@server1 ~]# tar -cvf /backup.tar *
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile2

[root@server1 ~]# ls -l /backup.tar
-rw-r-r-- 1 root root 40960 Jul 27 10:49 /backup.tar

[root@server1 ~]# _
```

