

```bash
# "/seyon.ge/script.sample
echo "Login Script"
waitfor "login": 10
transmit "moser*M"
waitfor "word": 3
transmit "asd4JK*M"
```

## 15.7 写入 CD-ROM

本节介绍了 Linux 下的 ISO 镜像创建和 CD-ROM 刻录。重点将是 ISO 9660 格式的单会话数据 CD，而其他变体（音频 CD、多会话 CD）将不被考虑。

首先，是重要步骤的概述：

- 在刻录 CD-ROM 之前，你需要准备数据，即为为 CD-ROM 文件系统处理过的数据创建一个 ISO 镜像。通常使用 `mkisofs` 命令来实现这一目的。
- 对于刻录 CD-ROM，你可以在 `cdwrite`（旧版，不再开发）和 `cdrecord` 程序之间进行选择。如果这些程序中都不支持你的 CD-R 驱动器，你也可以在 Windows 或其他操作系统下创建 CD；大多数 CD-R 程序都能写入用 `mkisofs` 创建的 ISO 镜像。
- 取决内核版本和 SCSI 硬件，在刻录 CD-ROM 之前，可能需要对内核进行补丁并重新编译。
- 最后，你应该检查 CD-ROM。有许多程序可用，可以用于读取所有数据块或所有文件，以便将 CD-ROM 的内容与现有文件系统进行比较。
- 除了面向命令的程序 `mkisofs` 和 `cdrecord`，你也可以使用 X 程序 `xcdrecord`，它允许你在用户友好界面的帮助下完成这两个步骤。

> 本节所讨论的程序的最新版本可以在互联网上找到。
http://ftp.ge.ucl.ac.uk/pub/mkhfs
http://ftp.fokus.gmd.de/pub/unix/cdrecord/
http://www.fh-muenchen.de/home/ze/rz/services/projects/xcdrecord

## 创建和测试 ISO 镜像

创建 ISO 镜像最简单的方法是你想原样复制一张数据 CD（不是音频 CD！）时：

```bash
root# dd if=/dev/cdrom of=/usr/local/iso.img bs=2048
```

```bash
mkisofs [options] -o iso_file directory
```

通常情况下是，你首先在一个目录中准备好新 CD-ROM 的数据，随后生成 ISO 镜像。这正是 `mkisofs` 所完成的：该命令创建一个包含目录中所有文件的文件，该文件按照 ISO-9660 规范格式化（可选带有 Rockridge 扩展）。

- 带有 `#` 或以 `~` 结尾的文件也会被考虑。通常并非如此，因为此类文件大多是备份文件。
- 指定的文件被存储为引导镜像。在计算机启动时，该文件会被自动执行（前提是 BIOS 配置正确）。文件的大小必须与 3.5 英或 5.25 英 英软磁盘能容纳的内容完全对应（1.2、1.44 或 2.88 MBytes）。
- 此选项指定了所谓的引导目录（boot catalog）存储在 CD上的文件名。该目录由 `mkisofs` 创建。在命名时，你只需确保它与现有文件没有冲突。（`mkisofs` 的手册页建议使用如 `boot.catalog` 的名称）。
- ISO 标准允许最多八级目录。`mkisofs` 通常遵循这一标准，并在需要时修改目录层次结构（以及受影响的文件名）。`-d` 选项可以防止此操作；但在某些要求严格遵守 ISO 标准的系统中，这可能会导致问题。
- 符号链接会被跟踪，即指定的文件或子目录的内容将被包含在 ISO 镜像中。（如果不使用此选项，只有链接本身存储在 ISO 镜像中。然而，符号链接只能映射到带有 Rockridge 扩展的 CD）。
- ISO 镜像存储在 `file` 文件中。
- ISO 镜像使用 Rockridge 扩展来存储长文件名信息。
- 类似于 `-r`，但所有文件的 UID 和 GID 都设置为 0（对应于 root）。同时，所有 R 访问位都被设置；如果原始文件中至少设置了一个 X 访问位（另请参见第 444 页的 `chmod`）。
- 文件 `TRANS.TBL` 被写入每个目录；它指定了具有长 Unix 文件名的文件可以被找到的短 ISO-9660 名称。（这对于允许在 DOS/Windows 下也关联到长文件名是必要的。）

