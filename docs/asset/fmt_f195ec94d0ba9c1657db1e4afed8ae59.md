
使用共享协议（`SUSP`）是 Rock 交换协议（`Rock Interchange Protocol`）中标识的记录。`SUSP` 记录可以包含 Unix 风格的属性，如所有权、长文件名和特殊文件（如字符设备和链接）。

`Joliet` 目录记录以 Windows 系统可以识别的格式存储较长的文件名。

分层文件系统（`HFS`）扩展允许 ISO 看起来像一个 `HFS` 文件系统，这是 Macintosh 的原生文件系统。同样，可以通过不同的方式添加数据分支和资源分支（Data and Resource forks），以便被 Mac 读取。

当你准备创建 ISO 镜像时，请考虑你最终需要在哪里通过使用 `mkisosfs` 备份来访问文件（Linux、Windows 或 Mac）。一旦镜像创建完成，就可以以不同的方式使用，最明显的方法是将镜像刻录到 CD 或 DVD 中。

除了可以将 Linux 文件系统的全部或部分制作到便携式介质上之外，`mkisosfs` 对于创建 CD/DVD 也很有用。它通过向镜像中添加启动信息，可以启动 Linux 内核或其他操作系统，从而绕过计算机的硬盘。

> 尽管你可以在 Fedora 中仍然使用 `mkisosfs` 命令，但 `mkisosfs` 是指向 `genisoimage` 的指针。`genisoimage` 命令源自 `mkisosfs`，而 `mkisosfs` 是 `cdtools` 软件包的一部分（详见 http://cdrecord berilios.de）。`genisoimage` 的开发是 `cdkit` 项目（www.cdkit.org）的一部分。

由于 Linux 用户将个人文件存储在主目录中，使用 `mkisosfs` 备份文件的一种常用方法是备份 `/home` 目录的所有内容。以下是使用 `mkisosfs` 从 `/home` 目录下的所有文件和目录创建 ISO 镜像的示例。

```
# cd /tmp
# mkisosfs -o home.iso /home          创建基础 ISO9660 镜像
# mkisosfs -o home2.iso -J -R /home      添加 Joliet Rock Ridge 扩展
# mkisosfs -o home3.iso -J -R -hfs /home 同时也添加 HFS 扩展
```

在这三个示例中，`/home` 目录下的所有文件和目录都被添加到 ISO 镜像（`home.iso`）中。第一个示例没有扩展，因此所有文件名都转换为 DOS 风格的命名（8 个字符）。第二个示例使用了 Joliet 和 Ridge 扩展，因此文件名和权限在当你在 Linux 或 Windows 系统上挂载该 ISO 时，看起来像它们在原始 Linux 系统上显示时一样。最后一个示例还让镜像上的文件可以从 Mac 文件系统读取。

你可以向镜像中添加多个源。以下是一些示例：

```
# mkisofs -o home.iso -R -J music/ docs/ \ 多个目录/文件
chris.pdf -J /spool/mail
# mkisofs -o home.iso -J \ 在镜像上嫁接文件
graft-Pictures /var/pics/ \
home/chris
```

第一个示例显示了将各种文件和目录组合并放置在 `/home` 镜像的根目录下。第二个示例将 `/var/pics` 目录嫁接到 `/home/chris/Pictures` 目录。结果是，CD 镜像中的 `/Pictures` 目录将包含 `/var/pics` 目录的所有内容。

在 ISO 镜像的头文件中添加信息可以帮助你以后识别该镜像的内容。如果镜像是在线保存或分发的，而没有物理磁盘可以写入，这非常有用。以下是一些示例：

```
# mkisofs -o /tmp/home.iso -R - \ 向头文件中添加信息
-p www.handsonhistory.com \ \
-publisher "Swan Folk Art Center" \ \
-V "WebBackup" \
-A "mkisofs"
-volset "1 of 4 backups, July 30, 2007" \ \
/home/chris
```

