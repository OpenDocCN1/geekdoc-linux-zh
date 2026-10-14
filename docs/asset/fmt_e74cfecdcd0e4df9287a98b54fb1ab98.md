
```
aha152x=0x140,11,7,1 hdb-ide-scsi hdd-ide-scsi"
root = /dev/hda2

image = /boot/vmlinux.safe
label = linux-safe
append="reserve=0x340,32,ether=9,0x340,eth0
aha152x=0x140,11,7,1 hdb-ide-scsi hdd-ide-scsi"
root = /dev/hda2

image = /boot/vmlinux-2.2.5-22.orig
label = linux-orig
append="aha152x=0x140,11,7,1 hdb-ide-scsi hdd-ide-scsi"
root = /dev/hda2
```

在你将内核镜像拷贝到 `/boot` 后，执行：

你应该能看到列出的每个启动目标：

```
[root@sloth /]# /sbin/lilo
Added linux-new *
Added linux-safe
Added linux-orig
```

如果有错误，`LILO` 会提示你。现在，你可以继续下一节，“重启”。

## 重启

内核和模块已经构建并安装。在重启之前，为了确保你的新内核按预期工作，请执行几次 `/bin/sync` 命令，以确保所有缓存数据已刷入硬盘。这可能并不是必要的，仅仅是我的某种迷信，但为了保险起见，我会执行三次 `sync`。你可能希望退出任何正在运行的应用程序，并在命令行提示符处使用 `reboot` 命令，或者按 `Ctrl+Alt+Delete`。

当 `LILO:` 提示符出现时，选择你的新内核。如果你将新内核设置为默认启动目标，只需按 `Tab` 键即可获取启动目标列表。你应该看到备份的启动内核 `linux-safe`，以防新内核无法启动。当新内核启动时，监控控制台的输出。它会快速滚动，但你可以使用 `Shift+PageUp` 向上滚动。如果启动失败，通过执行 `/bin/dmesg` 仔细检查控制台输出。你或或少地需要将该命令的输出通过分页器处理。确保你的硬件已被检测到且没有错误信息。最后，启动你的系统。

## 总结

在本章中，你学习了如何配置内核以满足你的需求。由于 Linux 的快速发展，内核版本不断更新。你还学习了如何配置硬件以改进系统。如果你遇到任何问题，可以始终回退到安全内核。此外，由于要配置内核，本章描述了内核可能提供的几种格式，例如 RPM、压缩包和补丁。最后，你学习了如何为 `LILO` 添加条目。如果一切顺利，你将拥有一个可以工作的内核。

# 第三部分 系统管理

## 第15章 硬件配置

有一个 ATAPI 或并行接口的 CD-R/RW。为了使用 CD-R/RW 的写入部分，它必须与 SCSI 接口协议兼容。如果你有一台 SCSI CD-R/RW，那么你在这里不需要做任何操作。如果你有一个 ATAPI 或并行接口 CD-R/RW，你必须为该设备开启 SCSI 仿真支持。首先，让我们看看 CD 刻录软件能否检测到你的硬件。请确保已安装了 `cdrecord` 工具。它是 TurboLinux 6.0.4 的一部分，很可能已经安装了。如果没有，请现在使用 `turbopkg` 安装它。在提示符处输入列表 15-1。

### 列表 15-1

```
[root@/root]# /usr/bin/cdrecord -scanbus
Cdrecord release 1.8a35 Copyright (C) 1995-1999 Jürgen Schilling
Using libscg 'shily-0.1'
scsisbus0:
  0,0,0 'HP' 'CD-Writer 7200 '3.01'
  Removable CD-ROM
    0,1,0 1 *
    0,2,0 2 *
    0,3,0 3 *
    0,4,0 4 *
    0,5,0 5 *
    0,6,0 6 *
    0,7,0 7 *
```

该工具扫描你的 SCSI 设备以寻找 CD-R/RW 设备。在前面的示例中，它找到了我的 HP CD-Writer 7200i。这实际上是一个被我配置为 SCSI 设备运行的 ATAPI 设备。我的操作如下：

1. 编辑 `/etc/modules.conf`：
   ```
   alias scd0 sr_mod
   alias scsi_hostadapter adapter ide-scsi
   options ide-cd ignore=hdd
   ```
