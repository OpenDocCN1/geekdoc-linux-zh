
ATA（附加附加）是常用 IDE 接口的官方 ANSI（美国国家标准学会）名称，通常用于将硬盘驱动器连接到 PC。ATAPI（ATA 包接口）用于控制 CD-ROM 驱动器和磁带驱动器等存储设备。虽然 ATAPI 较新，但它正迅速成为 CD-ROM 驱动器最流行的接口类型。原因是 ATAPI 基于 ATA（或 IDE）接口，不需要任何昂贵的控制卡或电缆。此外，ATAPI CD-ROM 可以简单地作为在与 PC 硬盘连接在同一接口上的第二个驱动器连接。这意味着 ATAPI CD-ROM 驱动器不需要单独接口。

Linux 内核包含一个 ATAPI 驱动程序，可与任何 ATAPI CD-ROM 驱动器配合。ATAPI CD-ROM 驱动器可用许多供应商，例如 Aztec、Mitsumi、NEC、Philips、Sony 和 Toshiba。如今，大多数 PC（如 Gateway 的电脑）都配置了 ATAPI 驱动器。

### SCSI CD-ROM 驱动器

Linux 支持连接到 SCSI 控制器的 SCSI CD-ROM 驱动器（更多信息见第 11 章）。唯一的限制是 SCSI CD-ROM 驱动器的块大小（用于数据传输）应为 512 或 2048 字节，这涵盖了市场上绝大多数 CD-ROM 驱动器。

某些 CD-ROM 驱动器带有修改过的接口。SCSI CD-ROM 驱动器可用许多供应商，如 Plextor、Sanyo 和 Toshiba。

### 专有 CD-ROM 驱动器

虽然 ATAPI 和 SCSI CD-ROM 驱动器分类且在 Linux 中运行良好，但对于带有专有接口的 CD-ROM 驱动器情况变得复杂得多。以下是一些混乱来源：

- 某些厂商（如著名的 Creative Labs）销售带有所有类型接口的 CD-ROM 驱动器：ATAPI、SCSI 以及声卡上的专有接口。因此，仅凭名称没有意义；你必须知道 CD-ROM 的接口类型。
- PC 厂商有时会将 CD-ROM 接口归类为 IDE，尽管该接口是专有的。与 IDE（或 ATAPI）接口一样，专有 CD-ROM 接口廉价且流行。

正如你所料的，专有 CD-ROM 接口流行是因为它们比 SCSI 简单得多，而在 ATAPI 出现之前 SCSI 是主要的替代方案。由于廉价 ATAPI 的流行，大多数新 PC 不再使用专有接口。然而，由于专有 CD-ROM 接口可以低成本构建在声卡中，某些 Linux 用户可能拥有专有 CD-ROM 驱动器的 PC。

表 12-1 列出了具有专有接口的 CD-ROM 驱动器以及支持这些驱动器的驱动程序名称。

| 驱动程序 | CD-ROM 驱动器 |
|---|---|
| aztcd | Aztech CDA268, Orchid CDS-3110, Okano/Wearnes CDD-110, Conrad TXC, CyPROM CR520ie/CR940ie |
| cdu31a | Sony CDU31A/CDU33A |
| cm206 | Philips/LMS CM 206 |
| gscd | GoldStar R420 |
| isp16 | 连接到 ISP16、MAD16 或 Mozart 声卡接口的 CD-ROM 驱动器 |
| mcd | Mitsumi CRMC LU005S, FX001 |
| optcd | Optics Storage Dolphin 8000AT, Lasermate CR328A |
| sbpcd | Matsushita/Panasonic (Panasonic CR-521, CR-522, CR-523, CR-562, 和 CR-563), Kotobuki, Creative Labs (CD-200), Longshine LCS-7260, Teac CD-55A |
| sjcd | Sanyo H94A |
| sonycd535 | Sony CDU-535/CDU-531 |

## 第 12 章：CD-ROM 驱动器与声卡

### CD-ROM 故障排除

你需要一个可以在 Linux 下正常工作的 CD-ROM 驱动器，以便从本书附带的 CD-ROM 安装 Linux。初始 Linux 内核带有所有支持的 CD-ROM 驱动器模块，因此只要你的 CD-ROM 驱动器被 Linux 支持，就不应该遇到任何问题。请记住，重要的是 CD-ROM 驱动器的接口而不是品牌。例如，任何带有 IDE 接口的 CD-ROM 都能在 Linux 下都能工作，因为 Linux 支持 IDE 接口。