在下面的示例中，`-p` 表示制者 ID（preparer ID），它可以包含电话号码、邮寄地址或用于联系 ISO 镜像制者的网站。使用 `-publisher` 选项，你可以指定一个 128 字符的制者描述。`-V` 表示卷 ID（volume ID）。卷 ID 非常重要，因为在 Linux 系统中，当插入 CD 时，此卷被用于挂载。在上面所示的命令行中，在 Fedora 和其他 Linux 系统中，CD 将挂载在 `/media/WebBackup`。`-A` 选项可以识别创建 ISO 镜像的应用程序。`-volset` 选项可以包含关于一组 ISO 镜像的信息字符串。

当你创建了 ISO 镜像后，在刻录之前，你可以检查镜像并确保你可以访问其中的文件。以下是几种检查它的方法：

```
# volumename home.iso 显示卷名
WebBackup
# isinfo -d -i home.iso 显示头信息
CD-ROM is in ISO 9660 format
System id: LINUX
```

Volume id: WebBackup

Volume set: All material on November 2, 2007

Publisher id: Swan Folk Art Center

# 第 8 章：备份与可移动介质

## 使用 growisofs 制作和刻录 DVD

使用 `growisofs` 命令，你可以将收集文件并为 ISO 镜像（`mkisos`）以及将该镜像刻录到 DVD（`cdrecord`）这两个步骤合并为一个。除了节省一个步骤外，`growisofs` 命令还提供了默认保持会话开启直到你将其关闭的优势，因此你不需要对多刻会话进行任何特殊操作。

以下是一个用于多刻会话的 `growisofs` 命令示例：

```bash
# growisofs -Z /dev/dvd -R j /home/chris    主并刻录到 DVD
# growisofs -Z /dev/dvd -R j /home/francois  添加到刻录
# growisofs -M /dev/dvd=/zero                关闭刻录
```

如果你想在创建 ISO 镜像时添加选项，可以简单地在命令行中添加 `mkisos` 选项。（例如，参见上述示例中是如何添加 `-R` 和 `-J` 选项的。）

如果你想使用 `growisofs` 刻录 DVD 镜像，可以使用 `-dvd-compat` 选项。例如：

```bash
# growisofs -dvd-compat -Z /dev/dvd-image.iso 将 ISO 刻录到 DVD
```

`-dvd-compat` 选项可以在某些多会话 DVD 刻录过程中提高与不同 DVD 驱动器的性。

## 总结

Linux 及其前身 Unix 系统通过组合每个处理离散功能的命令来处理数据备份。你的关键数据备份仍然可以通过这种方式进行。你使用的许多工具现在比以前任何时候都更安全、高效。

磁带存档工具已经远远超出了其制作数据磁带备份的原始工作。由于几乎每个 Linux 和 UNIX 系统都包含 `tar`，它已成为软件包打包和将数据备份到压缩存档的标准工具。这些存档随后可以通过各种方式进行传输和存储。

要通过网络将数据移回其他机器器，你可以使用 OpenSSH 工具的远程功能（如 `ssh`）。你还可以使用一个名为 `rsync` 的优秀工具。通过 `rsync`，你可以通过备份已更改的文件（或文件的部分）来节省资源。

廉价的 CD 和 DVD 已成为个人和小型办公室备份的流行介质。`mkisos` 命令可以创建 ISO9660 格式的备份数据文件系统，这些可以在多种系统（Linux、Windows 或 Mac）上恢复。一旦 `mkisos` 创建了 ISO 镜像，可以使用 `cdrecord` 或 `growisofs` 命令将镜像刻录到 CD 或 DVD。

## 检查和管理运行中的进程

当一个可执行程序启动时，它作为一个进程运行，由你的 Linux 系统进程表管理。Linux 提供了查看和更改系统上运行进程所需的所有工具。

`ps` 和 `top` 命令是查看运行进程信息的绝佳工具。`ps` 和 `top` 实际上有几十个选项，可以帮助你按照你想要的方式查看进程信息。`grep` 命令可以进一步帮助找到你需要的进程。

诸如 `nice` 和 `renice` 等命令用于提高或降低进程的优先级。你可以将进程移动到后台运行（`bg` 命令）或返回前台（`fg` 命令）。

向进程发送信号是改变其行为或将其完全杀死的方法。通过使用 `kill` 和 `killall` 命令，你可以分别通过 PID 或名称向进程发送信号。你还可以向进程发送信号以执行如重新读取配置文件或继续已停止的进程等操作。
