
## HAL 配置：`/etc/hal/fdi` 和 `/usr/hal/fdi`

关于设备的信息和管理设备的策略存储在 `/etc/hal/fdi` 和 `/usr/hal/fdi` 目录下的设备信息中。你可以在这些地方设置属性，例如用于 `/etc/fstab` 中 CD-ROM 的属性。

Fedora 上的 HAL 实现通过关注存储方法而非特定设备来配置存储管理。卷（Volume）属性定义了可以使用的操作和有效选项。特殊调用直接执行操作，例如用于挂载媒体的 `hal-storage-mount` 或用于移除媒体的 `hal-storage-eject`。

## 设备信息文件：fdi

设备属性由 `/usr/share/hal/fdi` 和 `/etc/hal/fdi` 目录下的设备信息文件 (`fdi`) 处理。`/usr/share/hal/fdi` 目录用于存储发行版（在此例为 Fedora）提供的配置，而 `/etc/hal/fdi` 用于设置用户管理配置。这两个目录中都列出了 HAL 管理的不同类型信息的子目录，例如“策略（policy）”，其子目录包含了关于如何管理设备的策略。这些文件被称为设备信息文件，具有获取设备信息的规则，以及检测和为可移动设备分配选项的规则。设备信息文件的扩展名为 `.fd`，例如 `storage-methods.fd`。例如，`policy` 目录下有子目录：`10vendor` 和 `20thirdparty`。在 Fedora 3 中，`10vendor` 替换了 `4default`。该目录包含用于存储设备的 `20-storage-methods.fd` 文件。在这里你将找到指定可移动设备（如 CD-ROM）选项的属性。目录以数字开头；数字越小的越读取。与 `with` 不同，本地属性将覆盖任何之前的属性设置，因此编号较高的目录及其持有的 fd 文件具有更高的优先级。这就是为什么默认策略在 `10vendor` 中，而覆盖默认设置的用户策略位于编号更高的目录中（如 `30user`），以及第三方策略 `20thirdparty`。

设备信息文件中设置了三类设备信息目录，分别对应每种信息：信息（information）、策略（policy）和预探测（preprobe）。

- `information` 目录用于关于设备本身的信息。
- `policy` 目录用于设置策略，例如存储策略。存储设备的默认策略位于 `10vendor` 目录下的 `20-storage-methods.fd` 文件中。
- Preprobe：`preprobe` 目录处理作为异常驱动器或驱动配置的困难设备，例如 `preprobe/10vendor/10-ide-rives.fdi` 中的设备。它包含了在设备探测之前所需的信息。

这些子目录内部是所有指示设备信息文件来源的其他子目录，例如 `vendor`、`thirdparty` 或它们的优先级。这里列出了某些关键文件：

- `information/10freesktop` 由 freedesktop.org 提供的信息
- `policy/10vendor` 默认策略（由系统管理员和操作系统发行版设置）
- `preprobe/10vendor` 困难设备的预探测策略

## 属性（Properties）

设备信息通过属性条目体现。这些条目由键值对组成，其中键指定设备及其属性，值是该属性的值。有许多类型的值，例如布尔值 `true/false`、作为目录挂载点使用的字符串值，或整数值。

属性按元数据（metadata）、物理连接、功能和策略进行分类。元数据提供有关设备的通用信息，例如它使用的总线、其 HAL ID。元数据属性以 `info` 键开头，例如 `info.bus`。物理属性描述物理连接以及总线使用的名称。IDE、PCI 和 SCSI 总线信息列在 `ide`、`pci` 和 `scsi` 键中。`usb_device` 属性用于 USB 总线：例如 `usb_device.number`。

功能属性适用于特定类型的设备。在这里你会找到存储设备的属性，例如 `storage.cdrom` 键，指定光设备是否具有写入能力。例如，`storage.cdrom.cdr` 键设置为 `true`，表示光驱驱动器可以写入 CD-R 光盘。

