
```bash
# mkisofs -o home.iso -R -j music/ docs/ \ Multiple directories/files chris.pdf /var/spool/mail \
# mkisofs -o home.iso -R \ Graft files on the image -graft-points /var/pics/ /home/chris
```

第一个示例显示了将各种文件和目录组合并放置在 ISO 镜像的根目录下。第二个示例将`/var/pics`目录的内容映射到`/home/chris/Pictures`目录中。在 CD 镜像上，`/Pictures`目录将包含来自`/var/pics`目录的所有内容。

添加关于 ISO 头部的信息有助于你以后识别其内容。如果镜像被保存或在网上发布，而没有可以写入的物理磁盘，这会特别有用。以下是一些示例：

```bash
# mkisofs -o /tmp/home.iso -R \ Add header into ISO -p www.handsonhistory.com \
-publisher "Swan Boy Art Center" \
-V "WebBackup" \
-A mkisofs \
-volset "1 of 4 backups, July 30, 2007" \
/home/chris
```

在示例中，`-p`指定制表者 ID，它可以包括电话号码、邮寄地址或用于联系 ISO 镜像制者的网站。使用`-publisher`选项，你可以指定对制表者的 128 字符描述（可能是公司或组织名称）。`-V`表示卷 ID（Volume ID）。卷 ID 在许多 Linux 系统中非常重要，此卷 ID 用于在插入 CD 时挂载它。例如，在上面的命令中，在 SUSE 和其他 Linux 系统中，CD 将挂载在`/media/WebBackup`。`-A`选项用于指示创建 ISO 镜像的应用程序。`-volset`选项可以包含关于一组 ISO 镜像的信息字符串。

当你创建了 ISO 镜像并在将其刻录到磁盘之前，你可以检查镜像并确保你可以访问这些文件。以下是检查方法：

```bash
# volname home.iso Display volume name
WebBackup
# infoiso -d i home.iso Display header information
CD-ROM is in ISO 9660 format
System id: LINUX
```

Volume id: WebBackup

Volume set: All Website material on November 2, 2007

Publisher id: Swan Bay Folk Art Center

Data preparer id: www.handsonhistory.com

Application id: mkisofs

Copyright File id:

Abstract File id:

Bibliographic File id:

Volume set sequence number is: 1

Logical block size is: 2048

Volume size is: 23805

Joliet with UCS level version 1 found

Rock Ridge signatures 1 found

（此处省略重复翻译）

你可以看到在创建镜像时输入`mkisofs`命令行的信息列表。如果你有一个要发布的镜像，你可能还会注意到 CD 上版权文件 (`-copyright`)、摘要文件 (`-abstract`) 和书目文件 (`-biblio`) 的位置。头部正常，你可以尝试通过挂载 ISO 来下次访问 ISO 上的文件：

```bash
# mkdir /mnt/myimage
# mount -o loop home.iso /mnt/myimage
# ls -l /mnt/myimage
# umount /mnt/myimage
```

- 创建挂载点

- 以回环模式挂载 ISO

- 检查 ISO 内容

- 完成后卸载镜像

除外，你还可以访问 ISO 上的文件和目录，确保日期/时间戳、所有权和权限设置为你预期的状态。如果你在以后某个日期需要恢复镜像，这些信息可能会有用。

# 使用 crecord 刻录备份镜像

`crecord`命令是 Linux 中最流行的刻录 CD 和 DVD 镜像的命令行工具。在你创建了 ISO 镜像（如前所述）或通过其他方式获取了镜像（例如从互联网下载安装 CD 或现场版 CD）后，`crecord`可以轻松地将该镜像放入磁盘。

> 注意：`crecord`命令已被`widom`命令取代。`widom`命令基于`crecord`代码库创建，仍然支持大多数选项。如果你运行`crecord`，在此 SUSE 版本中你实际上运行的是`widom`。如需帮助请访问 CDRkit 项目 (`http://cdrkit.org`)。

制作 CD 或 DVD ISO 镜像没有区别，只是 DVD 镜像显然可以比 CD 镜像大。检查你的介质的容量。CD 通常可以容纳 650MB、700MB 或 800MB，而迷你 CD 可以容纳 50MB、180MB、185MB 或 193MB。单层 DVD 可以容纳 4.7GB，而双层 DVD 可以容纳 8.4GB。

（此处省略大量重复段落）

# 使用 growisofs 制作并刻录 DVD

使用`growisofs`命令，你可以将收集文件到 ISO 镜像 (`mkisofs`) 和将该镜像刻录到 DVD (`cdrecord`) 的两个步骤合并。除了节省步骤外，`growisofs`命令还有默认在关闭之前保持会话开启的优势。这是一个示例：

```bash
# growisofs -Z /dev/dvd -R /home/chris      Master and burn to DVD
# growisofs -Z /dev/dvd -R /home/francois    Add to burn
# growisofs -M /dev/dvd=/dev/zero           Close burn
```

如果你想在创建 ISO 镜像时添加选项，只需将`mkisofs`选项添加到命令行即可。（例如，参见上面的示例中如何添加`-R`和`-J`选项。）

如果你想使用`growisofs`刻录 DVD，可以使用`-dvd-compat`选项。例如：

```bash
# growisofs -dvd-compat -Z /dev/dvd-image.iso Burn an ISO image to DVD
```

`-dvd-compat`选项可以提高与不同会话 DVD 程序的兼容性。

## 总结

Linux 及其前身 Unix 系统通过组合每个处理离散功能的命令来处理数据备份。你关键数据的备份仍然可以通过这种方式进行。事实上，你使用的许多工具比以前任何时候都更安全、更高效。

存档工具（`tar`命令）范围已远远超过了它最初制作磁带数据备份的工作。由于几乎每个 Linux 和 UNIX 系统包含`tar`，它已成为软件包和将数据备份到压缩存档的标准工具。这些存档可以通过多种方式进行传输和存储。

要通过网络将备份数据移动到其他机器，可以使用 OpenSSH 工具的远程功能（例如`ssh`）。你还可以使用一个名为`rsync`的优秀工具。通过`rsync`，你可以只备份已更改的文件（或文件的部分）来节省资源。

廉价的 CD 和 DVD 已成为个人和小型办公室备份的流行介质。`mkisofs`命令可以创建 ISO9660 格式的备份数据文件系统，该系统可以在各种系统（Linux、Windows 或 Mac）上恢复。一旦`mkisofs`命令创建了 ISO 镜像，可以使用`cdrecord`或`growisofs`命令将镜像刻录到 CD 或 DVD。

# 9

## 检查和管理运行中的进程

当一个可执行程序启动时，它会作为一个进程运行，并由你的 Linux 系统进程表管理。Linux 提供了所需的所有工具来查看和更改系统上运行的进程。

`ps`和`top`命令是查看运行中进程信息的绝佳工具。`ps`和`top`有多几十个选项，可以帮助你按照想要的方式查看进程信息。`pgrep`命令可以进一步找到你需要的进程。

还有诸如`nice`和`renice`等命令，用于提高或降低进程的优先级。你可以将进程移动到后台运行（`bg`命令）或返回前台（`fg`命令）。

向进程发送信号是改变其行为或彻底杀死它的方法。通过使用`kill`和`killall`命令，你可以分别通过 PID 或名称向进程发送信号。你还可以向进程发送其他信号来执行如重新读取配置文件或继续运行已停止进程等操作。
