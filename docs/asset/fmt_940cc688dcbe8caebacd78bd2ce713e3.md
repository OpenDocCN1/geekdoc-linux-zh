
```
ufsstore > cd sbin
ufsstore > ls
:/bin:
18498 /*       188505 config    188513 rc3      188517 sulogin
  2 *       188506 init       188510 rc5      188518 swapped
188500 autopost 188507 jsh        188510 rc6      188519 sync
188543 bggetfile 188508 mount    188514 rcS      188520 uadmin
188501 dhcpagent 188509 mountall 188507 sh       188521 umount
188502 *dhcpinfo 188510 rc0       188515 sconfig   188522 umamount
188503 fdisk       188511 rc1       188499 su         188523 uname
188504 hostconfig 188512 rc2       188516 su.static
```

要指定你想恢复列表中的 `dhcpinfo` 文件，使用 `ufsstore` 将其恢复到你运行的文件列表中：

`ufsstore > add dhcpinfo`

现在当你执行 `ls` 时，你会看到一个带星号的 `dhcpinfo` 条。

## 关键子系统

第二部分

你现在可以根据需要添加文件。也可以使用 Shell 通配符。因此，你可能可以说 `add rc*` 来获取所有以“rc.” 开头的文件和目录。要从待恢复的文件列表中删除文件，只需指定 `remove filename`。

```
ufsstore > extract
Extract requested files
You have not read any volumes.
Unless you know which volume your file(s) are on you should
with the last volume and work towards the first.
Specify next volume #:
```

继续操作，并指定卷号 #：1

`extract file .sbin/dhcpinfo`

添加链接

Add links

set directory mode, owner, and 'yn'

set owner/mode for '.?' [yn]

在此时提示符处，如果你正在恢复整个文件系统，请输入 yes（是）。如果你只是在恢复部分文件，请输入 no（否）。输入 no 将保持你当前工作目录的权限不变。输入 yes 将导致当前工作目录的权限恢复到备份磁带创建时的原始状态。

你可以通过输入 `q` 退出交互式会话：

- # `ufsstore > q`

要恢复整个文件系统，请指定 `r` 选项（递归）：

- # `ufsstore rvfvy /dev/rmt/on`

你需要从最后一个 Level 0 备份开始，并在每次增量复制后重复该命令，以找回所有内容。`dump` 和 `ufsdump` 也可以通过指定 `f` 选项向远程主机的磁带写入，只需在设备名称后加上其所连接的主机名来限定该设备名称即可：

- # `ufsdump unsdf 126 141000 11500 otherhost.umd.edu:/dev/rmt/0/dev/rdsk/ct030d55`

这要求 `otherhost.umd.edu` 通过 `/.hosts` 文件信任你的系统。许多站点由于潜在的安全风险不允许出现 `.hosts` 条目。如果你需要进行此类远程备份且无法使用 hosts，可以使用 `ssh`（参见第 8 章“为部署保护系统安全”）。

## 使用 dd 进行备份和恢复

`dd` 是一个从你指定的源到你指定的目标执行逐字节复制的命令。它特别适用于备份一类特殊数据：原始数据。原始数据是位于设备指向的磁盘空间上的数据，但那里没有构建文件系统结构。因为该空间内没有独立的文件，它完全是一个连续的空间。`dd` 是你唯一可以使用来制作此类磁盘副本的工具。以下是它的用法示例：

```
# dd if=/dev/rdsk/c0t3d0s1 of=/dev/rmt/
```

- `if`—代表“输入文件”，即读取位置。指定你正在备份的区域的原始设备名称。
- `of`—代表“输出文件”，即写入位置。在此处指定你的磁带设备名称（尽管当然，你也可以指定系统上的其他原始磁盘空间，这样你就会在系统上获得该空间的另一个精确副本）。

你可能希望指定至少 10KB 的块大小，以帮助磁带写入过程更高效。只需在命令中添加 `bs=10k` 即可。

要读取这些内容，只需反转 `if` 和 `of` 的位置即可：

```
# dd if=/dev/rmt/ of=/dev/rdsk/c0t3d0s1 bs=10k
```