策略本身并不是属性。它们指示了如何处理设备。实际上，这些指令指导了执行任务时调用的程序。存储媒体的策略使用 `Volume` 属性进行处理，指定了要使用的方法（调用）和作为挂载选项的有效选项。HAL 使用 `/usr/share/hal/scripts` 中的脚本直接管理方法。以下来自 `20-storage-methods.fdi` 文件的简要条目首先指定要采取的操作和要执行的调用 `hal-storage-mount`。

```xml
<append key="Volume.method_names" type="strlist">Mount</append>

<append key="Volume.method_excepts" type="strlist">hal-storage-mount</append>
```

挂载选项使用 `volume.mount.valid_options` 指定，此处所示用于 `ro`（只读）。这些选项是当执行挂载调用时将使用的选项。

```xml
<append key="volume.mount.valid_options" type="strlist">ro</append>
```

表 32-6 列出了若干种常用的策略指令。

## 设备信息指令（Device Information Directives）

属性定义在设备信息文件列出的指令中。如所述，设备信息文件具有 `.fdi` 扩展名。设备包含在 `<` 和 `>` 符号之间。有指令：

- `merge` 指令（合并）将一个新属性合并到设备信息数据库中。
- `append` 指令（追加）将添加或修改数据库中已存在的该设备的属性。
- `match` 指令（匹配）将测试设备信息值。

指令将包含一个类型，用于指定要存储的值类型，如 `string`、`int` 和 `double`。`copy_property` 类型将复制一个属性。

| 属性 | same |
|---|---|
| volume.method_excepath | 为设备运行的调用脚本 |
| volume.policy_desired_mount_point (string) | 存储设备的首选挂载点 |
| Volume.mount.valid_options.* (bool) | 用于特定设备的挂载选项，其中 * 可以是任何挂载选项，如 noauto 或 exec |
| volume.method_names | 要采取的操作 |
| volume.policy_mount_filesystem (string) | 挂载卷时使用的文件系统 |
| volume.mount.valid_mount_options.* (bool) | 卷的默认挂载选项，其中 * 可以是任何挂载选项，如 noauto 或 exec |

**表 32-6** HAL 存储策略

# 736 第 VI 部分：系统管理

对 `storage-methods.fdi` 文件的讨论展示了合并（merge）和匹配（match）指令的几个示例。

## storage.fdi

`/usr/hal/fdi/policy/1osmount` 目录下的 `dev-storage-methods.fdi` 文件列出了移动存储设备的策略。这里是你实际指定存储卷（例如 CD-ROM）选项的地方。该文件分区组织，从特定类型的设备到标准默认。使用键（Keys）来定义选项，例如 `volume.valid_options`，它将指定 CD-ROM 等存储设备的挂载选项。键也用于指定热插拔等异常情况。

`dev-storage-methods.fdi` 文件从默认属性开始，并列出特定类型设备的属性。除非在后面的键中重新定义，否则默认值将保持有效。你将在存储卷上列出的选项将适用于 CD-ROM。例如，`noexec` 选项被设置为有效的默认值。以下内容将 `noexec` 设置为存储设备的默认挂载选项。还有针对 `ro` 和 `quiet` 的项。代理（agent）添加了策略引擎。

```
<append key="volume.valid_options" type="strlist">noexec</append>
```

存储设备的默认挂载目录由挂载脚本 `hal-storage-mount` 设置。目前为 `/media`。默认挂载点是 `disk`。HAL 将尝试使用 `Volume` 属性生成挂载点。

以下示例管理磁盘。此类磁盘无法构建只能弹出。要确定可能的动作，HAL 对 `Volume` 属性使用 `method_names`、`method_signatures` 和 `match`（为了提高可读性，示例中删除了键的 `org.freedesktop.Hal` 前缀，即 `org.freedktop.Hal.Volume.method_names`）。
