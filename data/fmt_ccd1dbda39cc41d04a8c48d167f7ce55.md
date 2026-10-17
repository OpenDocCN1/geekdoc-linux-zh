
x aaaaa01354, 102 bytes, 1 tape blocks

x aaaaa01380, 102 bytes, 1 tape blocks

x aaaaa01405, 99 bytes, 1 tape blocks

:

:

x daaa01405, 28 bytes, 1 tape blocks

x daaa01487, 28 bytes, 1 tape blocks

x eaaaa01299, 28 bytes, 1 tape blocks

x eaaaa01333, 28 bytes, 1 tape blocks

x eaaaa01354, 28 bytes, 1 tape blocks

x eaaaa01380, 28 bytes, 1 tape blocks

x eaaaa01405, 28 bytes, 1 tape blocks

x eaaaa01487, 28 bytes, 1 tape blocks

x envd.action2, 28 bytes, 1 tape blocks

x envd.action5, 28 bytes, 1 tape blocks

x swagent.log, 600 bytes, 2 tape blocks

#

![](img/6969df54e516231f8e64fd1177ac1127_337_0.png)

在创建 `tar` 备份时，我首先进入了 `/var/tmp` 目录，然后使用了 `ls` 命令（该命令位于大多数键盘左上角，在波浪键附近，出现在 `ls` 前后）。这产生了相对路径，我可以很容易将其还原到 `/tmp/puttarfileshare` 目录。或者，我也可以切换到 `/var` 并执行 `tar cf /dev/rmt/0` 命令来备份 `/var/tmp` 目录的所有内容。

![](img/6969df54e516231f8e64fd1177ac1127_337_1)

此过程也可以单行完成。以下来自章节末尾 `tar` 手页的在 `fromdir` 生成归档并还原到 `todir` 的步骤：

```bash
cd fromdir; tar cf - | cd tod; tar xf -
```

`-` 告诉 `tar` 将数据发送到标准输出。`tar xf` 命令中的 `-` 则告诉 `tar` 从标准输入读取数据，这些数据是由之前执行的 `tar cf` 命令产生的。

![](img/6969df54e516231f8e64fd1177ac1127_338_0)

## cpio

`cpio` 是一个强大的工具，通常配合 `find` 一起执行全量和增量备份。`cpio` 是一个成熟的 UNIX 工具，在大多数变体中均适用。将在接下来的示例中使用以下几个命令：

```bash
find . -print | cpio -oB > /dev/rmt/0; 将当前目录的内容写入磁带
cpio -it < /dev/rmt/0; 读取磁带内容 (t)
cpio -it < /dev/rmt/0; 还原磁带内容 (i)，这是最常用的 cpio 命令
find . -print | cpio -oB | dd=/dev/rmt/0; 将当前目录的内容写入 (o) 远程机器
dd if=/dev/rmt/0 bs=8k | cpio -icdum; 将远程系统的磁带内容还原 (i) 到本地系统
```

我们将执行的第一个命令是查找 `/var/tmp` 中的内容并将其写入磁带设备 `/dev/rmt/0`。在后续示例中使用的 `cpio` 选项有：`o` 用于输出模式，`B` 用于块输出，`v` 用于详细报告：

![](img/6969df54e516231f8e64fd1177ac1127_339_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_339_1.png)

### cpio 299

```bash
cd /var/tmp
find -print | cpio -oBv > /dev/rmt/0
(使用立即报告模式的磁带驱动卷 #1))
envd.action2
envd.action5
swagent.log
tp
OBAMHBAa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBaa015440
aaaa01299
eaaa01487
OBAMFEaa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
```

在示例中，我们首先切换目录到 `/var/tmp`，然后执行 `find` 命令并将输出通过给 `cpio`。`cpio` 几乎总是如示例所示配合 `find` 使用。由于我们在执行备份命令之前切换到了 `/var/tmp` 目录，因此生成的备份使用了相对路径。

接下来，我们将查看磁带的内容以查看写入 cpio 的文件。`i` 选项用于输入，`t` 选项用于获取内容列表：

```bash
cpio -it < /dev/rmt/0
```

envd.action2

envd.action5

swagent.log

![](img/6969df54e516231f8e64fd1177ac1127_340_0.png)

### 300

### 第 6 章 备份

```bash
ntp
OBAMHBaa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBaa015440
aaaa01299
eaaa01487
OBAMFEaa01630
cmd_res8215
tmp_cfg_file
cmd_res82708
exclude.temp
arch.include.1
3570 blocks
```

![](img/6969df54e516231f8e64fd1177ac1127_341_0.png)

现在我们已经写入磁带并查看了其内容，我们将还原 `/var/tmp` 的内容。后续示例中使用的 `cpio` 选项有：`o` 用于输出模式，`B` 用于块输出，`v` 用于详细报告。这与我们在之前的章节中将 tar 文件还原到不同位置的过程相似。示例中使用的 `cpio` 命令是：

```bash
find . -print | cpio -oBv > /dev/rmt/0
envd.action2
envd.action5
swagent.log
tp
OBAMHBaaa1020
aaaa01558
aaaa01426
aaaa01112
OBAMHBaa015440
aaaa01299
eaaa01487
OBAMFEaa01630
cmd_res8215
tmp_cfg_file
cmd_res82708
exclude.temp
arch.include.1
3570 blocks
```

后续示例中的 `cpio` 命令是：

```bash
find . -print | cpio -oBv > /dev/rmt/0
```

#### cpio 303

```
aaaa01112
OBAMHBAa01540
aaaa01299
```

```
aaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
#
# pwd
/tmp/remotecpiofiles
### ls
envd.action2
envd.action5
swagent.log
ntp
OBAMHBAa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAa01540
aaaa01299
```

```
aaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
#
```

我们在示例结束处执行的 `ls` 命令确认了我们确实已经将磁带的内容写入了远程系统的新目录 `/tmp/remotecpiofiles`。你可能想向 `ls` 选项中添加 `-a` 命令以确保文件包含内容。

你可以根据此 cpio 部分的简单示例进行构建，以开发满足中等环境需求的备份和恢复命令。

![](img/6969df54e516231f8e64fd1177ac1127_344_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_344_1.png)

### 304

# 第6章 备份

## fbackup 和 frecover

![](img/6969df54e516231f8e64fd1177ac1127_345_0.png)

`fbackup` 和 `frecover` 是 HP-UX 上首选的备份和恢复程序。使用 `fbackup` 生成的备份无法用于其他 UNIX 变体。如果你在异构环境中工作，将无法将 HP-UX 系统上生成的 `fbackup` 磁带恢复到运行不同 UNIX 变体的系统中。
