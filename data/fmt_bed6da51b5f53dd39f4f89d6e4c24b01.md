
在文件系统中创建归档后，该文件可以通过网络发送到其他计算机。这是目前最常见的备份和分发软件的方法。遗憾的是，`tar` 工具不会压缩归档内部的文件。因此，网络传输归档的时间很长。为了减少传输时间，你可以在传输之前使用压缩工具压缩归档。由于这是一个常见任务，`tar` 命令允许在创建后立即使用 `gzip` 或 `bzip2` 压缩归档。

要创建一个包含当前目录内容的名为 `/backup.tar.gz` 的 `gzip` 归档并查看结果，可以使用以下命令：

```
[@server1]$ # tar -zcv /backup.tar.gz
Desktop/
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile
[@server1]$ # ls -l /backup.tar
-rw-r--r-- root 40960 Jul 27 10:49 /backup.tar
-rw-r--r-- root 12207 Jul 27 10:18 /backup.tar.gz
[@server1]$ #
```

注意前面的输出，`-z` 选项使用了 `gzip` 压缩，我们选择了 `.tar.gz` 扩展名。此外，`/backup.tar.gz` 文件的大小小于之前创建的 `/backup.tar` 文件。

![](img/bafa5678973f896b93838a140b8f7840_516_0.png)

以 `.tar.gz` 或 `.gz` 结尾的文件通常被称为 `tarball`，因为它们代表压缩后的归档。要查看 `gzip` 归档的内容，必须在使用 `-t` 选项的同时向 `tar` 命令提供 `-z` 选项。可以使用以下命令查看 `/backup.tar.gz` 的详细内容：

```
[@server1]$ # tar -ztv /backup.tar.gz
drwxr-xr-x root 2010-07-21 08:15 Desktop/
-rw-r--r-- root 3595 2010-06-21 20:32 Desktop/Home.desktop
-rw-r--r-- root 3595 2010-06-21 20:32 Desktop/trash.desktop
-rw-r--r-- root 20239 2010-07-21 08:15 samplefile
-rw-r--r-- root 574 2010-07-21 08:18 samplefile
[@server1]$ #
```

![](img/bafa5678973f896b93838a140b8f7840_516_1.png)

# 第11 章 压缩、系统备份和软件安装

同样，提取 `gzip` 压缩的归档时，必须向 `tar` 命令提供 `-z` 选项。要将 `/backup.tar.gz` 文件的内容提取到名为 `tartest2` 的新目录并查看结果，可以使用以下命令：

```
[server1 ~#]# mkdir /tartest2
[server1 ~#]# cd /tartest2
[server1 ~tartest2]# tar -xvf /backup.tar.gz
Desktop/Home.desktop
Desktop/trash.desktop
samplefile
samplefile
```

```
[server1 tartest2]# ls -F
Desktop/ samplefile samplefile
[server1 tartest2]#
```

当你通过网络传输归档数据时，将文件备份到文件系统的压缩归档是有用的。你可以直接将数据备份到磁带等设备。将文件备份到设备时，你可以使用 `tar` 命令的 `-f` 选项指定相应设备文件的路径。文件将直接传输到设备，覆盖可能存在的任何其他数据或文件系统。

例如，要在第一个等待的 `SCSI` 磁带上创建一个包含当前目录内容的归档，可以使用以下命令：

```
[server1 ~#]# tar -cvf /dev/st0 *
Desktop/
Home.desktop
Desktop/trash.desktop
samplefile
samplefile2
[server1 ~#]
```

你可以使用 `tar -tvf /dev/st0` 命令查看前一个示例设备上归档的内容，也可以像上面的示例一样使用 `tar -xvf /dev/st0` 命令提取设备上归档的内容。

由于磁带设备持有大量信息，你可能想向磁带上已存在的归档添加内容。为此，只需在使用 `tar` 时将 `-c` 选项替换为 `-r` 选项。例如，将 `samplefile3` 添加到之前输出中创建的归档并查看结果，可以使用以下命令：

```
[server1 ~#]# tar -rvf /dev/st0 samplefile3
samplefile3
[server1 ~#]# tar -tvf /dev/st0
drwx--r--r-- root 0 2020-07-21 08:15 Desktop/
-rw--r--r-- root 3595 2020-06-21 20:32 Desktop/Home.desktop
-rw--r--r-- root 3595 2020-06-21 20:32 Desktop/trash.desktop
-rw--r--r-- root 20239 2020-07-21 08:15 samplefile
-rw--r--r-- root 574 2020-07-21 08:18 samplefile2
```

# cpio 实用

另一种常用的备份工具是 `cpio in/out` (`cpio`)。虽然该工具使用的选项与 `tar` 工具类似，但 `cpio` 具有一些额外功能，包括长文件名和备份设备文件的能力。

它的主要用途是在系统故障时备份文件；`cpio` 在归档时默认使用绝对路径名。此外，`cpio` 通常从标准输入 (`stdin`) 获取待归档的文件列表，并将这些文件“输出”到由 `-o` 选项指定的归包中。相反，在提取时，你必须使用 `-I` 选项来指定从哪个归包读取“输入”文件。

表 11-6 列出了 `cpio` 命令的常用选项及其描述。

| 选项 | 描述 |
|---|---|
| `-A` | 将文件追加到现有归包<br>`--append` |
| `-B` | 将默认块大小从 512 字节更改为 5KB，从而加速信息传输 |
| `-C` | 使用 UNIX 和 Linux 不同版本的 `cpio` 广泛识别的存储格式 (SVR4) |
| `-d` | 在提取时根据需要创建目录<br>`--make-directories` |
| `-i` | 从归包中读取文件<br>`--extract` |
| `-I FILENAME` | 代表输入归包；它是查看或提取文件时使用的归包文件或设备文件 |
| `-L` | 防止 `cpio` 备份符号链接；相反，`cpio` 备份符号链接的目标文件<br>`--dereference` |
| `--no-absolute-filenames` | 使用相对路径名在归包中存储文件名 |
| `-o` | 创建新归包<br>`--create` |
| `-O FILENAME` | 代表输出归包；它是备份文件时目标归包的文件或设备文件 |
| `-t` | 列出现有归包的文件内容（目录列表）<br>`--list` |
| `-u` | 在提取时覆盖文件，而不提示用户进行确认<br>`--unconditional` |
| `-v` | 在操作归包时显示详细输出（文件和目录信息）<br>`--verbose` |

表 11-6 `cpio` 命令中使用的常用选项

要使用 `cpio` 创建归包，你必须先生成一个文件名列表。你可以使用 `find` 命令来实现这一点。要列出 `/root/sample` 目录下的所有文件名，可以使用以下命令：

```
[root@server1 ~]# find /root/sample
/root/sample
/root/sample/samplefile
/root/sample/samplefile2
[root@server1 ~]#
```

接下来，你可以将此列表通过 `stdin` 交给 `cpio` 命令。例如，要使用 5KB 的块大小和常用格式将 `/root/sample` 中的所有文件完全备份到第一个 `SCSI` 带设备，可以使用以下命令：

```
[root@server1 ~]# find /root/sample | cpio -vocB -o /dev/st0
/root/sample
/root/sample/samplefile
/root/sample/samplefile2
5 blocks
[root@server1 ~]#
```

要查看此归包的目录列表，你可以使用以下命令：

```
[root@server1 ~]# cpio -vitB -I /dev/st0
drwxr-xr-X 2 root 20239 Jul 27 13:40 /root/sample
-rw-rw-r-- 1 root 574 Jul 21 08:15 /root/sample/samplefiles2
5 blocks
[root@server1 ~]#
```