如果在重新编译内核后 Linux 似乎没有识别 CD-ROM 驱动器，请尝试以下步骤解决问题：

- 1. 如果你已经在支持 CD-ROM 驱动器的情况下重新编译了内核，请验证你确实正在运行新内核。要查看版本号，使用 `uname` 命令。以下是 `uname` 命令的典型输出：

```
Linux localhost 2.0.32 #1 Fri Jan 30 07:08:01 EST 1998 i5886 unknown
```

`uname` 命令的此输出显示了内核的版本号以及内核编译的日期。如果此日期与你重新编译内核的日期不符，你可能没有运行新内核。请按照第 2 章概述的步骤操作，确保你确实安装了新内核。一个常见问题是忘记重启，所以也尝试这一步。

- 2. 查看 `/proc/devices` 文件的内容以验证 CD-ROM 设备是否存在。使用以下程序查看 `/proc/devices` 的内容：

```
cat /proc/devices
Character devices:
1 mem
2 pty
3 tty
4 ttyp
5 cua
7 vcs
10 misc
```

```
Block devices:
1 ramdisk
2 rd
3 ide0
7 loop
8 sd
9 md
22 ideal
```

此列表对应于系统上的设备。你应该在块设备列表中寻找 CD-ROM 设备。我知道我的 CD-ROM 驱动器连接在辅助 IDE 接口上。两个 IDE 接口对应于 `/proc/devices` 中的设备 `ide0` 和 `ideal`。因为 `ideal` 出列表中，我知道 CD-ROM 驱动程序在内核中。

如果你将 CD-ROM 连接到 Sound Blaster Pro 或兼容接口，请查找设备号为 25 且名为 `spbcd` 的设备。

如果你没有看到对应于 CD-ROM 驱动器的设备，说明你没有正确配置内核以包含 CD-ROM 驱动程序。请重新配置并重新编译内核，确保包含对你的 CD-ROM 驱动器的支持。

- 3. 验证 CD-ROM 驱动程序在系统启动时检测到了 CD-ROM 驱动器。使用 `dmesg | more` 查看启动信息，查看是否有某行报告发现了 CD-ROM 驱动器。在我带有 ATAPI CD-ROM 驱动器的系统上，信息如下：

```
hdc: FX400_02, ATAPI1, cdrom drive
```

如果你没有找到关于 CD-ROM 驱动器的启动信息，请确保 CD-ROM 已物理安装。对于外部 CD-ROM 驱动器，确保驱动器已通电且电缆已连接。检查任何驱动器 ID 或跳线，确保它们设置正确。你可能希望先确保 CD-ROM 驱动器在 DOS 下工作，或者看到 CD-ROM 物理上正常。接下来，验证你是否已经在支持正确的 CD-ROM 接口的情况下重新编译了内核。

- 4. 验证你可以从 CD-ROM 驱动器读取数据。尝试以下命令并观察 CD-ROM 的活动灯是否亮起（应该会亮）以及是否有任何错误信息（不应该有）：

```
dd bs=1024 count=5000 < /dev/cdrom > /dev/null
5000+0 records in
5000+0 records in
```

`/dev/null` 设备就是你所谓的“垃圾桶”。重定向到 `/dev/null` 的输出直接消失。

如果 `dd` 命令不起作用，则 CD-ROM 设备文件可能没有设置正确。使用 `ls -l` 命令查看你的 CD-ROM 设备信息。例如，对于在辅助 IDE 接口上的 ATAPI CD-ROM 驱动器，我将如下查看 `/dev/hdc`：

```
ls -l /dev/hdc
brw- root 1 disk 22,0 Feb 4 1995
```

注意数字 22 和 0 是主设备和次设备号。这些数字需要修正。（本章后续章节列出了特定 CD-ROM 驱动程序的设备号）。

- 5. 验证你可以挂载 CD-ROM。将一张良好的 CD-ROM（例如书中的 CD-ROM）放入 CD-ROM 驱动器，并尝试使用以下命令挂载它：

```
mount -t iso9660 r /dev/cdrom /mnt/cdrom
```

如果你能通过 `dd` 命令从 CD-ROM 驱动器读取，但无法挂载 CD-ROM，你可能在配置内核时没有开启 ISO-9660 文件系统的支持。要验证当前支持的文件系统，请使用以下命令：

```
cat /proc/filesystems
ext2
msdos
smbfs
iso9660
```
