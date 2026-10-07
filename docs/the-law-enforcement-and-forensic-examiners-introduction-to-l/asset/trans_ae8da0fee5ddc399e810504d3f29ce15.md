

# v.4.33 Linux 作为数字取证平台的全面入门指南

无需扩展名，`ewfacquirestream` 会自动为生成的文件添加 E01 扩展名。要获取完整的选项列表，请查看 man 页面或或带有 `-h` 选项运行命令。

回到目标系统，我们使用标准的“通过网线从受控计算机发送数据”命令……

```
root@bootdisk:~# dd if=/dev/sda | nc 192.168.55.20 2525
```

一旦采集完成（你需要在目标系统上运行 `dd` 命令时，停止采集系统上的 `ewfacquirestream` 进程），就可以查看生成的文件并对比哈值。由于我们之前使用了 `shalsum`，现在我们将使用 `md5sum` 重新运行 `ewververify` 的输出：

```
root@bootdisk:~# md5sum /dev/sda
c96c510404d99b4684e50a6995443c9a /dev/sda
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E01
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E02
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E03
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E04
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E05
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E06
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E07
-rw-r--r 1 root root 1.5G May 09:50 nc_wf_image.E08
-rw-r--r 1 root root 293M May 09:50 nc_wf_image.E09
```

```
root@forensic1:~# ewverify nc_wf_image.E01
ewverify 20140608
```

验证开始于：May 06, 2017 09:51:52
...
验证完成于：May 06, 2017 09:55:50

读取：12 GiB (1288401888 bytes)耗时 3 分 58 秒，速度为 51 MiB/s (5413823 bytes/second)。

```
文件中存储的 MD5 哈希:
c96c510404d99b4684e50a6995443c9a
数据计算的 MD5 哈希:
c96c510404d99b4684e50a6995443c9a
```

```
ewverify: SUCCESS
```

...并且我们的验证成功了。

v.4.33 Linux 作为数字取证平台的全面入门指南

# 远程传输 – 其他选项

我们已经涵盖了通过网络管道进行介质镜像的最基础知识和机制。`netcat` 并不是此问题的完美解决方案，尽管它是简单选项之一，并且在大多数启动盘和 Linux 系统中都可用。

实际上，你可能需要考虑数据在穿越网络时是否经过了加密。在示例中，我们可能是通过交叉网线（接口到接口）或独立的网络集线器连接的。如果你处于许多连接被收集的环境怎么办？或者在企业级硬件（交换机等）上？在这种情况下，你就需要加密。为此，你可以使用 `cryptcat` 或 `ssh`。现在你已经理解了这项技术的基本机制，敦促你探索其他工具和方法。有诸如 ddd https://sourceforge.net/projects/ddd/ 和 air (https://sourceforge.net/projects/air-image/) 这样的项目你可能想要探索，不仅用于网络镜像。即时压缩通过

镜像时的另一个很有用功能是压缩。考虑到我们在这里对取证应用的关注，我们将务必管理好压缩技术，以便我们可以在不解压和不写入镜像的情况下验证我们的哈值。

对于这次练习，我们将使用 GNU `gzip` 应用。`gzip` 是一个命令行工具，允许我们对压缩过程进行相当细致的控制。还有其他压缩工具（zip, xz 等），但由于我们学习 `dd` 和 `vi` 的原因，我们将专注于 `gzip`……始终可用，且是学习命令行概念的起点。大多数软件的源码包都以 `.gz` 压缩格式最少提供，但我建议你自己探索其他压缩选项。

首先，为了熟悉起来，让我们看看 `gzip` 在单个文件上的简单用法，并探索我们可以使用的一些选项。我创建了一个名为 `testcomp` 的目录，并将镜像文件 `NTFS_Pract_2017.raw` 复制到该目录中练习。这为我提供了一个整洁的实验场所。首先，让我们双检镜像的哈值：

```
root@forens1:\# mkdir testcomp

root@forens1:\# cp nt NTFS_Pract_2017.raw testcomp/

root@forens1:\# cd testcomp

root@forens1:~/testcomp# ls -lh
total 501M
-rw-r--r-- 1 root root 500M 6 12:10 NTFS_Pract_2017.raw
```

```
root@forens1:~/testcomp# sha1sum NTFS_Pract_2017.raw
094123df4792b18a1f064f1e2fc609028695f85 NTFS_Pract_2017.raw
```

现在，在最简单的形式下，我们可以调用 `gzip` 并直接提供我们要压缩的文件名。这将原始文件替换为带有 `.gz` 后缀的压缩文件。

```
root@forensic:~/testcomp# gzip NTFS_Pract_2017.raw

root@forensic:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root root 61M May 09:50 NTFS_Pract_2017.raw.gz
```

现在，我们用一个带有 `.gz` 扩展名的 61M 文件替换了原始 500M 文件。要解压生成的 `.gz` 文件：

```
root@forensic:~/testcomp# gzip -d NTFS_Pract_2017.raw.gz

root@forensic:~/testcomp# ls -lh
total 501M
-rw-r--r-- 1 root root 500M May 12:10 NTFS_Pract_2017.raw
```

