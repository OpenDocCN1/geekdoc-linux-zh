
## cpio

**cpio** 是一款功能强大的实用工具，通常与 **find** 配合使用，以执行完全备份和增量备份。**cpio** 是一个成熟的 UNIX 实用工具，在大多数 UNIX 变体上都能以类似的方式工作。

在下面的示例中，我们将使用几条命令，包括以下内容：

- `# find . -print | cpio -oBv > /dev/rmt/0m` ;; 查找当前目录的内容并将其写入磁带。
- `# cpio -it < /dev/rmt/0m` ;; 读取磁带的内容表 (t)。
- `# cpio -icvBdum < /dev/rmt/0m` ;; 恢复 (i) 磁带的内容，这是最广泛使用的 cpio 命令。
- `# find . -print | cpio -oBv | (remsh tapesys dd of=/dev/rmt/0m)` ;; 查找当前目录的内容并将其写入 (o) 远程机器 tapesys 上的磁带。
- `# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum` ;; 将远程系统 tapesys 上磁带的内容 (i) 恢复到本地系统。

我们将发出的第一条命令是 **find**（查找）/var/tmp 中的内容并将其写入我们的磁带设备 /dev/rmt/0m。以下示例中使用的 **cpio** 选项为：*o* 表示输出模式，*B* 表示块输出，*v* 表示详细报告：

```bash
# cd /var/tmp
# find . -print | cpio -oBv > /dev/rmt/0m
(Using tape drive with immediate report mode enabled (reel #1)).
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
...
aaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
#
```

在该示例中，我们首先将目录更改为 `/var/tmp`，然后执行 `find` 命令并将其输出通过管道传递给 `cpio`。`cpio` 几乎总是像示例中那样与 `find` 配合使用。由于我们在发出备份命令之前更改到了目录 `/var/tmp`，因此生成了具有相对路径名称的备份。

接下来，我们将查看磁带的内容，以确认我们使用 `cpio` 写入的文件。`i` 选项用于输入，`t` 选项用于在以下列表获取内容表：

```bash
# cpio -it < /dev/rmt/0m

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
...
ea_aa01487
OB_AMFE_aa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
excl_ude_temp
arch_incl_ude_l
3570 blocks
#
```

既然我们已将内容写入磁带并查看了其内容表，接下来我们将恢复 /var/tmp 的内容。在以下示例中，我们对 `cpio` 使用了几个选项，包括：`i` 表示输入模式，`c` 表示 ASCII 头部格式，`v` 表示详细模式，`B` 表示块输出，`d` 表示目录，`u` 表示无条件覆盖现有文件，以及 `m` 表示恢复原始修改时间：

```bash
# cpio -icvBdum < /dev/rmt/0m
.
envd_action2
envd_action5
swagent_log
ntp
OB_AMHB_AA01020
aaaa01558
aaaa01426
aaaa01112
OB_AMHB_AA01540
aaaa01299
.
.
.
.
.
ea_aa01487
OB_AMFE_aa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
excl_ude_temp
arch_incl_ude_l
3570 blocks
#
```

**cpio** 命令生成将从磁带读取并恢复到系统的文件列表。由于我们包含了详细选项，我们将看到与恢复相关的所有信息。

既然我们已经了解了如何在本地系统上写入磁带、生成内容表以及读取磁带内容，让我们处理一下远程系统上的磁带驱动器。我们将执行向远程磁带驱动器进行备份，查看磁带上的内容表，然后使用远程磁带驱动器进行恢复。

首先，让我们执行向远程磁带驱动器的备份。本地系统没有连接磁带驱动器，它是 *orl*。远程系统连接了磁带驱动器，它是 *tapesy*。我们将在 *orl* 上运行 **cpio**（使用前面描述的相同的三个选项），并在 *tapesy* 上运行远程 shell 和 **dd**，这将存储备份的内容。在以下示例中，我们将在 *orl* 的 */var/tmp* 中运行这些命令：

```bash
# find . -print | cpio -oBv | (remsh tapesy dd of=/dev/rmt/0m)

. 
envd.action2 
envd.action5 
swagent.log 
ntp 
OBAMHBAA01020 
aaaa01558 
aaaa01426 
aaaa01112 
OBAMHBAA01540 
aaaa01299 
:
:
:
aaa01487 
OBAMPEAA01630 
cmd_res8215 
tmp_cfg_file 
cmd_res8708 
exclude.temp 
arch.include.l 
3570 blocks 
#
```

