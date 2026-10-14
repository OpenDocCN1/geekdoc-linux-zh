

好的，把一张 DOS 磁盘放入机器中，我们来试试一些例子。
这里可以看到 mdir 命令的运行情况，列出磁盘上的文件：

```
mdir A:

Volume in drive A has no label

Volume Serial Number is 1205-1049

Directory of A:\

COMMAND COM      54,645 05-31-94  6:22a
FORMAT  COM      22,974 05-31-94  6:22a
SYS     COM      9,432 05-31-94  6:22a
MOUSE   COM      28,949 04-02-93  4:39p
EDIT    COM        413 05-31-94  6:22a
FDISK   EXE      29,336 01-01-97 12:39a

              6 file(s)          145,749 bytes

                         1,311,915 bytes free
```

现在让我们从 Linux 复制一个文件到磁盘，反之亦然：

```
mcopy A:pandavu.tgz /tmp
mcopy /tmp/kornmeal.txt A:
```

mcopy 命令通过查找源或目标文件名中的 A: 来判断文件传输的方向。如果您有两个软盘驱动器，可以使用 B: 来引用第二个软盘驱动器。

下面是一个使用 mdel 命令删除磁盘上文件的示例：

```
mdel mouse.com
```

请注意，这次我们没有在要删除的文件名前加上 A:。所有 MTOOLS 命令（mcopy 除外）都假定您正在使用 A 驱动器，因此您可以省略 A:，但我建议您不要这样做，只是为了安全起见。

这将是 DOS 下执行 `dir C:` 命令的结果。您可以使用 `cd` 查看 `/dos` 下的其他目录，并使用任何 Linux 命令来处理您的 DOS 文件。

能够在 Linux 和 DOS 之间复制文件来回已经很棒了，但如果你发挥创意，还可以做一些巧妙的事情。我发现使用 `ln`（链接）命令在 Linux 和 DOS 之间共享我的 Netscape 书签文件特别有帮助，像这样：

```
`ln -s /dos/netscape/bookmark.htm $HOME/.netscape/bookmarks`
```

通过将这些文件链接在一起，我只需要管理一个书签文件。当然，这个技巧只有在 DOS 和 Linux 版本的产品对共享文件的格式相同的情况下才有效。

如果您希望每次启动 Linux 时都挂载 DOS 分区，请将下面显示的行添加到 `/etc/fstab` 文件中：

```
`/dev/hda1  /dos  msdos  umask=022`
```

Linux 启动时，会查看 `/etc/fstab` 文件并挂载其中指定的所有文件系统，这样您就无需手动发出 mount 命令即可访问 DOS 分区。您刚刚添加到 `/etc/fstab` 的这一行与前面显示的 mount 命令具有相同的效果。这里同样适用于 FAT32 文件系统的注意事项，因此您可能需要将前面的示例中的 `msdos` 替换为 `vfat`。

## 使用 DOSEMU 运行 DOS 程序

DOSemu（DOS 模拟器）是一个程序，让您能够在 Linux 下运行许多您喜爱的 DOS 应用程序。名字有点误导性——它实际上并不模拟 DOS；它利用 Intel 80386 及更高 CPU 中的特殊硬件功能将 DOS 启动到虚拟机中。

DOSemu 会话看起来和实际的 DOS 会话一样，有一些限制。并非所有视频和声卡都在 DOSemu 下得到支持，并且一些需要 DPMI（DOS 保护模式接口）的程序将无法运行。最著名的例子是 Windows 3.1，尽管有些人确实报告说能够在 DOSemu 下运行它。

## 设置 DOSEMU

设置 DOSemu 不难，但要获得一个完全功能的 DOS 会话确实需要几个步骤。不幸的是，本书光盘中没有 DOSemu 软件包，因此您必须从 DOSemu 网站下载——http://www.dosemu.org/。我建议您获取最新稳定版本（截至出版时为 v0.98）并远离开发版本，因为它们往往存在错误。

下载 DOSemu 的 RPM 文件后，以 root 身份登录并执行如下命令。文件名可能略有不同，具体取决于您下载的版本。（有关 rpm 命令的更多信息，请参阅第 14 章“更新您的 Linux 系统”。）

```
rpm -i dosemu-0.98.6-1.i386.rpm
```

安装 DOSemu v0.98

## 配置 DOSEMU

软件包现已安装，但在使用之前我们需要调整 DOSemu 配置文件。编辑 /etc/dosemu.conf 文件并修改 $_hdimage 条目，使其如下所示：

```
$_hdimage = "hdimage.test /dev/hda1"
```

hdimage.test 文件位于您的 /var/lib/dosemu 目录中，它是一个硬盘映像——一个包含完整 DOS 系统的特殊 Linux 文件。您刚刚修改的那一行告诉 DOSemu 在启动时将 hdimage.test 文件视为 C 驱动器。这个 C 驱动器不是您心爱的 DOS 分区；它是一个模拟的可启动硬盘分区，包含 FreeDOS 操作系统——MS-DOS 的免费克隆版。修改后行中的 /dev/hda1 部分告诉 DOSemu 将您的真实 DOS 分区视为下一个驱动器号，即 D 驱动器。（您可以直接从真实的 DOS 分区启动 DOSemu，但我们稍后会讨论这个问题。）

## 启动 DOSEMU 会话

在启动将访问 /dev/hda1（您的 MS-DOS 分区）的 DOSemu 会话之前，务必先卸载该分区。