```
root@forensic:~/testcomp# sha1sum NTFS_Pract_2017.raw
094123df4792b18a1f064f1e2fc609028695f85 NTFS_Pract_2017.raw
```

我们解压了文件并将 `.gz` 文件替换为原始镜像。哈值检查显示一切正常。假设我们想压缩一个文件但保留原始文件。可以使用 `gzip` 命令配合 `-c` 选项。它会写入标准输出而不是替换文件。在使用此选项时，我们需要将输出重定向到我们选择的文件，这里使用这种技术：

```
root@forensic:~/testcomp# ls -lh
total 51M
-rw-r--r-- 1 root root 500M May 12:10 NTFS_Pract_2017.raw
-rw-r--r-- 1 root root 61M May 12:10 NTFS_Pract_2017.raw.gz
```

```
root@forensic:~/testcomp# gzip -c NTFS_Pract_2017.raw > NewImage.gz

root@forensic:~/testcomp# ls -lh
total 51M
-rw-r--r-- 1 root root 500M May 12:10 NTFS_Pract_2017.raw
-rw-r--r-- 1 root root 61M May 12:10 NewImage.gz
```

```
root@forensic:~/testcomp# gzip -cd NewImage.gz > Newcompressed.raw
```

```
root@forens1:~/testcomp$ ls -lh
total 1G
-rw-r--r-- 1 root root 500M May 12:10 NTFS_Pract_2017.raw
-rw-r--r-- 1 root root 61M May 12:10 NewImage.gz
-rw-r--r-- 1 root root 500M May 12:10 Newcompressed.raw
```

```
root@forens1:~/testcomp# sha1sum Newcompressed.raw
094123df4792b18a1f064f1e2fc602855
```

在上面的输出中，我们看到第一个列表显示了镜像文件。然后使用 `gzip -c` 将其写入标准输出。我们将该输出重定向到一个新文件（自行选择）。第二个列表显示原始文件仍然存在，并且创建了压缩文件。然后使用 `gzip -cd` 解压文件，将输出重定向到一个新文件并保留压缩文件。这些都是使用 `gzip` 的非常基础的选项。`-c` 允许我们压缩文件并将输出管道到哈希算法。在实际意义上，这允许我们在不写入文件的情况下创建压缩镜像并检查其哈值。

如果我们回到目录中的镜像文件，可以执行此操作。删除我们刚刚创建的文件（使用 `rm` 命令）并保留原始镜像。现在我们将从原始镜像创建一个压缩文件，然后检查压缩文件的哈值以确保其有效性：

```
root@forens1:~/testcomp# ls -lh
total 501M
-rw-r--r-- 1 root root 500M May 6 12:10 NTFS_Pract_2017.raw
```

```
root@forens1:~/testcomp# sha1sum NTFS_Pract_2017.raw
```

```
root@forens1:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root root 61M May 6 12:10 NTFS_Pract_2017.raw.gz
```

```
root@forens1:~/testcomp# cd NTFS_Pract_2017.raw.gz | sha1sum
094123df4792b18a1f064f1e2fc602855 -
```

```
root@forens1:~/testcomp# ls -lh
total 61M
-rw-r--r-- 1 root root 61M May 6 12:10 NTFS_Pract_2017.raw.gz
```

# v.4.33 Linux 作为数字取证平台的全面入门指南

首先我们看到了正确的哈值。然后我们使用简单的 `gzip` 命令对其进行压缩并替换原始文件。现在我们接下来想要做是在不写入新镜像的情况下检查压缩镜像的哈值。我们可以使用 `gzip -c`（标准输出）`-d`（解压），传递压缩文件的文件名，但将输出管道到我们的哈希算法（在此 `sha1sum` 中）。结果显示了输出流的正确哈值，输出流由 `-` 表示。

好了，现在我们已经基础掌握了使用 `gzip` 压缩、解压和验证哈值的知识，让我们通过 `dd` “即时”投入工作，来创建一个压缩镜像。然后我们将根据原始哈值检查压缩镜像的值。

找一个小的 U 盘或其他介质进行镜像。我将使用一个 8GB 的 USB 闪存。清空 `testcomp` 目录以便我们有一个干净的地方写入镜像（或任何你有写入空间的地方）。

即时获取 `dd` 镜像是通过流并将该输出通过管道重定向到 `gzip` 命令，然后就可以检查生成的镜像。考虑以下内容。在这种情况下，我们作为示例的物理设备是 `/dev/sdi`（如果我们使用设备跟随操作，请记得使用 `lss` 和 `lsblk` 来找到正确的设备）。

```
root@forens1:~/testcomp sha1sum /dev/
21e8e63bfc9c3fa782339567dd94bbb2cfc /dev/
```

```
root@forens1:~/testcomp# dd if=/dev/sdi gzip -c > sdi_image.raw
156958571+0 records in
156958571+8 records out (8.0 GB, 7.5 GiB) copied, 283.091 s, 28.4 MB/s
```

```
root@forens1:~/testcomp# ls -lh
total 2.8G
-rw-r--r-- 1 root root 2.8G sdi_image.raw
```

```
root@forens1:~/testcomp# gzip -cd sdi_image.raw | sha1sum
21e8e66bfc9c3fa782339567dd94bbb2cfc
```