## 刻录 CD-ROMS

-V name
此选项指定卷 ID（volume ID），即 CD-ROM 的名称（最多 32 个字符），例如在 Windows 下显示。

## 示例

```bash
root# mkisofs -o /mnt/dos/iso.img -r -T -V Linux_3_98 /master
```

上述命令将 /master 目录中的所有文件写入文件镜像 `image.raw`。出于空间考虑，该文件存储在挂载到文件系统挂载点 mnt/dos 的分区上。master 本身并不是 ISO 镜像中的目录。

```bash
root# mkisofs -o /mnt/dos/iso.img -r -T /master \
> -b images/boot.img -c boot.catalog
```

如上所述，这次创建了一个可引导的 CD。

> 如果你没有使用 `-r` 选项，这里有一些提示：确保 master 目录中的所有文件都属于 root 并且对所有人可读！

```bash
root# chown -R root.root /master
root# chmod a+xr /master
```

## 测试 ISO 镜像

只要你在编译内核时开启了 Loopback 设备支持（块设备），或者相应的模块 `loop.o` 可用并可以通过 `insmod` 激活，你就可以将新创建的 `image.raw` 只读地挂载到文件系统中：

```bash
root# mkdir /iso-test
root# mount -t iso9660 -o loop,ro /mnt/dos/image.raw /iso-test/
```

你现在可以使用 `iso-test` 目录测试未来 CD-ROM 的内容（权限、TRANS.TBL 等）。你需要使用 2.0.31 或更高版本的内核——否则 Linux...

## 混合 CD

混合 CD 包含数据本身；然而它们允许根据操作系统访问不同的文件系统。在 Macintosh 上使用 HFS 文件系统；在 Windows 95/NT 下使用 Jol 扩展；在 Unix 下使用 Rockridge 扩展。因此，混合 CD 允许（几乎）所有操作系统使用文件名。

## 工具与实用程序

-h 创建带有 HFS 信息的混合 CD（Macintosh）。
-j 使用 Joliet 扩展（Microsoft）。

## 使用 cdrecord 刻录 CD

`cdrecord` 将格式化正确的镜像传输到 CD-R 驱动器。原则上，`cdrecord` 多会话能力，即 CD 可以在多个会话中扩展。但此描述限于单会话 CD。

```bash
cdrecord [options] dev=channel,id,lun
```

-driver=name
指定 CD-R 驱动器的类型。通过 `cdrecord driver=help` 显示支持的类型。可以使用 `cdrecord -checkdrive dev=n,n` 来确定现有 CD-R 驱动器的类型。

-dummy
仅模拟刻录过程。非常适合测试！

-eject
在刻录完成后弹出 CD。某些 CD-R 驱动器在刻录下一张 CD 之前需要弹出，即使上一个是使用 `-dummy` 模拟的。

-fs=n
此选项指定了用于硬盘和 CD 之间数据传输缓冲的 FIFO 缓冲区大小。合理值在 2 到 8 MBytes 之间（因此 `fs=2m` 或 `fs=8m`）。

-speed=n
无前缀的此选项指定写入速度（通常为 1、2 或 4）。

-v `cdrecord` 显示当前正在发生的详细信息。

关于指定 CD-R 驱动器的简要信息：`cdrecord` 期望的不是设备名称，而是三个数字的形式：SCSI 总线号（通常为 0）、设备的 SCSI ID，最后是逻辑单元号（LUN，也为 0）。确定这些数字最简单的方法是执行 `cat /proc/scsi/scsi`。

