

对于一个频繁使用的系统，在备份过程中备份的文件可能会发生变化，导致恢复的文件可能处于不稳定的状态。LVM 还可以对逻辑卷创建快照，然后对快照进行挂载和备份。

Red Hat 现在支持 LVM 的实现，并包含了一套十多个 LVM 软件工具，用于创建、修改和维护卷组。欲需更多信息，请访问 LVM 主页 http://www.sistina.com/products_lvm.htm，该网站通过 FTP 提供信息、帮助文档和可下载的文件。

## 文件系统操作

不同的人有不同的学习风格。对于你们中倾向于看示例而不是听课的人，这里有几个实用的示例，通过它们你可以学习如何在文件中创建一个文件系统，并使用回环文件系统（loopback filesystem）将其挂载——这是一个允许我们完成这一有用功能的特殊文件系统。你可以使用你创建的文件系统来实验和练习本章中找到几乎所有的命令，而无需担心损坏系统。

## 为测试创建文件系统

由于我们大多数人没有空闲的计算机或硬盘来供实验和练习，我们可以通过创建一个包含我们所选文件系统的镜像文件，并使用回环文件系统将其挂载来自己创建一个。这样，我们就不存在面临意外破坏系统本身的风险。虽然你也可以用软盘进行这些练习，但它们较小的容量限制了你的灵活性。

### 第 1 步——创建一个空白镜像文件

使用 `dd` 命令创建一个块大小为 1024 字节（1兆字节）的文件，并创建一个大小为 10MB 的文件。（你的硬盘上需要足够的空间来存放这么大的文件，因此请相应地调整大小）。我们需要 10,000KB (1024 字节) 的块，因此我们将 `floppy count` 设置为 10000。

如果我们想要软盘大小的镜像，我们会选择 512 的块大小，对于 1.4MB 的软盘选择 2880 次，或为 2.88MB 的软盘选择 5760 次。操作方法如下：

```
# dd if=/dev/zero of=/rhlstest.img bs=1024 count=10000
```

我们看到计算机返回了以下内容：

```
10000+0 records in
10000+0 records out
```

如果我们用 `file` 命令检查我们的新文件，会看到这些：

```
# file /tmp/rhlstest.img
/tmp/rhlstest.img: data
```

### 第 2 步——创建一个文件系统

现在我们需要让系统认为该文件是一个块设备而不是 ASCII 文件，因此我们使用 `losetup`，这是一个将回环设备与普通文件或块设备关联的实用程序；我们将使用回环设备。

```
# losetup /dev/loop0 /tmp/rhlstest.img
```

现在我们可以将该文件格式化为文件系统：

```
# mk2fs /dev/loop0
```

我们看到计算机返回如下：

```
mke2fs 1.27 (8-Mar-2002)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
2512 inodes, 10000 blocks
500 blocks (5.0%) reserved for the super user
First data block=1
2 block groups
8192 blocks per group, 8192 fragments per group
1256 inodes per group
Superblock backups stored on blocks:
8193
```

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

此文件系统将在每 21 次挂载或 180 天后自动检查，以先者为准。使用 `tune2fs -c -i` 可以覆盖。

### 第 3 步——挂载我们的文件系统

在创建测试文件系统后，你可以尝试你将使用的格式化命令的不同选项。为你的镜像文件创建一个挂载点将很有用：

```
# mkdir /mnt/image
```

然后挂载它

```
# mount /dev/loop0 /mnt/image
```

我们现在可以这样做，因为我们已经将回环文件系统与镜像文件关联。如果如果我们重新挂载，必须使用以下格式来使用 loop 选项：

```
# mount -o loop /tmp/rhlstest.img /mnt/image
```

挂载新文件系统后，我们可以查看它，发现上面已经创建了 `lost+found` 目录，并且 `df` 命令返回：

```
# df -h /mnt/image
Filesystem Size Used Avail Use% Mounted on /dev/loop0 \
9.5M 13k 8.9M 1% /mnt/image
```

要卸载它，请使用：

```
# umount /mnt/image
```

为镜像做个备份，以防我们损坏了原始文件：

```
# cp /tmp/rhlstest.img *.bak
```

在创建测试文件系统后，你可以创建目录、复制文件到其中、删除它们、尝试恢复它们，并在学习和练习宝贵技能的同时，在你的计算机上制造混乱。如果镜像上的文件系统损坏到无法修复，请卸载它、删除并创建一个新的。

### 使用 dumpe2fs

你可以使用 `dump2fs` 程序来检查 ext3 文件系统的结构。该程序由 Red Hat 提供。命令的语法为：

```
dump2fs [-superblock] [-o blocksize] [device]
```

要使用 `dump2fs` 检查我们的镜像，首先卸载它，然后使用：

```
dump2fs /tmp/rhlstest.img
dump2fs 1.27 (8-Mar-2002)
Filesystem name: <none>
Last mounted on: <available>
Filesystem UUID: 0364acf-581c-41f0-958921e
Filesystem magic number: 0xEF3
Filesystem revision #: 1 (dynamic)
Filesystem features: sparse
Filesystem state: clean
Errors: Continue
Filesystem OS type: Linux
Inode count: 2512
Block count: 10000
Reserved block count: 500
Free blocks: 9664
Free inodes: 2501
First block: 1
Block size: 1024
Fragment size: 1024
Blocks per group: 8192
Fragments per group: 8192
Inodes per group: 1256
Superblock backups stored on blocks:
8193
```

写入 inode 表: done
写入超级块 和文件系统计数信息: done

此文件系统将会在每 21 次挂载或 180 天后自动检查，以先者为准。使用 `tune2fs -c -i` 可以覆盖。

