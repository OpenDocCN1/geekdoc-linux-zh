
`-Z --compress --uncompress` | 使用 `compress` 工具对归档进行压缩/解压缩

要创建一个名为 `/backup.tar` 且包含当前目录内容的归档，可以使用以下命令：

```
[root@localhost root]# tar -cvf /backup.tar *
Desktop/
Desktop/Home
Desktop/Trash/
Desktop/Trash/.directory
Desktop/www.redhat.com
Desktop/cdrom
Desktop/.directory
Desktop/floppy
Desktop/KDE Control Panel
```

## 第 13 章 压缩、系统备份与软件安装

```
Desktop/Linux Documentation
samplefile
samplefile2
[root@localhost]# ls -l /backup.tar
-rw-r--r-- 1 root 40960 Jul 27 10:49 /backup.tar
-[root@localhost]#
```

从上面的命令可以看出，`-f` 选项后面跟着归档的路径，当前目录中的所有文件都将添加到此归档中。还要注意，默认会递归备份文件并使用相对路径存储；若要在创建归档时强制使用绝对路径，只需在 `tar` 命令中使用 `-P` 选项即可。

归档的文件不需要扩展名；但良好的做法是为归档文件命名扩展名以识别其内容，如上述示例中的 `/backup.tar`。

![](img/6148a12ef656b46c092b21c2e023d928_621_0.png)

在创建归档后，可以通过指定 `tar` 命令的 `-t`（目录）选项和要查看的归档来查看详细内容。例如，要查看之前创建的 `/backup.tar` 归档的详细内容，可以执行以下命令：

```
[root@localhost]# tar -tvf /backup.tar
drwx-r--r-- root 0 2002-07-21 08:15:09 Desktop/Home
-rw-r--r-- root 2558 2002-07-21 20:32:46 Desktop/Trash/
drwx-r--r-- root 757 2002-07-21 08:15:09 Desktop/Directory/.
-rw-r--r-- root 107 2002-07-21 20:32:48 Desktop/redhat.com
-rw-r--r-- root 321 2002-07-18 06:08:35 Desktop/.directory
-rw-r--r-- root 1117 2002-07-21 20:32:48 Desktop/cdrom
-rw-r--r-- root 151 2002-07-21 20:32:46 Desktop/linux
-rw-r--r-- root 149 2002-07-21 20:32:48 Desktop/KDE Control Panel
-rw-r--r-- root 80 2002-07-21 20:32:48 Desktop/Linux Documentation
-rw-r--r-- root 20239 2002-07-21 08:15:35 samplefile
drwx-r--r-- root 574 2002-07-21 08:18:00 samplefile
[root@localhost]#
```

可以使用 `-x` 配合 `tar` 命令将 `/backup.tar` 文件的内容提取到新目录 `tarest` 并查看结果，可以执行以下命令：

```
[root@localhost]# mkdir /tarest
[root@localhost]# cd /tarest
[root@localhost]# tar -xvf /backup.tar
Desktop/Home
Desktop/Trash/

## 系统备份 605

Desktop/Trash/.directory
Desktop/redhat.com
Desktop/cdrom
Desktop/.directory
Desktop/floppy
Desktop/KDE Control Panel
Desktop/Linux Documentation
samplefile
[root@localhost]# ls -F
```

一旦在文件系统中创建了归档，该文件就可以通过网络发送到其他计算机。遗憾的是，`tar` 工具不会压缩归档内部的文件；因此网络传输归档的时间会很长。为了减少传输，你可以在传输之前对归档进行压缩。由于这是一个常见任务，`tar` 命令允许你在创建后立即使用 `compress`、`gzip` 或 `bzip2` 工具进行压缩。

要创建一个包含当前目录内容的 `/backup.tar.gz` gzip 压缩归档，可以使用以下命令：

```
[root@localhost]# tar -zcvf /backup.tar.gz *

Desktop/
Desktop/Home
Desktop/Trash/
Desktop/Trash/.directory
Desktop/redhat.com
Desktop/cdrom
Desktop/.directory
Desktop/floppy
Desktop/KDE Control Panel
Desktop/Linux Documentation
samplefile

[root@localhost]# ls -l /backup.tar

-rw-r--r-- 1 root 40960 Jul 27 10:49 /backup.tar

-rw-r--r-- 1 root 12207 Jul 27 11:18 /backup.tar.gz

[root@localhost]#
```

> 注意上面的 `-z` 选项表示使用 `gzip` 工具，且我们选择以 `.tar.gz` 结尾。此外，`/backup.tar.gz` 文件的大小比之前创建的 `/backup.tar` 文件小得多。以 `.tar.gz` 或 `.tgz` 结尾的文件通常称为 tarball（tar 包)](img/6148a12ef656b46c092b21c2e023d928_622_0.png)

要查看 gzip 归档的内容，必须在使用 `-t` 之后加上 `-z` 选项。可以使用以下命令查看 `/backup.tar.gz` 文件的详细内容：

```
[root@localhost]# tar -ztvf /backup.tar.gz

drwx-r--r-- root 0 2002-07-21 08:15:09 Desktop/
-rw-r--r-- root 2558 2002-07-21 20:32:46 Desktop/Home
-rw-r--r-- root 757 2002-07-21 08:15:09 Desktop/Trash/
-rw-r--r-- root 107 2002-07-21 20:32:48 Desktop/Trash/.directory
-rw-r--r-- root 321 2002-07-21 20:32:48 Desktop/www.redhat.com
-rw-r--r-- root 1117 2002-07-21 20:32:48 Desktop/cdrom
-rw-r--r-- root 151 2002-07-21 20:32:46 Desktop/directory
-rw-r--r-- root 149 2002-07-21 20:32:48 Desktop/floppy
-rw-r--r-- root 80 2002-07-21 20:32:48 Desktop/KDE Control Panel
-rw-r--r-- root 20239 2002-07-21 08:15:35 Desktop/Linux Documentation
-rw-r--r-- root 574 2002-07-21 08:18:00 samplefile
-rw-r--r-- root 574 2002-07-21 
[root@localhost]#
```

同样，在提取 gzip 归档时，必须使用 `-z` 选项。为了将 `/backup.tar` 文件的内容提取到新目录 `tarest` 并查看结果，可以执行以下命令：

```
[root@localhost]# mkdir /tarest
[root@localhost]# cd /tarest
[root@localhost]# tar -xvf /backup.tar

Desktop/Home
Desktop/Trash/
Desktop/Trash/.directory
Desktop/redhat.com
Desktop/cdrom
Desktop/.directory
Desktop/floppy
Desktop/KDE Control Panel
```