现在让我们回到没有磁带驱动器的本地系统，恢复我们刚刚生成的 **cpio** 磁带的内容，但让我们将它们恢复到不同的目录。我们将磁带内容（最初在 /var/tmp）恢复到的目录是 /tmp/remoteepiofiles。这类似于本章前面 tar 部分中我们执行的过程，当时我们将 tar 文件恢复到了不同的位置。

在以下示例中，我们在 or1 上发出了一系列命令。这些命令中的最后一条是向系统 tapesys 发出 remsh，该系统上有一个装载了我们刚刚创建的 cpio 磁带的磁带驱动器。我们 dd 信息并通过 cpio 管道传输以恢复磁带的内容。在此示例中，我们对 cpio 使用了相同的恢复选项，包括：i 表示输入模式，c 表示 ASCII 头部格式，v 表示详细模式，B 表示块输出，d 表示目录，u 表示无条件覆盖现有文件，以及 m 表示恢复原始修改时间：

```bash
# hostname
or1
# cd /tmp
# mkdir remoteepiofiles
# cd remoteepiofiles
# pwd
/tmp/remoteepiofiles
# remsh tapesys "dd if=/dev/rmt/0m bs=8k" | cpio -icvBdum
envd.action2
envd.action5
swagent.log
ntp
OBAMHBAA01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAA01540
aaaa01299
.
.
.
aaaa01487
OBAMPEAA01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.1
3570 blocks
#
# pwd
/tmp/remoteepiofiles
# ls
envd.action2
enwd.action5
swagent.log
ntp
OBAMHBaa01020
aaaa01558
aaaa01426
aaaa01112
OBAMHBAA01540
aaaa01299
.
.
.
.
eaaa01487
OBAMFEAa01630
cmd_res8215
tmp_cfg_file
cmd_res8708
exclude.temp
arch.include.l
#
```

我们在该示例末尾发出的 ls 确认我们确实将远程系统上的磁带内容写入到了新目录 /tmp/remotecpiofiles。您可能希望在 ls 选项中添加 -a 命令，以确保文件包含内容。

您可以从本 cpio 部分中的简单示例构建备份和恢复命令，以满足您在适度环境中的需求。

## fbackup 和 frecover

**fbackup** 和 **frecover** 是 HP-UX 上首选的备份和恢复程序。使用 **fbackup** 产生的备份无法移植到其他 UNIX 变体。如果您在异构环境中工作，您将无法在 HP-UX 系统上生成的 **fbackup** 磁带恢复到一个运行不同 UNIX 变体的系统上。

在本节中，我将介绍在命令行上发出 **fbackup** 和 **frecover** 命令。您也可以使用 SAM（在第 3 章中有介绍）使用这些命令来管理备份。SAM 帮助您管理 *自动备份* 和 *交互式备份和恢复*。虽然 **fbackup** 和 **frecover** 是随您的 HP-UX 系统捆绑的最先进的备份和恢复程序，但您的需求可能会超越这些程序。您还可以从 HP 和第三方采购高级备份程序。总体而言，我发现 **fbackup** 和 **frecover** 的功能对于新的 HP-UX 安装已经足够。但是，如果您有一个高度分布的环境，或者需要备份大量数据，需要在运行不同操作系统的系统上执行备份，或者需要同时使用多个备份设备，您可能需要考虑更高级的产品。

**fbackup** 具有执行不同 *级别* 备份的功能。级别定义了要包含在备份中的信息量。完全备份，即本节中介绍的内容，是备份级别 0。其他级别定义了各种程度的增量备份。我是执行完全备份的坚定支持者，然后对自*上次完全备份*以来发生变化的每个文件执行增量备份。这意味着，为了从一个完全“损坏”（这是一个表示*毁坏*的技术术语）的系统恢复，您需要您的完全备份磁带和仅一个增量磁带（您将通过使用 **make_recovery** 生成的可启动 Ignite-UX 磁带恢复根卷，这在第 10 章中有介绍）。例如，如果您在周日执行完全备份，并在周一到周五执行增量备份，那么您需要仅加载周日的完全备份磁带和周五的增量备份磁带即可完全恢复系统。**fbackup** 支持此方案。

请记住，虽然我们将在本章的命令行上发出 **fbackup** 和 **frecover** 命令，但通过 SAM 管理这些命令会更加容易。以下是对 **fbackup** 命令及其*部分*选项的说明：