2. 按照以下语法编辑：
   ```
   <CD-R/RW device>=ide-scsi
   ```
   其中 `<CD-R/RW device>` 是与你的 CD-R/RW 驱动器关联的 IDE 设备。这是来自 `/etc/lilo.conf` 的一个具体示例：
   ```
   image=/boot/mlinuz
   label=linux
   root=/dev/hdal
   initrd=/boot/initrd
   append="aha152x=0x1440,11,7,0 hdd=ide-scsi"
   read-only
   ```

在第一步中，我配置了内核在访问 `/dev/scd0` 时加载 `sr_mod`。然后我指定了 `scsi_hostadapter ide-scsi`。最后，我指示 CD-R/W（即 `/dev/hdd`）不应被 `ide-cd` 驱动程序接触。我还在我的 `lilo.conf` 中显式地将其设置为启动参数 - `hdd=ide-scsi`。这可以防止 IDE 驱动程序处理它。完成这些设置后，再次执行 `cdrecord /scanbus` 命令。它现在应该能识别你的驱动器了，你应该看到类似于列表 15-1 的输出。你可以通过向 `/etc/rc.d/rc.modules` 添加以下行来在你的系统上加载 `ide-scsi` 模块：

```
echo "Inserting IDE-SCSI module..."

  modprobe ide-scsi
```

### 磁盘格式、扩展与挂载

大多数 CDR 都是用 ISO-9660 文件系统格式化的。这种格式允许旧的 MS-DOS 风格文件名，即包含 8 个字符的名字和 3 个字符的扩展名。ISO-9660 文件系统有两个流行的扩展。Rock Ridge 扩展允许长文件名和 UNIX 文件属性。微软还定义了一个名为 Joliet 的扩展，它也支持长文件名。你的 Linux 内核必须内置对 Joliet 的支持。默认的 TurboLinux 6.0.4 内核已启用了“Microsoft Joliet CD-ROM 扩展”。如果你正在创建自定义内核，请参考内核配置中的“文件系统”部分来启用此选项。

![](img/494a93e1dbdce90cc5cca36f1589d45f_307_0.png)

你可能会发现， `/dev` 中为你的 CD-ROM 和 CD-RW 创建一个符号链接非常方便且更有意义。

```
/dev/cdrom -> /dev/hdc

/dev/cdwriter -> /dev/scd0
```

在内核识别你的 CD 设备后，在 `/etc/fstab` 文件中为它们创建一个条目。你可以使用 `turbofscfg` 或直接编辑 `/etc/fstab`。指定文件系统类型为 `iso9660`。如果你使用 `autofs` 服务，可能希望为你的 CD-WRITER 添加一个条目并重启服务。

### CD-ROM 应用

由于 CD-ROM 被处理得类似于硬盘，因此不需要专门的软件来使用该驱动器。如果你想在驱动器中使用音频 CD，Linux 有许多可用的 CD 播放器。如果你可以访问互联网，应该考虑使用支持 CDDB 的播放器。它会将 CD 信息下载到播放器，这样你就可以看到 CD 上每条轨目的名称和艺术家了（http://www.cddb.com/）。

### 刻录 CD 的工具与应用

今天有很多工具可以帮助你刻录 CD。最少的情况下，你需要 `mkisofs` 或 `mkhfs`（用于混合 CD）、`cdrecord` 和 `cdrdao`。这些是你需要的必备命令行工具。TurboLinux 默认带有 `mkisofs` 和 `cdrecord`。`mkisofs` 工具创建写入到 CD 的镜像，而 `cdrecord` 写入该镜像。你可以使用 `mkisofs` 为 Macintosh/Apple 系统创建一个 HFS/ISO9660 混合文件系统。`cdrdao` 是刻录 CD 的另一种备选工具（http://www.cd.org/cdrdao）。有很多图形化程序可以作为这些工具的前端，或者取代它们的功能。这里有几个你可能感兴趣的：

- `X-CD-Roast`
- `Burnit`
- `Gcomburst`

刻录 CD 的基本步骤如下：

1. 使用你想要写入 CD 的文件创建一个 ISO-9660 文件系统。
2. 通过使用回环设备（loop device）挂载文件系统来验证其是否良好。
3. 将镜像写入 CD-R/RW。

第一步是创建 CD 镜像。要做到这一点，使用 `mkisofs`。基本格式如下：
