
# CentOS Linux 管理员命令：手册页第二卷（第 2 卷）

## 献词

本书献给 Michael Kerrisk 及其 Linux 文档项目团队。

编校与编辑：Gareth Morgan Thomas

# CentOS 管理员手册页

# 第二卷

> 名称

`ipmaddr` - 添加、删除和显示多播地址

## 语法概要

```
/usr/sbin/ipmaddr [<operation>] [<args>]
```

## 注意

此程序已过时。替代方案请检查 `ip maddr.`。

## 描述

`ipmaddr` 命令可以执行以下操作之一：

- `add` - 添加多播地址
- `del` - 删除多播地址
- `show` - 列出多播地址

## 相关

`ip(8).`

# IPRCONFIG

> 名称

`iprconfig` - IBM Power RAID 存储适配器配置/恢复实用程序

## 语法概要

```
iprconfig [-e editor] [-k dir] [-c command]
```

```
iprconfig --version --debug --force
```

## 描述

`ipconfig` 用于配置 IBM Power RAID 存储适配器，显示其信息，并执行适配器和磁盘单元恢复。菜单选项有：

- 1. 显示硬件状态。此选项可显示有关连接到系统的 IBM Power RAID 适配器以及其控制的磁盘单元的各种信息。对于每个适配器和磁盘单元，可以使用其 `/dev` 名称、物理位置、描述、供应商/产品 ID 和硬件状态。每个资源旁边有一个 OPT 字段。在任何资源处输入 1，可以获取该资源的详细信息。对于适配器资源，这将显示适配器固件版本和物理位置等。
- 2. 磁盘阵操作。此选项将显示一个包含磁盘阵相关命令的第二个菜单。

**显示磁盘阵状态**用于显示系统上磁盘阵的状态。

**创建磁盘阵**用于创建磁盘阵。

**删除磁盘阵**用于删除磁盘阵。选择此选项将为您提供一个可以删除的磁盘阵列表。

**向磁盘阵添加设备**用于将具有相似容量的设备包含在现有磁盘阵中。此功能目前仅支持 RAID 5 和 RAID 6 磁盘阵。

**高级功能格式化设备**用于将磁盘格式化为 512 字节/扇区，以便在磁盘阵中使用。只有未针对高级功能格式化或虽已格式化但未知是否清零的磁盘可供此功能选择。

**JBOD (512) 格式化设备**用于将磁盘格式化为 512 字节/扇区，以便作为独立磁盘使用。只有未针对 JBOD 功能格式化或已格式化 JBOD 功能且处于“需要格式化”状态的磁盘可供此功能选择。

**热备盘操作**用于创建热备盘，将设备指定为专用热备盘。它也用于删除热备盘，取消预先配置的热备盘。

**非对称访问操作**用于在双控制器环境中选择磁盘阵的哪条路径作为主路径。必须先在适配器上启用非对称访问。并非所有适配器都支持非对称访问，提供支持的适配器可能需要更新微代码。

**强制 RAID 一致性检查**用于对 RAID 阵强制执行一致性检查。所有 ipr 在空闲时都会持续执行后台一致性检查。此选项可强制执行一致性检查。

**迁移磁盘阵保护**用于将阵的 RAID 保护级别更改另一个支持的级别。在某些情况下，这将需要向阵中添加磁盘。3. 磁盘单元恢复操作用于执行以下操作：

并发添加设备用于在运行的系统中并发添加新磁盘。此功能仅由 Serv（机箱）封装支持。

并发移除设备用于在运行的系统中并发移除磁盘。此功能仅由 Serv（机箱）封装支持。

初始化并格式化磁盘单元用于向连接的设备发出 SCSI 命令。单元命令对适配器具有特殊含义，并用作某些错误条件的服务操作。格式化磁盘单元将丢失所有 512 字节/扇区。如果磁盘连接到 ipr 适配器，块大小将不会更改。要更改块大小，请使用磁盘菜单下的格式化选项。

回收 IO 缓存用于修复缓存错误。注意：谨慎使用此选项。这用于丢弃缓存中的数据并可能导致数据丢失。此设计旨在供授权的硬件客户工程师使用。

重建磁盘单元数据通常用于并发维护之后。在故障阵列成员被替换后选择此选项，以将设备重构为活动成员。

电池组资源操作用于显示有关可充电电池组的信息，并强制可充电电池组进入错误状态，以便在故障前更换。注意：一旦对可充电电池组强制错误，写入将被禁用，直到更换电池组。

- 4. SCSI 总线配置操作用于更改可配置的 SCSI 总线属性，例如最大 SCSI 总线速度、SCSI 初始化器 ID 等。
- 5. 驱动配置操作用于更改驱动配置属性，例如 `log_level`。
- 6. 磁盘配置操作用于更改可配置的磁盘属性，例如队列深度。
- 7. 适配器配置操作用于更改可配置的适配器属性，例如双适配器设置。更多信息请参考命令行选项：`primary`, `secondary`, `query-ha-mode`, `set-ha-mode`, `set-loa-asymmetric-access` 和 `set-array-asymmetric-access`。
- 8. 下载微代码用于向 ipr 适配器和连接的 SCSI 磁盘下载微代码。
- 9. 分析日志是一个用于分析 `/var/log/messages` 文件的选项。默认情况下，它将使用 `vi` 作为编辑器打开合并的错误日志文件。可以通过内核消息日志菜单上的选项 6 进行更改。在内核消息日志菜单中选择选项 1 将仅显示 ipr 设备驱动程序记录的最新错误，可能有助于过滤掉一些杂乱。选项 2 将显示 ipr 设备驱动程序记录的所有错误。选项 3 将显示所有内核消息。选项 4 将显示 `ipconfig` 工具记录的错误。这可能对调试问题有用。选项 5 可用于更改工具查找内核消息文件的位置。默认在 `/var/log` 中查找。

### 选项

- `editor`

查看错误日志的默认编辑器。默认编辑器为 `vi`，但可以通过此参数进行更改。

- `-k directory`

内核消息根目录。查找内核消息的根目录。为 `/var/log`。

- `-c command`

命令行，非交互式命令。目前支持的命令包括：

`show-config`

显示 ip 配置。

`show-alt-config`

显示备用 ip 配置信息。

`show-ioas`

显示所有 ip 适配器。

`show-arrays`

显示所有 ip阵列。

`show-battery-info [IOA]`

显示指定 IOA 的缓存电池信息。例如：`ipconfig -c show-battery-info sg5`

`show-details [device]`

显示指定设备的详情。例如：`ipconfig -c show-details sda`

`show-hot-spares`

显示所有配置的热备盘。

`show-of-disks`

显示已格式化为高级功能（Advanced Function）但未配置在阵列或作为热备盘的磁盘。

`show-all-of-disks`

显示所有格式化为高级功能的磁盘。

`show-jbod-disks`

显示所有格式化为 JBOD 功能的磁盘。

`show-slots`

显示系统上所有可磁盘槽。

`status [device]`

显示指定设备的状态。这与“显示硬件状态”（Display hardware status）最后一列显示的状态相同。可以指定 `/dev/sdX` 名称或 `/dev/sgX`。例如：`ipconfig -c status /dev/sda`

`alt-status [device]`

显示指定设备的状态。与上述状态相同，但在正在向设备执行长命令时，会打印该长命令的完成百分比。

`query-raid-create [IOA]`

显示连接到指定 IOA 的可作为 RAID 阵列候选的设备。例如：`ipconfig -c query-raid-create sg5`

`query-raid-delete [IOA]`

显示所有连接到指定 IOA 的可以删除的 RAID 阵列。`ipconfig -c query-raid-delete sg5`

`query-hot-spare-create [IOA]`

显示所有连接到指定 IOA 的可作为热备盘候选的设备。

`query-hot-spare-delete [IOA]`

显示所有连接到指定 IOA 的可以删除的热备盘。

`query-raid-consistency-check`

显示所有可以进行 RAID 一致性检查的 RAID 阵列。

`query-format-for-jbod`

显示所有可以重新格式化为 JBOD 功能的磁盘。

`query-reclaim`

显示所有可能需要回收缓存存储的 IOA。

`query-arrays-raid-include`

显示所有可以包含磁盘以增加容量的 RAID 阵列。

`query-devices-raid-include [array]`

显示所有可以添加到指定阵列以增加其容量的磁盘。

`query-supported-raid-levels [IOA]`

显示指定适配器支持的所有 RAID 级别。

`query-include-allowed [IOA] [raid level]`

某些 RAID 级别允许通过向现有磁盘阵列添加额外磁盘来增加其容量。如果指定的 RAID 级别支持此功能，则向标准输出打印 "yes"，否则打印 "no"。

`query-max-devices-in-array [IOA] [raid level]`

打印指定的 RAID 适配器上，指定 RAID 级别下 RAID 阵列中允许的最大设备数。

`query-min-devices-in-array [IOA] [raid level]`

打印指定的 RAID 适配器上，指定 RAID 级别下 RAID 阵列中允许的最少设备数。

`query-mult-in-array [IOA] [raid level]`

打印指定的 RAID 适配器上，指定 RAID 级别下 RAID 阵列所需的最小设备数。

`query-supp-stripe-sizes [IOA] [raid level]`

打印指定的 RAID 适配器上，指定 RAID 下 RAID 阵列支持的所有条带大小。条带大小以 KB 为单位打印。

`query-recommended-stripe-size [IOA] [raid level]`

打印指定的 RAID 适配器上，指定 RAID 级别 RAID 阵列的默认/推荐条带大小。条带大小以 KB 为单位。

`query-recovery-format`

显示所有可以为了错误恢复目的格式化的磁盘。

`query-raid-rebuild`

显示 RAID 阵列中所有可以重建的磁盘。

`query-format-for-raid`

显示所有可以格式化的磁盘，使其用于 RAID 阵列或作为热备盘。

`query-ucode-level [device]`

显示当前加载到指定设备上的微代码级别。

`query-format [device]`

显示指定设备的超时时间。注意：超时仅在命令执行时有效。

`query-depth [device]`

显示指定设备的队列深度。

`query-enable [device]`

如果启用队列，则向标准输出打印 1，否则打印 0。

`query-log [IOA]`

显示 IOA 的日志级别。

`query-add [device]`

显示所有可以添加的磁盘。

`query-remove [device]`

显示所有可以移除的磁盘。

`query-initiator-id [IOA] [busno]`

显示指定 IOA 的启动 ID。

`query-speed [IOA] [busno]`

显示指定 IOA 的速度。

`query-width [IOA] [busno]`

显示指定 IOA 的宽度。

`query-path-status [IOA]`

显示 IOA 的路径状态。

`query-details [device]`

显示指定设备的路径详情。

`query-arrays-migrate`

显示所有可以迁移的阵列。

`query-devices-migrate [array]`

显示指定阵列中所有迁移的所有磁盘。

`query-levels-migrate [array]`

显示阵列可以迁移的级别。

`query-stripe-sizes-migrate [array] [raid level]`

给定阵列级别，显示其可以迁移的条带大小。

`query-devices-min-migrate [array] [raid level]`

显示迁移所需的设备数量。

`query-asymmetric-access`

显示支持对称访问的 IOA。

`query-arrays-asymmetric`

显示支持对称访问的阵列。

`query-ioa-asymmetric-mode [IOA]`

显示 IOA 的对称访问模式。

`query-array-asymmetric-mode [array]`

显示阵列的对称访问模式。

`query-ioa-caching [IOA]`

显示 IOA 的缓存设置为默认还是禁用。

`query-array-label [label]`

显示指定标签的阵列名称。标签在创建 RAID 阵列时必须指定。参见 `raid-create` 命令。

`query-array-rebuild-rate [IOA]`

显示指定 IOA 的重建速率。

`query-array-rebuild-verify [IOA]`

显示指定 IOA 是否启用了重建验证。

`query-array [location]`

显示显示，该阵列中的一个磁盘具有指定的位置代码。

`query-device [location]`

显示具有指定位置代码的磁盘名称。

`query-location [device]`

指定的设备可以是磁盘名称，也可以是单个磁盘 0 阵列的名称。如果指定的设备是磁盘，将显示平台位置代码。如果指定的设备是单个磁盘 0 阵列，将显示作为指定阵列成员的磁盘的平台位置。

`query-write-cache-policy [device]`

显示 `[device]` 的当前缓存策略。

```
raid-create [-r raid_level] [-s stripe_size_in_kb] [-l label] [--skip-format] [devices...]
```

创建 RAID 阵列。RAID 级别可以是适配器支持的任何 RAID 级别，例如 0、10、5、6。目前指定的 KB 条带大小包括 16、64 和 256。如果没有指定 `raid_level`，将默认为所选 RAID 级别的推荐条带大小。设备使用完整名称指定，`/dev/sd` 名称或 `/dev/sd` 名称均可。在某些 RAID 适配器上，还可以指定标签。阵列创建示例：`ipconfig -c-create -r 5 -s 64 /dev/sda /dev/sdb /dev/sdc` 将使用指定的设备创建一个具有 64k 条带大小的 RAID 5 阵列。

`raid-delete [RAID device]`

删除指定的 RAID 阵列。指定 `/dev/sd` 名称或 `/dev/sg` 名称。

单个命令只能删除 1 个阵列。示例：`prconfig -c raid-delete /dev/sda [array] [disk] ... [disk]` 将删除由 `/dev/sda` 代表的磁盘阵列

将指定的设备添加到磁盘阵列以增加其容量。

示例：`prconfig -c raid-include s6 sg7`

`raid-migrate -r raid [-s stripe_size_in_kb] [disk] ... [disk]`

将现有 RAID 阵列迁移到新的 RAID 保护级别。可以提供新的条带大小。在某些情况下，必须添加一个或多个磁盘才能迁移成功。示例：`prconfig -c raid-migrate -r 10 -s 64 sg5 sg6`

`format-for-raid [disk] ... [disk]`

对指定的磁盘进行高级功能（Advanced Function）格式化，以便其用于 RAID 阵列或作为热备盘。

`format-for-jbod [disk] ... [disk]`

对指定的磁盘进行 JBOD 功能格式化，以便其作为独立磁盘使用。

`recovery-format [disk] ... [disk]`

根据参考指南对指定的磁盘进行格式化，用于错误恢复目的。

`hot-spare-create [disk]`

使用指定的高级功能磁盘创建热备盘。

`hot-spare-delete [disk]`

删除指定的热备盘。

`disrupt-device [disk]`

强制指定的高级功能设备失效。

`reclaim-cache [IOA]`

收回 IOA 的写入缓存。**注意**：请谨慎使用此选项。此操作用于丢弃缓存中的数据并可能导致数据丢失。此选项供授权的 IBM 硬件工程师使用。

`reclaim-unknown-cache [IOA]`

收回 IOA 的写入缓存并允许未知数据丢失。**注意**：请谨慎使用此选项。此操作用于丢弃缓存中的数据**会导致**数据丢失。此选项供授权的 IBM 硬件工程师使用。

`raid-consistency-check [array]`

对指定的阵列强制执行全 RAID 一致性检查。该命令会在 RAID 一致性检查完成之前返回。请使用 `status` 命令检查命令的状态。

`raid-rebuild [disk]`

在替换 RAID 阵列中的故障磁盘后，使用此命令将故障磁盘的数据重建到新磁盘，并将磁盘阵列恢复到活动（Active）状态。

`update-ucode [device] [microcode file]`

使用指定的微码文件更新指定设备（IOA 或磁盘）上的微码。**注意**：对微码镜像的检查有限。

确保指定的微码文件是适用于指定设备的正确文件。

`set-format-timeout [disk] [timeout in hours]`

设置格式化指定磁盘时使用的队列超时。

`set-qdepth [device] [queue depth]`



为指定的设备或磁盘阵列设置队列深度。

### `set-tcq-enable [device] [0 = disable, 1 = enable]`

为指定的设备启用/禁用命令队列。

### `set-log-level [IOA] [log level]`

为指定的 `IOA` 设置错误日志的详细程度。默认为 `2`。

### `set-write-cache-policy [device] [writeback|writethrough]`

为 `[device]` 设置缓存策略。可用策略为 `writeback`（写回）和 `writethrough`（直写）。此功能仅由 JBOD 磁盘支持。示例：`iprconfig -c set-write-cache-policy sdb writeback`

### `identify-disk [disk] [0 = turn off LED, 1 = turn on LED]`

开启/关闭指定磁盘的 LED。此功能取决于硬件封装是否可用。

### `identify-slot [location] [0 = turn off LED, 1 = turn on LED]`

开启/关闭指定位置的槽位 LED。此功能取决于硬件封装是否可用。示例：`iprconfig -c identify-slot 0000:d08:01/0:0:1:1`

### `remove-disk [disk] [0 = turn off LED, 1 = turn on LED]`

开启/关闭指定设备的移除 LED。当第二个参数指定为 `1` 时，指定的磁盘被设置为移除（remove）状态。在此状态下，可以移除磁盘。一旦磁盘被物理移除，可以调用 `iprconfig` 并将第二个参数设置为 `0`。这将关闭槽位指示灯并逻辑上从操作系统中移除磁盘。

### `remove-slot [location] [0 = turn off LED, 1 = turn on LED]`

开启/关闭指定位置的移除标识 LED。当第二个参数指定为 `1` 时，指定的位置被设置为移除状态。在此状态下，可以移除磁盘。一旦磁盘被物理移除，可以调用 `iprconfig` 并将第二个参数设置为 `0`。这将关闭槽位指示灯并逻辑上从操作系统中移除磁盘。示例：`iprconfig -c remove-slot 0000:d08:01/0:0:1:1`

### `add-slot [location] [0 = turn off LED, 1 = turn on LED]`

开启/关闭指定位置的磁盘插入指示 LED。当第二个参数指定为 `1` 时，磁盘被设置为插入（insert）状态。在此状态下，可以插入磁盘。一旦磁盘被物理插入，必须调用 `iprconfig` 并第二个参数设置为 `0`。这将关闭槽位指示灯并逻辑上从操作系统中移除磁盘。示例：`iprconfig -c add-slot 0000:d08:01/0:0:1:1`

### `set-initiator [IOA] [initiator]`

（等待，根据可用上下文，文本似乎在此处结束了。）

## 作者

Brian King <brking@us.ibm.com>

# 使用 iSeries 5250 telnet 的注意事项

仅在跨终端时使用此实用工具。由于在某些情况下 5250 telnet 是你访问 iSeries Linux 控制台的唯一选择，我们已尽努力使此工具在 5250 telnet 下可用。通过遵循以下指南，你可以让你的 5250 telnet 体验更加高效且减少挫败感。

- 1. 首先，了解按键在 5250 telnet 下的映射将有所帮助。在 5250 telnet 窗口中，按下 `ESC`。这将进入“发送 TELNET 控制函数”菜单。选择选项 `6` 显示键盘映射。注意 `TAB`、`CTLC` 和 `SENDWOCR` 是如何绑定的。它们在将来将很有用。
- 2. 在选择菜单选项时，输入菜单编号然后按回车键，与通常操作一样。
- 3. 在输入单字符命令（例如 `r=Refresh`）时，输入单字符，然后按 `SENDWOCR` 键（默认为 `F11`）。
- 4. 当在设备/数组/`IOA` 选择屏幕上（例如显示磁盘单元详情）时，不要使用方向键进行导航。相反，使用 `TAB` 键（默认为 `F7`）导航这些屏幕。
- 5. 注意退格键（backspace）和删除键（delete）。原则上，不要使用它们。
- 6. 在编辑根内核消息日志目录或默认编辑器时，可以使用方向键，但不能使用退格和删除键。使用空格键删除已输入的字符。

# IPRDBG

## 名称

`iprdbg` - IBM Power RAID 存储适配器调试实用工具

## 摘要

此可执行文件是‘`iprutils`’软件包的一部分：IBM Power Linux RAID 适配器的实用工具

## 描述

`iprdbg` 用于调试 IBM Power RAID 存储适配器。

## 退出状态

- `-EINVAL`

  无效输入。
- `-ENXIO`

  无 `IOA` 设备。

或指定命令的退出状态。

## 文件

```
/etc/iprdbg.conf
/var/log/iprdbg
```

## 注意

`iprdbg` 是 `iprutils` 软件包的一部分

## 另此参考

`iprconfig(8)`, `iprdump(8)`, `iprint(8)`, `iprupdate(8)`

## 作者

Wayne Boyer <wayneb@linux.vnet.ibm.com>

# IPRDUMP

## 名称

`iprdump` - IBM Power RAID 适配器 dump 工具

## 摘要

```
iprdump [-d directory]
iprdump --version --debug --use-polling --use-uevents
```

## 描述

`iprdump` 用于在适配器故障时收集信息。dump 数据默认保存在 `/var/log/` 目录下，前缀为 `iprdump.#`，其中 `#` 是文件的 dump ID。在进行转储时，`ipr dump` 工具会在系统错误日志中创建日志。`Ipdump`应该作为服务守护进程启动，而不是直接运行。尽管如此，它也可以随时启动，并正确处理从系统中动态添加和删除的适配器。当它直接运行时，它将永久运行以处理可能发生的任何 dump。你可以使用“`iprdump—daemon`”强制其在后台运行。

## 选项

- `-version`

  打印 `iprdump` 的版本号
- `-debug`

  启用额外的错误日志。启用此项将导致额外的错误日志到 `/var/log/messages`。
- `-d <directory>`

  存储 dump 数据的目录。默认是 `/var/log`。
- `-use-polling`

  不使用 netlink/uevent 通知，而是轮询适配器和设备配置的变化。
- `-use-uevents`

  使用 netlink/uevent 通知而非轮询适配器和设备配置的变化。如果未指定，将使用轮询，直到第一次 uevent 通知出现，然后将使用 netlink。
- `-daemon`

  强制守护进程在后台运行

## 作者

最初由 Michael Anderson 编写，

# MODEMMANAGER

## 名称

`ModemManager` - 调制解调器管理进程

## 摘要

```
ModemManager [--version] | [--help]
ModemManager [--debug] [--log-level=<level>] [--log-file=<filename>] [--timestamps] [--relative-timestamps]
```

## 描述

`ModemManager` 守护进程为通信（移动宽带）调制解调器提供统一的高级 API。虽然基本命令是标准化的，但更高级的操作（如连接时的信号质量监控）差异很大。

`ModemManager` 是一个系统守护进程，不打算直接从命令行使用。

## 选项

支持以下选项：

- `-version`

  打印 `ModemManager` 软件版本并退出。
- `-help`

  打印 `ModemManager` 的可用选项并退出。
- `-debug`

  以“DEBUG”日志级别运行 `ModemManager` 且不后台化。这对于调试很有用，因为它将日志输出重定向。
- `-log-level=<level>`

  设置 `ModemManager` 向 syslog 发送信息的量。可选 `"INFO"`, `"DEBUG"`。
- `-log-file=<filename>`

  指定文件位置。
- `-timestamps`

  在日志中包含绝对时间戳。
- `-relative-timestamps`

  包含相对于开始时间的时间戳。

## 另此参考

`NetworkManager(8)`.

# NETWORKMANAGER

## 名称

`NetworkManager` - 网络管理守护进程

## 摘要

`NetworkManager [OPTIONS]`

## 描述

`NetworkManager` 守护进程试图通过管理以太网、WiFi 和移动宽带等网络接口使网络配置变得尽可能简单。它提供了一个丰富的 API，用以检查和控制网络设置。

## 分发脚本

`NetworkManager` 将按字母顺序执行 `/etc/NetworkManager/dispatcher/` 中的脚本。每个脚本接收两个参数，第一个是接口名称，第二个是动作。动作包括：

- `pre-up`

  接口已连接到网络但尚未完全激活。处理此事件的脚本必须放在 `/etc/NetworkManager/dispatcher/pre-up.d` 中，`NetworkManager` 将等待脚本执行后再向应用程序指示接口已完全激活。
- `up`

  接口已激活。
- `pre-down`

  接口已去激活但尚未从网络断开。处理此事件的脚本必须放在 `/etc/NetworkManager/dispatcher/pre-down.d` 中，`NetworkManager` 将在从网络断开接口之前等待脚本执行。注意，对于强制断开（例如当载波丢失或普通连接性减弱）时，不会触发此事件。只有当有机会安全地处理网络事件时才会触发此事件。
- `down`

  接口已去激活。
- `vpn-pre-up`

  VPN 连接到网络但尚未完全激活。处理此事件的脚本必须放在 `/etc/NetworkManager/dispatcher/vpn-pre-up.d` 中，`NetworkManager` 将等待脚本执行后再向应用程序指示 VPN 已完全激活。
- `vpn-up`

  VPN 连接已激活。
- `vpn-pre-down`

  VPN 将去激活但尚未从网络断开。处理此事件的脚本必须放在 `/etc/NetworkManager/dispatcher/vpn-pre-down.d` 中，`NetworkManager` 将在从网络断开 VPN 之前等待脚本执行。注意对于强制断开（例如 VPN 意外终止或普通连接性丢失）时，不会触发此事件。只有当有机会安全地处理 VPN 断开事件时才会触发此事件。
- `vpn-down`

  VPN 连接已去激活。
- `hostname`

  系统主机名已更新。使用 `gethostname(2)` 获取。接口名称（第一个参数）为空且未为动作设置环境变量。
- `dhcp4-change`

  DHCP4 租约已更改（续租、绑定等）。
- `dhcp6-change`

  DHCP6 租约已更改（续租、绑定等）。

环境变量包含更多关于接口和连接的信息。以下变量供分发脚本使用：

- `CONNECTION_UUID`

  连接配置的 UUID。
- `CONNECTION_ID`

  连接配置的名称（ID）。
- `CONNECTION_FILENAME`

  连接配置的文件（如果有）。
- `DEVICE_IFACE`

  设备的接口名称。

## `DEVICE_IP_IFACE`

设备的 IP 接口名称。

## `IP4_ADDRESS_N`

格式为 `"address/prefix gateway"` 的 IPv4 地址，其中 N 是 0 到 (# IPv4 addresses - 1) 之间的数字。此变量中的 gateway 项已弃用，请改用 `IP4_GATEWAY`。

## `IP4_NUM_ADDRESSES`

该变量包含脚本可能预期的 IPv4 地址数量。

## `IP4_GATEWAY`

传统的数字和点分表示法的 IPv4 网关地址。

## `IP4_ROUTE_N`

格式为 `"address/prefix next-hop metric"` 的 IPv4 路由，其中 N 是 0 到 (# IPv4 routes - 1) 之间的数字。

## `IP4_NUM_ROUTES`

该变量包含脚本可能预期的 IPv4 路由数量。

## `IP4_NAMESERVERS`

该变量包含由空格分隔的 DNS 服务器列表。

## `IP4_DOMAINS`

该变量包含由空格分隔的搜索域列表。

`DHCP DHCP4dhcp-option-name>`

使用 DHCP 进行地址配置的连接，收到的 DHCP 配置通过标准的 DHCP 选项名称传递到环境变量，并带有 `"DHCP4_HOST_NAME=foobar"` 前缀。

## `IP6_<name>` and `DHCP6_<name>`

IPv6 与 IPv4 使用相同的变量，但前缀变为 `IP6_` 和 `DHCP6_`。

在 VPNset，会设置 `VPN_IP_IFACE`，还会导出带有 VPN 前缀的 `IP4_*` 和 `IP6_*` 变量，例如 `VPN_IP4_ADDRESS_0`、`VPN_IP4_NUM_ADDRESSES`。

Dispatcher 脚本顺序执行，但与主 `NetworkManager` 进程异步运行，如果运行时间过长会被杀死。如果你的脚本可能需要很长时间才能完成，你应该创建一个子进程并让父进程立即返回。还要注意，一旦脚本进入队列，它将始终会被执行，即使稍后的事件使其过时。（例如，如果一个接口启动后又迅速关闭，则可能在接口关闭后运行一个或多个“启动”脚本。）

## OPTIONS

以下是可识别的选项：

- `-version | -V`

  打印 `NetworkManager` 软件版本并退出。
- `-help | -h`

  打印 `NetworkManager` 的可用选项并退出。
- `-no-daemon | -n`

  不以后进程化。
- `-debug | -d`

  不以后进程化，除了 syslog 之外，将日志输出重定向到控制终端。
- `-pid-file | -p`

  指定 PID 文件的位置。PID 文件用于存储运行进程的 PID 并防止运行多个实例。
- `-state-file`

  指定用于持久存储 `NetworkManager` 状态的文件。如果未指定，将使用默认值 `/var/lib/NetworkManager/NetworkManager.state`。
- `-config`

  指定用于设置 `NetworkManager` 各项的配置文件。如果未指定，将使用默认值 `/etc/NetworkManager/NetworkManager.conf`，如果位于同一目录下，则回退到旧的 `'nm-system-settings.conf'`。更多关于配置文件的信息请参见 `NetworkManager.conf(5)`。
- `-plugins`

  列出管理系统级连接设置的插件。此列表的优先级高于配置文件中指定的插件。目前支持的插件有：`keyfile`, `ifcfg-rh`, `ifcfg-suse`, `ifdown`。
- `-log-level`

  设置 `NetworkManager` 向日志目标（通常是 syslog 的“daemon”设施）发送多少量的信息。默认情况下，只记录信息、警告和错误消息。有关更多信息，请参见 `NetworkManager.conf(5)` 中的日志部分。

## `--log-domains`

一个逗号分隔的列表，指定哪些操作被记录到日志目标（通常为 syslog）。默认情况下，大多数领域都启用了日志。有关更多信息，请参见 `NetworkManager.conf(5)` 中的日志部分。

## UDEV PROPERTIES

`udev(7)` 设备管理器用于网络设备发现。以下属性影响 `NetworkManager` 管理设备的方式：

`NM_UNMANAGED`

当设备的此属性设置为真（“1”或“true”）时，将不会创建默认连接，也不会尝试自动激活。你仍然可以手动为设备附加连接，或观察外部添加的配置（如地址或路由）。

创建一个 udev 规则设置此属性，以防止 `NetworkManager` 干扰由虚拟化工具管理的以太网设备接口。

`NM_PPP_DEBUG`：设置为任何值会导致 `NetworkManager` 在 `pppd` 中开启 PPP 调试，记录所有 PPP 和 PPTP 帧以及客户端/服务器交换。

## SEE ALSO

`NetworkManager.conf(5)`, `nmcli(1)`, `nmcli-examples(5)`, `nm-online(1)`, `nm-settings(5)`, `nm-applet(1)`, `nm-connection-editor(1)` `udev(7)`

## PAM

- NAME

`PAM`, `pam` - Linux 的可插认证模块（Pluggable Authentication Modules）

## DESCRIPTION

本手册旨在对 Linux-PAM 进行快速介绍。有关更多信息，请读者参考 Linux-PAM 系统管理员指南。

Linux-PAM 是一套库系统，用于处理系统上应用程序（服务）的认证任务。该库提供了一个授予权限的稳定通用接口（应用程序编程接口 - API）。

PAM 方法的主要特征是认证的性质是动态配置的。换句话说，系统管理员自由选择提供服务的应用程序如何进行身份验证。这种动态配置由单个配置文件 `/etc/pam.conf` 设置。或者，配置也可以通过 `/etc/pam.d/` 中的单独配置进行设置。如果该目录存在，Linux-PAM 将忽略 `/etc/pam.conf`。

对于本手册所服务的系统管理员来说，理解 Linux-PAM 库的内部行为并不是首要任务。识别的关键点是，配置文件定义了应用程序（服务）与执行实际认证任务的可插认证模块（PAMs）之间的连接。

Linux-PAM 将认证任务分为四个独立的管理组：账户管理；认证管理；密码管理；会话管理。（我们在配置文件中突出显示了这些组使用的缩写。）

简单来说，这些组处理典型用户对服务的请求的不同方面：



### account
提供账户验证类型的服务：该用户的密码是否已过期？用户是否被允许访问请求的服务？

### authentication
验证用户并设置凭据。这通常通过用户必须满足的挑战-响应请求来实现：如果你是你所声称的身份，请提供你的密码。并非所有认证都是这种类型，还存在基于硬件的认证方案（例如使用智能卡和生物识别设备），通过合适的模块，可以无缝替换更标准的认证方法——这正是 `Linux-PAM` 的灵活性所在。

### password
此组的职责是更新认证机制的任务。通常，此类服务与 `auth` 组紧密耦合。某些认证方法适合通过此类函数更新。标准的 `UN*X` 基于密码的访问是一个显而例子：请输入替换密码。

### session
此组的任务涵盖了在提供服务之前和撤回服务之后应该执行的事。此类任务包括审计跟踪的维护和用户主目录的挂载。会话管理组非常重要，因为它为模块提供了开启和关闭的钩子，以影响用户可用的服务。

## FILES

`/etc/pam.conf`

配置文件

`/etc/pam.d`

`Linux-PAM` 配置目录。通常，如果存在此目录，则忽略 `/etc/pam.conf` 文件。

## 错误

通常由 `Linux-PAM` 系统库生成的错误将将写入 `syslog(3)`。

## 遵循标准

`DCE-RFC 86.0`, 1995年10月。包含额外功能，但仍与此 RFC 向后兼容。

## 参见

`pam(3)`, `pam_authenticate(3)`, `pam_sm_setcred(3)`, `strerror(3)`, `PAM(8)`

# IP-ROUTE

名称 - 路由表管理

## 概要

```
ip [OPTIONS] route { COMMAND | help }
ip route { list | flush }
ip route save
ip route restore
ip route get ADDRESS [from ADDRESS]
ip route { add | del | append | replace }
```

## 描述

`ip route` 用于操作内核路由表中的条目。

路由类型：

- `unicast`（单播） - 该条目描述了通往前缀覆盖目的地的路径。
- `unreachable`（不可达） - 这些目的不可到达。数据包被丢弃并生成 ICMP 不可达消息。本地发送者将获得 `EHOSTUNREACH`。
- `blackhole`（黑洞） - 这些目的不可到达。数据包被静默丢弃。本地发送者将获得 `EINVAL`。
- `prohibit`（禁止） - 这些目的不可到达。数据包被丢弃并生成 ICMP 禁止消息。本地发送者将获得 `EACCES`。
- `local`（本地） - 目的地分配给此主机。数据包将环回并在本地递递。
- `broadcast`（广播） - 目的地是广播地址。数据包作为链路发送。
- `throw`（抛弃） - 一种配合策略规则使用的特殊控制路由。如果选择了此类路由，在此表中的查找将终止，表示未找到路由。在没有使用策略路由的情况下，它等同于路由表中不存在该路由。数据包被删除并生成 ICMP 不可达消息。本地发送者将获得 `ENETUNREACH`。
- `nat`（地址转换） - 一种特殊路由。前缀覆盖的终被视为虚拟（外部）地址，在转发之前需要翻译为真实的（内部）地址。要翻译的地址通过 `via` 属性选择。警告：Linux 2.6 不再支持 NAT 路由。
- `anycast`（任播） - 分配给此主机的目的主要等同于本地，但区别在于：此类地址作为数据包的源地址是无效的。
- `multicast`（多播） - 用于多播路由的特殊类型。它不存在于路由表中。

路由表：Linux-2.x 可以将路由打包到多个路由表中，这些表通过 1 到 2^31 范围内的数字或通过文件 `/etc/iproute2/rt_tables` 中的名称来标识。所有普通路由都插入到主表（ID 254），内核仅在计算路由时使用此表。某些值（0, 253, 254 和 255）被留供内置使用。

实际上，始终存在一个表，它是不可见的，但更为重要。它是本地表（ID 255）。该表由本地地址和广播地址的路由组成。内核自动维护此表，管理员通常不需要修改它甚至不需要查看它。

当使用策略路由时，多个路由表就会介入。

- `ip route add` 添加新路由
- `ip route change` 修改路由
- `ip route replace` 替换或添加新路由

### TYPE 前缀（默认）

路由的终。如果省略 `TYPE`，`ip` 假设类型为 `unicast`（单播）。`TYPE` 的其他值列在上方。`PREFIX` 是 IP 或 IPv6 地址，可选跟随一个斜杠和前缀长度。如果缺少前缀长度，`ip` 假设为全长度主机路由。还有一个特殊的 `PREFIX` 默认值 - 等同于 IP `0/0` 或 IPv6。

### tos TOS

`dsfield TOS`

服务类型（TOS）键。此键没有关联的掩码，最长匹配理解为：首先，比较路由和数据包的 TOS。如果它们不等，数据包仍可能匹配 TOS 为零的路由。TOS 是一个 8 位十六进制数或来自 `/etc/iproute2/rt_tables` 的标识符。

### metric 数值

`priority NUMBER`

路由的数值。`NUMBER` 是任意的 32 位数字。

### table 表 ID

将此路由添加到该表。`TABLEID` 可以是数字或 `/etc/iproute2/rt_tables` 中的字符串。如果省略此参数，`ip` 默认使用主表，本地、广播和 `nat` 路由除外。

### dev 名称

输出设备名称。

### via 地址

下一跳的地址。

### src 地址

向前缀覆盖的终发送数据时首选的源地址。

### realm 区域

分配此路由的区域。`REALMID` 可以是数字或 `/etc/iproute2/rt_realms` 中的字符串。

### mtu MTU

通往目的路径上的 MTU。如果不使用锁定，MTU 可能会通过路径 MTU 发现更新。如果锁定，则不会尝试 MTU 发现，IPv4 将不带 DF 位发送，IPv6 将分片。

### window 数值

向这些目的发布的 TCP 最大窗口，以字节为单位。

### rtt 时间

初始 RTT（往返时间）估计。如果没有指定后缀，单位为直接传递给内核的原始值以兼容之前的版本。否则，如果使用 `s`、`sec` 或 `secs` 表示秒，`ms`、`msec` 或 `msecs` 表示毫秒。

### rttvar (2.3.15+)

初始 RTT 方差估计。值由上述 `rtt` 指定。

### rto_min 时间 (2.6.23+)

与目的通信时使用的最小 TCP 重传超时。值由上述 `rtt` 指定。

### sstresh 数值 (2.3.15+)

初始启动阈值的估计值。

### cwnd 数值 (2.3.15+)

拥塞窗口的限制。如果没有锁定标志，则会被忽略。

### initcwnd 数值 (2.5.70+)

与这些目的连接的初始拥塞窗口大小。实际窗口大小为该值乘以连接的 MSS（最大段大小）。默认值为零，意味着使用 RFC2414 中指定的值。

### initrw 数值 (2.6.33+)

与这些目的连接的初始接收窗口大小。实际窗口大小为该值乘以连接的 MSS。默认值为零，意味着使用慢启动值。

### quickack 布尔值 (3.11+)

为这些目的连接启用或禁用快速确认。

### advmss 数值 (2.3.15+)

建立 TCP 连接时向这些目的发布的 MSS（最大段大小）。如果没有给出，Linux 使用根据第一个跳跳设备 MTU 计算的默认值。（如果通往这些目的的路径是对称的，这个猜测可能是错误的）。

### 重排序 reordering NUMBER (仅限 2.3.15+)

通往目的地路径上的最大重排序。如果未指定，Linux 将使用 sysctl 变量 `net/ipv4/tcp_reordering` 选择的值。

### 下一跳 nexthop NEXTHOP

- 多路径路由的。`NEXTHOP` 是一个复杂值，其语法与顶层参数列表类似：
- `via ADDRESS` - 下一跳路由器。
- `dev NAME` - 输出设备。
- `weight NUMBER` - 该多路径路由中该元素的权重，反映了其相对带宽或质量。

### 范围 scope SCOPE_VAL

路由前缀所覆盖的目的地的范围（scope）。`SCOPE_VAL` 可以是一个数字，也可以是来自文件 `/etc/iproute2/rt_scopes` 的字符串。如果省略此参数，`ip` 假设所有通过网关的单播路由作用范围为 `global`（全局），直接单播路由和广播路由的作用范围为 `link`（链路），本地路由的作用范围为 `host`（主机）。

### 协议 protocol PROTO

此条路由的路由协议标识符。`RTPROTO` 可以是一个数字，也可以是来自文件 `/etc/iproute2/rt_protos` 的字符串。如果没有给出路由协议 ID，`ip` 假设作用范围为 `boot`（启动），该路由是由某个不知道自己在做什么的人添加的。某些协议值具有固定解释：

- `redirect` - 路由由于 ICMP 重定向而安装的。
- `kernel` - 路由是由内核在自动配置期间安装的。
- `boot` - 路由在启动过程中安装的。如果启动了路由守护，它将清除所有此类路由。
- `static` - 路由是由管理员安装以覆盖动态路由的。路由守护将尊重它们可能会将其发布给对等节点。
- `ra` - 路由是由路由协议（Router Discovery）安装的。

其余值未保留，管理员可以自由分配（或不分配）协议标签。

### 链上 onlink

假设下一跳直接连接到此链路，无视它不匹配任何接口前缀。

### 删除路由 ip route delete route

- `ip route del` 的参数与 `ip route add` 相同，但语义略有不同。

关键值（to, tos, preference 和 table）选择要删除的路由。如果存在可选属性，`ip` 会验证这些属性与要删除的路由的属性一致。如果未找到给定键和属性的路由，`ip route del` 将失败。

`ip route show` 列出路由

`t` 命令显示路由表的内容或根据某些标准选择的路由。

### 选择器 SELECTOR (默认)

仅从给定的目的地范围内选择路由。`SELECTOR` 由一个可选的修饰符（root, match 或 exact）和一个前缀组成。`root PREFIX` 选择前缀短于 `PREFIX` 的路由。例如，`root 0/0` 选择整个表。`match PREFIX` 选择前缀长于 `PREFIX` 的路由。例如，`match 10.0/16` 选择 10.0/16、10/8 和 0/0，但不会选择 10.1/16 和 10.0.0/24。而 `EXACT PREFIX`（或直接 `PREFIX`）选择具有此精确前缀的路由。如果这两个选项都不存在，`ip` 假设为 `root 0/0`，即列出整个表。

### 服务类型 TOS

`dsfield TOS`

仅选择具有给定 TOS 的路由。

### 表 ID TABLEID

显示来自此表（这些表）的路由。默认设置是显示 `main` 表。`TABLEID` 可以是真实表的 ID，也可以特殊值之一：

- `all` - 列出所有表。
- `cache` - 导出路由缓存。

### 克隆 cloned

缓存的克隆路由，即由于某些路由属性（例如 MTU）更新而从其他路由动态派生的路由。实际上，它等同于 `cache` 表。

### 源自 from SELECTOR

语法与 `to` 相同，它绑定的是源地址范围而不是目的地。注意 `from` 选项仅适用于克隆路由。

### 协议 protocol RTPROTO

仅列出此协议的路由。

### 范围 scope SCOPE_VAL

仅列出此范围的路由。

### 类型 type TYPE

仅列出此类型的路由。

### 设备 dev NAME

仅列出通过此设备的路由。

### 通过 via PREFIX

仅列出通过 `PREFIX` 选择的下一跳路由器的路由。

### 源地址 src PREFIX

仅列出由 `PREFIX` 选择的优选源地址的路由。

### 领域 realm REALMID

### 领域 realms FROMREALM/TOREALM

仅列出具有这些领域的路由。

### 清除路由表 ip route flush routing tables

此命令清除根据某些标准选择的路由。

参数的语法和语义与 `ip route show` 的参数相同，但不是列出路由表而是将其清除。唯一的区别在于默认操作：`show` 导出所有 IP 路由表，而 `flush` 打印帮助页。

带有 `-statistics` 选项，命令将变得详细。它会打印删除路由的数量和重建路由表的轮数。如果给出两次选项，`ip route flush` 还会按照上一个节描述的格式导出所有删除的路由。

### 获取单条路由 ip route get a single route

此命令获取到目的地的单条路由，并按照内核看到的原始格式打印其内容。

### 目的地址 ADDRESS (默认)

目的地。

### 源地址 ADDRESS

源地址。

### 服务类型 TOS

### dsfield TOS

服务类型。

### 接口 if NAME

预期数据包将到达的设备。

### 输出接口 oif NAME

强制路由此数据包的输出设备。

### 连接 connected

如果没有给出源地址（选项 `from`），则 `ip` 假设所有通过网关的单播路由作用范围为 `global`，直接单播和广播路由的作用范围为 `link`，本地路由的作用范围为 `host`。

### 连接 connected

`connected`-此命令获取到目的地的单条路由，并按照内核看到的打印其内容。

### 目的地址 ADDRESS (默认)

目的地。

### 源地址 ADDRESS

源地址。

### 服务类型 TOS

### dsfield TOS

服务类型。

### 接口 if NAME

预期数据包将到达的设备。

### 输出接口 oif NAME

强制路由此数据包的输出设备。

### 连接 connected

如果没有给出源地址（选项 `from`），则 `ip` 假设所有通过网关的单播路由作用范围为 `global`，直接单播和广播路由的作用范围为 `link`，本地路由的作用范围为 `host`。

`unicast` - 规则规定返回该规则引用的路由表中找到路由。

`blackhole` - 规则规定静默丢弃数据包。

`unreachable` - 规则规定生成“网络不可达”错误。

`prohibit` - 规则规定生成“通信管理性禁止”错误。

`nat` - 规则规定将 IP 数据包的源地址翻译为其他值。

## ip rule add - 插入新规则

## ip rule delete - 删除规则

### type TYPE (默认值)

此规则的类型。有效类型列表在上一小节中给出。

### from PREFIX

选择要匹配的源前缀。

### to PREFIX

选择要匹配的目的前缀。

### iif NAME

选择要匹配的入站设备。如果接口是环回接口，规则仅匹配源自此主机的数据包。这意味着你可以为转发数据包和本地数据包创建路由表，从而将它们完全隔离。

### oif NAME

选择要匹配的出站设备。出站接口仅适用于源自绑定设备本地套字的数据包。

### tos TOS

### dsfield TOS

选择要匹配的 TOS 值。

### fwmark MARK

选择要匹配的 fwmark 值。

### priority PREFERENCE

此规则的优先级。每个规则都应该显式设置唯一的优先级值。选项 `preference` 和 `order` 是 `priority` 的同义词。

### table TABLEID

如果规则选择器匹配，则查找的路由表标识符。可以使用 `lookup` 代替 `table`。

### realms FROM/TO

如果规则匹配且路由表查找成功，则选择领域（Realm）。Realm TO 仅在路由未选择任何领域时使用。

### nat ADDRESS

要翻译的 IP 地址块基地址（针对源地址）。`ADDRESS` 可以是 NAT 地址块的起始地址（由 NAT 路由选择），也可以本地主机地址（甚至是 0）。在最后一种情况下，路由器不翻译数据包，而是将其伪装成该地址。使用 `map-to` 代替 `nat` 含义相同。

**警告：** 通过这些命令对 RPDB 进行的更改不会立即生效。假设在脚本完成批量更新后，它通过 `ip route flush cache` 刷新路由缓存。

**ip rule flush - 同时也导出所有已删除的规则。** 此命令没有参数。**ip rule show - 列出规则** 此命令没有参数。选项 `list` 或 `1st` 是 `show` 的同义词。

## 参见

`ip(8)`

## 作者

由 Michail Litvak <mci@owl.openwall.com> 编写原始 Manpage

# IP-TCP_METRICS

名称

`ip-tcp_metrics` - TCP 指标管理

## 概览

```
ip [ OPTIONS ] tcp_metrics { COMMAND | help }
ip tcp_metrics { show | flush } SELECTOR
ip tcp_metrics delete [ address ] ADDRESS
SELECTOR := [ [ address ] PREFIX ]
```

## 描述



`ip tcp_metrics` 用于操作内核中保留 IPv4 和 IPv6 目的地 TCP 信息的条目。这些条目在 TCP 套接等待共享目的地信息时创建，并以目的地址为键存储在缓存中。保存的信息可能包括指标值（最初从路由获取）、用于 TIME-WAIT 回收的近期 TSVAL、用于快速打开（Fast Open）功能的状态。为了性能考虑，缓存增长不能超过配置的限制，旧条目会被新信息替换，有时会被回收并用于新的目的地。内核从不移除条目，只能通过此工具进行刷新。

## `ip tcp_metrics show` - 显示缓存条目

`address PREFIX` (默认值)

IPv4/IPv6 前缀或地址。如果没有提供前缀，则显示所有条目。

输出可能包含以下信息：

`age <S.MAM>sec` - 条目创建、重置或使用套接字指标更新以后的时间。如果指标在过去一小时内未更新，则在使用路由指标时会重置并刷新条目。并非所有缓存值在更新时都会重置 `age`。

`cwd <N>` - CWND 指标值。

`fo_cookie <HEX-STRING>` - SYN-ACK 中的 Cookie 值，用于快速打开的下一个 SYN。

`fo_mss <N>` - SYN-ACK 中的的 MSS 值，用于快速打开的下一个 SYN。

`fo_syn_drops <N>/<S.MAM>sec ago` - 通过接收 SYN 重传后的 SYN-ACK 检测到的初始带数据的快速打开 SYN 的丢弃次数。秒数为上次 SYN 丢弃后的时间，结合丢弃计数可禁用一段时间快速打开。

`reordering <N>` - 重排序指标值。

`ttt <N>us` - RTT 指标值。

`tttvar <N>us` - RTTVAR 指标值。

`ssthresh <SSTHRESH>` - SSTHRESH 指标值。

`tw_ts <TSVAL>/<SEC>sec ago` - 近期 TSVAL 以及保存到 TIME-WAIT 套接字后的秒数。

## `ip tcp_metrics delete` - 删除单个条目

`address ADDRESS` (默认值)

IPv4/IPv6 地址。地址是必需参数。

## `ip tcp_metrics flush` -

此命令刷新符合某些标准的条目。

此命令的参数与 `show` 相同。

## 示例

`ip tcp_metrics show address 192.168.0.0/24`

显示来自子网的目的地条目。

`ip tcp_metrics show 192.168.0.0/24`

`ip tcp_metrics delete 192.168.0.0/24`

`ip tcp_metrics show address 192.168.0.0/24`

（此处省略重复的示例...）

`ttl` 与此选项不兼容：具有固定 `ttl` 的隧道始终会 `pmtu` 发现。

## `key K`

`ikey K`

`okey K`

( 仅 GRE 隧道 ) 使用带有密钥 `K` 的加密 GRE 隧道。`K` 可以是一个数字或类似于 IP 地址的点分四位值。`key` 参数设置双方向均使用的密钥。`ikey` 和 `okey` 参数为输入和输出设置不同的密钥。

## `csum`, `icsum`, `ocsum`

( 仅 GRE 隧道 ) 为封装内的数据包生成/要求校验和。`ocsum` 标志为传出的数据包计算校验和。`icsum` 标志要求所有输入数据包必须具有正确的校验和。`csum` 标志等同于 `icsum` 和 `osum` 的组合。

## `seq`, `isseq`, `oseq`

( 仅 GRE 隧道 ) 对数据包进行序列化。`oseq` 标志启用传出数据包的排序。`isseq` 标志要求所有输入数据包序列化。`seq` 标志等同于 `isseq` 和 `oseq` 的组合。无效。请勿使用。

## `encaplim ELIM`

( 仅 IPv6 隧道 ) 设置固定的封装限制。默认值为 4。

## `flowlabel FLOWABEL`

( 仅 IPv6 隧道 ) 设置固定的流标签。

## `ip tunnel prl potential router list` (ISATAP 仅)

## `dev NAME`

强制性设备名称。

## `prl-default ADDR`

`prl-nodefault ADDR`

`pr-delete ADDR`

添加或删除 `ADDR` 作为潜在路由器或默认路由器。

## `ip tunnel show list tunnels` 此命令没有参数。

## 另阅

`ip(8)`

## 作者

原始 Man页由 Michail Litvak <mci@owl.openwall.com>

# IP-XFRM

### 名称

`ip-xfrm` - 转换配置

## 摘要

```
ip [ OPTIONS ] xfrm { COMMAND | help }
ip xfrm-OBJECT { COMMAND | help }
```

`XFRM-OBJECT := state | policy | monitor`



```ip xfrm state { add | update } ID [ ALGO-LIST ] [ mode MODE ] [ mark MARK [ mask MASK ] [ reqid REQID ] [ SEQ ] [ replay-window SIZE ] [ replay-seq SEQ ] [ reploseq SEQ ] [ flag FLAG-LIST ] [ SELECTOR ] [ LIMIT-LIST ] [ encap ENCAP
[ co ADDR/PLEN ] [ ctx CTX ]
ip xfrm state allocspi ID [ mode MODE ] [ mark MARK [ mask MARK ] [ reqid REQID ] [ seq ] [ min SPI max SPI ]
ip xfrm state { delete | get } ID [ mark MARK [ mask MARK ]
ip xfrm state { deleteall | list } ID [ mode MODE ] [ reqid REQID ] [ flag FLAG-LIST]
ip state flush { proto XFRM-PROTO }
ip xfrm state count
ID := [ src ADDR ] [ dst ADDR ] [ proto XFRM-PROTO ] [ spi SPI ]
XFRM-PROTO := esp | ah | comp | route2 | hao
ALGO-LIST := [ ALGO-LIST ] ALGO
ALGO := { enc | auth } ALGO-NAME ALGO-KEYMAT | auth-trunc ALGO-NAME ALGO-KEYMAT ALGO-TRUNC-LEN | aead algo-NAME ALGO-KEYMAT ALGO-ICLEN | comp ALGO-NAME
MODE := { transport | tunnel | be | ro | in_trigger }
FLAG-LIST := { FLAG-LIST } FLAG
FLAG := { noecn | decap-dscp | noptmidutc | redcrew | icmp | af-unspec | align4
SELECTOR := [ src ADDR/PLEN ] [ dst ADDR/PLEN ] [ dev DEV ]
UPSPEC := { proto } [ tcp | udp | scp | dcp ] [ sport PORT ]
 sportport ] [ [port PORT ] [ icmp | ipv6-icmp | mobility-header ] [ type NUMBER ] [ code ] [ gre | key DOTTED-QUAD | NUMBER ]
LIMIT-LIST := { LIMIT-LIST } limit
LIMIT := { time-soft | time-hard | time-use-soft | use-hard } SECONDS | { byte-soft | byte-hard } SIZE | { packet-soft | packet-hard } COUNT
AP := { espudin | espudin-nonike } SPORT DOADDR
ip xfrm policy { add | update } SELECTOR DIR { ctx CTX } [ mark MARK [ mask MASK ] [ index INDEX ] [ ptype PTYPE ] [ action ACTION ] [ priority PRIORITY ] [
```

带认证的加密数据 (`a`)，包括

加密算法包括 `deflate`, `lzs` 和 `ljih`。

`MODE` 指定了传输协议的运行模式。IPsec 和 IP 负载压缩模式为 `transport`, `tunnel`, `be`, `ro` 和 `in_trigger`。

`FLAG-LIST` 包含一个或多个标记。标记包括：`noecn`, `decap-dscp`, `noptmidutc`, `redcrew`, `icmp`, `af-unspec` 和 `align4`。

`SELECTOR` 由策略控制流量，基于源地址、目的地址、网络设备以及 `UPSPEC`。`UPSPEC` 通过协议选择流量。`tcp`, `udp`, `scp` 或 `dcp` 协议，源端口和目的端口可以可选指定。对于 `icmp`、`ipv6-icmp` 和移动 `header` 协议，类型和代码可以指定。对于 `gre` 协议，密钥可以可选指定点分四位值或数字。其他协议可以通过名称或数字选择。`LIMIT-LIST` 设置秒、字节或数据包限制。

- `xfrm policy add` 添加新策略
- `xfrm policy update` 更新现有的策略
- `xfrm policy delete` 删除现有的策略
- `xfrm policy get` 获取现有的策略
- `xfrm policy deleteall` 删除所有 `xfrm` 策略
- `xfrm policy list` 列出 `xfrm` 策略列表
- `xfrm policy flush` 清空现有的策略
- `xfrm policy count` 计数现有的 `xfrm` 策略

`SELECTOR := [ src ADDR/PLEN ] [ dst ADDR/PLEN ] [ dev DEV ] [ UPSPEC ]`

`UPSPEC := proto { PROTO ] [ tcp | udp | scp | dcp ] [ sport PORT ] [ dport PORT ] | { icmp | ipv6-icmp | mobility-header } [ type NUMBER ] [ code NUMBER ] [ gre | key DOTTED-QUAD | NUMBER } ]`

`DIR := in | fwd`

`PTYPE := main | sub`

`ACTION := allow | block`

`FLAG-LIST := { FLAG-LIST } FLAG`
`FLAG := localok | icmp`

`LIMIT-LIST := { LIMIT-LIST } LIMIT`

`LIMIT := { time-soft | time-hard | time-use-soft | use-hard } SECONDS | { soft | byte-hard } SIZE | { packet-soft | packet-hard } COUNT`

`TMPL-LIST := { TMPL-LIST } tmpl MPL`

`TMPL := ID { mode MODE } [ reqQID ] [ level LEVEL ]`

`ID := { src ADDR } [ dst ADDR ] [ proto XFRM-PROTO ] [ spi SPI ]`

`XFRM-PROTO := esp | ah | comp | route2 | hao`

`MODE := transport | tunnel | beet | ro | in_trigger`

`LEVEL := required | use`

`ip xfrm monitor { all-nsid } [ ListOfXFRM-OBJECTS ]`

## 

`xfrm` 是用于转换数据包（例如加密负载）的 IP 框架。该框架用于实现 IPsec 协议族（作用于安全关联数据库的 `state` 对象和作用于安全策略数据库的 `policy` 对象）。也用于 IP 负载压缩协议和移动 IPv6。

- `xfrm state add` 添加新的 `xfrm` 状态
- `xfrm state update` 更新现有的 `xfrm` 状态
- `xfrm state allocspi` 分配 SPI 值
- `xfrm state delete` 删除现有的 `xfrm` 状态
- `xfrm state get` 获取现有的 `xfrm` 状态
- `xfrm state deleteall` 删除所有 `xfrm` 状态列表
- `xfrm state list` 列出所有 `xfrm` 状态
- `xfrm state count` 计数现有的 `xfrm` 状态
- `xfrm monitor state` 监控 `xfrm` 对象

## ID

## XFRM-PROTO

指定转换协议：IPsec 封装安全负载 (`esp`)、IPsec 认证头 (`ah`)、IP 负载压缩 (`comp`)、移动 IPv6 类型 2 头部 (`route2`) 或移动 IPv6 地址选项 (`hao`)。

## ALGO-LIST

包含一个或多个使用的算法。每个 `ALGO` 由以下项指定：算法类型：加密 (`enc`)、认证 (`auth` 或 `auth-trunc`)、带认证的加密 (`a`) 或压缩 (`comp`)算法名称 `ALGO-NAME` `ALGO-KEYMAT` | `auth-trunc` `ALGO-NAME` `ALGO-KEYMAT` `ALGO-TRUNC-LEN` | `aead` `algo-NAME` `ALGO-KEYMAT` `ALGO-ICLEN` | `comp` `ALGO-NAME`
`MODE := { transport | tunnel | be | ro | in_trigger }`
`FLAG-LIST := { FLAG-LIST } FLAG`
`FLAG := noecn | decap-dscp | noptmidutc | redcrew | icmp | af-unspec | align4`
`SELECTOR := [ src ADDR/PLEN ] [ dst ADDR/PLEN ] [ dev DEV ] [ UPSPEC ]`
`UPSPEC := { proto } [ tcp | udp | scp | dcp ] [ sport PORT ] [ dport PORT ] [ icmp | ipv6-icmp | mobility-header ] [ type NUMBER ] [ code NUMBER ] [ gre | key DOTTED-QUAD | NUMBER ]`
`LIMIT-LIST := { LIMIT-LIST } limit LIMIT`
`LIMIT := { time-soft | time-hard | time-use-soft | use-hard } SECONDS | { byte-soft | byte-hard } SIZE | { packet-soft | packet-hard } COUNT`
`AP := { espudin | espudin-nonike } SPORT DOADDR`
`ip xfrm policy { add | update } SELECTOR DIR { ctx CTX } [ mark MARK [ mask MASK ] [ index INDEX ] [ ptype PTYPE ] [ action ACTION ] [ priority PRIORITY ] [`

带认证的加密数据 (`a`)，包括

加密算法包括 `deflate`, `lzs` 和 `ljih`。

`MODE` 指定传输协议的运行模式。IPsec 和 IP 负载压缩模式为 `transport`, `tunnel`, `be`, `ro` 和 `in_trigger`。

`FLAG-LIST` 包含一个或多个标记。标记包括：`noecn`, `decap-dscp`, `noptmidutc`, `redcrew`, `icmp`, `af-unspec`, 和 `align4`。

`SELECTOR` 由策略控制流量，基于源地址、目的地址、网络设备以及 `UPSPEC`。`UPSPEC` 通过协议选择流量。`tcp`, `udp`, `scp` 或 `dcp` 协议，源端口和目的端口可以可选指定。对于 `icmp`、`ipv6-icmp` 和移动 `header` 协议，类型和代码可以指定。对于 `gre` 协议，密钥可以可选指定点分四位值或数字。其他协议可以通过名称或数字选择。`LIMIT-LIST` 设置秒、字节或数据包限制。

- `xfrm policy add` 添加新策略
- `xfrm policy update` 更新现有的策略
- `xfrm policy delete` 删除现有的策略
- `xfrm policy get` 获取现有的策略
- `xfrm policy deleteele` 删除所有 `xfrm` 策略
- `xfrm policy list` 列出 `xfrm` 策略列表
- `xfrm policy flush` 清空现有的策略
- `xfrm policy count` 计数现有的 `xfrm` 策略

`SELECTOR := [ src ADDR/PLEN ] [ dst ADDR/PLEN ] [ dev DEV ] [ UPSPEC ]`

`UPSPEC := proto { PROTO ] [ tcp | udp | scp | dcp ] [ sport PORT ] [ dport PORT ] | { icmp | ipv6-icmp | mobility-header } [ type NUMBER ] [ code NUMBER ] [ gre | key DOTTED-QUAD | NUMBER } ]`

`DIR := in | fwd`

`PTYPE := main | sub`

`ACTION := allow | block`

`FLAG-LIST := { FLAG-LIST } FLAG`
`FLAG := localok | icmp`

`LIMIT-LIST := { LIMIT-LIST } LIMIT`

`LIMIT := { time-soft | time-hard | time-use-soft | use-hard } SECONDS | { soft | byte-hard } SIZE | { packet-soft | packet-hard } COUNT`

`TMPL-LIST := { TMPL-LIST } tmpl MPL`

`TMPL := ID { mode MODE } [ reqQID ] [ level LEVEL ]`

`ID := { src ADDR } [ dst ADDR ] [ proto XFRM-PROTO ] [ spi SPI ]`

`XFRM-PROTO := esp | ah | comp | route2 | hao`

`MODE := transport | tunnel | beet | ro | in_trigger`

`LEVEL := required | use`

`ip xfrm monitor { all-nsid } [ ListOfXFRM-OBJECTS ]`

`PRIORITY` 是一个默认为零。

`FLAG-LIST` 包含一个或两个可选标志：`local` 或 `icmp`。

`LIMIT-LIST` 以秒、字节或数据包数量设置限制。

`TMPL-LIST` 是使用 `ID`、`MODE`、`REQID` 和/或 `LEVEL` 指定的模板列表。

`ID` 由源地址、目的地址、转换协议 `XFRMPROTO` 和/或安全参数索引 `SPI` 指定。（对于 IP 负载载压缩，使用压缩参数索引 `CPI` 作为 `SPI`。）

`XFRMPROTO` 指定转换协议：IPsec 封装安全载荷 (`esp`)、IPsec 身份验证头 (`ah`)、IP 负载载压缩 (`comp`)、移动端 IPv6 类型 2 路由头部 (`route2`) 或移动端 IPv6 家庭主地址选项 (`hao`)。

`MODE` 指定转换协议的运行模式。IPsec 和 IP 负载载压缩模式包括 `transport`（传输）、`tunnel`（隧道）以及（仅限 IPsec ESP）端到端隧道 (`beet`)。移动端 IPv6 模式包括路由优化 (`ro`) 和入站触发 (`in_trigger`)。

`LEVEL` 可以是 `required`（默认）或 `use`。

可以可选地指定要监控的 `xfrm` 对象。

如果设置 `all-nsid` 选项，程序将监听所有与程序运行的网络空间分配了 `nsid` 的网络空间。将显示一个前缀以显示消息源自的网络空间。例如：

```
[nsid 1]Flushed state proto 0
```

## AUTHOR
手册页由 David Ward <david.ward@ll.mit.edu> 修订。手册页由 Nicolas Dichtel <nicolas.dichtel@wind.com> 修订。

# IPRINT

> NAME
`iprint` - IBM Power RAID 适配器/设备初始化实用

## SYNOPSIS
```
iprint

iprint —debug —daemon —use-polling —use-uevents
```



## DESCRIPTION
`iprint` 用于设置 IBM Power RAID 适配器和设备以获得最佳性能。如果确定磁盘柜支持，它将启用 U320 scsi 速度。它还将启用标记命令队列。由 `iprconfig` 设置的任何 scsi 总线属性（如总线宽度）或磁盘属性（如队列深度）也将加载。建议在启动过程中调用此程序，使用提供的 `init.d` 脚本。

## OPTIONS
- `-version`
打印 `iprint` 的版本号
- `-debug`
启用额外的错误日志。启用此会将额外的错误日志记录到 `/var/log/messages`。
- `-daemon`
作为守护进程运行，处理热插的适配器和设备。
- `-use-polling`
不使用 `netlink/uevent` 通知，而是轮询适配器和设备的配置更改。
- `-use-uevents`
使用 `netlink/uevent` 通知而非轮询适配器和设备的配置更改。如果未指定，将使用轮询，直到第一个 `uevent` 通知出现，然后将使用 `netlink`。

## AUTHOR
Brian King (`brking@us.ibm.com`)

# IPRSOS

> NAME
`iprsos` - IBM Power RAID 报告生成器

## SYNOPSIS
`iprsos`

## DESCRIPTION
`iprsos` 用于通过从系统收集硬件信息以及其他如 `lspci`、`lscsi` 等其他系统调用来生成类似 `sosreport` 的报告。信息从 `iprconfig` 命令中收集并附加到 `/var/log/iprsos.log` 文件。

## FILES
在 `/var/log/iprsos.log` 创建一个包含从硬件和系统收集的信息的详细报告文件。

## AUTHORS
Daniel B. Kreling <kreling@linux.vnet.ibm.com> Brian King <brking@us.ibm.com>

# IPRUNDATE

> NAME
`iprudate` - IBM Power RAID 适配器/设备微代码更新实用

## SYNOPSIS
`iprudate`
`iprudate --debug --check_only --daemon --use-polling --use-uevents`

## DESCRIPTION
用于将 IBM 存储适配器及其连接的磁盘单元上的微代码更新到最低支持的级别。可以在 `ipr` 设备驱动程序加载时随时运行。实用程序将检查系统上每个存储适配器/磁盘单元的微代码版本级别，并与安装在 `/etc/microcode`、`/usr/lib/microcode` 和 `/lib/firmware` 中的微代码版本级别进行比较。如果适配器/设备上的微代码级别低于最低支持级别且最新镜像级别更高，则会将微代码更新为可用的最新级别。建议在启动过程中调用此程序。

## OPTIONS
- `-version`
打印 `iprudate` 的版本号
- `-debug`
启用额外的错误日志。启用此会将额外的错误日志记录到 `/var/log/messages`。
- `-check_only`
检查是否有任何适配器或磁盘单元低于其最低支持级别。
- `-daemon`
作为守护进程运行，处理热插的适配器和设备。
- `-use-polling`
不使用 `netlink/uevent` 通知，而是轮询适配器和设备的配置更改。
- `-use-uevents`
使用 `netlink/uevent` 通知而非轮询适配器和设备的配置更改。如果未指定，将使用轮询，直到第一个 `uevent` 通知出现，然后将使用 `netlink`。

## AUTHOR
Brian King (`brking@us.ibm.com`)

# IPSEC

> NAME
`ipsec` - 调用 IPsec

## SYNOPSIS
```
ipsec [argument...] --help
ipsec --version
ipsec --directory
```

## DESCRIPTION
`ipsec` 调用控制 IPsec 加密/身份验证系统的多个实用程序之一，就像直接调用它们一样。大多数实用程序有自己的手册页，例如 `ipsec_auto(8)`。

`ipsec` 版本输出软件版本。格式为 “Uxx/Kyy” 的版本表示用户级实用程序和内核部分为 XFR 栈。

## COMMANDS
要获取支持的命令列表，请使用 `ipsec --help`。以下描述了一些常用的命令：

- `ipsec auto` 用于手动添加、删除、启动连接。更多信息请查看 `ipsec_auto`
- `ipsec whack` 使用 `whack` 接口与 `pluto` 守护进程通信直接命令。更多信息请查看 man `ipsec_pluto`
- `ipsec import` 将 PKCS#12 X509 文件导入 NSS 数据库。

## FILES
`/usr/local/libexec/ipsec` 通常目录

## SEE ALSO
`ipsec.conf(5)`, `ipsec.secrets(5)`, `ipsec_auto(8)`, `ipsec_setup(8)`, `ipsec_showhostkey(8)`

## AUTHOR
Henry Spencer

# IPSEC_KEYCENSOR

> NAME
`ipsec__keyensor` - 移除敏感信息的内部程序

## DESCRIPTION
`_keyensor` 被 `ipsec barf` 用于处理 `/etc/ipsec.secrets` 文件，移除密钥信息。

## SEE ALSO
`ipsec(8)`, `ipsec_barf(8)`

## HISTORY
手册页由 Michael Richardson 为 Linux FreeSWAN 项目 <http://www.freeswan.org/m[]> 编写。原始程序由 Henry Spencer。

## AUTHOR
Paul Wouters

# IPSEC_PLUTORUN

> NAME
`ipsec__plutorun` - 在旧 SYSV 初始化脚本系统中（重新）启动 `pluto` 的内部脚本

## DESCRIPTION
`_plutorun` 被 `_realsetup` 调用以配置并启动 `pluto`。它调用 `pluto` 并监控确保 `pluto` 在失败时重启，因为 SYSV 初始化脚本不提供重启机制。当使用其他初始化系统（如 `systemd` 或 `upstart`）时，不使用 `_plutorun`。

## 另见
`ipsec(8)`, `ipsec_setup(8)`, `ipsec__realsetup(8)`, `pluto(8)`.

## 历史
帮助页由 Michael Richardson 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org/m[]> 编写。原始程序由 Henry Spencer 编写。Paul Wouters 为 Libreswan 项目 <http://www.libreswan.org/m[]> 进行更新。

## 作者
Paul Wouters

用于抑制警告的占位符

# IPSEC_SECRETCENSOR

- 名称
`ipsec__secretensor` - 用于清理文件的内部路由

## 描述
`_secretensor` 被 `ipsec_barf` 调用，用于处理 `/etc/ipsec.secrets` 文件，在显示内容之前从该文件中的私钥组件。

## 另见
`ipsec(8)`, `ipsec_barf(8)`.

## 历史
帮助页由 Michael Richardson 为 Linux FreeSWAN/WAN 项目 <http://www.freeswan.org/m[]> 编写。原始程序由 Henry Spencer 编写。

## 作者
Paul Wouters

用于抑制警告的占位符

# IPSEC_STACKMANAGER

## 名称
`ipsec__stackmanager` - 为 Libreswan 启动内核组件的内部脚本

## 概要
```
ipsec _stackmanager start
ipsec _stackmanager stop
```

## 描述
`ipsec _stackmanager` 被从初始化子系统（`systemd`, `up`, `sysv initscripts`）内部调用，根据 `ipsec.conf` 配置文件中 `protostack=` 选项的配置启动 Libreswan 内核组件。

这涉及加载可选卸载所需的内核模块。由于 Linux 内核无法按需自动检测大多数与加密相关的驱动程序，`_stackmanager` 负责加载硬件随机数（RNG）设备驱动程序、OpenBSD/FreeBSD 加密框架（OCF）驱动程序、CryptoAPI 驱动程序以及特定栈（Linux NETKEY/XFM 或 KLIPS/MAST）的模块。不支持对支持 OCF 的硬件进行探测——这些模块必须在 Libreswan 子系统启动之前由系统加载。

## 另见
`ip(8)`, `ipsec_tncfg(8)`, `ipsec.conf(5)`, `ipsec_addconn(8)`, `pluto(8)`

## 历史
此脚本引入自 Libreswan。在旧的 Openswan 系统中，此功能被分在多个脚本文件中，如 `ipsec _startnetkey`, `ipsec _startklips`, `ipsec _realsetup` 和 `ipsec setup`。帮助页由 Paul Wouters 为 Libreswan 项目 <http://www.libreswan.org/m[]> 编写。

## 作者
Paul Wouters

用于抑制警告的占位符

# IPSEC_ipsec_updown

- 名称
`ipsec_ipsec_updown` - klips 操作脚本

## 概要
`ipsec_updown` 在 `pluto` 建立新连接时被调用。该脚本用于为 IPsec 操作插入适当路由条目。脚本的接口在 `pluto` 帮助页中有记录。

## 另见
`ipsec(8)`, `ipsec_pluto(8)`.

## 历史
帮助页由 Michael Richardson 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org/m[]> 编写。原始程序由 Henry Spencer 编写。

## 作者
Paul Wouters

用于抑制警告的占位符

# IPSEC_ADDCONN

- 名称
`ipsec_addconn` - 将给定策略加载到 `pluto` IKE 守护进程

## 概要
```
ipsec addconn --configsetup [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--noexport] [--warningsfatal]
ipsec addconn --liststack [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--noexport] [--warningsfatal]
ipsec addconn --checkconfig [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--noexport] [--warningsfatal]
ipsec addconn --autoall [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--noexport] [--warningsfatal]
ipsec addconn [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--noexport] [--warningsfatal] name1 [name2 ..]
ipsec addconn --listall] [--liststart] [--listroute] [--listadd] [--listignore] [--rootdir dir] [--config filename] [--ctlbase socketfile] [--verbose] [--warningsfatal]
ipsec addconn --help
```

## 描述
`ipsec addconn` 接收一个包含 `ipsec.conf` 格式或单个“conn”部分格式的配置文件（或 stdin），并使用这些信息将该配置文件定义的命名连接或所有连接加载到运行的 libreswan `pluto` 守护进程中。如果未指定配置文件，则使用默认配置文件。

## 历史
帮助页由 Paul Wouters 为 Libreswan 项目 <http://www.libreswan.org/m[]> 编写。

## 作者
Paul Wouters

用于抑制警告的占位符

# IPSEC_AUTO

- 名称
`ipsec_auto` - 控制自动密钥 IPsec

## 概要
```
ipsec auto --showonly] [--asynchronous] [--config configFile] [--verbose]
ipsec auto --showonly] [--asynchronous] [--config configFile] [--verbose]
```



## 描述

Auto

操作自动密钥 Libreswan IPsec 连接，根据配置文件启动并关闭它们。在正常用法下，`connection` 是 `--add`, `--delete`, `--replace`, `--up`, `--down`, `--route` 或 `--unroute`。`--ready`, `--rereadsecrets`, `--rereadgroups` 和 `--status` 不需要连接名称。Auto 生成相应的命令并将其交给 shell。

`--add` 操作将连接规范添加到内部数据库；如果 plato 已经同名规范，则会失败。`--delete` 操作从 plato 的内部数据库中删除连接规范（同时关闭基于该规范的连接）；`--replace` 操作等同于 `--delete`（如果已加载连接），用于更新内部规范以匹配外部规范。（注意，rereads 操作会导致策略组生效（这目前是 ready 的同义词，但可能会发生））。其他操作都不会更改内部数据库。

`--up` 操作请求 plato 为其内部数据库中的条目建立连接。`--down` 操作告诉 plato 关闭连接。

通常，plato 会作为 `--up` 操作的一部分为连接指定的目的地建立路由。然而，路由和数据捕获是通过 `--route` 操作建立的。在实际建立连接之前，这将丢弃任何发送的数据包，这比将其发送到更通用的路由（例如默认路由）可能更好。此类路由可以使用 `--unroute` 操作移除（并在删除时隐含移除）。

`--ready` 操作告诉 plato 监听其他主机的连接请求。在双方之前执行 `--up` 操作是徒劳且无效的，尽管这现在作为 IPsec 启动的一部分已自动化，通常没有问题。

`--status` 操作请求 plato 提供连接状态。输出格式是临时的且可能会更改。

`--rereadsecrets` 操作告诉 plato 重新读取 `/etc/ipsec.secrets` 密钥文件，通常只在启动时读取。（目前是 `--ready` 的同义词，可能会发生变化。）

`--rereadsecrets` 操作告诉 pluto 重新读取 `/etc/ipsec.secrets` 密钥文件，该文件通常只在启动时读取。（目前是 `--ready` 的同义词，但可能会发生变化。）

`--reredacerts` 操作读取 `/etc/ipsec.d/cacerts` 目录中包含的所有证书文件，并将它们添加到 pluto 的证书授权 (CA) 证书列表中。注意，CA 可以存储在 NSS 中，而不是 `/etc/ipsec.d/cacerts` 目录中，这将实现自动更新。该选项在不久后将废弃。

`--rereadcrl` 操作读取 `/etc/ipsec.d/crls` 目录中包含的所有吊销列表 (CRL) 文件，并将它们添加到 pluto 的 CRL 列表中。注意，CRL 可以并且存储在 NSS 中，而不是 `/etc/ipsec.d/crls` 目录中，这将实现自动更新。该选项在不久后将废弃。

`--rereadall` 操作等同于执行 `--rereadsecrets`、`--rereadkeys` 和 `--rereadcrl`。

`--listpubkeys` 操作列出所有 RSA 公钥，这些密钥是通过嵌入身份验证负载的 IKE 协议从对端接收的，或者是使用 `ipsec(5)` 中的 `rightcert` / `leftcert` 或 `right-` / `leftsasigkey` 参数在本地加载的。

`--listcerts` 操作列出所有使用 `ipsec(5)` 中的 `rightcert` 和 `leftcert` 参数在本地加载的 X.509 证书。要查看 NSS 数据库中的所有证书，请使用 `certutil -d /etc/ipsec.d -L`。

`--checkpubkeys` 操作列出所有即将过期或已过期的加载 X.509 证书。

`--listacerts` 操作列出所有从 `/etc/ipsec.d/cacerts` 目录本地加载的或通过 IKE 协议以 PKCS#7 封装的证书负载接收的 X.509 CA 证书。

`--listgroups` 操作列出所有在 `ipsec(5)` 的连接定义中使用的组（groups），或者嵌入在已加载的 X.509 属性证书中的组。

`--listcrl` 操作列出所有从 `/etc/ipsec.d/crls` 目录本地加载的或从 HTTP 或 LDAP 服务器动态获取的证书吊销列表 (CRL)。

`--listall` 操作等同于执行 `--listpubkeys`、`--listcerts`、`--listac`、`--listgroups`、`--listcrl`。

`--showonly` 操作导致 auto 在标准输出上显示将运行的命令，但不执行它们。

`--asynchronous` 操作仅适用于 up 操作，让 pluto 尝试建立连接，但不延迟报告结果。这在网络链路较慢时并行启动多个连接特别有用。

- `verbose` 选项指示 `auto` 传递来自 `ipsec_whack(8)` 的所有输出，包括通常被过滤掉的无紧要的日志输出。
- `config` 选项指定 IPsec 配置文件的非标准位置（默认为 `/etc/ipsec.conf`）。

配置文件的详情请参阅 `ipsec.conf(5)`。

## 文件

| 路径 | 描述 |
| :--- | :--- |
| `/etc/ipsec.conf` | 默认 IPSEC 配置文件 |
| `/etc/ipsec.d/` | X.509 和机会性加密文件 |
| `/var/run/pluto/pluto.ctl` | Pluto 命令套字 |

## 另参

`ipsec.conf(5)`, `ipsec(8)`, `ipsec_pluto(8)`, `ipsec_whack(8)`

## 历史

最初由 Henry Spencer 为 FreeS/WAN 项目 http://www.freeswan.org/ 编写。

# 缺陷

尽管 `--up` 操作在两端执行连接设置，但 `--down` 仅断开连接的一端（尽管孤立端最终会超时）。

不支持透传连接 (passthrough connections)。

如果连接描述在其中一个下一跳参数中使用了 `%defaultroute` 但在另一个中没有，在某些情况下可能会被错误地拒绝为无效的。

`--showonly` 的退出状态并不总是反映在处理请求期间发现的错误。（这对于人工检查没有问题，但不利于在脚本中使用。）

## 作者

Paul Wouters

抑制警告的占位符

# IPSEC_BARF

> 名称

`ipsec_barf` - 输出收集到的 IPsec 调试信息

## 概要

```
ipsec barf [--short --maxlines <100>]
```

## 描述

Barf
在标准输出上输出与 IPsec 加密/认证系统相关的调试信息集合（文件内容、日志选择内容等）。它主要是为了远程调试提供的便利工具，一个打包（并标记）这些信息的命令。

`--short` 选项限制了 barf 的输出，否则输出可能会非常多。

`--maxlines <100>` 设置了 barf 输出的长度，默认为 100。

`--debug` 选项允许你指定要输出的调试信息级别。

## OR

SAID（said），指示应使用哪个安全关联（Security Association）来处理数据包。

地址以 IPv4 点分进制或 IPv6 冒号十六进制写入，协议为“ah”、“esp”、“comp”或“tun”之一，SPI 是前缀的十六进制数字，其中“.”代表 IPv4，“:”代表 IPv6。

SAID 的写入格式为“protoafSPI@address”。还有 5 个“魔术”SAID，具有特殊含义：

- `%drop` 意味着匹配项将被丢弃
- `%reject` 意味着匹配项将被丢弃，并在可能的情况下返回 ICMP 消息以进行通知
- `%trap` 意味着匹配项将向密钥管理守护进程（s）触发 ACQUIRE 消息，并将设置保持路由（holdroute）以防止后续数据包再次触发 ACQUIRE 消息
- `%hold` 意味着匹配项将被存储，直到该路由被替换或该路由被收回
- `%pass` 意味着匹配项将允许通过且不经过 IPSEC 处理

`/proc/net/ipsec_eroute` 的格式请参见 `ipsec_eroute(5)`。

## EXAMPLES

`ipsec eroute—eraf inet—src 192.168.0.1/32—dst 192.168.2.0/24—af inet—edst 192.168.0.2—spi 0x135—proto tun`

在安全网关上设置一条路由，保护主机 192.168.0.1 与具有 24 位子网掩码的子网 192.168.2.0 之间的流量，通过安全网关 192.168.0.2 使用地址为 192.168.0.2、安全参数索引 0x135 以及协议 tun (50, IPPROTO_ESP)的安全关联。

`ipsec eroute—add—eraf inet6—src 3049:1::128—dst 3049:2::64—af inet6—edst 3049:1::2—spi 0x145—proto tun`

在安全网关上设置一条路由，保护主机 3049:1::1 与具有 64 位子网掩码的子网 3049:2:: 之间的流量，通过安全网关 3049:1::2 使用地址为 3049:1::2、安全参数索引 0x145 以及协议 tun (50, IPPROTO_ESP)的安全关联。

`ipsec eroute—replace—eraf inet—src company.com/24—dst ftp.org/32—said tun.135@gw.ngo.org`

替换安全网关上的某路由，保护具有 24 位子网掩码的 company.com 与主机 ftp.org 之间的流量，通过安全网关 gw.ngo.using 使用安全关联 ID 为 tun0x135@gw.ngo 的安全关联。

`ipsec eroute—del—eraf inet—src company.com/24—dst www.ietf.org/32—said %passthrough`

删除安全网关上的某路由，该路由原先允许具有 24 位子网掩码的子网 company.com 与主机 ietf.org 之间的流量以明文、未经处理的形式通过。

`ipsec eroute—add—eraf inet—src company.com/24—dst mail.ngo.org/32—transport-port 6—dst port 110—said tun.135@mail.ngo.org`

在安全网关上设置一条路由，仅保护具有 24 位子网掩码的子网 company.com 与主机 ftp.org 之间端口 110 (pop3) 的 TCP 流量，通过安全网关 mail.ngo.using 使用关联 ID 为 tun0x135@mail.ngo.org 的安全关联。注意，任何其他发往 mail.ngo.org 并通过该设备的流量都将被丢弃。如果您希望允许其他流量通过，则必须添加 `%pass` 规则。例如，以下规则与上述规则结合时，将确保从 mail.ngo.org 读取或从 mail.ngo.org 读取的 POP3 消息将以明文形式传输。

`ipsec eroute—add—eraf inet—src company.com/24—dst mail.ngo.org/32—said %pass`

## FILES

```
/proc/net/ipsec_eroute, /usr/local/bin/ipsec
```

`ipsec(8)`, `ipsec_tncfg(8)`, `ipsec_spi(8)`, `ipsec_spigrp(8)`, `ipsec_klipsdebug(8)`, `ipsec_eroute(5)`

## HISTORY

为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m/]> 由 Richard Guy Briggs 编写。

## AUTHOR

Paul Wouters

用于抑制警告

# IPSEC_IKEPING

- - NAME

`ipsec_ikeping` - 发送/接收 ISAKMP/IKE 回显请求/响应

## SYNOPSIS

`ipsec ikeping [--listen] [--verbose] [--wait time] [--exchangeanum num] [--ikeport localport] [--ikeaddress address] [--inet] [--inet6] destaddr [/dst]`

## DESCRIPTION

`ipsec ikeping`
发送/接收 ISAKMP/IKE 回显请求/响应。

在编写本文时，`ipsec ikeping` 用于测试 IPsec 的连通性。该选项用于设置超时时间。`listen` 选项用于监听每个请求/响应。

`listen` 选项用于监听。`ikeport` 选项用于指定端口。`ikeaddress` 选项用于指定地址。`inet` 选项用于使用 IPv4。`inet6` 选项用于使用 IPv6。`wait` 选项用于指定超时。`verbose` 选项用于详细输出。`exchangeanum` 选项用于指定交换次数。`destaddr` 是目标地址。`/dst` 是可选地址。

`ipsec ikeping` 命令用于验证 IPsec 的连通性。它发送 ISAKMP/IKE 回显请求并等待响应。如果收到响应，则连接视为正常；如果在超时时间内未收到响应，则连接视为中断。

该命令还可以通过观察回显请求和响应来调试 IPsec 问题。`verbose` 选项可查看请求和响应的详细内容。

## IPSEC_IPSIPS

`klipsdebug` 控制 ips 的各个部分。

当前的标志名称为：

- `tunnel`
- `tunnel-xmit`
- `pfkey`
- `xform`
- `eroute`
- `spi`
- `radij`
- `esp`
- `ah`
- `ipcomp`

`/proc/net/ipsec_eroute` 的格式请参见 `klipsdebug(5)`。

## SYNOPSIS

`ipsec klipsdebug`

- `ipsec klipsdebug—set flagname`
- `ipsec klipsdebug—clear flagname`
- `ipsec klipsdebug—all`
- `ipsec klipsdebug—none`
- `ipsec klipsdebug—help`
- `ipsec klipsdebug—version`

## DESCRIPTION

`klipsdebug`
设置和清除控制 Klips（FreeS/WAN 的内核部分）的标志。

不带参数的形式列出内容。`set` 格式开启指定的标志，`clear` 格式关闭指定的标志。`all` 格式开启除 verbose 外的所有标志，`none` 格式关闭所有标志。

用于设置或取消特定的标志组合。输出写入 `/proc/net/klipsdebug`。`set` 选项用于指定标志名称。`clear` 选项用于指定名称。`all` 选项开启所有标志。`none` 选项关闭所有标志。`help` 选项提供帮助。`version` 选项显示命令版本。

## EXAMPLES

`klipsdebug—all`

开启除 verbose 以外的所有标志。

`klipsdebug—clear tunnel`

关闭 tunnel 消息。

## FILES

`/proc/net/klipsdebug, /usr/local/bin/ipsec`

## SEE ALSO

`ipsec(8)`, `ipsec_manual(8)`, `ipsec_tncfg(8)`, `ipsec_eroute(8)`, `ipsec_spi(8)`, `ipsec_spigrp(8)`, `ipsec_klipsdebug(5)`

## HISTORY

为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m/]> 由 Michael Richardson 编写。

## BUGS

应该能够设置或取消特定的标志组合。

## AUTHOR

Paul Wouters

用于抑制警告

## LOOK

- - NAME

`ipsec_look` - 获取 Libreswan 状态的快速摘要

## SYNOPSIS

`ipsec look`

## DESCRIPTION

Look

用于快速概述 Libreswan 的状态。它等同于运行 `ipsec eroute`、`ipsec spigrp`、`ipsec tncfg`、`ipsec spi` 和 `netstat -rn`。然而，对输出进行了处理以合并。

上述某些命令（因此 `ipsec look`）仅支持 KLIPS 或 MAST 栈，在 BSD、Windows 或带有 NETKEY 的 Linux 上使用会报错。

## 参见

`ipsec(8)`, `ipsec_tncfg(8)`, `ipsec_spi(8)`, `ipsec_spigigp(8)`, `ipsec_eroute(5)`, `netstat(8)`.

## 历史

本帮助页专为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m[]> 由 Michael Richardson 编写。原始程序由 Henry Spencer 编写。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_RANBITS

+ >  {览

`ipsec_newhostkey` - 为主机生成新的原始 RSA 认证密钥

## 概要

```
ipsec newhostkey [[--configdirssdbdir] | [--password password]] [[--quiet]] | [--verbose]] [--bits bits] [--random device] [--hostname hostname] [--output filename]
```



## 描述

`newhostkey`

输出（输出到文件名，可以使用 `-` 表示标准输出）一个适用于该主机的 RSA 私钥，格式类似于 `/etc/ipsec.secrets`（请参见 `ipsec.secrets(5)`），默认使用 `--quiet` 选项。

`--output` 选项是强制性的。如果指定的文件不存在，将根据 `umask 077` 创建它；如果文件已存在且非空，则向标准错误发送关于该点的警告信息，并将输出追加到文件中。

`--quiet` 选项会抑制 RSA 密钥的生成过程说明以及文件已存在的警告信息。

当带有 NSS 支持编译时（默认值），`--configdir` 指定 NSS 配置目录，证书密钥和 modsec 数据库均位于该目录。没有默认值，但 `/etc/ipsec.d` 可能是一个合理的选择。

当带有 NSS 支持编译时（默认值），`--password` 指定一个模块认证密码，如果启用了 FIPS 模式，可能需要该密码。

`--bits` 选项指定 RSA 密钥的位数；当前的默认值是 3072 到 4096 之间的随机值（16 的倍数）。允许的最小值为 2172。

`--random` 用于指定随机设备（默认使用 `/dev/random` 为加密库的 RNG 种子）。

`--hostname` 选项传递给 `rsasikey`，告诉它使用哪个主机名来标记输出（通过其 `--hostname` 选项）。

输出格式采用 `rsasikey` 格式，并添加括号以完成 `ipsec.secrets` 格式。在通常情况下，如果 `ipsec.secrets` 只包含主机自身的私钥，则 `newhostkey` 的输出就足够构成完整的 `ipsec.secrets` 文件。

## 文件

`/dev/random`, `/dev/urandom`

## 参见

`ipsec_rsasigkey(8)`, `ipsec.secrets(5)`

## 历史

最初为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m> 由 Henry Spencer 编写。由 Paul Wouters 更新。

# 缺陷

与 `rsasigkey` 一样，其运行时间难以预测，因为系统随机数池的耗尽可能导致对随机位的任意长时间等待，而且质数搜索也可能消耗不可预测的（且可能是大量的）CPU 时间。请参见 `ipsec_rsasigkey(8)`。

如果有一个处理切换新密钥等性细节的高级工具将非常有帮助。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_PF_KEY

`ipsec_pf_key` - 显示在使用 KLIPS 或 MAST 栈时内核发出的 pfkey 消息。

## 概要

`pf_key`—`ah`—`esp`—`ipip`—`ipcomp`—`daemon` `file` `hmac-md5-96` | `hmac-sha1-96`

## 栈

注意 `pf_key` 仅在 KLIPS 和 MAST 栈上支持。其他任何栈都不支持。

## 描述

`pf_key` 是一个打开 PF_KEY 套字并打印从中接收到的所有消息的程序。在不提供选项的情况下，它将注册自身以接收 AH、ESP、IPIP 和 IPCOMP 安全关联的密钥请求。如果给了更具体的选项，它将只监听列出的协议。

如果消息被识别，将对消息进行解码。

如果提供了 `--daemon` 选项，在完成注册后，程序将派生到后台运行。提供的文件将被打开，后台进程的进程 ID 将写入其中。此选项是为了是为了回归测试中呈现竞态条件。

## 文件

`/proc/net/pf_key`

## 参见

`pf_key(5)`, `ipsec(8)`, `ipsec_eroute(5)`, `ipsec_spi(5)`, `ipsec_spigrp(5)`, `ipsec_klipsdebug(5)`, `ipsec_tncfg(8)`, `ipsec_version(5)`

## 历史

为 Linux FreeS/WAN 项目 <http://www.freeswan.org/m[]> 由 Michael Richardson <mcr@freeswan.org> 编写。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_PLUTO

`pluto` - ipsec IKE 守护进程和控制接口

## 概要

`ipsec pluto [help] [version] [--leak-all]`

## 描述

### pluto

`pluto` 是一个 IKE（“IPSec 密钥交换”）守护进程。`whack` 则是一个辅助程序，允许向运行中的 `pluto` 请求。

`pluto` 用于在具有 IPsec 的系统上自动构建共享关联。数据包的安全传输是系统其他部分——即内核的责任。`Pluto` 可以与各种内核实现交互，如 KLIPS、NETKEY 以及 KAME IPsec 栈。`ipsec_auto(8)` 为 `pluto` 和 `whack` 提供了一个更方便的接口。

### IKE 的工作

安全关联（SA）是两个网络节点之间如何处理流量的协议。这种处理涉及封装、认证、加密或压缩。

IKE 可以部署在网络节点上为该节点协商安全关联。IKE 实现只能与其他 IKE 实现进行协商，因此作为 IKE 协商安全关联的端点必须安装 IKE。

一个 IKE 实例（即特定网络节点上的 IKE 实现）使用 UDP IP 包与另一个 IKE 实例通信，因此节点之间必须存在路由。

安全关联（Security Association）拥有一组一致的特征，当双方都认可彼此的身份验证时，它们就可以建立安全关联。标准并没有规定是什么导致 IKE 实例启动协商。

总而言之，IKE 实例准备用于在 IPsec 环境中自动管理安全关联，但有许多问题被视为策略范畴，并留给系统管理员处理。

### Pluto

`pluto` 是 IKE 的一种实现。它作为守护进程运行在网络节点上。目前，这种网络节点模式是指运行着 KLIPS 或 NETKEY 实现的 IPsec 的 LINUX 系统，或者是运行 KAME 实现的 IPsec 的 FreeBSD/NetBSD/Mac OSX 系统。

`pluto` 实现了 IKE 的很大一个子集。这足以让它与其他 `pluto` 实例以及许多其他 IKE 实现协同工作。它目前支持 XAUTH、ModeConfig、X.509、死对端检测（Dead Peer Detection）、机会加密以及所有的 NAT 穿越（NAT Traversals）。

安全关联可接受特征的策略大部分硬编码在 `pluto` 的代码（`spdb.c`）中。最终，这将移动到一个具有响应式表达能力且更方便使用的的安全策略数据库中。

`pluto` 使用密钥或 RSA 签名来对与其协商的伙伴进行身份验证。这些 RSA 签名可以来自 DNS(SEC)、配置文件或 X.509 和 CA 证书。

当 `pluto` 被手动触发时，它会启动安全关联协商：通过运行 `whack` 程序来触发。当 KLIPS 捕获到用于机会加密的出站数据包时，它也会启动协商。

`pluto` 自身实现了 ISAKMP SA。在协商完 IPsec SA 的特征后，它会指导实现它。如有必要，它还会调用脚本来调整任何防火墙和 `route(8)` 命令以重定向 IP 包。

当 `pluto` 关闭时，它会关闭所有的安全关联。

### 在运行 Pluto 之前

`pluto` 以 root 用户身份作为守护进程运行。在运行它之前，必须设置好几项内容。

- `pluto` 需要一个良好的 IPsec 栈。
- `pluto` 支持多个公共网络（即被认为是不安全的且需要对其流量进行加密或身份验证的网络）。它通过查看所有已配置的接口来发现要使用的公共接口（可以使用 `--interface` 选项来限制考虑的接口）。这仅在 `whack` 告诉它 `--listen` 时发生，接口必须由它们配置。名称格式为 `ipsec[0-9]` 的接口被视为 KLIPS 虚拟公共接口。另一个具有 IP 地址的网络接口（将使用找到的第一个）被相应的真实公共接口。`--listen` 可用于限制在中心接口的一个 IP 地址上监听。`ifconfig(8)` 或带有 `-a` 标志的 `ip(8)` 将显示每个网络接口的名称和状态。
- `pluto` 需要预共享密钥和 RSA 私钥数据库。这在 `ipsec.secrets(5)` 中描述。通过 `whack` 命令告知 `pluto` RSA 公钥。如果连接是机会性的，且未知 RSA 公钥，`pluto` 将尝试使用域名命名系统（DNS）获取 RSA 密钥。

### 为 pluto 配置 KLIPS

`pluto` 支持的最基础网络拓扑是安全网关代表客户端子集进行协商。RGB 测试平台的图示是一个很好的例子（参见 `klips/doc/rgb_setup.txt`）。

该发行版根目录下的 `INSTALL` 文件解释了如何启动整个 KLIPS 系统。

确保安全网关之间有路由。这通常由默认路由覆盖，但可能需要发布 `route(8)` 命令。路由必须通过特定的 IP 接口（我们假设是 `eth0`，但不必如此）。连接安全网关到客户端的接口必须是不同的。

需要在每个网关上执行 `ipsec-tncfg(8)` 命令。所需的命令是：

```
ipsec tncfg --attach virtual ipsec0--physical eth0
```



还需要运行一个设置 `ipsec0` 虚拟接口的命令。它的参数将与使用 `ipsec_tncfg(8)` 连接物理接口时所使用的参数相同。

## 为 pluto 配置 NETKEY

使用 NETKEY 不需要特殊要求——它随所有现代版本的 Linux 2.4 和 2.6 一起发布，然而某些供应商或旧版发行版使用了损坏的 NETKEY 旧版本或回传版本。如果可能，请使用尽可能基于 Linux 2.6.11 或更新版本或回传的 NETKEY 版本。

## ipsec.secrets 文件

`pluto` 守护进程和另一个 IKE 守护进程（例如另一个 `pluto` 实例）在任何协商成功之前，必须说服彼此他们是他们应当的身份。这种身份验证通过使用预先共享（手动）的密钥或使用 RSA 签名来实现。还有其他技术，但它们尚未在 `pluto` 中实现。

文件 `/etc/ipsec.secrets` 用于保存预共享密钥、RSA 私钥、X.509 编码密钥文件和 XAUTH 密码。智能卡由 NSS 处理。为了调试，`pluto` 命令有一个参数用于使用不同的文件。该文件在 `ipsec.secrets(5)` 中描述。

## 运行 Pluto

要启动守护进程，只需输入 `pluto`（确保已以超级用户身份运行）。默认端口号为 500，IANA 分配给 Pluto 的 UDP 端口必须由超级用户运行才能使用 UDP 500 端口。如果告诉 `pluto` 启用 NAT 穿越（NAT-Traversal），则 UDP 端口 4500 也会被 Pluto 占用监听。

Pluto 支持操作系统上不同的 IP 。可以通过以下选项配置：`--use-netkey`（默认）、`--use-klips`、`--use-bdame`、`--use-win2k`、`--use-nostack`。后者用于测试——实际的 IPsec 连接将加载到内核中。`use-auto` 已过时。启动时，`pluto` 可能会读取协议栈来选择 IPsec 栈，如果同时指定了 `--use-XXX` 和 `--config/ipsec.conf`，最后一个参数优先。

Pluto 支持 RFC 3947 NAT 穿越。NAT 路由器下的允许范围通过 `virtual-private` 提交。语法参见 `ipsec.conf(5)`。`--force-alive` 强制发送心跳包，发送这些包是为了防止 NAT 路由器在流量不足时关闭端口。`keep-alive` 设置心跳包的延迟（秒）。新的 NAT-T 标准支持端口浮，Lib 默认启用。

Pluto 在需要时支持 X.509 证书并进行认证。这可能会让未实现此功能的 IKE 实现感到困惑，例如旧的 FreeS/WAN 实现。`nocrcend` 阻止 `pluto` 发送这些。启动时，`pluto` 会从目录 `/etc/ipsec.d/certs` 一直到 `/etc/ipsec.d/crls` 加载所有 X.509 相关文件。证书撤销列表（CRL）可以从 URL 获取。`--crlckinterval` 设置检查 CRL 过期并发布新获取命令的时间。首次更新尝试将在下次更新前的 `2*crlckinterval` 开始。如果没有为连接加载或获取有效的 CRL，Pluto 将记录警告。如果给出了 `strictpolicy`，则连接将在有效 CRL 加载之前被拒绝。

Pluto 还可以帮助子进程卸载加密操作。这种行为可以通过 `--helpers` 进行精细调整。Pluto 将启动 (n-1) 个辅助进程，其中 n 是 CPU 的数量（包括超线程 CPU）。值 0 强制在主进程中执行所有操作。值 -1 则指示执行上述计算。

Pluto 使用 NSS 加密库作为其随机源。某些政府要求 `pluto` 在从 NSS 库提取随机数之前，从 `/dev/random` 读取 440 位并将其找到 NSS RNG，尽管 NSS 库本身为其内部状态种子。由于此过程可能会阻塞一段时间，默认不执行冗余种子。`--seedbits` 选项可以指定从 `/dev/random` 提取的位数并注入伪随机数生成器（PRNG）。这也可以通过在 `ipsec.conf` 的 "config setup" 部分指定来实现。大多数人不应该使用此选项。

使用 `/var/run/pluto.pid` 创建一个锁。如果无法创建锁，`pluto` 将退出——这防止了多个 `pluto` 实例的竞争。`pluto` 将其 PID 写入此文件，以便脚本可以找到它。如果该文件位于 NFS 卷上，此锁将无法正常工作。

`pluto` 会派叉（fork）并退出。这是传统的“守护进程”模式。这会让调试变得困难，因此有一个选项可以抑制这种派叉。在某些配置中，`pluto` 还会启动辅助进程来协助 DNS 查询或加密操作。

所有日志（包括诊断信息）都发送到 `syslog(3)`，`facility=auth` 决定了这些消息存放的位置（可能在 `/var/log/secure` 或 `/var/log/auth.log`）。由于这可能也会让调试变得困难，因此 `--stderrlog` 选项用于将日志重定向到 stderr。

或者，`--logfile` 可将所有日志发送到特定文件。

如果给出 `--peerlog` 选项，`pluto` 将为每个连接打开一个日志文件。默认情况下，这位于 `/var/log/pluto/`，由点 (.) [IPv4] 或冒号 (:) [IPv6] 的子目录。

可以通过 `--peerlogbase` 修改基础目录。

一旦 `pluto` 启动，它就会等待来自 `whack` 的请求。

## Pluto 的内部状态

为了理解如何使用 `pluto`，了解它的内部状态是有帮助的。此外，需要这些术语来解释某些诊断消息。

`pluto` 支持组和 X.509 证书。这些位于 `/etc/ipsec.d`，或者通过 `--ipsecdir` 指定另一个目录。

`pluto` 可能会进行核心转储（core dump）。它通常会进入当前工作目录。你可以为 `pluto` 指定 `--coredir` 选项，或者在 `ipsec.conf` 中指定 `dumpdir` 选项。

如果你正在调查 `pluto` 中潜在的内存泄漏，使用 `--leak-detect` 选项启动 `pluto`。在泄漏导致系统或 `pluto` 崩溃之前，以常规方式关闭 `pluto`。`pluto` 将显示它检测到的泄漏列表。

（潜在）连接数据库描述了连接的属性。这些包括主机和客户端子集的地址以及所需的安全特性。`pluto` 在响应构建 SA 的请求之前（简单称为连接）需要这些信息。每个连接在创建时会被赋予一个名称，并使用 IKE 名称进行所有引用。

在构建 SA 的 IKE 交换期间，关于协商的信息表示在状态对象中。每个状态对象反映了协商的进度。一旦协商完成并建立了 SA，状态对象将保留以表示该 SA。当 SA 终止时，状态对象会被丢弃。每个状态对象都有一个序列号，用于在日志中引用状态对象。

每个状态对象对应一个连接，可以被视为该连接的一个实例。在任何特定时刻，可能有多个对应特定连接的状态对象。通常有一个代表 ISAKMP，另一个代表 IPsec SA。

KLIPS 挂钩到 LINUX 内核的路由代码。由 IPsec SA 处理的流量必须通过路由命令导向 KLIPS。此外，要执行的处理由 `ipsec eroute()` 命令指定。`pluto` 负责管理这两种特殊路由。

## NETKEY 不需要特殊路由。

每个连接都可以被路由，并且在拥有 IPsec SA 时必须路由。连接指定了路由的特性：此机器上的接口、“网关”（下一跳 hop）以及对端的客户端子网。如果两个连接属于同一个对端客户端子网但使用不同的接口或网关，则不能同时路由（`pluto` 的逻辑并未反映任何高级路由能力）。

在 KLIPS 上，每个路由与 IPsec SA 的状态对象关联，因为它具有 SA 的特定特性。如果两个路由指定了相同的本地和远程客户端，就会冲突（与路由不同，本地客户端会被考虑在内）。

当 `pluto` 需要为连接安装路由时，它必须确保没有正在使用的冲突路由。如果另一个连接具有冲突路由，只要没有 IPsec SA 实例化该连接，该路由就会被关闭。如果存在这样的 IPsec SA，安装路由的尝试将失败。

存在一个异常。如果 `pluto`（响应者）需要为连接安装到固定客户端子网的路由，而已经存在冲突路由，则使用该路由的 SA 将被删除，以为新 SA 留出空间。理由是新连接可能是最新的。这种需求是 Road Warrior 连接的产物（后文将解释；它们无法使用）。

当 `pluto` 需要为 IPsec SA 安装一个区域（针对状态对象）时，必须先对状态对象的连接进行路由（如果无法实现，则不会安装路由和 SA）。如果另一个连接已经有了冲突路由，则不会安装路由和 SA（但注意，上述的路由异常可能已经删除了冲突的 SA）。如果同一个连接已有了路由，新路由将接管。这种特性在重密钥期间会被利用。

## 使用 whack

`whack` 用于命令运行中的 `pluto`。`whack` 使用 Unix 套接字与 `pluto` 通信（默认为 `/var/pluto.ctl`）。

`whack` 拥有复杂的语法。该语法允许指定许多功能。显示显示用法或版本信息。connection 表为 `pluto` 提供潜在连接的描述。public key 表为 `pluto` 提供潜在对端的 RSA 公钥。delete 表删除连接描述及其对应的 SA。list 表让 `pluto` 启动或停止在公共接口上监听来自对端的请求。route 表让 `pluto` 为连接设置路由；unroute 表撤销此操作。initiate 表让 `pluto` 为连接协商 SA，包括正在协商的 SA。status 表让 `pluto` 对应连接的所有 SA，包括已协商的。status 显示 `pluto` 的内部状态。debug 表让 `pluto` 动态更改调试输出的选择。shutdown 表让 `pluto` 关闭并删除所有 SA。

`crash` 选项请求 `pluto` 认为某个目标 IP 已崩溃，并尝试以该 IP 地址作为网关重启所有连接。通常，你应该使用死对端检测来自动检测这种情况，但这并不总是可行。

大多数选项适用于特定的表，并在该表中进行描述。三个选项适用于所有表。

- `--ctlbase path`
`path.ctl` 被用作 `pluto` 通信的 Unix 套接字。此选项有助于调试。
- `--label string`
为 `whack` 生成的所有错误信息添加该字符串。

`whack` 的 help 表自言自明。

- `--help`
显示用法消息。
- `--version`
显示 `whack` 版本。

connection 表描述了 `pluto` 的潜在连接。`pluto` 需要知道哪些连接可以且应该协商。当 `pluto` 是发起者时，它需要知道提议什么。当 `pluto` 作为响应者（responder）时，它需要足够的信息来决定是否愿意建立提议的连接。

连接的描述可以指定大量的细节。每个连接都有一个唯一的名称。该名称将出现在 updown 命令中，因此它不应包含会导致命令格式错误的标点符号。

- `name connection-name`
设置连接的名称

连接的拓扑是对称的，因此为了节省空间，这里显示了一半图：

`client_subnet<--ikeport<--nexthop>`

标志（flags）中使用了一种巧妙的技巧。标志名称同时用于两端。— 符号之前的标志描述左侧，— 符号之后的标志描述右侧。当 `pluto` 尝试使用该连接时，它会根据其接口的 IP 地址来判断自己是连接的左侧还是右侧。

- `id id`：端的身份。目前，这可以是一个 IP 地址（指定为点分四位格式或完全限定域名本身（前缀加“”以表示不进行解析））、或者是 `user@FQDN`、`X.509 DN`，或者值 `%myid`。Pluto 仅对身份进行验证，而不将其用于寻址，例如，IP 地址不需要是数据包发送到的那个地址。如果缺少此选项，身份默认为由—host 指定的 IP。`%myid` 允许单独指定身份（通过 `pluto` 或 `whack` 选项—myid，或者通过 `ipsec.conf(5)` 配置设置参数 myid）。否则，`pluto` 会尝试猜测 `%myid` 代表什么：如果该 IP 的响应中由适当的 TXT 记录支持，则为 `%default` 的 IP；如果在系统的正向记录中由相应的 TXT 记录支持，则为系统的主机名。

- `host ip-address`, `--host %any`, `--host %opportunistic`：端的 IP 地址（通常是公网接口）。如果 `pluto` 要充当从未知 IP 地址发起的 IKE 协商的响应者（路边游兵案例），则应将 IP 地址指定为 `%any`（目前也接受过时的表示法 0.0.0.0）。如果让 `pluto` 机会发起连接，请使用 `%opportunistic`。

- `cert filename`：X.509 证书的文件名。这必须仅是公钥证书，不能是 PKCS#12 证书文件。请参考 `ipsec.conf(5)` 关于如何从 PKCS#12 文件中提取它。

## ca distinguished name
X.509 证书颁发机构的名称（DN），作为此连接的信任锚。这是签署主机证书的 CA 证书，以及传入客户端的证书。

## --groups access control groups
使用的访问控制组。

## --sendcert yes|forced|always|ifaked|no|never
是否发送我们的 X.509 证书凭据。这可能会给攻击者提供过多关于哪些身份允许连接到此主机的信息。当作为响应者时，默认为 ifaked；当作为发起者（Initiator）时，默认为 yes（这与 forced 和 always 等同）。no 和 never 是等的。注意：“forced”似乎并未实际实现 - 请勿使用它。

## --sendca none|issuer|all
随端证书一起发送多少我们可用的 X.509 信任链（排除根 CA）。指定 issuer 仅发送颁发中间 CA，而 all 则会发送整个中间 CA 链。none 将不发送任何 CA 证书。默认是 none，以保持当前的 libreswan 行为。

## --certificate type number
X.509 证书类型数字。

## --ikeport port-number
在该主机上 Ike 监听的 UDP 端口。默认值为 500。（本台机器上的 `pluto` 使用其自身命令行参数指定的端口，因此这仅影响 `pluto` 发送消息的位置。）

## --nexthop ip-address
向对端客户端路由数据包的位置（推测也用于对端，但不会在此使用）。当 `pluto` 安装 IPSec 时，它会发布路由命令。它使用 nexthop 作为网关。默认是对端的 IP 地址（可以显式写为 `%direct`；接受过时的表示法 0.0.0.0）。如果 `pluto` 主机用于向对端发送数据包的接口既不是点对点也不是与对端直接连接，则此选项是必要的。

## --client subnet
IPsec 流量的目标子网。如果未指定，主机将作为客户端。子网可以使用 `ipsec_atossubnet(3)` 支持的任何形式指定。通用格式是地址/掩码。地址可以是域名，也可以是用点分隔的四个十进制数字（指定字节）。掩码最方便的形式是十进制整数，指定掩码中起始比特数。例如，`10.0.0.0/8` 将指定 A 类网络“Net 10”。

## --clientwithin
此选项已过时并将删除。请停止使用此选项。

## --clientprotoport protocol/port
指定在此连接上使用的端口选择器（过滤器）。通用格式为协议/端口。这最常用于将连接限制为 L2TP 流量，通过为 UDP（协议 17）和端口 1701 指定 `17/1701`。表示法 `17/%any` 可允许所有 UDP 流量，适用于与 Service Pack 2 之前的 Windows XP 节点的 L2TP 连接。

## --srcip ip-address
此主机在向远程 ipsec 网关本身传输数据包时使用的 IP 地址。此选项用于让网关本身使用其内部 IP，该 IP 是 `--client subnet` 的一部分。否则它将使用最近的 IP 地址，该地址不在子网间 IPsec 隧道中，因此不会被加密。

## --authserver
此端是认证服务器（authserver）。它将在允许连接建立之前查找 xauth 用户名和密码并进行验证。

## --xauthclient
此端是认证客户端（xauthclient）。使用 `--initiate` 建立此连接时还需要客户端指定 `--xauthuser` 用户名和 `--xauthpass` 密码。

## --xauthuser
xauth 认证的用户名。当使用 `ipsec auto --up conn  xauth` 连接时，此选项由 `ipsec_auto(8)` 传递。

## --xauthpass
xauth 认证的密码。此选项通常传递。

## --modeserver
此端是认证服务器（modeserver）。

## --modeclient
此端是认证客户端（modeclient）。

## --modecfg1
第一个 DNS 的 IP 地址

## --modecfg2
第二个 DNS 的 IP 地址

## --dnsdemands
指定需要 RSA 密钥

## --updown
指定每当 `pluto` 建立或关闭连接时运行的外部命令。脚本会传递多个关于连接的环境。

## --psk
为 IKE 对端提议并允许预共享密钥（PSK）认证。此认证要求双方使用相同的密钥。

## --rsasig
为 IKE 对端认证提议并允许 RSA 签名。

主机将是什么。这并不意味着——隧道，以便在未实际指定隧道时可以安全地使用该标记。请注意，对于连接，所有隧道地址必须属于相同的地址族（Address Family）。

## -pfs
应该具有完全前向密钥（Perfect Forward Secrecy）——每个 IPsec SA 都会生成新的密钥材料，而不是派自 ISAKMP SA 的密钥材料。由于使用的组组无法协商（这是标准中的一个可疑特性），**pluto** 将提议与阶段 1 期间使用的相同组。我们没有实现更强形式的 PFS，那将需要在协商 IPSEC SA 之后删除 ISAKMP SA。

## -disablearrivalcheck
如果连接是隧道，则允许通过隧道到达的封包具有任何源地址和目的地址。

## -esp esp-algos
用于连接（阶段 2，即 IPsec SA）的 ESP 加密/认证算法。这些选项必须适用于 **ipsec_spi(8)** 的值。有关算法格式的详细说明，请参阅 **ipsec.conf(5)**。

## -aggmode
此隧道使用激进模式（aggressive mode）ISAKMP 协商。默认是主模式（main mode）。激进模式比主模式不安全，因为它会向窃听者暴露你的身份，但它支持使用 PSK 密钥的远程战士（warriors），或与坚持使用激进模式的其他缺陷实现相互操作。

## -modecfgpull
从对端拉取模式配置（Mode Config）网络信息。

## -dpddelay seconds
设置用于此连接的死亡对端检测（RFC 3706）心跳（R_U_THERE, R_U_THERE_ACK）之间的延迟（秒）（默认为 30 秒）。

## -timeout seconds
设置我们在没有听听到来自对端的 R_U_THERE 轮询或 R_U_THERE_ACK 回复的情况下空闲的时间（秒）。如果在此时间过去后没有响应且没有流量，我们将宣布对端死亡并移除 SA（默认为 120 秒）。

## -dpdaction action
当 DPD 对端被声明为死亡时，应该采取什么操作。
hold（默认）意味着路由将被置于 `%hold` 状态，而 clear 意味着同时清除路由和 SA。Clear 实际上仅在 Road Warrior 配置的服务器上有用。action restart 用于需要永久连通且具有静态 IP 地址的隧道。action restart_by_peer 已废弃，其功能已移动到 restart 操作中。

## -forceencaps
在某些情况下，例如当 ESP 节点被过滤或当损坏的 IPSec 对端无法正确识别 NAT 时，使用此选项强制进行 RFC-3948 封装可能有用。它会让 `pluto` 告诉远程对端需要 RFC-3948 封装（UDP 端口 4500 数据包中的 ESP）。

如果未设置 —encrypt、—authenticate、—compress 或 —pfs 标记，发起连接的一端将仅构建 ISAKMP SA。对于此类连接，客户端子网没有意义且不能指定。

除了直接使用 —initiate 选项直接启动外，隧道还可以使用不同的策略加载。

## -initiatetraffic
只有当我们有流量要通过连接发送时，才发起连接。

## -pass
允许未加密的流量流动，直到隧道建立。

## -drop
静默丢弃未加密流量。

## -reject
静默丢弃未加密流量，但发送 ICMP 消息通知另一端。

这些选项需要编写文档：

## -failnone
待文档。

## -failpass
待文档。

- -faildrop
待文档。

- -failreject
待文档。

`pluto` 支持各种与 X.509 证书相关的选项。

- -utc
以 UTC 显示所有时间。

- -listall
列出 `pluto` 已知的所有 X.509 信息。

- -listpubkeys
列出所有成功加载的公钥。

- -listcerts
列出所有当前加载的 X.509 证书。

- -checkpubkeys
列所有即将过期或已过期的 X.509 证书。

- -listacerts
列出所有当前加载的 X.509 证书颁发机构（CA）证书。

- -listacerts
列出所有当前加载的 X.509 属性证书。

- -listaacerts

- -listgroups

- -listcrls
列出所有加载的证书吊销列表（CRLs）

相应的选项—rereadsecrets—rereadall—rereadcerts,—rereadacters,—rereadacters, 和 —rereadcrl 从它们各自的源重新读取这些信息，并清除所有在线获得的信息.—listevents 选项列出所有 CRL 获取命令。

还需要更多工作来允许灵活策略。目前策略硬编码在 `spdb.c` 文件中。ISAKMPs 可能使用 Oakley 组 MODP1024 和 MODP1536；AES 或 3DES 加密；SHA1-96 和 MD5-96 认证。IPSec SAs 的 ESP 可能使用 AES 或 3DES 以及 MD5-96 或 SHA1-96，或者 AH 仅使用 MD5-96 或 SHA1-96。IPCOMP 压缩始终使用 Deflate。

## —iketimes seconds
**pluto** 提议允许 ISAKMP SA 多久。默认为 3600（一小时）。

## —ipsecetime seconds
**pluto** 提议允许 IPSec SA 多久。默认为 28800（八小时）。

## —rekeymargin seconds
**pluto** 提议允许 ISAKMP SA 多久。默认为 540（九分钟）。

## —rekeymargin percentage
**pluto** 提议允许 IPSec SA 多久。默认为 100。

## —keyingtries seconds
**pluto** 应该尝试协商 SA 的次数，无论是首次协商还是重密钥。默认为三次。

## —dontrekey
误导性名称（不重密钥）。只有当我们是发起方且连接上近期有流量时，才重密钥连接。这适用于阶段 1 和阶段 2。这对于 Road Warrior 或 机会性连接可能有用。由于 SA 是任听随缘的，响应者通常使用配置中较短的一个。

尝试设置一个。

## --initiate, --name connection-name, --asynchronous
`whack` 命令的初始化形式将通过 UNIX 域套字回传 `pluto` 状态信息（除非指定了 `--asynchronous`）。该状态信息看起来类似于 FTP 的信息。目前 `whack` 仅简单将其复制到 stderr。当请求完成时（例如 SA 建立建立或 `pluto` 放弃），`pluto` 将关闭通道，导致 `whack` 终止。

机会性初始化形式主要用于调试。

## --tunnelipv4, --tunnelipv6, --oppothere ip-address, --oppothere ip-address
这将导致 `pluto` 尝试从这里到那里机会性地发起连接，即使之前已经尝试过。`whack` 日志将显示此尝试的进度。

结束连接

## --terminate, --name connection-name
terminate 形式告诉 `pluto` 删除使用指定连接的 SA，以停止任何正在进行的协商。它不会阻止新协商的启动（delete 形式具有此效果）。

## --crash ip-address
如果远程对端已崩溃，因此没有通知我们，我们将继续发送加密流量，并拒绝来自远程对端的所有明文（非 IKE）流量。`--crash` 会导致我们端指向指定 ip-address 的已知连接也关闭。

## --whackrecordfilename, --whackstoprecord
这导致 `pluto` 打开指定的文件进行写入，并记录从 `whack` 或 `addconn` 到的每条消息。这将一直持续到使用 whackstoprecord 选项。此选项可能与其他任何命令组合。启动/停止命令本身不会被记录。这些文件通常用于创建单元测试的输入文件，特别是对于实际上可能重叠的复杂设置。

文件格式由以 `#-whack` 开头的行、文件开始的日期作为主机名以及换行符组成。后续是二进制格式，包括一个 32 位的记录长度（包含长度记录本身）、一个 64 位的时间戳，然后接收到的 `whack` 消息的原始内容。所有整数均为主机格式。为了无歧地确定主机字节，第一条记录是一个仅包含当前 WHACK_MAGIC 值的空记录。该记录长度 16 字节。

## ip-address
如果远程对端已崩溃，因此没有通知我们，我们将继续发送加密流量，并拒绝来自该远程对端的所有明文（非 IKE）流量。`--crash` 会导致我们端指向指定 ip-address 的已知连接也关闭。

公钥告知 `pluto` 潜在对端的 RSA 密钥。私钥必须保密，因此它们存储在 `ipsec.secrets(5)` 中。

## -keyid id
指定应使用公钥的对端身份。其格式与连接中的身份相同。如果没有指定公钥，`pluto` 将尝试从 DNS 查找该 id 的 KEY 记录（如果是 FQDN）或通过反向查找（如果是 IP 地址）。请注意，这种方式在安全性方面有几种非常趣的实现方法。

## -addkey
指定将新密钥添加到集合中；否则新密钥将替换任何旧密钥。

## -pubkeyrsa key
指定 RSA 公钥的值。它是 RFC 2537《域名命名系统 (DNS) 中的 RSA/MD5 KEYS 和 SIGs》中描述的字节序列。它以适用于 `ipsec_ttodata(3)` 的方式表示。例如，base 64 数字以 0 开。

列表形式告诉 `pluto` 开始在它的公共接口上监听 IKE 请求。为了避免竞态条件，在允许其监听之前，将适当的连接加载到 `pluto` 中是正常的。如果 `pluto` 没有监听，发起协商就没有意义，因此它将拒绝这样做。当使用监听形式时，`pluto` 会寻找公共接口，并在新接口被添加和旧接口被移除时注意到。这也是 `pluto` 读取 `ipsec.secrets` 文件的触发器。因此 listen 可能会多次执行。

## -listen
开始在公共接口上监听 IKE 流量。

## -unlisten
停止在公共接口上监听 IKE 流量。

status 形式将显示关于 `pluto` 内部状态的信息：关于每个潜在连接、每个状态对象以及 `pluto` 正在管理但没有关联连接的每个 shunt 的信息。

## --status
trafficstatus 形式将显示 xauth 用户名、add_time 以及 IPsec SA 的总入/出字节数。

## --trafficstatus
shutdown 形式是关闭 `pluto` 的正确方法。它将拆除此机器上 `pluto` 协商的 SA。它不会通知对端，因此它们机器上的 SA 仍然存在。

## --shutdown

## 示例

在系统初始化脚本之一中启动 `pluto` 是正常的。它需要由超级用户运行。通常，不需要参数。要手动运行，超级用户只需输入：

- `ipsec pluto`

命令将立即返回，但会留一个运行中的 `pluto` 进程等待来自 `whack` 或对端的请求。

使用 `whack`，将描述几个潜在连接：

- `ipsec whack --name silly --host 127.0.0.1 --to --host 127.0.0.2 --ikelifetime 900 --iplifetime 800 --keyingries 3`

由于此连接描述未指定加密、认证或隧道，因此它只能用于建立 ISAKMP SA。

- `ipsec whack --name conn_name --host 10.0.0.1 --client 10.0.1/24 --to --host 10.0.0.2 --client 10.0.2/24 --encrypt`

这种方式在我们不希望立即建立两个客户端之间的安全连接，这是必须在双方都执行的。如果对方是 `pluto`，可以使用相同的 `whack` 命令（命令语法设计为不区分哪方）。

现在连接已指定，`pluto` 准备好通过公共接口处理请求和响应：

- `ipsec whack --listen`

为了防止不安全流量，路由形式要求 `pluto` 将从我们客户端发送的数据包通过 ipsec 设备路由；如果没有 SA，它们将被丢弃：

- `ipsec whack --route conn\_name`

最后，我们准备好使用 `pluto` 发起 IPSec SA 的协商（隐含地包括 ISAKMP SA）：

- `ipsec whack --initiate --name conn\_name`

感兴趣事件的小日志将出现在标准输出上（其他日志发送到 syslog）。

`whack` 也可以用于安全终止 `pluto`，拆除它已协商的所有 SA。

- `ipsec whack --shutdown`

任何 IPSEC 删除但 ISAKMP SA 删除的通知将发送到对端。遗憾的是，这种通知不可靠。此外，`pluto` 本身忽略通知。

## XAUTH

如果 `pluto` 需要额外的认证（如 XAUTH 规范定义的），它可能会使用 `whack` 提示操作员用户名或密码。通常，这些是交互式输入的。`whack` 的 GUI 可能会查找 041（用户名）或 040（密码）提示并将其显示给用户。

为了测试目的，可以在 `--initiate` 之前提供 `--xautouser user --xauthpass pass` 选项，为用户名和密码提示提供响应。

updown 命令

每当 `pluto` 建立或关闭连接时，都会调用 updown 命令。该命令通过 `--updown` 选项指定。这允许对路由和防火墙管理进行自定义。

updown 被五个不同的操作调用。这些操作中的每一个都可以针对我们的客户端子网或针对我们的主机本身。

**prepare-host** 或 **prepare-client**

在没有其他相同客户端开启的情况下建立新连接运行时。通常，这是为了删除在运行 `pluto` 之前或由某些不知道 `pluto` 的代理设置的路由。

**route-host** 或 **route-client**

在为新的对端客户端子网建立连接运行时（即使运行了 prepare-host 或 prepare-client）。该命令应安装合适的路由。路由决策仅基于目标（对端客户端）子网地址，与 eroutes 不同，后者也会根据源地址进行区分。

- unroute-host 或 unroute-client
在关闭特定对端子网的最后一个连接时运行。
它应该撤销 route-host 或 route-client 所执行的操作。

- up-host 或 up-client
在启动一个尚未具有隧道路由的、客户端子网的隧道 eroute 时运行。
此命令应该根据情况安装防火墙规则。通常情况下，允许 IKE 消息（UDP 端口 500）在主机之间传输是一个好好主意。

- down-host 或 down-client
在关闭一对客户端子网的 eroute 时运行。
此命令应该根据情况删除防火墙规则。注意，可能仍然存在一些与这些客户端子网关联的入站 IPsec SA。

脚本将接收到大量的环境变量，以指定需要执行的操作。

## PLUTO_VERSION
指示正在使用的此接口版本。本文描述的是版本 1.1。该版本与 1.0 版本向上兼容。

## PLUTO_VERB
指定要执行的操作名称（prepare-host、prepare-client、up-host、up-client、down-host 或 down-client）。如果安全网关到安全网关通信的地址族为 IPv6，则会在动词后加上 -v6。

## PLUTO_CONNECTION
我们正在路由的连接名称。

## PLUTO_NEXT_HOP
发往对端的包必须发送的下一跳地址。

## PLUTO_INTERFACE
将使用的 ipsec 接口名称。

## PLUTO_ME
我们主机的 IP 地址。

## PLUTO_MY_CLIENT
我们客户端子网的 IP 地址 / 数量。如果客户端仅为主机，则将是主机自身的 IP 地址 / 最大值（IPv4 为 32，IPv6 为 128）。

## PLUTO_MY_CLIENT_NET
我们客户端网络的 IP 地址。如果客户端仅为主机，则将是主机自身的 IP 地址。

## PLUTO_MY_CLIENT_MASK
我们客户端网络的掩码。如果客户端仅为主机，则将是 255.255.255.255。

## PLUTO_PEER
对端的 IP 地址。

## PLUTO_PEER_CLIENT
对端客户端子网的 IP 地址 / 数量。如果客户端仅为对端，则将是对端自身的 IP 地址 / 最大值（IPv4 为 32，IPv6 为 128）。

## PLUTO_PEER_CLIENT_NET
对端客户端网络的 IP 地址。如果客户端仅为对端，则将是对端自身的 IP 地址。

## PLUTO_PEER_CLIENT_MASK
对端客户端网络的掩码。如果客户端仅为对端，则将是 255.255.255.255。

## PLUTO_MY_PROTOCOL
列此 IPsec SA 上允许的协议。

## PLUTO_PEER_PROTOCOL
列对端在此 IPsec SA 上允许的协议。

## PLUTO_MY_PORT
列此 IPsec SA 上允许的端口。

## PLUTO_PEER_PORT
列对端在此 IPSec SA 上允许的端口。

## PLUTO_MY_ID
列我们的 ID。

## PLUTO_PEER_ID
列对方 ID。

## PLUTO_PEER_CA
列对端的 CA。

脚本发送到 stderr 或 stdout 的所有输出都会被记录。脚本仅在成功时才应返回退出状态 0。

Pluto 会等待脚本完成，并在等待期间不会进行任何处理。脚本可以假设在脚本运行期间 pluto 不更改任何内容。脚本应避免任何耗时的操作，并且不发布任何需要 pluto 处理的命令。这些活动均可以通过脚本的后台子进程完成。

## 重密钥 (Rekeying)

当由 `pluto` 发起的 SA 仅剩一点生命周期时，`pluto` 将启动创建新的 SA。这适用于 ISAKMP 和 IPSec SA。当 SA 的剩余生命周期小于 rekeymargin 加上一个在 0 到 rekeyfuzz 之间的随机百分比时，将触发重密钥。

同样地，当由对端发起的 SA 仅剩一点生命周期时，`pluto` 将尝试启动创建替换连接。为了优先考虑发起者，只有当 SA 的剩余生命周期为 rekeymargin 的一半时才会启动重密钥。如果重密钥是由响应者执行的，则角色将反转：旧 SA 的响应者将成为替换 SA 的发起者。之前的发起者也可能发起重密钥，因此可能会创建冗余的 SA。为了避免这些复杂情况，请确保重密钥设置足够充裕。

让之前的响应者发起的风险在于，其提议中可能没有一个是被之前的发起者接受的（它们未在成功的协商中使用过）。为了减少这种情况发生的概率并防止安全性的丢失，策略设置将从旧 SA 获取（当之前的发起者发起时情况此类此）。这些设置可能比连接本身的设置更严格。

如果 SA 不是其类型（IPSec 或 ISAKMP）中最新的，`pluto` 将不会对其进行重密钥。

重密钥中的随机部分（rekeyfuzz）旨在防止出现某些病态模式。如果双方同时决定重密钥，将创建双倍的 SA。这可能会导致资源峰值需求（带宽、CPU）。这些连接可能同时需要重密钥。可以使用 rekeyuzz 来错开重密钥。

## 在进行时选择连接：移动支持 (Road Warrior)

当 `pluto` 接收到初始模式（Initial Mode）消息时，它需要决定适用于哪个连接。它根据消息的源和目的 IP 地址进行选择。如果存在多个合适的 IP 地址，则随机选择其中一个。（消息中提出的 ISAKMP SA 本可以被考虑，但此处并未这样做。）

由于 ISAKMP SA 在进一步标识信息之前就已经协商，因此具有相同 IP 地址的所有连接的 ISAKMP 特性应该是相同的。目前，唯一可能不同的是身份验证方法。

到目前，所有配置都确保 IP 地址是预知的。当终端是移动的（或由于原因分配了动态 IP 地址）时，这将无法工作。我们称之为“Road Warrior”。它相当复杂并具有一些限制，大部分是 IKE 协议的特性。

只有发起者可能是移动的：响应者未知 IP 地址。当响应者在第一个主模式包上无法识别 IP 地址时，它会寻找一个自身为、%any 为其他的连接。如果找不到，则拒绝协商。如果找到了，将创建一个临时连接，除了将 %any 替换为包中的源 IP 地址外；如果没有为对方指定身份，则将使用新的 IP 地址。

当 `pluto` 使用这些临时连接并需要在 `ipsec.secrets` 中查找密钥或 RSA 私钥时，如果连接未为对方指定身份，则使用 %any 作为其身份。毕竟，真实的 IP 地址对配置显然是未知的，因此要求出现在表中是不合理的。

在使用其中一种连接描述进行第一阶段（主模式）协商的中途中，`pluto` 将收到身份负载（Identity Payload）。此时，`pluto` 会检查是否存在更合适的连接，其对方身份与负载匹配且使用相同的认证密钥。如果找到，它将切换到使用该连接（如果它对对方 IP 地址使用的是 %any，则使用其派生的临时连接）。最后结果可能是没有匹配的连接
新发现的身份，包括当前的连接；如果是，**pluto** 将终止协商。

遗憾的是，如果正在使用预共享密钥（preshared secret）认证，则身份负载（Identity Payload）将使用该密钥进行加密，因此响应者在知道此负载的情况下必须选择该密钥。这限制了连接到主机的所有路路战士（Road Warrior）系统最多只有一个预共享密钥。RSA 签名认证不需要响应者在解码启动者的身份负载后知道如何选择启动者的公钥（使用响应者的私钥进行解码，因此该密钥应该是预先选定的）。

当 **pluto** 通过这些临时连接描述之一响应快速模式（Quick Mode）协商时，它可能会发现启动者指定的子网与临时连接描述中的子网不匹配。如果是这样，它将寻找具有匹配子网、自己的主机地址、对端地址为 **%any** 且身份匹配的连接。如果找到了，将从该连接派生出一个新连接，并用于 IPsec SA 的快速模式协商。如果未找到，**pluto** 将终止协商。

请确保为响应者指定一个向启动者发送消息的适当下一跳（nexthop）：**pluto** 没有办法猜测它（如果未使用使用转发，请使用显式的 **%direct** 作为下一跳，并将填充启动者的 IP 地址；过时的 0.0.0.0 仍然被接受）。

**pluto** 在启动者端没有特殊位置。在定义连接时，必须使用当前的（可能是动态的）IP 地址和下一跳。每次启动者的 IP 地址更改时，必须正确配置这些内容。**pluto** 没有自动机制来执行此操作。

尽管我们称之为“路路战士支持”（Road Warrior Support），但它也可以用于支持匿名启动者的加密连接。响应者的组织可以宣布与未识别启动者使用的预共享密钥，并允许任何人连接。当然，启动者的身份将不会通过认证。

如果支持任何路路战士连接，**pluto** 在确定密钥未共享或签名无效之前，无法拒绝由未知主机发起的交换。它必须等待启动者的第三次主模式（Main Mode）协商。如果不支持任何路路战士连接，来自未知源的第一条消息将被拒绝。这对于配置调试的易用性以及拒绝服务攻击有影响。

虽然路路战士连接必须由移动端发起，但另一侧将重新密钥它已创建的临时连接。如果路路战士希望能够断开连接，明智的做法是在非移动端的连接上将 **-keyintries** 设置为 1，以防止尝试对连接重密钥。遗憾的是，没有自动取消路由连接的机制。

## 调试

`pluto` 接受几个可选参数，主要用于调试。除了 --interface 外，每个参数最多出现一次。

- `--interface interface` 指定应考虑的具名真实公网网络接口。指定的接口名称不应该是 `ipsec-N`。如果该选项未出现，则考虑所有接口。要指定多个接口，请为每个接口使用一次该选项。该选项的一个用途是指定当两个或多个接口共享相同 IP 地址时，应该使用哪个接口。
- `--ikeport port-number` 更改 `pluto` 将使用的 UDP 端口（默认由 IANA 指定：500）
- `--ctlbase path basename` 控制文件的路径、文件名。`path.ctl` 是 `whack` 与 `pluto` 通信的套接字。`path.pid` 是防止多个 `pluto` 实例的锁文件（默认是 `/var/run/pluto/pluto`）。
- `--secretsfile` 指定认证密钥文件（默认：`/etc/ipsec.secrets`）。此名称遵循如 `sh(1)` 中的“通配符”（globbing），每个匹配名称的文件都会被处理。通常需要引号以防止 shell 执行通配符。
- `--adns path to adns` 指定查找 `pluto` 用于异步 DNS 查找的辅助程序的路径。`pluto` 可以编译为使用 _pluto_adns。默认情况下，`pluto` 会在 IPSEC_DIR（如果定义了该环境变量）中查找该程序，否则在与 `pluto` 相同的目录中查找。
- `--nofork` 禁用 --daemon fork”（默认是派生）。此外，在创建锁文件和控制套接字后，向标准输出打印行“Pluto initialized”。
- `--uniqueds` 如果选择了此选项，每当建立新的 ISAKMP SA 时，任何具有相同 Peer ID 但具有不同 Peer IP 地址的连接都将取消路由（导致其所有 SA 被删除）。这有助于在连接丢失并在另一个 IP 地址处恢复时清理悬挂的 SA。
- `--force-busy` 如果选择了此选项，`pluto` 将强制处于“忙忙”状态。在这种状态下（发生拒绝服务攻击时），将强制 `pluto` 在接受传入的 IKE 包之前使用 Cookie。Cookie 在 ikev1 激进模式和 ikev2 中被发送并需要。此选项主要用于测试目的，但也可以被多疑的管理员选择。
- `--stderrlog` log 记录到标准输出（默认使用 `syslog(8)`）

例如：
```
pluto --secretsfile ipsec.secrets --ctlbase pluto.base --ikeport 8500 --nofork --use-nostack --stderrlog
```
允许在不使用超级用户账户的情况下测试 `pluto`。

`pluto` 愿意产生大量的调试信息。为了做到这一点，必须使用 -DDEBUG 进行编译。有几类调试输出，`pluto` 可以被指示产生其中某些类。所有调试输出行都带有“ ” 前缀，以与错误消息区分开来。

当 `pluto` 被调用时，可以给出参数来指定输出哪些类。当前的选项有：

- `-debug-none` 禁用调试
- `-debug-all` 启用所有调试
- `-debug-raw` 显示原始字节
- `-debug-crypt` 显示加密和解密
- `-debug-parsing` 显示输入结构
- `-debug-emitting` 显示输出结构
- `-debug-control` 显示 `pluto` 的决策
- `-debug-controlmore` 显示更详细的 `pluto` 决策
- `-debug-lifecycle [此选项为临时]` 显示生命详情
- `-debug-klips` 显示 `pluto` 与 KLIPS 的交互
- `-debug-pfkey` 显示 `pluto` 与 PFKEY 的交互
- `-debug-dns` 显示 `pluto` 与 DNS 的交互
- `-debug-dpd` 显示对端检测（DPD）
- `-debug-natt` 显示 NAT 穿透的处理
- `-debug-oppo` 显示 `pluto` 为什么没有找到合适的 SA
- `-debug-oppinfo` 在启动连接时记录
- `-debug-busy` 在由于密钥启动时记录
- `-debug-whack` 如果设置，会导致 `pluto` 在 SA 建立之前释放通道
- `-debug-private` 允许带密钥的调试

例如：
```
pluto --secretsfile ipsec.secrets --ctlbase pluto.base --ikeport 8500 --nofork --use-nostack --stderrlog
```
允许在不使用超级用户账户的情况下测试 `pluto`。

要启动 `pluto` 并显示输入输出结构：
```
pluto --debug-emitting --debug-parsing
```
稍后将此更改为 仅显示原始字节：
```
whack --debug-raw
```

IANA Pluto 还避免了选择 0x100 到 0xFF 范围内的 SPI，将这些 SPI 留作手动指定。请记住，如果对方不是 Pluto，可能会选择此范围内的 SPI。

# 策略

在尝试配置 Pluto 和另一个 IKE 实现进行互操作时，策略目录可能会很有用。

在阶段 1 中，仅支持主模式（Main Mode）。我们不确定主动模式（Aggressive Mode）是否安全。其一在于，它不支持身份保护。它可能允许更严重的拒绝服务攻击。

不支持信息交换（Informational Exchanges）。这些是可选的，且由于其交付性无法保证，因此它们不应该产生影响。虽然在没有信息交换的情况下 IKE 实现将无法互操作，但我们认为它们是有缺陷的。

不支持信息载荷（Informational Payloads）。这些是可选的，但很有用。令人担忧的是，这些载荷在阶段 1 中以及那些使用 HASH(3) 验证的阶段 2 消息中未经过身份验证。

> 支持 Diffie-Hellman 组 MODP 1024 和 MODP 1536 (2 和 5)。不支持组 MODP768 (1)，因为它太弱了。

主机身份验证可以通过 RSA 签名或预共享密钥完成。

3DES CBC（密码块链模式）是唯一支持的加密算法，适用于 ISAKMP SA 和 IPSec SA。

两种 SA 的数据包身份验证都支持 MD5 和 SHA1 哈希算法。

支持 ESP、AH 或 AH ESP。只有当且仅当 AH 和 ESP 结合时，ESP 才不需要自己的认证组件。选择由 --encrypt 和 --authenticate 标志控制。

这些中的每项都可能与 IPCOMP Deflation 结合，但仅当潜在连接指定了压缩时，且仅当 KLIPS 配置了 IPCOMP 支持时才如此。

IPSEC SA 可以根据情况采用隧道模式（tunnel mode）或传输模式（transport mode）。当 `pluto` 发起时，由 --tunnel 标志控制。

响应 ISAKMP SA 提议时，最大可接受的寿命为八小时。默认为一小时。没有最小限制。--ikelifetime 标志在 `pluto` 发起时控制。

响应 IPS SA 提议时，最大可接受的寿命为一天。默认为八小时。没有最小限制。--ipseclifetime 标志在 `pluto` 发起时控制。

PFS 是接受的，如果指定了 --pfs 标志，将提议 PFS。提议的 DH 组将与阶段 1 协商的组相同。

# 信号

Pluto 响应 SIGHUP 时发出建议，暗示可能意图执行“whack—listen”。

Pluto 在接收到 SIGTERM 时退出。

## 退出状态

`pluto` 通常会派生守护进程，因此退出状态通常是一个非常初步的结果。



0

意味着到目前一切正常。

1

意味着出现了某些错误。

10

意味着锁文件已存在。

如果 `whack` 检测到问题，它将返回退出状态 1。如果收到来自 `pluto` 的进度消息，它返回最后一条非发送到 syslog 或非注释的消息的数字前缀作为状态（但成功的前缀被视为 0）。否则，退出状态为 0。

## 文件

```
/var/run/pluto/pluto.pid
/var/run/pluto/pluto.ctl
/etc/ipsec.secrets
/dev/urandom
```

# 环境

`IPSEC_EXECDIR` `IPSEC_myid` `PLUTO_CORE_DIR`

## 另参

`Libreswan` 分发的其余部分，特别是 `ipsec(8)`。

`ipsec_auto(8)` 设计用于让使用 `pluto` 更加愉快。使用它！

`ipsec_secrets(5)` 描述密钥文件的格式。

`ipsec_atoaddr(3)` 是 `Libreswan` 分发的一部分，描述了 IP 地址可能的形式。`ipsec_autosubnet(3)` 是 `Libreswan` 分发的一部分，描述了子网规格的形式。

有关 IPsec、邮件列表和相关文档的更多信息，请参：

https://datatracker.ietf.org/wg/ipsecme/charter/

此时，最相关的 IETF RFC 有：

RFC5996 密钥交换协议版本 2 (`IKEv2`)

`Libreswan` 网站 <https://libreswan.org> 以及那里描述的邮件列表。

另请查看主目录下的 `CHANGES/CREDITS` 文件和 `doc/` 目录。

# 缺陷

请访问 <https://bugs.libreswan.org/> 查看已知 bug 和缺失功能的列表。

缺陷应报告至 <swan-dev@lists.libreswan.org> 邮件列表。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC READWRITECONF

## 名称
`ipsec_readwriteconf` - 验证并输出 Libreswan IPsec 配置文件

## 摘要

`ipsec readwriteconf [--config file] [--debug] [--verbose] [--rootdir dir]`

## 描述

此程序读取给定的 `ipsec.conf` 样式配置文件，解释备选项，并输出等效的 `ipsec.conf`。该程序的目的是验证语法。`--rootdir` 选项更改输入。`--debug` 和 `--verbose` 是同义词。默认值为 `gethostname(2)` 的返回值。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_RSASIGKEY

## 名称
`ipsec_rsigkey` - 生成 RSA 签名

## 摘要

`ipsec rsasigkey [--config dir] [--random device] [--seed nbits] [--hostname hostname] [--password nbits]`

## 描述

`Rsasigkey` 生成一对适用于数字签名的 RSA 公私钥，长度为（精确）`nbits`，并将其输出到标准输出。公指数被强制设置为 3，这具有已知弱点。`verbose` 选项在准备绪保持安静。`random` 选项指定源。默认是 `/dev/random`。然而，不应通过此选项直接访问，因为硬件故障会导致极不随机的值（世界上观察到了零流）。`seedsbit` 选项指定从随机设备提取多少种子来填充 NSS PRNG。种子向上取到 8 的倍数。当系统在 FIPS 模式运行时，防止使用不同的随机设备或重定向种子。`configdir` 选项指定使用的 NSS 配置。这是 NSS 证书、密钥和安全模块所在的目录。默认值为 `/etc/`。`password` 选项在 NSS 模块已配置时指定 NSS 模块认证密码。硬件令牌以及配置的内部软件模块都需要密码。如果参数是 `configdir/npassword`，密码来自该文件；否则参数为密码。`hostname` 选项指定输出第一行使用的主机名（见下文）；默认值为 `gethostname(2)` 的返回值。

输出格式所示（为了清晰起裁剪了长数字）：

```
# RSA 2048 bits xy.example Sat Apr 15 13:53:22 2000 # 用于
签名，不安全加密 #publicKey=saQ0F8tt2ZNT-
Y+PuFun/Modulus: 0cc2a33156fcf440..cf1011abbd21PublicExponent: 0x3
# 此点之后的所有都是私钥 PrivateExponent: 0xb881c59fdf8...
ab05c677d23 Prime1: 0xf49fd1f779..46504c7bf3 Prime2: 0xd5a9108453...
321d43cb2 Exponent1: 0xa315364a4f..536d98adda77 Exponent2:
```

```
# 0x8e70b5ad8d..9142168d7cc7 Coefficient: 0xafb761d001..0c13e98d98
```

第一行（注释行）指示密钥的性质并提供主机名，`ipsec_showhostkey(8)` 在生成某些形式的密钥输出时会使用。

被注释的 `pubkey=` 行包含公钥、公指数和模数，它们以类似于 RFC 2537 的格式合并（唯一的区别是合并后的值带有 Os 前缀，而不是原始的 base-64），适用于 `ipsec.conf` 文件。

`Modulus`（模数）、`PublicExponent`（公指数）和 `PrivateExponent`（私指数）行提供了基本的签名和验证数据。

`Prime1` 行和 `Prime2` 行给出质数本身（即 p 和 q），按从大到小排序。`Exponent1` 和 `Exponent2` 行分别给出 mod p-1 和 q-1 的私指数。`Coefficient`（系数）行给出中国剩余定理系数，即 q mod p 的逆元。这些额外的数字（必须像私指数一样保持保密）是用于快速签名生成的预计算辅助。当使用 NSS 时，这些值在 NSS 安全数据库（软件令牌或硬件令牌）之外是不可用的，而是用 `CKA_ID` 填充。

程序未尝试折行长行。

RSA 算法的美国专利已于 2000 年 9 月 20 日过期。

```
# ipsec rsasigkey —verbose 4096 >mykey.txt
```

生成一个 4096 位的签名密钥并将其放入 `mykey.txt` 文件，同时向标准错误输出运行注释。该文件内容可以逐字地插入 `ipsec.secrets` 文件中的相应条目（参见 `ipsec_secrets(5)`），然后可以提取公钥并编辑到 `ipsec.conf` 中（参见 `ipsec_showhostkey(8)`）。

## FILES

`/dev/random`, `/dev/urandom`

## SEE ALSO

`random(4)`, `rngd(8)`, `ipsec_showhostkey(8)`. Applied Cryptography, 2nd. ed., by Bruce Schneier, Wiley 1996, RFCs 2537, 2313, GNU MP, the GNU multiple precision arithmetic library, edition 2.0.2, by Torbj Granlund

## HISTORY

最初由 Henry Spencer 为 Linux FreeS/WAN 项目 <http://www.freeswan.org[]> 编写。由 Paul Wouters 为 Libreswan 项目进行了更新。

`—round` 和 `—noopt` 选项已废弃，因为它们仅用于旧的非库加密代码。

`—random` 设备仅用于为加密库提供种子，不用于直接通过随机数生成密钥。

## BUGS

`nbits` 有内部限制，目前为 20000。

`rsasigkey` 的运行时间难以预测，因为如果系统的熵池随机性不足，`/dev/random` 的输出可能会任意延迟，而且搜索质数的时间也具有不可预测性。具体而言，嵌入式系统和大多数虚拟机熵较低。在这种情况下，考虑在另一台机器上生成 RSA 密钥，并将 `ipsec.secrets` 和 `ipsec.d/*db` 文件复制到嵌入式平台。注意，NSS 在 DB 文件嵌入了完整路径，因此代理机器上的路径必须与目标机器上的路径相同。

## AUTHOR

Paul Wouters

placeholder to suppress warning

# IPSEC_SECRETS

## NAME

`ipsec_secrets` - 重新读取 `ipsec.secrets` 文件

## SYNOPSIS

`ipsec secrets`

## DESCRIPTION

`secrets` 是 `ipsec auto —reresecrets` 的别名，并重新读取 `ipsec.secrets` 文件中的所有 secrets。

## SEE ALSO

`ipsec.secrets(5)`

## HISTORY

较旧版本的 libreswan（以及 openswan）允许 secrets 文件包含指向加密 RSA 私钥的文件名。这些现在不再被支持，且必须保存在 NSS 数据库中。NSS 数据库本身可以使用密码保护。

## BUGS

无

## AUTHOR

Paul Wouters

placeholder to suppress warning

# SETUP

## NAME

`ipsec_setup` - Libreswan 初始化系统的封装例程

## DESCRIPTION

系统管理员通过 `ipsec setup` 调用 setup，以执行与 Libreswan 相关的初始化系统相关任务，例如对互联网密钥交换（IKE）守护进程 `pluto` 执行启动、停止、状态、重载等操作。它为了兼容 Openswan 和 FreeS/WAN 而提供。

# SUPPORTED INIT SYSTEMS

目前支持经典的 initscripts (sysv) 和 systemd。很快将添加对 upstart 的支持。

## SEE ALSO

`systemd(8)`, `systemd.service(5)`, `ipsec(8)`, `ipsec__realsetup(8)`, `ipsec__plutorun(8)`.

## HISTORY

Michael Richardson 为 Linux FreeS/WAN 项目编写了该页。原始程序由 Henry Spencer 。由 Paul Wouters 更新至 http://www.libreswan.org/m[]。

## AUTHOR

Paul Wouters

placeholder to suppress warning

# IPSEC_SHOWHOSTKEY

## NAME

`ipsec_showhostkey` - 显示主机的认证密钥

## SYNOPSIS

`ipsec showhostkey [--ipseckey] [--left] [--right] [--dump] [--verbose] [--version] [--list] [--gateway gateway] [--precedence precedence] [--dhclient] [--file secretfile] [--keynum count] [--id identity]`

## DESCRIPTION

`Showhostkey` （在标准输出上）输出适用于主机的公钥，格式指定，使用存储在 `/etc/ipsec.secrets` 中的主机信息。通常只有超级用户可以运行此命令，因为只有他可以运行 `ipsec.secrets`。

`--left` 和 `--right` 选项导致输出采用 `ipsec.conf(5)` 格式，分别为 `leftrsasigkey` 和 `rightrasigkey`。如果可用则包含该信息。例如，`--left` 输出（如下）：

```
# RSA 2048 bits xy.com Sat Apr 15:53:20
leftrsasigkey=2000
```

`--ipseckey` 选项导致输出适用于配置 Wavesec 的 `dhclient.conf(5)`。参见 <http://www.wavesec.org/>。

通常情况下，提取默认主机密钥（未指定身份的主机）。`--id` 选项将覆盖此操作，提取指定身份的密钥（如果有）。指定的身份必须与文件中的身份完全匹配；特别是比较是区分大小写的。

可能存在多个相同的身份。所有密钥根据它们在文件中线性顺序（包括所有 include 指令）进行编号。

`--file` 选项覆盖了密钥信息的默认位置，并从指定的 `secretfile` 获取。

# DIAGNOSTICS

关于“找不到 pubkey 行”的投诉表明主机有一个密钥，但它是用旧版本的 FreeS/WAN 生成的，不包含 showhost 需要的信息。

## FILES

```
/etc/ipsec.secrets
```



## SEE ALSO

`ipsec.secrets(5)`, `ipsec.conf(5)`, `ipsec_rsasigkey(8)`

## HISTORY

Henry Spencer 为 Linux FreeS/WAN 项目编写。由 Paul Wouters 为 IPSECKEY 格式进行了更新。

## BUGS

可以说，与其仅仅报告找不到 KEY 行的问题，`showhost` 应该足够智能，能够通过运行带 `—oldkey` 选项的 `rsasigkey` 来处理现有密钥，以生成合适的输出行。

`—id` 选项假设身份出现在与密钥正文 `: RSA {` 同一行。

## AUTHOR

Paul Wouters

placeholder to suppress warning

# IPSEC_SPI

> NAME

`ipsec_spi` - 管理 IPSEC 安全关联

## 概要

注意：在下文中，

`<SA>` 意味着：`—af` (`inet` `inet6`) `—est` `daddr` `—spi` `spi` `—proto` `proto` OR `—said` `said`,
`<life>` 意味着：`—life` (`soft` | `hard`) 分配 | 字节 | `addtime` | `usetime` | 包 | `[value...]` `<SA>` `—src` `src` `—ah` (`hmac-md5-96` | `hmac-sha1-96`) [`—replay_window` `replayw`] [`<life>`] `—autauth` `akey`
`ipsec spi <SA> —src src —esp (3des 3des-md5-96 | 3des-sha1-96) [—replay_window replayw] [<life>] —enckey ekey`
`—authtay akey`
`ipsec spi <SA> —src src —comp deflate`
`ipsec spi <SA> —ip4 —src encap-src —dst encap-dst`
`ipsec spi <SA> —ip6 —src encap-src —dst encap-dst`
`ipsec spi <SA> —del`
`ipsec spi —help`
`ipsec spi —version`
`ipsec spi —clear`

## 描述

`Spi`

创建和删除 IPSec 安全关联（Security Associations）。安全关联（SA）是一种转换，包内容在转发之前会对其进行处理。这种转换可以是 IPv4-in-IPv4 或 IPv6-in-IPv6 封装、IPSec 身份验证头（AH，不带加密的认证）或 IPSec 封装安全载荷（ESP，加密，可能包含认证）。

当数据包从高网络层通过 IPSec 虚拟接口传递时，在扩展路由表 `ipsec_route(8)` 中搜索将产生有效的目的地址、安全参数索引（SPI）和一个 IP 协议数。当 IPSec 数据包从网络到达时，将使用其目的地址、SPI 以及由最外层 IPSec 头部指定的 IP 协议。目的地/SPI/协议的组合用于选择 SA。有关如何组合多个转换的讨论，请参阅 `ipsec_spigrp(8)`。

`af`、`daddr`、`spi` 和 `proto` 指定了要创建或删除的 SA。*af* 是地址族（`inet` 代表 IPv4，`inet6` 代表 IPv6）。*Daddr* 是 IPv4 的点分十进制表示法或 IPv6 的十六进制表示法的目的地址。*SPI* 是一个数字，十六进制前加“0x”，位于 `0x100` 到 `0xffffff` 之间；`0x` 到 `0xff` 的值被保留。*Proto* 是一个 ASCII 字符串，“ah”、“esp”、“comp”或“tun”，指定 IP 协议。该协议必须与所选算法匹配。

或者，*said* 参数也可以指定要创建或删除的 SA。*Said* 结合了上述三个参数，例如：`tun:101@1.2.3.4` 或 `tun:101@1:2::3:4`；其中地址族通过“.”指定 IPv4，通过":"指定 IPv6。地址族指示符替换了十六进制的“0x”。

为了使入站策略检查生效，必须提供源地址 `src`。如果禁用了入站策略检查，则不需要包含源地址。

密钥向量必须以十六进制或 base64 数字的形式输入。它们应该是密码学强随机数。

所有十六进制数字都以十六进制数字字符串（0-9 和 a-f）的形式输入，中间没有空格，前面加“0x”，每个十六进制位表示 4 位。所有 base64 数字都以 base64 数字字符串（0-9, A-Z, a-z, ‘+’ 和 ‘/’）的形式输入，中间没有空格，前面加“0s”，每个字符表示 6 位，并用“=” 进行填充。

删除已分组的 SA 将导致整个链被删除。带有附加参数的形式列出了 `/proc/net/ipsec_spi` 的内容。`/proc/net/ipsec_spi` 的格式在 `ipsec_spi(5)` 中进行了讨论。

*soft* 周期在请求密钥管理守护进程重密钥 SA 时设置一个限制。*hard* 周期设置了 SA 必须过期的限制。

`lifetime allocations`（分配寿命）告诉系统何时因为被重路由过多而导致 SA 过期（目前未使用）。`bytes` 生命周期类型告诉系统在用 SA 处理了一定数量的字节数后使 SA 过期。`addtime` 生命周期类型告诉系统在 SA 安装若干秒后使 SA 过期。`usetime` 生命周期类型告诉系统在 fact SA 处理其第一个数据包若干秒后使 SA 过期。`packets` 生命周期类型告诉系统在用该 SA 处理了一定数量的数据后使 SA 过期。

## 选项

- `-af` 指定地址族（`inet` 代表 IPv4，`inet6` 代表 IPv6）
- `-edst` 指定安全关联的有效目的 `daddr`
- `-spi` 指定安全关联的安全参数索引 `spi`
- `-proto` 指定安全关联的 IP 协议 `proto`
- `-said` 以单体格式指定安全关联
- `-ah` 为 IPSEC 身份验证头添加一个 SA，由以下转换标识符指定（**`hmac-md5-96`** 或 **`hmac-sha1-96`**）（RFC2402, 废弃了 RFC1826）

### hmac-md5-96

遵循 HMAC 和 MD5 标准的转换，使用 128 位密钥产生 96 位认证器（RFC2403）

### hmac-sha1-96

遵循 HMAC 和 SHA1 标准的转换，使用 160 位密钥产生 96 位认证器（RFC2403）

- `-esp` 为 IPSec 封装安全载荷添加一个 SA，由以下转换标识符指定（**`3des 3des-md5-96 | 3des-sha1-96`**）[`—replay_window replayw`] [`<life>`] `—enckey ekey`
`—authtay akey`
- `-comp` 为压缩添加一个 SA（`deflate`）
- `-ip4` 为 IPv4-in-IPv4 添加一个 SA
- `-ip6` 为 IPv6-in-IPv6 添加一个 SA

### 3des

遵循 Triple-DES 标准的转换，使用 64 位密钥 *iv*（RFC2406, 废弃了 RFC1827）

### des-md5-96

遵循 DES 标准的标准，通过 HMAC 和 MD5 产生 96 位认证器，使用 192 位密钥 *ikey*（RFC2451）

### des-sha1-96

遵循 Triple-DES 标准的转换，通过 HMAC 和 SHA1 产生 96 位认证器，使用 192 位密钥 *ikey*（RFC2404）

- `-replay_window` 设置重放窗口大小
- `--life` 设置寿命
- `--del` 删除指定的 SA
- `--clear` 清空 SA 表
- `--help` 显示摘要
- `--version` 显示版本信息

## 示例

为了保持行长度并减少混乱，示例中的某些长密钥已缩写为“...”。在程序实际运行时，密钥应该是对应算法所需的完整长度。

```
ipsec spi —af inet —edst gw2 —spi 0x15 —proto esp —src gw1 —esp 3des-md5-96 —enckey 0x6630...97 —authkey 0x9941...7df
```

从 `gw1` 到 `gw2` 设置 SPI 为 `0x15` 协议为 ESP (50) 的 SA，使用 3DES 加密和 MD5-96 转换，使用 `0x6630...97` 加密密钥和 `0x9941...7df` 认证密钥（参见上方关于缩写的说明）。

```
ipsec spi —af inet —edst 3049::9000:3100 —spi 0x150 —proto ah —src 3049::9:9000:3101 —ah hmac-md5-96 —authkey 0x1234...2eda
```

从 `3049::9:9000:3101` 到 `3049::9:9000:3100` 设置 SPI 为 `0x150` 协议为 AH (50) 的 SA，使用 MD5-96 认证转换，使用 `0x1234...2eda` 认证密钥（参见上方关于缩写的说明）。

```
ipsec spi —said tun.987@192.168.100.100 —del
```

删除目的为 `192.168.100.100`、SPI 为 `0x987` 的 IPv4-in-IPv4 SA。

```
ipsec spi —said tun:500@3049:9::1000:1 —del
```

删除目的为 `3049:9::1000:1`、SPI 为 `0x500` 的 IPv6-in-IPv6 SA。

## 文件

```
/proc/net/ipsec_spi, /usr/local/bin/ipsec
```

# 另请

`ipsec(8)`, `ipsec_tncfg(8)`, `ipsec_eroute(8)`, `ipsec_spigrp(8)`, `ipsec_klipsdebug(8)`, `ipsec_spi(5)`

## 历史

由 Richard Guy Briggs 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org/m/> 编写。

# 缺陷

语法很混乱，转换命名也需要改进。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_SPIGRP

## 名称

`ipsec_spigrp` - 分组/取消分组 IPSEC 安全关联 (Security Associations)

## 摘要

```
ipsec spigrp
ipsec spigrp [—label] af1dst1spi1proto1
[af2dst2spi2proto2 [af3dst3spi3proto3 [af4dst4spi4proto4]]]
ipsec spigrp [—label] —said SA1 [SA2 SA3 [SA4]]
ipsec spigrp —help
ipsec spigrp —version
```

# 废弃

注意，`spi` 仅在经典的 KLIPS 栈上支持。它不支持任何其他栈，并将在未来的版本中完全移除。仍需设计一个替代命令。

## 描述

`Spigrp` 将 IPSEC 安全关联 (SAs) 分组在一起，或取消之前分组的 SAs。IPSEC 扩展路由表中的条目只能（通过目的地址、安全参数索引 (SPI) 和协议标识符）指向一个 SA。如果必须对一组数据包应用多个转换，可以通过设置多个具有相同目的地址但可能不同 SPI 和协议的 SA，并使用 `spigrp` 将它们分组来实现。

要分组的 SAs 指定由目的地址（DNS 名称查找、IPv4 点分四位进制或 IPv6 冒号十六进制）、SPI（以 '0x' 前缀的十六进制数）和协议（'ah'、'esp'、'comp' 或 'tun'），从内层转换到外层转换列出；换句话说，转换按照命令行的顺序应用并按反序移除。生成的 SA 组由其第一个 SA（通过 `af1, dst1, spi1` 和 `proto1`）引用。

`—said` 选项表示 SA ID 将作为每个参数单独指定，格式为 `<proto><af<spi@<dest>`。SA ID 必须全部作为单独参数指定（不使用 `—said` 选项），或者在 `—said` 选项后作为整体参数指定。

SAs 必须已经存在且不能已经是某个组的一部分。

如果仅带一个 SA 规范调用 `spigrp`，它将取消包含所指定 SA 的之前分组的 SA 集合。

`—label` 选项用用户提供的标签标识该命令调用的所有响应，标签作为 `label` 选项的参数提供。这对于在大量调用中调试某一次调用非常有帮助。

不带额外参数的命令形式列出 `/proc/net/ipsec_spigrp` 的内容。`/proc/net/ipsec_spigrp` 的格式在 `ipsec_spigrp(5)` 中讨论。

## 示例

```
ipsec spigrp gw2 0x113 tun gw2 0x115 esp gw2 0x116 ah
```

将 3 个 SA 分组在一起，所有地地址均为 `gw2`，但首先应用 SPI 为 `0x113` 的 IPv4-in-IPv4 隧道，然后应用 SPI 为 `0x115` 的 ESP 头加密数据包，最后应用 SPI 为 `0x116` 的 AH 头验证数据包。

```
ipsec spigrp —said tun.113@gw2 esp.115@gw2 ah.116@gw2
```

将 3 个 SA 分组在一起，所有目的地址均为 `gw2`，但首先应用 SPI 为 `0x113` 的 IPv4-in-IPv4 隧道，然后应用 SPI 为 `0x115` 的 ESP 头加密数据包，最后应用 SPI 为 `0x116` 的 AH 头验证数据包。

```
ipsec spigrp —said tun:233@3049::1 esp:235@3049::1 ah:236@3049:1::1
```

将 3 个 SA 分组在一起，所有目的地址均为 `3049:1::1`，但首先应用 SPI 为 `0x233` 的 IPv6-in-IPv6 隧道，然后应用 SPI 为 `0x235` 的 ESP 头加密数据包，最后应用 SPI 为 `0x236` 的 AH 头验证数据包。

```
ipsec spigrp inet6 3049:1::1 0x233 tun inet6 3049:1::1 0x235 esp inet6 3049:1::1 0x236 ah
```

将 3个 SA 分组在一起，所有目的地址均为 `3049:1::1`，但首先应用 SPI 为 `0x233` 的 IPv6-in-IPv6 隧道，然后应用 SPI 为 `0x235` 的 ESP 头加密数据包，最后应用 SPI 为 `0x236` 的 AH 头验证数据包。

## 文件

```
/proc/net/ipsec_spigrp, /usr/local/bin/ipsec
```

# 另请

`ipsec(8)`, `ipsec_manual(8)`, `ipsec_tncfg(8)`, `ipsec_eroute(8)`, `ipsec_spi(8)`, `ipsec_klipsdebug(8)`, `ipsec_spigrp(5)`

## 历史

由 Richard Guy Briggs 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org/m/> 编写。

# 缺陷

是的，它确实限制为最多四个 SA，尽管很难看出你为什么需要这么多。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_TNCF

## 名称

`ipsec_tncfg` - 操作 KLIPS 虚拟接口

## 摘要

```
ipsec tncfg
ipsec tncfg —create virtual ipsec tncfg —delete virtual ipsec tncfg —attach —virtual —physical ipsec tncfg —version ipsec tncfg —help
```

# KLIPS

注意 `tncfg` 仅在 KLIPS 栈上支持，该栈使用绑定到物理接口的 `ipsecX` 接口

## 描述

`tncfg` 的目的是将 IPsec 虚拟接口（例如 `ipsec0`）绑定/分离到物理接口（例如 `eth0`），数据包在经过 KLIPS 处理后通过这些接口转发。

在使用 MAST 栈时，`tncfg` 用于创建和删除名为 `mast` 的虚拟接口。

不带额外参数的形式列出 `/proc/net/ipsec_tncfg` 的内容。`/proc/net/ipsec_tncfg` 的格式在 `ipsec_tncfg(5)` 中讨论。

`—attach` 形式将虚拟接口绑定到物理接口。

`—detach` 形式将虚拟接口从其绑定的任何物理接口上分离。

`—clear` 形式从所有绑定的物理接口上清除虚拟接口。虚拟接口的名称类似 `ipsec0` 或 `mast0`，而物理接口的名称类似 `eth0` 或 `ppp0`。

## 示例

```
ipsec tncfg—create mast12
```

创建 `mast12` 设备。

```
ipsec tncfg—create ipsec4
```

创建一个 `ipsec4` 设备，但不绑定它。

```
ipsec tncfg—attach —virtual ipsec0 —physical eth0
```

将 `ipsec0` 虚拟设备绑定到 `eth0` 物理设备。

## 文件

```
/proc/net/ipsec_tncfg, /usr/local/bin/ipsec
```

# 另请

`ipsec(8)`, `ipsec_eroute(8)`, `ipsec_spi(8)`, `ipsec_spigrp(8)`, `ipsec_klipsdebug(8)`, `ipsec_tncfg(5)`

## 历史

由 Richard Guy Briggs 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org/m/> 编写。

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_VERIFY

## 名称

`ipsec_verify` - 检查 IPsec 子系统是否安装正确

## 摘要

```
ipsec verify
```



## 描述

`ipsec verify` 检查本地系统中常见的系统故障和配置错误。

## 历史

最初由 Michael Richardson 为 Linux FreeSwan/WAN 项目 <http://www.freeswan.org> 编写。由 Paul Wouters 用 `python` 重写。

## 缺陷

`Verify` 已从 `shell` 转换为 `perl` 再转为 `python`，`MASQUERADING/NAT` 规则测试仍需移植。`ss` 命令在各种不直观且有 Bug 的版本，导致在监听 `UDP` 端口 `500` 和 `4500` 时出现某些误报。请见 https://bugzilla.redhat.com/show_bug.cgi?id=829630

## 作者

Paul Wouters

用于抑制警告的占位符

# IPSEC_PLUTO

## 名称

`pluto` - `ipsec whack` : IPsec IKE 密钥交换进程和控制接口

## 摘要

```
ipsec [--help] [--version] [--leak-detective] [--config filename] [--vendor VID]
--nofork] [--stdderrlog] [--plostderrlogtime] [--logfile filename] [--use-klips] [--use-
mast] [--use-netkey] [--use-nostack] [--uniqueids] [--virtual-private network_list] [---
keep-alive delay_sec] [--force-bysec] [--forsnorced] [--strictcontrolpolicy] [--lrcheckinterval]
--interface ifacamen] [--listen ipaddr] [--ikeport number] [---
ateport dirname] [--ctbase path] [--secretsfile filename] [--adspath pathname] [---
helpers number] [--seedbits number] [--peerplog] [--peergebase dirname
```



```
ipsec whack --whackrecord [filename]
ipsec whack --name connection-name --delete [ctlbase path] --label string
ipsec whack --delestate-state-name [ctlbase path] --label string
ipsec whack --name connection-name [debug-none] [debug-all] [debug-raw] [debug-crypt] [debug-parsing] [debug-emitting] [debug-control] [debug-dns] [debug-controlmore] [debug-lifecycle] [debug-klips] [debug-pfkey] [debug-dpd] [debug-natt] [debug-oppo] [debug-oppoinfo] [debug-whack] [debug-private] [impair-delay-adns-keys-answer] [impair-delay-adns-txt-answer] [impair-bust-mi2] [impair-bust-mr2] [impair-sa-fail] [impair-die-info] [impair-retransmits] [impair-send-bogs-isakmp-flag] [impair-send-ikev2-ke] [impair-send-key-size-check]
ipsec whack --utc [listpubkeys] [listcerts] [listcacerts] [listacerts] [listacerts]
ipsec whack --utc [listgroups] [listctrls] [rereadsecrets] [rereadall] [rereadcerts] [rereadacerts] [rereadacerts] [rereadacerts]
ipsec whack
ipsec whack --listevents
ipsec whack --status [ctlbase path] --label string
ipsec whack --trafficstatus [ctlbase path] --label string
ipsec whack --shutdown [ctlbase path] --label string
```

# 说明

`pluto` 是 IKE（“IPsec 密钥交换”）守护进程。`whack` 是一个辅助程序，允许向正在运行的 `pluto` 发起请求。

`pluto` 用于在具有 IPsec（安全 IP 协议）的系统上自动构建共享“安全关联”（Security Associations）。换句话说，`pluto` 可以消除大量的手动密钥工作。数据包的实际安全传输由系统的其他部分——内核负责。`Pluto` 可以与各种内核实现通信，例如 `KLIPS`、`NETKEY` 以及 `KAME IPsec` 栈。`ipsec_auto(8)` 为 `pluto` 和 `whack` 提供了一个更方便的接口。

## IKE 的工作

安全关联（SA）是两个网络节点之间关于如何处理它们之间流量的约定。这种处理涉及封装、身份验证、加密或压缩。

IKE 可以部署在网络节点上，为该节点协商安全关联。这些 IKE 实现只能与其他 IKE 实现进行协商，因此，在每个作为 IKE 协商安全关联端点的节点上，都必须运行 IKE。其他节点不需要运行 IKE。

一个 IKE 实例（即特定网络节点上的 IKE 实现）使用 UDP IP 数据包与另一个 IKE 实例通信，因此节点之间在每个方向上都必须存在路由。

安全关联的协商需要涉及许多选择，这些选择涉及到安全性、便利性、信任和效率之间的权衡。这些是策略问题，通常由 IKE 索引管理员指定。

IKE 处理两种安全关联。IKE 实例之间协商的第一部分是建立一个 ISAKMP SA。ISAKMP SA 用于保护两个 IKE 之间的通信。随后，IKE 可以建立建立 IPsec SAs——这些 SA 用于在系统之间携带受保护的 IP 流量。

ISAKMP SA 的协商被称为第一阶段。理论上，主模式（Main Mode）和激进模式（Aggressive Mode）是由 IKE 实例完成的。第二阶段是建立 IPsec SA 的协商，包括对 NAT 穿透的支持。

IKE 实例必须能够认证彼此，这是对于可以协商的 ipsec SA。总而言之，IKE 实例是初始化安全关联 的。

`pluto` 启动安全关联 的协商。这些 RSA 签名可以来自 DNS(SEC)、配置文件或 X.509 证书。

`pluto` 使用共享密钥或 RSA 签名来认证与其协商的对方。

对于 IPsec SA 的策略是硬编码在代码中的。在它协商了 SA 之后，它还会调用任何关闭。

## 运行 Pluto

`pluto` 是 IKE 的一种实现。它作为守护进程运行。在运行它之前，必须设置一些内容。

`pluto` 需要工作良好的 IP 栈。它支持多个网络（即需要加密的网络）。它通过查看所有接口来发现使用的接口。如果连接是机会性的，且未知公钥，`pluto` 将尝试获取它。带有 `-a` 标志的 `config(8)` 将显示每个接口名称和状态。

# 设置 KLIPS

`pluto` 支持的最基本的网络拓扑是代表客户端的两个安全网关。RGB 的测试平台是一个很好的示例（见 `klips/doc/rgb_setup.txt`）。

基础目录下的 `INSTALL` 文件解释了如何启动整个 KLIPS 系统。

确保安全网关之间有路由。这通常由默认路由覆盖，但可能需要为特定的 IP 接口发布路由（我们假设为 `eth0`）。连接安全网关到客户端的接口必须是另一个。

需要在每个网关执行 `ipsec tncfg(8)` 命令。所需的命令是：

```
ipsec tncfg --attach virtual ipsec--physical eth0
```

还需要运行设置 `ipsec0` 虚拟接口的命令。它将具有与其连接的物理接口时使用的命令相同的参数。

# 为 pluto 设置 NETKEY

使用 `NETKEY` 不需要特殊要求——它随所有现代 Linux 2.4 和 2.6 版本一起发布，然而，某些供应商或旧发行版使用了损坏的 `NETKEY` 版本或移植版本。如果可能，请使用基于或自 Linux 2.6.11 或更新版本的 `NETKEY` 版本。

编码的密钥文件和 XAUTH 密码。智能卡由 NSS 处理。为了调试，`pluto` 命令有一个参数可以使用不同的文件。该文件在 `ipsec.secrets(5)` 中进行了描述。

## 运行 Pluto

要启动该守护进程，只需输入 `pluto`（以确保其以超级用户身份运行）。默认 IKE 端口号为 500，这是 IANA 为 Ike 守护进程分配的 UDP 端口。`Pluto` 必须由超级用户运行才能使用 UDP 500 端口。如果告诉 `pluto` 启用 NAT 穿透（NAT-Transversal），则 UDP 端口 4500 也会被 Pluto 占用监听。

`Pluto` 在不同的操作系统上支持不同的 IP 栈（IPStacks）。可以使用选项之一进行配置——`--use-network`（默认）、`--use-klips`、`--use-bsdkame`、`--use-win2k` 或 `--use-nstack`。后者仅用于测试——实际的 IPsec 连接不会加载到内核。`--use-auto` 已过。启动时，如果将 `--config/etc/ipsec.conf` 作为参数传递给 `pluto`，`pluto` 可能会读取协议栈以选择要使用的 IPsec 栈。如果同时指定了 `--use-XXX` 和 `--config/etc/ipsec.conf`，则最后一个参数具有优先级。

`Pluto` 支持 RFC 3947 NAT 穿透。NAT 路由器之间的允许范围通过 `--virtual-private` 选项提交。语法请参见 `ipsec.conf(5)`。`--force-alive` 选项强制发送保活包（keep-alive packets），这些数据包用于防止在 IPsec 连接上流量不足时 NAT 路由器关闭其端口。`--keep-alive` 设置保活包的延迟（秒为单位），默认启用此功能。

`Pluto` 支持使用 X.509 证书并在需要时发送它。这可能会让没有实现此功能的 IKE 实现产生困惑，例如旧的 FreeS/WAN 实现。`--nocrsend` 防止 `pluto` 发送这些数据包。启动时，`pluto` 会从目录 `/etc/ipsec.d/cacerts`、`/etc/ipsec.d/acerts`、`/etc/ipsec.d/private` 和 `/etc/ipsec.d/crls` 加载所有与 X.509 相关的文件。可以重新读取证书吊销列表（CRL）以检查 CRL 过期并发布新的获取命令。首次更新 CRL 的尝试将在下次更新前的 2*crcheckinterval 开始。如果没有加载或获取有效的 CRL，Pluto 会记录一个警告。如果给出 `--strictcrpolicy`，则连接将被拒绝，直到加载了有效的 CRL。

`Pluto` 还可以帮助子进程卸载加密操作。此行为可以使用 `--helpers` 进行微调。`Pluto` 将启动 (n-1) 个，其中 n 是 CPU 的数量（包括超线程 CPU）。值 0 强制 `pluto` 在主进程执行操作。值 -1 告诉 `pluto` 执行上述计算。

`Pluto` 使用 NSS 加密库作为随机源。某些政府机构要求 `pluto` 从 `/dev/random` 读取 440 位，并在从 NSS 库提取随机数之前将其找到 NSS RNG 中，尽管 NSS 库本身会对其内部状态建模。由于此过程可能会阻塞长时间，默认不执行这种冗余的密封。`--seedbits` 选项可指定从 `/dev/random` 提取并种子到 NSS RNG 的位数。这也可以通过在 `ipsec.conf` 的“config setup”部分中指定种子来实现。大多数人不应使用此选项。

`pluto` 会创建一个名为 `/var/run/pluto.pid` 的锁。如果无法创建锁，`pluto` 将退出——这防止了多个 `plutos` 竞争。在 `pluto` 将其 PID 写入此文件之前，必须移除任何遗留的锁，以便脚本找到它。如果锁位于 NFS 卷上，它将无法正常工作（反正在多台机器上拥有锁是没有意义的）。

`pluto` 分生（fork）并且父进程退出。这是传统的“守护进程派生”。这会让调试变得尴尬，因此有一个选项可以抑制这种派生。在某些配置下，`pluto` 可能会启动辅助程序来协助 DNS 查询或卸载加密操作。

所有日志（包括诊断信息）都发送到 facility=authpriv 的 `syslog(3)`；它决定了将这些消息放在哪里（可能在 `/var/log/secure` 或 `/var/log/auth.log`）。由于这也会让调试变得尴尬，可以使用 `--stderrlog` 选项将日志重定向到。

或者，可以使用 `--logfile` 将所有日志信息发送到特定文件。

如果给出 `--peerlog` 选项，则 `pluto` 为每个连接打开日志文件。默认情况下，它位于 `/var/log/pluto/peer`，由将所有点 (.) [IPv4] 或冒号 (:) [IPv6] 转换为斜杠 (/) 的子目录。可以通过 `--peerlogbase` 修改基本目录。

一旦 `pluto` 启动，它将等待来自 `whack` 的请求。

## Pluto 的内部状态

了解如何使用 `pluto`，了解它的内部状态会有帮助。此外，需要一些术语来解码某些诊断消息。

`Pluto` 支持组和 X.509 证书。这些位于 `/etc/ipsec.d` 或由 `--ipsecdir` 指定的其他目录。

`Pluto` 可能会产生核心转储（core dump）。它通常进入当前工作目录。你可以为 `pluto` 指定 `--coredir` 选项，或者在 `ipsec.conf` 中指定 `dumpdir=option`。

如果你正在调查 `pluto` 中潜在的内存泄漏，请使用 `--leak-detective` 选项启动 `pluto`。如果没有有效的 CRL 加载，连接将被拒绝，直到加载了有效的 CRL。

当 KLIPS 和 NETKEY 合并为一个栈时，所有这些路由特性预计都会发生变化。

# 使用 whack

`whack` 用于命令运行中的 `pluto`。`whack` 使用 UNIX 域套字与 `pluto` 通信（默认为 `/var/pluto`）。

`whack` 具有复杂的参数语法。该语法允许指定许多不同的功能。帮助形式（help form）显示用法或版本信息。连接形式（connection form）为 `pluto` 提供潜在连接的描述。公钥形式（public key）告知 `pluto` 潜在对端的 RSA 公钥。删除形式（delete form）删除连接描述及其对应的所有 SA。列表形式（list form）告诉 `pluto` 在公共接口上启动或停止监听来自对端的 I 请求。路由形式（route form）告诉 `pluto` 为连接设置路由；取消路由形式（unroute form）撤销此操作。发起形式（initiate form）告诉 `pluto` 为连接协商 SA，包括正在协商中的 SA。状态形式（status form）显示 `pluto` 的内部状态。调试形式（debug form）告诉 `pluto` “动态”更改调试输出的选择。关闭形式（shutdown form）告诉 `pluto` 关闭，并删除所有 SA。

`crash` 选项请求 `pluto` 考虑某个特定的目标 IP 崩溃，并尝试使用该 IP 地址作为网关重启所有连接。通常情况下，你应该使用死亡对端检测（Dead Peer Detection）来自动检测这种情况，但这并不总是可能的。

大多数选项特定于某一种形式，将在该形式中进行描述。有三个选项适用于所有形式。

- `-ctlbase path`
`path.ctl` 用作与 `pluto` 通信的 UNIX 域套字。此选项有助于调试。
- `-label string`
将字符串添加到由 `whack` 生成的所有错误消息中。

`whack` 的帮助形式是自言自义的。

- `-help`
显示用法信息。
- `-version`
显示 `whack` 的版本。

连接形式描述了到 `pluto` 的潜在连接。`pluto` 需要知道哪些连接可以且应该被协商。当 `pluto` 是发起者时，它需要知道要提议什么。当 `pluto` 是响应者时，它需要足够的信息来决定是否愿意建立所提议的连接。

潜在连接的描述可以指定大量的细节。每个连接都有唯一的名称。此名称将出现在 updown shell 命令中，因此不应包含会导致命令格式不正确的标点符号。

- `-connection-name`
设置连接的名称

连接的拓扑是对称的，因此为了节省空间，这里显示半幅：
`client_subnet--->hikeport<--nexthop`

标志（flags）中使用了一种巧妙的技巧。标志名称同时用于两端。—to 之前的标志描述左侧，之后的标志描述右侧。当 `pluto` 尝试使用该连接时，它根据其接口的 IP 号来决定自己是连接的左侧还是右侧。

- `-id`
端的身份。目前，这可以是一个 IP 地址（指定为点分四位数或完全限定域名，后者将立即解析），或本身就是一个完全限定域名（以“@”为前缀表示不应被解析），或者以 `user@FQDN` 形式，以及一个 X.509 DN，或者作为值 `%myid`。`Pluto` 仅进行身份验证，不将其用于地址寻址，例如，IP 地址不需要是数据包发往的那个地址。如果缺少该选项，身份默认为由 —host 指定的 IP 地址。`%myid` 允许单独指定身份（通过 `pluto` 或 `whack` 选项 —myid —myid，或者通过 `ipsec.conf(5)` 配置参数 `myid`）。否则，`pluto` 尝试猜测 `%myid` 代表什么：如果该 IP 的反向解析中由合适的 TXT 记录支持，则是 `%defaultroute` 的 IP；如果在系统的正向解析中由合适的 TXT 记录支持，则是系统的主机名。

- `-ip-address`, `—host %any`, `—host opportunistic`
端的 IP 地址（指定为 `%any`，—host 机会性）。当 `pluto` 响应时，需要知道的 IP 地址。如果是机会性发起，应指定为 `%any`（旧式表示 0.0.0.0 是接受的）。

- `-cert filename`
`pluto` 使用的证书文件名。该文件名必须是 PKCS12 证书。参见 `ipsec.conf(5)` 如何从 PKCS12 文件提取。

# ca distinguished name
用于此连接的 CA 证书的 X.509 证书机构名称（DN）。

# access groups
访问控制组

- `-sendcert yes|always|ifaked|never`
是否发送证书，以及允许连接的身份凭据。默认是 yes（在我们是响应者时使用），在我们是发起者时使用 forced 或 always（no 和 never 似乎并未实现）。

- `-sendca none|issuer|all`
发送多少我们的 X.509 证书链。指定 `issuer` 只发送发行者 CA，而 `all` 将发送整个 CA 链。`none` 将不发送任何 CA 证书。默认是 `none`（当前的）。

- `-certype number`
X.509 证书类型数字

- `-ikeport port-number`
IKE 监听的 UDP 端口。默认是 500。

- `-nexthop ip-address`
路由数据包到端。当 `pluto` 安装 SA 时，它使用 `nexthop` 作为网关。默认是对端的 IP 地址（可以显式写为 `%direct`；接受的）。

- `-client subnet`
IPsec 流量的目标子网。如果未指定，主机将是客户端。子网可以使用 `ipsecsubnet(3)` 支持的任何格式指定。通用形式为地址/掩码。地址可以是域名或四个用点分隔的十进制数字（字节）。掩码最方便的形式是十进制整数，指定掩码的前导位数。例如，`10.0.0.0/8` 指定了 A 类网络 '10'。

- `-clientwithin`
此选项已过时并将删除。不要再使用此选项。

- `-clientprotoport protocol/port`
指定在此连接使用的端口选择器（过滤器）。通用形式为协议/端口。这通常用于通过指定 UDP（协议 17）和端口 1701 来限制连接仅 L2TP 流量。`17%%any` 符号允许所有 UDP 流量，对于 Service Pack 2 之前的 Windows XP 机器的 L2TP 连接是必要的。

- `-srcip`
此主机向远程 IPsec 网关传输数据包时使用的 IP 地址。此选项用于让网关本身使用其内部 IP，它是客户端子网的一部分。否则，它将使用最近的 IP 地址，即其公网 IP，该 IP 不属于 IPsec 隧道子网，因此不会被加密。

端是 xauth 服务器。它将查找 xauth 用户名和密码，并在允许建立连接之前进行验证。

客户端端是 xauth 客户端。要使用 `--initiate` 建立此连接，还需要客户端指定 `--xauthuser` 用户名和 `--xauthpass` 密码。

- `-xauthuser`
xauth 认证的用户名。此选项通常由 `ipsec_auto(8)` 在使用 `ipsec auto --up conn` 启动 xauth 连接时传递。

- `-xauthpass`
xauth 认证的密码。此选项通常由

## ipsec_auto(8) 当使用 ipsec auto --up conn 启动 xauth 连接时

### —modecfgserver
此端为 Mode Config 服务器

### —modecfgclient
此端为 Mode Config 客户端

### —modecfgdns1
传递给 ModeConfig 客户端的 DNS 服务器 IP 地址。

### —modecfgdns2
传递给 ModeConfig 客户端第二个 DNS 服务器 IP 地址。

### —dnskeydemands
指定当需要 RSA 公钥来验证此主机且该公钥尚未知时，从 DNS 获取。

### —updown updown
指定一个每当 `pluto` 建立或关闭连接时都会运行的外部 shell 命令。该脚本用于构建 shell 命令，因此可能包含位置参数，但不应包含会导致最终生成的命令格式错误的标点符号。默认值为 `ipsec ipsec_updown`。`Pluto` 会向脚本传递有关相关连接的十余个环境变量。

### —to
分离连接左端和右端的规格。`Pluto` 尝试根据此选项两端提供的信息判断其是左端还是右端。潜在的连接描述还规定了重密钥和安全特性。

### —psk
为 IKE 对端提议并允许使用预共享密钥认证。此认证要求双方使用相同的密钥。可以与 —rsasig 结合使用；至少必须指定其中之一。

### —rsasig
为 IKE 节点端提议并允许使用 RSA 签名认证。此认证要求双方都拥有自己的私钥，并知道对方的公钥。可以与 —psk 结合使用；至少必须指定其中之一。

### —encrypt
所有提议或接受的 IPsec SA 将包含非空 ESP。转换的实际选择已内置在 **pluto** 中。

### —authenticate
所有提议的 IPsec SA 将包含 AH。所有接受的 IPsec SA 将包含 AH 或带有认证的 ESP。转换的实际选择已内置在 **pluto** 中。注意，这与 IKE 认证无关。

### —compress
所有提议的 IPsec SA 将包含 IPCOMP（压缩）。如果 KLIPS 未配置 IPCOMP 支持，则此项将被忽略。

### —tunnel
IPsec SA 应使用隧道模式。如果 SA 是针对客户端的，则是隐式的。必须与 —authenticate 或 —encrypt 一起使用。

### —ipv4
主机地址将被解释为 IPv4 地址。这是默认值。注意，对于连接，所有主机地址必须属于同一地址族（IPv4 和 IPv6 使用不同的地址族）。

### —ipv6
主机地址（包括下一跳）将被解释为 IPv6 地址。注意，对于连接，所有主机地址必须属于同一地址族（IPv4 和 IPv6 使用不同的地址族）。

### —tunnelipv4
客户端地址将被解释为 IPv4 地址。默认值与主机将使用的地址匹配。这并不意味着 —tunnel，因此在未实际指定隧道时可以安全使用该标记。注意，对于连接，所有隧道地址必须属于同一地址族。

### —tunnelipv6
客户端地址将被解释为 IPv6 地址。默认与主机将使用的地址匹配。这并不意味着 —tunnel，因此在未实际指定隧道时可以安全使用该标记。注意，对于连接，所有隧道地址必须属于该地址族。

### —pfs
应具有完全前向安全性 - 为每个 IPSec SA 生成新的密钥材料，而不是从 ISAKMP SA 的材料中派生。由于使用的组无法协商（这是标准的一个可疑特性），`pluto` 将提议在阶段 1 中使用的相同组。我们没有实现更强形式的 PFS，因为那将在协商完 IPSEC SA 后删除 ISAKMP SA。

### —pfsgroup modp-group

### —disablearrivalcheck
如果连接是隧道，允许通过隧道到达的数据包具有任何源和目的地址。

### —esp esp-algos
用于连接（阶段 2，即 IPSec SA）的 ESP 加密/认证算法。选项必须适用于 `ipsec_(8)`。算法格式详见 `ipsec.conf(5)`。

### —aggrmode
此隧道使用激进模式（aggressive mode）ISAKMP 协商。默认模式为主模式。激进模式比主模式不安全，因为它向窃听者暴露了身份，但支持使用 PSK 密钥的移动用户，或与其它强制要求使用激进模式的缺陷实现进行互操作。

### —modecfgpull
从对端拉取 Mode Config 网络信息。

### —dpddelay seconds
设置为此连接发送的死亡对端检测（RFC 3706）存跳（R_U_THERE, R_U_THERE_ACK）之间的延迟（秒）（默认 30 秒）。

### —timeout seconds
设置我们在未听到来自对端的 R_U_THERE 轮询或 R_U_THERE_ACK 回复时的空闲时间（秒）。在此期间若无响应且无流量，我们将声明 SPI 失效并移除 SA（默认 120 秒）。

### —dpdaction action
当启用 DPD 且对端被声明为失效时，应采取什么操作。`hold`（默认）意味着路由将进入 `%hold` 状态，而 `clear` 表示同时清除路由和 SA。在 Road Warrior 配置的服务器上，`clear` 非常有用。`restart` 操作在 Road Warrior 配置的服务器上非常有用。`restart` 操作用于重启连接。

在 SA 过期前多久，`pluto` 应该尝试协商一个新的 SA。这只有在 `pluto` 是发起者（Initiator）时才会发生。默认值为 540（九分钟）。

- `-rekeyfuzz 百分比`
要加到 `rekeymargin` 的随机组件的最大尺寸，以 `rekeymargin` 的百分比表示。`pluto` 将在该范围内选择一个分布均匀的延迟。默认情况下，该百分比为 100。如果需要更高的确定性，请指定 0。该百分比远大于 100 可能是合适的。

- `-keyingintries 计数`
`pluto` 应该尝试协商 SA 的次数，无论是第一次协商还是重新密钥。值 0 被解释为一个非常大的数字：永不放弃。默认值是 3。

- `-dontree`
一个误导性的名称。仅当我们是发起者（Initiator）且连接上最近有流量时，才对连接重新密钥。这适用于 Phase 1 和 Phase 2。这是目前连接终止的唯一自动方式。它对于路边游者（Road Warrior）或机会性连接（Opportunistic connections）可能有用。由于 SA 寿命协商是“接受或拒绝”的，响应者（Responder）会使用协商寿命或配置寿命中较短的一个。这只有在寿命短于协商值时才有效，响应者将及时重新密钥以确保一切正常工作。这与 `dontree` 会产生不利交互。在这种情况下，响应者将重新密钥以纠正 IPS SA 寿命的不足；对于 ISAKMP SA，响应者将接受协商的寿命。

- `-delete`
在连接形式（connection form）中使用时，它会在添加此连接之前删除任何同名的先前连接。与普通删除不同，如果没有先前的连接要删除，则不会产生诊断信息。该连接已有的任何路由都将被撤销。

- `-delete, 连接名称`
`delete` 表单删除命名的连接描述以及所有使用此连接建立的 SA 或发起的协商。该连接已有的任何路由都将被撤销。

- `-delete 状态编号`
`delete` 表单删除指定序列号的状态对象。这对于选择性地删除连接实例很有用。

`whack` 命令的路由形式告诉 `pluto` 为连接设置路由。虽然是传统的路由，但它使用 ipsec 设备作为虚拟接口。一旦设置好路由，数据包将不会“明文”发送到连接中指定的对端客户端。将安装一个 TRAP 分流路由；如果捕获到输出流量，`Pluto` 将发起连接。并不总是需要显式的 `whack` 路由：如果在安装 IPSec SA 时尚未执行操作，则将自动尝试设置一个。

- `--route, --name 连接名称`
当尝试为连接路由时，不能已经存在一个具有相同子网但接口或目的地不同的连接的路由，如果存在，则该路由不能被 IPSec SA 使用。否则尝试将失败。

- `--unroute, --name 连接名称`
`whack` 命令的 `unroute` 形式告诉 `pluto` 撤销路由。如果一个 IPSec SA 正在使用该连接，`pluto` 将拒绝。如果另一个连接共享相同的路由，则将将其保留。如果没有路由，数据包将在不进行加密或身份验证的情况下发送。

发起形式（initiate form）告诉 `pluto` 针对命名的连接与另一个 `pluto`（或其他 IKE 守护进程）发起协商。发起需要 `--route` 提供的路由；如果在安装 IPSec SA 时没有路由，`pluto` 将尝试设置一个。

- `--initiate, --name 连接名称, --asynchronous`
`whack` 命令的发起形式将通过 UNIX 域套字回传 `pluto` 状态信息（除非指定了 `--asynchronous`）。状态信息旨在像来自 FTP 的位。目前 `whack` 将其拷贝到 `stderr`。当请求完成（SA 已建立或 `pluto` 放弃）时，`pluto` 会关闭通道，导致 `whack` 终止。

机会性发起形式用于调试。

- `--tunnelipv4, --tunnelipv6, --opphere IP地址, --optthere IP地址`
这将导致 `pluto` 在之前尝试过的情况下，尝试从这里到那里机会性发起连接。`whack` 日志将显示此尝试的进度。

## 关闭连接

- `--terminate, --name 连接名称`
终止形式告诉 `pluto` 删除任何使用指定连接的 SA 并停止任何正在进行的协商。它不会阻止新协商的开始（`delete` 表单具有此效果）。

- `--crash IP地址`
如果远程对端崩溃，因此没有通知我们，我们将继续发送加密流量，并拒绝来自远程对端的所有明文（非 IKE）流量。`--crash` 也会关闭我们端到指定 IP 地址的所有已知连接。

- `--whackrecordfilename, --whackstoprecord`
这会导致 `pluto` 打开指定的文件进行写入，并记录从 `whack` 或 `addconn` 接收的每条消息。一直持续到使用 `whackstoprecord`。此选项不能与其他命令组合。启动/停止命令本身不会被记录。这些文件通常用于为单元测试创建输入文件，特别是对于策略可能重叠的复杂设置。

文件格式由由 `#pluto-whack` 开头的行、文件开始日期、主机名以及换行符组成。随后是二进制记录，由一个 32 位记录长度（字节，包括长度记录本身）、一个 64 位的时间戳以及收到的 `whack` 消息字面内容组成。所有整数均为主机格式。为了无歧地确定主机字节，第一条记录是一个空记录，仅包含当前的 `WHACK_MAGIC` 值。此记录为 16 字节。

`IP地址`

如果远程对端崩溃，因此没有通知我们，我们将继续发送加密流量，并拒绝来自对端的所有明文（非 IKE）流量。`--crash` 也会关闭我们端到指定 IP 地址的所有已知连接。

公密钥通知 `pluto` 用于对端的密钥。私密钥必须保密，位于 `ipsec.secrets` 中。

- `-keyid 身份`
指定应使用公密钥的身份。其形式与连接相同。如果在安装 IPSec SA 时没有指定公密钥，`pluto` 将尝试通过域名查找（如果是 FQDN）或反向查找（如果是 IP 地址）。

- `-addkey`
将新密钥添加到集合中；否则新密钥将替换旧密钥。

公密钥的值。它是 RFC 2537 中描述的 RSA/MD5 密钥。从 0 开始。

`list` 告诉 `pluto` 开始监听 IKE 请求。每当使用 `list` 时，`pluto` 会注意到新连接的添加和旧连接的删除。这也是触发 `pluto` 读取 `ipsec.secrets` 文件的开关。因此 `listen` 可以使用多次。

# listen

# unlisten
停止在公共接口上监听 IKE 流量。

`status` 将显示 `pluto` 的内部状态：关于每个连接、每个状态对象以及 `pluto` 正在但没有关联连接的分流的信息。

# status

`trafficstatus` 将显示 xauth 用户名、添加时间以及 IPSec SA 的进出总字节。

# trafficstatus

`shutdown` 是关闭 `pluto` 的正确方法。它将终止此机器上 `pluto` 协商的所有 SA。它不会通知其对端，因此它们机器上的 SA 将保留。

# shutdown

## 示例

通常会在系统初始化脚本中启动 `pluto`。它需要超级用户运行。通常不需要参数。手动运行时，超级用户只需输入

```
pluto
```



`ipsec pluto`

```
该命令将立即返回，但会留下一个 pluto 进程等待来自 `whack` 或对端的请求。
```

使用 `whack` 可以描述几个潜在的连接：

```
ipsec connection --name silly --host 127.0.0.1 --to --host 127.0.0.2 --ikelifetime 900 --ipsecftime 800 --keytries 3
```

由于此连接描述没有指定加密、身份验证或隧道，它只能用于建立 ISAKMP SA。

```
ipsec connection --name conn_name --host 10.0.0.1 --client 10.0.0.1/24 --to --host 10.0.0.2 --client 10.0.2.0/24 --encrypt
```

这是必须在双方都执行的操作。如果另一端是 pluto，可以在它上使用相同的 `whack` 命令（该命令语法的设计不区分哪一边是我们的）。

现在连接已经指定，pluto 已经准备好通过公共接口处理请求和响应。我们必须告诉它发现这些接口并开始接收来自对端的消息。

## `ipsec whack --listen`

如果我们不立即希望在客户端之间建立安全连接，那么我们希望阻止不安全的流量。路由表要求 **`pluto`** 将从我们的客户端发送到对端客户端的封包路由到 `ipsec0` 设备；如果没有 SA（安全关联），这些包将会被丢弃。

`ipsec whack --route conn_name`

最后，我们准备好让 **`pluto`** 启动 IPsec SA 的协商（隐式地，作为 ISAKMP SA 启动）：

`ipsec whack --initiate --name conn_name`

标准输出将显示一些有趣事件的简短日志（其他日志将发送到 syslog）。**`whack`** 也可以用于安全地终止 **`pluto`**，拆除它已协商的所有 SA。

`ipsec whack --shutdown`

任何 IPSEC 删除的通知（但不包括 ISAKMP SA 删除的通知）都会发送给对端。遗憾的是，这种通知不可靠的。此外，**`pluto`** 本身会忽略这些通知。

## XAUTH

如果 **`pluto`** 需要 XAUTH 规范定义的额外身份验证，它可能会要求 **`whack`** 提示操作员输入用户名或密码。通常，这些是通过交互式输入的。封装 **`whack`** 的 GUI 可能会查找 041（用户名）或 040（密码）提示，并将它们显示给用户。

为了测试目的，可以在执行 **`initiate`** 之前提供 `--xauthuser user --xauthpass pass` 选项，以便对用户名和密码提示提供响应。

## updown 命令

每当 **`pluto`** 建立或断开连接时，它都会调用 `updown` 命令。该命令通过 `--updown` 选项指定。这允许对路由和防火墙操作进行自定义控制。

`updown` 会因五种不同的操作被调用。这些操作中的每一种都可以针对我们的客户端子网，也可以针对我们的主机本身。

### prepare-host or prepare-client

在没有其他具有相同客户端的连接建立的情况下，在建立新连接之前执行。通常，这用于删除可能在运行 **`pluto`** 之前设置的、或者由某些 **`pluto`** 未知的代理设置的路由。

### route-host or route-client

在为新的对端客户端子网建立连接时运行（即使运行了 prepare-host 或 prepare-client）。该命令应该安装一条合适的路由。路由决策仅基于目标（对端）子网地址，而路由也会根据源地址进行区分。

### unroute-host or unroute-client

在断开特定对端客户端子网的最后一个连接时运行。它应该撤销 `route-host` 或 `route-client` 执行的操作。

### up-host or up-client

在为一对还没有隧道路由的客户端子网建立隧道路由时运行。该命令应相应安装防火墙规则。通常，允许 IKE 消息（UDP 端口 500）在主机之间传输是一个好主意。

### down-host or down-client

在断开一对客户端子网的路由时运行。该命令应相应删除防火墙规则。注意，这些客户端子网可能仍然存在一些入站的 IPsec SA。

脚本将接收大量的环境变量，以指定需要执行的操作。

## `PLUTO_VERSION`

表示正在使用的此接口的版本。本文描述的是版本 1.1。它与版本 1.0 向上兼容。

## `PLUTO_VERB`

指定要执行的操作名称（prepare-host, prepare-client, up-host, up-client, down-host, 或 down-client）。如果安全网关到安全网关通信的地址族是 IPv6，则动词后加上 -v6 后缀。

## `PLUTO_CONNECTION`

我们正在进行路由的连接名称。

## `PLUTO_NEXT_HOP`

发往对端的包必须发送的下一跳。

## `PLUTO_INTERFACE`

将使用的 ipsec 接口名称。

## `PLUTO_ME`

我们主机的 IP 地址。

## `PLUTO_MY_CLIENT`

我们客户端子网的 IP 地址/计数。如果客户端只是主机，这将是主机自身的 IP 地址 / 最大值（IPv4 为 32，IPv6 为 128）。

## `PLUTO_MY_CLIENT_NET`

我们客户端网的 IP 地址。如果客户端只是主机，这将是主机的 IP 地址。

## `PLUTO_MY_CLIENT_MASK`

我们客户端网的掩码。如果客户端只是主机，这将是 255.255.255.255。

## `PLUTO_PEER`

对端的 IP 地址。

## `PLUTO_PEER_CLIENT`

对端客户端子网的 IP 地址/计数。如果客户端只是对端，这将是对端自身的 IP 地址 / 最大值（IPv4 为 32，IPv6 为 128）。

## `PLUTO_PEER_CLIENT_NET`

对端客户端网的 IP 地址。如果客户端只是对端，这将是对端的 IP 地址。

## `PLUTO_PEER_CLIENT_MASK`

对端客户端网的掩码。如果客户端只是对端，这将是 255.255.255.255。

## `PLUTO_MY_PROTOCOL`

列出在此 IPsec SA 上允许的协议。

## `PLUTO_PEER_PROTOCOL`

列出对端在此 IPsec SA 上允许的协议。

## `PLUTO_MY_PORT`

列出在此 IPsec SA 上允许的端口。

## `PLUTO_PEER_PORT`

列出对端在此 IPsec SA 上允许的端口。

## `PLUTO_MY_ID`

列出我们的 ID。

## `PLUTO_PEER_ID`

列出对端的 ID。

## `PLUTO_PEER_CA`

列出对端的 CA。脚本发送到 stderr 的所有输出都会记录。只有在执行成功时，脚本才会返回状态码 0。pluto 在等待脚本完成期间不会进行任何处理。其中任何活动都可以由后台子进程执行。

## 重密钥

一旦协商了一组新的 SA，pluto 将不再在旧 SA 上发送流量。在旧 SA 过期之前，流量仍会被接受。当由 pluto 发起的 SA 剩余寿命很短时，pluto 将启动新 SA 的创建。这适用于 ISAKMP 和 IPsec SA。当剩余寿命小于 `rekeymargin` 加上一个随机比例（0 到 `rekeyfuzz` 之间）时，将启动重密钥。同样，当对端发起的 SA 剩余寿命很短时，pluto 将尝试启动替换的创建。为了优先考虑启动者，只有当剩余寿命小于 `rekeymargin` 的一半时才会启动重密钥。如果重密钥是由响应者执行，角色将相反：旧 SA 的响应者将成为替换的启动者。原启动者也可能启动重密钥，因此可能会创建冗余的 SA。原启动者的风险之一是，它的提议可能无法被对端接受（这些提议未在成功的协商中使用）。为了减少这种情况概率并防止安全性降低，策略设置将从旧 SA 获取（即使是由原启动者发起的）。这些设置可能比连接的设置更严格。pluto 不会在 SA 不是其潜在连接的最最新类型（IPsec 或 ISAKMP）时进行重密钥。这避免了创建冗余的 SA。

重密钥时间中的随机组件（`rekeyfuzz`）旨在使某些病态重密钥模式不稳定。如果双方决定在同一时间重密钥，产生的 SA 数量翻倍。如果没有随机性，这可能会变成一种稳定的模式。

另一个重要情况是安全网关与许多安全网关拥有 SA。这些连接可能在同一时间重密钥。这将导致资源（网络带宽、CPU 时间、随机数熵）出现峰值需求。`rekeyfuzz` 可用于错开重密钥时间。

## 响应时选择连接：路游战士支持

当 `pluto` 接收到初始的主模式消息时，它需要决定哪个连接

此消息是用于的。它仅针对消息的源 IP 和目的 IP 地址。可能会多个具有合适 IP 地址的连接，在这种情况下，将随机选择其中一个。（消息中包含的 ISAKMP SA 提议可以被考虑，但此处未考虑。）

ISAKMP SA 在双方进一步识别身份信息之前协商，因此在连接描述中指定的所有 ISAKMP 特性对于每个具有相同主机 IP 地址的连接都应该是相同的。目前，唯一可能不同的特性是身份验证。

到目前为止，所有的配置都假设所有方都通过时间获知 IP 地址。当其中一方是移动的（或由于其他原因被分配了动态 IP 地址）时，这种方法将失效。我们将这种情况称为“游路战士”（Road Warrior）。这相当复杂，并且具有一些重要的局限性，这些特性都是 IKE 协议的。

唯一的发起者可能是：发起者的 IP 地址可能是响应者未知的。当响应者不识别主模式（Main Mode）数据包上的 IP 地址时，它会查找一个与自身的连接，并将另一端视为 `%any`。如果找不到，它将拒绝协商。如果找到了，它会创建一个临时连接，该连接与原连接重复，只是将 `%any` 替换为数据包中的源 IP 地址；如果对端没有指定身份，将使用新的 IP 地址。

当 `pluto` 使用这些临时连接之一，并且需要在 `ipsec.secrets` 中查找预共享密钥或 RSA 私钥时，如果没有为对方身份指定连接，则使用 `%any` 作为其身份。由于真实的 IP 地址对配置来说显然是未知的，因此要求在这些表中使用它是不合理的。

在使用这些连接描述之一进行阶段 1（主模式）协商的中途，`pluto` 将接收到一个身份有效负载（Identity Payload）。此时，`pluto` 会检查是否有更合适的连接，即一个对方身份与负载匹配的连接，该连接将使用与目前用于身份验证的相同的密钥。如果它找到了，它将切换到使用这个更好的连接（或者从此派生的临时连接，如果对方 IP 地址具有 `%any`）。结果可能是发现没有连接可以匹配新发现的身份，包括当前连接；在这种情况下，`pluto` 将终止协商。

遗憾的是，如果使用预共享密钥身份验证，身份有效负载将使用该密钥加密，响应者必须在不知道此负载的情况下选择该密钥。这限制了所有连接到它的游路战士最多只能有一个预共享密钥。RSA 签名身份验证不需要响应者在发起者负载解码后就知道如何选择发起者的密钥（这需要使用响应者的私钥进行解码，因此必须预先选择）。

当 `pluto` 通过这些临时连接描述之一响应快速模式（Quick Mode）协商时，它可能会发现发起者指定的子网与临时连接描述中的子网不匹配。如果是这样，它将查找一个具有匹配子网、其自身的主机地址、地址为 `%any` 的对方地址以及匹配身份的连接。如果找到了，则将从该连接派生出一个新的临时连接，并用于 IPSec SA 的快速模式协商。如果找不到，`plato` 将终止协商。

请确保为响应者指定一个用于向发起者发送消息的适当的 `nexthop`（下一跳）：`pluto` 没有办法猜测它（如果不需要转发，请使用显式的 `%direct` 作为下一跳，并将填充发起者的 IP 地址；过时的 0.0.0.0 仍然被接受）。

`pluto` 对当前的（动态的）IP 地址没有特殊规定，在定义连接时必须使用下一跳。每当发起者的 IP 地址更改时，这些必须正确配置。`pluto` 没有自动执行此操作的机制。

尽管我们称之为“战士支持”（Warrior Support），但它也可以用于支持具有匿名发起者的加密连接。响应者的组织可以宣布与未知发起者使用的预共享密钥，并允许任何人连接。当然，发起者的身份将不会通过身份验证。

如果支持任何“战士”连接，在确定密钥未共享或签名无效之前，`pluto` 无法拒绝由未知主机发起的交换。这必须等待发起者的第三条主模式消息。如果不支持“游路”连接，来自未知源的第一条消息将被拒绝。这对于配置调试的易用性和拒绝服务攻击有影响。

尽管游路战士连接必须由移动端发起，但另一端可以对其创建的临时连接重新密钥。如果游路战士希望能够断开连接，在非移动端的连接上将 `--keytries` 设置为 1 可能是明智的，以防止它尝试重新密钥连接。遗憾的是，没有自动取消连接的机制。

# 调试

`pluto` 接受几个可选参数，主要用于调试。除了 `interface` 之外，每个参数最多出现一次。

- `-interface internacename`
- 指定命名的公共网络接口应为 ipsecN。如果指定的接口名称未出现，则考虑所有接口。要指定多个接口，请对每个接口使用该选项。此选项的一个用途是指定当两个或多个接口共享相同 IP 地址时应使用哪个接口。

- `-ikeport port-number`
- 更改 pl 将使用的 UDP 端口（默认由 IANA 指定：500）

- `-ctlbase path`
控制文件的基名。`path.ctl` 是 `whack` 与 pluto 通信的套接字。`path.id` 是防止多个 pluto 实例的锁文件。默认是 `/var/run/pluto/pluto`。

# `-secretsfile`
指定身份验证密钥文件（默认：`/etc/ipsec.secrets`）。此名称受类似于 `sh(1)` 中“通配符匹配”的影响，因此每个文件都会被处理。

- `-adns path`
指定查找 pluto 的路径。默认情况下，pluto 在 IPSEC_DIR（如果定义了）或。

- `-nofork`
禁用守护进程（默认是 fork）。此外，在创建锁文件和套接字后，向标准输出打印“Pluto initialized”。

- `-uniqueids`
如果选择了此选项，每当建立新的 ISAKMP SA 时，相同 IP 地址的连接将被注销（导致 SA 被删除）。

- `-force-busy`
如果选择了此选项，pluto 将强制进入“忙碌”状态。这种状态发生在拒绝服务攻击时，强制 pluto 在接受 IKE 数据包之前使用 Cookie。Cookie 在 ike1 激进模式和 ikev2 中发送并需要。此选项主要用于测试，谨慎的管理员可以选择。

- `-stdderlog`
日志输出到标准输出

```
pluto --secrets ipsec.secrets --ctlbase pluto --ikeep 500 --nofork--use-
```

可以在不使用超级用户账户测试 pluto。

`pluto` 会产生大量的调试信息。为了做到这一点，必须带有 DEBUG 编译。多个调试类，所有的调试输出行都以 `|` 开头，以便与错误消息区分来。

当调用 `pluto` 时，可以给出参数来指定输出哪些类。

当前选项有：

`- `-debug-none`

禁用所有调试

- `-debug-all`

启用所有调试

- `-debug-raw`

显示消息的原始字节

- `-debug-crypt`

显示消息的加密和解密

- `-debug-parsing`

显示输入消息的结构

- `-debug-emitting`

显示输出消息的结构

- `-debug-control`

显示 **`pluto`** 的决策

- `-debug-controlmore`

显示更详细的 **`pluto`** 决策

- `-debug-lifecycle`

[此选项为临时]记录 SA 生命周期的细节

- `-debug-klips`

显示 pluto 与 **`KLIPS`** 的交互

- `-debug-pfkey`

显示 pluto 与 **`PFKEY`** 接口的通信

- `-debug-dns`

显示 pluto 与 **`DNS`** 中 KEY 和 TXT 记录的交互

- `-debug-dpd`

显示 pluto 的**死连接检测**（Dead Peer Detection）处理

- `-debug-natt`

显示 pluto 的**NAT穿透**（NATversal）处理

- `-debug-oppo`

显示为什么 **`pluto`** 没有找到合适的 DNS TXT 记录来授权机会性发起

## debug-oppoint

当由于内核发起连接时，记录日志。这通常很有用，但在繁忙的系统中可能会产生大量的调试输出。

## debug-watch

如果设置了此项，会导致 Pluto 不会释放句柄，直到 SA 完全建立。这在测试用例中常见。

## debug-private

使用私钥进行调试输出。

`debug` 命令的格式会更改 Pluto 的选择。如果指定了名称，则每当 Pluto 识别到正在处理该连接时，都会添加日志。

例如，启动 Pluto 并显示输出：

`pluto --debug-parsing`

稍后更改 Pluto 显示原始字节：

`plack --debug-raw`

对于测试，SSH 的页面很有用：

`http://isakmp-test.ssh/`

提示：ISAKMP SA 即使在 IPsec 建立后通常也由 IKE 保持存活。这允许直接协商 IPsec SA。如果其中一个 IKE 重启，另一个可能会尝试使用 ISAKMP SA，但新的 Pluto 不知晓这一点。Pluto 不够聪明来避免这种混乱。

## Pluto 在出现问题时的行为

当 Pluto 不理解或接受某条消息时，它会忽略该消息。IKE 守护进程在未来可能会使用通知（Notifications）来实现这一点。

当 Pluto 没有收到消息的响应时，它会重发相同的消息（最多发送三次）。这是合适的：UDP 是不可靠的。

当 Pluto 收到已经见过的消息时，它会丢弃。这对于 UDP 是合适的。



结合这三条规则，可以解释许多奇怪的行为。在 Pluto 日志中，重试不是最有趣的事件。关键点是早于（Pluto 收到了一条它不喜欢的消息并忽略了，因为它仍在等待可接受的消息）或者在另一端（Pluto 没有发送之前的消息）。

## 注意事项

如果 Pluto 编译时没有带 `-DKIPS`，它会协商安全关联（Security Associations），但永远不会进行路由更改。这在没有 KLIPS 的系统中是有用的。每个 IPSec 分配一个32 位 SPI，IKE 协议允许 SA 选择 SPI。0 到 `0xFF` 范围留给 IANA 使用。Pluto 还避免选择 `0x100` 到 `0FFF` 范围内的 SPI，用于手动密钥。记住，如果不是 Pluto，对方可能会选择此范围内的 SPI。

## 策略

此策略目录在尝试让 Pluto 与另一个 IKE 实现进行互操作时可能有用。

在阶段 1 中，只支持主模式（Main Mode）。我们不确定激进模式（Aggressive Mode）是否安全。对于某些情况，它允许更严重的拒绝服务攻击。

不支持信息交换（Informational Exchanges）。这些是可选的，且其交付无法保证，它们并不重要。事实是某些 IKE 实现无法与信息交换互操作，但我们认为它们损坏了。

不支持信息负载（Informational Payloads）。这些是可选的，但很有用。令人担心的是这些负载在阶段 1 或阶段 2 消息中均未经过 `HASH(3)` 认证。

- Diffie-Hellman 组 MODP 1024 和 MODP 1536（2 和 5）被支持。MODP768（1）不受支持，因为太弱了。
- 主机认证可以通过 RSA 签名或预共享密钥（Pre-Shared Secrets）完成。
- `3DES CBC`（密码块链模式）是唯一支持的加密，同时适用于 ISAKMP SA 和 IPSec SA。
- 两种 SA 都支持 MD5 和 SHA1 哈希用于数据认证。
- 支持 ESP、AH 或 AH ESP。当且仅当 AH 和 ESP 结合时，ESP 不需要其认证组件。该选择由 `--encrypt` 和 `authenticate` 标志控制。
- 这些中的每一项都可能与 IPCOMP Deflate 压缩结合，但仅当潜在连接指定了压缩且 KLIPS 配置了 IPCOMP 支持时如此。
- 在适当的情况下，IPSEC SA 可以是隧道（tunnel）或传输模式。`--tunnel` 标志控制 Pluto 的发起。
- 当响应 ISAKMP SA 提议时，最大可接受寿命为八小时。默认为一小时。没有最小值。`--ikelifetime` 标志在 Pluto 时控制此。
- 当响应 IPSEC SA 提议时，最大可接受寿命为一天。默认为八小时。没有最小值。`--ipseclifetime` 标志在 Pluto 发时控制此。
- PFS 是接受的，如果指定了 `--pfs` 标志，则会被提议。建议的 DH 组将与阶段 1 协商的相同。

## 信号

Pluto 响应 `SIGHUP` 时会发出一个建议，暗示可能本想执行“`plack --listen`”。

Pluto 在接收 `SIGTERM` 时退出。

## 退出状态

Pluto 通常会派生一个守护进程，因此退出状态通常是一个非常初步的结果。

- `0`：意味着到目前一切正常。
- `1`：意味着出现了一些错误。
- `2`：意味着锁文件已存在。

`plack` 检测到问题时，将返回退出状态 `1`。如果它收到了来自 Pluto 的进度消息，它返回最后一条非发送到 syslog 或非注释消息的数字前缀值作为状态（但成功的前缀被视为 `0`）。否则，退出状态为 `0`。

## 文件

```
/var/run/pluto.pid
/var/run/pluto.ctl
/etc/ipsec.secrets
/dev/urandom
```

## 环境

`IPSEC_EXECDIR`

`IPSECmy`

`PLUTO_CORE_DIR`

## 另请

相关的 Pluto 发行版，特别是 `ipsec(8)`。

`ipsec_auto(8)` 设计用于让 Pluto 更加方便。

`ipsec_secrets(5)` 描述 secrets 文件的格式。

`ipsec_atoaddr(3)` 是 Libreswan 发行版的一部分，描述了地址可能采取的形式。`ipsec_atosubnet(3)` 是 Libreswan 发行版的一部分，描述了子网可能采取的形式。

关于 IPSec、邮件列表以及相关文档，请参：

`https://datatacker.ietf.org/wg/ipsec/charter/`

在编写时，相关的 IETF RFC 是：

`RFC5996` 密钥交换协议版本2 (`IKEv2`)

Libreswan 网站 `<https://libreswan.org>` 以及上面的邮件列表。

## 历史

此代码根据 GPL 条款发布。详情见随附的文件 `COPYING` 和 `CREDITS`。

此软件最初是为 Free/WAN 项目 `<http://www.freeswan.org>` 编写的，该项目由 John Gilmore 创立并 Hugh Daniel 管理。Angelos D. Keromytis (`angelos@dsl.cis.upenn.edu`) 于 1997 年 5 月至 6 月在希腊编写。感谢 John Ioannidis 的帮助。

希腊加拿大的法规允许代码自由分发。

Free/WAN 的 Pluto 在 2000 年至 2004 年间由 D. Hugh Redelmeier (`hugh@mimosa.com`) 在加拿大开发。

IKE 版本 2 最初由 Michael Richardson、Antony Antony 和 Paul Wouter 编写。随后由 Avesh Agarwal、D. Hugh Redelmeier、Matt Rogers、Antony Antony 和 Paul Wouter 进行了扩展。

# 缺陷 (BUGS)

请访问 `<https://bugs.libreswan.org>` 查看当前已知和缺失功能的列表。

缺陷应向 `<swan-dev@lists.libreswan.org>` 邮件列表报告。

用于抑制警告的占位符

# iptables-extensions

| 名称 |

| iptables-extensions – 标准 iptables 分发版中的扩展列表 |

## 摘要

```
ip6tables [-m name [module-options...]] [-j target-name [target-options...]
```

```
iptables [-m name [module-options...]] [-j target-name [target-options...]
```

# 匹配扩展 (MATCH EXTENSIONS)

`iptables` 可以使用 `-m` 或 `--match` 选项扩展数据包匹配，后跟匹配模块名称；在此之后，取决于特定的模块，可以使用各种额外的命令行选项。你可以在同一行中指定多个扩展匹配模块，并在指定模块后使用 `-h` 或 `--help` 选项来接收针对该模块的特定帮助信息。扩展模块按照它们在规则中指定的顺序进行评估。

如果指定了 `-p` 或 `--protocol`，且仅仅当遇到未知选项时，`iptables` 将尝试加载与协议同名的匹配模块，以尝试使该选项可用。

此模块根据**地址类型** (address type) 匹配数据包。地址类型用于内核网络栈内部，并将地址分类为不同的组。该组的准确定义取决于特定的三层协议。

以下是可能的地址类型：

- UNSPEC
  - 未指定的地址（即 0.0.0.0）
- UNICAST
  - 单播播地址
- LOCAL
  - 本地地址
- BROADCAST
  - 广播地址
- ANYCAST
  - 任播播数据包
- MULTICAST
  - 组播地址
- BLACKHOLE
  - 黑洞地址
- UNREACHABLE
  - 不可到达的地址
- PROHIBIT
  - 禁止地址
- THROW
  - FIXME
- NAT
  - FIXME
- XRESOLVE

- `[!]`--src-type type
  - 如果源地址为给定类型，则匹配
- --dst-type type
  - 如果目标地址为给定类型，则匹配
- --limit-if-in
  地址类型检查可以限制为数据包进入的接口。
  此选项仅在 PREROUTING、INPUT 和 FORWARD 链中有效。不能与 --limit-iface-out 选项一起指定。
- --limit-iface-out
  地址类型检查可以限制为数据包出的接口。
  此选项仅在 POSTROUTING、OUTPUT 和 FORWARD 链中有效。不能与 --limit-iface-in 选项一起指定。

# ah (特定于 IPv6)

此模块匹配 IPsec 数据包中认证头部（Authentication header）中的参数。

- `[!]` --ahspi spi[:spi]
  匹配 SPI。
- `[!]`--ahlen length
  此头部以字节为单位的总长度。
- --ahres
  匹配预留字段是否填充为零。

# ah (特定于 IPv4)

此模块匹配 IPsec 数据包认证头部（Authentication header）中的 SPI。

- `[!]`--ahspi spi[:spi]

# bpf

使用 Linux 套接字过滤器 (Socket Filter) 进行匹配。期望十进制格式的 BPF 程序。这是由 `nbfpf_compile` 工具生成的格式。

- --bytecode code
  传递 BPF 字节码格式（见下文示例）。
  代码格式类似于 `tcpdump -ddd` 命令的输出：第一行存储指令数量，随后每条指令占一行。指令行遵循十进制表示法的 ‘u16 u8 u8 u32’ 模式。字段编码了操作、未设置时跳转、跳转偏移量为假以及通用数值字段 ‘K’。不支持注释。
  例如，要仅读取匹配的‘ip proto 6’，请插入以下内容（不包含注释或末尾空格）：
  `+ 4 # 指令数量 48 0 0 9 # 加载字节 ip->proto 21 0 1 6 0 # 跳转，如果相等`
  `IPPRTO_TCP 6 0 0 1 # 返回通过（非零） 6 0 0 0 # 返回失败（零）`
  你可以通过以下命令将其传递给 bpf 过滤器：

```
iptables -A OUTPUT -m bpf --bytecode '4,48 0 0 9,21 0 1 6 0 1,6,0 0 1,0 0' -j
```

# ACCEPT

或者，你可以调用 `nbfpf_compile` 工具。

```
iptables -A OUTPUT -m bpf --bytecode `nbfpf_compile RAW 'ip proto 6''' -j ACCEPT
```

你可能想从 FreeBSD 的 `bpf(4)` 手书中学习更多关于 BPF 的知识。

# cgroup

- --cgroup fwid
  匹配此数据包对应的 cgroup。
  可用于系统上的任务/作业分配特定的防火墙策略。这允许针对系统部分进程实现更细粒度的防火墙策略。`fwid` 是通过 net_cls cgroup 的 id 设置的标记。
  示例：

```
iptables -A OUTPUT -p tcp --sport 80 -m cgroup ! --cgroup 1 -j DROP
```

自 Linux 3.14 起可用。

# cluster

允许在没有负载均衡器的情况下部署网关和后端负载共享集群。

此匹配要求所有节点具有相同的包。因此，集群匹配根据以下选项决定该节点是否需要处理数据包：

- --cluster-total-nodes num
  设置集群节点总数。
- `[!]`--cluster-local-node num
  设置本地节点 ID。
- `[!]`--cluster-local-nodemask
  设置本地节点 ID 掩码。你可以使用此选项代替 --cluster-local-node。
- --cluster-hash-seed value
  设置 Jenkins.hash 的种子值。
  示例：

```
iptables -A PREROUTING -t mangle -i eth1 -m cluster
```

# comment

允许为任何规则添加注释（最多 256 字符）。

示例：
`iptables -A INPUT -m comment --comment`

# connbytes

根据连接到为止传输的字节数或包数进行匹配。

...

# connlimit

允许每个客户端 IP 地址（或客户端地址块）到服务器的并行连接数。

- --connlimit-upto n
  如果现有连接数小于或等于 n，则匹配。
- --connlimit-above n
  如果现有连接数大于 n，则匹配。
- --connlimit-mask prefix_length
  使用前缀长度对主机进行分组。对于 IPv4，必须是 0 到 32 之间的数字。对于 IPv6，在 0 到 128 之间。如果未指定，则使用适用协议的最大前缀长度。

## --connlimit-saddr

将限制应用于源组。如果未指定 --connlimit-saddr，则使用默认值。

## --connlimit-daddr

将限制应用于目的组。

示例：

# 为每个客户端主机允许 2 个 telnet 连接

```
iptables -A INPUT -p tcp --syn --dport 23 -m connlimit --connlimit-above 2 -j REJECT
```

# 你也可以反过来进行匹配：

```
iptables -A INPUT -p tcp --syn --dport 23 -m connlimit --connlimit-upto 2 -j ACCEPT
```

# 限制每个 C 类网络（24 位子掩码）的并行 HTTP 请求数量为 16 个

```
iptables -p tcp --syn --dport 80 -m connlimit --connlimit-above 16 --connlimit-mask 24 -j REJECT
```

# 限制本地链路局域网的并行 HTTP 请求数量为 16 个

```
iptables -p tcp --syn --dport 80 -s fe80::64 -m connlimit --connlimit-above 16 --connlimit-mask 64 -j REJECT
```

# 限制到特定主机的连接数：

```
iptables -p tcp --syn --dport 49152:65535 -d 2001:db8::1 -m connlimit --connlimit-above 100 -j REJECT
```

## --connnmark

此模块设置带有连接标记的 netfilter 字段（该标记通过下方的 CONNMARK 目标设置）。

- `[!]` --mark value[/mask]
  匹配具有给定标记值的连接中的数据包（如果指定了掩码，则在比较之前将其与标记进行逻辑与与运算）。

## --conntrack

此模块与连接跟踪（connection tracking）结合使用时，允许访问此数据包/连接的连接跟踪状态。

- `[!]` --ctstate statelist
  `statelist` 是一个用逗号分隔的匹配连接状态列表。可能的状态列在下文所示。
- `[!]` --ctproto l4proto
  要匹配的第四层协议（通过数字或名称）。
- `[!]` --ctorigsrc address[/mask]
- `[!]` --ctorigdst address[/mask]
- `[!]` --ctpletrd address[/mask]
  匹配原始/响应的源/目的地址
- `[!]` --ctorisrcport port[:port]
- `[!]` --ctorigdstport port[:port]
- `[!]` --ctplesrcport port[:port]
- `[!]` --ctreplldstport port[:port]
  匹配原始/响应的源/目的端口（TCP/UDP/等）或 GRE 键。端口范围的匹配仅在 2.6.38 以上的内核版本中支持。
- `[!]` --ctatus statelist
  `statuslist` 是一个用逗号分隔的匹配连接状态列表。状态列表在下文所示。
- `[!]` --ctexpire time[:time]
  与给定值或值范围（包含边界）匹配剩余的寿命（单位为秒）。
  `ctdir {ORIGINAL|REPLY}`
  匹配在指定方向流的数据包。如果未设置此标志，则匹配两个方向的数据包。
  --ctatus 的状态：
  ### INVALID
  数据包与任何已知的连接关联。
  ### NEW
  数据包启动了一个新连接，或者关联了一个双向都没有出现过数据包的连接。
  ### ESTABLISHED
  数据包与一个双向都出现过数据包的连接关联。
  ### RELATED
  数据包正在启动新连接，但关联于现有连接，例如 FTP 数据传输或 ICMP 错误。
  ### UNTRACKED
  数据包完全没有被跟踪，这发生在你在 raw 表中使用 `-j CT --notrack` 显式跟踪它时。
  ### SNAT
  虚拟状态，如果原始源地址与响应目的地址不同，则匹配。
  ### DNAT
  虚拟状态，如果原始目的地址与响应源地址不同，则匹配。
  --ctatus 的状态：
  ### NONE
  均不是。
  ### EXPECTED
  这是一个预期的连接（即由 conntrack 助手设置的）。
  ### SEEN_REPLY
  conntrack 已经看到双向的数据包。



### ASSURED

`conntrack` 条目不应过早过期。

### CONFIRMED

连接已确认：原始数据包已离开设备。

## `--cpu`

- `[!]` `--cpu number`

匹配处理此数据包的 CPU。CPU 编号从 0 到 `NR_CPUS-1`。可以与 RPS（远程数据包调度）或在不同队列上带有网络流量的多队列网卡结合使用。

示例：

```
iptables -t nat -A PRERUTING -p tcp --dport 80 -m cpu --cpu 0 -j REDIRECT --to-port 8080
iptables -t nat -A PRERUTING -p tcp --dport 80 -m cpu --cpu 1 -j REDIRECT --to-port 8081
```

自 Linux 2.6.36 起可用。

## `--dccp`

- `[!]` `--source-port,--sport port[:port]`

- `[!]` `--destination-port,--dport port[:port]`

- `[!]` `--dccp-types mask`

当 DCCP 数据包类型为 ‘mask’ 之一时匹配，“mask’ 是用逗号分隔的数据包类型列表。数据包类型有：REQUEST RESPONSE DATA ACK DATAACK CLOSEREQ CLOSE SYNCACK

- `[!]` `--dccp-type`

匹配 DCCP 数据包类型为 ‘mask’ 之一，“mask’ 是用逗号分隔的数据包类型列表。数据包类型有：REQUEST RESPONSE DATA ACK DATAACK CLOSEREQ CLOSE SYNCACK

- `[!]` `--dccp-type`

匹配 DCCP 数据包类型为 ‘mask’ 之一，“mask’ 是用逗号分隔的数据包类型列表。数据包类型有：REQUEST RESPONSE DATA ACK DATAACK CLOSEREQ CLOSE SYNCACK

## `--dev`

- `[!]` `--dev`

匹配设备接口。

- `[!]` `--src-group`

匹配入站接口。

- `[!]` `--dst-group`

匹配出站接口。

## `--dscp`

- `[!]` `--dscp`

匹配 IP 头部中的 DSCP 字段。这是 TOS 字段中的 6 位字段。

- `[!]` `--dscp-value`

匹配 TOS 字段中的 DSCP 值。

- `[!]` `--dscp-class`

匹配 DSCP 类。

## `--dst`

- `[!]` `--dst`

匹配目的地址。

- `[!]` `--dst-len`

匹配目的长度。

- `[!]` `--dst-opts`

匹配目的选项。

- `[!]` `--dst-type`

匹配目的类型。

- `[!]` `--dst-class`

匹配目的类。

## `--esp`

- `[!]` `--esp`

匹配 ESP 头部。

- `[!]` `--esp-spi`

匹配 SPI 索引。

## `--eui64`

- `[!]` `--eui64`

匹配 EUI-64 地址。

## `--ecn`

- `[!]` `--ecn`

匹配 ECN 字节。

- `[!]` `--ecn-cwr`

匹配设置的 CWR 位。

- `[!]` `--ecn-ece`

匹配设置的 ECE 位。

- `[!]` `--ecn-num`

匹配 ECN 数量。

## `--frag`

- `[!]` `--frag`

匹配分片参数。

- `[!]` `--frag-id`

匹配分片标识。

- `[!]` `--frag-len`

匹配分片长度。

- `[!]` `--frag-first`

匹配第一个分片。

- `[!]` `--frag-more`

如果有更多分片则匹配。

- `[!]` `--frag-last`

匹配最后一个分片。

- `[!]` `--frag-res`

匹配保留字段。

## `--hashlimit`

`hashlimit` 使用哈希桶（hash buckets）表示对连接组的速率匹配（类似于 `limit`）。分组可以按主机（源地址和或目的地址）以及/或端口进行。它提供了“每个时间量子 N 个包”或“每秒 N 字节”的能力（见下文示例）。

需要限制选项（`hashlimit-upto,--hashlimit-above`）和 `--hashlimit-name`。

- `[!]` `--hashlimit-upto [/second/minute/day]`

当速率小于或等于量子时匹配。它可以指定为数字并带有可选的时间后缀（默认是 shour），或者指定为数量/秒（每秒字节数）。

- `[!]` `--hashlimit-above [/second/minute/day]`

当速率高于数量/量子时匹配。

- `[!]` `--hashlimit-burst`

最大初始匹配包数：每当未达到上述限制时重新加载此数字；默认值为 5。当请求基于字节的匹配时，此选项指定超出给定速率的字节数。

- `[!]` `--hashlimit-mode {scrip/srcport/dst/dstport},...`

要考虑的对象逗号分隔列表。如果给了一个 `--hashlimit-mode` 选项，`hashlimit` 的作用类似于 `limit`，但是以进行哈希维护为代价的。

- `[!]` `--hashlimit-scrmask prefix`

当使用 `--hashlimit-mode scrip` 时，所有遇到的源地址将根据给定的前缀长度进行分组，创建的子网将受 `hashlimit` 控制。前缀必须在 0 到 32 之间（包含）。注意 `--hashlimit-srcmask 0` 基本上与没有为 `--hashlimit-mode` 指定 scrip 相同，但技术上开销更大。

- `[!]` `--hashlimit-dst prefix`

类似于 `--hashlimit-scrmask`，但针对目的地址。

- `[!]` `--hashlimit-name foo`

`/proc/net/ipt_hashlimit/foo` 条目的名称。

- `[!]` `--hashlimit-htable-size buckets`

哈希表的桶数量

# `hashlimit-htable-max entries`

哈表中的最大条目。

**`hashlimit-htable-expire msec`**

哈希条目过期的时间（毫秒）。

**`hashlimit-htable-ginterval msec`**

垃圾回收间隔的时间（毫秒）。

示例：

- 匹配源端口

"对于 192.168.0.0/16 中的每个主机每秒 1000 个数据包" => `s-192.168.0.0/16 --hashlimit-mode script --hashlimit-upto 1000/sec`

"192.168.1.1 的每个服务每秒 100 个数据包" => `s-192.168.1.1 --hashlimit-mode srcport --hashlimit-upto 100/sec`

匹配子网

"10.0.0.0/8 中的 /28 子网（每 8 个地址一组）每分钟 10000 个数据包" => `s-10.0.0.0/8 --hashlimit-mask 28 --hashlimit-upto 10000/min`

匹配每秒字节

"超过 512kb/s 的流" => `--hashlimit-mode script,dstip,srcport,dstport --hashlimit-above 512kb/s`

匹配每秒字节

"超过 512kb/s 的主机，但允许达到 1Megabytes 而不匹配" `--hashlimit-mode dst --hashlimit-above 512kb/s --hashlimit-burst 1mb`

# `hbb` (IPv6 专用)

此模块匹配逐跳选项（Hop-by-Hop Options）头部中的参数。

- **`hbb-len length`**

该头部的总长度（字节为）。

**`hbb-opts type[:length][type[:length]...]`**

选项的数值类型以及选项数据的长度（字节为）。

# `helper`

此模块匹配与特定连接跟踪辅助（conntrack-helper）相关的数据包。

- **`helper string`**

匹配与指定的 conntrack-helper 相关的数据包。

字符串可以是 "`ftp`" ，用于匹配与默认端口上的 ftp 会话相关的数据包。对于其他端口，在值后附加 `--portnr`，例如 "`ftp-2121`"。

相同的规则适用于其他 conntrack-helpers。

# `hl` (IPv6 专用)

此模块匹配 IPv6 头部中的跳数（Hop Limit）字段。

- **`hl-eq value`**

如果 Hop Limit 值等于该值则匹配。

- **`hl-lt value`**

如果 Hop Limit 小于该值则匹配。

- **`hl-gt value`**

如果 Hop Limit 大于该值则匹配。

# `icmp` (IPv4 专用)

当指定 `--protocol icmp` 时可以使用此扩展。它提供了以下选项：

- `[!]` `--icmp-type {type/code}typename`

这允许指定 ICMP 类型，可以是数值型 ICMP 类型、类型/代码对，或者命令 `iptables -p icmp -h` 显示的 ICMP 类型名称之一。

# `icmp6` (IPv6 专用)

如果指定 `--protocol icmp6` 或 `--protocol icmpv6`，可以使用此扩展。它提供了以下选项：

- `[!]` `--icmp6-type type/[code]typename`

这允许指定 IPv6 类型，可以是数值型 IPv6 类型、类型和代码，或者命令 `iptables -p ipv6-icmp -h` 显示的 ICMP6 类型名称之一。

# `ipprange`

匹配给定的任意 IP 地址范围。

- `[!]` `--src-range from[--to]`

匹配指定范围内的源 IP。

- `[!]` `--dst-range from[--to]`

匹配指定范围内的目的 IP。

# `ipv6header` (IPv6 专用)

此模块匹配 IPv6 扩展头部和/或上层头部。

- `--soft`

如果数据包包含使用 `--header` 指定的任何头部则匹配。

- `[!]` `--header header[--header...]`

这匹配**恰好**包含所有指定头部的数据包。使用 ESP 头部封装的头部不在范围内。可能的头部类型可以是：

- `hop-by-hop`: 逐跳选项头部（Hop-by-Hop Options header）

- `dst`: 目的选项头部（Destination Options header）

- `route`: 路由头部（Routing header）

- `frag`: 分片头部（Fragment header）

- `auth`: 认证头部（Authentication header）

- `esp`: 封装安全负载头部（Encapsulating Security Payload header）

- `none`: 在任何 IPv6 扩展头部的“下一个头部”（Next Header）字段中匹配 59 的 Next头部，或匹配任何上层协议的 proto。数字 255 等同于所有。

# `ipvs`

- 匹配 IPVS 连接属性。

- `[!]` `--ipvs` 数据包属于 IPVS 连接。以下任何选项都意味着 `--ipvs`（即使是取反的）：

- `[!]` `--vproto protocol` 待匹配的协议；通过数字或名称，例如 "`tcp`"。

- `[!]` `--vaddr[/mask]` 待匹配的 VIP 地址。

- `[!]` `--vport` 待匹配的 VIP 端口；通过数字或名称，例如 "`http`"。

- `[!]` `--vdir {ORIGINAL|REPLY}` 数据包的方向。

- `[!]` `--method {GATE|IP|MASQ}` 使用的 IP 转发方法。

- `[!]` `--vportctl` 匹配的控制连接端口，例如 FTP。

# `length`

此模块将三层负载（例如四层数据包）的长度与特定值进行匹配。

- `[!]` `--length[:length]`

# `limit`

此模块使用令牌桶以限制速率进行匹配。使用此扩展的规则将一直匹配直到达到此限制。它可以用于限制。

- `[!]` `--limit[:second][/day]` 限制速率，直到达到此限制后停止匹配。

- `--limit-burst` 限制时允许的突发数据包数。

# `mac`

- `[!]` `--mac` 源 MAC 地址。

Windows [2000:SP3]:Windows XP SP1, 2000 SP3]: 11.22.33:55:4024 -> 11.22.33.44:139 hops=3 Linux [2.5-6] : 1.2.3.4:42624 -> 1.2.3.5:22 hops=4

OS 系统指纹可以通过 `nfnl_ofs` 程序加载。要从 a 加载指纹，使用：

```
nfnl_ofs -f /usr/share/xtables/pf.os
```

要删除它们，

```
nfnl_ofs -f /usr/share/xtables/pf.os
```

指纹数据库可以从 http://www.openbsd.org/cgi-bin/cvsweb/src/etc/pf.os 下载。

## `owner` 所有

该模块尝试为本地生成的数据包匹配数据包创建者的各种特征。这种匹配仅在 OUTPUT 和 POSTROUTING 链中有效。转发的数据包没有与之关联的套接字（socket）。内核线程的数据包有套接字，但通常没有所有者。

- `[!]`--uid-owner 用户名

- `[!]`--uid-owner 用户ID[-uid]

如果数据包的文件结构（如果有的话）属于指定的用户，则匹配。

你也可以指定一个数值 UID 或一个 UID 范围。

- `[!]`--gid-owner 组名

- `[!]`--gid-owner 组ID[-groupId]

如果数据包的文件结构属于指定的组，则匹配。你也可以指定一个数值 GIF 或一个 G 范围。

- `[!]`--socket-exists

如果数据包与套接字关联，则匹配。

## `physdev` 物理设备

该模块匹配隶属于桥接设备（bridge device）的桥接端口输入输出设备。该模块是实现透明桥接防火墙的基础设施的一部分，仅适用于内核版本 2.5.44 以上。

- `[!]`--physdev-in 名称

接收数据包的桥接端口名称（仅用于进入 INPUT、FORWARD 和 PREROUTING 链的数据包）。如果接口名称以“+”结尾，则任何以此名称开头的接口都将匹配。如果数据包不是通过桥接设备到达的，除非使用 '!'，否则该数据包不会匹配此项。

- `[!]`--physdev-out 名称

发送数据包的桥接端口名称（用于进入 FORWARD、OUTPUT 和 POSTROUTING 链的数据包）。如果接口名称以“+”结尾，则任何以此名称开头的接口都将匹配。注意，在 nat mangle OUTPUT 链中无法匹配桥输出端口，但在 filter OUTPUT 链中可以。如果数据包不会离开桥接设备，或者尚未知输出设备是什么，则数据包不会匹配此选项，除非使用了‘！’。

- - **physdev-is-in**

如果数据包通过桥接接口进入，则匹配。

## `pkttype` 数据包类型

该模块匹配链路层数据包类型。

- **pkt-type {单播|广播|组播}**

## `policy` 策略

该模块匹配 IPsec 使用的策略

- **dir {in|out}**

用于选择匹配用于解封装的策略或将要用于封装的策略。**in** 在 **PREROUTING、INPUT 和 FORWARD** 中有效，**out** 在 **POSTROUTING、OUTPUT 和 FORWARD** 链中有效。

- **pol {none|ipsec}**

如果数据包受 IPsec 处理，则匹配。**pol none** 无法与 **strict** 结合。

- **strict**

选择是匹配精确策略，还是匹配匹配给定策略的任何规则。

对于每个策略元素，可以使用以下一个或多个选项。当 —**strict** 起作用时，每个元素至少必须使用一个。

- **reqid id**

匹配策略规则的 reqid。可以通过 **setkey(8) using unique:id** 作为级别指定 reqid。

- **spi spi**

匹配 SA 的 SPI。

- **proto {ah|esp|ipcomp}**

匹配封装协议。

- **mode {隧道模式|传输模式}**

匹配封装模式。

- **tunnel-src 地址[/掩码]**

匹配隧道模式 SA 的源端点地址。仅对 —**mode tunnel** 有效。

- **tunnel-dst 地址[/掩码]**

匹配隧道 SA 的目的端点地址。仅对 —**next mode tunnel 有效。开始策略规范中的下一个元素。只能与 —**strict** 使用。

## `quota` 配额

通过对每个数据包递减字节计数器来实现网络配额。条件一直持续到字节计数器达到零。行为在取反时会改变（即在字节计数器达到零之前条件不匹配）。

> [!]—quota 字节

以字节为单位的配额。

## `rateest` 速率估计

速率估计器可以匹配 RATEEST 目标收集的估计速率。支持匹配绝对 bps/pps 值、比较两个速率估计器并匹配两个速率估计器之间的差。

为了更好地理解可用选项，这些是所有可能的组合：rateest 操作 rateest-bps rateest 操作 rateest-pps (rateest 减 rateest-bps1) 操作 rateest-bps2 rateest1 操作 rateest-bps2 rateest1 操作 rateest-bps(无速率!) rateest1 操作 rateest-pps(无速率!) (rateest1 减 rateest-bps1) 操作 (rate2 减 rateest-bps) (rate1 minus rate-pps)

## `rateest-delta` 速率差



对于每个估计器（无论是绝对模式还是相对模式），计算估计器确定的流速率与静态值之间的差。如果流速率高于指定的 PPS，则使用 0 代替负值。`“max(0, rateest_bps)”`。

> [!]—`rateest-lt`

如果速率小于指定的速率/估计器，则匹配。

> [!]—`rateest-gt`

如果速率大于指定的速率/估计器，则匹配。

> [!]—`rateest-eq`

如果速率等于指定的速率/估计器，则匹配。在所谓的“绝对模式”中，使用一个估计器并对比静态值；而在“相对模式”中，比较两个估计器。

- —`rateest` 名称

绝对模式的估计器名称。

- —`rateest1`

—`rateest2`

相对模式的两个估计器名称。

`rateest-bps` [值]

`rateest-pps` [值]

`rateest-bps1` [值]

`rateest-bps2` [值]

`rateest-ps1` [值]

`rateest-ps2` [值]

通过字节或每秒比较估计器(s)，并与选择的值比较。查看上方列表在什么情况下使用选项。后缀可以是：`[gt]bit, [gt]bit, [gt]ps`。

示例：这是根据连接开始时的可用带宽路由来自服务器的连接：

## Estimate outgoing rates 估计输出速率

```
iptables -t mangle -A POSTROUTING -o eth0 -j RATE --rateest-name eth0 --rateest-interval 250ms --rateest-ewma 0.5s
iptables -t mangle -A POSTROUTING -o ppp0 -j RATE --rateest-name ppp0 --rateest-interval 250ms --rateest-ewma 0.5s
```

## Mark based on available bandwidth 基于可用带宽标记

```
iptables -t mangle -A balance -m conrack -ctstate NEW -m helper -m rateest --rateest-delta eth0 --rateest-bps1 2bit --rateest-gt ppp0 --rateest-bps2 2bit -j CONNMARK --set-mark 1
iptables -t mangle -A balance -m conrack -ctstate NEW -m helper -m rateest --rateest-delta ppp0 --rateest-bps1 2bit --rateest-gt eth0 --rateest-bps2 2bit -j CONNMARK --set-mark 2
iptables -t mangle -A balance -j CONNMARK --restore
```

## realm 区域（IPv4 特定）

匹配路由区域。路由区域用于涉及 BGP 等动态协议的复杂路由设置。

> [!]—`realm` 数字（可选掩码）。如果不是数字，值可以是 `/etc/route2/rt_realms` 中的命名区域（情况下不能使用掩码）。匹配 `/etc/route2/rt_realms` 中的给定区域（情况下不能使用掩码）。

## recent 最近

允许你动态创建 IP 地址列表，然后以几种方式匹配该列表。例如，你可以为尝试连接到防火墙 139 端口的人创建一个“坏人”列表，并在不考虑它们的情况下丢弃所有后续数据包。

—`set`、—`check`、update 和 —`remove` 是互斥的。

- —`name` 名称

指定命令使用的列表。如果没有给出名称，将使用 DEFAULT。

- [!]—`set`

将数据包的源地址添加到列表中。如果源地址已经在列表中，则更新更新现有条目。这将始终返回成功（或传递失败 !）。

- —`source`

匹配/保存最近列表表中每个数据包的源地址。这是默认值。

- —`rdest`

匹配/保存最近列表表中每个数据包地址。

- —`mask` 掩码

应用于此最近列表的网络掩码。

- [!]—`rcheck`

检查数据包的源地址当前在列表中。

- [!]—`update`

类似于—`rcheck`，如果匹配，将更新“最后看到”时间戳。

- [!]—`remove`

检查数据包的源地址当前在列表中，如果是，则将该地址从列表中移除且规则返回 true。如果未找到地址，则返回 false。

- —`seconds` 秒数

此选项必须与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中并在最后指定的秒数内被看到时发生。

- —`reap`

此选项只能与 —`seconds` 配合使用。当使用时，这将清除早于最后指定的秒数的条目。

- —`hitcount` 次

此选项必须与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中且收到的数据包大于或等于该值时发生。此选项可以配合 —`seconds` 使用，创建一个在特定时间内需要特定次数的更窄的匹配。`hitcount` 参数的最大值由 `xt_recent` 内核模块的“`ip_pkt_list_to`”参数给出。超过此值的命令行将导致路由被拒绝。

- —`rtl`

此选项可能只能与 —`rcheck` 或 —`update` 之一一起使用。当使用时，这将匹配缩小为仅当地址在列表中且当前数据包的 TTL 与命中 —`set` 规则的数据包的 TTL 匹配时发生。

如果你在使用此模块通过发送伪造数据包到你的网站来阻止他人访问时，遇到了 DoS 伪造源地址的问题，那么这可能有所帮助。

示例：

```
iptables -A FORWARD -m recent --name badguy --rcheck --seconds 60 -j DROP
iptables -A FORWARD -p tcp --i eth0 --dport 139 -m recent --name badguy --set -j DROP
```

`/proc/net/xt_recent/*` 是当前地址列表以及每个列表中每个条目的信息。

可以读取 `/proc/net/xt_recent/` 下的每个文件来查看当前列表，或使用以下命令进行写入以修改列表：

```
echo +addr > /proc/net/xt_recent/DEFAULT
将 addr 添加到 DEFAULT 列表中
echo -addr > /proc/net/xt_recent/DEFAULT
从 DEFAULT 列表中移除 addr
echo / > /proc/net/xt_recent/DEFAULT
清空 DEFAULT 列表（移除所有条目）。
```

该模块本身接受参数，默认值如所示：

- `ip_list_tot=100`

每个表记录的地址数量。

- `ip_pkt_list_tot=20`

每个地址记录的数据包数量。

- `ip_list_hash_size=0`

哈希表大小。0 表示根据 `ip_list_tot` 计算，默认值：512。

- `ip_list_perms=0644`

`/proc/net/xt_recent/*` 文件的权限。

- `ip_list_uid=0`

`/proc/net/xt_recent/*` 文件的所有者数值 UID。

- `ip_list_gid=0`

`/proc/net/xt_recent/*` 文件的所有者数值 GID。

# rpfilter

对数据包执行反路径过滤测试。如果对数据包的回复通过数据包到达的接口发送，则该数据包将匹配。注意，与内核中的 `rp_filter` 不同，受 IPsec 的数据包不会被特殊处理。如果你需要，可以将此匹配与策略匹配结合。此外，通过环回接口到达的数据包始终是允许的。此匹配只能在 raw 或 mangle 表的 PREROUTING 链中使用。

- -`loose`

用于指定即使选定的输出设备不是预期的设备，反路径过滤测试也应匹配。

以及在执行反路径路由查找时数据包的 `nfmark` 值。

- -`accept-local`

这将允许来自网络且源地址分配给本地机器的数据包通过检查。

- -`invert`

这将反转匹配的含义。不再匹配通过反路径过滤测试的数据包，而是匹配测试失败的数据包。

记录并丢弃反路径过滤测试失败包的示例：

```
iptables -t raw -N RPFILTER
iptables -t raw -A RPFILTER -m rpfilter -j RETURN
iptables -t raw -A RPFILTER -m limit --limit 10/minute -j nflog --nlog-prefix "rpfilter drop"
iptables -t raw -A RPFILTER -j DROP
iptables -t raw -A PREROUTING -j RPFILTER
```

不记录日志直接丢弃失败包的示例：

```
iptables -t raw -A RPFILTER -m rpfilter --invert -j DROP
```

# rt (IPv6 专用)

匹配 IPv6 路由头部

- [!] --`rt-type` type

匹配类型（数值）。

- [!] --`rt-segleft` num[:num]

匹配“剩余段”字段（范围）。

- [!] --`rt-len` length

匹配该头部的长度。

- --`rt-0-res`

也匹配预留字段（type=0）

- --`rt-0-adds` addr[,addr...]

匹配 type=0 的地址（列表）。

- --`rt-0-strict`

type=0 的地址列表为严格匹配。

# sctp

- [!] --`source-port,--sport[::port]`

源端口

- [!] --`destination-port,--dport[::port]`

目的端口

- [!] --`chunk-types` {all|any|only} chunktype[:flags]

大写标记表示在已设置时匹配，小写表示在未设置时匹配。

块类型：DATA INIT INIT_ACK SACK HEARTBEAT HEARTBEAT_ACK ABORT SHDOWN SHDOWN_ERROR COOKIE ECHOCHO COOKIE_ACK ECN SHDOWN_COMPLETE ASCONF ASCONF_ACK CWR FORWARD_TS SHDOWN_COMPLETE

（小写表示“关闭”，大写表示“开启”）

示例：

```
iptables -A INPUT -p sctp --dport 80 -j DROP
iptables -A INPUT -p sctp --chunk-types any -j DROP
iptables -A INPUT -p sctp --chunk-types any -j ACCEPT
```

此模块匹配由 `ipset()` 定义的 IP 集

- [!] --`match-set` setname[,flag]...

其中 flags 是逗号分隔的 src 或 dst 指定，最多可以六个。因此，命令 `iptables -A FORWARD -m set --match-set src,dst` 会匹配在指定的集中可以找到（例如 ipmap））源地址和目的端口对的数据包。

- --`nomatch`

如果指定了 --`nomatch` 且集支持 nomatch 标记，则匹配反转：标记为 nomatch true 的元素，匹配返回 false。

- --`update-counters`

如果 --`update-counters` 标记被反转，则集中匹配元素的数据包计数和字节计数不会更新。默认更新数据包计数。

- --`update-subcounters`

如果 --`update-subcounters` 标记被反转，则集中匹配元素的数据包计数和字节计数不会更新。默认更新数据包计数。

- [!] --`packets-eq` value

如果数据包匹配集中的元素，仅当数据包计数等于给定值时匹配。

- --`packets-lt` value

如果数据包匹配集中的元素，仅当数据包计数小于给定值时匹配。

- --`packets-gt` value

如果数据包匹配集中的元素，仅当数据包计数大于给定值时匹配。

- --`bytes-eq` value

如果数据包匹配集中的元素，仅当字节计数等于给定值时匹配。

- --`bytes-lt` value

如果数据包匹配集中的元素，仅当字节计数小于给定值时匹配。

- --`bytes-gt` value

如果数据包匹配集中的元素，仅当字节计数大于给定值时匹配。

当定义集时不带计数器时，数据包和字节计数相关的选项将被忽略。使用 -m set 需要 iptset 支持，标准内核从 Linux 2.6.9 起提供。

# socket

如果通过对数据包进行 socket 查找可以找到的 TCP/UDP socket，则匹配。如果存在已建立的监听 socket（带有本地地址）。查找使用嵌入 ICMP 错误中的 TCP/UDP 头部元组执行。

- --`transparent`

忽略非透明 socket。

- --`wildcard`

不忽略绑定到“any”地址的 socket。socket 匹配默认接受零绑定监听，因为本地服务可能会拦截流量。此选项用于匹配转发到本地的流量。在使用 socket 匹配实现对非本地地址完全透明时，建议使用 --`transparent`。

示例（假设标记 1 的数据包被递送）：

```
iptables -t mangle -A PREROUTING -m socket --transparent -j MARK --set-1
```

# state

“state”扩展是“conntrack”模块的子集。“state”允许访问此数据包的连接状态。

- --`state` state

逗号分隔的要匹配连接状态列表。仅识别“conntrack”理解的部分状态：INVALID、ESTABLISHED、NEW、RELATED 或 UNTRACKED。有关它们的描述，请参见此手册中的“conntrack”章节。

# statistic

此模块根据某些统计条件匹配数据包。它支持通过 --`mode` 选项设置两种不同模式。

支持的选项：

- --`mode` mode

设置匹配规则的匹配模式，支持的模式为 random（随机）和 nth（第n）。

- [!] --`probability` p

设置数据包随机匹配的概率。它仅在 random 模式下有效。p 必须在 0.0 到 1.0 之间。支持的粒度为 1/2147483648 增量。

- [!] --`every` n

每 n 个数据包匹配一个。它仅对 nth 模式有效（见 --`packet` 选项）。

- --`packet` p

为 nth 模式设置初始计数（0 <= p <= n-1,默认为 0）。

# string

此模块通过某些匹配策略匹配字符串。它要求 linux 内核 >= 2.6.14。

- --`algo` {bmkmp}

选择匹配策略。（bm = Boyer-Moore, kmp = Knuth-Pratt-Morris）

- --`from` offset

设置查找任何匹配的偏移量。如果没有传递，默认为 0。

- --`to` offset

设置扫描到哪个偏移量。即 offset-1（从 0 开始计数）是最后一个扫描的。如果没有传递，默认为数据包大小。

- [!] --`string` pattern

匹配给定的模式。

- [!] --`hex-string` pattern

匹配十六进制表示的给定模式。

示例：

# 字符串模式可用于简单的文本字符。`iptables -A INPUT -p tcp --dport 80 -m string --algo --string ‘GET/index.html’ -j LOG`

# 十六进制模式可用于不可打印字符，如 |0D 0A| 或 |0D0A|, `iptables -p udp --dport 53 -m string --algo --from 40 --to 57 --hex-string ‘[03]www[09]netfilter[03]org[00]’`

当指定了 `protocol tcp` 时，可以使用这些扩展。它提供了以下选项：

- --`source-port,--port[:port]` 源端口范围指定。这可以是服务名，也可以是端口号。可以指定包含范围，默认为 "0"；如果省略了最后一个，则认为 "65535"。如果省略了第一个端口，且第一个端口大于第二个端口，则将交换它们。`--port` 参数是该选项的方便别名。

- --`destination-port,--dport port[:port]` 目的端口范围指定。`--dport` 参数是该选项的方便别名。

- --`tcp-flags mask` 当 TCP 标志符合指定时进行匹配。第一个参数 `mask` 是我们需要检查的标志，而 `argument` 是必须设置的标志的逗号分隔列表。标志有：ACK FIN RST URGSH ALL NONE -A FORWARD。例如 -p tcp-flags SYN, ACK, FIN, RST 将仅匹配设置了 SYN 标志且未设置 ACK, RST 标志的数据包。

- --`syn` 仅匹配带有 SYN 位且清除了 ACK、RST 和 FIN 位的 TCP 数据包。此类数据包用于请求建立 TCP 连接；例如，阻塞进入接口的此类包将阻止入站 TCP 连接，而不会影响传出的 TCP 连接。它等同于 `tcp-flags SYN,RST,ACK,FIN SYN`。如果 "!" 标志位于 `--syn` 之前，该选项会被取反。

- --`tcp-option number` 如果设置了选项则进行匹配。

## tcpmss

此匹配 TCP 头部中的 MSS（最大段大小）字段。你仅可以在 TCP SYN 或 SYN/ACK 包上使用此项，因为 MSS 仅在连接启动时的 TCP 握手期间协商 [:value]。

- --`mss value[:value]` 匹配给定的 TCP MSS 值或范围。

## time



## 时间匹配

如果数据包到达的时间日期在给定范围内则进行匹配。所有选项均为可选，指定时采用 `AND` 逻辑关系。默认情况下，所有时间均解释为 `UTC`。

`--datstart YYYY-MM-DD[HH:mm[:ss]]`
`--datestop YYYY-MM-DD[HH:mm[:ss]]`

仅在给定时间范围内匹配，该时间必须符合 ISO 8601 的 `"T"` 表示法。可能的时间范围是 `1970-01-01T00:00:00` 到 `2038-01-19T19:04:07`。如果未指定 `--datstart` 或 `--datestop`，它们将默认为 `1970-01-01` 和 `2038-01-19`。

`--timestart:mm[:ss]`
`--timestamp:mm[:ss]`

仅在给定的白天范围内匹配。可能的时间范围是 `00:00:00` 到 `23:59:59`。允许前导零，例如 `"06:03"`，并被正确解释为 10 进制。

- `--monthdays day[,day...]`

仅在月份的指定日期匹配。可能值为 `1` 到 `31`。注意，指定 `31` 将导致在没有 `31` 日的月份无法匹配；`28` 天或 `29` 天的二月也是如此。

- `--weekdays day[,day...]`

仅在指定的星期几匹配。可能的值分别为 `Mon`, `Tue`, `Wed`, `Thu`, `Fri`, `Sat`, `Sun`，或者 `1` 到 `7` 的值。你也可以使用双字符变体 `Mo`, `Tu` 等。

- `--contiguous`

当 `--timestart` 小于 `--timestamp` 值时，将其视为单一时段而非离散的间隔。参见示例。

- `--kernelz`

使用内核时区而不是 `UTC` 来判断数据包是否符合时间规定。

关于内核时区：Linux 始终以 `UTC` 保持系统时间，并一直如是。在启动时，系统时间从参考时间源初始化。如果该时间源没有时区信息，例如 `x86 CMOS RTC`，则将假设为 `UTC`。然而，如果时间源不是 `UTC`，用户空间应该向内核提供正确的系统时间和时区。

本地时间是建立在系统时间之上的一个功能。每个进程都有自己的本地时间概念，通过 `TZ` 环境变量指定。内核也有它自己的时区偏移变量。当显示基于 `UTC` 的系统时间时，例如当你运行 `date(1)` 时，或者你在桌面时钟上看到的内容，`TZ` 字符串可能会在不同日期解析不同的偏移，这使得用户空间在夏令时间 `DST` 变化时能够实现自动时间跳转。内核时区偏移用于将非 `UTC` 源如 `FAT` 文件系统转换为 `UTC`。

内核时区的陷阱在于，Linux 发行版可能会忽略内核时区，仅设置系统时间。即使特定的发行版设置了时区，它通常也保持内核时区偏移即在夏令时间变化的部分是最新的。`ntpd` 不接触内核时区，因此运行它无法解决此问题。因此，可能会遇到一个始终为 `+0000` 的时区，或者一个每年偏差半年的时间。因此，非常不建议使用 `--kernelz`。

示例。要匹配周末，使用：

```
-m time --weekdays Sa,
```

或者，在国家假日区块内匹配一次：

```
-m time --datestart 2007-12-25 --datestop 2007-12-25
```

## MSS 匹配

由于 `MSS` 仅在连接启动时的 `TCP` 握手期间协商 `[:value]`。

- `--mss value[:value]` 匹配给定的 `TCP MSS` 值或范围。

## 匹配总长度 >= 256 的 IP 数据包

`IP` 头部字节 `2-3` 包含一个总长度字段。

```
-u32 "& 0xFFFF >> 16 = 0x100"
```

读取字节 `0-3`，将与 `0xFFFF` 进行与并测试其是否在范围 `[0x100:0xFFFF]`。

## 匹配 `icmp` 类型为 `0` 的 `ICMP` 数据包

首先测试它是否为 `ICMP` 数据包，当第 `9` 字节协议 `= 1` 时为真

```
-u32 "& 0xFF >> 0 = 1"
```

读取字节 `6-9`，使用 `&` 丢弃字节 `6-8` 并将结果与 `1` 比较。接着测试它不是分片。

```
- 4 & 0x3FFF = 0
```

最后测试：`IP` 头部后的第一个字节类型为 `0`。这里必须使用 `@` 语法。`IP` 头部长度 `HL` 以 `32` 位形式存储在 `IP` 头部字节 `0` 的右半部分。

```
... 0 >> 22 & 0x3C @ 0 >> 24 = 0
```

## TCP 负载匹配示例

```
-u32 "& 0xFF >> 0 = 6"
... 0 >> 22 & 0x3C @ 12 >> 26 & 0x3C @ 8 = 1,2,5,8
```

## udp

如果指定了 `--protocol udp`，可以使用这些扩展。它提供了以下选项：

- `--source-port,--sport[:port]` 源端口或端口范围规范。参见 `TCP --source-port` 选项的描述。
- `--destination-port,--dport[:port]` 目的端口或端口范围规范。参见 `TCP` 扩展 `--destination-port` 的描述。

## unclean (IPv4 特定)

此模块不接受选项，但尝试匹配格式异常或异常的数据。这被认为是实验性的。

## TARGET EXTENSIONS

`iptables` 可以使用扩展目标：标准发行版包含以下：

### AUDIT

`AUDIT` 目标允许为命中数据的包创建审计记录。它可以用于记录被接受、丢弃和被拒绝的数据包。更多信息请参见 `auditd(8)`。

`--type {accept|drop|reject}`

设置审计类型。示例：

```
iptables -N AUDIT_DROP
iptables -A AUDIT_DROP -j DROP
```

### CHECKSUM

`CHECKSUM` 目标允许选择性地处理损坏/旧的应用程序。对于缺少校验和的数据包计算并填充校验和。

### CLASSIFY

`CLASSIFY` 模块允许你设置 `skb->priority` 值。

`--set-class major:minor`

设置主类和次类值。即使没有 `0` 前缀，值总是被解释为十六进制。

### CLUSTERIP (IPv4 特定)

此模块允许你配置共享特定 `IP` 和 `MAC` 地址的节点集群。

`--new` 创建一个新的 `ClusterIP`。
`--hashmode mode` 指定哈希模式。可以是 `sourceip`。
`--clustermac mac` 指定 `ClusterIP MAC` 地址。
`--total-nodes num` 集群内的总节点数。
`--local-node num` 集群内的本地节点数。
`--hash-init rnd` 指定用于哈希初始化的随机种子。

### CONNMARK

`CONNMARK` 模块设置与连接相关的 `netfilter` 标记。标记宽度为 `32` 位。

`--set-xmark value[/mask]`
`--save-mark [--mask nfmask] [--ctmask]`
`--restore-mark [--mask nfmask]`

### CONNSEMARK

`CONNSEMARK` 模块将安全标记从包复制到连接，并从连接复制回包。

`+ -save`
`+ -restore`

### CT

`CT` 目标允许为包或其关联连接设置参数。

`+ -notrack`
`+ -helper name`
`+ -events event`
`+ -pexevents event`
`+ -zone id`
`+ -timeout name`

### DNAT

此目标仅在 `nat` 表的 `PREROUTING` 和 `OUTPUT` 链中有效。

`-to-destination [ipaddr--ipaddr]][port-[port]]`
`-random`
`-persistent`

### DNPT (IPv6 特定)

提供无状态的 IPv6 到 IPv6 网络前缀翻译。

`-src-pfx [prefix/length]`
`-dst-pfx [prefix/length]`

示例：

```iptables
iptables -t mangle -I POSTROUTING -s fd00::/64 -o vboxnet0 -j SNPT --src-pfx fd00::/64 --dst-pfx 2001:e20:2000:40f::/64
iptables -t mangle -I PREROUTING -i wlan0 -d 2001:e20:2000:40f::/64 -j DNPT --src-pfx 2001:e20:2000:40f::/64 --dst-pfx fd00::/64
```

`sysctl -w net.ipv6.conf.all.proxy_ndp=1`

### DSCP

此目标允许修改 IPv4 数据包 `TOS` 头中 `DSCP` 位的值。

`-set-dscp value`
`-set-dscp-class class`



## ECN (针对 IPv4 特定)

此目标允许选择性地绕过已知的 ECN 黑洞。它只能在 `mangle` 表中使用。

- `-ecn-tcp-remove`

从 TCP 头中移除所有 ECN 位。当然，它只能与 `-p tcp` 配合使用。

## HL (针对 IPv6 特定)

此用于修改 IPv6 头中的 Hop Limit（跳数限制）字段。Hop Limit 字段类似于 IPv4 中所谓的 TTL 值。设置或增加 Hop Limit 字段可能非常危险，因此应不惜代价避免。此目标仅在 `mangle` 表中有效。

不要对离开本地网络的数据包设置或增加该值！

- `-hl-set value`

将 Hop Limit 设置为 `value`。

- `-hl-dec value`

将 Hop Limit 减少 `value` 次。

- `-hl-inc value`

将 Hop Limit 增加 `value` 次。

## HMARK

类似于 MARK，即设置防火墙标记（fwmark），但标记是根据选择的数据包选择器哈希计算得的。你必须指定标记范围，并可选指定的起始偏移量，用于检查 ICMP 错误消息并用于计算哈希。

现有的选项：

- `-hmark-tuple tuple`

可能的元组成员包括：`src` 表示源地址（IPv4, IPv6 地址），`dst` 表示目的地址（IPv4, IPv6 地址），`sport` 表示源端口（TCP, UDP, DLprite, SCTP, DCC），`dport` 表示目的端口（TCP, UDP, DLprite, SCTP, DCC），`spi` 表示安全参数索引（AH, ESP），以及 `ct` 表示数据包选择器计数隧道插入的使用。

- `-hmark-mod value`（必须 > 0）

### 用于哈希计算的模数（以限制可能标记的范围）

- `-hmark-offset value`

从此处开始标记的偏移量。

对于高级用法，与其使用 `-hmark-tuple`，不如指定自定义的前缀和掩码：

### `-hmark-src-prefix cidr`

CIDR 记法下的源地址掩码。

### `-hmark-dst-prefix cidr`

CIDR 记法下的目的地址掩码。

### `-sport`

源端口掩码。

### `-dport`

目的端口掩码。

### `-spi`

SPI 掩码。

### `-proto`

协议掩码。

### `-tuple`

元组掩码。

### `-offset`

偏移值。

（注：此处根据原文结构调整对齐）

## IDLETIMER

这用于识别接口空闲一段时间。属性位于：

```
/sys/class/idletimer/<label>
```

当计时器超时时，内核向用户空间发送通知。以下选项控制计时器：

- `-timeout amount`

秒数。

- `-label string`

计时器的唯一标识符。

## LED

创建一个 LED 触发器，当特定数据包通过时，可以附加到指示灯。以下选项控制触发器：

- `-trigger-id name`

赋予 LED 的名称。实际名称将带有 "netfilter" 前缀。

- `-led-delay ms`

数据包到达时 LED 保持亮起的时间（毫秒）。默认0（尽可能闪烁）。可以给 LED 指定特殊值 `inf` 以永久开启（在这种情况下，需要手动分离并重新附加 LED 来关闭）。

- `-always-blink`

即使 LED 已经亮起，始终让 LED 闪烁。

示例：

为入站流量创建一个 LED 触发器：

```
iptables -A INPUT -p tcp --dport 22 -j LED --trigger-id ssh
```

然后附加：

## LOG

开启匹配数据包的日志。当规则设置了此选项时，Linux 内核将通过内核日志（可以使用 `dmesg(1)` 或在 syslog 读取）打印某些数据包的信息（如大多数 IP/IPv6 头部字段）。

这是一个“非终止目标”，即规则继续执行。如果你想记录拒绝的数据包，请使用两个具有相同匹配标准的独立规则，先使用 log DROP（或 REJECT）。

- `-log-level level`

日志级别，可以是系统特定的数值或缩写。可能的值（按优先级递减排序）：`emerg, alert, crit, error, warning, notice, info` 或 `debug`。

- `-log-prefix prefix`

用指定的前缀标记日志消息；最长29个字母，有助于区分日志中的消息。

- `-log-tcp-sequence`

记录 Tcp 序列号。如果日志可供用户读取，存在安全风险。

- `-log-tcp-options`

记录 TCP 数据包头中的选项。

## log-ip-options

来自 IP/IPv6 数据包头的日志选项。

## log-uid

记录生成数据包进程的用户 ID。

## MARK

此目标用于设置与数据包关联的 Netfilter 标记（mark）。例如，它可以与基于 fwmark 的路由配合使用（需要 iproute2）。如果你计划这样做，请注意，标记需要在影响路由的 mangle 链的 PREROUTING 链中设置。标记字段宽度为 32 位。

### -set-xmark value[mask]

将 mask 提供的位清零，并将 value 通过异或（XOR）到数据包标记（“nfmark”）中。如果省略 mask，则默认为 `0xFFFFFFFF`。

### -set-mark value[mask]

将 mask 提供的位清零，并将 value 通过位或（OR）到数据包标记中。如果省略 mask，则默认为 `0xFFFFFFFF`。

以下是可用助记符：

### -and-mark bits

将 nfmark 与 bits 进行二进制与（AND）运算。（set-xmark 0/invbits 的简写，其中 invbits 是 bits 的二进制取反。）

### -or-mark bits

将 nfmark 与 bits 进行二进制或（OR）运算。（set-xmark bits/bits 的简写。）

### -xor-mark bits

将 nfmark 与 bits 进行二进制异或（XOR）运算。（set-xmark bits/0 的简写。）

## MASQUERADE

此目标仅在 `nat` 表的 `POSTROUTING` 链中有效。它应该仅用于动态分配的 IP（拨号）连接：如果你有静态 IP 地址，应该使用 SNAT 目标。伪装（Masquerading）等同于映射到数据包流出接口的 IP 地址，但它具有接口掉线时忘记连接的效果。当下次拨号不太具有相同的接口地址（因此已建立的连接将丢失）时，这是正确的行为。

### -to-ports port[port]

指定要使用的源端口范围，覆盖默认的 SNAT 源端口选择启发式算法（见上文）。这仅在规则也指定了协议之一：tcp、udp、dccp 或 sctp 时才有效。

### -random

随机化源端口映射。如果使用了 `--random` 选项，则端口映射将随机化（内核 >= 2.6.21）。

Linux 内核 >= 3.7 起支持 IPv6。

## MIRROR (仅限 IPv4)

这是一个实验性演示目标，它会反转 IP 头中的源和目的字段并重新发送数据包。它仅在 INPUT、FORWARD 和 PREROUTING 链以及仅从这些链调用的自定义链中有效。注意，传出的数据包不会被任何包过滤链、连接跟踪或 NAT 查看，以避免循环和其他问题。

## NETMAP

此目标允许你将整个地址网络静态映射到另一个地址网络。它只能在 `nat` 表的规则中使用。

- `- address[/mask]` 要映射到的网络地址。结果地址将按以下方式构造：mask 中的“1”位将填充在新的“address”中。mask 中所有为0的位将从原始地址填充。

Linux 内核 >= 3.7 起支持 IPv6。

## NFLOG

此目标提供对匹配数据包的日志记录。Linux 内核会将数据包传递给已加载的后端进行日志记录。这通常与 `nftkernel_log` 作为日志后端配合使用，通过 netlink 套接字将数据包多播到指定的多播组。一个或多个用户态进程可以订阅该组以接收数据包。与 LOG 一，这是一个非终止目标，即规则将继续执行下一条。

- `- ngroup` 数据包发送到的 netlink 组（0 - 2^16-1）（仅适用于 fnnetlink_log）。默认值为 0。

- `- nlog-prefix prefix` 包含在日志消息中的前缀字符串，最长 64 个字符，用于区分日志中的消息。

- `- nlog-size size` 要拷贝到用户态的字节数（仅适用于 fnnetlink_log）。fnnetlink_log 实例可以指定自己的范围，此设置将覆盖默认值。

- `- nlog-threshold size` 在发送到用户态之前在内核内部队列的数据包数量（仅适用于 fnnetlink_log）。值越高每个数据包的开销越小，但会增加数据包到达用户态的延迟。默认值为 1。

## NFQUEUE

此目标使用 `nfnetlink_queue` 程序将数据包传递给用户态。数据包被放入由其 16 位队列号标识的队列中。用户态可以根据需要检查并修改数据包。然后用户态必须丢弃数据包或将其重新注入内核。详情请参阅 libnetfilter-queue。nfnetlink_queue 在 Linux 2.6.14 中引入。queue-balance 选项在 Linux 2.6.31 中引入，queue-bypass 在 2.6.39 中引入。

### --queue-num value

指定要使用的队列 编号。有效的队列编号为 0 到 65535。默认值为 0。

### --queue-balance value:value

指定要使用的队列范围。数据包将在给定的队列之间负载均衡。这对于多核系统非常有用：在队列 x, x+1... x+n 上启动多个用户态程序实例，并使用“queue-balance x:x+n”。

类似于取决于链的 SNAT/DNAT：它接受一个地址范围（`to 1.2.3.4-1.2.3.7`）并为每个连接为客户端提供相同的源=/目的地址。

注意：DNAT 目标——`persistent` 选项替换了 SAME 目标。

- **to ipaddr[ipaddr]**: 要映射的源地址。可以指定多次以匹配多个范围。

- **nodst**: 在选择新的源 IP 时，在计算时不使用目的 IP（destination-ip）。

- **random**: 端口映射将被强制随机化，以避免基于端口预测的攻击（内核 >= 2.6.21）。

## SEMARK

此模块用于设置与数据包关联的安全标记值，供 SELinux 等安全子系统使用。它在 `security` 表中有效（为了与旧内核后兼容，它在 `mangle` 表中也有效）。标记宽度为 32 位。

- **selctx** 安全上下文（security_context）

## SET

- 此模块从由 `ipset(8)` 定义的 IP 集中添加和删除条目。

- **add-set** setname flag[,flag...]: 将数据包的地址（或）端口（或）添加到集合。

- **del-set** setname flag[,flag...]: 从集合删除数据包的地址（或）端口（或），flag 为 `src` 或 `dst` 指定，且数量不超过六个。

- **timeout** value: 在添加条目时，使用该超时值代替集合定义中的默认值。

- **exist**: 在添加条目时，如果其已存在，则将超时值重置为指定的值或集合定义中的默认值。

使用 `-j SET` 要求提供 ipset 内核支持，对于标准内核，自 Linux 2.6.39 以来一直如此。

## SNAT

该目标仅在 `nat` 表中有效，位于 `POSTROUTING` 和 `INPUT` 链以及仅从这些链调用的自定义链中。它指定修改数据包的源地址（此连接中的后续所有数据包也将被修改），应检查相关规则。它接受以下选项：

- **to-source** `[ipaddr[ipaddr]][:port]]`: 可以指定一个新的源地址，即 IP 地址的闭区间范围。如果规则指定了以下协议之一：tcp、udp 或 sctp，则可选一个范围。如果未指定低于 512 的端口范围，则低于 512 的源端口将映射到 512 到 1023 之间的端口；在可能的情况下不会发生端口更改。对于内核 2.6.10 的内核，你可以拥有多个 `--to-source` 选项（通过地址范围或多个 `--to-source` 选项），这些地址之间会进行简单的轮询（循环中一个）。后续内核（>= 2.6.11-rc1）不具备 NAT 到多个范围的能力。如果使用了选项 `-random`，则端口映射将被随机化（内核 >= 2.6.21）。

## SNPT (IPv6 特有) 提供无状态的源到 IPv6 网络前缀翻译（如 RFC 6296 所述）。你必须在 mangle 表中使用它，而不是在 nat 表中。它接受以下：

- **src-pfx [prefix/length]**: 设置想要翻译的源前缀和长度。

- **dst-pfx [prefix/length]**: 设置要使用的目的前缀。

必须使用 DNPT 目标来取消翻译。例如：

```
iptables -t mangle -I POSTROUTING -s fd00::/64 -o net0 -j SNPT --src-pfx fd00::/64 --dst-pfx 2001:e20:2000:f/64 -j DNPT
iptables -t mangle -I PREROUTING -s wlan0 -d 2001:e20:2000:f/64 -j DNPT
```

你可能需要启用 IPv6 邻居发现：

```
sysctl -w net.ipv6.conf.all.proxy_ndp=1
```

还必须使用 Track 目标禁用翻译流的跟踪。

## TCPMSS 这允许你修改 TCP 数据包的 MSS 值，以控制该连接的最大 own（通常限制为你的出口接口的 MTU 减去 IPv4 的 40 或 IPv6 的 60）。当然，它可以与 -p tcp 配合使用。此目标用于设置 SYN 数据包的 MSS 值。

此目标用于克服那些阻塞“ICMP 分段需要”或“ICMP 包太大”的愚蠢 ISP 或服务器。此问题的症状是你的防火墙/路由器工作正常，但其后的机器永远无法交换大数据包：

1. 网页浏览器连接，然后挂起且无数据。

2. 小邮件工作正常，但大邮件挂起。

3. ssh 工作正常，但在初始握手后挂起。

解决方法：激活此选项并向你的防火墙添加如下规则：

```
iptables -t mangle -A FORWARD -p tcp --tcp-flags SYN,RST SYN TCPMSS --set-mss value
```

- **set-mss value**: 显式将 MSS 设置为指定值。如果数据包的 MSS 已经低于 value，则不会增加（从 Linux 2.6.25 开始），以避免对依赖正确 MSS 的主机产生更多问题。

- **clamp-mss-to-pmtu**: 自动将 MSS 设置为指定值（对于 IPv4 减 40，IPv6 减 60）。在 2.6.10 之前的内核中，你可以有多个 `--to-source` 选项（通过地址范围或多个 `--to-source` 选项），这些地址之间会进行简单的轮询（循环中一个）。后续内核（>= 2.6.11-rc1）不具备 NAT 到多个范围的能力。如果使用了选项 `-random`，则端口映射将被随机化（内核 >= 2.6.21）。

## TCPOSTRIP 此目标将剥离 TCP 数据包中的选项（如 NO-Ops）。因此需要添加 -p tcp 参数。可以通过 TCP 选项编号或符号名称指定。

- **strip-options option[option...]**: 剥离给定的选项。可以通过 `iptables -j TCPOSTRIP` 获取选项列表。

## TEE Tee 会复制数据包并将其重定向到网络段的另一台机器。换句话说，如果需要，它可以向 nextthop 转发。

- **gateway ipaddr**: 将复制的数据包发送到给定 IP 地址的主机。

转发 eth0 上的所有入流量：

```
iptables -t mangle -A PREROUTING -i eth0 -j TEE --gateway 2001:db8
```

## TOS 此模块设置 IPv4 头部中的服务类型字段（包括优先级位）或 ECN。IPv6 头部的 TOS 字段。注意 TOS 与 DSCP 共享位。

- **set-tos value[mask]**: 根据 mask 清零位（见下文），并将值异或到 TOS 字段中。如果省略 mask，则假设为 0FF。

- **set-tos symbol**: 在使用 TOS 目标时可以使用符号名称。它隐含 mask 为 0FF（见下文）。可以通过 `iptables -j TOS` 获取 TOS 名称列表。

可用以下助符：

- **and-tos bits**: 将 TOS 与 bits 进行逻辑与运算（用于 `--set-tos 0/invbits`，其中 invbits 是 bits 的取反。见下文）。

- **or-tos bits**: 将 TOS 与 bits 进行逻辑或运算（用于 `--set-tos bits/bits`。见下文）。

- **xor-tos bits**: 将 TOS 与 bits 进行逻辑异或（用于 `--set-tos bits/0`。见下文）。



注意：在截至 2.6.38 的 Linux 内核中，除了长期发布版 2.6.32 (>=42)、2.6.33 (>=15) 和 2.6.35 (>=14) 之外，存在一个错误，导致 IPv6 TOS 更改不符合文档且与 IPv4 版本不同。TOS 掩码指示要清零的位，因此在原始 TOS 字段之前需要取反。然而，上述内核忽略了取反，这导致了 `--set-tos` 及其助符失效。

# PROXY
该目标仅在 `mangle` 表中有效，位于 `PRROUTING` 链以及仅从该链调用的自定义链中。它将数据包重定向到本地套接而不以任何方式更改数据包头部。它还可以更改标记值，该值可用于高级路由规则。它接受三个选项：

- `on-port port`

此项指定了要使用的目的端口。这是一个必用选项，0 表示新的目的端口与原始端口相同。这仅在规则指定了 `-p tcp` 或 `-p udp` 时有效。

`-o ip` 地址

此项指定了要使用的目的地址。默认情况下，地址是进入接口的 IP 地址。这仅在规则指定了 `-p tcp` 或 `-p udp` 时有效。

`-tproxy-mark value[/mask]`

使用给定的值/掩码标记数据包标记。在这里设置的 fwmark 值可用于高级路由。（透明代理工作所需的：否则这些数据包将被转发，这可能不是你想要的）

# TRACE（跟踪）
该目标对数据包进行标记，以便内核在数据包遍历表、链、规则时，将记录每条匹配这些数据包的规则。

一个日志后端，使用字符串前缀记录：“TRACE:tablename:chainname:type:rulenum”，其中 type 可以是“rule”（表示普通规则）、“return”（表示自定义链末尾的隐式规则）和“policy”（表示内置链的策略）。它只能在 `raw` 表中使用。

# TTL (IPv4 特有)
此用于修改 IPv4 TTL 头部字段。TTL 字段决定了数据包在其生存时间超时前可以跨越多少跳数（路由器）。

设置或增加 TTL 字段可能非常危险，因此应不惜地避免。此目标仅在 `mangle` 表中有效。

**不要在离开你本地网络的数据包上设置或增加该值！**

- `-ttl set value`

将 TTL 值设置为 `value`。

- `-ttl-dec value`

将 TTL 值递减 `value` 次。

- `-ttl-inc value`

将 TTL 值增加 `value` 次。

# ULOG (IPv4 特有)
这是 NFLOG 目标的已废弃的、仅限 IPv4 的前身。它为匹配的数据包提供用户态日志记录。当为规则设置了此目标时，Linux 内核将通过 `netlink` 套接字多播发送此数据包。一个或多个用户态进程随后可以订阅各种多播组并接收数据包。像 LOG 一样，这是一个“非终止目标”，即规则遍历将继续到下一条规则。

- `-ulog-nlgroup nlgroup`

指定数据包发送到的 netlink 组 (1-32)。默认值为 1。

- `--ulog-prefix prefix`

使用指定的前缀作为日志消息的前缀；长度最多 32 个字符，用于区分日志中的消息。

- `--ulog-cprange size`

复制到用户态的字节数。值为 0 时，无论数据包大小，始终复制整个数据包。默认值为 0。

- `--ulog-qthreshold size`

在内核内部队列的数据包数量。将此值设置为例如 10，会在内核中累积十个数据包，并将它们作为一个多部分 netlink 消息发送到用户态。默认值为 1（为了向后兼容）。

# IPTABLES-RESTORE（恢复）
- `- NAME`

`iptables-restore` – 恢复 IP Tables 表

`ip6tables-restore` – 恢复 IPv6 表

# SYNOPSIS（概要）
`iptables-restore [-chntv] [-M modprobe]`

`ip6tables-restore [-chntv] [-M modprobe] [-T name]`

# DESCRIPTION（描述）
`iptables-restore` 和 `ip6tables-restore` 用于从 STDIN 指定的数据恢复 IP 和 IPv6 表。使用你的 shell 提供的 I/O 重定向从文件读取。

- `-c,--counters`

恢复所有计数器的值。

- `-h,--help`

打印帮助信息。

- `-n,--nof`

不刷新（清空）表。

- `-t,--test`

测试规则。

- `-v,--verbose`

详细输出。

- `-M,--modprobe`

指定 modprobe 路径。

- `-t,--table`

指定表名。

# BUGS（缺陷）
已知无缺陷（版本为 1）。

# AUTHORS（作者）
Harald Welte 编写了 `iptables-restore`。Andras Kis-sabo 贡献了 `ip6tables-restore`。

# SEE ALSO（另参）
`iptables-save(8)`。`iptables-HOWTO` 详细介绍了 iptables 的用法，`NAT-HOWTO` 详细介绍了 NAT，而 `netfilter-HOWTO` 详细介绍了内部机制。

# IPTABLES（iptables）
- `> NAME`

`iptables` – IPv4 数据包过滤和 NAT 管理工具

`ip6tables` – IPv6 管理工具

# SYNOPSIS（概要）
```
iptables [-t table] {-A|-C|-D} chain rule-specification
ip6tables [-t table] {-A|-C|-D} chain rule-specification
iptables [-t table] -I chain [rulenem] rule-specification
iptables [-t table] -R chain rule-specification
iptables [-t table] -D chain
iptables [-t table] -S chain [rulenem]
iptables [-t table] {-F|-L|-Z} [chain [rulenem]]
iptables [-t table] -N chain
iptables [-t table] -X chain
iptables [-t table] -P chain target
iptables [-t table] -E old-chain-name new-chain-name
rule-specification = [matches...] [target]
match = -m matchname [per-match-options]
target = -j targetname [per-target-options]
```

# DESCRIPTION（描述）
`iptables` 和 `ip6tables` 用于设置、维护和检查内核中的 IPv4 和 IPv6 数据包过滤规则。可以定义多个不同的表。每个表包含若干内置链，也可以包含自定义链。

每个链是匹配数据包的规则列表。每条规则规定了对匹配的数据包的操作。这被称为 `target`，它可以跳转到同一表中的自定义链。

# TARGETS（目标）
防火墙规则指定数据包的属性和目标。如果数据包不匹配，则检查链中的下一条规则；如果匹配，则下一条规则由目标的值指定，该值可以是自定义链的名称、`iptables-extensions(8)` 中描述的目标之一，或者是 ACCEPT、DROP 或 RETURN 特殊值。

ACCEPT 表示允许通过。DROP 表示丢弃数据包。RETURN 表示停止遍历此链，并恢复到之前（调用）链的下一条规则。如果到达内置链的末尾或匹配了内置链目标为 RETURN 的规则，则由链指定的策略决定数据包的命运。

# 表 (TABLES)
目前有五个独立的表（哪些表存在取决于内核配置选项以及存在哪些模块）。

`-t,--table` 选项指定命令应该操作的数据包匹配表。如果内核配置了自动模块加载，当该表尚不存在时，系统将尝试加载该表相应的模块。

这些表如下：

- `filter`: 默认表（如果没有传递 -t 选项）。它包含内置链 INPUT（针对目标地为本地套接字的数据包）、FORWARD（针对通过该机器路由的数据包）和 OUTPUT（针对本地生成的数据包）。

- `nat`: 当遇到创建新连接的数据包时，会查询此表。它由三个内置链组成：`PREROUTING`（在数据包进入时立即对其进行修改）、`OUTPUT`（在路由之前修改本地生成的数据包）和 `POSTROUTING`（在数据包即将发出时对其进行修改）。从内核 3.7 版本开始支持 IPv6 NAT。

- `mangle`: 此表用于特殊的数据包修改。在内核 2.4.17 之前，它有两个内置链：`PREROUTING`（在路由之前修改传入的数据包）和 `OUTPUT`（在路由之前修改本地生成的数据包）。从内核 2.4.18 版本起，还支持另外三个内置链：`INPUT`（针对进入机器自身的数据包）、`FORWARD`（针对通过该机器路由的数据包）和 `POSTROUTING`（在数据包即将发出时对其进行修改）。

- `raw`: 此表主要用于结合 NOTTRACK 配置来自连接跟踪的设备配置。它以更高的优先级在 netfilter 钩子中注册，因此被称为 ip_contract，或任何其他 ip tables 表。它提供了以下内置链：`PREROUTING`（通过任何网络接口到达的数据包）`OUTPUT`（由本地进程生成的数据包）。

- `security`: 此表用于强制访问控制（MAC）网络规则，例如由 SECMARK 和 CONNSEMARK 标签启的规则。强制访问控制是由 SELinux 等 Linux 安全模块（LSM）实现的。`security` 表在 `filter` 表之后被调用，允许 `filter` 表中的任何自律访问控制（DAC）规则在 MAC 规则生效之前生效。此表提供了以下内置链：`INPUT`（针对进入机器自身的数据包）、`OUTPUT`（在路由之前修改本地生成的数据包）和 `FORWARD`（针对通过该机器路由的数据包）。

# 选项 (OPTIONS)
`iptables` 和 `ip6tables` 识别的选项可以分为几个不同的组。

# 命令 (COMMANDS)
选项指定了要执行的操作。除非下文另有说明，命令行上只能指定其中一个。对于命令和选项名称的长版本，你只需要使用足够的字母以确保 iptables 可以将其与其他所有选项区分开。

- `-A,--append` 链规范

向所选链的末尾添加一个或多个规则。当源和/或目的名称解析为多个地址时，将为每种可能的组合添加规则。

- `-C,--check` 链规范

检查所选链中是否存在匹配规范的规则。此命令使用与 -D 相同的逻辑来查找匹配项，但不会更改现有的 iptables 配置，并使用其退出码表示成功或失败。

- `-D,--delete` 链 规则规范

从所选链中删除一个或多个规则。此命令有两个版本：规则可以指定为链中的数字（从第一条规则开始为1）或通过匹配来指定。

- `-I,--insert` 链 [rulenum] 规则规范

在指定的链中按照指定的规则编号插入一个或多个规则。因此，如果规则编号为 1，则规则将插入到链的头部。如果没有指定规则编号，这这也是默认操作。

- `-R,--replace` 链 rulenum-规范

替换所选链中的规则。如果源和/或目的名称解析为多个地址，命令将失败。规则从 1 开始编号。

- `-L,--list` [chain]

列出所选链中的所有规则。如果没有选择链，则列出所有链。像所有其他 iptables 命令一样，它适用于指定的表（默认是 filter），因此 NAT 规则通过 `iptables -t nat -L` 列出。请注意，它通常与 -n 选项一起使用以避免长时间的反向 DNS 查询。指定 -Z（清零）选项也是合法的，此时链（或链）将原子化地列出并清零。输出受给定的其他参数的影响。在运行 `iptables -L -v` 之前，具体的规则会被隐藏。

- `-S,--list-rules` [chain]

打印所选链中的所有规则。如果没有选择链，则打印所有链（格式类似于 `iptables-save`）。像所有其他 iptables 命令一样，它适用于指定的表（默认是 filter）。

- `-F,--flush` [chain]

清空所选链（如果没有给出链，则清空表中的所有链）。这等同于逐条删除所有规则。

- `-Z, --zero` [chain rulelem]

将所有链或仅针对指定的链、或仅针对链中的特定规则的数据包和字节计数器清零。指定 -L, --list 选项也是合法的，以便在清除计数器之前立即查看它们（见上文）。

- `-N, --new-chain` chain

通过给定的名称创建一个新的用户定义链。该名称不能已经存在。

- `-X,--delete-chain` [chain]

删除指定的可选用户定义链。不能有对该链的引用。如果有，你必须在删除链之前删除或替换引用该链的规则。该链必须是空的，即不包含任何规则。如果没有提供参数，它将尝试删除表中的所有非内置链。

- `-P, --policy` chain target

将链的策略设置为给定的目标。参见 TARGETS 部分以获取合法目标。内置（非用户定义）链可以拥有策略，但内置链和用户定义链都不能作为策略目标。

- `-E,--rename-chain` old-chain new-chain

将指定的链重命名为用户提供的名称。这些是外观上的，对表的结构没有影响。

- `-h`

帮助。给出命令语法的（目前非常简短的）描述。

# 参数 (PARAMETERS)
以下参数组规则规范（在 add、delete、insert、replace 和 append 命令中使用）。

- `-4, --ipv4`

此选项在 `iptables` 和 `iptables-restore` 中没有作用。如果插入了使用 -4 选项的规则（且仅在模块加载时），它将被静默忽略。任何其他用法将抛出错误。

- `-6, --ipv6`

如果插入了使用 -6 选项的规则（且仅在模块加载时），它将被静默忽略。任何其他用法将抛出错误。

- `-p, --protocol`

规则的协议。协议可以是 tcp、udp、icmp、ah、sctp 或 all。

- `-s,--source` address[][mask]

源规范。地址可以是网络名、主机名或纯 IP 地址。

- `-d,--destination` address[][mask]

目的规范。

- `-m,--match`

指定要使用的匹配项，这是一个用于测试特定属性的扩展模块。

- `-j,--jump` target

指定规则的目标；即如果数据包匹配规则，要执行的操作。

- `-g,--goto` chain

指定处理在指定的链中继续。

- `-i,--in-interface` name

接收数据包的接口名称。

- `-o,--out-interface` name

发送数据包的接口名称。

用在接口名称之前，其含义是反的。如果接口以 "+" 结尾，则任何以此名称开头的接口都将匹配。如果省略此选项，则任何接口名称均匹配。

- `-f, --fragment`

这意味着该规则仅针对分片数据包的第二个及后续 IPv4 分片。由于无法确定此类数据包的源端口或目的端口（或 ICMP 类型），数据包将不会匹配任何指定了这些内容的规则。如果 "!" 参数位于 "-f" 标志之前，规则将仅匹配头部碎片或未分片的数据包。此选项 IPv4 专用，在 ipv6 中不可。

- `-c, --set-counters` packets bytes

这允许管理员初始化规则的数据包和字节计数器（在 INSERT、APPEND、REPLACE 操作期间）。

# OTHER OPTIONS
可以指定以下附加选项：

- `-v, --verbose`

详细输出。此选项使 list 命令显示接口名称，规则选项（如果有）使用后缀 ‘K’、『M’ 或 ‘G’ 分别代表 1000、1,000,000 和 1,000,000,000 倍数（但请参见 -X 标志进行更改）。对于追加、插入、删除和替换，这将更改规则或规则的详细信息；-v 可以指定多次，可能可能输出更详细的调试语句。

- `-w, --wait` [seconds]

等待 xtables 锁。为了防止多个程序实例同时运行，程序启动时将尝试获取排斥锁。默认情况下，如果无法获取，程序将退出。此选项将使程序等待（无限期或指定的秒数），直到获取排斥锁。

- `-n, --numeric`

数字输出。IP 地址和端口号将以数字格式打印。默认情况下，程序将尝试将它们显示为主机名、网络名或服务（如果适用）。

- `-x, --exact`

扩展范围。显示数据包和字节计数器的精确值，而不是仅舍入到 K（1000 的倍数）、M（1000K 的倍数）或 G（1000M 的倍数）数字。此选项仅对 -L 命令有效。

- `--line-numbers`

列出规则时，在每条规则开头添加行号，对应该规则在链中的位置。

- `--modprobe=command`

在链中添加或插入规则时，使用命令加载任何必要的模块（目标、匹配扩展等）。

# MATCH AND TARGET EXTENSIONS
`iptables` 可以使用扩展的数据包匹配和目标模块。这些模块列表可以在 `iptables-extensions(8)` 手页中找到。

# DIAGNOSTICS
各种错误信息将打印到标准错误输出。运行正常时退出码为 0。由无效或滥用命令行参数引起的错误退出码为 2，其他错误退出码为 1。

## BUGS
有 Bug？那是什么鬼？ ;-) 你可能想查看一下 http://bugzilla.netfilter.org/

# COMPATIBILITY WITH IPCHAINS



`iptables` 与 Rusty Russell 编写的 `ipchains` 非常相似。主要区别是 `INPUT` 和 `OUTPUT` 链分别仅针对进入主机和源自本地主机的数据包进行遍历。因此，每个数据包通过这三个链中的一个（环回流量除外，它涉及 `INPUT` 和 `OUTPUT` 链）；此前，转发的数据包会通过所有三个链。

另一个主要区别是 `-i` 指输入接口，`-o` 指输出接口，两者都适用于进入 `FORWARD` 链的数据包。

各种形式的 NAT 已经分离；使用默认的 `filter` 表时，`iptables` 是一个纯数据包过滤器，带有可选的扩展模块。这应该简化之前关于 IP 伪装和数据包过滤结合的大部分混乱。因此，以下选项的处理方式不同：

`-j MASQ -S -M -L` `iptables` 中还有其他变化。

## SEE ALSO

`iptables-apply(8)`, `iptables-save(8)`, `iptables-restore(8)`, `iptables-extensions(8)`,

`packet-filtering-HOWTO` 详细介绍了 `iptables` 在数据包过滤中的用法，`NAT-HOWTO` 详细介绍了 NAT，`netfilter-extensions-HOWTO` 详细介绍了标准发行版未包含的扩展，`netfilter-hacking-HOWTO` 详细介绍了 netfilter 内部。访问 http://www.netfilter.org/。

## AUTHORS

Rusty Russell 最初编写了 `iptables`，并在早期咨询了 Michael Neuling。

Marc Boucher 通过游说在 `iptables` 中引入通用数据包选择框架，使 Rusty 放弃了 `ipnatctl`，然后编写了 `mangle` 表、`owner` 匹配、`mark` 相关功能，并在到处忙于酷炫。

James Morris 编写了 `TOS` 目标和 `tos` 匹配。

Jozsef Kadlesik 编写了 `REJECT` 目标。

Harald Welte 编写了 `ULOG` 和 `NFQUEUE`。

Netfilter Team：Marc Boucher, Martinsson, Yasuyuki Kozakai, Jozsef Kadlesik, Patrick Morris, Pablo Neira, Harald Welte, Herve Eychen。

# VERSION

本手册适用于 `iptables`。

# IPTUN

`-j MASQ -S -M -L` `iptables` 中还有其他变化。

# SYNOIS

`-w`, `--wait [seconds]`

# NOTE

如果无法获取锁，程序将退出。

## DESCRIPTION

程序将等待（无限期或指定的秒数），直到获取排斥锁。

## SEE ALSO

`iptables(8)`。

## OPTIONS

- `-n`, `--numeric`

数字输出。IP 地址和端口号将以数字格式打印。默认情况下，程序将尝试将它们显示为主机名、网络名或服务（如果适用）。

- `-x`, `--exact`

扩展范围。显示数据包和字节计数器的精确值，而不是仅舍入。

- `-v`, `--verbose`

详细输出。此选项使 list 命令显示接口名称，规则选项（如果有）使用后缀 ‘K’、『M’ 或 ‘G’ 分别代表 1000、1,000,000 和 1,000,000,000 倍数（但请参见 `-X` 标志进行更改）。对于追加、插入、删除和替换，这将更改规则或规则的详细信息；`-v` 可以指定多次，可能可能输出更详细的调试语句。

- `-h`, `--help`

显示帮助

- `-c`, `--set-counters packets bytes`

这允许管理员初始化规则的数据包和字节计数器（在 INSERT、APPEND、REPLACE 操作期间）。

- `-f`, `--fragment`

这意味着该规则仅针对分片数据包的第二个及后续 IPv4 分片。由于无法确定此类数据包的源端口或目的端口（或 ICMP 类型），数据包将不会匹配任何指定了这些内容的规则。如果 `"!"` 参数位于 `"-f"` 标志之前，规则将仅匹配头部碎片或未分片的数据包。此选项 IPv4 专用，在 ipv6 中不可。

- `-p=prefix`

使用前缀而不是 “iqn.2005-03.org。

```
iptables <args>
```

## 描述

`isciadm` 工具是一个命令行工具，允许发现和登录 iSCSI 目标，并对 open-iscsi 数据库进行访问和管理。

Open-iscsi 没有使用 iSCSI RFC 定义的“节点 (node)”术语（在 RFC 中，节点是指单个 iSCSI 初始化器或目标）。Open-iscsi 使用“节点”一词来指代目标上的门户 (portal)。

对于会话模式，使用了会话 ID (`sid`)。可以通过通过运行 `isciadm -m session -P 1` 找到会话的 sid。会话 ID 和 sysfs 路径目前不是持久的，并且部分取决于会话建立的时间。

请注意，许多节点和发现操作要求 iSCSI 守护进程 (`iscsid`) 运行。

## 选项

- `-a`,—ip=`ipaddr`

`ipaddr` 可以是 IPv4 或 IPv6。

此选项仅对 ping 子模式有效。

- `-A`,—portal-type=`[ipv4|ipv6]`

为要创建的新 flash 节点条目指定门户类型。

此选项仅对主机模式下的 flash 子模式有效，且仅用于新操作。

- `-b`,—packetsize=`packetsize`

指定 ping 数据包大小。

此选项仅对 ping 子模式有效。

- `-c`,—count=`count`

`count` 指定 ping 迭代次数。

此选项仅对 ping 子模式有效。

- `-C`,—submode=`op`

指定模式的子模式。必须是子模式的名称。

目前 `isciadm` 支持 ping 作为子模式。例如：

`isciadm -m if -I ifacename -C -a ipaddr -b packetsize -c count -i interval`

对于主机，支持 cap、flashnode 和 stats 作为子模式。例如：

`isciadm -m host -H hostno -C chap -x chap_tbl_idx -o operation`

`isciadm -m host -H hostno -C flashnode -x flashnode_idx -o operation`

`isciadm -m host -H hostno -C stats`

- `-d`,—debug=`debug_level`

打印调试信息。`debug_level` 的有效值为 0 到 8。

- `-h`,—help

显示帮助文本并退出。

- `-H`,—host=`[hostno|MAC]`

`host` 参数指定用于操作的 SCSI 主机。它可以是内核 scsi 层分配的主机号或 MAC 地址。

- `-i`,—interval=`interval`

`interval` 指定两次 ping 迭代之间的延迟。

此选项仅对 ping 子模式有效。

- `-l`,—interface=`[iface]`

`interface` 参数指定用于操作的 iSCSI 接口。iSCSI 接口 (`iface`) 定义在 `/var/lib/scsi/ifaces`。

- `-D`,—discover

使用与传入的发现类型和门户匹配的发现记录来发现目标。如果没有匹配的记录，将使用 `iscsid.conf` 中的发现设置进行创建。必须在 discoverydb 模式下传递，以指示 `isciadm` 执行发现。

此选项仅对 SendTargets 模式有效。

- `-I`,—interface

指定用于操作的接口。此选项适用于 discovery、node 和 face 模式。

- `-L`,—loginall=`[all|manual]`

对于节点模式，登录到。

- `-m`,—mode=`op`

指定模式。

- `-n`,—name=`name`

使用名称。此选项适用于 node 模式。

- `-o`,—op

指定操作。

- `-p`,—portal=`ip[:port]`

使用门户。

- `-P`,—print=`printlevel`

指定打印级别。

- `-T`,—targetname=`targetname`

使用目标名称。

- `-r`,—sid=`sysfsdir`

使用会话 ID。

- `-s`, --stats

显示会话统计。此选项与主机模式（host mode）配合使用时，显示主机统计。

- `-S`, --show

在显示记录时，不隐藏掩码值，例如 CHAP 密钥（密码）。

此选项仅适用于节点模式（node）和会话模式（session）。

- `-t`, --type=`type`

`type` 必须是 `sendtargets`（缩写为 `st`）、`slp`、`isns` 或 `or`。目前支持 `sendtargets`、`fw` 和 `ISNS`，请参见“发现类型”章节。

此选项仅适用于发现模式（discovery mode）。

- `-u`, --logout

退出指定的记录。

此选项仅适用于节点模式和会话模式。

- `-U`, --logoutall=`[all,manual,automatic]`

退出所有传入 node 或 conn 状态值的会话，或者如果传入了 all，则退出所有运行中的会话（但排除标记为 onboot 的会话）。

此选项仅适用于节点模式（在会话模式下有效但不起作用）。

- `-v`, --value=`value`

指定用于更新操作符的值。

此选项仅适用于节点模式和主机模式下的 flashnode 子模式。

- `-V`, --version

显示版本并退出。

- `-x`, --index=`index`

指定要操作的实体的索引。

此选项仅适用于主机模式下的 chap 和 flashnode 子模式。

## 发现类型

iSCSI 定义了 3 种发现类型：SendTargets、SLP 和 iSNS。

## SendTargets

一种原生 iSCSI 协议，允许每个 iSCSI 目标向启动器（initiator）发送可用目标列表。

## SLP

可选地，iSCSI 目标可以使用服务位置协议（SLP）来发布可用目标。启动器可以直接实现 SLP 查询，也可以使用单独的工具获取可用目标的信息。

## iSNS

iSNS（互联网存储名称服务）记录大型网络内的存储卷信息。要利用 iSNS，请将 iSNS 服务器的地址以及可选的端口传递给 discover 命令。

## fw

若干 NIC 和系统包含一个用于启动的微型 iSCSI 启动器。可以使用 `fw` 选项获取启动所需的值。执行 `fw` 发现不会在节点或发现数据库中存储持久记录，因为这些值存储在系统或 NIC 的资源中。

执行 `fw` 发现将像与其他方法一样打印门户（portals）。要查看 CHAP 值和启动器设置等其他设置（就像在节点模式下一样），请运行 `isciadm -m fw`。

open-scsi 中的 `fw` 支持是实验性的。设置、`isciadm` 语法和输出可能会发生变化。

`isciadm` 支持 iSNS (`isns`) 或 SendTargets (`st`) 发现类型。SLP 实现正在开发中。

## 退出状态

成功时返回 0。出错时将返回以下返回代码之一。

对多个对象（会话、记录等）进行操作的命令，`isciiadm/iscsistart` 将返回遇到的第一个错误；`isciiadm/iscsistart` 将尝试在它可以操作的对象上执行操作。如果没有找到任何对象，则返回 `ISCSI_ERR_NO_OBJS_FOUND`。

- `ISCSI_SUCCESS` - 命令执行成功。

- `ISCSI_ERR` - 通用错误代码。

- `ISCSI_ERR_SESS_NOT_FOUND` - 找不到会话。

- `ISCSI_ERR_NOMEM` - 无法为操作分配资源。

- `ISCSI_ERR_TRANS` - 连接问题导致操作失败。

- `ISCSI_ERR_LOGIN` - 通用 iSCSI 登录失败。

- `ISCSI_ERR_IDBM` - 访问/管理 iSCSI 数据库错误。

- `ISCSI_ERR_INVAL` - 无效参数。

- `ISCSI_ERR_TRANS_TIMEOUT` - 尝试连接时连接器超时。

- `ISCSI_ERR_INTERNAL` - 通用内部 iscsid/内核失败。

- `ISCSI_ERR_LOGOUT` - iSCSI 登录失败。

- `ISCSI_ERR_PDU_TIMEOUT` - iSCSI PDU超时。

- `ISCSI_ERR_TRANS_NOT_FOUND` - 内内核或 iscsid 中未加载 iSCSI 传输模块。

- `ISCSI_ERR_ACCESS` - 没有足够的操作系统权限访问 iscsid 以执行 iscsiadm 命令。

- `ISCSSI_ERR_TRANS_CAPS` - 传输模块不支持该操作。

- `ISCSSI_ERR_SESS_EXISTS` - 会话已登录。

- `ISCSSI_ERR_INVALID_MGMT_REQ` - 无效的 IPC 管理请求。

- `ISCSSI_ERR_ISNS_UNAVAILABLE` - 不支持 iSNS 服务。

- `ISCSSI_ERR_ISCSID_COMM_ERR` - 对 iscsid 的读写失败。

- `ISCSSI_ERR_FATAL_LOGIN` - 致命 iSCSI 登录错误。

- `ISCSSI_ERR_ISCSID_NOTCONN` - 无法连接到 iscsid。

- `ISCSSI_ERR_NO_OBJS_FOUND` - 未找到可执行操作的记录/目标/会话/门户。

- `ISCSSI_ERR_SYSFS_LOOKUP` - 无法在 sysfs 中查找对象。

- `ISCSSI_ERR_HOST_NOT_FOUND` - 无法查找主机。

- `ISCSSI_ERR_LOGIN_AUTH_FAILED` - 授权失败导致登录失败。

- `ISCSSI_ERR_ISNS_QUERY` - iSNS 查询失败。

- `ISCSSI_ERR_ISNS_REG_FAILED` - iSNS 注册/注销失败。

## 示例

在给定 IP 地址发现目标：`iscsiadm --mode discoverydb type sendtargets --portal 192.168.1.10 --discover` Login，必须使用发现的节点记录 ID：`iscsiadm --mode node targetname iqn.2001-05.com.doe:test --portal 192.168.1.1:3260 --login` 退出：`iscsiadm --mode node --targetname iqn.2001-05.com.doe:test --portal 192.168.1.1:3260 --logout` 列出节点记录：`iscsiadm --mode node` 显示特定节点记录的所有数据：`iscsiadm --mode node --targetname iqn.2001-05.com.doe:test --portal 192.168.1.1:3260`

- `etc/iscsi/iscsid.conf`：`iscsid` 和 `isciadm` 启动时读取的配置文件。

- `etc/iscsi/initiatorname.iscsi`：`iscsid` 和 `isciadm` 启动时读取的包含 iSCSI 启动器名称和别名的文件。

- `var/lib/iscsi/nodes`：包含节点的 Open-iSCSI 配置数据库。

- `var/lib/iscsi/targets`：此目录包含目标。

- `var/lib/iscsi/portals`：此目录包含门户。

- `-c|config`：从配置文件而非默认的 `/etc/iscsi/iscsid.conf` 读取配置。

- `-i|initiatorname`：从 iname-file 读取启动器名称，而非默认的 `/etc/iscsi/initiatorname.iscsi` 文件。

- `-f|foreground`：在前台运行 `iscsid`。

- `-d|debug`：打印调试信息。`debug_level` 的有效值为 0 到 8。

- `-u|uid`：以用户 ID 运行（默认为当前用户）。

- `-g|gid`：以用户组 ID 运行（默认为当前组 ID）。

- `-n|no-pid-file`：不写入进程 ID 文件。

- `-p|pid`：将进程 ID 写入 `pid-file` 而默认的 `/var/run/iscsid.pid`。

- `-h|help`：显示此帮助并退出。

- `-v|version`：显示版本并退出。

## OPTIONS

- `-i|initiatorname=name`

将 InitiatorName 设置为 `name`（如果不使用 iBFT 或 OF，则需要）

- `-t|targetname=name`

将 TargetName 设置为 `name`（如果不使用 iBFT 或 OF，则需要）

- `-g|tgp=N`

将门户组标签设置为 `N`（如果不使用 iBFT 或 OF，则需要）

- `-a|address=A.B.C.D`

将 IP 地址设为 `A.B.C.D`（如果不不使用 iBFT 或 OF，则需要）

- `-p|port=N`

将端口设置为 `N`（可选。默认值为 3260）

- `-u|username=N`

将用户名设为 `N`（可选）

- `-w|password=N`

将密码设为 `N`（可选）

- `-U|username_in=N`

将传入的用户名设置为 `N`（可选）

- `-W|password_in=N`

将传入的密码设置为 `N`（可选）

- `-d|debug=debug_level`

打印调试信息

- `-b|fwparam_session_connect`

使用 iBFT 或 OF 信息创建目标创建一个会话

- `-N|fwparam_network`

按照 iBFT 或 OF 的指定启动网络

- `-f|fwparam_print`

将 iBFT 或 OF 信息打印到标准输出 (STDOUT)

- `-P|param=NAME=VALUE`



将参数 `NAME` 设置为 `VALUE`。`NAME` 是节点记录或 `isscid.conf` 中的设置之一。可以传递多个参数。

- `-h|help`
显示此帮助信息并退出

- `-v|version`
显示版本并退出

## SEE ALSO
+ - `iscsiadm(8)`

## AUTHORS
Open-ISCSI project <http://www.open-iscsi.org/> Mike Christie <mchristi@redhat.com>

## iscsiuio
+ > NAME
`iscsiuio` - iSCSI 用户空间 I/O 驱动

## SYNOPSIS
```
iscsiuiu [-d][ -v]
```

## DESCRIPTION
`iscsiuio` 是适用于 Broadcom NetXtreme II BCM5706/5708/5709/5710/5771/5780/57810/5840 系列 PCI-E 万兆以太网卡 (NIC)的用户空间 I/O 驱动程序。该驱动已在 2.6.28 及以上的内核上通过测试。请参考驱动包中的 README 获取如何编译和安装驱动。参考各种 Linux 文档如何配置网络。

## DEPENDENCIES

## PARAMETERS
运行此应用程序时的参数很少。

- `-d<debuglevel>`
用于启用调试模式，调试消息将发送到标准输出。支持以下调试模式：
`DEBUG` 4 - 打印所有消息
`INFO` 3 - 打印所需的消息
`WARN` 2 - 打印警告消息
`ERROR` 1 - 仅打印关键错误

- `-f`
启用前台模式，使此程序进入后台。

- `-v`
打印版本号。

- `-p<pidfile>`
使用 `pidfile`（默认 `/var/run/iscsiuio.pid`）

- `-h`
显示此帮助信息并退出。

## AUTHOR
Benjamin Li - benli@broadcom.com
Eddie Wai - eddie.wai@broadcom.com

## ISOSIZE
+ > NAME
`isosize` - 输出 iso9660 文件系统的长度

## SYNOPSIS
```
isosize [options] iso9660_image
```

## DESCRIPTION
`isosize` 输出指定文件中包含的 iso9660 文件系统的长度。该可以是普通文件或块设备（例如 `/dev/sr0`）。在没有任何选项（且没有错误）的情况下，它将以字节为单位输出 iso9660 文件系统的大小。存放 iso9660 文件系统的文件（或块设备）的大小可能略大于设备的实际大小。

- `-x`, `--sectors`
以人类可读的形式显示块计数和块大小。输出使用“sectors”（区块）一词代替“blocks”（块）。

- `-d`, `--divisor`
仅在未给出 `-x` 时生效。显示的值（如果没有错误）是 iso9660 文件大小（字节）除以该数字的结果。因此，如果数字是块大小，那么显示的值将是块计数。其原因之一是，CD 刻录机允许在 iso9660 镜像末尾添加“用尽”区块。

## AVAILABILITY
`isosize` 命令是 util-linux 软件包的一部分，可在 Linux 归档中获取

## IW
+ > NAME
`iw` - 显示/操作无线设备及其配置

## SYNOPSIS
```
iw [ OPTIONS ] { help [ command ] | OBJECT }
OBJECT := { dev | phy | reg }
OPTIONS := { --version | --debug }
```

## OPTIONS
- `-version`
打印版本信息并退出。

- `-debug`
启用 netlink 消息调试。

## IW - COMMAND SYNTAX
### OBJECT
- `dev <interface name>`
网络接口。

- `phy <phy name>`
无线硬件设备（通过名称）。

- `phy<phy index>`
无线硬件设备（通过索引）。

- `reg`
监管代理。

### COMMAND
指定在对象上执行的操作。可能的动作取决于对象类型。`iw help` 将打印所有支持的命令，而 `iw command` 将打印所有匹配命令的帮助信息。

## SEE ALSO
`ip(8)`, `crda(8)`, `regdbdump(8)`, `regulatory.bin(5)`
http://wireless.kernel.org/en/users/Documentation/iw

## KBDRATE
+ > NAME
`kbdrate` - 重置键盘重复速率和延迟时间

## SYNOPSIS
```
kbdrate [ -s ] [ -r rate ] [ -d delay ]
```

## DESCRIPTION
`kbdrate` 用于更改键盘重复速率和延迟时间。延迟是按键按下到开始重复之前的时间。在不带任何选项的情况下使用 `kbdrate` 将基于 Intel 和 M68K 的系统的速率重置为每秒 10 个字符 (cps)，延迟重置为 250 毫秒 (ms)。这些是 IBM 的默认值。在基于 SPARC 的系统上，它将速率重置为 20 cps，延迟为 200 ms。

## OPTIONS
- `-s` 静音。不打印任何消息。
- `-r rate`
将键盘重复速率更改为 `rate` cps。对于 Intel 系统，允许范围是 2.0 到 30.0 cps。只有某些特定的值是可能的，程序将选择最接近指定值的可能值。可能的值（以每秒字符计）如下：2.0, 2.1, 2.3, 2.5, 3.0, 2.7。
- `-d delay`
将延迟更改为 `delay` 毫秒。对于 Intel 系统，允许范围是 250 ms 到 1000 ms，步长 25 ms。对于 SPARC 系统，可能的值在 10 ms 到 1440 ms 之间，间隔 10 ms。
- `-V` 显示版本号并退出

#### UGS
并非所有键盘都支持所有速率。
并非所有键盘的映射方式都相同。
在 Gateway 上设置重复速率无效。如果有 Gateway 用户知道如何编写键盘，请发送邮件至 util-linux@uio.no。
所有这些都取决于架构。现在 `kbdrate` 首先尝试 `KDKBDREP` 和 `KIOCRATE` ioctl（前者通常在 m68k 机器有效，后者用于 SPARC）。当这些 ioctl 失败时，假设使用 i386 的 ioport 接口。

## FILES
```
/etc/rc.local /dev/port /dev/kbd
```

## KDUMP
+ > NAME
`kdump` - 这是一个占位符，直到编写真正的手册页

## SYNOPSIS
```
kdump [options] start_address...
```

## DESCRIPTION
`kdump` 还没有手册页。

## AUTHOR
`kdump` 由 Eric Biederman 编写。
此手册页由 Khalid Aziz <khalid.aziz@hp.com> 编写，供 Debian 项目（但也可供使用）。

## KDUMPCTL
### NAME
`kdumpctl` - `kdump` 的控制接口

## SYNOPSIS
`kdumpctl COMMAND`

## DESCRIPTION
`kdumpctl` 用于检查或控制 `kdump` 服务。在大多数情况下，您应该使用 `systemctl` 来启动/停止/启用 `kdump` 服务。然而，`kdumpctl` 为调试提供了更详细的信息，并提供了设置 ssh 密钥认证的辅助。

## COMMANDS
- `start`
启动服务。
- `stop`
停止服务。
- `status`
打印 `kdump` 服务的当前状态。如果 `kdump` 未正常运行，则返回非零值。
- `restart`
等同于 `start; stop`。
- `propagate`
帮助为 ssh 存储设置密钥认证，因为在 `kdump` 期间无法使用密码认证。
- `showmem`
以兆字节为单位打印为崩溃内核（crash kernel）保留内存内存。

## SEE ALSO
`kdump.conf(5)`, `mkdumprd(8)`

## KERNEL-INSTALL
### NAME
`kernel-install` -向 `/boot` 添加或删除内核和 initramfs 镜像

## SYNOPSIS
```
kernel-install COMMAND KERNEL-VERSION [KERNEL-IMAGE]
```

## DESCRIPTION
`kernel-install` 用于向 `/boot` 安装和删除内核以及 initramfs 镜像。
`kernel-install` 将执行位于 `/usr/lib/kernel/install.d/` 目录和本地管理目录 `/etc/kernel/install.d/` 中的文件。所有文件都会被统一排序并按字典顺序执行，无论它们位于哪个目录。然而，文件名相同的文件会互相替换。`/etc/kernel/install.d/` 中的文件优先级高于 `/usr/lib/kernel/install.d/` 中的同名文件。这可以在需要时用本地文件覆盖系统提供的可执行文件；如果 `/etc/kernel/install.d/` 中有一个与 `/usr/lib/kernel/install.d/` 中可执行文件同名的符号链接并指向 `/dev/null`，则完全禁用该执行文件。执行文件必须具有“.install”扩展名；其他扩展名将被忽略。

## COMMANDS
支持以下 `KERNEL-VERSION KERNEL-IMAGE`：
- `add KERNEL-VERSION KERNEL-IMAGE`
`kernel-install` 创建目录 `/boot/MACHINE-ID/KERNEL-VERSION/`，并带参数调用每一个 `/usr/kernel/install.d/*.install` 和 `/etc/kernel/install.d/*.install`
`add KERNEL-VERSION /boot/MACHINE-ID/KERNEL-VERSION/`
`kernel-install` 插件 `50-depmod.install` 会移除 `KERNEL-VERSION` 的 depmod。
`kernel-install` 插件 `90-loaderentry.install` 将 `KERNEL-IMAGE` 拷贝到 `/boot/MACHINE-ID/KERNEL-VERSION/linux`。它还会根据 `/boot/loader/entries/MACHINE-ID-KERNEL-VERSION.conf` 中的引导程序规范创建引导器条目。条目的标题是 `/etc/os-release` 或 `/usr/lib/os-release` 中指定的 `PRETTY_NAME` 参数（如果前者缺失），或者在未设置时为“Linux KERNEL-VERSION”。如果在 linux 文件旁边找到 initrd 文件，则会将 initrd 添加配置中。
- `remove KERNEL-VERSION`
带参数调用每一个 `/usr/kernel/install.d/*.install` 和 `/etc/kernel/install.d/*.install`
`remove KERNEL-VERSION /boot/MACHINE-ID/KERNEL-VERSION/`
`kernel-install` 随后会移除整个目录 `/boot/MACHINE-ID/KERNEL-VERSION/`。
`kernel-install` 插件 `90-loaderentry.install` 会移除文件 `/boot/loader/entries/MACHINE-ID-KERNEL-VERSION.conf`。

## EXIT STATUS
如果每个执行文件返回 0，则返回 0，否则返回非零失败代码。

## FILES
- `/usr/lib/kernel/install.d/*.install /etc/kernel/install.d/*.install`
由 `kernel-install` 执行的插拔文件。
- `/etc/kernel/cmdline /proc/cmdline`
文件 `/etc/kernel/cmdline` 的指定要使用的内核命令行。如果该文件不存在，则使用 `/proc/cmdline`。
- `/etc/machine-id`
文件内容指定机器标识 `MACHINE-ID`。
- `/etc/os-release /usr/lib/os-release`
文件内容指定操作系统的标题 `PRETTY_NAME`。

## SEE ALSO
`machine-id(5)`, `os-release(5)`, `Boot loader specification(5)`.

## NOTES
1. 引导程序规范
http://www.freedesktop.org/wiki/Specifications/BootLoaderSpec

## kexec
### NAME
`kexec` - 直接进入内核

## SYNOPSIS
```
/sbin/kexec [-v] [-f] [-h] [-l] [-p] [-t=type] [-u] [-x] [--mem-min=addr] [--mem-max=addr] [--entry=addr] [--load-preserve-context] [--load-jump-back-helper] [--reuseinitrd] 
```

## DESCRIPTION
`kexec` 是一个系统调用，允许您加载并启动到另一个内核。注意，它跳过了 BIOS/UEFI 引导程序。这对于快速重启或崩溃转储（crash dumping）有用。

## 使用
使用 `kexec` 包括：
(1) 将内核加载到当前内核，以及
(2) 实际重启到加载的内核。

## EXAMPLE
例如，如果你想要重启的内核镜像 `/boot/vmlinux`，`/proc/cmdline` 的内容为 `root=/dev/da1`，且 initrd 的路径为 `/boot/initrd`，则可以使用以下命令加载内核：
```
kexec -l /boot/vmlinux --append=root=/dev/da1 --initrd=/boot/initrd
```
加载此内核后，可以使用以下命令随时启动：
```
kexec -e
```

## OPTIONS
- `-d (--debug)`
启用调试消息。
- `-e (--exec)`
运行当前加载的内核。注意，它将重启到加载的内核，而不调用 `shutdown(8)`。
- `-f (--force)`
强制立即执行 `kexec` 调用，不调用 `shutdown(8)`（与不带任何参数的默认操作相反）。此选项在一次调用中执行 `-l` 和 `-e` 相同的操作。
- `-h (--help)`
为 `kexec` 打开帮助文件。
- `-l (--load)`
将指定的内核加载到当前内核中。
- `-p (--load-panic)`
加载新内核以便在崩溃（panic）时使用。
- `-t (--type=type)`
指定新内核为这种类型。
- `-u (--unload)`
卸载当前的 `kexec` 目标内核。如果正在卸载捕获内核，则在使用 `-u` 时指定 `-p`。
- `-v (--version)`
返回已安装工具程序版本号。
- `-x (--no-ifdown)`
关闭运行的内核，但在重新加载时恢复接口。（如果使用此选项，必须最后指定。）
- `--mem-min=addr`
指定加载代码的最低内存地址 `addr`。
- `--mem-max=addr`
指定加载代码的最高内存地址 `addr`。
- `--entry=addr`
指定跳转回地址。（它不是跳转回或保留上下文）
- `--load-preserve-context`
加载新内核并在 `kexec` 期间保留当前内核的上下文。
- `--load-jump-back-helper`
加载辅助镜像以回到原始 `kexec`。
- `--reuseinitrd`
复用首次启动时的 initrd。

# 支持的内核文件类型及选项

## Reboot-x86
- `-args-elf`: 传递 ELF 启动备注。
- `-args-linux`: 传递 Linux 内核风格选项。
- `-real-mode`: 使用内核的实模式入口点。

## elf-x86
- `-append=string`: 将字符串追加到内核命令行。
- `-command-line=string`: 将内核命令行设置为字符串。
- `-reuse-cmdline`: 使用正在运行系统的命令行。当加载 panic 内核（崩溃内核）时，它会自动剥离 crashkernel 参数。`BOOT_IMAGE` 参数也会被剥离。
- `-initrd=file`: 使用文件作为内核的初始内存盘（ramdisk）。
- `-ramdisk=file`: 使用文件作为内核的初始内存盘（ramdisk）。

## bzImage-x86
- `-append=string`: 将字符串追加到内核命令行。
- `-command-line=string`: 将内核命令行设置为字符串。
- `-reuse-cmdline`: 使用正在运行系统的命令行。当加载 panic 内核（崩溃内核）时，它会自动剥离 crashkernel 参数。`BOOT_IMAGE` 参数也会被剥离。
- `-initrd=file`: 使用文件作为内核的初始内存盘（ramdisk）。
- `-ramdisk=file`: 使用文件作为内核的初始内存盘（ramdisk）。
- `-real-mode`: 使用实模式入口点。

## multiboot-x86
- `-command-line=string`: 将内核命令行设置为字符串。
- `-reuse-cmdline`: 使用正在运行系统的命令行。当加载 panic 内核（崩溃内核）时，它会自动剥离 crashkernel 参数。`BOOT_IMAGE` 参数也会被剥离。
- `-module=mod arg1 arg2 ...`: 加载带有命令行参数 `arg1 arg2 ...` 的模块 `mod`。此参数可以指定多次。

## 架构选项
- `- console-serial`: 启用串口控制台。



- - `console-vga`: 启用 VGA 控制台。
- - `elf32-core-headers`: 准备 ELF32 格式的核心头文件。
- - `elf64-core-headers`: 准备 ELF64 格式的核心头文件。
- - `reset-vga`: 尝试重置标准 VGA 设备。
- - `serial=port`: 指定调试输出的串口端口。
- - `serial-baud=baud_rate`: 指定串口的波特率。

## KEY.DNS_RESOLVER

- > 名称

`key.dns_resolver` - 用于 `request-key` 的回调，以处理 `dns_resolver` 密钥

## 摘要

```
/sbin/key.dns_resolver <key> /sbin/key.dns_resolver -D [-v] <keydesc> <calloutinfo>
```

## 描述

此程序由 `request-key` 代表内核调用，当内核服务（如 NFS、CIFS 和 AFS）想要执行主机名查找且内核没有缓存密钥时。它通常不预期被直接调用。

可以在调试模式下，通过在命令行上传递 `-D` 标志来测试其功能。要使此功能工作，必须提供密钥描述和回调信息（callout information）。通过提供一个或多个 `-v` 标志可以增加详细程度。

# 错误

所有错误将记录在 `syslog` 中。

## 参见

`request-key(8)`, `request-key.conf(5)`

## KILLALL5

- > 名称

`killall5` — 向所有进程发送信号。

## 摘要

```
killall5 -signalnumber [-o omitpid[,omitpid..]] [-o omitpid[,omitpid..]]
```

## 描述

**killall** 是 SystemV 的 killall 命令。它向内核线程和自身会话中的进程之外的所有进程发送信号，因此它不会杀死运行该脚本的 shell。它的主要（唯一）用途是在位于 `/etc/init.d` 目录下的 **rc** 脚本。

## 选项

- -o `omitpid`: 告诉 `killall` 忽略具有该 PID 的进程。

## 注意事项

`killall` 也可以作为 `pidof` 被调用，它仅仅是指向 `killall` 程序的（符号）链接。

## 退出状态

如果程序杀死了进程，则返回零。如果没有进程被杀死，则返回 2；如果无法找到任何进程（`/proc/` 缺失），则返回 1。

## 参见

`halt(8)`, `reboot(8)`, `pidof(8)`

## 作者

Miquel Smooreburg, miquels@cron.nl

## KMOD

- > 名称

`kmod` - 管理 Linux 模块的程序

## 摘要

```
kmod [OPTIONS...] [COMMAND] [COMMAND_OPTIONS...]
```

## 描述

`kmod` 是多功能二进制文件，实现了用于控制 Linux 模块的程序。大多数用户只会通过其他名称运行它。

## 选项

- `-V` `--version`: 显示程序版本并退出。
- `-h` `--help`: 显示帮助信息。

## 命令

- `help`: 显示帮助信息。
- `list`: 列出当前加载的模块。
- `static-nodes`: 输出运行内核的模块提供的静态设备节点。

## 版权

本手册页版权所有 2014, Marco Dimitri。由 Lucas Dei 等人维护。

## 参见

`lsmod(8)`, `rmmod(8)`, `insmod(8)`, `modinfo(8)`, `modprobe(8)`, `depmod(8)`

## 作者

Lucas De Marchi <lucas.marchi@gmail.com> 开发者

## KPARTX

- > 名称

`kpartx` - 从分区表创建设备映射

## 摘要

```
kpartx [-a | -d | -l] [-v] whole disk
```

## 描述

该工具源自 `util-linux-partx`，读取指定设备的分区表并创建设备映射。它在热插时调用。

## 选项

- `-a`: 添加分区映射
- `-r`: 只读分区映射
- `-d`: 删除分区映射
- `-u`: 更新分区映射
- `-l`: 列出已添加的分区映射
- `-p`: 设置分区编号
- `-f`: 强制创建映射；覆盖 no_partitions 功能
- `-g`: 强制分区表 (GPT)
- `-v`: 详细模式
- `-s`: 同步模式。直到分区创建

## 示例

挂载磁盘镜像中的所有分区：

```
kpartx -av disk.img
```

这将输出如下行：

```
loop3p1 : 2096472 /dev/loop3
```

`loop3p1` 是 mapper 下的设备名称，你可以使用它，例如进行 fsck：

```
fsck /dev/mapper/loop3
```

当你完成后，你需要移除设备：

```
kpartx -d disk.img
```

## 参见

`multipath(8)` `multipathd(8)` `hotplug(8)`

## 作者

本手册页由 Patrick Caulfield 为 Debian 项目汇编。来自 multipath 作者 Christophe Varqui <christophe.varoqui@opensvc.com> 等人的。

## LASTLOG

- > 名称

`lastlog` - 报告所有用户或指定用户的最近登录

## 摘要

```
lastlog [options]
```

## 描述

`lastlog` 格式化并打印登录日志文件 `/var/log/lastlog` 的内容。将打印登录名、端口和最后登录时间。默认（无标志）会按照 `/etc/passwd` 中的顺序打印 lastlog 。

## 选项

适用于 `lastlog` 命令的选项有：

- `-b` `--before DAYS`: 只打印早于 DAYS 的最后登录记录。
- `-h`, `--help`: 显示帮助信息并退出。
- `-R`, `--root CHROOT_DIR`: 应用 `CHROOT_DIR` 目录中的更改并使用该目录下的配置文件。
- `-t`, `--time DAYS`: 打印晚于 DAYS 的最后登录记录。
- `-u`, `--user LOGIN|RANGE`: 打印指定用户对应的 lastlog 记录。可以通过登录名、数值用户 ID 或用户范围指定用户。用户范围可以使用最小值和最大值 (`UID_MIN-UID_MAX`)、最大值 (`-UID_MAX`) 或最小值 (`UID_MIN-`) 指定。

如果用户从未登录，将显示 ** Never logged in** 代替端口和时间。

只显示系统当前用户的条目。可能存在以前删除的用户的条目。

## 注意

`lastlog` 文件是一个包含每个用户最后登录信息的数据库。你不应该对它进行轮转（rotate）。它是一个稀疏文件，因此它在磁盘上的实际大小通常比“ls -l”显示的要小得多（如果你在 passwd 中有具有高 UID 的用户，这可能会指示一个非常大的文件）。你可以使用“ls -s”显示其真实大小。

## 文件

`/var/log/lastlog`

以前用户登录的时间记录数据库。

# 注意事项

UID 编号之间存在较大的间隙会导致 `lastlog` 程序运行时间更长，且屏幕上没有输出（即：如果 `lastlog` 数据库中没有 UID 范围介于 170 和 800 之间的用户条目，`lastlog` 在处理 UID 为 171-799 的条目时看起来像卡住了一）。

# LD.SO

**> 名称**

`ld.so`, `ld-linux.so*` - 动态链接器/加载器

## 概要

动态链接器可以通过两种方式运行：通过运行某些动态链接的程序或库间接运行（在这种情况下，无法向动态链接器传递命令行选项，且在 ELF 情况下，将执行存储在程序 `.interp` 段的动态链接器），或者通过直接运行：

```
/lib/ld-linux.so.* [OPTIONS] [PROGRAM [ARGUMENTS]]
```

## 描述

`ld.so` 和 `ld-linux.so*` 程序查找并加载程序所需的共享库，准备程序运行环境，然后运行它。

除非在编译期间向 `ld(1)` 提供了 `-static` 选项，否则 Linux 二进制文件需要动态链接（在运行时进行链接）。

`ld.so` 程序处理二进制文件（这是一种以前使用的格式）；`ld-linux.so*` 处理 ELF（lib5 使用 `/lib/ld-linux.so.1`，glibc2 使用 `/lib/ld-linux.so.2`），多年来大家都在使用它。其他行为相同，并使用相同的支持文件和程序 `ldd(1)`、`ldconfig(8)` 以及 `/etc/ld.so.conf`。

在解析库依赖时，动态链接器首先检查依赖字符串查看其是否包含斜杠（如果在链接时指定了包含斜杠的库路径，可能会发生这种情况）。如果发现斜杠，则依赖字符串被解释为（相对或绝对）路径，并使用该路径加载库。

如果库依赖不包含斜杠，则按以下顺序进行搜索：

- （仅限 ELF）如果二进制文件中存在 `DT_RPATH` 动态段属性且不存在 `DT_RUNPATH` 属性，则使用其中的目录。`DT_RPATH` 已被弃用。
- 使用环境变量 `LD_LIBRARY_PATH`。除非可执行文件设置为 set-user-ID/set-group-ID 二进制，这种情况下会被忽略。
- 如果二进制文件中存在 `DT_RUNPATH` 动态段属性，则使用其中的目录。
- 来自缓存 `/etc/ld.so.cache`，其中包含了之前在扩展库路径中找到的候选库编译列表。然而，如果二进制文件是用 `-z nodeflib` 选项链接的，将跳过默认库路径。安装在硬件能力目录（见下文）中的库优于其他库。
- 在默认路径 `/lib`，然后是 `/usr/lib`。如果二进制文件是用 `-z nodeflib` 选项链接的，则将跳过此路径。

# Rpath 令牌扩展

`ld.so` 理解 rpath 规范（`DT_RPATH` 或 `DT_RUNPATH`）中的某些字符串；这些字符串将按如下方式替换：

`$ORIGIN` (或等效的 `${ORIGIN}`)

扩展为包含应用程序可执行文件的目录 somedir。因此，位于 `somedir/app` 的应用程序可以如下编译编译：

```bash
gcc -Wl,-rpath,'$ORIGIN/../lib'
```

以便无论 somedir 在目录层次中处于什么位置，它都能在 `somedir/lib` 中找到关联共享库。这有助于创建“开箱即用”的应用程序，这些程序不需要安装到特殊目录，而是可以解压到任何目录并仍然找到它们自己的共享库。

`$LIB` (或等效的 `${LIB}`)

根据架构扩展为 lib 或 lib64（例如，在 x86-64 上扩展为 lib64，在 x86-32 上扩展为 lib）。

`$PLATFORM` (或等效的 `${PLATFORM}`)

扩展为对应于主机系统处理器种的字符串（例如“x86_64”）。在某些架构上，Linux 内核不向动态链接器提供平台字符串。该字符串的值来自辅助向量中的 `AT_PLATFORM` 值（见 `getauxval(3)`）。

## 选项

- `-list`
- 列出所有依赖项及其解析方式。
- `-verify`
- 验证程序是动态链接的，且此动态链接器可以处理它。
- `-library-path PATH`
- 使用 `PATH` 代替 `LD_LIBRARY_PATH` 环境变量（见下文）。
- `-inhibit-rpath`
- 忽略 RPATH 和 RUNPATH
- `-audit`
- 在程序链接时加载一组审计库列表。

# 硬件能力

某些库需要所有 CPU 都不具备的硬件功能。动态链接器检查机器的硬件能力并选择最合适的库。支持以下内容：

- Alpha
- MIPS
- PowerPC
- SPX
- SPARC
- s390
- x86 (32位)

# 环境

存在重要的环境变量。

# LD_ASSUME_KERNEL

(glibc 2.2) 每个共享库都可以告知动态链接器其所需的最小 ABI 版本。（此要求编码在 ELF note 中，可以通过 `readelf -n` 查看。）在运行时，动态链接器确定运行内核的 ABI，并拒绝加载超过该 ABI 的库。

`LD_ASSUME_KERNEL` 可让动态链接器假设运行在不同内核 ABI 的系统上。例如，以下命令会导致动态链接器在加载共享库时假设运行在 Linux 2.2.5 上

```bash
$ LD_ASSUME_KERNEL=2.2.5 ./myprog
```

在提供具有不同内核 ABI要求的共享库多个系统中，`LD_ASSUME_KERNEL` 可用于选择使用的库版本。历史上，`LD_ASSUME_KERNEL` 最常用的用法是在同时提供 LinuxThreads 和 NPTL（通常默认）的系统上手动选择旧的 LinuxThreads 线程实现；请使用 `pthreads(7)`。

# LD_BIND_NOW

(glibc 2.1.1) 如果设置为非空字符串，会导致动态链接器在程序启动时解析所有符号，而不是将函数调用解析推迟到引用它们。这在使用调试器时有用。

# LD_BIND_NOT

(glibc 2.2) 在解析符号时不更新全局偏移表 (GOT) 和过程链接表 (PLT)。

# LD_LIBRARY_PATH

用于执行时搜索 ELF 库的冒号分隔目录列表。类似于 `PATH` 环境变量。在 set-user-ID 和 set-group-ID 程序中被忽略。

# LD_PRELOAD

一个在加载所有库之前加载的额外的、用户指定的 ELF 库列表。列表项可以用空格或冒号分隔：这可以用于选择性地覆盖其他共享库中的函数。库的搜索使用描述规定的规则。对于 set-user-ID/set-group-ID ELF 二进制文件，包含斜杠的预加载名称会被忽略，并且当库文件启用了 set-user-ID 权限位时才会加载标准搜索目录中的库。

(仅限 ELF) 设置为非空字符串会导致程序列出其动态库依赖项，类似于 `ldd(1)`，而不是正常运行。

然后还有更多或较少晦涩的变量，许多已过时或仅供内部使用。

# LD_AOUT_LIBRARY_PATH

(glibc 2.25) 仅用于二进制程序的 `LD_LIBRARY_PATH` 版本。旧版本的 `ld-linux.so.1` 支持 `_LIBRARY_PATH`。

# LD_AOUT_PRELOAD

(glibc 2.25) 仅用于二进制程序的 `LD_PRELOAD` 版本。旧版本的 `ld-linux.so.1` 支持 `_PRELOAD`。

# LD_AUDIT

(glibc 2.4) 一个由冒号分隔的列表，指定在发生其他符号绑定之前加载的 ELF 共享对象（例如，加载新库、解析符号或从另一个共享对象调用符号）。这些库可用于审计动态链接器的操作。详情请参见 `rtld-audit(7)`。审计接口与 Solaris 的 `Linker and Libraries` 手册中的 `Runtime Linker Auditing` 章节描述的基本。`LD_AUDIT` 对于 set-user-ID/set-group-ID 二进制文件被忽略。

# LD_BIND_NOT

(glibc 2.1.9) 在解析符号后不更新 GOT（全局偏移表）和 PLT（过程链接表）。

# LD_DEBUG

(glibc 2.1) 输出关于动态链接器的详细调试信息。如果设置为 `all`，则打印所有调试信息；设置为 `help`，则打印关于环境变量可以指定的类别的帮助信息。从 glibc 2.3.4 开始，`LD_DEBUG` 对于 set-user-ID/set-group-ID 二进制文件被忽略。

# LD_DEBUG_OUTPUT

(glibc 2.1) 写入 `LD_DEBUG` 输出的文件。默认是标准输出。如果变量未定义或定义为空字符串，则默认值为 `/var/tmp`。`LD_DEBUG_OUTPUT` 对于 set-user-ID 和 set-group-ID 程序被忽略，尽管它们使用了 `/var/profile`。

# LD_DYNAMIC_WEAK

(glibc 2.1.9) 允许符号被覆盖（恢复到旧 glibc 行为）。出于安全考虑，从 glibc 2.3.4 开始，`LD_DYNAMIC_WEAK` 对于 set-user-ID/set-group-ID 二进制文件被忽略。

# LD_HWCAP_MASK

(glibc 2.1) 硬件能力的掩码。

# LD_KEEPDIR

(仅限 ELF)(glibc 5) 不要忽略要加载的库名称中的目录。强烈建议使用此选项。

# LD_WARN

(仅限 ELF)(libc5) 抑制关于次版本号不兼容的库的警告。

# LD_ORIGIN_PATH

(glibc 2.1) 查找二进制文件的路径（非 set-user-ID 程序）。出于安全考虑，从 glibc 2.4 开始，`LD_ORIGIN_PATH` 对于 set-user-ID/set-group-ID 二进制文件被忽略。

# LD_POINTER_GUARD

(glibc 2.4) 设置为 0 以禁用指针保护。任何其他值均启用保护，这也是默认值。指针保护是一种安全机制，对存储在可写程序内存中的指针（由 `setjmp(3)` 保存的返回地址或 glibc 内部使用的函数指针）进行半随机管理，使得攻击者在发生缓冲区溢出或崩溃攻击时难以劫持这些指针。

# LD_PROFILE

(glibc 2.1) 要分析的共享对象，可以通过路径名或 soname 指定。分析输出被写入名为 `$LD_PROFILE_OUTPUT/$LD_PROFILE.profile` 的文件中。

# LD_PROFILE_OUTPUT

(glibc 2.1) 写入 `LD_PROFILE` 输出的目录。如果变量未定义或定义为空字符串，则默认值为 `/var/tmp`。`LD_PROFILE_OUTPUT` 对于 set-user-ID 和 set-group-ID 程序被忽略，尽管它们使用了 `/var/profile`。

# LD_SHOW_AUX



(glibc 2.1) 显示内核内核的辅助数组。出于安全考虑，从 glibc 2.3.5 开始，`LD_SHOW_AUX` 对于 set-user-ID/set-group-ID 二进制文件被忽略。

# `LD_USE_LOAD_BIAS`

默认情况下（即变量未定义），可执行文件和预链接对象将具有其依赖库的基地址，而非预链接的位置无关可执行文件（PIE）和共享对象将不遵循。如果 `LD_USE_LOAD_BIAS` 定义了值，则可执行文件和 PIE 都遵循基地址。如果 `LD_USE_LOAD_BIAS` 定义为 0，则可执行文件和 PIE 都不遵循基地址。此变量被 set-user-ID 和 set-group-ID 程序忽略。

# `LD_VERBOSE`

(glibc 2.1) 如果设置了 `LD_TRACE_LOADED_OBJECTS` 环境变量，设置为非空字符串，则输出关于程序的符号版本信息。

# `LD_WARN`

(仅限 ELF)(glibc 自 2.1.3 起) 如果设置为非空字符串，则对未解析的符号发出警告。

# `LD_ARGV`

(仅限 ELF) 设置为非空字符串会导致程序列出其动态库依赖，类似于 `ldd(1)`，而不是正常运行。

# 另请

`inputattach(1)`, `ttys(4)`

## 作者

Tilman Schmidt (`tilman@imap.cc`)

# 可用性

`ldconfig` 命令是 util-linux 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# `LDCONFIG`

## 名称

`ldconfig` - 配置动态链接器运行时绑定

## 概要

```
/sbin/ldconfig [ -nNvXV ] [ -f conf ] [ -C cache ] [ -r root ] directory ...
```

```
/sbin/ldconfig -l [ -v ] library ...
```

```
/sbin/ldconfig -p
```

## 说明

`ldconfig` 为命令行、`/etc/ld.so.conf` 文件以及受信任目录（`/lib` 和 `/usr/lib`）中找到的最新的共享库创建必要的链接和缓存。该缓存由运行时链接器 `ld.so` 或 `ld-linux.so` 使用。`ldconfig` 在确定哪些版本的链接应该更新时，会检查它遇到的动态库的头文件和文件名。

`ldconfig` 将尝试根据库链接到了哪些 C 库（如果有的话）来推断 ELF 库的类型（即 libc5 或 libc6/glibc）。

某些现有库不包含足够的信息来推断其类型。因此，`etc/ld.so.conf` 文件允许指定预期的类型。这仅用于我们无法确定的 ELF 库。格式为“dirname=TYPE”，其中 TYPE 可以是 libc4、libc5 或 libc6。（此语法在命令行也有效）。不允许出现空格。另请参见 -p 选项。`ldconfig` 通常应由超级用户运行，因为它可能需要对某些 root 拥有的目录和文件写入权限。

## 选项

- `-v` 详细模式。打印当前版本号、扫描时每个目录的名称以及创建的任何链接。覆盖静默模式。
- `-n` 仅处理命令行指定的目录。不处理受信任目录（`/lib` 和 `/usr/lib`）也不处理 `/etc/ld.so.conf` 中指定的目录。隐含 `-N`。
- `-N` 不重建缓存。除非同时也指定了 `-X`，否则仍更新链接。
- `-X` conf 不更新链接。除非同时也指定了 `-N`，否则仍会重建缓存。
- `-C` cache 使用 conf 代替 `/etc/ld.so.conf`。
- `-r` root 使用 cache 代替 `/etc/ld.so.cache`。
- `-l` 切换并使用 root 作为根目录。
- `-p` 库模式。手动链接单个库。仅供专家使用。打印当前缓存中存储的目录和候选库。

## 文件

`/lib/ld.so`

运行时链接器/加载器

`/etc/ld.so.conf`

包含一个由冒号、空格、制表符、换行或逗号分隔的目录列表，在这些目录中搜索库。

`/etc/ld.so.cache`

包含在 `/etc/ld.so.conf` 中指定的目录以及 `/lib` 和 `/usr/lib` 中找到的库的有序列表。

# 另请

`ldd(1)`, `ld.so(8)`

# 结语

本页面是 Linux man-pages 项目发布 3.53 版本的一部分。关于项目的描述以及报告错误的信息可以在 `http://www.kernel.org/doc/man-pages/` 找到。

# `ledctl`

## 名称

`ledctl` - 用于存储机箱的 Intel(R) LED 控制应用程序。

## 概要

```
ledctl [OPTIONS] pattern_name=list_of_devices ...
```

## 说明

`ledctl` 是一个用户空间应用程序，用于控制与机箱或驱动器槽每个槽位相关的 LED。`list_of_devices` 中列出的设备 LED 将设置为给定的模式 `pattern_name`，所有其他 LED 将被关闭。用户必须具有 root 权限才能使用此程序。

有两种类型的系统：2-LED 系统（活动指示 LED、状态 LED）和 3-LED 系统（活动指示 LED、定位 LED、故障 LED）。`ledctl` 应用程序使用 GPIO 和 SES-2 协议控制 LED。该程序实现了 SFF-8489 规范的 GPIO IBPI 模式。请注意，某些机箱并不严格遵守 SFF-8489 规范。可能会出现机箱处理器接受 IBPI 模式但以不同于 SFF-8489 标准的方式闪烁 LED，或者支持的有限。

不支持 LED 管理 (AHCI) 和 SAF-TE 协议。

`ledctl` 应用程序已验证可与 Intel(R) 存储控制器（即 Intel(R) AHCI 控制器和 Intel(R) SAS 控制器）配合。该程序可能适用于其他厂商的存储控制器（特别是 SCSI/SAS 控制器）。然而，尚未测试其他厂商的存储控制器。

`ledmon` 应用程序在访问 LED 时具有最高优先级。这意味着如果 `ledmon` 运行，`ledctl` 的某些模式可能无效（定位模式除外）。

`ledctl` 应用程序是 Intel(R) Enclosure LED Utilities 的一部分。

## 模式名称

`ledctl` 应用程序根据 SFF-8489 规范接受以下 `pattern_name` 参数名称。

- `locate`: 开启与给定设备（s）或空槽位相关的定位 LED。
- `locate_off`: 仅关闭定位 LED。
- `normal`: 关闭状态 LED、故障 LED 和定位 LED。

## 模式翻译

当向设备发送非 ses-2 模式时，会进行自动翻译。

- `locate`: 翻译为 `ses_ident`
- `locate_off`: 翻译为 `ses_ident`
- `normal`: 翻译为 `ses_ok`
- `off`: 翻译为 `ses_ok`
- `degraded`: 翻译为 `ses_ica`
- `rebuild`: 翻译为 `ses_rebuild`
- `rebuild_p`: 翻译为 `ses_rebuild`
- `failed`: 翻译为 `ses_ifa`
- `hotspare`: 翻译为 `ses_hotspare`
- `pfa`: 翻译为 `ses_rsvd_dev`
- `failure`: 翻译为 `ses_fault`
- `disk_failed`: 翻译为 `ses_fault`

## 设备列表

应用程序接受两种格式的设备列表。第一格式是逗号分隔元素的列表。第二格式是花括号内的列表，元素之间用空格分隔。详情请见下方的示例部分。

设备是 `/dev` 目录或 `/sys/block` 目录下的文件路径。它可能标识块设备、RAID 设备或容器设备。在 RAID 设备或容器设备的情况下，将为所有相关的块设备设置状态。

`list_of_devices` 中列出的设备 LED 将设置为给定的模式 `pattern_name`，所有其他 LED 将被关闭。

## 选项

`-c` or `--config=path`

设置本地配置文件的路径。如果指定了此选项，全局配置文件和用户配置文件将无效。

`-l` or `--log=path`

设置本地日志文件的路径。如果指定了此选项，则不使用全局日志文件 `/var/log/ledctl.log`。

`-h` or `--help`

打印此文本并退出。

`-v` or `--version`

显示 `ledctl` 版本以及有关许可证的信息并退出。

## 文件

`/var/log/ledctl.log`

全局日志文件，供 `ledctl` 应用程序的所有实例使用。要强制将日志写入用户定义的文件，请使用 `-l` 选项开关。

`~/.ledctl`

用户配置文件，`ledmon` 和所有 `ledctl` 应用程序实例之间共享。

`/etc/ledcfg.conf`

全局配置文件，`ledmon` 和所有 `ledctl` 应用程序之间共享。

## 示例

以下示例说明了如何定位单个块设备。

```
ledctl locate=/dev/sda
```

以下示例说明了如何关闭同一块设备的定位指示灯（Locate LED）。

```
ledctl locate_off=/dev/sda
```

以下示例说明了如何定位 RAID 设备的磁盘，以及如何同时为两个块设备设置重建模式。此示例同时使用了设备列表的两种格式。

```
ledctl locate=/dev/md127 rebuild={ /sys/block/sd[a-b] }
```

以下示例说明了如何关闭给定设备的状态指示灯（Status LED）和故障指示灯（Failure LED）。

```
ledctl off={ /dev/sda /dev/sdb }
```

以下示例说明了如何定位三个块设备。此示例使用了设备列表的第一种格式。

```
ledctl locate=/dev/sda, /dev/sdb, /dev/sdc
```

# 许可证

Copyright (c) 2009-2013 Intel Corporation.

本程序根据自由软件基金发布的 GNU 通用公共许可证进行分发。有关许可证和不提供担保的详情，请参阅内置帮助。

## 参见

`ledmon(8)`, `ledctl.conf(5)`

## 作者

本手册页由 Artur Wojcik <artur.wojcik@intel.com> 编写。其他人可以使用它。

# `ledmon`

## 名称

`ledmon` - 用于存储机箱的 Intel(R) LED 监控服务。

## 概要

```
ledmon [OPTIONS]
```

## 描述

`ledmon` 应用程序是一个守护进程，用于监控软件 RAID 设备的状态（仅限 md）或块设备的状态。该状态通过与机箱每个插槽或驱动器槽相关的 LED 进行可视化展示。系统有两种类型：2-LED 系统（活动 LED、状态 LED）和 3-LED 系统（活动 LED、定位 LED、故障 LED）。该应用程序在访问 LED 时具有最高优先级。

`ledmon` 应用程序使用 SGPIO 和 SES-2 协议控制 LED。程序实现了 SFF-8489 规范中 SGPIO 的 IBPI 模式。请注意，机箱并不完全遵守 SFF-8489 规范。可能会出现机箱处理器接受 IBPI 模式但闪烁 LED 不符合 SFF-8489 规范，或者支持的模式有限。

不支持 LED 管理 (AHCI) 和 SAF-TE 协议。

未提供指定监控哪个 RAID 卷以及哪些监控的方法。`ledmon` 应用程序监控所有 RAID 设备并将其状态可视化。

`ledmon` 应用程序已验证适用于 Intel(R) 存储控制器（即 Intel(R) AHCI 控制器和 Intel(R) SAS 控制器）。该应用程序可能适用于其他厂商的存储控制器（特别是 SAS/SCSI 控制器）。然而，其他厂商的存储控制器尚未经过测试。

`ledmon` 应用程序是 Intel(R) 机箱 LED 工具包的一部分。允许运行单个应用程序实例。

## 选项

- `-c` 或 `--config=path`

设置本地配置文件的路径。如果指定了此选项，全局配置文件和用户配置文件将不起作用。

- `-l` 或 `--log=path`

设置本地日志文件的路径。如果指定了此选项，则不使用全局日志文件 `/var/log/ledmon.log`。

- `-t` 或 `--interval=seconds`

设置扫描 sysfs 的时间间隔。值以秒为单位。最小为 5 秒，最大值未指定。

- `--quiet` 或 `--error` 或 `--info` 或 `--debug`

'quiet' 表示无输出，'all' 表示所有。

- `-h` 或 `--help`

打印此帮助文本。

- `-v` 或 `--version`

显示版本。

`/var/log/ledctl.log`

全局日志文件，供 `ledctl` 应用程序的所有实例使用。要强制将日志写入用户定义的文件的文件。

`~/.ledctl`

用户配置文件，`ledmon` 和所有 `ledctl` 应用程序实例共享。

`/etc/ledcfg.conf`

全局配置文件，`ledmon` 和所有 `ledctl` 应用程序实例共享。

# 许可证

Copyright (c) 2009-2013 Intel Corporation.

本程序根据自由软件基金发布的 GNU 通用公共许可证进行分发。有关许可证和不提供担保的详情，请参阅内置帮助。

# 缺陷

`ledmon` 应用程序无法识别 SFF-8489 规范的 PFA 模式，因此状态不可可视化。

## 参见

`ledctl(8)`, `ledctl.conf(5)`

## 作者

本手册页由 Artur Wojcik <artur.wojcik@intel.com> 编写。其他人可以使用它。

# `NSS-MYHOSTNAME`

## 名称

`nss-myhostname`, `libnss_myhostname.so` - 为本地配置的系统提供主机名解析。

## 概要

```
libnss_myhostname.so
```

## 描述

`nss-myhostname` 是 GNU C 库 名称切换功能的插件，用于解析 `gethostname(2)` 返回的本地配置主机名。此模块解析的精确主机名包括：

本地配置的主机名根据范围解析为本地配置的 IP 地址，如果没有配置，则是 IPv4 地址 127.0.2（本地回环）和 IPv6 地址 ::1（本地主机）。

主机名“localhost”解析为 IP 地址 127.0.0.1 和 ::1。

主机名“gateway”解析为当前默认网关地址，按其指标排序。这为当前网关分配了一个稳定的主机名，便于独立于网络配置进行引用。

各种软件依赖于一个始终可解析的主机名。在在使用动态主机名时，传统做法是在更改主机名的同时修改 `/etc/hosts`。

在启用 `nss-myhostname` 后，没有必要修改 `/etc/hosts`。

要激活 NSS 模块，必须将“myhostname”添加到 `/etc/nsswitch.conf` 中以“hosts.”开头的行。

建议将“myhostname”放在 nsswitch.conf 行的最后，以确保该映射仅作为备备，任何 DNS 或基于 `/etc/hosts` 的映射都具有优先级。

## 示例

这是一个 `/etc/nsswitch.conf` 文件的示例，它可以正确启用 `myhostname`：

```
passwd: compat group: compat shadow: compat hosts: files dns mymymachines myhostname networks: files protocols: db files services: db files ethers: db files rpc: db files netgroup: nis
```

使用 `glibc` 的 `getent` 工具进行测试：

```
$ getent ahosts `hostname` ::1 STREAM omega ::1 DGRAM ::1 RAW 127.0.0.2 STREAM 127.0.0.2 DGRAM 127.0.0.2 RAW
```

在这种情况下，本地主机名是 omega。

## 参见

`systemd(1)`, `nss-mymachines(8)`, `nsswitch.conf(5)`, `getent(1)`

## `NSS-MYMACHINES`

## 名称

`nss-mymachines`, `libnss_mymachines.so.2` - 为本地容器实例提供主机名解析。

## 概要

```
libnss_mymachines.so.2
```

## 描述

`nss-mymachines` 是 GNU C Library (glibc) 中 GNU 名称服务切换 (NSS) 功能的插件，为本地运行并由 `systemd-machined.service(8)` 注册的容器提供主机名解析。容器名称将被解析为特定容器的 IP 地址，并按其范围排序。

要激活 NSS 模块，必须在 `/etc/nsswitch.conf` 中以 “hosts:” 开头的行中添加 “mymachines”。

建议将 “mymachines”放置在 nsswitch.conf 行末尾，以确保该映射仅作为回备使用，且任何基于 DNS 或 `/etc/hosts` 的映射都具有优先权。

## 示例

这里是一个 `/etc/nsswitch.conf` 文件的示例，它可以正确启用 mymachines：

```
npasswd: compat group: compat shadow: compat hosts: files dns mymachines nmyhostname networks: files protocols: db hosts files services: db files ethers: db files rpc: db files netgroup: nis
```

## 另参

`systemd(1)`, `systemd-machined.service(8)`, `nss-myhostname(8)`, `nsswitch.conf(5)`, `getent(1)`

## `LIBVIRTD`

- way



# libvirtd - libvirtd 管理守护进程

## 概要

```
libvirtd [-dlv ] [ -f config_file ] [ -p pid_file ] [ -t timeout_seconds ]
```

```
libvirtd—version
```

## 描述

`libvirtd` 程序是 `libvirt` 虚拟化管理系统的服务端守护进程组件。

该守护进程运行在主机服务器上，为虚拟化虚拟机执行所需的管理任务。这包括启动、停止和在主机服务器之间迁移虚拟机、配置和操作网络，以及管理虚拟机使用的存储。

`libvirtd` 客户端库和工具连接到此守护进程，发布任务并收集有关主机系统和虚拟机配置及资源的信息。

默认情况下，`libvirtd` 守护进程在本地 Unix 域接字上监听请求。使用 `-l|listen` 命令选项，可以指示 `libvirtd` 守护进程额外在 TCP/IP 接字上监听。要使用的 TCP/IP 接字在 `libvirtd` 配置文件中定义。

重启 `libvirtd` 不影响运行中的虚拟机。虚拟机将继续运行，如果它们的 XML 配置已定义，则会被自动拾起。任何未定义 XML 配置的虚拟机将从配置中丢失。

## 选项

- `-h`, `--help`

显示命令行帮助用法后退出。

- `-d`, `--daemon`

作为守护进程运行并写入 PID 文件。

- `-f`, `--config FILE`

使用此配置文件，覆盖默认值。

- `-l`, `--listen`

监听 TCP/IP 连接。

- `-p`, `--pid-file FILE`

使用此名称作为 PID 文件，覆盖默认值。

- `-t`, `--timeout SECONDS`

在超时时间（以秒为单位）结束后没有客户端连接或注册资源后退出。请注意，自动启动的网络等资源会导致永远无法达到超时，即使在没有客户端连接的情况下也是。

- `-v`, `--verbose`

启用详细消息的输出。

- `--version`

显示版本信息后退出。

## 信号

接收到 `SIGHUP` 时，`libvirtd` 将重新加载其配置。

## 文件

当以 root 身份运行时

`SYSCONFDIR/libvirtd.conf`

`libvirtd` 使用的默认配置文件，除非在命令行上使用 `-f|config` 选项覆盖。

`LOCALSTATEDIR/run/libvirtd/libvirtd-sock`

`LOCALSTATEDIR/run/libvirtd/libvirtd-sock-ro`

`libvirtd` 将使用的接字。

`SYSCONFDIR/pki/CA/cacert.pem`

`libvirtd` 将使用的 TLS 证书机构证书。

`SYSCONFDIR/pki/libvirtd/servercert.pem`

`libvirtd` 将使用的 TLS 服务器证书。

`SYSCONFDIR/pki/libvirtd/private/serverkey.pem`

`libvirtd` 将使用的 TLS 服务器私钥。

`LOCALSTATEDIR/run/libvirtd.pid`

要使用的 PID 文件，除非被 `-p|pid-file` 选项覆盖。

当以 root 身份运行时。

`$XDG_CONFIG_HOME/libvirtd.conf`

`libvirtd` 使用的默认配置文件，除非在命令行上使用 `-f|config` 选项覆盖。

`$XDG_RUNTIME_DIR/libvirtd/libvirtd`

`libvirtd` 将使用的接字。

`$HOME/.pki/cacert.pem`

`libvirtd` 将使用的 TLS 证书机构证书。

`$HOME/.pki/servercert.pem`

`libvirtd` 将使用的 TLS 服务器证书。

`$HOME/.pki/serverkey.pem`

`libvirtd` 将使用的 TLS 服务器私钥。

`$XDG_RUNTIME_DIR/libvirtd.pid`

要使用的 PID 文件，除非被 `-p|pid-file` 选项覆盖。

## 示例

获取版本：

```
libvirtd --version
```

启动 `libvirtd`，创建一个 PID 文件：

```
libvirtd -d
```

守护化：

```
libvirtd -l -v
```

## 缺陷

通过以下方式报告你发现的缺陷：

a) 邮件列表

b) 缺陷跟踪器

或者，你可以向你的软件发行者报告。

## 作者

请参考

## 版权

Copyright (C) 2006-2012 Red Hat, Inc., 以及作者

## 许可

`libvirtd` 根据 LGPL v2.1 发布；请查看源码拷贝条件。没有特定用途

## 另参

`virsh(1)`, `virt-install(1)`, `virt-xml-validate(1)`, `virt-top(1)`, `df(1)`

## SETARCH

### 名称

`setarch` - 在新环境中更改架构并设置特性标志

## 概要

```
setarch <arch> [options] [program [[arguments]]] arch [options] [program [[arguments]]]
```

## 描述

`setarch` 目前影响 `uname -m` 的输出。例如，在 AMD 系统上，运行 '`setarch i36 program`' 会导致 '`program`' 看到 机器类型。它还可以设置特性选项。默认程序为 `/bin/sh`。

## 选项

- `-v`, `--verbose`

详细

- `-h`, `--help`

显示帮助（当 `setarch` 不带参数时也会显示）。

- `-V`, `--version`

输出版本信息并退出。

- `-uname-2.6`

导致程序看到以 2.6 开头的内核版本

- `-3`, `--3gb`

在支持的系统中指定进程使用最大 3GB 地址空间 (`ADDR_LIMIT_3GB`)。

- `-4gb`

仅为了向下兼容

- `-list`

列出可以设置的架构。

- `-B`, `--32bit`

开启 `ADDR_LIMIT_32BIT`。

- `-F`, `--fdpic-funcptrs`

用户空间指针指向描述符（开启 `FPIC_FUNCPTRS`）。

- `-I`, `--short-node`

开启 `SHORT_NODE`。

- `-L`, `--addr-compat-layout`

更改虚拟内存分配方式（开启 `ADDR_COMPAT_LAYOUT`）。

- `-R`, `--addr-no-randomize`

禁用虚拟地址空间的随机化（开启 `ADDR_NO_RANDOMIZE`）。

- `-S`, `--whole-seconds`

开启 `WHOLE_SECONDS`。

- `-T`, `--sticky-timeouts`

开启 `STICKY_TIMEOUTS`。

- `-X`, `--read-implies-exec`

开启 `READ_IMPLIES_EXEC`。

- `-Z`, `--mmap-page-zero`

开启 `MMAP_PAGE_ZERO`。

## 示例

```
setarch ppc32 rpmbuild --target=ppc --rebuild foo.src.rpm
```

```
setarch ppc32 -v -vL3 rpmbuild --target=ppc --rebuild bar.src.rpm
```

```
setarch ppc32 --32bit rpmbuild --target=ppc --rebuild foo.src.rpm
```

## 作者

Elliot Lee Jindrich Novy

## 可用性

`setarch` 命令是 `util-linux` 软件包的一部分，可在 Linux 内核归档中使用。

# lldpad

## 名称

`lldpad` - 链路层发现协议 (LLDP) 代理守护进程

## 概要

```
lldpad [-h] [-v] [-V level] [-d] [-k] [-p] [-s] [-t] [-f filename]
```

## 描述

为支持的网络接口执行 LLDP 协议。目前支持的 TLV 列表如下：

- IEEE 802.1AB 强制性 TLV

- IEEE 802.1AB 基础管理 TLV

- IEEE 802.3 组织特定 TLV

- LLDP-MED 组织特定 TLV

- 数据中心桥接能力交换协议 (DCBX) TLV

- 边缘虚拟桥接 (EVB) TLV

`lldpad` 的功能包括：

- 从已启用端口传输包含启用 TLV 的 LLDP PDU。

- 接收来自已启用端口的 LLDP PDU。

- 为支持 DCB rtnetlink 接口的接口运行 DCBX 协议。这包括在 LLDP 之上运行 DCBX 状态机以及对网络接口 DCB 参数的相应配置。支持的 DCB 功能包括：扩展传输选择 (ETS)、优先级流控制 (PFC) 和 FCoE 应用。

- 根据 DCBX 的运行配置网络驱动程序的 DCBX 设置。

- 为客户端应用程序提供多通道接口，用于查询和配置功能。客户端接口上还会生成事件以通知客户端发生的更改。`lldpad` 软件包包含两个客户端：用于通用 LLDP 代理管理的 `lldtool` 和用于 DCB 管理的 `dctool`。

`lldpad` 支持以下列出的 DCB 能力交换协议 (DCBX) 协议版本：

version 1 - 也称为 CIN DCBX

<http://download.intel.com/technology/edc/dcb_cp_spec.pdf>

version 2 - 也称为 CEE DCBX

<http://www.ieee802.org/files/public/docs2008/az-wadekar-dcbx-capability-exchange-discovery-protocol-1108-v1.01.pdf>

## IEEE DCBX

详情参见 IEEE 802.1Qaz-2011 规范。

IEEE DCBX 是具有 DCB 能力接口的默认 DCBX 模式，以便接口能够启动。**Lldpad** 可以进行全局配置以支持一种旧 DCBX 版本（CIN 或 CEE）。如果远程 LLDP 代理没有传输任何 IEEE DCBX TLV，但传输了与配置的旧 DCBX 版本匹配的旧 DCBX TLV，则 DCBX 模式将退回到旧 DCBX 模式。在下次链路重置之前，它不会切换回 IEEE DCBX 模式。如果 **Lldpad** 为给定接口退回到旧 DCBX 模式且守护进程停止并重启，则该接口将使用旧 DCBX 模式，而不是从 IEEE DCBX 模式启动。此行为仅适用于 **Lldpad** 重启的情况，且不会跨系统重启持久化。

查看 **dcbtool** 获取有关如何全局配置 **Lldpad** 执行何种旧版本 DCBX 的信息。

查看 **lldptool** 获取有关如何将接口的 DCBX 模式重置为默认（从 IEEE DCBX 模式启动）的信息。

**Lldpad** 还支持边缘虚拟桥接，目前处于 IEEE 802.1Qb 工作组的规范制定中。<http://www.ieee802.org/1/pages/802.1bg.html>

## 选项

`Lldpad` 有以下命令行选项：

- `-h` 显示用法信息

- `-f filename` 使用指定的文件作为配置文件而不是默认文件：`/var/lib/lldpad/lldpad.conf`。`lldpad` 期望配置文件的目录存在，但如果配置文件不存在，将创建一个默认配置文件。`lldpad` 会创建并维护配置的内容。配置应通过 `lldtool` 或 `dbctool` 完成。

- `-d` 以守护进程运行 `lldpad`

- `-v` 显示 `lldpad` 版本

- `-V level` 设置 `lldpad` 调试级别。使用 syslog 调试级别，详见 syslog,2。

- `-k` 用于终止已启动的第一个 `lldpad` 实例（例如从 initrd 启动）。一旦调用 `lldpad -k` 且 `lldpad` 重启，后续的 `lldpad` 调用将...

- `-s` 从共享内存中移除 `lldpad`

- `-p` 不要创建 `lldpad`

- `-t` 在 `lldpad` 中省略时间戳

## 注意

在终止时，`lldpad` 不会撤销它设置的任何配置。这种方法最大限度减少了重启守护进程导致意外行为的风险。

## 参见

`dcbtool(8)`, `lldptool(8)`, `dcbx(8)`,

- `et(8)`

- `med(8)`

- `ets(8)`

- `pfc(8)`

- `med(8)`

- `evb(8)`

- `vdp(8)`

## 版权

`lldpad` - 链路层发现协议 (LLDP) 代理守护进程

(c) 2007-2012 Intel Corporation.

## 许可证

本程序是自由软件；您可以根据通用公共许可证对其进行分发或修改。您应该收到了一份本程序的通用公共许可证副本；如果没有收到，请查看名为“COPYING”的文件。

## 支持

联系信息：open-ldap 邮件列表 <open-lldp.org>

# lldptool

## 名称

APP - 显示 / 操作 APP TLV

## 概要

```
lldptool -t -i ethx -V APP [-c app]
lldptool -T -i ethx -V APP [-d] app=prio,sel,pid
```

## 描述

APP TLV 是一种信息 TLV，并将显示应用程序表。如果对方 APP TLV 和本地 TLV 匹配选择器字段，则使用本地参数。

## 参数

`app` 使用三个参数配置本地应用程序数据字段：优先级 (`prio`)、选择器 (`sel`) 和协议 (`pid`)。提供 `-d` 选项可以移除匹配三个参数的项。

## 原理

APP TLV 是大多数终站的信息 TLV。预计不需要设置 APP 数据。在假设不存在具有匹配选择器和优先级的本地项的情况下，对方数据将被处理并添加到应用程序数据表中。

通过将 APP 数据添加到应用程序表中，应用程序（例如 `isscid`）可以对其进行查询。应用程序查询特定的协议和选择器，并可以使用这些数据将流量映射到相应的流量类别。

## 示例与用法

在 eth2 上配置优先级为 4 的 ISCSI 应用程序

```
lldptool -T -i ethx -V APP app=4,2,3260
```

在 eth2 上配置优先级为 3 的 FCoE 应用程序

```
lldptool -T -i ethx -V APP app=3,1,35078
```

从 eth2 上移除优先级为 3 的 FCoE 应用程序

```
lldptool -T -i ethx -V APP app=3,1,35078
```

在 eth2 上显示本地配置的应用程序表

```
lldptool -t -i ethx -V APP -c app
```

显示 eth2 上最后传输的 APP TLV

```
lldptool -t -i ethx -V APP
```

## SOURCE

IEEE 802.1Qaz (http://www.ieee802.org/1/pages/dcbridges.html)

## SEE ALSO

`lldptool(8)`, `lldpad(8)`

## AUTHOR

John Fastabend

## lldptool-dcbx

### NAME

DCBX - 显示 / 操作 DCBX 配置

## SYNOPSIS

```
lldtool -t -i ethx -V IEEE-DCBX -c [mode]
lldtool -T -i ethx -V IEEE-DCBX mode=reset
lldtool -t -i ethx -V <CIN-DCBX|CEE-DCBX> -c [enableTx]
lldtool -T -i ethx -V <CIN-DCBX|CEE-DCBX> enableTx=<yes|no>
```

## DESCRIPTION - DCBX MODE

`Lldpad` 支持以下版本的 DCB 能力交换（DCBX）协议：

- CIN DCBX: <http://download.intel.com/technology/eedc/dcb-cep_spec.pdf>

- CEE DCBX: <http://www.ieee802.org/1/files/public/docs2008/az-wadekar-dcb-capability-exchange-discovery-protocol-1108-v1.01.pdf>

- IEEE DCBX: 详情见 IEEE 802.1Q-2021 规范。



IEEE DCBX 是支持 DCB 接口的默认 DCBX。因此，接口启动时将传输默认和配置的 DCBX TLV。`Lldpad` 可以全局配置为支持一种旧 DCBX 版本（CIN 或 CEE）。如果 LLDP Agent 未传输任何 DCBX TLV，但传输了与配置的 DCBX 版本匹配的旧 DCBX TLV，则 DCBX 模式将退回到 `legacyBX` 模式。在下次链路重置之前，它不会回到 DCBX 模式。如果 `lldpad` 回退到 `legacy BX` 模式，该接口将使用该模式而不是从 DCBX 模式启动。这种 `legacy BX` 行为仅适用于 `lldpad` 重启的情况，不会在系统重启后持续。

可以使用特殊的 `IEEE-DCBX` 参数查询和配置 DCBX 模式。实际上并没有对应的 TLV。查询时，DCBX 模式可以取以下值：

- `auto`: 如果 `lldpad` 重启，（初始）将使用 IEEE DCBX。例外是 DCBX 模式已被强制设置为 `legacy BX` 模式，则将使用指定的旧模式。有关此异常，请参见 `dcbtool(8)` 中的 `mode` 参数信息。
- `CEE`: 如果 `lldpad` 重启，将使用 CEE DCBX。
- `CIN`: 如果 `lldpad` 重启，将使用 CIN DCBX。

通过将 `mode` 参数设置为 `reset` 可以将 DCBX 模式重置为 `auto`。CIN 和 CEE DCBX TLV 的详细配置使用 `dcbtool`（参见 `dcbtool(8)`）。然而，`lldtool` 可以配置 CIN 和 CEE DCBX TLV 的 `enableTx` 参数（与大多数其他 TLV 一样）。由于 `lldtool` 在任何给定接口上只传输一个版本的 DCBX TLV，因此 CIN 和 CEE DCBX TLV（以及 IEEE DCBX TLV）的 `enableTx` 参数仅在相应的 DCBX 版本激活状态时生效。

## ARGUMENTS

`mode=reset`

通过使用特殊的 `IEEE-DCBX` 参数将 `mode` 参数设置为 `reset`，重置 `lldpad` 重启后将使用的 DCBX 模式。

`enableTx`

如果指定接口选择了相应的 DCBX 模式（`CIN-DCBX` 或 `CEE-DCBX`），则启用指定的 DCBX TLV 在 LLDU 中传输。

## EXAMPLE & USAGE

查询 `lldpad` 重启后将使用的当前 DCBX 模式（此为非持久化设置）：

```
lldtool -t -i eth3 -V IEEE-DCBX -c mode
```

在下次 `lldpad` 重启后将 DCBX 模式重置为“auto”（从 DCBX 模式启动）：

```
lldtool -T -i eth3 -V IEEE-DCBX mode=reset
```

启用 CEE DCBX TLV 的传输：

```
lldtool -T -i eth3 -V CEE-DCBX enableTx=yes
```

禁用 CIN DCBX TLV 的传输：

```
lldtool -T -i eth3 -V CIN-DCBX enableTx=no
```

查询 CEE DCBX TLV 的 `enableTx` 配置：

```
lldtool -t -i eth3 -V CEE-DCBX -c enableTx
```

## NOTES

## SEE ALSO

`dcbtool(8)`, `lldptool(8)`, `lldptool-ets(8)`, `lldptool-pfc(8)`, `lldptool-app(8)`, `lldpad(8)`

## AUTHOR

Eric Multanenen

## lldptool

> **NAME**

ETS-{CFG|REC} - 显示 / 操作 ETS TLV 配置

## SYNOPSIS

```
lldtool -t -i eth -V ETS-CFG -c CONFIG_ARG ...]
CONFIG_ARG := { enableTx | willing | tsa | up2tc | numtcs | tcbw }
CONFIG_ARG=value ...
CONFIG_ARG :=
enableTx = {yesno} |
willing = {yesno} |
tsa = tc:{ets|strict|vendor},... |
up2tc = priority:tc,... |
ccbw = bw1,bw2,...
[-c CONFIG_ARG ...]
CONFIG_ARG=value ...
CONFIG_ARG :=
enableTx = {yesno} |
tsa = tc:{ets|strict|vendor},... |
up2tc = priority:tc,... |
ccbw = bw1,bw2,...
```

## DESCRIPTION

增强传输选择（ETS）功能分别通过 `ETS-REC` 和 `ETS-CFG` 配置了建议 TLV 和配置 TLV。

## ARGUMENTS

`enableTx`

启用 ETS TLV。

`willing`

设置 `ETS-CFG` willing 位。

`tsa`

启用 ETS 选择算法（逗号分隔）。

`up2tc`

将优先级映射到流量类的逗号分隔列表。

`tcbw`

带宽的逗号分隔列表。

`numtcs`

显示支持的流量类数量。

## THEORY OF OPERATIONS

IEEE 802.1Qaz 随 ETS 配置默认启用。为了支持旧 DCBX（CIN 或 CEE），会通过 DCBX 模式禁用 ETS 功能。这允许交换机为特定应用程序编码 DCBX 参数。有关操作的更多信息请参见 `dcbxd(8)`。

## EXAMPLE & USAGE

为接口 `eth2` 配置 willing 位：

```
lldtool -T -i eth2 -V ETS-CFG willing=yes
```

在 `eth2` 上配置 ETS 和严格优先的流量类：

```
lldtool -T -i eth2 -V ETS-CFG tsa=0:ets,1:ets,2:ets,3:strict,4:strict,5:strict
```

在 `eth2` 上配置优先级到流量类的 1:1 映射：

```
lldtool -T -i eth2 -V ETS-CFG up2tc=0:0,1:1,2:2,3:3,4:4,5:5,6:6,7:7
```

# 来源

IEEE 802.1Qaz (http://www.ieee802.org/1/pages/dcbridges.html)

## 注意

旧版本内核在 2.6.38 中添加了对 `tc-mqprio` 的；可能需要使用其他机制将应用程序映射到流量类。

## 参见

`lldptool(8)`, `lldptool-app(8)`, `lldpadd(8)`, `tc-mqprio(8)`, 

## 作者

John Fastabend

# lldptool

+> 名称

evb - 显示 / 操作 EVB TLV 配置

# 概要概要

```
lldtool -t -g ncb -i ethx -V evbCfg -c enableTx
lldtool -T -g ncb -i ethx -V evbCfg -c enableTx=[yes|no]
lldtool -t -g ncb -i ethx -V evbCfg -c fmode
lldtool -T -g ncb -i ethx -V evbCfg -c fmode=[bridge|reflectiverelay]
lldtool -t -g ncb -i ethx -V evbCfg -c capabilities
lldtool -T -g ncb -i ethx -V evbCfg -c capabilities=[rte|ecp|vdp|none]
lldtool -t -g ncb -i ethx -V evbCfg -c rte
lldtool -T -g ncb -i ethx -V evbCfg -c rte=[<rte>]
lldtool -t -g ncb -i ethx -V evbCfg -c vsis
lldtool -T -g ncb -i ethx -V evbCfg -c vsis=[<number of vsis>]
```

## 描述

EVB TLV 是一种用于发布站点和桥边缘虚拟桥（evb）能力并请求桥转发的 TLV。如果双方都同意边缘控制协议（ECP）和 VSI 发现协议（VDP）能力，双方可以使用 ECP 帧交换 VDP TLV。`vsis` 参数将设置 VSI 的最大数量，并显示当前配置的 VSI 数量。

# 参数

`enableTx`

启用传输 EVB TLV

`fmode`

显示或设置桥（默认）或反射中继（RR）之间的转发模式。

+ `capabilities`

显示或设置在 TLV 中向相邻交换机公布的本地能力。此参数接受 `rte`、`vdp` 或 `ecp` 的任何组合，并用逗号 ","隔开。如果你不想设置任何能力，请使用关键字“none”。

`rte`

显示或设置本地运行时间指数（RTE）。RTE 将作为 ECP 和 VDP 协议计时的基准。

`vsis`

显示或设置在 TLV 中向相邻交换机公布的虚拟站点接口（VSIs）数量。此参数期望一个 0 到 65535 之间的数字。

# 工作原理

EVB TLV 用于在站点和相邻交换机之间发布和交换支持的参数。TLV 使用最近的客户桥代理。

如果将“reflectiverelay”设置为转发模式，交换机将允许来自不同源的帧在同一端口上“反射”回该端口。这将允许同一主机上的虚拟机通过交换机进行通信。

`capabilities` 参数用于设置 RTE、ECP 和 VDP 支持。只有当双方都同意将 ECP 和 VDP 作为能力时，才能在 ECP 帧中交换 VDP TLVs。RTE 将作为 ECP 和 VDP 的基准计时参数。

# 使用示例

显示 `eth8` 的本地配置值

```
lldtool -t -g ncb -i eth8 -V evbCfg
```

显示 `eth8` 的远程配置值

```
lldtool -n -g ncb -i eth8 -V evbCfg
```

显示 `eth8` 是否配置了 evb tv 发送

```
lldtool -t -g ncb -i eth8 -V evbCfg -c enableTx
```

显示 `eth8` 当前请求的转发模式

```
lldtool -t -g ncb -i eth8 -V evbCfg -c fmode
```

将转发模式设置为反射中继

```
lldtool -T -g ncb -i eth8 -V evbCfg -c fmode=reflectiverelay
```

显示当前配置的能力

```
lldtool -t -g ncb -i ethx -V evbCfg - capabilities
```

将本地可能的能力设置为 RTE、ECP 和 VDP

```
lldtool -T -g ncb -i ethx -V evbCfg -c capabilities=rte,ecp,vdp
```

```
lldtool -T -g ncb -i ethx -V evbCfg -c capabilities=none
```

显示 RTE 的本地配置值

```
lldtool -t -g ncb -i ethx -V evbCfg -c rte
```

设置 RTE 值

```
lldtool -T -g ncb -i ethx -V evbCfg -c rte=[<rte>]
```

显示配置的 VSI 最大数量

```
lldtool -t -g ncb -i ethx -V evbCfg -c vsis
```

设置 VSI 的最大数量

```
lldtool -T -g ncb -i ethx -V evbCfg -c vsis=[<number of vsis>]
```

# 来源

IEEE 802.1Qbg (http://www.ieee802.org/1/pages/802.1bg)

## 注意

`lldpad` 中的代码反映了即将发布的标准草案 0。线上的 EVB TLV 可以用 `wireshark` 解码。

## 参见

`lldptool-vdp(8)`, `lldptool(8)`, `lldpad(8)`

## 作者

Jens Osterkamp

# lldptool

+> 名称

evb - 显示 / 操作 EVB 802.1 标准 TLV

## 概要

```
lldtool -t -g ncb -i ethx -V evb
lldtool -t -g ncb - i ethx -V evb -c
lldtool -t -g ncb - i ethx -V evb -c enabletx
lldtool -T -g ncb - i ethx -V evb -c enabletx=[yes|no]
lldtool -t -g ncb - i ethx -V evb -c evbmode
lldtool -T -g ncb - i ethx -V evb -c evbmode=[bridge|station]
lldtool -t -g ncb - i ethx -V evb -c evbrreq
lldtool -T -g ncb - i ethx -V evb -c evbrreq=[yes|no]
lldtool -t -g ncb - i ethx -V evb -c evbrrcap
lldtool -T -g ncb - i ethx -V evb -c evbrrcap=[yes|no]
lldtool -t -g ncb - i ethx -V evb -c bgpid
lldtool -T -g ncb - i ethx -V evb -c bgpid=[yes|no]
lldtool -t -g ncb - i ethx -V evb -c ecpretries
lldtool -T -g ncb - i ethx -V evb -c ecpretries=[0..31]
lldtool -t -g ncb - i ethx -V evb -c ecprte
lldtool -T -g ncb - i ethx -V evb -c ecprte=[0..31]
lldtool -t -g ncb - i ethx -V evb -c vdprwd
lldtool -T -g ncb - i ethx -V evb -c vdprwd=[0..31]
lldtool -t -g ncb - i ethx -V evb -c vdprka
lldtool -T -g ncb - i ethx -V evb -c vdprka=[0..31]
```

## 描述

边缘桥（EVB）TLV 是一种用于发布站点和桥的边缘桥接能力，并可能请求桥端口设置为反射中继（发夹）模式。如果双方都同意模式和超时，将使用边缘控制协议（ECP）在主机接口和面向主机接口的交换机端口之间通过 ECP 帧交换 VSI 发现协议（VDP）。

此手册页描述了 2012 年7 月 5 日 IEEE 802.1Qbg 批准标准。参数和属性与实现的 IEEE 802.1Qbg 草案 0.2 有不同。EVB 协议版本取决于 LLDP 数据流中 EVB TLV 的组织唯一标识（OUI）。OUI 值 `0x001b3f` 代表 IEEE 802.1Qbg 草案 0.2，OUI 值 `0x0080c2` 代表 IEEE 802.1Qbg 批准标准。ECP 和 VDP 协议的版本由以太网头中的类型字段决定。IEEE 802.1Qbg 草案 0.2 的以太网类型值为 `0x8bb7`，IEEE 802.1Qbg 批准标准的值为 `0x890`。注意 EVB 协议仅在最近的客户桥之间交换，使用保留的组播 MAC 地址 `01:80:c2:00:00:00` 作为目标 MAC 地址。`lldpad(8)` 支持两个版本，交换机端口配置决定将使用哪个版本。参数和属性见 `ldtool(8)` 手册。

# 参数

调用命令行 '-c' 和参数将以漂亮格式显示完整的 EVB、ECP 和 VDP 设置。下文提供了如何解释输出的详细说明。使用命令行选项 '-c' 和以下一个参数来显示和设置单个参数。文本可以是以下值之一：

`enabletx` 启用或禁用 EVB TLV 的传输。设置为禁用时，LLDP 数据流中不会包含 EVB TLV。此外，没有选项 '-c' 的完整 EVB 设置输出将为空。

`evbmode` 当前的角色或将角色设置为给定值。支持的值为 "station" 或 "bridge"。

`evbrreq` 显示当前的反射中继（发夹）请求模式或反射中继（发夹）请求模式。如果值为 "yes"，则站点请求接口交换端口设置为反射中继（发夹）模式。此字段仅对站点有效，即 `evbmode` 的输出等于 "station"。

`evbrrcap` 显示当前的反射中继（发夹）能力或设置反射中继（发夹）能力。如果值为 "yes"，交换端口将设置为反射中继（发夹）模式。此字段仅对交换机有效，即 `evbmode` 的输出等于 "bridge"。

`gpid` 显示分组的支持状态或开启/关闭站点或交换机对分组的支持。如果设置为 true，站点或交换机希望在 VDP 协议中使用分组标识。

`ecpretries` 显示或设置 ECP 帧重传的最大次数。如果在给定的时间范围内未收到 ECP 确认消息，则发生重传。

`ecprite` 显示或设置本地运行时间指数（RTE）。RTE 将作为 ECP 协议超时和重传计时的基准。等待时间计算为 `10*2ecprite` 微秒。

`vdprwd` 显示或设置等待延迟值。该值计算为 `10*2vdprwd` 微秒，并决定 VDP 协议确认的最大等待时间。

显示或设置初始化存活值（re-init keep alive）。该值计算为 `10*vdprka` 微秒，决定了 VDP 协议发送心跳消息的等待时间。

# 工作原理

EVB TLV 用于在站点与相邻交换机之间发布和交换支持的参数。如果反射继（reflectiverelay）处于激活状态，交换将在接收帧的相同端口上发回以太网帧。这是对当前桥接标准的扩展，允许同一台主机上的虚拟机通过交换机端口进行通信。

# 使用示例

显示 `eth0` 的本地配置值



进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

`lldptool -t gcb -i eth0 -V evb EVB Configuration TLV:(00)`

`station:rreq,rrstat(0x5) retries:7 rte:31 mode:station r/1:0`

`r/1:0 rka:8`

此输出在启用`enabletablex`后显示。第一行显示网桥的当前已知状态。第二行显示站点的当前已知状态。状态以详细形式显示，并在括号中附带十六进制值。详细输出使用了标准文档中的位命名约定。第三行显示 ECP 协议重传次数（`retries`）数和重传超时指数的值。第四行显示当前运行模式（网桥或站点）、资源等待延迟值（`rwd`）以及是否使用本地 (`0`) 或远程 (`1`) `rwd`值的指示。第五行显示初始化存活计数器（`rka`）的值以及是否使用本地 (`0`) 或远程 (`1`) `rka`值的指示。

显示 `eth0` 当前请求的转发模式

```
lldptool -t gcb -i eth0 -V evb - evbrrreq
```

显示 RTE 的本地配置值

```
lldptool -t gcb -i eth0 -V evb -c evbrte
```

将 RTE 设置为 `-g ncb -i` 的最大值

```
lldptool -T -g ncb -i eth0 -V evb -c rte=7
```

将 `enabletablex` 设置为 `yes`

```
lldptool -T -g ncb -i eth0 -V evb -c enabletablex=
```

# 注意事项

目前 `lldpad` 中的代码反映了即将发布的标准 IEEE 802.1 Qbg 的 0.2 草案。`Wireshark` 目前缺少对已批准 IEEE 802.1 Qbg 标准 TLV 的支持。对已批准 IEEE 802.1 Qbg 标准协议 ECP 和 VDP 的支持正在开发中，尚未完全功能。

# 另

`lldptool-vdp(8), lldptool(8), lldpad(8)` IEEE 802.1Qbg (http://www.ieee802.org/1/pages/802.1bg.html)

## 作者

Thomas Richter

# lldptool

> 名称

LLDP-MED - 显示 / 操控 MED TLV 配置

## 概要

```
lldptool -i - ethx -V [ TLV_TYPE ] enableTx
lldptool -T -i ethx -V { TLV_TYPE } enableTx = { yes | no }
lldptool -T -i ethx -V LLDP-MED devtype = { class1 | class2 | class3 | none }
lldptool -t - i ethx -V LLDP-MED devtype
```

`TLV_TYPE` : = { LLDP-MED | medCap | medPolicy | medLoc | medPower | medHwRev | medFwRev | medSwRev | medSerNum | medManuf | medModel | medAssetID }

## 描述

LLDP-MED 扩展支持 ANSI/TIA-1057-2006 文档定义的媒体终端设备链路层发现协议。每个 TLV 都可以配置为类 I、类 II 或类 III 设备。类 I 设备是基础基础的终端设备类，类 II 设备支持媒体流能力，而类 III 设备直接支持 IP 通信系统的终端用户。有关类类型的说明请参阅 ANS-TIA-1057。

# 参数

`enableTx`

启用 TLV 传输

`devtype`

设置或查询设备的类别类型。

# TLV_TYPE

适用于媒体终端设备的支持的 TLV 标识符列表。

# LLDP-MED

将参数应用于所有支持的 MED TLV。

# medCAP

LLDP-MED 能力 TLV

# medPolicy

LLDP-MED 网络策略 TLV

# medLoc

LLDP-MED 位置 TLV

# medPower

LLDP-MED 扩展通过 MDI 供电 TLV

# medHwRev

LLDP-MED 硬件版本 TLV

# medFwRev

LLDP-MED 固件版本 TLV

# medSwRev

LLDP-MED 软件版本 TLV

# medSerNum

LLDP-MED 序列号 TLV

# medManuf

LLDP-MED 厂商 TLV

# medModel

LLDP-MED 型 TLV

# medAssetID

LLDP-MED 资产 ID TLV

# 示例与用法

在 `eth2` 上启用类 I 设备

```
lldptool -T - i eth2 -V enabletablex=class1
```

查询 `eth2` med 状态

```
lldptool -t - i eth2 -V enabletablex
```

查询 `eth2` medPolicy

```
lldptool -t - i eth2 -V medPolicy
```

# 来源

媒体终端设备链路层发现协议 (ANSI-TIA-1057_final.pdf)

# 注意事项

`lldptool(8), lldpad(8)`

# 另

`lldptool(8), lldpad(8)`

# lldptool

> 名称

PFC - 显示 / 操控 PFC TLV

## 概要

```
lldptool -t - i ethx -V PFC -c enableTx
lldptool -T - i ethx -V PFC -c enableTx={yes|no}
lldptool -t - i ethx -V PFC -c mode
lldptool -T - i ethx -V PFC -c mode=<mode>,<mgrid>,<typeid>,<typeversion>,<instanceid>,<mac>,<vlan>
lldptool -t - i ethx -V PFC -c role
lldptool -T - i ethx -V PFC -c role=[station|bridge]
```

## 描述

PFC TLV 用于显示 PFC。

# 参数

`enableTx`

启用 TLV 传输

`willing`

显示或设置愿意（willing）属性。

`enabled`

显示或设置优先级。

`delay`

显示或设置延迟属性。

# 工作原理

PFC TLV 使用对称状态机。如果愿意位被设置为 1，则使用对方属性。如果愿意位被设置为 0，则使用本地属性。当对方和本地都愿意时，将使用决胜方案。

# 示例与用法

在 `eth2` 上为优先级 1、2 和 4 启用 PFC

```
lldptool -T - i eth2 -V enabled=1,2,4
```

在 `eth2` 上禁用所有优先级的 PFC

```
lldptool -T - i eth2 - enabled=none
```

显示 `eth2` 启用 PFC 配置

```
lldptool -t - i eth2 -V PFC -c enabled
```

显示 `eth2` 最后的 PFC TLV

```
lldptool -t - i eth2 -V PFC
```

# 来源

IEEE 802.1Qaz (http://www.ieee802.org/1/pages/dcbridges.html)

# 注意事项

由于硬件缓冲区满导致帧丢弃。

# 另

`lldptool(8), lldpad(8)`

## 作者

John Fastabend

# Ildptool

> 名称

vdp - 显示 / 操控 VDP TLV 配置

## 概要

```
lldptool -t - i ethx -V vdp -c enableTx
lldptool -T - i ethx -V vdp -c enableTx={yes|no}
lldptool -t - i ethx -V vdp -c mode
lldptool -T - i ethx -V vdp -c mode=<mode>,<mgrid>,<typeid>,<typeversion>,<instanceid>,<mac>,<vlan>
lldptool -t - i ethx -V vdp -c role
lldptool -T - i ethx -V vdp -c role=[station|bridge]
```

VSI 发现协议 (VDP) *并不是 LLDP 意义上的 TLV*，而是一种用于管理站点与相邻交换机之间虚拟站接口 (VSIs) 关联与去关联的协议。VDP 使用 ECP 作为 VDP TLV 的传输载体。一个 ECP 帧可能包含多个 VDP TLV。每个 VDP TLV 均包含一个 VSI 的 `mode`、`typeid`、`version`、`instanceid`、`mac` 和 `vlan`。

# 参数

`enableTx`
启用或禁用 VDP

`mode`
显示或设置具有以下参数的 VSI 模式：

- `<mode>`
`mode` (0=预关联, 1=带 RR 的预关联, 2=关联, 3=去关联)
- `<mgrid>`
管理器（数据库）id
- `<typeid>`
VSI 类型 id
- `<version>`
VSI 类型 id 版本
- `<instanceid>`
VSI 实例 id
- `<format>`
VDP 过滤器信息格式
- `<mac>`
VSI mac 地址
- `<vlan>`
VSI vlan id

`role`
显示或设置本地机器作为站点（默认）或桥接器的角色。

# 工作原理

VDP 协议用于对 VSI 与相邻交换机进行预关联、关联或去关联。关于 VSI 的信息被格式化为 VDP TLV，然后交给 ECP 进行底层传输。每个 ECP 帧可能包含多个 VDP TLV。

`lldpad` 中存在接收 VSI 两种方法：通过 `netlink` 或使用 `lldtool`。`libvirt` 使用 `netlink` 将 VSIs 通信到 `lldpad`。可以使用 `lldtool` 从命令行关联/去关联 VSIs。这对于对于测试目的非常有帮助。

# 示例与用法

显示 `eth8` 上是否启用了 vdp

```
ldptool -t -i eth8 -V vdp -c enableTx
```

在 `eth8` 上启用 vdp

```
ldptool -T -i eth8 -V vdp -c enableTx=yes
```

显示 `eth8` 当前配置的 VSIs

```
lldptool -t -i eth8 -V vdp -c mode
```

在 `eth8` 上关联一个 VSI

```
lldptool -T -i eth0 -V vdp -c mode=2,12,1193046,fa9b7fff-b0a0-4893-8e0e-beef4ff188f,2,52:54:00:C7:3E:CE,3
```

显示 `eth8` 上本地配置的 VDP 角色

```
lldptool -t -i eth8 -V vdp -c role
```

在 `eth8` 上设置 VDP 的本地角色

```
lldptool -T -i eth8 -V vdp -c role=bridge
```

# 来源

IEEE 802.1Qbg (http://www.ieee802.org/1/pages/802.1bg.html)

## 注意

目前 `lldpad` 中的代码反映了即将发布的标准草案 0。线上的 ECP/VDP TLV 可以使用 `wireshark > v1.8` 进行解码。

# 参见

`lldptool-evb(8), lldptool(8), lldpad(8)`

## 作者

Jens Osterkamp

# lldptool

# > 名称

`lldptool` - 管理 `lldpad` 的 LLDP 设置和状态

# 语法

```
lldptool <command> [options] [argument]
```

## 描述

`lldptool` 用于查询和配置 `lldpad`。它连接到 `lldpad` 的客户端接口以执行这些操作。如果执行时不带有 `command`，`lldptool` 将以交互模式运行。在交互模式下，`lldptool` 还作为事件监听器，在从 `lldpad` 异步接收事件时打印它们。在可用时，它将使用 `libreadline` 进行交互式输入。

## 选项

- `- i [ifname]`
指定命令适的网络接口。大多数 `lldtool` 命令都需要指定网络接口。

- `- V [tvid]`
指定 TLV 标识符。`tvid` 是用于识别特定 LLDP TLV 的整数值。对于类型不等于 127（组织特定类型）的类型，`tvid` 是 Type 值。对于组织特定的 TLV，`tvid` 是由 3 字节 OUI 和 1 字节子类型表示的值——子类型是 `tvid` 的低位字节。`tvid` 可以以数值（例如 10 或 0xa）输入，或者对于受支持的 TLV，作为关键字输入。查看 `lldtool` 帮助输出以查看支持的 TLV 关键字列表。

- `-n`
对于可以使用它的命令的“neighbor”（邻居）选项（例如，`get-tlv`）

- `- g [bridge scope]`
指定命令操作的桥接范围。允许对 "nearest_bridge"（简写: "nb"）、"nearest_customer_bridge" ("ncb") 和 "nearest_ntmppr_bridge" ("ntmpprb") 组地址设置并查询所有 LLDP TLV 模块。配置保存存在 `lldpad.conf` 的独立章节中。如果未为 "nearest bridge" 提供桥接范围，则保留之前的行为。

- `- c <argument list>`
用于 TLV 查询的“config”（配置）选项。表示查询是指定 TLV 的配置元素。参数列表指定要查询的特定元素。如果没有列出参数，则返回 TLV 的所有配置元素。

- `-r`
显示原始客户端

- `-R`
显示原始客户端消息

# 命令

- `license`
- `h`
- `v`
- `S`
- `t`
- `T`
- `l`
- `p`
- `q`

# 参数

`lldpad` 中的代码反映了即将发布的标准草案 0。线上的 ECP/VDP TLV 可以使用 `wireshark > v1.8` 进行解码。

VDP 协议用于对 VSI 与相邻交换机进行预关联、关联或去关联。关于 VSI 的信息被格式化为 VDP TLV，然后交给 ECP 进行底层传输。每个 ECP 帧可能包含多个 VDP TLV。

`lldpad` 中存在接收 VSI 两种方法：通过 `netlink` 或使用 `lldtool`。`libvirt` 使用 `netlink` 将 VSIs 通信到 `lldpad`。可以使用 `lldtool` 从命令行关联/去关联 VSIs。这对于测试目的非常有帮助。

VSI 发现协议 (VDP) *并不是 LLDP 意义上的 TLV*，而是一种用于管理站点与相邻交换机之间虚拟站接口 (VSIs) 关联与去关联的协议。VDP 使用 ECP 作为 VDP TLV 的传输载体。一个 ECP 帧可能包含多个 VDP TLV。每个 VDP TLV 均包含一个 VSI 的 `mode`、`typeid`、`version`、`instanceid`、`mac` 和 `vlan`。

`enableTx`
启用或禁用 VDP

`mode`
显示或设置具有以下参数的 VSI 模式：

- `<mode>`
`mode` (0=预关联, 1=带 RR 的预关联, 2=关联, 3=去关联)
- `<mgrid>`
管理器（数据库）id
- `<typeid>`
VSI 类型 id
- `<version>`
VSI 类型 id 版本
- `<instanceid>`
VSI 实例 id
- `<format>`
VDP 过滤器信息格式
- `<mac>`
VSI mac 地址
- `<vlan>`
VSI vlan id

`role`
显示或设置本地机器作为站点（默认）或桥接器的角色。

# 工作原理

VDP 协议用于对 VSI 与相邻交换机进行预关联、关联或去关联。关于 VSI 的信息被格式化为 VDP TLV，然后交给 ECP 进行底层传输。每个 ECP 帧可能包含多个 VDP TLV。

`lldpad` 中存在接收 VSI 两种方法：通过 `netlink` 或使用 `lldtool`。`libvirt` 使用 `netlink` 将 VSIs 通信到 `lldpad`。可以使用 `lldtool` 从命令行关联/去关联 VSIs。这对于测试目的非常有帮助。

VSI 发现协议 (VDP) *并不是 LLDP 意义上的 TLV*，而是一种用于管理站点与相邻交换机之间虚拟站接口 (VSIs) 关联与去关联的协议。VDP 使用 ECP 作为 VDP TLV 的传输载体。一个 ECP 帧可能包含多个 VDP TLV。每个 VDP TLV 均包含一个 VSI 的 `mode`、`typeid`、`version`、`instanceid`、`mac` 和 `vlan`。

# 示例与用法

显示 `eth8` 上是否启用了 vdp

```
ldptool -t -i eth8 -V vdp -c enableTx
```

在 `eth8` 上启用 vdp

```
lldptool -T -i eth8 -V vdp -c enableTx=yes
```

显示 `eth8` 当前配置的 VSIs

```
lldptool -t -i eth8 -V vdp -c mode
```

在 `eth8` 上关联一个 VSI

```
lldptool -T -i eth0 -V vdp -c mode=2,12,1193046,fa9b7fff-b0a0-4893-8e0e-beef4ff188f,2,52:54:00:C7:3E:CE,3
```

显示 `eth8` 上本地配置的 VDP 角色

```
lldptool -t -i eth8 -V vdp -c role
```

在 `eth8` 上设置 VDP 的本地角色

```
lldptool -T -i eth8 -V vdp -c role=bridge
```



# 来源

IEEE 802.1Qbg (http://www.ieee802.org/1/pages/802.1bg.html)

## 注意

目前 `lldpad` 中的代码反映了即将发布的标准草案 0。线上的 ECP/VDP TLV 可以使用 `wireshark > v1.8` 进行解码。

## 参见

`lldptool-evb(8)`, `lldptool(8)`, `lldpad(8)`

## 作者

Jens Osterkamp

# lldptool

## 名称

`lldptool` - 管理 `lldpad` 的 LLDP 设置和状态

## 语法

```
lldptool <command> [options] [argument]
```

## 描述

`lldptool` 用于查询和配置 `lldpad`。它连接到 `lldpad` 的客户端接口以执行这些操作。如果执行时不带有 `command`，`lldptool` 将以交互模式运行。在交互模式下，`lldptool` 还作为事件监听器，在从 `lldpad` 异步接收事件时打印它们。在可用时，它将使用 `libreadline` 进行交互式输入。

## 选项

- `-i [ifname]`
  指定命令适的网络接口。大多数 `lldtool` 命令都需要指定网络接口。
- `-V [tvid]`
  指定 TLV 标识符。`tvid` 是用于识别特定 LLDP TLV 的整数值。对于类型不等于 127（组织特定类型）的类型，`tvid` 是 Type 值。对于组织特定的 TLV，`tvid` 是由 3 字节 OUI 和 1 字节子类型表示的值——子类型是 `tvid` 的低位字节。`tvid` 可以以数值（例如 10 或 0xa）输入，或者对于受支持的 TLV，作为关键字输入。查看 `lldtool` 帮助输出以查看支持的 TLV 关键字列表。
- `-n`
  对于可以使用它的命令的“neighbor”（邻居）选项（例如，`get-tlv`）
- `-g [bridge scope]`
  指定命令操作的桥接范围。允许对 "nearest_bridge"（简写: "nb"）、"nearest_customer_bridge" ("ncb") 和 "nearest_ntmppr_bridge" ("ntmpprb") 组地址设置并查询所有 LLDP TLV 模块。配置保存存在 `lldpad.conf` 的独立章节中。如果未为 "nearest bridge" 提供桥接范围，则保留之前的行为。
- `-c <argument list>`
  用于 TLV 查询的“config”（配置）选项。表示查询是指定 TLV 的配置元素。参数列表指定要查询的特定元素。如果没有列出参数，则返回 TLV 的所有配置元素。
- `-r`
  显示原始客户端
- `-R`
  显示原始客户端消息

# 命令

- `license`
- `h`
- `v`
- `S`
- `t`
- `T`
- `l`
- `p`
- `q`

# 参数

（此处后续为原文重复内容，已根据指令要求进行翻译对齐处理）

## 另参

`lldptool-dcbx(8)`, `lldptool-ets(8)`, `lldptool-pfc(8)`, `lldptool-app(8)`, `lldptool-med(8)`, `lldptool-vdp(8)`, `lldptool-evb(8)`, `lldptool-evb22(8)`, `dcbtool(8)`, `lldpad(8)`

# 版权

`lldtool` - LLDP 代理配置工具 Copyright(c) 2007-2012 Intel Corporation. `lldptool` 的部分基于：
`hostapd-0.5.7`
Copyright

(c) 2004-2008, Jouni Malinen <j@w1.fi>

# 许可证

本程序是自由软件；你可以根据自由软件基金会发布的《通用公共许可证》第 2 版的条款和条件对其进行分发和/或修改。

本程序的分发是希望它有用，但**不提供任何保证**；甚至对商品性或特定用途的适用性没有隐含保证。更多详情请参阅《通用公共许可证》。

你应当随本程序收到了一份《通用公共许可证》的副本；如果没有，请写信至：Free Software Foundation, Inc., 51 Franklin St - Fifth Floor, Boston, MA 02110-1301 USA。

完整的《通用公共许可证》包含在此分发包的名为“COPYING”的文件中。

# 支持

联系方式：`open-lldp` 邮件列表 <lldp-devel@open-lldp.org>

# SMTP

## 概要

```
smtp [generic Postfix daemon options]
```



## 描述

Postfix SMTP+LMTP 客户端实现了 SMTP 和 LMTP 邮件投递协议。它处理来自队列管理器的消息投递请求。每个请求都指定了队列文件、发送者地址、投递的域名或主机以及接收者信息。该程序期望从 `master(8)` 进程运行。

SMTP+LMTP 客户端会更新队列文件并将接收者标记为已完成，或者通知队列管理器稍后重试投递。投递状态报告将根据情况发送到 `bounce(8)`、`defer(8)` 或 `trace(8)` 守护进程。

SMTP+LMTP 客户端会查找目标主机的邮件交换地址列表，按优先级排序，并连接到列出的每个地址，直到找到有响应的服务器为止。

当服务器不可用或由于可恢复错误状况导致邮件投递失败时，SMTP+LMTP 客户端将尝试将邮件投递到备用主机。

在邮件事务成功后，连接可能会保存到 `scache(8)` 连接缓存服务器，以便任何 SMTP+LMTP 客户端在后续事务中使用它。

默认情况下，对于活动队列中存在大量邮件的目的，会临时启用连接缓存。可以为特定目的永久启用连接缓存。

# SMTP 目的语法

SMTP 目的具有以下形式：

`domainname`
`domainname:port`

查找指定域名的邮件更改器，并连接到指定的端口（默认：`smtp`）。
`[hostname]`
`[hostname]:port`

查找指定主机的地址（地址），并连接到指定的端口（默认：`smtp`）。
`[address]`
`[address]:port`

连接到指定地址的主机，并连接到指定的端口（默认：`smtp`）。IPv6 地址必须格式化为 `[ipv6:address]`。

# LMTP 目的语法

LMTP 目的具有以下形式：

`unix:pathname`
连接到绑定到指定路径的本地 UNIX 域服务器。如果进程在 chroot 环境下运行，则绝对路径将相对于 Postfix 队列目录进行解释。

`inet:hostname`

`inet:hostname:port`

`inet:[address]`

`inet:[address]:port`

连接到指定本地或远程主机上的指定端口。如果没有指定端口，则连接到 `services(4)` 中定义为 `lmtp` 的端口。如果未找到此类服务，将使用 `lmtp_tcp_port` 配置参数（默认值为 24）。IPv6 地址必须格式化为 `[ipv6:address]`。

# 安全

SMTP+LMTP 客户端对安全具有中等敏感。它与网络上的 SMTP 或 LMTP 服务器以及 DNS 服务器通信。SMTP+LMTP 客户端可以在固定的低权限下以 chroot 运行。

# 标准

`RFC 821` (SMTP 协议) `RFC 822` (ARPA 互联网文本消息) `RFC 1651` (SMTP 服务扩展) `RFC 1652` (8bit-MIME 传输) `RFC 1870` (消息大小声明) `RFC 2033` (LMTP 协议) `RFC 2034` (SMTP 增强错误代码) `RFC 2045` (MIME: 互联网消息体格式) `RFC 2046` (MIME: 媒体类型) `RFC 2554` (AUTH) `RFC 2821` (SMTP 协议) `RFC 2920` (SMTP 管道化) `RFC 3207` (STARTTLS) `RFC 3461` (DSN) `RFC 3463` (增强状态码) `RFC 4954` (AUTH) `RFC 5321` (SMTP 协议)

# 诊断

问题和事务被记录到 `syslog(8)`。

根据 `notify_classes` 的设置，管理员将收到退信（bounces）的通知。

# 缺陷

SMTP+LMTP 连接缓存与 TLS 不兼容。

SMTP+LMTP 连接缓存假设 SASL 凭据有效。

# 配置参数

在 Postfix 2.3 版本之前，`smtp_xxx` 参数在 SMTP 中具有部分可用功能。

本文仅描述不简单的与 LMTP 相关的参数。

下文仅提供摘要。示例请参阅 `postconf(5)`。

# 兼容性控制

`ignore_mx_lookup_error` (no)
忽略没有响应的 DNS 查询。

`smtp_always_send_ehlo` (yes)
在 SMTP 会话开始始终发送 EHLO。

`smtp_never_send_ehlo` (no)
在 SMTP 会话开始从不发送 EHLO。

`smtp_defer_if_no_mx_address` (no)
当 MX 记录解析为 IP 地址时延迟投递。

`smtp_line_length_limit` (998)
Postfix 将的消息头部和正文最大长度。

`smtp_pix_workaround_delay_time` (10s)
Postfix 暂停的时间。

`smtp_pix_workaround_threshold` (500s)
在开启 smtp fixup 的防火墙之前，队列需要多长时间。

`smtp_pix_workarounds` (disable_delay_ctrl)
指定 CISCO 防火墙解决方案的列表。

`smtp_pix_workaround_maps` (empty)
按远程 SMTP 地址索引的查找表，包含针对特定目的 CISCO PIX 防火墙的解决方案。

`smtp_quote_rfc5321_envelope` (yes)
按照 RFC 5321 要求对 Postfix SMTP 客户端 MAIL FROM 和 RCPTO 命令中的地址加引号。

`smtp_reply_filter` (empty)
逐行转换远程 SMTP 服务器回复的机制。

`smtp_skip_5xx_greeting` (yes)
跳过以 5XX 状态码打招呼的 SMTP 服务器。

`smtp_skip_quit_response` (yes)
等待 Postfix QUIT 命令的响应。

适用于 Postfix 2.0 及更版本：

`smtp_skip_4xx_greeting` (yes)
跳过以 4XX 状态码打招呼的 SMTP 服务器。

适用于 Postfix 2.2 及更高版本：

`smtp_discard_ehlo_keyword_address_maps` (empty)
按远程 SMTP 服务器地址索引的查找表，包含 Postfix SMTP 客户端忽略的 EHLO 关键字（pipelining, strttls, auth 等）。

将忽略来自远程 SMTP 服务器的 EHLO 响应。

## `smtp_discard_ehlo_keywords` (空)

一个不区分大小写的 EHLO 关键字列表（pipelining, startles, auth 等），Postfix SMTP 客户端将从来自远程 SMTP 服务器的 EHLO 响应中忽略这些关键字。

## `smtp_generic_maps` (空)

一个可选的查找表，用于在 Postfix SMTP 客户端中执行地址重写，通常用于在跨 Internet 发送邮件时将本地有效地址转换为全局有效地址。

在 Postfix 2.2.9 及更高版本可用：

## `smtp_cname_overrides_servername` (取决于版本)

允许 DNS CNAME 记录覆盖 Postfix SMTP 客户端用于日志、SASL 密码查找、TLS 策略决策或 TLS 证书验证时使用的服务器名称（servername）。

在 Postfix 2.3 及更高版本中可用：

## `lmtp_discard_lhlo_keyword_address` (空)

以 LMTP 服务器地址为索引的查找表，其中包含不区分大小写的 LHLO 关键字列表（pipelining, startles, auth 等），Postfix LMTP 客户端将从来自远程 LMTP 服务器的 LHLO 响应中忽略这些关键字。

## `lmtp_discard_lhlo_keywords` (空)

一个不区分大小写的 LHLO 关键字列表（pipelining, startles, auth 等），Postfix LMTP 客户端将从来自远程 LMTP 服务器的 LHLO 响应中忽略这些关键字。

在 Postfix 2.4.4 及更高版本可用：

## `send_cyrus_sasl_authzid` (否)

当使用默认设置“no”向远程 SMTP 或 LMTP 服务器进行验证时，不发送 SASL 身份 ID (authzid)；仅发送 SASL 身份 ID (authcid) 以及客户端密码。

在 Postfix 2.5 及更高版本中可用：

## `smtp_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `header_checks(5)` 表。

## `smtp_mime_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `mime_header_checks(5)` 表。

## `smtp_nested_header_checks` (空)

用于 Postfix SMTP 客户端的受限 `nested_header_checks(5)` 表。

## `smtp_body_checks` (空)

用于 Postfix SMTP 客户端的受限 `body_checks(5)` 表。

在 Postfix 2.6 及更高版本可用：

## `tcp_windowsize` (0)

针对破坏 TCP 窗口缩放的路由器的可选变。

在 Postfix 2.8 及更高版本中可用：

## `smtp_dns_resolver_options` (空)

用于 Postfix SMTP 客户端的 DNS 解析器选项。
在 Postfix 2.9 及更高版本可用：

## `smtp_per_record_deadline` (否)

更改 `smtp_*timeout` 限制的行为，从每次读取或写入系统调用的时间限制更改为发送或接收完整记录（一个 SMTP 命令行、SMTP 响应行、SMTP 消息内容行或 TLS 协议消息）的时间限制。

## `smtp_send_dummy_mail_auth` (否)

是否在 SASL 验证的 SMTP 会话中向 MAIL FROM 命令中追加 "AUTH<=>" 选项。

# MIME 处理控制

在 Postfix 2.0 及更高版本可用：

`disable_mime_output_conversion` (否)
禁用 8BITIME 格式到 7BIT 格式的转换。

`mime_boundary_length_limit` (2048)
MIME 多部分边界字符串的最大长度。

`mime_nesting_limit` (100)
MIME 解析器处理的最大递归深度。

# 外部内容检查

在 Postfix 2.1 及更高版本可用：
`smtp_send_xforward_command` (否)

当 Postfix SMTP 服务器的 EHLO 响应宣布支持 XFORWARD 时，发送非标准的 XFORWARD 命令。

# SASL 验证控制

`smtp_sasl_auth_enable` (否)
在 Postfix SMTP 客户端中启用 SASL 验证。

`smtp_sasl_password_maps` (空)
可选的 Postfix SMTP 客户端查找表，每个远程主机名或域名对应一个用户名:密码 条目，或者在启用了发送者相关验证时对应一个发送者地址。

`smtp_sasl_security_options` (noplaintext, anonymous)
Postfix 客户端 SASL 安全选项；从 Postfix 2.3 开始，可用功能列表取决于通过 `smtp_sasl_type` 选择的 SASL 客户端实现。

在 Postfix 2.2 及更高版本可用：

`smtp_sasl_mechanism_filter` (空)
如果为空，则是一个 Postfix SMTP 客户端过滤器，用于过滤远程 SMTP 服务器提供的 SASL 机制列表。

在 Postfix 2.3 及更高版本中可用：

`smtp_sender_dependent_authentication` (否)
在 Postfix SMTP 客户端中启用发送者相关验证；这仅在使用 SASL 验证可用，并且会禁用 SMTP 连接缓存以确保来自不同发送者的邮件使用适当的凭据。

`smtp_sasl_path` (空)
Postfix SMTP 客户端传递给 SASL 插件实现的特定实现信息，该实现是通过通过 `smtp_sasl_type` 选择的。

`smtp_sasl_type` (cyrus)
Postfix SMTP 客户端用于验证时应使用的 SASL 插件。

在 Postfix 2.5 及更高版本中可用：

`smtp_sasl_cache_name` (空)
一个可选的表，用于防止与相同的远程 SMTP 主机名、用户名和密码重复发生 SASL 验证失败。

`smtp_sasl_cache_time` (90)
SASL 缓存的有效期。

`smtp_sasl_soft_bounce` (yes)
当远程 SMTP 服务器拒绝 SASL 验证时退回邮件。

在 Postfix 2.9 及更高版本可用：

`smtp_send_dummy_mail_auth` (否)
是否在 SASL 验证的 SMTP 会话中向 MAIL FROM 命令中追加 “AUTH<=>” 选项。

# STARTTLS 支持

关于 STARTTLS 的详细信息请参考 README。

`smtp_tls_security_level` (空)
Postfix SMTP 客户端使用的 TLS 安全级别；当指定为空时，将使用过时的 `smtp_tls`。

用于用于 TLS 加密 SMTP 会话的 Postfix 客户端 TLS 选项。

`smtp_tls_starttls_timeout` (300)
TLS 启动期间的时间限制。

`smtp_tls_ca` (空)
包含受信任 CA 的证书文件。

`smtp_tls_path` (空)
用于验证远程 SMTP 服务器的证书目录。

`smtp_tls_cert_file` (空)
Postfix SMTP 客户端使用的 PEM 格式证书。

`smtp_tls_mandatory_ciphers` (medium)
Postfix SMTP 客户端使用的强制 TLS 等。

`smtp_tls_exclude_ciphers` (空)
Postfix SMTP 客户端中排除的加密类型。

`smtp_tls_mandatory_exclude_ciphers` (空)
Postfix SMTP 客户端中排除的加密类型。

`smtp_tls_dcert_file` (empty)
Postfix SMTP 客户端使用的 DSA 证书。

`smtp_tls_dkey_file` (empty)
Postfix SMTP 客户端使用的 DSA 密钥。

`smtp_tls_key_file` (empty)
Postfix SMTP 客户端使用的 RSA 密钥。

`smtp_tls_loglevel` (empty)
启用额外的 TLS 日志。

`smtp_tls_note_starttls` (否)
记录启用 TLS 的远程 SMTP 服务器主机名。

`smtp_tls_policy_maps` (空)
带有目的地的 TLS 策略查找表；当指定不为空时，覆盖过时的 `smtp_tls_per_site`。

`smtp_tls_mandatory_protocols` (!SSLv2)
Postfix SMTP 客户端使用的强制 SSL/TLS 协议列表。

`smtp_tls_scert_verifydepth` (9)
SMTP 证书验证深度。

`smtp_tls_secure_match` (nextthop, dot-nextthop)
Postfix SMTP 客户端在“secure”级别验证证书。

`smtp_tls_session_cache_database` (empty)
包含可选客户端缓存的文件名。

`tls_session_cache_timeout` (3600s)
客户端缓存的过期时间。

`smtp_tls_verify_match` (hostname)
Postfix SMTP 客户端在“verify”级别验证证书。

`tls_daemon_random_bytes`(32)
`smtp(8)` 或 `smtpd(8)`进程向 `tlsmgr(8)` 服务器请求的伪随机字节数，用于种子其内部随机数生成器 (PRNG)。

`tls_high_cipherlist` (ALL:EXPORT!MEDIUM:+RC4@STRENGTH)
“HIGH”级加密。

`tls_medium_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“MEDIUM”级或更高级别的加密。

`tls_low_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“LOW”级或更高级别的加密。

`tls_export_cipherlist` (ALL:EXPORT:+RC4@STRENGTH)
“EXPORT”级或更高级别的加密。

`tls_null_cipherlist` (eNULL!:aNULL)
提供身份验证但不加密的“NULL”级加密。

在 Postfix 2.4 及更高版本可用：

`smtp_sasl_tls_verified_security_options` ($smtp_sasl_security_options)
用于具有已验证服务器证书的 TLS 加密 SMTP 会话的 SASL 验证选项。

在 Postfix 2.5 及更高版本可用：

`smtp_tls_fingerprint_cert_match` (空)
“fingerprint”TLS 安全级别允许的远程服务器证书指纹列表 (`smtp_tls_security_level` = fingerprint)。

`smtp_tls_fingerprint_digest` (md5)
用于构建 SMTP 服务器证书指纹的消息摘要算法。

指纹。

在 Postfix 2.6 及更高版本可用：
`smt_tls_protocols` (!SSLv2)

- Postfix SMTP 客户端在使用机会性 TLS加密时将排除或包含的 TLS 协议列表。

`smtp_tls_ciphers` (export)
Postfix SMTP 客户端在使用机会性 TLS加密时使用的最小 TLS 密套等级。

`smtp_tls_eccert_file` (empty)
包含 PEM 格式的 Postfix SMTP 客户端 ECDSA 证书的文件。

`smtp_tls_eckey_file` (Smtp_tls_eccert_file)
包含 PEM 格式的 Postfix SMTP 客户端 ECDSA 私钥的文件。

在 Postfix 2.7 及更高版本可用：
`smt_tls_block_early_mail_reply` (no)

- 尝试基于 TLS 协议漏洞（CVE-2009-35555）检测邮件劫持攻击，攻击者会在 Postfix SMTP 客户端的 TLS 会话中插入恶意的 HELO、MAIL、RCPT、DATA 命令。

在 Postfix 2.8 及更高版本可用：
`tls_disable_workarounds` (参见 ‘postconf -d’ 输出)

- 要禁用的 OpenSSL 错误变通方案列表或位掩码。

# 过时的 STARTTLS 控制

以下配置参数是为了兼容 2.3 之前的 Postfix 版本而存在的。这些支持将在未来的发布中移除。

**`smtp_use_tls` (no)**
机会性模式：当远程 SMTP 服务器宣布支持 STARTTLS 时使用 TLS，否则以明文形式发送邮件。

**`smtp_enforce_tls` (no)**
强制模式：要求远程 SMTP 服务器使用 TLS 加密，且从不明文发送邮件。

**`smtp_tls_enforce_peername` (yes)**
在强制 TLS 加密的情况下，要求远程 SMTP 服务器的主机名与远程 SMTP 服务器证书中的信息匹配。

**`smtp_tls_per_site` (empty)**
可选的查找表，根据下一跳目的地和远程 SMTP 服务器主机名定义 Postfix SMTP 客户端 TLS 使用策略。

**`smtp_tls_cipherlist` (empty)**
过时的 Postfix < 2.3 控制，用于控制 Postfix SMTP 客户端的 TLS 密套列表。

# 资源和速率控制

`smtp_destination_concurrency_limit` ($default_destination_concurrency_limit)
通过 smtp 消息传递传输向目标进行并行投递的最大数量。

`smtp_destination_recipient_limit` ($default_destination_recipient_limit)
smtp 传递传输每条消息允许的最大接收者数量。

`smtp_connect_timeout` (30s)
Postfix SMTP 客户端完成 TCP 连接的时间限制，或为 0（使用操作系统的内置时间限制）。

`smtp_helo_timeout` (30s)
Postfix SMTP 客户端发送 HELO 或 EHLO 命令以及接收远程 SMTP 服务器初始响应的时间限制。

`lmptp_lhlo_timeout` (30s)
Postfix LMTP 客户端发送 LHLO 命令以及接收远程 LMTP 服务器初始响应的时间限制。

`smtp_xforward_timeout` (30s)
Postfix SMTP 客户端发送 XFORWARD 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_mail_timeout` (30s)
Postfix SMTP 客户端发送 MAIL FROM 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_rcpt_timeout` (30s)
Postfix SMTP 客户端发送 SMTP RCPT 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_data_init_timeout` (120s)
Postfix SMTP 客户端发送 SMTP DATA 命令以及接收远程 SMTP 服务器响应的时间限制。

`smtp_data_xer_timeout` (180s)
Postfix SMTP 客户端发送 SMTP 邮件内容的时间限制。

`smtp_data_done_timeout` (600s)
Postfix SMTP 客户端发送 SMTP “.,,”以及接收远程 SMTP 服务器响应的时间限制。

`smtp_quit_timeout` (300s)
Postfix SMTP 客户端发送 QUIT 命令以及接收远程 SMTP 服务器响应的时间限制。

在 Postfix 2.1 及更高版本可用：

`smtp_mx_address_limit` (5)
Postfix SMTP 客户端查找邮件交换器后可能产生的 MX（邮件交换器）IP 地址的最大数量，或为 0（不限制）。

`smtp_mx_session_limit` (2)
Postfix 放弃之前的最大 SMTP 会话数。

`smtp_timeout` (20s)
Postfix SMTP 客户端发送 RSET 命令以及接收远程 SMTP 服务器响应的时间限制。

在 Postfix 2.2 及更高版本可用：
`ltmp_timeout` (empty)
Postfix 放弃之前的最大 LMTP 连接数。

`smtp_cache_on_demand` (yes)
临时启用 SMTP 缓存。

`smtp_time_limit` (300s)
Postfix 客户端保持开启的时间。

在 Postfix 2.3 及更高版本可用：
`smtp_connection_timeout` (5s)
SMTP 连接开启状态下的时间限制。

在 Postfix 2.7 及更高版本可用：
`smtp_tcp_port` (no)
SMTP 客户端连接的默认 TCP 端口。

在 Postfix 2.9 及更高版本可用：
`smtp_protocol_timeout` (30s)
Postfix SMTP 客户端建立或接收连接的时间限制。

# 故障排除控制

`debug_peer_level` (2)
当远程客户端或服务器匹配时，日志级别的增量。

`debug_peer_list` (empty)
导致调试日志级别增加的模式列表。

`error_notice` (postmaster)
邮件投递问题的通知接收者。

`internal_mail_filter` (empty)
哪些类邮件受内部过滤。

`notify_classes` (resource, software)
报告给 postmaster 的错误类别。

# 杂项控制

`best_mx_transport` (empty)
当 Postfix 检测到“返回自身”错误条件时，投递邮件的地方。

`config_directory` (参见 ‘postconf -d’ 输出)
main.cf 和 master.cf 配置文件的位置。

`daemon_timeout` (18000s)
Postfix 守护进程在处理请求时被守护计时器终止前允许的时间。

`delay_logging_resolution` (2)
记录秒级数值时，小数点后的最大位数。

`disable_dns_lookups` (no)
Postfix SMTP 和 LMTP 客户端中的 DNS 查找。

`inet_interfaces` (all)
该邮件系统接收的网络接口地址。

`inet_protocols` (all)
Postfix 在建立或接受连接时尝试使用的 Internet 协议。

`ipc_timeout` (3600s)
通过内部通道发送或接收信息的时间限制。

`ltmp_assume_final` (no)
当远程 LMTP 服务器不支持 DSN 时，假设执行最终投递，并将“已传递”状态通知为“已交付”。

`ltmp_tcp_port` (24)
SMTP客户端连接的默认 TCP 端口。

`max_idle` (100s)
空闲的 Postfix 守护进程在等待传入连接前被动终止前的最大等待时间。

`max_use` (100)
Postfix 守护进程在被动终止前服务的最大传入连接数。

`process_id` (read-only)
Postfix 命令或守护进程的进程标识符。

`process_name` (read-only)
Postfix 命令或守护进程的进程名称。

`proxy_interfaces` (empty)
通过代理或网络地址转换单元接收邮件的网络接口地址。

`smtp_address_preference` (any)
Postfix SMTP 客户端尝试的地址类型（“ipv6”、“ipv4”或“any”），

当一个目标同时具有 IPv6 和 IPv4 地址且 MX 偏好值相等时。

**`smtp_bind_address` (空)**

一个可选的数值地址，Postfix 客户端在建立 IPv4 连接时应绑定到该地址。

**`smtp_bind_address6` (空)**

一个可选的数值地址，Postfix 客户端在建立 IPv6 连接时应绑定到该地址。

**`smtp_helo_name` ($hostname)**

EHLO 或 HELO 命令中的主机名映射。

**`lmtp_lhlo_name` ($hostname)**

LMTP LHLO 命令中的主机名映射。

**`smtp_host_lookup` (dns)**

Postfix 客户端用于查找主机 IP 地址的机制。

**`smtp_randomize_addresses` (yes)**

随机化相同 MX 优先级的地址顺序。

**`syslog_facility` (mail)**

postconf -d 输出的 syslog 设施名。

**`syslog_name` (见‘postconf -d’)**

在 syslog 记录中附加的系统名称，例如“smtpd”变为“postfix/smtpd”。

**`fallback_relay` (空)**

对于找不到或无法访问的 SMTP 目标，可选的中继列表。适用于 Postfix 2.2 及早期版本。

**`smtp_fallback_relay` ($fallback_relay)**

对于找不到或无法访问的 SMTP 目标，可选的中继列表。适用于 Postfix 2.3 及更高版本。

## SEE ALSO

（见 postconf -d）

# README FILES

使用 `postconf readme_directory` 或 `postconf_directory` 查找此信息。

# LICENSE

Secure Mailer 许可随此软件分发。

# AUTHOR(S)

Wietse Venema IBM T. Watson Research Box 704 Yorktown Heights, NY 合作者：Jon Ribbons Oaktree Internet Solutions Ltd., Internet House, Canal Basin, Coventry, CV1LY, United Kingdom 最初支持：Till Franke SuSE Rhein/Main AG 65760 Eschborn, Germany 最初支持：Lutz Jaenicke Cottbus Allgemeine Elektrotechnik Universitaplatz-3-4 Cottbus, Germany 修订并支持：Victor Duchov Morgan Stanley

# LNSTAT

+ > NAME

instat - 统一 Linux 网络统计

## SYNOPSIS

instat [options]

## DESCRIPTION

本手册页简要介绍了 instat 命令。
**Instat** 是旧 rtstat 程序的通用且功能更完整的替代品。除了路由缓存统计，它还支持 Linux 内核通过 /proc/net/stat/ 提供的任何统计信息。

## OPTIONS

instat 支持以下选项：

- -h, --help 显示选项摘要。
- -V, --version 显示程序版本。
- -c, --count 打印 <count> 个间隔。
- -d, --dump 转储可用文件/键。
- -f, --file <file> 使用的统计文件。
- -i, --interval <intv> 将间隔设置为 ‘intv’ 秒。
- -k, --keys k,k,k... 仅指定的键。
- -s, --subject [0-2] 指定标题显示。“0’表示无标题，“1’在程序启动时打印标题，“2’每隔 20 行打印一次标题。
- -w, --width n,n,n… 每个字段的宽度。

# USAGE EXAMPLES

# instat -d 获取支持的统计文件列表。

# instat -k arp_cache:entries,rt_cache:in_hit,arp_cache:destroys 选择的文件和键。

# instat -i 10 使用 10 秒的间隔。

# instat -f ip_conrack 仅对指定文件进行统计。

# instat -s 0 完全不打印标题。

# instat -s 20 在启动时和每 20 行打印一次标题。

# instat -c -1 -i 1 -f rt_cache -k entries,in_hit,in_slow_tot 每秒显示字段 rt_cache 的键 entries、in_hit 和 in_slow_tot 的统计信息。

## SEE ALSO

ip(8)， 以及 /usr/share/doc/iproute-3.10.0/README.lnstat（Debian 中的 iproute-doc 包）

## AUTHOR

Instat 由 Harald Welte <laforge@gnumonks.org> 编写。

本手册页由 Michael Prokop <mika@grml.org> 为 Debian 项目编写（也可供使用）。

# LOAD_POLICY

+ > NAME

load_policy - 将新的 SELinux 策略加载到内核

## SYNOPSIS
```



# load_policy

`load_policy [-qi]`

## NAME

`load_policy` - 将新的 SELinux 策略加载到内核

## DESCRIPTION

`policy` 将安装的策略文件加载到内核。现有的策略值在策略重载时会被保留，而不是重置为策略文件中的默认值。

## OPTIONS

`-q` 抑制警告消息。
`-i` 初始化加载。仅在首次加载时使用（通常由 `initfs` 调用）。

## EXIT STATUS

`0` 成功
`1` 参数无效
`2` 策略失败
`3` 请求初始化

## SEE ALSO

`boolean` (8)

## AUTHORS

本手册页由 Dan Walsh <dwalsh@redhat.com> 编写。程序由 Stephen Smalley <sds@epoch.nc> 编写。

# LOADIMAP

## NAME

`loadunimap` - 加载内核字体表

## SYNOPSIS

```
loadunimap [C console ] [o oldmap ] [ map ]
```



## DESCRIPTION

`loadunimap` 命令已过——其功能现在包含在 `setfont` 中。为了兼容性仍然可用。

程序在内核字体表中加载指定的 map。如果没有 map，则假设为 `def`。默认扩展（可以省略）为 `.uni`。

如果给了 `-o oldmap` 选项，旧 map 保存到指定的文件中。

在 Linux 2.6.1 及更高版本上，可以使用 `-C` 指定控制台设备。

通常不会直接调用 `loadunimap` - 其功能也包含在 `setfont` 中。

## FILES

`/lib/kbd/unimaps` 是 映射的默认目录。

## SEE ALSO

`mapscrn(8)`, `setfont(8)`

# LOCAL

+ > NAME

`local` - Postfix 本地邮件投递

## SYNOPSIS

`local [generic Postfix daemon options]`

## DESCRIPTION

`local(8)` 进程处理来自队列管理器的本地接收者投递请求。每个请求指定队列文件、发送者地址、目标域名或主机以及一个或多个接收者。程序期望从 `master(8)` 进程管理器运行。

`local(8)` 进程更新队列文件并标记接收者为完成，或者通知队列管理器稍后重试。投递状态报告根据情况发送到 `bounce(8)`、`defer(8)` 或 `trace(8)` 守护进程。

# CASE FOLDING

所有投递决策都使用原始接收者名称（即地址本地部分），并转换为小写。请见下文的 ADDRESS EXTENSION 以了解少数例外。

# 系统级和用户级别名

系统管理员可以设置一个或多个系统级 sendmail 风格的别名数据库。用户可以拥有 sendmail 风格的 `~/.forward` 文件。发送给名的邮件将投递到别名、投递到 `~/.name/.forward` 中的目的地、投递到该用户名拥有的邮箱，或者作为无法投递邮件返回。

系统管理员可以通过 `forward_path` 配置参数指定由逗号/空格分隔的 `~/.forward` 文件列表。在投递时，本地投递代理会尝试列表中的每个路径，直到找到其中一个。

通过 `~/.forward` 文件的投递是以 Suser 的权限进行的。因此，`~/.forward` 文件必须对接收者可读，其父目录需要赋予接收者“执行”权限。

`forward_path` 参数支持 Suser（接收者用户名）、`$shell`（接收者 shell）、`$recipient`（完整收件者地址）、`$extension`（收件者地址扩展）、`$domain`（收件者域名）、`$local`（完整收件者本地部分）和 `$recipient_description` 的插值。`${name?value}` 和 `${value}` 格式在 `$name` 为（未定义）时会条件性扩展为 value。对 shell 或文件系统可能有特殊含义的字符将被下划线替换。可用字符列表由 `forward_expansion_filter` 配置参数指定。

别名或 `~/.forward` 文件可以列出外部命令、目标文件名、`:include:` 指令或邮件地址的任何组合。请参阅 `aliases(5)` 获取精确描述。用户 `.forward` 文件中的每行的语法与别名的右侧部分相同。

当在别名扩展中找到别名时，邮件将改为投递给该用户。当用户列在用户的 `~/.forward` 文件中时，邮件将投递到该用户的邮箱收件箱。一个空的 `~/.forward` 文件意味着不转发邮件。

为了防止邮件系统消耗过多的内存，来自 `:include:` 或 `~/.forward` 文件的输入记录会被拆分成长度为 `line_length_limit` 的块。

在扩展别名、`~/.forward` 等内容时，程序会尝试避免重复投递。`duplicate_filter_limit` 配置参数限制了记录的收件者数量。

# 邮件转发

为了可靠性，转发的邮件将作为新消息重新提交，以便每个收件者都有一个独立的磁盘投递状态记录。

为了尽早停止邮件转发循环，软件会添加一个可选的 `Delivered-To:` 头部，包含最终的信封接收者地址。如果邮件到达一个已列在 `Delivered-To:` 头部中的接收者，则消息将被退回。

# 邮箱投递

默认的每个用户的邮箱是 UNIX 堆栈目录中的一个文件 **`(var/mail/user 或 /var/spool/mail/user)`**；该位置可以通过 **`mail_spool_directory`** 配置参数指定。指定一个以 `/` 结尾的名称以进行兼容 qmail 的 maildir 投递。

或者，每个用户的邮箱可以是用户主目录下的一个文件，名称由 **`home_mailbox`** 配置参数指定。指定相对路径名。指定一个以 `/` 结尾的名称以进行兼容 qmail 的 maildir 投递。

邮箱投递可以委托 **`mailbox_command_maps`** 和 **`mailbox_command`** 配置参数指定的外部命令。该命令以接收者用户的权限执行（例外：不启用辅助组；当以 root 身份投递时）。

邮箱投递可以委托给 **`master.cf`** 文件中指定的替代消息传输。**`mailbox_transport_maps`** 和 **`mailbox_transport`** 配置参数指定了用于本地接收者的可选消息传输，无论它们是否在 UNIX passwd 数据库中找到。**`fallback_transport_maps`** 和 **`fallback_transport`** 参数指定了未在 `aliases(S)` 或 UNIX passwd 数据库中找到接收者的可选消息传输。

在 UNIX 风格的邮箱投递的情况下，**`local(8)`** 守护进程会在每条消息前添加一个“**发送者时间戳**”信封头部，在前面添加一个包含接收者地址的 **`X-Original-To:`** 头部，前面添加一个可选的 **`Delivered-To:`** 头部（包含最终信封接收者地址），前面添加一个包含信封发送者地址的 **`Return-Path:`** 头部，在“From ”开头的行前添加 `>` 字符，并追加一个空行。投递过程中邮箱会被锁定以进行独占访问。如果发生问题，将尝试将邮箱截断为原始长度。

在 **`maildir`** 投递的情况下，本地守护进程会在消息前添加一个可选的 **`Delivered-To:`** 头部（包含最终信封接收者地址），在前面添加一个传递给 Postfix 的接收者地址的 **`X-Original-To:`** 头部，并在前面添加一个包含信封发送者地址的 **`Return-Path:`** 头部。

# 外部命令投递

`allow_mail_to_commands` 配置参数限制了投递到外部命令。默认设置（alias, forward）禁止 `:include:` 文件中的命令目标。

可选地，进程的工作目录将更改为 `command_execution_directory` 指定路径（Postfix 2.2 及更高版本）。更改目录失败将导致投递推迟。

`command_execution_directory` 参数值支持 `$User`（接收者用户名）、`$Home`（接收者主目录）、`$shell`（接收者 shell）、`$recipient`（客户端接收者地址）、`$extension`（收件者地址扩展）、`$domain`（收件者域名）、`$Local`（完整收件者本地部分）和 `$Recipient_delimiter` 的插值。`${name?value}` 和 `${value}` 格式在 `$name` 为（未定义）时会条件性扩展为 value。对 shell 或文件系统可能有特殊含义的字符将被下划线替换。可用字符列表由 `forward_expansion_filter` 配置参数指定。

别名或 `~/.forward` 文件可以列出外部命令、目标文件名、`:include:` 指令或邮件地址的任何组合。请参阅 `aliases(5)` 获取精确描述。用户 `.forward` 文件中的每行的语法与别名的右侧部分相同。

当在别名扩展中找到别名时，邮件将改为投递给该用户。当用户列在用户的 `~/.forward` 文件中时，邮件将投递到该用户的邮箱收件箱。一个空的 `~/.forward` 文件意味着不转发邮件。

为了防止邮件系统消耗过多的内存，来自 `:include:` 或 `~/.forward` 文件的输入记录会被拆分成长度为 `line_length_limit` 的块。

在扩展别名、`~/.forward` 等内容时，程序会尝试避免重复投递。`duplicate_filter_limit` 配置参数限制了记录的收件者数量。

- `$User`: 接收者用户名
- `$Home`: 接收者主目录
- `$shell`: 接收者 shell
- `$recipient`: 客户端接收者地址
- `$extension`: 收件者地址扩展
- `$domain`: 收件者域名
- `$Local`: 完整收件者本地部分
- `$Recipient_delimiter`

- `$SHELL`: 接收者的登录 shell
- `$HOME`: 接收者的主目录
- `$USER`: 接收者用户名
- `$EXTENSION`: 可选收件者地址扩展
- `$DOMAIN`: 收件者域名部分
- `$LOGNAME`: 接收者用户名
- `$LOCAL`: 接收者地址本地部分（@ 左侧的文本）
- `$ORIGINAL_RECIPIENT`: 重写或别名之前的接收者地址（Postfix 2.5 及更高版本）
- `$RECIPIENT`: 完整接收者地址
- `$SENDER`: 完整发送者地址

- `$CLIENT_ADDRESS`: 客户端网络地址。Postfix 2.2 起可用。
- `$CLIENT_HELO`: 客户端 EHLO 命令参数。Postfix 2.2 起可用。
- `$CLIENT_HOSTNAME`: 客户端主机名。Postfix 2.2 起可用。
- `$CLIENT_PROTOCOL`: 客户端协议。Postfix 2.2 起可用。
- `$SASL_METHOD`: 客户端 AUTH 命令指定的 SASL 认证方法。Postfix 2.2 起可用。
- `$SASL_SENDER`: 客户端 MAIL FROM 命令指定的 SASL 发送者地址。Postfix 2.2 起可用。
- `$SASL_USERNAME`: 客户端 AUTH 命令指定的 SASL 用户名。Postfix 2.2 起可用。

`PATH` 环境变量始终被重置为系统相关的默认路径，通过由未更改名称保护的 `export_environment` 配置变量来实现。

当前工作目录是邮件队列目录。

`local(8)` 守护进程会在每条消息前添加一个“From sender 时间戳”信封头部，在前面添加一个包含传递给 Postfix 的接收者地址的 `X-Original:` 头部，前面添加一个可选的 `Delivered-To:` 头部（包含最终信封接收者地址），前面添加一个包含信封发送者地址的 `Return-Path:` 头部，且不追加空行。

# 外部文件投递

投递格式取决于目标文件名语法。默认使用 UNIX 风格的邮箱格式。指定以 `/` 结尾的名称以进行兼容 qmail 的 **`maildir`** 投递。

**`allow_mail_to_files`** 配置参数限制向外部文件的投递。默认设置（**`alias, forward`**）禁止在 **`:include`** 中使用文件目标。

在 UNIX 风格的邮箱投递的情况下，**`local(8)`** 守护进程会在传递给 Postfix 的收件人地址之前添加一个 **“From sender time_stamp”** 信封头部，添加一个带有最终收件人信封地址的可选 **`Delivered-To:`** 头部，在以“From ”开头的行之前添加 `>` 字符，并追加一个空行。信封发件人地址可以在 **`Return-Path:`** 头部获取。当目标是普通文件时，在投递过程中将对其锁定进行单独访问。如果发生问题，将尝试将普通文件截断为原始长度。

在 **`maildir`** 投递的情况下，本地守护进程添加带有最终信封收件人地址的 **`Delivered-To:`** 头部，并添加带有传递给 Postfix 的收件人地址的 **`X-Original-To:`** 头部。信封发件人地址可以在 **`Return-Path:`** 头部获取。

# 地址扩展

可选的 `recipient_delimiter` 配置参数指定了如何将地址扩展与本地收件人名分开。

例如，设置“`recipient_delimiter = +`”时，`name+foo` 将投递到别名 `name+foo` 或别名 `name`，投递到 `~name/.forward+foo` 或 `~name/.forward` 中列出的目标，投递到用户 `name` 拥邮箱，或者作为无法投递的消息退回。

# 投递权限

向外部文件和外部命令的投递是以代表投递的收件人用户的权限进行的。在没有用户上下文的情况下，**`local(8)`** 守护进程使用 **`include:`** 文件或别名数据库的所有者权限。当这些文件由超级用户拥有时，将使用 **`default_privs`** 配置参数指定的权限进行投递。

# 标准

`RFC 822 (ARPA 文本消息)` `RFC 3463 (增强状态码)`

# 诊断

问题和事务被记录到 `syslogd(8)` 中。损坏的消息文件会被标记，以便队列管理器随后将它们移动到损坏队列。

根据 `notify_classes` 参数的设置，主管理员将收到邮件退信（bounces）和其他故障。

# 安全

**`local(8)`** 投递代理需要双重身份：1) 访问私有的 Postfix 队列和 IPC 机制；2) 模拟收件人并投递到收件人指定的或或命令。因此，它是敏感的。

**`local(8)`** 投递代理不允许在 **`alias_maps`** 中进行 `$1` 等正则表达式替换，因为这会产生安全漏洞。

**`local(8)`** 投递代理将静默忽略在 **`alias_maps`** 中使用 **`proxymap(8)`** 服务器的请求。相反它将直接打开表。在 Postfix 2.2 版本之前，**`local(8)`** 投递代理将致命错误终止。

# Bug

出于安全考虑，外部命令或外部文件的消息投递状态从不检查到文件中。因此，程序偶尔可能会向命令或外部文件投递多次。宁安全勿错过。

相互递归的别名或 `~/.forward` 文件无法及早检测。产生的邮件转发循环通过使用 `Delivered-To:` 消息头部来打破。

# 配置参数

`main.cf` 的更改会被自动读取，因为 `local(8)` 进程运行时间有限。使用命令“`postfix reload`”来加速更改生效。

下文仅提供参数摘要。查看 `postconf(5)` 获取更多详情，包括示例。

# 兼容性

- `biff (yes)`: 是否使用 biff。
- `owner_alias (no)`: 当投递到别名时。
- `owner_special (no)`: 对别名特殊特殊。
- `mailtool_compatibility (no)`: 过时功能。
- `frozen_to (yes)`: 更新 `local(8)` 投递代理的认知。
- `strict_ownership (yes)`: 当邮箱不归其所有时延迟投递。
- `reset_owner (no)`: 重置 `local(8)` 投递代理的认知。

# 投递方法控制

`local(8)` 投递的优先级从高到低为：
- `aliases`
- `.forward` 文件
- `mailbox_transport_maps`
- `mailbox_transport`
- `mailbox_command_maps`
- `mailbox_command`
- `home_mailbox`
- `mail_spool_directory`
- `fallback_transport_maps`
- `fallback_transport`
- `user_relay`

# 邮箱锁定控制

- `deliver_lock_attempts (20)`: 在邮箱文件或 `bounce(8)` 日志文件上获取独占锁的最大次数。
- `deliver_lock_delay (1s)`: 尝试在邮箱文件或 `bounce(8)` 日志文件上获取独占锁之间的时间。
- `stale_lock_time (500s)`: 过期邮箱锁文件被移除的时间。
- `mailbox_delivery_lock`（查看‘`postconf -d`’输出）：在尝试投递之前如何锁定 UNIX 风格的本地(8) 邮箱。

# 资源与速率控制

`command_time_limit (1000)`
向外部命令投递的时间限制。

`duplicate_filter_limit (1000)`
地址重复过滤器为别名(5) 或为虚拟(5) 别名扩展，或为 `showq(8)` 队列重复显示所记住的地址最大数量。

`local_destination_concurrency_limit (2)`
通过本地邮件投递传输层向同一接收者并行投递的最大数量（当“`local_destination_recipient_limit = 1`”时），或向同一本地域进行并行投递的最大数量（当“`local_destination_recipient_limit > 1`”时）。

`local_destination_recipient_limit (1)`
通过本地邮件投递传输层每条消息投递的接收者最大数量。

`mailbox_size_limit (51200000)`
任何本地(8) 个人邮箱或 maildir 文件的最大大小，或为 0（不限制）。

# 安全控制

`allow_mail_to_commands (alias, forward)`
限制将本地(8) 邮件投递到外部命令。

`allow_mail_to_files (alias, forward)`
限制将本地(8) 邮件投递到外部文件。

`command_expansion_filter (参见 ‘postconf -d’ 输出)`
限制本地(8) 投递代理在 `$mailbox_command` 和 `$command_execution_directory` 的 `$name` 扩展中允许的字符。

`default_privs (nobody)`
本地(8) 投递代理投递到外部文件或命令时使用的默认权限。

`forward_expansion_filter (参见 ‘postconf -d’ 输出)`
限制本地(8) 投递代理在 `$forward_path` 的 `$name` 扩展中允许的字符。

适用于 Postfix 2.2 及更高版本：

`execution_directory_expansion_filter (参见 ‘postconf -d’ 输出)`
限制本地(8) 投递代理在 `$command_execution_directory` 的 `$name` 扩展中允许的字符。

适用于 Postfix 2.5.3 及更高版本：

`strict_mailbox_ownership (yes)`
当邮箱文件所有者不属于接收者时，延迟投递。

# 杂控制

`config_directory (参见 ‘postconf -d’ 输出)`
Postfix `main.cf` 和 `master.cf` 配置文件的默认位置。

`daemon_timeout (18000s)`
Postfix 守护进程在被内置守护进程定时器终止之前处理请求可能花费的时间。

`delay_logging_resolution_limit (2)`
记录亚秒值时小数点后的最大数字位数。

`export_environment (参见 ‘postconf -d’ 输出)`
Postfix 进程将导出到非 Postfix 进程的环境变量列表。

`ipc_timeout (36000s)`
通过内部通道发送或接收信息的时间限制。

`local_command_shell (empty)`
用于本地(8) 投递到非 Postfix 命令的可选 shell 程序。

`max_idle (100s)`
空闲 Postfix 守护进程在自愿退出前等待接入连接的最大时间。

`max_use (100)`
Postfix 守护进程在自愿退出前服务的最大接入连接数。

`prepend_delivered_header (command, file, forward)`
Postfix 本(8) 投递代理在这些投递上下文中添加 `Delivered-To:` 消息头部，内容为邮件投递到的地址。

`process_id (read-only)`
Postfix 命令或守护进程的进程 ID。

`process_name (read-only)`
Postfix 命令或守护进程的名称。

`propagate_unmatched_extensions (canonical, virtual)`
哪些地址查找表会将地址扩展从查找键复制到查找结果。

`queue_directory (参见 ‘postconf -d’ 输出)`
Postfix 顶层队列目录的位置。

`recipient_delimiter (empty)`
用户名和地址扩展之间的分隔符（user+foo）。

`require_home_directory (no)`
要求在尝试投递邮件之前，本地(8) 接收者的家目录必须存在。

`syslog_facility (mail)`
Postfix 日志的 syslog facility。

`syslog_name (参见 ‘postconf -d’ 输出)`
在 syslog 记录中附加进程名称前的邮件系统名称，例如“smtpd”将变为“postfix/smtpd”。

## 文件

以下是示例；不同系统之间的细节不同。
`$HOME/.forward`，每用户别名 `/etc/aliases`，系统级别名
database `/var/spool/mail`，系统邮箱

# 另请

`qmgr(8)`, 队列管理器 `bounce(8)`, 投递状态报告 `newaliases(1)`, 创建/更新别名数据库 `postalias(1)`, 创建/更新别名数据库 `aliases(5)`, 别名数据库格式 `postconf(5)`, 配置参数 `master(5)`, 通用守护进程选项 `syslogd(8)`, 系统日志

# 许可证

Secure Mailer 许可证随此软件发行。

## 历史

Delivered-To 消息出现在 Daniel Bernstein 的 qmail 中。
Delivered-To 头部出现在 Daniel Bernstein 的 qmail 中。

## 作者

Wietama Watson，P.O. Box 7049 Yorktown, NY

# LOCKDEV

名称
Lockdev 是一个提供文件独占访问的二进制文件。

## 描述
Lockdev 设计用于简化产生大量日志文件的系统管理。它允许对日志文件进行自动轮转、压缩、删除和邮件发送。每个日志文件可以在每天、每周、每月或在增长过大时处理。

通常，lockdev 作为每日 cron 任务运行。



# 资源与速率控制

`command_time_limit` (1000)

向外部命令投递的时间限制。

`duplicate_filter_limit` (1000)

地址重复过滤器为别名(5) 或为虚拟(5) 别名扩展，或为 `showq(8)` 队列重复显示所记住的地址最大数量。

`local_destination_concurrency_limit` (2)

通过本地邮件投递传输层向同一接收者并行投递的最大数量（当“`local_destination_recipient_limit = 1`”时），或向同一本地域进行并行投递的最大数量（当“`local_destination_recipient_limit > 1`”时）。

`local_destination_recipient_limit` (1)

通过本地邮件投递传输层每条消息投递的接收者最大数量。

`mailbox_size_limit` (51200000)

任何本地(8) 个人邮箱或 `maildir` 文件的最大大小，或为 0（不限制）。

# 安全控制

`allow_mail_to_commands` (alias, forward)

限制将本地(8) 邮件投递到外部命令。

`allow_mail_to_files` (alias, forward)

限制将本地(8) 邮件投递到外部文件。

`command_expansion_filter` (参见 ‘`postconf -d`’ 输出)

限制本地(8) 投递代理在 `$mailbox_command` 和 `$command_execution_directory` 的 `$name` 扩展中允许的字符。

`default_privs` (nobody)

本地(8) 投递代理投递到外部文件或命令时使用的默认权限。

`forward_expansion_filter` (参见 ‘`postconf -d`’ 输出)

限制本地(8) 投递代理在 `$forward_path` 的 `$name` 扩展中允许的字符。

适用于 Postfix 2.2 及更高版本：

`execution_directory_expansion_filter` (参见 ‘`postconf -d`’ 输出)

限制本地(8) 投递代理在 `$command_execution_directory` 的 `$name` 扩展中允许的字符。

适用于 Postfix 2.5.3 及更高版本：

`strict_mailbox_ownership` (yes)

当邮箱文件所有者不属于接收者时，延迟投递。

# 杂控制

`config_directory` (参见 ‘`postconf -d`’ 输出)

Postfix `main.cf` 和 `master.cf` 配置文件的默认位置。

`daemon_timeout` (18000s)

Postfix 守护进程在被内置守护进程定时器终止之前处理请求可能花费的时间。

`delay_logging_resolution_limit` (2)

记录亚秒值时小数点后的最大数字位数。

`export_environment` (参见 ‘`postconf -d`’ 输出)

Postfix 进程将导出到非 Postfix 进程的环境变量列表。

`ipc_timeout` (36000s)

通过内部通道发送或接收信息的时间限制。

`local_command_shell` (empty)

用于本地(8) 投递到非 Postfix 命令的可选 shell 程序。

`max_idle` (100s)

空闲 Postfix 守护进程在自愿退出前等待接入连接的最大时间。

`max_use` (100)

Postfix 守护进程在自愿退出前服务的最大接入连接数。

`prepend_delivered_header` (command, file, forward)

Postfix 本(8) 投递代理在这些投递上下文中添加 `Delivered-To:` 消息头部，内容为邮件投递到的地址。

`process_id` (read-only)

Postfix 命令或守护进程的进程 ID。

`process_name` (read-only)

Postfix 命令或守护进程的名称。

`propagate_unmatched_extensions` (canonical, virtual)

哪些地址查找表会将地址扩展从查找键复制到查找结果。

`queue_directory` (参见 ‘`postconf -d`’ 输出)

Postfix 顶层队列目录的位置。

`recipient_delimiter` (empty)

用户名和地址扩展之间的分隔符（user+foo）。

`require_home_directory` (no)

要求在尝试投递邮件之前，本地(8) 接收者的家目录必须存在。

`syslog_facility` (mail)

Postfix 日志的 syslog facility。

`syslog_name` (参见 ‘`postconf -d`’ 输出)

在 syslog 记录中附加进程名称前的邮件系统名称，例如“smtpd”将变为“postfix/smtpd”。

## 文件

以下是示例；不同系统之间的细节不同。

`$HOME/.forward`，每用户别名 `/etc/aliases`，系统级别名

database `/var/spool/mail`，系统邮箱

# 另请

`qmgr(8)`, 队列管理器 `bounce(8)`, 投递状态报告 `newaliases(1)`, 创建/更新别名数据库 `postalias(1)`, 创建/更新别名数据库 `aliases(5)`, 别名数据库格式 `postconf(5)`, 配置参数 `master(5)`, 通用守护进程选项 `syslogd(8)`, 系统日志

# 许可证

Secure Mailer 许可证随此软件发行。

## 历史

`Delivered-To` 消息出现在 Daniel Bernstein 的 `qmail` 中。

`Delivered-To` 头部出现在 Daniel Bernstein 的 `qmail` 中。

## 作者

Wietama Watson P.O. Box 7049 Yorktown, NY

# LOCKDEV

## 名称

`Lockdev` 是一个提供文件独占访问的二进制文件。

## 描述

`Lockdev` 设计用于简化产生大量日志文件的系统管理。它允许对日志文件进行自动轮转、压缩、删除和邮件发送。每个日志文件可以在每天、每周、每月或在增长过大时处理。

## 配置文件

`logrotate` 从命令行指定的一系列配置文件中读取关于它应该处理的日志文件的所有信息。每个配置文件都可以设置全局选项（本地定义会覆盖全局选项，且较晚的定义会覆盖之前的定义），并指定要轮转的日志文件。一个简单的配置文件如下：

```
# sample logrotate configuration file /var/log/messages {
rotate 5 weekly postrotate /var/bin/killall -HUP syslog endscript
    /var/log/http/access.log /var/log/http/error.log { rotate 5 mail
    www@my.org size 100k sharedscripts postrotate /var/bin/killall -HUP
    endscript
    /var/log/news/* { monthly 2 olddir
    /var/log/news/old missings postrotate -HUP 'cat /var/run/inn.pid'
    endscript nocompress - ~/*.log }
```

前几行设置了选项；日志在轮转后会被压缩。注意，注释可以出现在配置文件的任何位置，只要行的第一个非空白字符是 `#`。

配置文件的下一个部分定义了如何处理日志文件 `/var/log/messages`。该日志将在经过五周轮转后被删除。在日志文件轮转后（但在旧版本的日志被压缩之前），将执行命令 `/bin/killall -HUP syslogd`。

下一个部分定义了 `/var/log/http/access.log` 和 `/var/log/http/error.log` 的参数。当它们的大小增长到 100K 时会进行轮转，在经过五次轮转后，旧文件将通过邮件发送（不压缩）到 `www@my.org`，而不是删除。`sharedscripts` 意味着 `postrotate` 脚本只会运行一次（在日志压缩后），而不是为每个轮转的日志各运行一次。注意，本节开头第一个文件名周围的双引号遵循引用规则，并支持 ' ' 和 `'\''` 字符。

下一个部分定义了 `/var/log/news/` 下所有文件的参数。每个文件每月轮转一次。这被视为一个单一的轮转指令，如果超过一个文件发生错误，则日志文件将不会压缩。

最后一部分使用波浪号扩展来轮转当前用户主目录下的日志文件。只有当你的 glob 库支持波浪号扩展时，此功能可用。GNU glob 支持此。

请谨慎使用通配符。如果你指定 `*`，`logrotate` 将轮转所有文件，包括之前轮转过的文件。避免这种情况的方法是使用 `olddir` 指令或更精确的通配符（例如 `*.log`）。

以下是关于包含在 `logrotate` 配置中的指令的信息：

- **compress**: 默认情况下，旧版本的日志文件使用 `gzip(1)` 进行压缩。我们也支持 `ncompress`。

- **compresscmd**: 指定使用哪个命令来压缩日志文件。默认是 `gzip`。另见 `uncompress`。

- **uncompresscmd**: 指定使用哪个命令来解压缩日志文件。默认是 `gunzip`。

- **compressext**: 如果启用了压缩，则指定对压缩的日志文件使用什么扩展名。默认值遵循所配置的压缩命令。

- **compressions**: 如果使用了压缩程序，可以将命令行选项传递给该程序。对于 `gzip(1)`，默认值是“-6”（倾向于高压缩率以牺牲速度为代价）。如果你使用不同的压缩命令，可能需要更改 `compressions` 以匹配。

- **copy**: 为日志文件创建一个副本，但不完全更改原始文件。此选项可以用于创建当前日志文件的快照，或者当某些其他实用程序需要截断或解析该文件时。使用此选项时，`create` 选项将不起作用，因为旧日志文件留在原地。

- **copyrunc**: 在创建副本后在原地截断原始日志文件，而不是移动旧日志文件并可选地创建一个新文件。它可以用于某些程序无法告知清理其日志文件并可能继续向之前的日志文件写入（追加）的情况。注意，在复制文件和截断文件之间存在极极短的时间片，因此可能会丢失某些日志数据。使用此选项时，`create` 选项将不起作用，因为旧日志文件留在原地。

- **create mode owner group, create owner group**: 在轮转后立即（在运行 `postrotate` 脚本之前）创建日志文件（文件名与之前相同）。...（此处省略重复的句子，已按要求处理）...

- **olddir mode owner group**: 在轮转后立即（在运行 `postrotate` 脚本之前）创建日志文件（文件名与之前相同）。...（此处省略重复的句子，已按要求处理）...

- **daily**: 日志在 `logrotate` 运行时每天轮转一次（通常是每月第一天）。

- **extension**: 如果启用了压缩，则指定对压缩的日志文件使用什么扩展名。默认值遵循所配置的压缩命令。

- **dateformat**: 日志在 `logrotate` 运行时每天轮转一次（通常是每月第一天）。

- **hourly**: 日志在 `logrotate` 运行时每小时轮转一次（通常是每月第一天）。

- **missingok**: 如果日志缺失，继续处理下一个而不报错（通常是每月第一天）。

- **monthly**: 日志在 `logrotate` 运行时每月轮转一次（通常是每月第一天）。

- **nocompress**: 旧版本的日志文件不进行压缩。另见 `compress`。

- **nocopy**: 不复制原始日志文件并留在原地（这会覆盖 `copy` 选项）。

- **nopyrtruncate**: 在创建副本后不在原地截断原始日志文件（这会覆盖 `copy` 选项）。

`copytruncate` 选项

`nocreate`

不创建新的日志文件（这会覆盖 `create` 选项）。

`nocreateolddir`

当目录不存在时，`logrotate` 不会创建 `olddir` 目录。

`nodelaycompress`

不要将上一个日志文件的压缩推到下一个轮转周期（这会覆盖 `delaycompress` 选项）。

`nodatext`

不使用日期扩展名归档旧版本的日志文件（这会覆盖 `dateext` 选项）。

`nomail`

不将旧日志文件发送到任何地址。

`nomissingok`

如果日志文件不存在，则发布错误。这是默认设置。

`nolddir`

日志在通常所在的相同目录进行轮转（这会覆盖 `olddir` 选项）。

`nosharedscripts`

为每个被轮转的日志文件运行 `prerate` 和 `postrotate` 脚本（这是默认设置，并会覆盖 `sharedscripts` 选项）。日志文件的绝对路径将作为第一个参数传递给脚本。如果脚本以错误退出，仅对受影响的日志不再执行剩余操作。

`noshred`

删除旧日志文件时不使用 `shred`。另请参见 `shred`。

`notifemptym`

如果日志为空，则不进行轮转（这会覆盖 `ifempty` 选项）。

`olddir` 目录

日志被移动到轮转目录中。除非使用了 `copy`、`copytruncate` 或 `renamecopy`，否则该目录必须与被轮转的日志文件位于同一物理设备上。除非指定了绝对路径，否则该目录被认为相对于存放日志文件的目录。当使用此选项时，该目录中将包含所有旧版本的日志。此选项可能会被 `noolddir` 选项覆盖。

`postrotate/endscript`

`postrotate` 和 `endscript` 之间的行（两者都必须单独成行）将在日志文件轮转后执行（`/bin/sh`）。这些指令只能出现在日志文件定义内部。通常，日志文件的绝对路径将作为第一个参数传递给脚本。如果指定了 `sharedscripts`，则整个模式将传递给脚本。还有 `prerotate`。错误处理请参见 `sharedscripts` 和 `nosharescripts`。

# prerotate/endscript

`prerot` 和 `endscript` 之间的行（两者都必须单独成行）将在日志文件轮转前执行（`/bin/sh`），且仅在日志确实会被轮转时才执行。这些指令只能出现在日志文件定义内部。通常，日志文件的绝对路径将作为第一个参数传递给脚本。如果指定了 `sharedscripts`，则整个模式将传递给脚本。另请参见 `postrotate`。错误处理请参见 `sharedscripts` 和 `nosharescripts`。

# firstaction/endscript

`firstaction` 和 `endscript` 之间的行（两者都必须单独成行）将在所有匹配通配符模式的日志文件轮转前、`prerate` 脚本运行前执行（`/bin/sh`），且仅在至少有一个日志被轮转时才执行。这些指令只能出现在日志文件定义内部。模式将作为第一个参数传递给脚本。如果脚本以错误退出，则不再进行后续处理。另请参见 `lastaction`。

# lastaction/endscript

`lastaction` 和 `endscript` 之间的行（两者都必须单独成行）将在所有匹配通配符模式的日志文件轮转后、`postrotate` 脚本运行后执行一次（`/bin/sh`），且仅在至少有一个轮转时。这些指令只能出现在日志文件定义内部。模式将作为第一个参数传递给脚本。如果脚本以错误退出，将显示错误消息（因为这是最后一个操作）。另请参见 `firstaction`。

# preremove/endscript

`preremove` 和 `endscript` 之间的行（两者都必须单独成行）在删除日志文件后立即执行一次（`/bin/sh`）。`rotate` 将传递即将被删除的文件名。另请参见 `firstaction`。



# rotate count

日志文件在被删除或发送到 `mail` 指令指定的地址之前，会轮转 `count` 次。如果 `count` 为 0，则移除旧版本而不是轮转。

# size size

只有当日志文件大小大于 `size` 字节时才进行轮转。如果 `size` 后面跟着 `k`，则单位为千字节。如果使用 `M`，则单位为兆字节，如果使用 `G`，则单位为吉字节。因此 `size 100`、`size 100k`、`size 100M` 和 `size 100G` 都是有效的。

# sharedscripts

通常，每个轮转的日志都会运行 `prerotate` 和 `postrotate` 脚本，并将日志文件的绝对路径作为第一个参数传递给脚本。这意味着对于匹配多个文件的日志项（例如 `/var/log/news/*`），如果指定了 `sharedscripts`，无论匹配多少日志，脚本都只运行一次，并将整个模式传递给它们。然而，如果模式中没有日志轮转，脚本将不会运行。如果脚本以错误退出，将不对任何日志执行剩余操作。此选项覆盖 `nosharedscripts` 选项并隐含 `create` 选项。

# shred

使用 `shred -u` 代替 `unlink()` 删除日志文件。这应该确保日志在删除后不可读；这是默认设置。另请参见 `noshed`。

# shredcycles count

要求 `GNU shred(1)` 在删除前覆盖日志文件 次。如果没有此选项，将使用 `shred` 的默认值。

# start count

轮转基数的数字。例如，如果你指定 0，日志在轮转时将以 `.0` 扩展名创建。

# su group

使用此用户和组而不是默认用户/组（通常为 `root`）旋转文件。

# tabooext

更改当前的禁用列表（参见禁用扩展的 `include` 指令）。如果列表前有 `+`，则会扩展当前的禁用列表，否则将其替换。

# weekly

如果当前周小于上次轮转周，或者距离上次轮转已超过一周，则对日志进行轮转。这通常等同于每周的第一天轮转，但如果 `logrotate` 每天运行一次效果更好。

# yearly

如果当前年份与上次轮转不同，则对日志进行轮转。

# logsave 选项

- `-a` 此选项将输出追加到日志文件，而不是替换其当前内容。
- `-s` 此选项将使 `logsave` 跳过写入被控制-A（ASCII 001 或帧头开始）和控制-B（ASCII 002 或文本开始）括起来的日志文件文本。这允许进度条信息在控制台上对用户可见，而不会写入日志文件。
- `-v` 此选项将使 `logsave` 在向用户输出时更加详尽。

## 作者

Theodore Ts'o (`tytso@mit.edu`)

# 另请

`fsck(8)`

# LOSETUP

> 名称

`losetup` - 设置并控制回环设备

## 概要

获取信息：

`losetup -l loopdev`

`losetup -l [-a]`

`losetup -j file [-o offset]`

删除回环设备：

`losetup -d loopdev...`

删除所有使用的回环设备：

`losetup -D`

打印第一个未使用的回环设备名称：

`losetup -f`

设置回环设备：

`losetup [-o offset] [--sizelimit size] [-p pfd] [-rP] {-f[--show]|loopdev} file`

调整调整回环设备大小：

`losetup -c loopdev`

## 描述

`losetup` 用于将回环设备与普通文件或块设备关联，解绑回环设备并查询回环设备的状态。如果仅给出 `loopdev` 参数，则显示相应回环设备的状态。

请注意，旧的输出格式（例如 `losetup -a`）使用逗号分隔的字符串已废弃，取而代之的是 `--list` 输出格式（例如 `losetup -a -l`）。

大小和偏移量参数后可以跟随乘法后缀 `+KiB=1024, MiB=1024*1024` 等，类推适用于 `GiB, TiB, PiB, EiB, ZiB` 和 `YiB+`（“B”是可选的，例如“K”与“KiB”具有相同含义），或后缀 `+KB=1000, MB=1000*1000` 等，类推适用于 `GB, TB, PB, EB, ZB` 和 `YB`。

- `-a,--all`

显示所有回环设备的状态。注意，非 `root` 用户无法访问所有信息。另见 `--list`。旧的输出格式（在不带 `--list` 时打印的内容）已废弃。

- `-c,--capacity loopdev`

强制驱动程序重新读取与指定回环设备关联的文件的大小

- `-d,--detach loopdev...`

解绑与指定回环设备关联的文件或设备

- `-D,--detach-all`

解绑所有回环设备

- `-f,--find`

查找第一个未使用的回环设备。如果存在文件参数，则使用此设备。否则，打印其名称

- `-h,--help`

打印帮助信息

- `-j,--associated file`

显示与给定文件关联的所有回环设备的状态

- `-l,--list`

如果指定了回环设备或 `-a` 选项，则为特定回环设备或所有回环设备打印默认列，默认打印所有设备的信息。

- `-o,--offset offset`

数据起始位置进入指定文件或设备偏移 `offset` 字节

- `-O,--output columns`

指定 `--list` 输出中要打印哪些列

- `--size limit`

将数据结束位置设置为在数据起始位置后不超过 `size` 字节

- `-P,--partscan`

强制内核在新创建的回环设备上扫描分区表

- `-r,--read-only`

设置只读回环设备

- `--show`

如果存在 `-f` 选项且有文件参数，则打印设备名称。

- `-v,--verbose`

详细模式

# 加密

`Cryptoloop` 不再支持，转而支持 `dm-crypt`。更多详情请见 `cryptsetup(8)`。

# 返回值

`losetup` 成功返回 0，失败返回非零。当 `losetup` 显示回环设备的状态时，如果设备未配置则返回 1，如果发生错误无法确定设备状态则返回 2。

## 文件

`/dev/loop[0..N]`

回环块设备

`/dev/loop-control`

回环控制设备

## 示例

以下命令可以作为使用回环设备的示例。

```
# dd if=/dev/zero of=~/file.img bs=1MiB count=10 # losetup --find -- 
show ~/file.img /dev/loop0 # mkfs -t ext2 /dev/loop0 # mount /dev/loop0 # losetup --detach /loop0
```

## 作者

Karel Zak <zak@redhat.com>，基于 Theodore Ts'o <tsso@mit.edu> 的原始版本

# 可用

`losetup` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/util-linux/` 获取。

# lpadmin

> 名称

`lpadmin` - 配置打印机和类

## 概要

```
lpadmin [ -E ] [-U username ] [ -h server[:port] ] -d destination lpadmin [ -E ] [-U username ] [ -h server[:port] ] -p destination [ -R name-default ] option(s) lpadmin [ -E ] [-U username ] [ -h server[:port] ] -x destination
```

## 描述

`lpadmin` 配置 `CUPS` 提供的打印机和类队列。它也可以用于设置服务器的默认打印机或类。

在 `-d` 之前指定时，可以设置服务器的默认打印机或类。

在 `-d`、`-p` 或 `-x` 之前指定时，`-E` 选项强制加密。第一种格式的设置打印机或类。第二种格式的命令 (`-p`) 配置打印机或类。第三种格式的命令 (`-x`) 删除打印机或类。

# 配置选项

在配置打印机时识别以下选项：

- `-c class`

将指定的打印机添加到类中。如果类不存在，则会自动创建。

- `-i interface`

设置打印机的 System V 接口。此选项配合 `-P` 选项（PPD 文件）使用，用于提供驱动。

- `-m model`

设置 System V 接口脚本或 PPD 文件。使用 `-m` 配合 `lpinfo(8)` 命令获取模型列表。

- `-o cupsSupplies=true`

- `-o cupsSupplies=false`

指定是否报告 IPP 供应水平。

- `-o cupsMPlies=true`

- `-o cupsMPlies=false`

指定是否报告 SNMP 供应水平（RFC 3805）。

- `-o job-klimit=value`

- `-o job-page-limit=value`

设置用户的千字节限制。其值为整数；1 个千字节为 1024 字节。

设置用户的页数限制。其值为可打印页数的整数；双面页计为两页。

- `-o job-quota-period=value`

设置用户的配额周期。其值为整数秒数；86,400 秒为一天。

- `-o job-sheets-default=banner`

- `-o job-sheets-default=banner,banner`

设置打印作业使用的默认幅页。

- `-o name=value`

设置打印机的 PPD 选项。可以使用 `lpoptions(1)` 命令的 `-l` 列出 PPD 选项。

- `-o name-default=value`

设置目的地的服务器端选项。任何打印选项都可以设置默认值，例如“o cpi-default=17”将默认“cpi”选项设置为 17。

- `-o port-monitor=name`

设置打印时使用的二进制通信程序，“none”、“bcp”或“btcp”。默认程序为“none”。指定的端口监控器必须列在打印机的 PPD 文件中。

- `-o printer-error-policy=name`

设置打印机后端无法将作业发送到打印机时使用的错误策略。该名称必须是“abort-job”、“retry-job”、“retry-current-job”或“stop-printer”之一。默认错误策略对于打印机为“stop-printer”，对于类为“retry-current-job”。

- `shared`

将目的地设置为共享/发布或未共享/未发布。共享/发布的目的地将根据 `cupsd.conf` 中的浏览配置在局域网内公开发布，而未共享/未发布的目的地不进行发布。默认值为“true”。

- `printer-op-policy=name`

设置与目的地相关的 IPP 操作策略。该名称必须在 `cupsd.conf` 的 Policy 部分中定义。默认操作策略为“default”。

- `-R name-default`

从打印机中删除命名选项。

- `class`

从类中移除命名的打印机。如果结果类变为空，则将其删除。

## 兼容性

与 System V 打印系统不同，`CUPS` 允许打印机名称包含除空格、制表符、“/或“#以外的任意打印字符。此外，打印机和类不区分大小写。最后，取决于打印系统的配置，`CUPS` 版本的 `lpadmin` 可能会要求用户输入密码。这与 System V 版本不同，后者要求 `root` 用户执行此命令。

## 局限性

`CUPS` 版本的 `lpadmin` 不支持所有的 System V 或 Solaris 打印系统配置选项。

## 另参

`cupsaccept(8)`, `cupsenable(8)`, `lpinfo(8)`, `lpoptions(1)`, `http://localhost:631/help`

## 版权

Copyright 2007-2013 by Apple Inc.

## lpc

## 名称

`lpc` - 线路打印机控制程序

## 语法

```
lpc [ command [ parameter(s) ] ]
```

## 描述

`lpc` 对 `CUPS` 提供的打印机类队列提供有限控制。它也可以用于查询队列状态。

如果命令行上没有指定命令，`lpc` 将显示提示符并从标准输入接受命令。

## 命令

`lpc` 程序接受与同名的 Berkeley `lpc` 程序接受的命令子集：

- `exit` 退出命令解释器。[command]
- `?` `help` [command] 显示短帮助信息。
- `quit` 退出命令解释器。`status` [queue] 显示一个或多个打印机或类队列的状态。

## 局限性

由于 `lpc` 针对 Berkeley 打印系统，因此无法使用 `lpc` 配置 `CUPS` 提供的打印机或类队列。要配置打印机或类队列，必须使用 `lpadmin(8)` 命令或具有该功能的其他 `CUPS` 兼容客户端。

## 兼容性

`CUPS` 版本的 `ipc` 未实现所有的标准的 Berkeley 或 LPRng 命令。

## 另参

`cancel(1)`, `cupsaccept(8)`, `cupsenable(8)`, `lp(1)`, `lpr(1)`, `lprm(1)`, `lpstat(1)`, `http://localhost:631/help`

## 版权

Copyright 2007-2013 by Apple Inc.

## Lpinfo

## 名称

`lpinfo` - 显示可用设备或驱动程序

## 语法

```
lpinfo [ -E ] [ -U username ] [ -h server[:port] ] [ -l ] [ --device-id device-id-string ] [ --exclude-schemes scheme-list ] [ --include-schemes scheme-list ] [ --language locale ] [ --make-and-model name ] [ --product name ] -m lpinfo [ -E ] [ -U username ] [ -h server[:port] ] [ -l ] [ --exclude-schemes scheme-list ] [ --include-schemes scheme-list ] [ --timeout seconds ] -v
```

## 描述

`lpinfo` 列出了 `CUPS` 服务器已知的可用设备或驱动程序。第一种形式 (--m) 列出可用驱动程序，而第二种形式 (-v) 列出可用设备。

## 选项

`lpinfo` 接受以下选项：

- `-E` 在连接到服务器时强制加密。
- `-U username` 连接到服务器时设置用户名。
- `-h server[:port]` 选择备用服务器。
- `-l` 显示设备或驱动程序的“详细”列表。
- `-device-id device-id-string` 在使用 `-m` 选项列出驱动时时指定匹配的 IEEE-1284 设备 ID。
- `-exclude-schemes scheme-list` 指定从结果中排除的设备或 PPD 方案的逗号分隔列表。静态 PPD 文件使用“file”方案。
- `-include-schemes scheme-list` 指定包含在结果中的设备或 PPD 方案的逗号分隔列表。静态 PPD 文件使用“file”方案。
- `-language locale` 在使用 `-m` 选项列出驱动程序时指定匹配的语言。
- `-make-and-model name` 在使用 `-m` 选项列出驱动程序时指定匹配的品牌和型号。
- `-product name` 在使用 `-m` 选项列出驱动程序时指定匹配的产品。
- `-timeout seconds` 在使用 `-v` 列出设备时指定超时时间。

## 兼容性

`CUPS` 版本的 `lpinfo` 是 `CUPS` 特有的。

## 另参

`lpadmin(8)`, `http://localhost:631/help`

## 版权

Copyright 2007-2013 by Apple Inc.

## lpmove

## 名称

`lpmove` - 移动作业或所有作业

## 语法

```
lpmove [ -E ] [ -h server[:port] ] [ -U username ] lpmove destination
```

## 描述

`lpmove` 将指定的作业或所有作业移动到目标。`lpmove` 读取 `sysfs` 文件系统以收集信息。

该命令以树形格式打印所有设备（RAM 磁盘除外）。默认输出以及拓扑可能会发生变化。因此，只要可能，您应该避免在脚本中使用默认输出。始终通过 output 定义预期的列。

## 选项

`lpmove` 命令支持以下选项：

- `-E` 在连接到服务器时强制加密。
- `-U` 指定备用用户名。
- `-h server[:port]` 指定备用服务器。

## 另参

`cancel(1)`, `lp(1)`, `http://localhost:631/help`

## 版权

Copyright 2007-2013 by Apple Inc.

## LSBLK

## 名称

`lsblk` - 列出设备

## 语法

`lsblk [options] [device...]`

## 描述

**`lsblk`** 列出关于所有或指定设备的信息。该命令以树形格式打印所有设备（RAM 磁盘除外）。使用 `--help` 获取可用列的列表。如果以格式 `+list lsblk -o +UUID` 指定，默认列列表可能会扩展。输出是稳定的。

## 选项

`lsblk` 接受以下选项：

- `-a, --all` 也列出空设备。（默认跳过）。
- `-b, --bytes` 以字节打印 SIZE 列，而不是易读格式。
- `-D, --discard` 为每个设备打印丢弃能力（TRIM, UNMAP）。
- `-d, --nodeps` 不打印持有设备或从设备。例如，`lsblk --nodeps /dev/sda` 仅打印 `sda` 设备的信息。
- `-e, --exclude list` 根据逗号分隔的主设备列表排除设备。注意，内存设备（主设备 1）默认被排除。过滤器应用于顶层设备。
- `-f, --fs` 输出文件系统信息。此选项等同于 `o NAME,FSTYPE,LABEL,MOPOINT`。文件系统和 RAID 的权威信息由 `blkid(8)` 命令提供。
- `-h, --help` 打印帮助文本并退出。



- `-I`, `--include list` 根据逗号分隔的主设备列表包含设备。过滤器应用于顶层设备。

- `-i`, `--ascii` 使用 ASCII 字符进行树形格式化。

- `-l`, `--list` 以列表形式产生输出。

- `-m`, `--Perms` 输出设备所有者、组和模式的信息。此选项等同于 `o NAME,SIZE,OWNER,GROUP,MODE`。

- `-n`, `--noheadings` 不打印标题行。

- `-o`, `--output list` 指定要打印的输出列。使用 `--help` 获取所有支持列的列表。如果以格式 `+list lsblk -o +UUID` 指定，默认列列表可能会扩展。

- `-P`, `--pairs` 以键="值”值对的形式产生输出。所有潜在的不安全字符都经过十六进制转义。

- `-p`, `--paths` 打印完整的设备路径。

- `-r`, `--raw`

以原始格式生成输出。所有潜在的不安全字符在 `NAME`、`KNAME`、`LABEL`、`PARTLABEL` 和 `MOUNTPOINT` 列中均会被十六进制转义（`x<<<code>`）。

- `-S`, `--scsi`

仅输出关于 SCSI 设备的信息。所有的分区、从设备和持有者设备都会被忽略。

- `-s`, `--inverse`

逆逆打印依赖关系。

- `-t`, `--topology`

输出关于块设备拓扑的信息。此选项等同于 `-0 NAME,ALIGNMENT,MIN-IO,OPT-IO,PHY-SEC,LOG-SEC,ROTA,SCHED,RQ-SIZE,WSAME`。

- `-V`, `--version`

输出版本信息并退出。

# NOTES

对于分区，某些信息（例如队列属性）是从父设备继承的。

`lsblk` 命令需要能够通过主:从设备号查找每个块设备，这是通过使用 `/sys/dev/block` 实现的。该 sysfs 目录出现在内核 2.6.27（2008年10月）。如果足够新的内核出现问题，请检查在内核编译时是否启用了 `CONFIG_SYSFS`。

## AUTHORS

Milan Broz <mbroz@redhat.com> Karel Zak <kzak@redhat.com>

# ENVIRONMENT

设置 `LIBMOUNT_DEBUG=0xffff` 可启用调试输出。

## SEE ALSO

`findmnt(8)`, `blkid(8)`, `ls(1)`

# AVAILABILITY

`lsblk` 命令是 util-linux 包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# LSLOCKS

> NAME

`lslocks` - 列出本地系统锁

## SYNOPSIS

`lsocks [options]`

## DESCRIPTION

**lslocks** 列出 Linux 系统中当前持有的所有文件锁的信息。

## OPTIONS

- `-h`, `--help`

打印帮助文本并退出。

- `-n`, `--noheadings`

不打印表头。

- `-o`, `--output list`

指定要打印的输出列。使用 `--help` 获取所有支持列的列表。

如果以 `+list` 的格式指定 `list`（例如 `blocks -o +BLOCKER`），则可以扩展默认列列表。

- `-p`, `--pid`

仅显示由此 pid 进程持有的锁。

- `-r`, `--raw`

使用原始输出格式。

- `-u`, `--notrate`

不在列中截断文本。

# OUTPUT

`COMMAND`

持有锁的进程命令名称。

`PID`

持有锁的进程 ID。

`TYPE`

锁的类型；可以是 `FLOCK`（通过 `flock(2)` 创建）或 `POSIX`（通过 `fcntl(2)` 和 `lockf(3)` 创建）。

`SIZE`

被锁文件的大小。

`MODE`

锁的访问权限（读、写）。如果进程被阻塞并等待锁，则模式末尾会带有一个后缀 '* '（星号）。

`M`

锁是否为强制性；0 表示否（意味着锁仅是建议性的），1 表示是。（参见 `fcntl(2)`）。

`START`

锁的相对字节偏移量。

`END`

锁的结束偏移量。

`PATH`

锁的完整路径。如果没有找到，或者没有权限读取路径，它将回退到设备的挂载点。路径可能会被截断；使用 `notruncate` 获取完整路径。

`BLOCKER`

阻塞锁的进程 PID。

# NOTES

`lslocks` 命令旨在替换 `lslk(8)` 命令，该命令最初由 Victor A. Abell <abe@purdue.edu> 编写，自 2001 年起未再维护。

## AUTHORS

Davidlohr Bueso <dave@gnu.org>

## SEE ALSO

`flock(1)`, `fcntl(2)`, `lockf(2)`

# AVAILABILITY

`lslocks` 命令是 util-linux 包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# LSMOD

> NAME

`lsmod` - 显示 Linux 内核模块状态

## SYNOPSIS

`lsmod`

## DESCRIPTION

`lsmod` 是一个简单的程序，用于很好地格式化 `/proc/modules` 的内容，显示当前加载了哪些内核模块。

# COPYRIGHT

此手册页版权最初所有 2002, Rusty Russell, IBM Corporation。由 Jon Masters 及其他人维护。

## SEE ALSO

`insmod(8)`, `modprobe(8)`, `modinfo(8)`

## AUTHORS

**Jon Masters** <jcm@jonmasters.org>

开发者

**Lucas De Marchi** <lucas.de.marchi@.com>

开发者

# LSOF

> NAME

`lsof` - 列出打开的文件

## SYNOPSIS

`lsof [options]`

## DESCRIPTION

`lsof` 列出由进程打开的文件。

后续字符不具有歧义。例如，`-Fn` 可能代表 `-F` 和 `-n` 选项，也可能代表紧跟在 `-F` 选项后的 n 标识符字符。当可能出现歧义时，用 '-' 字符开始一个新选项——例如“-F -n”。如果下一个选项是文件名，请在可能歧义的选项后加上“—”——例如“-F—name”。

`+` 或 `-` 前缀可以应用于一组选项。对于在每个前缀下不产生独立含义的选项——例如 `-i`，它们可以被分组在任一前缀下。因此，例如，“+M -i”可以被读作“+Mi”，而该组则被视为独立的选项。当组中的一个或多个选项在不同前缀下具有独立含义时，请注意前缀的使用——例如，“+-M; -IM”与请求“-i+M”的效果不相同。若有疑问，请使用带有适当前缀的独立选项。

## -? -h

这两个等效选项用于选择一个（帮助）输出列表。当 `lsof` 检测到其提供的选项存在错误时，会在显示解释每个错误的消息后，显示此输出的简短形式。（根据你的 shell 要求转义 '?' 字符。）

## -a -A

导致列表选择选项执行“与（AND）”操作，如上所述。

该选项适用于配置了 AFS 的系统。AFS 内核代码通过动态模块实现。它允许 `lsof` 用户指定 A 为备用名称文件，其中可以找到动态模块的内核地址。关于动态模块、其符号以及它们如何影响 `lsof` 的更多信息，请参阅 `lsof` FAQ（FAQ 部分给出了其位置）。

## -b

导致 `lsof` 避免调用阻塞它的内核函数 `-stat(2)`、`readlink(2)` 和 `stat(2)`。

请参阅“THE BLOCKS AND TIMEOUTS AND AVOIDING KERNEL BLOCKS”章节获取有关使用此选项的信息。

## -c c

选择执行以 c 字符开头的命令进程的文件列表。可以使用多个 `-c` 选项指定多个命令。它们在参与“与（AND）”选项选择之前，会被合并到一个“或（OR）”集中。如果 c 以 ^ 开头，则随后的字符将指定一个命令名称，该命令的进程将被忽略（排除）。

如果 c 以斜杠 ('/') 结尾，则斜杠后的字符被解释为正则表达式。正则表达式中的 shell 元字符必须引用，以防止被 shell 解释。结束斜杠后可以跟随这些修饰符：

- b 表示正则表达式是基础的。忽略字母大小写。

- x 表示正则表达式是扩展的（默认值）。

请参阅 `lsof` FAQ（FAQ 部分给出了其位置）获取关于基础和扩展正则表达式的更多信息。

首先测试简单的命令规范。如果测试失败，则应用命令正则表达式。如果简单测试成功，则不进行命令正则表达式测试。这可能在指定 `lsof` 的 `-V` 选项时导致“no command found for regex:”消息的产生。

## +c w

定义与进程相关的 COMMAND 名称的初始字符的最大数量（由 UNIX 方言提供），以便在 COMMAND 列中打印。（默认值为 9。）

请注意，许多 UNIX 方言并不会通过 `lsof` 获取命令名的文件和结构提供所有的命令名称字符。通常，方言限制了从这些源中提供的字符数量。例如，Linux 2.4.27 和 Solaris 8 将命令名称长度限制为 16 个字符。

如果 w 为零（'0'），则 UNIX 方言提供给 `lsof` 的所有命令字符都将被打印。

如果 w 小于列标题“COMMAND”的长度，它将被提升到该长度。

## -C

禁用从内核名称缓存中报告任何路径组件。请参阅“KERNEL CACHE”章节。

## +d

除非指定 `-x` 选项，`lsof` 不会跟踪链接。除非指定 `-x` 选项，`lsof` 不。导致 `lsof` 搜索内核名称缓存中的所有实例以及其包含的文件。

除非指定 `-x` 选项，`lsof` 不会跟踪链接。除非指定 `-x` 选项，`lsof` 不会跟踪链接。导致 `lsof` 搜索内核名称缓存中的所有实例以及其包含的文件。

## -d

除非指定 `-x` 选项，`lsof` 不会跟踪链接。指定一个排除的路径组件。除非指定 `-x` 选项，`lsof` 不会跟踪链接。导致 `lsof` 搜索内核名称缓存中的所有实例以及其包含的文件。

除非指定 `-x` 选项，`lsof` 不会跟踪链接。除非指定 `-x` 选项，`lsof` 不会跟踪链接。

 -D

除非指定 `-x` 选项，`lsof` 不会跟踪链接。除非指定 `-x` 选项，`lsof` 不会跟踪链接。

## -D

控制 `lsof` 对设备缓存的使用。此选项的使用有时受限。请参阅“DEVICE CACHE”章节及后续章节获取更多信息。

`-D` 必须后跟一个设备文件；函数可以可选后跟随路径名。`lsof` 识别这些函数字母：

b、r 和 u 函数有时受限。

? 函数报告 `lsof` 可用于设备缓存的只读和写路径、`lsof` 在形成设备缓存路径时将检查的环境变量名称，以及个人设备缓存路径。（根据你的 shell 要求转义 '?' 字符。）

可用时，b 函数导致 `lsof` 在默认或指定的路径构建新的设备缓存文件。

i 函数导致 `lsof` 忽略设备缓存文件并通过内核调用获取设备信息。

r 函数导致 `lsof` 在默认或指定的路径读取设备缓存，但防止在不存在或现有文件结构不正确时创建新的设备缓存文件。

u 函数导致 `lsof` 在默认或指定的路径读取并更新设备缓存。

可用时，b、r 和 u 函数可以后跟设备缓存文件的路径。默认是执行 `lsof` 的真实用户 ID 目录下的 `lsof_hostname`，但这在 `lsof` 配置编译时可能已被更改。（`-h` 和 `-q` 选项的输出显示默认前缀——例如“lsof.”。后缀 hostname 是由 `gethostname(2)` 返回的主机名的第一个部分。）

替换为新一个。当不指定路径参数时，`r` 函数始终可用；但它可能会受到 `lsof` 进程权限的限制。可用时，`u` 引导 `lsof` 从默认或指定的路径读取设备缓存文件（如果可能），并在必要时重建它。这是指定 `-D` 选项时的默认设备缓存函数。

- `+-e` 免文件系统名称受到阻塞内核函数调用的。`+e` 选项免于 `stat(2)`、`lstat(2)` 以及大多数 `readlink(2)` 内核函数调用。`-e` 选项免于 `stat(2)` 和 `lstat(2)` 内核函数调用。可以通过多个 `+-e` 指定指定多个文件系统，每个系统可以选择是否豁免 `readlink(2)` 调用。

此选项目前仅针对 Linux 实现。

注意：此选项很容易被误应用到感兴趣的文件系统之外，因为它使用了路径而不是更可靠的设备号和节点号（设备号和节点号是通过可能阻塞的 `stat(2)` 内核调用获取的，且不可用，但可以使用 `+-m` 选项作为提供设备号的替代方案）。请务必谨慎使用此选项，并完整指定要豁免的文件系统的路径名。

当报告豁免文件系统的打开文件时，可能无法获取其所有信息。因此，某些信息列将为空，`TYPE` 列中的值将以 "UNKN" 为前缀，并在 `NAME` 列的括号中添加豁免选项。（某些设备号信息可以通过 `+-m` 选项获取。）

- `+-f [cfggn]`

`f` 本身说明了路径名参数如何被解释。当它后面接 `c`、`f`、`g` 或 `n` 的任意组合时，它指定了启用 (+) 或 抑制 (-) 内核文件结构信息的列出。

如果一个普通路径参数匹配由 `mount(8)` 指定的挂载目录，或者它代表一个在 `mount` 输出中命名并与挂载目录名关联的块设备，则被视为文件系统名称。当指定 `+f` 时，所有路径名参数将被视为文件系统名称，如果其中任何一个不是，`lsof` 将报错。这非常有用，例如，当文件系统名称（挂载设备）不是块设备时。这发生在某些 CD-ROM 文件系统上。

当单独指定 `-f` 时，所有路径名参数将被视为普通文件。因此，例如 `-f --` 参数引导 `lsof` 搜索路径名为 `/` 的打开文件，而不是 `/`（根）文件系统中的所有打开文件。

请注意确保 `+f` 和 `-f` 正确终止，并且后面没有跟随可能被视为参数的字符（例如文件名或文件系统名的字符）。例如，在这些示例中使用 `--` 后面接 `+f` 和 `-f`。

```
$ lsof -f-/system/name $ lsof -f--/filename
```

通过 `+f [cfggn]` 选项请求的内核文件结构信息列出是被抑制的，并且在整体上或某些方言中不可用——例如 2.6.22 以下基于 `/proc` 的 Linux 内核。当 `f` 的前缀为加号(`+`) 时，这些字符请求文件结构信息：

- c 文件结构计数（非 Linux）

- f 文件结构地址（非 Linux）

- g 文件标志缩写（Linux 2.6.22 及以上）

- G 十进制文件标志（Linux 2.6.22 及以上）

- n 文件结构节点地址（非 Linux）

当前缀为减号(`-`) 时，相同的字符表示禁用指定的值。

文件结构地址、使用计数、标志和节点地址可用于更容易地检测子进程继承的相同文件以及不同进程之间的相同文件。`lsof` 的列输出可以通过包含这些值的列进行排序并列出以识别相同文件，或者可以通过 AWK 或 Perl 后过滤脚本或 C 程序解析 `lsof` 的字段输出。

- `+- f` 指定字符 `f` 用于选择供另一个程序处理的输出字段，以及终止每个输出字段的字符。每个要输出的字段用 `f` 中的单个字符指定。字段终止符默认为 `NL`，但可以更改为 `NL (000)`。参见 `OUTPUT FOR OTHER PROGRAMS` 中关于字段识别字符和字段输出过程的描述。

当字段选择字符为空时，选择所有标准字段（出于兼容考虑，原始设备文件、安全上下文和节点字段除外），并使用 NL 字段终止符。

当字段选择字符仅包含一个零 (`'0'`) 时，选择所有字段（出于兼容考虑，原始设备文件除外），并使用 NUL 终止字符。

其他字段及其关联的字段终止字符组合必须在 `f` 中通过显条目设置，如 `OUTPUT PROGRAMS` 节所述。

当字段选择字符识别出 `lsof` 通常不列出的项目时——例如 PPID，通过 `-R` 规格指定字段字符——例如“FR”进行选择——也会选择该项目的列出。

- `+-g` 排除或列出可选进程组标识 ID (PGID) 数字在逗号分隔的集合（例如“123”或“123,456”）中的进程的文件列出。（集合中不应有空格。）

PGID 排除。

多个 PGID 在参与 AND 选项选择之前会合并到一个 OR 集合中。然而，PGID 排除在不进行 OR 或 AND 运算的情况下应用，并在其他选择标准之前生效。

- `+-i` 选择列出可选进程组标识 ID (PGID) 数字在逗号分隔的集合（例如“123”或“123,456”）中的进程的文件列出。（集合中不应有空格。）

PGID 排除。

多个 PGID 在参与 AND 选项选择之前会合并到一个 OR 集合中。然而，PGID 排除在不进行 OR 或 AND 运算的情况下应用，并在其他选择标准之前生效。

- `+-i` 选择列出可选进程组标识 ID (PGID) 数字在逗号分隔的集合（例如“123”或“123,456”）中的进程的文件列出。（集合中不应有空格。）

Internet IPv6 out address ::1, port 1234UDP: UDP service port tcp@lsof.it:513 TCP, port and host name lsof.itat tcp:foo:1-10,smtp,99 - TCP, port 1 through 10, service smtp, port 99, host name tcp@bar:1-smtp - TCP, port 1 through $smtp, host bar :time - 无论是 tcp, UDP 或 UDPLITE 服务端口。

- `-K` 在支持任务（线程）报告的方言上列出进程的任务（线程）列表。（如果帮助输出——即 `-h` 或 `-q` 选项的输出显示了此选项，则表示该方言支持任务（线程）报告。）

- 当 Linux 上同时指定 `-K` 和 `-a` 时，主进程的任务将由其他选项选择，主进程也将像任务一样被列出，但没有任务 ID（TID）。参见 OUTPUT 部分中 TID 列的描述。）



进入 `/path/to/xxx` 目录，找到 `xxx.json`。

## 线程与任务继承

如果 FreeBSD 版本支持线程，所有线程都将与其 ID 一起列出。通常情况下，线程和所有任务继承调用者的文件，但可能会关闭并打开其他文件，因此 `lsof` 始终报告线程和任务打开的文件。

## 选项说明

### `-k k`
指定一个内核内存文件 `k`，以代替 `/vmunix`, `/mach` 等。在 IBM RISC/System 6000 上的 AIX 上无法使用 `-k`。

### `-l`
抑制将用户 ID 转换为登录名。当登录名查找工作正常或速度缓慢时，此选项也有用。

### `+-L`
启用 `'+'` 或禁用 `'-'` 文件链接计数的列出，前提是这些计数可用——例如，套接字、FIFO 和管道是不可用的。

当指定 `+L` 后没有跟随数字（默认值）时，将列出所有链接计数。

当 `-L` 后面跟随一个数字时，仅列出链接计数小于该数字的文件。`-L` 后可以不跟任何数字。`"+L1"` 格式的指定将选择已删除（unlinked）的打开文件 `"-L"` 格式的指定将选择指定文件系统中已删除的打开文件。对于其他链接计数比较，请使用字段输出 `-F` 和后处理脚本或程序。

### `+-m m`
指定一个备用内核内存文件 `m`，或激活表补充处理。

选项形式 `-m` 指定一个内核内存文件 `m`，以代替 `/dev/kmem` 或 `/dev/mem`——例如崩溃转储文件。

选项形式 `+m` 请求将一个补充文件写入标准输出文件。所有其他选项将被静地忽略。

挂载补充文件中每个挂载的文件系统有一行，包含挂载的文件系统目录，后跟一个空格，然后是十六进制格式的 `"0x"` 设备号——例如 `/0x801`

当 `lsof` 无法通过 `stat(2)` 或 `lstat(2)` 获取设备号时，可以使用补充文件获取文件系统的设备号。

选项形式 `+m` 将 `m` 标识为挂载补充文件。

注意：并非所有支持的方言都可用 `+m` 和 `-m` 选项。检查 `lsof -h` 或 `-z` 的输出以查看这些选项是否可用。

### `+-M`
启用 `+` 或禁用 `'-'` 在支持端口映射的 TCP、UDP 和 UDP 端口上的 portmapper 注册报告。

默认报告模式由 `lsof` 构建者通过方言头文件中的 `HASPMMAPENABLE` #define 设置；`lsof` 分发时已创建 `HASPMAPENABLE` #define，因此默认禁用 portmapper 注册，必须通过 `+M` 请求。指定 `lsof -h` 或 `-z` 选项将返回默认模式。在已禁用时禁用或已启用时启用将被忽略。当启用 portmapper 注册报告时，`lsof` 会在本地 TCP、UDP 或 UDP 端口号或服务名称后的方括号中显示 portmapper 注册（如果有）——例如 `"1234[name]"` 或 `"name[100083]"`。注册信息可能是名称或数字，取决于注册程序在注册端口时向 portmapper 提供的内容。

当启用 portmapper 注册报告时，如果访问 portmapper 变得拥堵或停止，`lsof` 的运行可能会变慢甚至被阻塞。反转报告模式以确定 portmapper 注册日志是否正在减慢或阻塞 `lsof`。

为了 portmapper 注册报告，`lsof` 将 TCP、UDP 或 UDPITE 视为本地：它位于其包含内核结构的本地部分；或者如果它位于包含内核结构的远程部分，且本地远程 Internet 地址相同；或者如果位于包含内核结构的远程部分，且远程 Internet 地址为 `INADDR_LOOPBACK` `127.0.0.1`。当远程 Internet 地址与本地地址不在同一接口时，此规则可能导致 `lsof` 忽略多接口机器上的某些远程端口。

进一步讨论 portmapper 注册报告问题请 FAQ。

portmapper 注册报告仅支持具有 RPC 头文件的方言。当支持 portmapper 注册报告时，`-h` 或 `-z` 帮助输出将显示 `+-M` 选项。

### `-n`
抑制将网络数字转换为主机名。抑制转换可能会让 `lsof` 更快。当主机查找工作不正常时，此选项也有用。

### `-N`
选择列出 NFS 文件。

### `-s`
指导 `lsof` 始终显示偏移量。这会导致 `SIZE/OFFSET` 列标题发生更改。注意：在某些 Unix 方言上，`lsof` 无法从数据源获取准确或一致的偏移量信息。咨询 `lsof` FAQ 以获取更多信息。

`-o` 和 `-s` 选项是互斥的；不能同时指定。当两者都未指定时，`lsof` 将根据文件类型显示大小或偏移量 `-`。

`-o` 定义打印在大小后的十进制数字 `o`。值为 `0`（无限制）将限制 `lsof` 使用 `-s` 进行仅限偏移量的输出。此选项**并不会**指示 `lsof` 始终显示偏移量；指定 `-o`（不带后随数字）仅在混合大小和偏移量输出中显示位数。因此，为了指示 `lsof` 显示带有 10 位小数的偏移量：允许大小后的默认位数为 9，但可能被 `lsof` 构建者更改。在 `-h` 或 `-z` 选项的输出中构建 `-o` 选项的描述以定义正在生效的默认值。

`lsof` 跳过了避免被某些内核操作阻塞的策略——即在子进程中执行。虽然使用此选项将减少 `lsof` 的启动开销，但在内核不响应函数时，可能会导致 `lsof` 挂起。请 `BLOCKS AND TIMEOUTS AND AVOIDING KERNEL BLOCKS` 部分获取更多关于可能阻塞 `lsof` 的内核操作的信息。

### `-p`
排除或选择进程文件，其标识 `PID` 数字位于逗号分隔的集合——例如 `"123"` 或 `"123,456"`。集合中不应有空格。包含 `^`（否定）的 PID 数字表示排除。多个进程 ID 在参与 AND 选项选择之前合并到单个集合中。然而，PID 排除是在 OR 或 AND 生效之前适的。

### `-P`
抑制将网络文件中的端口号转换为端口名。抑制转换可能会让 `lsof` 运行得快一点。当端口查找工作不正常时，此选项也有用。

### `+r [t[m<fmt>]]`
将 `lsof` 置于重复模式。在该模式下，`lsof` 打开由其他选项选择的文件，延迟 `t` 秒（默认十五秒），然后重复列表，重复地延迟和列出，直到由选项前缀定义的条件停止。

如果前缀为 `-`，重复模式是无限的。`lsof` 必须通过中断信号或退出信号来终止。

如果前缀为 `+`，当没有列出任何打开的文件时，重复模式将结束第一个循环——当然，`lsof` 将通过中断信号或退出信号停止。重复模式因为没有列出文件而结束，如果曾列出过任何文件，进程退出码将为零；如果曾列出过一个或一个都没有，则非如此。

`lsof` 标记每次列表的结束：如果正在进行字段输出（指定了 `-F` 选项），默认标记为 `m`；否则，默认标记为 `====`。该标记后紧跟一个换行符 `NL`。

可选的 `<fmt>` 参数指定了标记行的格式。紧跟在 `'m'` 后的 `<fmt>` 字符被解释为指向 `strftime(3)` 函数的格式说明，前提是该方言的 C 库中同时存在该函数和 `localtime(3)` 函数。关于其格式说明中可能出现的内容，请参阅 `strftime(3)` 的文档。当使用 `-F` 选项请求字段输出时，`<fmt>` 不能包含换行符 `%n`。另注意，当 `<fmt>` 包含空格或其他影响 shell 对参数解释的字符时，必须对 `<fmt>` 进行适当引用。

重复模式减少了 `lsof` 的启动开销，因此与在 shell 脚本中反复调用 `lsof` 相比，使用这种模式更高效。

为了最有效地使用重复模式，请避免在使用其他 `lsof` 选择选项时配合 `+r`，以便将 `lsof` 对内核内存的访问降至最低。在进程级别过滤的选项——例如 `-c`, `-g`, `-p`, `-u`——是最高效的选择器。

重复模式在与字段输出（见 `-F` 选项说明）以及监控 `awk` 或 `Perl` 脚本或 C 程序配合使用时非常有用。

直接让 `lsof` 在 `PPID` 列中列出父进程 ID。

### `-s [p:s]`
单独的 `s` 引导 `lsof` 始终显示文件大小。它会将 `SIZE/OUT` 输出列改为 `SIZE`。如果文件没有大小，则不显示任何内容。

可选的 `-s p:s` 形式仅某些选定的方言可用，并且当 `-h` 或 `?` 提供帮助列表时显示。

当可选形式可用时，`s` 后面跟着一个协议名称 `p`，`TCP` 或 `UDP`，随后是一个冒号 `:` 和一个用逗号分隔的协议名称列表，该选项情况将排除状态名称对应的 TCP 和 UDP 文件。

### `-V`
指示 `lsof` 指出它被要求列出但未找到的项目 - 命令名、文件名、Internet 地址或文件、登录名、NFS 文件、PID、PGID 和 UIDs。

当其他选项与其他搜索选项进行“逻辑与 AND”操作时，编译时选项会限制某些文件的列出；当 AND 选项或编译时选项阻止列出包含已定位搜索项的打开文件时，`lsof` 可能不会报告未找到搜索项。

例如，`lsof -V -tCP@foobar -a d 999` 可能会报告无法定位 `"tCP@foobar"` 的打开文件，并且如果没有任何文件的文件描述符为 `999`，则可能不会列出任何内容。当编译时定义了 `HASNOSOCKSECURITY` 且它们阻止了打开文件的列出时，也会出现类似的情况。

### `+-w`
启用 `+` 或禁用 `-` 警告消息。

`lsof` 构建器可能选择默认禁用或启用警告消息。默认警告状态显示在 `-h` 或 `-?` 的输出中。当警告消息已经禁用时启用它们是可以接受的。

`-w` 选项选择 `-w`。

### `-x [l]`
可能配合 `+d` 和 `+D` 选项，在扫描目录 `+d` 或目录树 `+D` 时处理符号链接和文件系统点。

如果指定了 `-x` 但没有后续参数，必须以 `-` 或 `+` 开头。

`'f'` 参数启用文件系统点处理；`'l'` 符号链接处理。

`-x` 选项可能在未提供 `+d` 或 `+D` 选项的情况下。

### `-X`
这是一个特定方言的选项。

AIX：IBM RISC/System 6000 请求报告执行的文件和共享库引用。

警告：由于此选项使用了内核 `readx()` 函数，在繁忙的 AIX 系统上可能会导致进程完全挂起，无法被杀死或停止。

默认情况下 `readx()` 是禁用的。在 AIX 5L 及以上版本中，`lsof` 可能设置 setuid-root 权限来执行此选项。

`lsof` 构建器可能限制 UID 为 root 的进程的 `-X` 选项。

如果已执行此操作，`-X` 选项将出现在 `-h` 或 `-?` 输出中，除非进程的真实 UID 为 root。

默认 `lsof` 分布允许任何 UID 指定 `-X`。

当使用 AIX `readx()` 时，`lsof` 可能无法报告所有文本和加载器引用，这是一个已知的“段 ID 错误”。

`lsof` 或其他进程访问内核某些内存区域的 `readx()` 函数可能会触发段 ID 错误。通过 `open(2)` 使用该选项可能会导致无限循环，从而挂起进程。

Linux：

此 Linux 选项请求 `lsof` 跳过所有打开的 TCP、UDP 和 UDP6 IPv4 和 IPv6 文件的报告。当系统存在大量的打开 TCP、UDP 和 UDP6 文件时，此 Linux 选项非常有用，因为处理 `/proc/net/tcp*` 和 `/proc/net/udp*` 文件中的信息会耗费 `lsof` 大时间，且这些报告并不感兴趣。

使用此选项时要小心，仅在你确定想要 `lsof` 显示的信息与打开的 TCP、UDP 或 UDP 套接无关时使用。

Solaris 10 及以上版本请求已删除文件（即通过 `rm(1)` 或 `unlink(2)` 移除）的缓存路径。

缓存路径后跟随字符串 `"(deleted)"`，表示打开该文件的路径已被删除。

由于对路径进行的中间更改（即通过 `mv(1)` 或 `rename(2)` 重命名）未记录在缓存路径中，`lsof` 的是打开文件时的路径，而不是不同的最终路径。

### `-z [z]`
处理 Solaris 10 及更高版本的区域信息。如果没有后续参数，该选项指定在输出列中列出区域名称。`-z` 选项可能跟随区域名称 `z`。这导致 `lsof` 只列出翻译进程的打开文件。可以指定多个 `-z` 选项和对以形成命名区域列表。根据其他选项和参数指定的条件，任何区域的任何打开文件将被列出。

### `-Z [Z]`
处理 SELinux 安全上下文。当运行的 Linux 内核禁用了 SELinux 时，“Z” 字段输出字符的支持被抑制。参见 `FOR OTHER PROGRAMS` 以获取更多关于 ‘Z’ 字段输出字符的信息。

*name* 中指定了通它的某个路径。例如，如果路径是 `/dev/log`，且当工作目录为 `/dev` 时启动了 `lsof` 搜索，那么 *name* 可能是 `/.log`。

如果 *name* 不是上述任何一个，`lsof` 将列出任何设备和 inode 节点与指定路径 *name* 匹配的已打开文件。

如果你还指定了 `-b` 选项，你可能安全指定的 *names* 只有那些挂载表提供了备用设备号的文件系统。更多信息请参见 **AVOIDING KERNEL BLOCKS** 和 **ALTERNATE DEVICE NUMBERS** 部分。

多个文件名在参与 AND 选项选择之前会合并成单个 OR 逻辑组合。

## AFS

`lsof` 支持对以下方言的 AFS 文件进行识别：

- AIX 4.1.4 `AFS 3.4a`
- HP-UX 9.0.5 `AFS 3.4a`
- Linux 1.2.13 `AFS 3.3`
- Solaris 2.[56] `AFS 3.4a`

它可能识别这些方言其他版本的 AFS 文件，但这些版本尚未经过测试。取决于 AFS 的实现方式，`lsof` 可能会识别其他方言中的 AFS 文件，或者在支持的方言中识别 AFS 文件时遇到困难。

当 AFS 内核支持通过动态模块实现，且这些地址未出现在内核变量名列表中时，`lsof` 可能难以识别支持方言中 AFS 文件的所有方面。在这种情况下，`lsof` 可能必须猜测 AFS 文件的身份，并可能无法从内核获取计算 AFS 卷节点号所需的卷信息。当 `lsof` 无法计算卷节点号时，会在 `NODE` 列中报告为空。

在 `lsof` 的某些方言实现中，可以使用 `-A` 选项来指定可能找到动态模块内核地址的符号列表文件。当此选项可用时，它将出现在响应 `-h` 或 `-?` 的 `lsof` 帮助输出中。

参阅 `lsof` FAQ 获取有关动态模块、其符号以及它们如何影响 `lsof` 选项的更多信息。

由于 AFS 路径查找似乎没有参与内核的缓存操作，`lsof` 无法识别 AFS 文件的路径名称组件。

## SECURITY

`lsof` 有三个可能引起安全关注的功能。首先，默认编译模式允许任何人使用它列出所有打开文件。其次，默认情况下，它会在执行 `lsof` 的用户 ID 的主目录中创建一个用户可读和用户可写的设备缓存。第三，`-k` 和 `-m` 选项命名了备用的内核列表或内存文件。

对列出所有打开文件的限制受编译时 `HASSECURITY` 和 `HASNOSOCKSECURITY` 选项的控制。当定义了 `HASSECURITY` 时，`lsof` 仅允许 root 用户列出所有打开文件。非 root 用户仅可以列出用户标识与 `lsof` 进程真实用户 ID 相同的进程的打开文件。

然而，如果 `HASSECURITY` 和 `HASNOSOCKSECURITY` 都已定义，任何人都可以列出打开的套接字文件，只要它们通过 `-i` 选项选中。

当未定义 `HASSECURITY` 时，任何人都可以列出所有打开文件。

响应 `-h` 或 `-?` 选项的帮助输出给出了 `HASSECURITY` 和 `HASNOSOCKSECURITY` 定义的状态。

参阅 `lsof` 分发版 `README` 文件的章节，获取启用 `HASSECURITY` 和 `HASNOSOCKSECURITY` 选项构建 `lsof` 的信息。

用户可读和用户可写设备缓存的创建受编译时 `HASCACHE` 选项的控制。详情请参见 `DEVICE CACHE FILE` 部分及其后续章节。安全考虑方面重要的是：在默认 `lsof` 分发版中，如果以 root 身份执行 `lsof` 的真实用户 ID，设备缓存文件将写入 root 的主目录——例如 `/root`。当未定义 `HASCACHE` 时，`lsof` 不写入或创建设备缓存文件。

当定义了 `HASCACHE` 时，响应 `-h`、`-D` 或 `-?` 选项的 `lsof` 帮助输出提供设备缓存文件的处理信息。当未定义 `HASCACHE` 时，`h` 或 `-?` 输出将产生 `-D` 选项描述。

在决定禁用设备缓存文件功能之前——请阅读 `lsof` 分发版中的 `00CACHE` 文件和 `lsof` FAQ。

**如有疑问，可以使用 `-Di` 选项临时禁用设备缓存文件的使用。**

当 `lsof` 使用 `-k` 和 `-m` 选项声明备用内核列表或内存文件时，`lsof` 会检查用户的读取权限 `access(2)`。此举意是为了防止 `lsof` 模式可能赋予的任何特殊权限使其能够无法通过真实用户 ID 权限访问的文件。

## OUTPUT

本节描述了 `lsof` 为每个打开文件的信息。有关可由另一个程序处理的输出附加信息，请参见 `OUTPUT FOR OTHER PROGRAMS` 部分。



`lsof` 仅打印可打印的（由 `isprint(3)` 定义）8 位字符。（注：原文此处存在大量重复，翻译已按逻辑流处理）。

### 字段说明

- `PID`: 进程的标识符。
- `TID`: 任务（线程）标识符，如果该方言支持任务（线程）报告且正在列出任务（线程）。Linux 中的空 `TID` 列表示非任务。（注：此处的 OCR 文本非常乱码）。
- `ZONE`: Solaris 10 及更高版本的区域名称。此列必须通过 `-z` 选项选择。
- `SECURITY-CONTEXT`: SELinux 安全上下文。此列必须通过 `-Z` 选项选择。注意，当运行内核中禁用 SELinux 时，`-Z` 选项会被抑制。
- `PPID`: 进程的父进程标识符。仅在指定了 `R` 选项时显示。
- `PGID`: 与进程相关的组标识符。仅在指定了 `-g` 选项时显示。
- `USER`: 进程所属的用户 ID 或登录名，通常与 `ps(1)` 相同。在 Linux 上，它是拥有 `/proc` 目录的用户 ID，可能在其有效 ID 时有所不同。
- `FD`: 文件描述符。

| FD | 描述 |
|---|---|
| `cwd` | 工作目录 |
| `Lnn` | 库 (AIX) |
| `err` | 错误 |
| `jld` | 监狱 (FreeBSD) |
| `...` | ... |

访问；如果模式未知且没有锁字符，则显示空格；

跟随；如果模式未知且后续有锁字符，则显示 `-`。

模式后紧跟以下锁字符之一，描述了应用于文件的锁类型：

- `N` 表示未知类型的 Solaris 锁；`r` 表示对文件部分的读锁；`R` 表示整个文件的读锁；`w` 表示对文件的写锁；`W` 表示整个文件的写锁；`u` 表示任意长度的读取和锁定；`U` 表示未知类型的锁；`x` 表示对文件部分的 SCO OpenServer Xenix 锁；`X` 表示对整个文件的 SCO OpenServer Xenix 锁；如果没有锁，则显示空格。

有关锁信息字符的更多信息，请参阅 `LOCKS` 章节。

`FD` 列包含一个字段，用于在后处理脚本中解析。

## `TYPE`（类型）

- `+` 是与文件相关的节点类型 - 例如 `GDIR`, `GREG`, `VDIR`, `VREG` 等。
- 或 `"IPv4"` 表示 IPv4 套接字；
- 或 `"IPv6"` 表示打开的 IPv6 网络网络文件 - 即使其地址是 IPv4，也映射在 IPv6 地址中；
- 或 `"ax25"` 表示 Linux AX.25 套接字；
- 或 `"inet"` 表示 Internet 域套接字；
- 或 `"lla"` 表示 HP-UX 链路级访问文件；
- 或 `"rte"` 表示 `AF_ROUTE` 套接字；
- 或 `"sock"` 表示未知域套接字；
- 或 `"unix"` 表示 UNIX 域套接字；
- 或 `"x.25"` 表示 HP-UX x.25 套接字；
- 或 `"BLK"` 表示块特殊文件；
- 或 `"CHR"` 表示字符特殊文件；
- 或 `"DEL"` 表示已删除；
- 或 `"DIR"` 表示目录；
- 或 `"DOOR"` 表示 DOOR；
- 或 `"FIFO"` 表示 FIFO 特殊文件；
- 或 `"KQUEUE"` 表示 BSD 风格的事件队列文件；
- 或 `"LINK"` 表示符号链接；
- 或 `"MPB"` 表示复用块文件；
- 或 `"MPC"` 表示复用字符文件；
- 或 `"NOFD"` 表示 `/proc/<PID>` 目录路径出现在 `NAME` 列，后跟错误消息；
- 或 `"PAS"` 表示 `/proc/as` 文件；
- 或 `"PAXV"` 表示 `/proc/auxv` 文件；
- 或 `"PCRE"` 表示 `/proc/cred` 文件；
- 或 `"PCTL"` 表示 `/proc` 控制文件；
- 或 `"PCUR"` 表示当前 `/proc` 进程；
- 或 `"PCWD"` 表示 `/proc` 当前工作目录；
- 或 `"PDIR"` 表示 `/proc` 目录；
- 或 `"PETY"` 表示可执行类型 (`etype`)；
- 或 `"PFD"` 表示 `/proc` 文件描述符；
- 或 `"PFDR"` 表示 `/proc` 文件描述符目录；
- 或 `"PFIL"` 表示 `/proc` 可执行文件；
- 或 `"PPPR"` 表示 `/proc` 寄存器集；
- 或 `"PGD"` 表示 `/proc/pagedata` 文件；
- 或 `"PGID"` 表示 `/proc` 分组通知文件；
- 或 `"PIPE"` 表示管道；
- 或 `"PLC"` 表示 `/proc/lwpctl` 文件；
- 或 `"PLDR"` 表示 `/proc/lpw` 目录；
- 或 `"PLDT"` 表示 `/proc/ldt` 文件；
- 或 `"PLPI"` 表示 `/proc/lsinff`；
- 或 `"PLST"` 表示 `/proc/lstatus` 文件；
- 或 `"PLU"` 表示 `/proc/usage` 文件；
- 或 `"PLWG"` 表示 `/proc/windows` 文件；
- 或 `"PLWI"` 表示 `/proc/lwpsinfo` 文件；
- 或 `"PLWS"` 表示 `/proc/lpusage` 文件；
- 或 `"PLWU"` 表示 `/proc/usage` 文件；
- 或 `"PLWX"` 表示 `/proc/xregs` 文件；
- 或 `"MAP"` 表示 `/proc` map 文件 (`map`)；
- 或 `"PMEM"` 表示 `/proc` 内存镜像文件；
- 或 `"PNTF"` 表示 `/proc` 进程通知文件；
- 或 `"POBJ"` 表示 `/proc/object` 文件；
- 或 `"PODR"` 表示 `/proc/object` 目录；
- 或 `"POLP"` 表示旧格式 `/proc` 轻量文件；
- 或 `"POPF"` 表示旧格式 `/proc` PID 文件；
- 或 `"POPG"` 表示旧格式 `/proc` 页数据文件；
- 或 `"PORT"` 表示 SYSV 命名管道；
- 或 `"PREG"` 表示 `/proc` 寄存器文件；
- 或 `"PRMP"` 表示 `/proc/rmap` 文件；
- 或 `"PRID"` 表示 `/proc` 根目录；
- 或 `"PSGA"` 表示 `/proc/sigact` 文件；
- 或 `"PSIN"` 表示 `/proc/psinfo` 文件；
- 或 `"PSTA"` 表示 `/proc` 状态文件；
- 或 `"PSXSEM"` 表示 POSIX 信号量文件；
- 或 `"PSXSHM"` 表示 POSIX 共享内存文件；
- 或 `"PSUG"` 表示 `/proc/usage` 文件；
- 或 `"PW"` 表示 `/proc/watch` 文件；
- 或 `"PXMP"` 表示 `/proc/xmap` 文件；
- 或 `"REG"` 表示普通文件；
- 或 `"SMT"` 表示共享内存传输文件；
- 或 `"STSO"` 表示流套接字；
- 或 `"UNNM"` 表示未知类型的 OpenServer 特殊文件；
- 或 `"XSEM"` 表示 OpenServer 信号量文件；
- 或 `"XSD"` 表示 OpenServer 共享数据文件；对应的名称未知。

## `FILE-ADDR`（文件地址）

- 当指定为 `+f` 时，`+` 包含内核文件地址。

## `FCT`（文件计数）

- 当指定为 `+f` 时，`+` 包含内核结构中的引用计数。

## `FILE-FLAG`（文件标志）

- 当指定为 `g` 或 `G` 时，`+` 包含内核结构中 `flag` 成员的内容和每个进程标志（如果可用）；`G` 导致它们以十六进制形式显示；`g` 为简写名称；可能会显示用逗号分隔的两个列表；第一个列表可能包含以下值的简写：

- `AIO` 异步 I/O (例如 `FAIO`) `ASYN` I/O (例如 `FASYNC`) `BAS` 块，且如果正在使用中则设置；`BSS` 块 复制 避免 `CIO` `CLONE` `CLORD` `CR` `DEFER` `DEFI` `FLU` `DOOC` `DSYN` 任何 `OVO` 条目仅用于 `EXE` `FSYN` 同步写入 `ungp()` (AIX) `GCMK` 标记 `hasck` `LG` 大文件 `MNT` `MSYN` `NTRY` 不更新 `AT8` `BDRM` `NBIO` `SYS` `NBF-` 缓冲已生效 `NC` 无延迟 `NDS` `NFFLK` `NMFS` `NOT` `NTTY` `TLY` `ORLM` `PAIS` `POSIX` 管道读取和记录 `REV` `RSYN` `Rw` 访问 共享锁 快照拍摄 套接字 `SQSH` 打开时设置 `SQS` 打开时设置 `SQS1` `SQS2` `STPI` `SWR` 唤醒 并行 I/O 同步 `WTG` `VH` 挂起 `VTX` 虚拟独占此名称列表源于方言头文件 `<fcntl.h>`, `<linux/fs.h>`, `<sys/fcntl.h>`, `<file.h>` 显示上述关系的头文件，第二个列表（分号后）可能包含来自此表的内核进程标志的简写：

- `own` 拥有 `ALLOC` `BHUP` 被 `SIGHW` 停止活动 `CLSG` 退出关闭 (`exec`) `fcntl(_SETFD))` 正在中 `RSV` 等待 `SHMT` `UF_SHMAT` (AIX) 使用 (多线程)

## `NODE-ID`（节点 ID）

- 当指定为 `+f` 时，`+`（或在某些方言中的 `INODE-ADDR`）包含文件节点的唯一标识符（通常是内核 `vnode` 和地址，有时也是设备号和节点号的拼接）。

## `DEVICE`（设备）

- `+` 包含设备号，用逗号分隔，适用于字符特殊文件、块特殊文件、目录或 NFS 文件；
- 在 Tru64 UNIX 下，文件系统节点为 `"memory"`；
- Solaris 套接字流的私有数据区域地址；
- 标识文件的内核引用地址（例如，内核引用地址可用于 FIFO）；

Linux AX.25 套接字的基地址或设备名称。通常显示 Tru64 内核地址的低三十位。

`SIZE/OFF` 或 `OFFSET` 是以字节计算的文件大小或偏移。只有在可用时在此列显示值。`lsof` 会根据文件类型和 `lsof` 版本显示适当的大小或偏移。在 Unix 方言中，`lsof` 无法从内核数据源获取准确或一致的文件偏移信息，对于某些类型的文件（例如套接字）。对于没有真实大小的文件（例如套接字、FIFO、管道），`lsof` 显示其缓冲区的内容（例如 TCP 窗口大小）。请参考 `lsof` FAQ 获取更多信息。

文件大小以十进制显示；偏移量通常以十进制显示，如果是 8 位则前缀 `"0"`；如果超过 8 位则以十六进制显示并前缀 `"0x"`（查看 `-o` 描述了解 8 可能会变为其他值的情况）。因此，前缀 `"0"` 和 `"o"` 在列可能同时包含大小和偏移时标识偏移（例如其标题为 `SIZE/OFF`）。

如果指定 `-o` 选项，`lsof` 始终显示文件偏移（如果没有大小则不显示），并将列命名为 `OFFSET`。偏移量始终如所述开头为 `"0t"` 或 `"0x"`。`lsof` 用户可以通过 `-o` 选项控制从 `"0t"` 切换到 `"0x"`。查看其描述获取更多信息。

如果指定 `-s` 选项，`lsof` 始终显示文件大小（如果没有大小则不显示），并将列命名为 `SIZE`。`-o` 和 `-s` 选项是互斥的；不能同时指定。

- 是本地文件的节点号；
- 或是 NFS 未指定地址、IPv 或网络协议类型（例如 `"TCP"`）的 inode 号；而非用于流；
- 或是对于 HP-UX x.25 套接字的 `"CCIT"`；
- 或是 Linux AX.25 套接字设备的 IRQ 或 inode 号。
- 是文件所在的挂载点名称和文件系统名称；
- 或者是 `names` 选项中指定的文件名（在解析任何符号链接之后）；
- 或是字符设备或特殊设备的名称；
- 或是网络文件的本地和远程 Internet 地址；本地主机或 IP 号后跟一个冒号（`':'`）、端口 `":"`、以及两部分的远程地址；[注：原文为 `"->"`，可能意思是 `":"`]，以及两部分的远程地址；IP 地址可以以数字或名称出现，取决于 `-M`、`-n` 和 `-P` 选项；用颜色分隔的 IPv6 地址包含在方括号中；IPv4 `INADDR_ANY` 和 `IPv6_IS_ADDR_UNSPECIFIED` 地址以及零端口号后跟一个星号（`*`）；UDP 目的地址后可能跟上自上次数据包设置到目的地以来经过的时间；参数中的 TCP/TPI 信息——状态（例如 `"ESTABLISHED"`）、（`"Unbound"`）、队列大小和窗口大小（并非所有方言都支持）——类似于 `netstat(1)` 的报告；有关状态、队列大小和窗口大小的信息，请参见 `-T` 选项或 `OUTPUT FOR ALL PROGRAMS` 中 TCP/TPI 字段的描述；
- 或是 UNIX 域域套接字的地址或名称，可能包括流克隆设备、文件系统对象的路径名、本地和外部内核地址、套接字对信息以及绑定地址；
- 或是 NFS 文件的本地和远程挂载点名称；
- 或是 `"STR"`，后跟流或流字符设备名称，后跟 `"->"`，然后是流名称或由 `"->"` 分隔的流模块列表；又或是 `"STR":` 后面后跟 SCOpen 服务器设备和模块，由 `"->"` 分隔；
- 或是系统目录、`"—"`，以及 `lsof` 在选定方言的内核名称缓存中找到的路径名中的等数量分量（更多信息请参阅 `KERNEL NAME CACHE`）；
- 或是 `"PIPE->"`，后跟 Solaris 管道目的地址；
- 或是 `"COMMON:"`，后跟 `vnode` 设备信息结构的设备名称，或 Solaris 通用 `vnode`；
- 或是地址，后跟斜杠（`/`），后跟十四个逗号分隔的非 Internet 套接字地址字节；
- 或是 HP-UX x.25 本地地址，后跟虚拟连接号（如果有），后跟远程地址（如果有）；
- 或是对于已分离的 Tru64 UNIX 文件使用（dead）——通常是已标记了 `TIOCNoffset` `ioctl` 且被守护进程关闭的终端文件；
- 或是对于 FIFO 的读写偏移值使用 `"rd=<offset>"` 和 `"wr=<offset>"`；
- 或是对于 SCO OpenServer 的 `/dev/event` 设备文件使用 `"clone n:/dev/event"`，其中 `n` 是该文件的设备号；
- 或是对于由 `socketpair(3)` 网络函数创建的 Solaris 2.6、8、9 或 10 UNIX 域套接字使用 `("socketpair n")`；
- 或是对于没有关联协议块的套接字文件使用 `"no PCB"`，如果启用了套接字发送，则可选后跟 `"CANTSENDMORE"`，或者如果禁用了套接字接收（例如通过 `shutdown(2)` 函数），则后跟 `"CANTRCVMEM"`；
- 或是 Linux IPX 套接字的本地和远程地址，格式为 `<net>:[node]`，括号内为发送接收队列大小以及连接状态；
- 或是对于 UnixWare 7.1.1 及以上版本的内核 UNIX 域使用 `"drm"` 或 `"stream"`，可用时后跟冒号（`':'`）和本地路径名，可用时后跟 `">` 和十六进制远程路径名或套接字地址；
- 或是对于 Linux SCTP 套接字的关联值、关联索引、端点值、本地地址、本地端口、远程地址和远程端口；
- 或是 `"protocol: "` 后跟 Linux 套接字的协议属性。

对于支持 `"namesf"` 文件系统的方言，允许通过 `fattach(3)` 将一个文件附加到另一个文件，`lsof` 会 `NAME` 列中添加 `"FA:<address1><<address2>"`。`<address1>` 和 `<address2>` 是十六进制 `vnode` 地址。`<direction>` 将变为 `" <address2"` 已 `fattach` 附加到地址为 `<address1>` 的此 `vnode`；如果 `<address1>`（此 `vnode` 的 `vnode` 地址）已 `fattach` 附加到 `<address2>` 则变为 `">"`。如果 `<address1>` 已经出现在 `DEVICE` 列中，可以省略。

`lsof` 可能为打开的 Solaris 10 文件 `NAME` 列添加两个括号注释：如果 `lsof` 认为路径名的准确性存疑，则添加 `(?)`；如果指定了 `X` 选项且 `lsof` 检测到打开的文件路径名已被删除，则添加 `"deleted"`。咨询 `lsof` FAQ（FAQ 部分提供了位置）获取有关这些 `NAME` 列添加内容的更多信息。

# `LOCKS`

`lsof` 无法通过单个字符充分报告各种 UNIX 方言文件锁。它在单个字符中报告的内容是在内核中找到的信息与报告格式局限性之间的折中。

此外，当进程对文件持有的多个字节级锁时，`lsof` 只报告状态。

通过前缀识别（`'='` 是前缀的一部分）：`QR=` 读取查询大小=`<发送查询大小选项和值（并非所有方言）`SS=<套接字状态（并非所有方言）`ST=<连接状态>` 及其值（并非所有方言）`WR=<窗口写入大小>`（并非所有方言）（并非所有支持 UNIX 系统都会报告 TCP/IP 信息。对于 `-T` 选项的 `-h` 或 `?` 帮助输出将显示如何请求 TCP/IP 报告。）使用用户 ID `Z` Solaris 0 及更高版本区域 `Z` SELinux 安全字符（在禁用 SELinux 时被抑制）或使用 NULL 字段字符替换 `NL` 1-9 依赖于方言的字段标识符（`-F` 的输出标识了在特定方言字段中要查找的信息。）

你可以通过指定 `-F7` 选项来在联机上获取关于这些字符及其描述的在线信息。（像你使用的 shell 一样转义 `'?'` 字符）。关于字段内容的更多信息可以在 `OUTPUT` 部分找到。

例如，`"-F pcf"` 将使用 `NL` 字段终止符选择 ID (`'p'`)、命令名 (`'c'`)、描述符 (`'f'`) 和文件名 (`'n'`)；`"F pfn0"` 则使用 NUL (`0`) 字段终止符选择相同的输出。

`lsof` 不会为每个进程或文件生成所有字段，仅生成可用字段。字段之间是互斥的：文件设备字符和主/次设备号；文件节点和协议名；文件名和流信息；文件大小和偏移量。这些互斥集合中的其中一个将出现在字段输出中，但不会两个都出现。

通常，`lsof` 以 `NL` (`012`) 结束每个字段。可以指定 `0`（零）字段标识符将字段终止符字符更改为 `NUL` (`000`)。NULL 终止符对于 `xargs (1)` 可能更容易处理，或者或者用于那些引用机制可能无法轻松处理字段输出中字符范围的程序。当 `NL` 字段终止符存在时，`lsof` 以 `NL` (`012`) 结束每个进程和文件。

`lsof` 的分发版中包含了三个用于生成处理字段输出程序的辅助工具。第一个是 C 头文件 `lsof_fields.h`，它包含了字段标识字符的符号、存储在表中的索引以及可以编译到程序中的说明字符串。`lsof` 使用了此头文件。

第二个辅助工具是一组处理字段输出的示例脚本，用 `awk`、`Perl 4` 和 `Perl 5` 编写。它们位于 `lsof` 分发版的子目录下。



第三个辅助工具是用于 `lsof` 测试的库。测试套件用 C 编写，并使用字段输出来验证 `lsof` 的正确操作。可以在 `lsof` 分发版的 `tests/Llib.c` 文件中找到该库。该库使用了第一个辅助工具 `lsof_fields.h` 头文件。

# 阻塞与超时

`lsof` 可能会被它使用的某些内核函数阻塞 - `lstat(2)`、`readlink(2)` 和 `stat(2)`。这些函数会在内核中停顿，例如，当挂载的 NFS 文件系统的主机变得不可访问时。

`lsof` 尝试通过计时器和子进程来打破这些阻塞，但这些技术并非完全可靠。当 `lsof` 成功打破阻塞时，它将通过错误消息报告此中断。这些可以通过 `-t` 和 `-w` 选项抑制。

默认超时值可以通过 `-h` 或 `-?` 选项显示，并可以通过 `-S [t]` 选项进行更改。`t` 的最小值为两秒，但你应该避免小值，因为系统响应缓慢可能导致短超时意外过期，并可能在 `lsof` 产生任何输出之前停止它。

当 `lsof` 在访问挂载的文件系统信息期间必须打破阻塞时，它通常会继续，尽管关于打开文件的可用信息较少。

`lsof` 还可以通过指定 `-O` 选项使用可能阻塞此操作的内核函数，从而避免计时器和子进程的保护。虽然这允许 `lsof` 以较小的开销启动，但它让 `lsof` 完全暴露在可能阻塞它的内核状况之下。请谨慎使用此选项。

# 避免内核阻塞

你可以使用 **`b`** 选项告诉 `lsof` 避免使用会导致阻塞的内核函数。需要注意以下事项。

首先，使用此选项通常要求你的系统提供替代设备号，以替换 `lsof` 正常通过 `lstat(2)` 和 `stat(2)` 内核函数获取的设备号。有关替代设备号的更多信息，请参见 `ALTERNATE DEVICE NUMBERS` 章节。

其次，你无法为 `lsof` 指定定位的*名称*，除非它们是文件系统名称。这是因为 `lsof` 需要知道 `lsof` 选项中以*名称*列出的文件的设备号和 inode 号，而 **`b`** 选项阻止了 `lsof` 获取它们。此外，由于 `lsof` 仅对有替代的文件系统拥有设备号，它定位文件系统上文件的能力完全取决于替代方案的可用性和准确性。如果没有可用替代方案，或者它们不正确，`lsof` 将无法在命名的文件系统上定位文件。

第三，如果 `lsof` 从你的系统挂载表中获取的文件系统目录名称是符号链接，`lsof` 将无法解析这些链接。这是因为 **`b`** 选项导致 `lsof` 避免使用用于解析符号链接的内核 `readlink(2)` 函数。

最后，使用 **`b`** 选项会导致 `lsof` 在需要使用 **`b`** 选项引导其使用的内核函数时发出警告消息。你可以通过指定 `-w` 选项来抑制这些消息。

# 替代设备号

在某些方言中，当 `lsof` 因为无法通过 `lstat(2)` 和 `stat(2)` 函数获取挂载文件系统的信息，或者因为你指定了 `-b` 选项而打破阻塞时，`lsof` 可以从挂载表中获取文件系统的设备号。如果可行，`lsof` 将返回设备号。（你可以通过指定 `w` 选项来抑制输出）

如果你的挂载表包含选项字符串，可以通过为没有该字段的挂载点添加 `devxxxx` 字段来协助此过程。注意：最近的 Solaris `/etc/mtstab` 或 Linux `/proc` 等挂载表是只读的，无法修改。

你可能还可以使用 `+m` 和 `m` 选项提供设备号，前提是方言支持这些选项。检查 `lsof` 的 `-h` 或 `-` 选项的输出查看是否可用 `+m` 和 `m`。

文件系统设备号十六进制值的 `"xxxx"` 部分。（参考 `lstat(2)` 和 `stat(2)` 函数的 `st_dev` 字段获取适用于你文件系统的相应值）。这里有一个 Solaris 2.6 `/etc/mtstab` 的 NFS 挂载文件系统示例：

```
nfs ignore, dev=2a40001
```

在挂载表中拥有 `"devxxxx"` 条目是有优势的，特别是对于从 NFS 服务器挂载的文件系统。当远程服务器崩溃，你想通过在其中一个客户端上运行 `lsof` 来识别其用户时，`lsof` 可能无法从 `lstat(2)` 和 `stat(2)` 函数获取该文件系统的输出。如果它能从挂载表中获取文件系统的设备号，它将能够显示在崩溃的 NFS 服务器上打开的文件。

某些方言不使用 ASCII;/etc/mtstab 或 /etc/mtstab 作为挂载表，但其内部挂载表可能提供替代设备号。这包括 AIX、Apple Darwin、FreeBSD、NetBSD、OpenBSD 和 Tr64 UNIX。`lsof` 知如何获取这些方言的替代设备号，并在尝试 `lstat(2)` 或 `stat(2)` 文件系统被阻塞时使用它。

如果你不确定方言是否从挂载表为文件系统提供替代设备号，可以使用此 `lsof` 命令查看它是否报告了任何替代设备号：

```
lsof -b
```

寻找以 `"assuming dev=xxxx"` 开头的标准错误警告消息，来自 ...

# 内核名称缓存 (KERNEL NAME CACHE)

`lsof` 能够检查某些文件系统（排除 AFS）的内核名称缓存或其他内核设施（例如 ADVFS 4.x 的 `tag_to_path()`），并从中提取最近使用的路径名称组件。（AFS 文件系统路径查找不使用内核名称缓存；某些 Solaris VxFS 文件系统操作显然也不使用它。）

`lsof` 在 `NAME` 列中报告完整路径。如果 `lsof` 无法报告路径中的所有组件，它会在 `NAME` 列中报告文件系统名称，随后跟着一个空格、两个 `-` 字符、另一个空格，以及它已定位的名称组件，并用 `/` 隔开。

当 `lsof` 处于重复模式时——即指定了 `-r` 选项——它对同一个文件报告路径名称组件的程度在每个循环之间可能会不同。这是因为其他运行的进程会导致内核从其名称缓存中删除条目并替换为其他项。

`lsof` 使用内核名称缓存来识别文件路径可能会在某些情况下导致它报告错误的组件。当内核名称缓存使用设备号和节点号作为键（例如 SCO OpenServer），且在快速变化的文件系统上使用键时，就会发生这种情况。如果 UNIX 方言的内核在文件取消链接（unlink）时没有清除该文件的名称缓存，`lsof` 可能会在缓存中找到错误条目的引用。`lsof` FAQ（FAQ 部分提供了其位置）上有关于此情况的更多信息。

`lsof` 可以报告以下方言的路径名称组件：

- FreeBSD HP-UX Linux FreeBSD NEXTSTEP OpenBSD OPENSTEP OpenServer SCO|Caldera UnixWare Solaris Tru64 UNIX

`lsof` 无法报告以下方言的路径名称组件：

- AIX

如果你想知道为什么 `lsof` 无法为某些方言报告路径名称组件，请参阅 `lsof` FAQ（FAQ 部分提供了其位置）。

## 设备缓存文件 (DEVICE CACHE FILE)

使用 `stat(2)` 函数检查 `/dev`（或 `/devices`）节点树的所有成员可能非常耗时。此外，`lsof` 需要的信息——设备号、inode 节点号和路径——很少发生改变。

因此，`lsof` 通常会维护一个缓存的 `/dev`（或 `/devices`）信息的 ASCII 文本文件（例外：基于 `/proc` 的 Linux `lsof`，它不需要）。构建 `lsof` 的本地系统管理员可以控制设备缓存文件的路径形成，从以下选项中选择：

- 来自 `-D` 选项的路径；
- 来自环境变量的路径；
- 系统级路径；
- 个人路径（默认值）；
- 由环境变量修改的个人路径。

咨询 `-h`、`-D?` 或 `?` 帮助选项的输出以获取设备缓存支持的当前状态。帮助输出列出了当前 `lsof` 调用中使用的默认读模式设备缓存文件路径。`-D` 选项列出了只读和可写缓存文件路径、任何适用环境变量的名称以及设备缓存路径格式。

`lsof` 可以通过完整性检查检测到当前设备缓存文件被意外或恶意地修改过，包括对文件内容进行计算和验证十六位循环冗余校验（CRC）总和。当 `lsof` 感到文件有问题时，它会发出警告并尝试删除当前缓存文件并创建一个新副本，但仅创建到进程可以合法写入的路径。

`lsof` 进程尝试读取设备缓存文件的路径可能与其可以合法写入的路径不相同。因此，当 `lsof` 感到它需要更新设备缓存文件时，它可能会选择一个不同的路径进行写入，而不是从读取错误或过时版本的路径进行写入。

如果可用，`-Dr` 选项将抑制新设备缓存文件的写入。（当不带路径参数的情况下指定时，它总是可用的。）

当系统添加了新设备时，设备缓存文件可能需要重建。由于 `lsof` 会比较设备缓存文件的 `mtime`（修改时间）与 `/dev`（或 `/devices`）目录的 `mtime` 和 `ctime`，它通常能检测到添加了新设备；在这种情况下，`lsof` 会发出警告并尝试重建设备缓存文件。

每当 `lsof` 写入设备缓存文件时，它会将所有权设置为执行进程的实际 UID，并将权限模式设置为 `0600`，将其读取和写入限制为文件所有者。

## 影响设备缓存文件访问的 lsof 权限 (LSOF PERMISSIONS THAT AFFECT DEVICE CACHE FILE ACCESS)

`lsof` 可执行文件的两个权限影响其访问设备缓存文件的能力。这些权限在安装 `lsof` 时由本地系统管理员设置。

第一个且较罕见的权限是 `setuid-root`。它在执行 `lsof` 时生效；其有效 UID 是 root，而其实际（即登录用户的 UID）不是 root。`lsof` 分发建议这些方言的版本运行 `setuid-root`。

- HP-UX 11.11 和 11.23 Linux

第二个更常见的权限是 `setgid`。当 `lsof` 进程的有效组 ID (GID) 设置为可以访问内核内存设备——例如“kmem”、“sys”或“system”时，它生效。

具有 `setgid` 的 `lsof` 进程通常在访问内核内存设备后放弃该权限。当此时，`lsof` 可以允许更宽松的设备缓存路径形成。`lsof` 分发建议这些方言的版本运行 `setgid`。

- AIX
- Apple
- FreeBSD
- HP-UX
- Linux
- Mac OS NEXTSTEP
- OpenBSD
- OPENSTEP
- OpenServer
- SCO|Caldera UnixWare
- Solaris
- SPARC
- Tru64 UNIX
- Ultrix
- V7
- VAX
- Xenix
- ZOS

（注意：AIX 的 `lsof` 还需要 setuid-root）

Linux 的 `lsof` 不设备缓存，因此赋予可执行文件的权限不适用于设备缓存。

## 来自 -D 选项的缓存路径 (DEVICE CACHE PATH FROM THE -D OPTION)

`-D` 选项提供了指定设备缓存路径的有限方法。它的功能是 `lsof` 使用的只读写缓存文件路径。

当 `-D b`、`r` 和 `u` 函数可用时，可以使用它们请求在特定位置构建缓存（`b[path]`）；读取但不重建（`r[path]`）；读取并重建（`u[path]`）。`b`、`r` 和 `u` 函数在某些条件下会受到限制。当软符号进程为 `setuid-root` 时，它们受到限制。使用 `r` 函数指定的路径始终是只读的，即使它是可用的。

当 `lsof` 进程运行 `setgid` 且不放弃 `setgid` 权限时，`b`、`r` 和 `u` 函数也会受到限制。（请在设备缓存访问部分查看通常不放弃 setgid 权限的实现。）

另一个 `-D` 函数 `i`（忽略）始终可用。

在可用时，`b` 函数告诉 `lsof` 使用 `stat(2)` 函数从内核读取设备信息并在指定的路径构建设备缓存文件。

可用时，`r` 函数告诉 `lsof` 读取设备缓存文件但不更新它。当带有路径参数 `-Dr` 时，它命名设备缓存文件路径。当不带路径参数指定时，`r` 函数总是可用的。如果 `lsof` 未以 `setuid-root` 运行并渲染了 setgid 权限，路径名可以随 `r` 函数。

可用时，`u` 函数告诉 `lsof` 尝试读取并使用设备缓存文件。如果它无法读取文件，或者发现文件内容错误或过时，它将从内核读取信息，并尝试写入更新版本的设备缓存文件，但仅写入它认为对 `lsof` 进程有效和实际 UID 都合法的路径。

# 来自环境变量的设备缓存路径

`lsof` 用于设备缓存文件的第二个选择是 `LSOFDEV` 环境变量的内容。如果 `lsof` 进程是 setuid-root，或者进程的实际 UID 为 root，则避免使用此选择。

对来自 `LSOFDEV` 环境变量的设备缓存路径有进一步限制：如果 `lsof` 进程未放弃 setgid 权限，`lsof` 将不会向路径写入设备缓存文件。（参见“影响设备缓存文件的权限”部分以获取不放弃 setgid 权限的实现。）

本地系统管理员可以在构建 `lsof` 时禁用 `LSOFDEV` 环境变量的使用，或更改其名称。参考 `-?` 的输出获取环境变量的名称。

# 系统级设备缓存路径

本地系统管理员可能在构建 `lsof` 时选择一个系统级设备缓存文件。该文件通常在系统启动或 `/dev/` 目录发生变化时由特殊的管理程序构建。如果已定义，它是 `lsof` 的第三个缓存路径选择。

通过检查 `-h` 或 `-?` 选项的输出，判断系统级缓存文件是否对本地安装生效。默认情况下，`lsof` 不会写入系统级缓存文件。必须通过 `-D` 函数显式命名。一旦文件被写入，程序必须将其权限更改为 `0644`（所有者读写、组读和其他读）。

# 个人设备缓存路径（默认）

`lsof` 分发版的默认设备缓存路径记录在执行 `lsof` 的实际 UID 的家目录下。家目录下添加了 `.lsof_hostname` 格式的第二个组件。这是 `lsof` 的第四个缓存路径选择，通常是默认值。如果在构建 `lsof` 时定义了系统级缓存路径，当 `lsof` 找不到系统级缓存文件时，将应用此第四选择。

这是 `lsof` 在读取设备缓存文件时使用两个路径的情况。第二个部分是 `hostname(2)` 返回的主机名。基名定义为 `hostname(2)` 输出中第一个 `.` 之前的字符，如果 `hostname(2)` 输出不包含 `.`。

设备缓存文件属于用户 ID 且仅该用户可读可写——即，其模式为 `0600`。执行 `lsof` 的给定主机上的每个实际 UID 都有一个设备缓存文件。从不同主机写入家目录的主机部分区分了设备缓存文件。

通过此方法形成的个人设备缓存路径代表 `lsof` 将尝试读取的设备缓存文件，如果其不存在或内容错误或过期，将尝试写入。

没有路径参数的 `-Dr` 选项将抑制新设备缓存文件的写入。

`-D?` 选项将列出构建设备缓存文件的格式规范。`lsof` 分发版的缓存文件中描述了格式规范中使用的转换。

# 修改后的个人设备缓存路径

如果本地系统管理员在构建 `lsof` 时定义了此选项，可以使用 `LSOFPERSATH` 环境变量的内容来添加个人设备缓存路径的组件。

`LSOFPERSATH` 变量的内容被插入到路径中，位置位于方言 `machine.h` 头文件的格式规范中，由本地系统管理员用 `%p` 转换标记处。（它放置在默认 `lsof` 分发版的家目录之后。）

因此，例如 `LSOFPERSATH` 包含 `LSO`，家目录为 `home/abe`，主机名为 `lsof.itap.purdue.edu`，且格式DC 格式是默认的（`%h%p.lsof_%L`），则修改后的设备缓存路径为：

```
/home/abe/lsof/.lsof_vic
```

当 `lsof` 进程设置为 setuid-root 或进程的实际 UID 为 root 时，忽略 `LSOFPERSATH` 环境变量。

如果 `lsof` 进程未放弃 setgid 权限，`lsof` 将不会写入修改后的个人设备缓存路径。（参见不放弃权限的实现。）

例如，如果你想使用 `LSOFPERSATH` 环境变量来创建一个个人设备缓存路径的子目录，而 `lsof` 未放弃其 setgid 权限，你必须允许 `lsof` 在标准路径创建设备缓存文件，并使用 shell 命令将其移动到你的子目录。

本地系统管理员可以：在构建 `lsof` 时禁用此选项；将环境变量名称从 `LSOFPERSATH` 更改为其他；更改格式将个人路径包含在其他地方；或完全排除个人路径组件。参考 `-?` 的输出获取格式规范。

# 诊断

错误通过消息标识。

如果检测到任何错误（包括无法找到名称、PID 或 UID），`lsof` 返回一 (1)。

如果没有检测到任何错误，`lsof` 返回零 (0)。

当 `lsof` 无法打开 `/dev` 时，它会发出警告。

## 示例

欲需更多详尽文档的示例，请参见 `lsof` 分发版的 `QUICKSTART` 文件。

列出所有打开的文件，使用：

```
lsof
```

列出所有打开的 Internet、x.25 和 UNIX 域文件，使用：

```
lsof -i -U
```

列出所有 PID 为 1234 的打开 IPv4 网络文件，使用：

```
lsof -i 4 -p 1234
```

假设 UNIX 方言支持 IPv6，仅列出 IPv6 网络文件，使用：

```
lsof -i 6
```

列出主机 `wonderland.cc.purdue.edu` 使用协议 513、514 或 515 的所有文件，使用：

```
lsof - @wonderland.cc.purdue.edu:513-515
```

列出 `mace.cc.purdue.edu` 上任何端口使用协议的所有文件（cc.purdue.edu 是默认域），使用：

```
lsof -i@mace
```

列出所有登录名为“abe”、或用户 ID 为 1234、或进程 ID 为 456、789 的打开文件，使用：

```
lsof -p 456,789 -u 1234,abe
```

列出设备 `/dev/hd4` 所有打开文件，使用：

```
lsof /dev/hd4
```

查找打开 `/u/abe/foo` 的进程，使用：

```
lsof /u/abe/foo
```

向打开 `/u/abe/bar` 的进程发送 SIGHUP信号，使用：

```
kill -HUP -t /u/abe/bar*
```

查找名为 `/dev/log` 的任何打开文件（包括一个 UNIX 域套接字），使用：



```
lsof /dev/log
```

# lsof -b /nfs/mount/point

要在抑制警告信息的情况下执行上述搜索，请使用：

```
lsof -bw /nfs/mount/point
```

要忽略设备缓存文件，请使用：

```
lsof -Di
```

要获取每个进程、每个文件描述符、每个文件设备号以及每个进程每个文件的文件节点号（inode）的 PID 和命令名称字段输出，请使用：

```
lsof -FpcfDi
```

要每 10 秒列出登录 ID 为 "abe" 的运行 lsof 命令的进程中描述符为 1 和 3 的文件，请使用：

```
lsof -c lsof -a 1d -3 -u abe -r10
```

要列出运行的命令长度恰好为四个字符且字符中包含 'o' 或 'O' 的进程的当前工作目录，请使用此 `-c` 选项的正则表达式形式：

```
lsof -c /\..$i -a -d cwd
```

要通过其关联的数字点格式地址查找 IP 版本 4 套接文件，请使用：

```
lsof -i@128.210.15.17
```

当 UNIX 方言支持 IPv6 时，通过其关联的数字冒号格式地址查找 IP 版本 6 套接文件，请使用：

```
lsof -i@[0:1:2:3:4:5:6:7]
```

当 UNIX 方言支持 IPv6 时，通过其包含连续零的关联数字冒号格式地址（例如环回地址）查找 IP 版本 6 套接文件，请使用：

```
lsof -i@::1]
```

要获取一个包含当前时间的重复模式标记行，请使用：

```
lsof -rm====%T====
```

要在上一个标记行中添加空格，请使用：

```
lsof -r "m==== %T ==="
```

# BUG

`lsof` 在搜索打开的文件时会读取内核内存，内核内存的快速变化可能会产生不可预测的结果。

当一个文件有多个记录锁时，锁状态字符（紧随文件描述符）源于对第一个锁结构的测试，而不是源于可能由多个锁结构描述的任何单个记录锁的组合。

除非以 root-UID 权限安装，否则 `lsof` 无法搜索具有限制访问权限的文件。否则，它仅限于搜索其用户或 set-GID 组（如果有）具有访问权限的文件。

原始套接字（例如用于 ping）get 目标地址的显示取决于 UNIX 操作系统。某些方言将目标地址存储在原始套接字的协议控制块中，某些则没有。

Lsof 无法总是像 `ls(1)` 那样表示 Solaris 设备。例如，`lstat(2)` 和 `stat(2)` 函数为挂载 CD-ROM 文件的目录（通常为 `/cdrom`）报告的主、次要设备号，与它们报告的挂载 CD-ROM 文件的设备（通常为 `/dev/sr0`）的设备号不同。（Lsof 报告的是目录编号。）

对 `/proc` 文件的支持仅适用于 BSD 和 Tru64 Unix 方言、Linux 以及来自 SYSV R4 的方言 - 例如 FreeBSD、OpenBSD、Solaris、UnixWare。

某些 `/proc` 文件项目——设备号、节点（node）和文件大小在某些方言中是不可用的。在 `/proc` 文件系统中搜索文件可能需要指定完整路径。

Linux 进程不显示任何文本（txt）文件描述符。除了当前工作目录、根目录和数字文件描述符外，所有文件项都标记为 mem。

Lsof 无法通过名称搜索 Tru64 UNIX 命名管道，因为它们的内核 `lstat(2)` 实现对命名管道返回了不适当的数字。

由于对内核数据的访问权限不足或内核数据错误，`lsof` 无法对 HP-UX 9.01、10.20 和 11.0 锁提供完整或正确的报告。（`lsof` 的 FAQ 部分提供了其位置。）

AIX 的 SMT 文件类型是伪造的。它是为了某些其类型 15 在 AIX `/usr/include/sys/file.h` 头文件中未定义的文件结构而创建的。创建此类文件结构的方法是运行 DISPLAY 变量设置为 ":0" 的 X。

在 `/proc` 下，`lsof` 的 `-f` 选项是不可用的，因为它是从内核内存读取的。

# 环境变量

`lsof` 可能会访问这些环境变量。

`LANG` 定义语言区域。请查看 `setlocale(3)`。

`LC_ALL`、`LC_TYPE` 等变量可以替代 `LANG`。请查看 ENVIRONMENT 部分。

`DECACHE` 定义了设备缓存文件的路径。请查看 ENVIRONMENT 部分获取更多信息。

`PATH` 定义了设备缓存文件。请查看 PATH 部分。

`PERSONAL PATH` 定义了修改后的设备缓存文件路径。请查看 PERSONAL PATH 部分获取更多信息。

# FAQ

常见问题及其解答（一个 FAQ）可在 `lsof` 发行版的 `00FAQ` 文件中找到。

该文件也可以通过匿名 ftp 从 `lsof.itap.purdue.edu` 获取。URL 为：

```
ftp://lsof.itap.purdue.edu/pub/unix/FAQ
```

| 路径 | 描述 |
| :--- | :--- |
| `/dev/kmem` | 内核内存 |
| `/dev/mem` | 物理内存 |
| `/dev/swap` | 分页内存 |
| `/lsof_hostname` | 设备缓存文件（后缀是 `gethostname(2)` 返回的主机名） |

## 作者

`lsof` 由 Purdue大学的 Victor Abell <abe@purdue.edu> 编写。许多其他人对 `lsof` 做出了贡献。他们列在 `lsof` 发行版的 `00CREDITS` 文件中。

# 发行

`lsof` 的最新版本可以通过匿名 ftp 从主机 `lsof.itap.purdue.edu` 获取。

你也可以使用此 URL：

```
ftp://lsof.itap.purdue.edu/pub/unix/lsof
```

`lsof` 在其他地方镜像。当你访问 `lsof.itap.purdue.edu` 并切换到 `pub/unix/lsof` 时，你将获得一些站点列表。

## 参见

并非每个移植到 `lsof` 的 UNIX 系统中都存在以下帮助页。

`access(2)`, `awk(1)`, `crash(1)`, `fattach(3)`, `ff(1)`, `fstat(8)`, `fuser(1)`, `gethostname(2)`, `isprint(3)`, `kill(1)`, `localtime(3)`, `lstat(2)`, `modload(8)`, `mount(8)`, `netstat(1)`, `ofiles(8L)`, `perl(1)`, `ps(1)`, `readlink(2)`, `setlocale(3)`, `stat(2)`, `time(2)`, `uname(1)`。

# lspci

## 名称

`lspci` - 列出所有 PCI 设备

## 语法

```
lspci [options]
```

## 描述

`lspci` 是一个用于显示系统中 PCI 总线及其连接设备信息的工具。

默认情况下，它显示设备的简短列表。使用下面描述的选项请求更详细的输出或供其他程序解析的输出。

如果你要报告 PCI 设备驱动程序或 `lsof` 本身的错误，请包含“`lspci -vvx`”的输出，甚至是更好的“`lspci -vvvxx`”输出（但是，请注意下文可能的限制）。

输出的某些部分（特别是在高度详细的模式下）可能只有经验丰富的 PCI 黑客才能理解。有关字段的精确定义，请查阅 PCI 规范或 `header.h` 和 `/usr/include/linux/pci.h` 头文件。

在许多操作系统中，对 PCI 配置空间某些部分的访问被限制 root，因此普通用户可使用的 `lspci` 功能是有限的。然而，`lspci` 会尽力显示可用信息，并对所有其他信息标记为 `<access denied>` 文本。

## 选项

### 基础显示模式

- `-m` 以后兼容的机器可读格式导出 PCI 设备数据。详见下文。
- `-mm` 以机器可读的格式导出 PCI 设备数据，方便脚本解析。详见下文。
- `-t` 显示树状图，其中包含所有总线、桥接器、设备以及它们之间的连接。

### 显示选项

- `-v` 开启详细模式，显示所有设备的详细信息。
- `-vv` 开启极其详细模式，显示更多细节。此级别包含所有被认为有用的信息。
- `-vvv` 更加详尽的模式，显示我们能够解析的所有内容，即使它们看起来完全无趣（例如，未定义的内存区域）。
- `-k` 显示处理每个设备的内核驱动程序，以及能够处理该设备的内核模块。在普通输出模式下给出 `-v` 时默认会进行此调整。（目前仅在内核 2.6 或更高版本的 Linux 上有效。）
- `-x` 显示配置空间标准部分（前 64 字节，或 CardBus 桥接器为 128 字节）的十六进制转储。
- `-xxx` 显示整个 PCI 配置空间的十六进制转储。只有 root 用户可以使用此选项，因为你正在尝试读取配置空间的某些部分（这种行为可能并不违反 PCI 标准，但至少非常愚蠢）。然而，此类设备很少见，所以无需过度担心。
- `-xxxx` 显示 PCI-X 2.0 和 PCI Express 总线上可用的扩展（4096 字节）PCI 配置空间的十六进制转储。
- `-b` 以总线为中心的视图。显示 PCI 总线上卡所看到的全部 IRQ 和地址，而不是内核看到的地址。
- `-D` 始终显示 PCI 域（domain）编号。默认情况下，在只有域 0 的机器上，`lspci` 会隐藏这些数字。

### 控制 ID 转换为名称的选项

- `-n` 以数字显示 PCI 厂商和设备代码，而不是在 PCI ID 列表中查找。
- `-nn` 同时以数字和名称显示 PCI 厂商和设备代码。
- `-q` 如果在本地 `pci.ids` 文件中未找到设备，则使用 DNS 查询中央 PCI ID 数据库。如果 DNS 查询成功，结果将缓存在 `~/.pciids-cache` 中，并在后续运行中（如果没有给出 `-q` 参数）被识别。请在自动化脚本中谨慎使用此开关，以避免数据库服务器过载。
- `-qq` 与 `-q` 相同，但会重置本地缓存。
- `-Q` 查询中央数据库中本地已识别的条目。如果你怀疑显示的条目错误，请使用此选项。

### 设备选择选项

- `-s [[<domain>]:<bus>]:<slot>][<func>]`
- `-d [<vendor>]:<device>` 仅显示具有指定厂商和设备 ID 的设备。两个 ID 都以十六进制给出，并可以省略或给为 "* "，两者都表示“任意值”。

### 其他选项

- `-i <file>` 使用 `<file>` 作为 PCI ID 列表，代替 `/usr/share/hwdata/pci.ids`。
- `-p <file>` 使用 `<file>` 作为内核模块处理的 PCI ID 映射。默认情况下，`lspci` 使用 `/lib/modules/kernel_version/modules.pcimap`。仅适用于具有近期模块工具的 Linux 系统。
- `-M` 调用总线映射模式，该模式会对所有 PCI 设备进行彻底扫描，包括配置错误的桥接器后的设备等。此选项仅在直接硬件访问模式下产生有效结果，通常需要 root 权限。请注意，总线映射器只扫描 PCI 0。
- `-version` 显示 `lsp` 版本。此选项应独立使用。

### PCI 访问选项

PCI 工具程序使用 PCI 库与 PCI 设备通信（详情请见 `pciib(7)`）。你可以使用以下选项来影响其行为：

- `-A <method>` 库支持多种访问 PCI 硬件的方法。默认情况下，它使用第一个可用方法，但你可以使用此选项覆盖该决策。使用 `-A help` 查看可用方法及其描述。
- `-O <param>=value` 库的行为由多个命名参数控制。此选项允许设置任何一个参数的值。使用 `-O help` 查看已知参数及其默认值。
- `-H1` 通过 Intel 配置机制 1 直接访问硬件。（这是 `-A conf1` 的简写）。
- `-H2` 通过 Intel 配置机制 2 直接访问硬件。（这是 `-A conf2` 的简写）。
- `-F <file>` 不再访问硬件，而是从文件读取配置。
- `-G` 增加库的调试级别。
- `-rev` 修订号。
- `-progif` 编程接口。

## 机器可读输出

### 简单格式 (-m)

在简单格式中，每个设备用一行描述。所有数字以十六进制打印。定义的标签有：

- Slot (`[domain:]bus:function`)
- Class
- Vendor
- Device

### 详细格式 (-v)

详细输出是由空行分隔的记录序列。每个记录包含一个 `tag: value` 对。`tag` 和 `value` 之间用制表符分隔。记录及其内部行没有固定顺序。标签大小敏感。

定义的标签有：

- Slot
- Class
- Vendor
- Device
- SVendor
- SDevice
- PhySlot
- Rev
- Progif
- Driver
- Module

### 后兼容详细格式 (-vm)

在此模式下，`lspci` 尝试与旧版本完全兼容。它与常规详细格式相似，但 Device 标签同时用于槽和设备名称，因此在记录中会出现两次。请在新代码中避免使用此格式。

### 详细格式 (-vmm)

详细输出是由空格分隔的记录序列。每个记录通过一系列行描述一个设备，每行包含一个 `tag: value` 对。`tag` 和 `value` 之间用单个制表符分隔。

## 文件

`/usr/share/hwdata/pci.ids`

所有已知 PCI ID 的列表（厂商、设备、类和子类）。维护在 http://pciids.sourceforge.net/，使用 `update-pciids` 工具下载最新版本。

`/usr/share/hwdata/pci.ids.gz`

`lspci` 编译时支持压缩，会在 `pci.ids` 之前尝试此文件。

`~/.pciids-cache`

在 DNS 查询模式下找到的所有 ID 缓存在此文件中。

## 缺陷

有时，`lspci` 无法完全解码配置寄存器。这通常是因为作者没有获得足够的文档。在这种情况下，它至少会打印 `<?>` 标记，以指示可能还有更多内容。如果你了解细节，欢迎提交补丁。

# 另另

`setpci(8)`, `update-pciids(8)`, `pcilib(7)`

## 作者

PCI 工具集由 Martin Mares <mj@ucw.cz> 维护。

# lsscsi

## 名称

`lsscsi` - 列出 SCSI 设备（或主机）及其属性

## 概览

```
lsscsi [--classic] [--device] [--generic] [--help] [--hosts] [--kname] [--list] [--lunhex] [--long] [--protection] [--protmode] [--scsi_id] [--size] [--sysfsroot=PATH] [--transport] [--verbose] [--version] [--wwn] [H:C:T:L]
```

## 描述

使用 `sysfs`（Linux 内核 2.6 及更高版本）中的信息列出当前连接到系统的 SCSI 设备（主机）。可以使用选项来控制每个设备提供的信息数量和格式。

如果给出了 `H:C:T:L` 参数，它将作为过滤器，仅列出匹配的设备。冒号不一定存在，末尾缺失的参数 `-`、`*`、`?` 被解释为通配符。默认是 `*:*:*:*`，意味着匹配所有内容。使用 `*` 或 `?` 的过滤字符串应用单引号或双引号引起以防止 shell 扩展。`-` 用作通配符，此时命令行上不再有更多选项被解释。允许开头为 `[` 结尾为 `]`（例如，`[1:0:0]` 匹配 1:0:0 上的所有 LUN）。也可以用于过滤--主机，在这种情况下只有 H 有效，它可以是数字或以 'host<n>' 的形式，其中 <n> 是主机编号。

默认情况下，在此工具中，设备名称（例如 "dev/sda" 或 "dev/root_disk"）是通过记录从 `sysfs` 获取列出设备的主设备和小号获得的（例如 "/sys/block/sda/dev" 的内容），然后在 "dev" 目录中查找匹配项。这种“通过主设备和小号匹配”将允许被 `udev`（例如）赋予不同名称的设备由此工具正确报告。

在某些情况下，查看 Linux 默认生成的设备名称可能有用，因此提供了 `--kname` 选项。这可能有用的示例是内核错误日志，它们倾向于使用磁盘的默认内核名称报告磁盘错误消息。

## 选项

长选项的参数对于短选项也是强制性的。选项根据长选项的名称按字母顺序排列。

- `-c`, `--classic`

输出与通过‘cat /proc/scsi/scsi’获得的结果相似。

- `-d`, `--device`

在列出（可能的）SCSI 设备名称后，在括号中显示设备节点的主设备和小号（例如 “dev/sda/8:0”）。

- `-g`, `--generic`

输出 SCSI 设备文件名。请注意，如果 `sg` 驱动程序是一个模块，则可能需要加载，否则可能会出现 '-'。

- `-h`, `--help`

输出用法信息并退出。

- `-H`, `--hosts`

列出当前连接到系统的 SCSI 主机。如果给出此选项，则列出 SCSI 设备。

- `-k`, `--name`

使用默认算法为设备命名（例如，块主设备 8，小号 0 是“dev/sda”），而不是使用上述发现的“dev” 目录中的“通过主设备和小号匹配”。

- `-L`, `--list`

以 `<attribute_name>=<value>` 对的形式输出额外信息，每行一个，前面留有两个空格。此选项的效果与 ‘-ll’ 相同。

- `-l`, `--long`

输出每个 SCSI 设备（主机）的额外信息。可以多次使用，以输出短选项更频繁的内容（例如 ‘-ll’）。当使用三次时（即 ‘-llll’），按每行输出一个 SCSI 设备（主机）属性；前面留有两个空格；格式为“<attribute_name>=<value>”。

- `-x`, `--lunex`



当使用一次此选项时，元组中的 LUN（在每个设备的开头）将以“T10”格式显示，该格式最高可达十六进制。它的前缀是“0x”。此外，分级 LUN 用一个字符分隔级别显示。例如，两个 LUN: 0x35500660000000 将显示为 0x355-0066。如果给出此选项（例如使用‘0x355-0066’），则为每个 LUN 显示完整的 16 位数字。

- `-p`, `--protection`

输出目标 (DIF) 和初始化器 (DIX) 保护。

- `-P`, `--protmode`

输出每个设备的有效保护信息。

- `-i`, `--scsi_id`

输出在 `/dev/by-id/` 中找到的 udev 匹配。这仅适用于磁盘类设备。如果没有匹配，则输出 `/sys/class/block/`。

- `-s`, `--size`

以人类可读格式打印磁盘容量。

- `-t`, `--transport`

输出传输信息。如果给出此选项，则列出 SCSI 设备。当使用 `--list` 时，输出目标信息或主机信息。对于设备，通常是传输类型，前面留有两个空格。输出 `attribute_name=value` 对。

- `-v`, `--verbose`

输出详细信息。

- `-V`, `--version`

输出版本信息。

- `-w`, `--wwn`

输出磁盘的全球名称 (WWN)，通常为 64 位，但也可以是 128 位。为了指示 WWN，前缀为“0x”。

- `-y`, `--sysfsroot=PATH`

假设 sysfs 挂载在 PATH。如果给出此选项，PATH 应该是绝对路径。

# 传输方式

此工具列出作为逻辑单元 (LU) 的 SCSI 设备，位于 SAM-4 架构（https://www.t10.org）。当给出 `--hosts` 选项时，它是初始化器。SAM-4。通过传输到达目标，并延伸到逻辑单元。目标设备可能包含多个端口。如果 FC 或 SAS 磁盘是可见的，lsscsi 将显示两个端口。初始化器（即主机）也具有多个端口，而 HBA 则每个初始化器有一个条目。对于设备，则每个初始化器有一个条目。

通常此工具为每个“设备”或主机提供一行输出。通过添加 `--list` 选项可以获得显著更多信息。在设备上提供的传输信息是 SAM-4 架构。当配合 `--transport` 选项时，在摘要行之后以 `attribute_name=value` 的格式输出传输信息，前面留有两个空格。当给出 `--list` 选项时，输出目标信息。如果存在设备列表，使用过滤参数可以减少输出量。

目前识别的传输方式包括：IEEE 1394, ATA, FC, iSCSI, SAS, SATA, SPI 和 USB。

对于 IEEE 1394（也称为 Firewire，当涉及存储时为 SBP），在给出 `--transport` 且没有 `--hosts` 选项的情况下，输出基于 EUI64 的目标端口。给出 `--hosts` 选项时，输出 EUI64 初始化器端口。特定 IEEE 1394 传输的摘要行前缀为“sbp”。

为了检测 ATA 和 SATA，在耗尽其他传输检查后对名称进行粗略检查。根据驱动名称选择 ATA 或 SATA 传输类型。摘要行的输出为“ata”或“sata”。没有给出其他属性。标记为“ata”的设备和主机将使用并行 ATA (PATA)。对于光纤 (FC)，在给出传输时输出端口名称和端口标识符。在没有 `--hosts` 选项的情况下，这些 ID 是与列出的设备（逻辑单元）关联的目标端口。给出 `--hosts` 选项时，这些 ID 是主机使用的初始化器端口。特定 FC 传输的摘要行前缀为“fc”：如果检测到 FCoE（通过以太网），则前缀改为“fcoe”。

对于 iSCSI，在给出 `--transport` 且没有 `--hosts` 选项的情况下，输出目标端口。这由 iSCSI 名称和目标端口组组成。

由于 iSCSI 名称以 "iqn" 开头，因此不使用前缀。当给出 `--*hosts*` 选项时，摘要行将输出 "iscsi:"。

对于串行连接 SCSI（SAS），它将输出目标端口的 SAS 地址（如果也给了 `--*hosts*` 选项，则输出初始化器端口）。这将是一个 naa-5 地址。对于 HBA 和 SAS 目标设备（如 SAS 磁盘和磁带驱动器），SAS 地址是唯一的。对于连接到 SAS 扩展器的 SATA 磁盘，扩展器通过在其自身的 SAS 地址上加上一个非零值（即扩展器的 SAS 地址）来提供 SAS 地址（例如 `expander_sas_address+ phys_id+1`）。直接连接到 SAS HBA 的 SATA 磁盘似乎具有不确定的 SAS 地址。摘要行中特定于 SAS 传输的输出前缀为“sas:”

对于 SCSI 并行接口（SPI），在给出 `--*transport*` 且没有 `--*hosts*` 选项的情况下，将输出目标端口标识符（通常为 0 到 15 之间的数字）。当给出 `--*hosts*` 选项时，摘要行中仅输出 “spi:”。

当检测到 USB 传输时，摘要行将包含 “usb:” 后跟一个 USB 设备名称。USB 设备名称的格式为 “<b>-<p1>.<p2>.<p3>:<>,<>,,<i>”，其中 <b> 是 USB 总线号，<p1> 是端口，<p2> 是存储设备，<p3> 指配置号，而 <i> 是接口号。每个 USB 目标都有一个独立的 SCSI 主机。一个 USB SCSI 目标可能包含多个逻辑单元。因此，USB SCSI 主机和属于该 USB 主机的所有逻辑单元将显示相同的“device_name”字符串。

## LUN

出于历史原因以及多个 Unix 系统的习惯，Linux 使用一个整数元组来描述 SCSI 设备（也称为逻辑单元 LU）。该元组的最后一个元素是所谓的逻辑单元数（LUN）。最初 SCSI LUN 最初是 3 位的整数，后变为 8 位。如今的 SCSI LUN（SAM-5 第 4.7 节）是 64 位，但 SCSI 标准现在将 LUN 视为 8 字节的整数。

在 2013 年之前，Linux 通过取 SCSI LUN 的前 4 个字节并忽略后 4 个字节将 SCSI LUN 映射为 32 位整数。Linux 将 SCSI LUN 的两个字节视为一个单元（字），并使其成为 LUN 整数中的低 16 位。SCSI LUN 的后两个字节成为 LUN 整数中的高 16 位。这样做的理由通常是为了常用的较小 LUN 整数。在 SCSI LUN（十六进制）表示法中，常见的 LUN 是 00 00 00 00 00 00 00 00，这变为 Linux LUN 0。下一个常见的 LUN 是 00 01 00 00 00 00，这变为 Linux LUN 1。

2013 年，有人提议通过扩展上述映射将 Linux LUN 增加到 64 位整数。在这种情况下，SCSI LUN 中可以表示的所有信息都将映射到一个 LUN（64 位）整数中。且该映射是可以反向的，不会丢失信息。

此版本的实用程序支持 32 位和 64 位 LUN 整数。默认情况下，每行开头元组结尾显示的 LUN 是十进制整数格式的 LUN。当给出 `--lunhex` 选项时，LUN 以 SCSI LUN 格式显示，8 个字节连接在一起，以十六进制输出并带有前缀 ‘0x’。LUN 根据 SAM-5 的描述进行解码，且不显示末尾的零（即右侧数字）。LUN 0（即 00 00 00 00 00 00 00 00）显示为 0x0，LUN 65（即 41 00 00 00 00 00 00 00）显示为 0x041。如果给出两次 `--lunhex` 选项，则显示完整的 64 位（即十六进制数字）。

如果命令行上没有给出 `--lunhex` 选项，则会检查环境变量 `SCSI_LUNHEX_OPT`。如果存在 `SCSI_LUNHEX_OPT`，则其关联值将成为内部设置 `--lunhex` 的次数。例如，`SCSI_LUNHEX_OPT=2 lscsi` 和 ‘`lscsi -xx`’ 是等效的。

## EXAMPLES

关于此实用程序的信息（示例也可以此处找到：http://sg.danny.cz/scsi/lscsi.html

## NOTES

此命令的信息源自 sysfs 文件系统，除非用户另有指定，否则假设其挂载在 `/sys`。被 SCSI 中层检测到的 SCSI（伪）设备，即使所需的上层驱动程序（即 sd, sr, st, sg 或 ch）未加载，也会列出。如果未加载相应的上层驱动，设备文件名将显示为 而不是类似 `/dev/sto0`。请注意，某些设备（例如扫描仪和介质库器）没有主上层驱动，只能通过 SCSI 通用 (sg) 设备名称访问。

还可以通过 Linux 中的 bsg 驱动访问通用 SCSI 设备。默认情况下，bsg 驱动的设备节点名称格式为 `/dev/bsg/H:C:T:L`。因此，此实用程序在以 ‘6:0:1:2’ 开头的行中显示的 SCSI 设备，可以通过 `/dev/bsg/6:0:1:2’ 设备节点名通过 bsg 驱动进行访问。

在 Linux 内核 2.6.26（及可能的后续版本）未定义 CONFIG_SYSFS_DEPRECATED_V2 内核选项的情况下，需要 iscsi 版本 0.21 或更高版本才能正确显示 SCSI 设备。

## AUTHOR

Doug Gilbert 编写

## REPORTING BUGS

向 <dgilbert at interlog dot com> 报告 bug。

## COPYRIGHT

Copyright © 2003-2013 Gilbert 本软件根据 GPL 分发；即使对于特定适用性也不提供任何保证。

## SEE ALSO

lspci, lsusb

## lsusb

- NAME

lsusb - 列出 USB 设备

## LVCHANGE

- NAME

lvchange – 修改逻辑卷属性

- DESCRIPTION

lsusb 是一个用于显示 USB 总线和连接设备信息的实用程序。

- OPTIONS

- `-v`, `--verbose`

告诉 usb 输出详细信息并显示信息。

- `-s [[bus]:devnum]`

仅显示指定总线和设备号的设备。

- `-d [vendor]:[product]`

仅显示指定厂商和产品的设备。

- `-t`

以树形形式导出 USB 层次结构。

- `-V`, `--version`

在标准输出打印版本信息并退出。

- RETURN VALUE

如果未找到设备，则返回非零退出码。

- FILES

```
/usr/share/hwdata/usb.ids
```

已知 USB ID 列表（厂商、产品、类、子类）。

- SEE ALSO

lspci(8), usbview(8).

- AUTHOR

Thomas Sailer, <sailer@ife.ee.ethz.ch>.

# 说明

lvchange 允许你更改逻辑卷的属性，包括使其被内核感知并准备就。

## 选项

常用选项请参阅 lvm [aeisls]{1n}。

- `-a,--activate` 控制逻辑卷的可用性。通过 libdevmapper 与内核设备映射器驱动通信，以激活 (-ay) 或取消激活 (-an) 逻辑卷。

激活逻辑卷会创建一个指向设备节点的符号链接 `/dev/VolumeGroupName/LogicalVolumeName`。所有软件和脚本都应该通过此符号链接访问设备，并将其呈现为设备名称。底层设备节点的位置和名称可能取决于发行版和配置（例如 udev），并可能随版本的发布而变化。

如果使用了自动激活 (-aay)，则只有当逻辑卷匹配 `lvm.conf` 中的 `activation/auto_activation_volume_list` 列表时才会被激活。如果未设置列表，则所有卷都将进入激活考虑。在系统启动期间应使用 `-ay` 选项，可以通过 `activation/auto_activation_volume_list` 设置来选择要激活哪些卷。

在集群卷组（VG）中，使用 `clvmd` 进行激活，可能的选项有：

- `-aey`，clvmd 在独占模式（带有独占锁）下激活逻辑卷（LV），允许单个节点激活该 LV。

- `-sy`，clvmd 在共享模式（带有共享锁）下激活 LV，允许多个节点并发激活该 LV。如果 LV 类型禁止共享访问（例如带有快照的 LV），则忽略 's' 选项并使用独占锁。

- `-ay`（未指定模式），如果 LV 类型允许并发访问（例如线性逻辑卷 LV），`clvmd` 将以共享模式激活 LV。否则，`clvmd` 将以独占模式激活 LV。

- `-aey`, `-asy`, 和 `-ay`，clvmd 尝试在所有节点上激活 LV。如果使用独占模式，则只有其中一个节点会执行成功。

- `-an`，clvmd 尝试在所有节点上取消激活 LV。

- `-aly`，clvmd 仅在本地节点激活 LV，而 `-aln` 仅在本地节点取消激活。如果 LV 类型允许并发访问，则使用共享模式，否则使用独占模式。

带有快照的 LV 始终以独占方式激活，因为它们同时只能在一个节点上。

对于本地卷组（VG），-aey, -asy, 和 -asy 都是等效的。

- `-activationmode {complete|degraded|partial}` 激活模式决定了在物理卷（PV）缺失（例如由于设备故障）时是否允许激活逻辑卷。`complete` 是最严格的；仅激活未受缺失 PV 影响的逻辑卷。`degraded` 允许在 PV 缺失的情况下激活 RAID 逻辑卷。（注意，“镜像分段类型”不被视为逻辑卷。应使用 raid1 分段类型。）最后，`partial` 允许在 PV 缺失或失败导致分区缺失的情况下激活任何逻辑卷。此选项应仅在执行恢复或修复操作时使用。默认模式为。要更改它，请参阅 `llvm.conf(5)` 中的 `activation_mode`。

- `-K`, `--ignoreactivations` 忽略在激活期间跳过逻辑卷的标记。

- `-cachepolicy`, `--cachesettings key=value` 仅适用于缓存的 LV；另请参阅 `llvmcache(7)`。设置缓存策略及其可调设置。在大多数用例中，默认值已经足够。

- `-C`, `--contiguous {y|n}` 尝试设置或重置逻辑卷的连续分配策略。只有当所有分配的物理范围区（extents）都是相邻的时，才可以将非连续逻辑卷的分配策略更改为连续。

- `-detachprofile` 卸载任何附加到逻辑卷的元数据配置方案。有关元数据配置更多信息请参阅 `llvm.conf(5)`。

- `-discards {ignore|nopass|passdown}` 设置此项以忽略精简池（thin pool）卷接收到的任何丢弃。设置为在精简池内部处理此类丢弃，并允许长时间需要的区域被新数据覆盖。设置为 passdown（默认值）则在精简池内部处理并将其传递给底层设备。

- `-errorwhenfull {y|n}` 设置数据空间耗尽时精简池的行为。信息请参阅 `lvcreate(8)`。

- `-resync` 强制镜像进行完全重同步。在正常情况下，你不需要此选项，因为同步会自动发生。数据从主镜像设备读取并复制到其他镜像中，因此这可能花费大量时间——在此期间，你将没有数据的完整冗副本。

- `-metadataProfileName` 使用并将 ProfileName 配置方案附加到逻辑卷元数据中。每当下次处理该逻辑卷时，该方案将自动应用。如果卷组附加了另一个方案，则优先使用逻辑卷方案。有关元数据方案的更多信息请参阅 `llvm.conf(5)`。

- `--minor minor` 设置次号。

- `--major major` 设置主号。此选项仅在旧系统（内核 2.4）上支持，在动态分配主号的现代 Linux 系统上会被忽略。

- `--monitor {y|n}` 如果安装了 dmevent，则启动或停止对镜像或快照逻辑卷的监控。

- `--poll {y|n}` 如果被监控的卷所使用的设备报告错误，则对其进行处理。

- `--writmost {y|n}` 将设备标记为只写。使用 `auto_activation_volume_list` 设置。

- `--raidmaxrecoveryrate {y|n}` 设置卷的最大恢复率。

- `--raidminrecoveryrate {y|n}` 设置卷的最小恢复率。

- `--raidrecoveryrate {y|n}` 设置卷的恢复率。

- `--raidwritebehind {y|n}` 指定允许的最大待处理写入数。

- `--raidwriteount {y|n}` 设置允许的最大待处理写入数。

- `--udev` 禁用 udev 同步。

- `--ignoremonitoring` 除非指定 `--monitor`，否则不尝试与 dmevent 交互。

- `--persistent {y|n}` 设置 y 使指定的次号持久化。

- `--permission {r|w}` 更改访问权限为只读或读写。

- `--readahead {ReadAheadSector|auto}` 设置此逻辑卷的预读扇。

- `--raidsync {check|repair}` 此参数用于启动同步操作。

- `--zero {y|n}` 设置精简池的置零模式。注意：当将 zero 设置为 y 时，从池中从非零模式分配的块在重写部分不会被清除。

# 环境变量

LVM_SUPPRESS_LOCKING_FAILURE_MESSAGES

抑制锁定失败信息的输出。

## 示例

将卷组 vg00 中卷 lvol1 的权限更改为只读：

```
lvchange -pr vg00/lvol1
```

# 另见参见

lvm(8), lvmcache(7), lvmthin(7), lvcreate(8), vgchange(8)

# LVCONVERT

+ > 名称

lvconvert – 将逻辑卷从线性转换为镜像或快照

# 语法

lvconvert -m|mirrors Mirrors [--type SegmentType] [--mirrorlog

{disk<mirrored}] [--corelog] [-R]-resize MirrorLogRegionSize] [---

stripes Stripes [-I--stripize Stripe] [-A--alloc AllocationPolicy] [-b-



# lvconvert 用法

```
background] [-f--force] [-i--interval Seconds] [--commandProfile ProfileName
[-h-?]--noudevsync] [-v--verbose] [-y--yes] [--version]
```

`LogicalVolume[Path] [PhysicalVolume[Path]:PE-[PE]]...`

```
lvconvert --split [--commandProfile ProfileName] [-h-?]--help] [--noudevsync
[-v--verbose] SplittableLogicalVolume[NamePath]
```

```
lvconvert --splitcache --uncache [--commandProfile ProfileName] [-h-?]--help]
--noudevsync [-v--verbose] [--version] CacheLogicalVolume[NamePath]
```

```
lvconvert --splitmirrors Images [--nameSplitLogicalVolumeName] [---
trackchanges MirrorLogicalVolume[Path] [--commandProfile ProfileName]
SplittablePhysicalVolume[Path]:PE-[PE]]...
```

```
lvconvert --snapshot [--commandProfile ProfileName] [-h-?]--help] [---
noudevsync] [-v--verbose] [--version] SnapshotLogicalVolume[Path]
```

```
lvconvert --s--snapshot [-cchunkize Size[BBskmG]] [-Z--zero {yn}] [---
commandProfile ProfileName] [-h-?]--help] [--noudevsync] [-v--verbose] [---
version] OriginalLogicalVolume[Path] SnapshotLogicalVolume[Path]
```

```
lvconvert --merge [-b--background] [-i--interval Seconds] [--commandprofile
ProfileName] [-h-?]--help] [-v--verbose] [--version] LogicalVolume[Path]...
```

```
lvconvert --repair [-s--stripes Stripes [-I--stripize StripeSize] [---
commandProfile ProfileName] [-h-?]--help] [-v--verbose] [--version]
LogicalVolume[Path] [PhysicalVolume[Path]...
```

```
lvconvert --type thin[--pool] [-T--thin] [--originate
ExternalOriginLogicalVolume[Name] [--thinpool ThinLogicalVolume[Name|Path]
[-c--chunkize Size[BBskmG]] [--discards
ignorepassdonpassdown] [--poolmetadata
ThinPoolMetadataLogicalVolume[Name|Path] [--poolmetadata
ThinPoolMetadataSize[BBskmG]] [-r--readhead
[ReadAddSectors(auto|one)] [-s--stripes Stripes [-I--stripize StripeSize]] [---
polmetadataspace[yn}] [-Z--zero {yn}] [--commandProfile ProfileName] [--
h--?] [-v--verbose] [--version]
[[ExternalOriginThinLogicalVolume[Name|Path] [PhysicalVolume[Path]:PE
PE]]...
```

```
lvconvert --type cache[--pool] [--cachepool
CachePoolLogicalVolume[Name|Path] [-c--chunkize Size[BBskmGmg]]
[—cachemode {writeback|writethrough}] [—cachepolicy policy] [—cachesettings key=value] [—poolmetadata CachePoolMetadataLogicalVolume{Name|Path} |—poolmetadatasize CachePoolMetadataSize[bBsSkKmMgG]] [—polmetadataspare {y|n}] [—commandprofile ProfileName [-h|-?|--help] [-v|--verbose] [--version] LogicalVolume[Path} [PhysicalVolume[Path]]...
```

## 描述

`lvconvert` 用于更改分段类型（例如线性、镜像、快照）或逻辑卷的特征。它可以添加或移除镜像的冗余镜像，更改逻辑卷的日志类型，将逻辑卷指定为快照。如果指定了物理卷，它会释放这些特定 `PE` 范围的物理段，这些物理段将从镜像中分离。`--split` 分离 `SplittableLogicalVolume`。`--splitcache` 从缓存池中分离 `CacheLogicalVolume`。`--splitmirrors` 指定要分离的冗余镜像数量。

## 选项

参见 `lvm(8)` 获取常用选项。`--cache,--corelog,--merge,--mirror,--mirrors,--repair,--snapshot,--split,--splitcache,--splitnap,--type` 或 `--uncache`。

`-b--background` 在后台运行。

`-c--chunkize Size[BBskmG]` 为快照、缓存池和逻辑卷指定块的大小。

`-cachemode {writeback|writethrough}` 设置缓存模式。

`-cachepolicy policy` 设置缓存策略。

`-cachesettings key=value` 设置缓存设置。

`--corelog` 等同于 `mirrorlog`。

`-commandprofile ProfileName` 设置命令配置。

`--discards ignorepassdonpassdown`（未详，但列为选项）。

`--cache` 是。

`--cachepool CachePoolLogicalVolume[Name|Path]` 指定缓存池。

`--poolmetadata CachePoolMetadataLogicalVolume[Name|Path] |—poolmetadatasize CachePoolMetadataSize[bBsSkKmMgG]` 设置池元数据。

`--polmetadataspare {y|n}` 设置池元数据备用。

`--noudevsync` 禁用设备同步。

`--interval Seconds` 每隔一段时间以百分比报告进度。

`--mirrors Mirrors` 镜像的冗余镜像数量。

`--merge` 将镜像卷合并回线性卷。

`-h--?` 或 `-h|-?|--help` 显示帮助。

`-i--interval Seconds`（重复列表）。

`-n--name` 应用于从镜像分离出的逻辑卷的名称。

`-R--resize MirrorLogRegionSize` 镜像被分为此大小的区域（MB）。

`-repair` 修复卷（未详）。

`-type SegmentType` 指定类型（例如线性、镜像、快照、精简）。

`-v--verbose` 启用更详细的输出。

`--version` 显示版本。

`--split` 分离 `SplittableLogicalVolume`。

`--splitcache` 从缓存池中分离 `CacheLogicalVolume`。

`--splitmirrors` 指定要分离的冗余镜像数量。

`--snapshot` 从组成逻辑卷重建快照。

`--trackchanges` 跟踪 `raid1` 设备的变化以允许合并。

`--uncache` 取消缓存并移除缓存池。

`--zero {yn}` 设置置零选项。

默认单位为千字节（KB）。

对于快照，该值必须是 `4KiB` 到 `512KiB` 之间 2 的幂次方，默认值为 `4`。

对于缓存池（cache pools），该值必须在 `32KiB` 到 `1GiB` 之间，默认值为 `64`。

对于精简池（thin pools），该值必须在 `64KiB` 到 `1GiB` 之间，默认值从 `64` 开始，并向上扩展以适应池元数据大小 `128MiB`（在未指定池元数据大小时如此）。该值必须是 `64KiB` 的倍数。（在 thin target 版本 `1.4` 之前的早期内核要求该值为 2 的幂次方。除非 thin target 版本为 `1.5`，否则不支持非 2 幂值的丢弃（Discards）。）

- `-discards {ignore|nopassdownpassdown}`

指定精简层在传递给物理卷（Physical Volume）时是否处理丢弃操作。目前选项仅支持精简池。默认为透传（passdown）。

- `-Z, --zero {y|n}`

控制快照中前 `4KiB` 数据的置零。如果卷是只读的，快照将不会置零。对于精简池卷，它控制已分配块的置零。注意：分配大型置零块会负面影响性能。

- `-merge`

将快照合并到其源卷，或将从镜像中分出的带有跟踪更改（trackchanges）的 `raid1` 镜像合并回镜像。

要检查您的内核是否支持快照合并功能，请在 `dmset targets` 的输出中查找 `'snapshot-merge'`。如果源卷和快照卷未打开，合并将立即启动。否则，将在源卷或快照卷首次激活且两者都处于激活状态时启动。将快照合并到源卷（例如根文件系统）无法关闭，直到源卷下次激活。当合并开始时，生成的逻辑卷将具有源卷名称、次设备号和 UUID。在合并期间，对源卷的读写操作似乎是定向到正在合并的快照。当合并完成后，合并的快照将被移除。可以在命令行上指定多个快照，或使用 `@tag` 来指定多个要合并到各自源卷的快照。

- `-originExternalOriginVolumeName`

原始逻辑卷的新名称，它将使用 `--thinpool`。如果没有此选项，将生成默认名称 `"lv<n>"`，其中 `<n>` 是 LVM 内部逻辑卷编号。只要该卷被用作外部源，它将是只读的且无法进一步修改。

- `-poolmetadata PoolMetadataLogicalVolume{Name|Path}`

指定缓存池或精简池的元数据逻辑卷。大小应在 `2MiB` 到 `16GiB` 之间。缓存池通过选项 `--cachepool` 指定。精简池通过选项 `--thinpool` 指定。当指定的指定的池已存在时，该池的元数据卷将与给定的 LV 交换交换。在这种情况下，池属性（如块大小或置零）默认会被保留。这对于池元数据的修复或其离线扩容非常有用，因为元数据卷可以作为普通卷供使用 `cache_dump(8)`、`cache_repair(8)`、`cache_restore(8)`、`thin_dump(8)`、`thin_repair(8)` 和 `thin_restore(8)` 等配置工具的用户使用。

- `--poolmetadatase PoolMetadataSize|BsSkKmMgG`

如果池元数据卷未定义，则设置缓存或精简池元数据卷的大小。通过选项 `--cachepool` 或 `--thinpool` 指定池。精简池支持的值范围在 `2MiB` 到 `16GiB` 之间。默认值通过此公式估计（Pool_LV_size / Pool_LV_chunk_size * 64b），单位为兆字节。

- `--poolmetadataspare [yn]`

控制池元数据备用卷的创建和维护，卷组内将维护一个大小等于最大池元数据卷的备用卷。默认是 yes。

- `-r, --reahead [ReadAheadSectors](autone)`

设置池元数据卷的预读扇数。默认值为“auto”，允许内核自动选择合适的值。*None* 等同于指定零。

- `--repair`

在发生磁盘故障后修复镜像或修复精简池元数据。

默认情况下，如果可能将恢复原始镜像数量。在命令行上指定 `-y` 以跳过提示。如果不替换任何替换项则使用 `-U`。此外，您可以使用 `--use-policies` 使用 `lvm.conf(5)` 中指定的设备替换策略，即 `activation/mirror_log_fault_policy` 或 `activation/mirror_device_fault_policy`。

精简池更新了 `thin_repair(8)` 工具的使用。只有非激活的精简池可以修复。内核和 Lvm2 之间没有元数据校验。这需要进一步的手动操作。修复后，未修改的旧元数据仍然存在于“`<pool>_meta<n>`”中。

- `--replaceVolume`

移除指定的设备（物理卷），并用卷组可用或特定列表中设备替换。此选项适用于 RAID 类型（例如 `raid1, raid5` 等）。

- `--stripes`

给出条带数。这等于分散逻辑卷的物理卷数量。这不适用于已分配的空间，只有新分配的空间可以条带化。

- `-I, --stripesize`

给出条带粒度的千字节数。`StripeSize` 必须是 `2^n`。

- `--type thin`

将逻辑卷转换为精简池。原始卷重命名为源。

- `--thinpool ThinLogicalVolume{Name|Path}`

指定要使用的精简池。卷转换为该池。

- `--uncache`

取消卷的缓存。

在卷变为未缓存状态之前，缓存会被刷新。

## 示例

将线性卷“`vg00/lvol1`”转换为双路镜像：

```
lvconvert -m1 vg00/lvol1
```

将线性卷“`vg00/lvol1`”转换为精简卷：

```
lvconvert --type thin -m1 vg00/lvol1
```

将磁盘日志的镜像转换为内存日志镜像：

```
lvconvert --mirrorlog core vg00/lvol1
```

将内存日志的镜像转换为磁盘日志镜像：

```
lvconvert --mirrorlog disk vg00/lvol1
```

将镜像转换为线性卷：

```
lvconvert -m0 vg00/lvol1
```

将镜像转换为具有相同数量的 `raid1` 逻辑卷：

```
lvconvert --type raid1 vg00/lvol1
```

将逻辑卷“`vg00/lvol2`”转换为源卷“`vg00/lvol1`”的快照：

```
lvconvert -s vg00/lvol1 vg00/lvol2
```

将线性卷“`vg00/lvol1`”转换为双路镜像，分配新扇区时使用 `/dev/sda:0-15` 和 `/dev/sdb:0-15`：

```
lvconvert -m1 vg00/lvol1 /dev/sda:0-15 /dev/sdb:0-15
```

将镜像卷“`vg00/lvmirror1`”转换为线性，释放来自 `/dev/sda` 的扇区：

```
lvconvert -m0 vg00/lvmirror1 /dev/sda
```

将“`vg00/lvol1_snap`”合并到其源：

```
lvconvert --merge vg00/lvol1_snap
```

如果“`vg00/lvol1`”、“`vg00/lvol2`”和“`vg00/lvol3`”都标记了“some_tag”，则每个快照卷将顺序合并，例如：“`vg00/lvol1`”，然后是“`vg00/lvol2`”，最后是“`vg00/lvol3`”。如果使用 `--background` 并启动所有快照逻辑卷：

```
lvconvert --merge @some_tag
```

从镜像中提取出一个镜像，使其成为名为“`lv_split`”的新逻辑卷。镜像数量将相应减少。

```
lvconvert --splitmirrors 1 --name lv_split vg00/lvmirror1
```

使用 `--type raid1` 创建的镜像逻辑卷在拆分镜像时可以使用 `--trackchanges` 参数。从镜像逻辑卷 `lv_raid1` 中分离出一个镜像作为单独的只读设备，并跟踪该镜像在分离状态下对镜像所所的更改。拆分出的设备名称格式为 `lv_raid1_image_N`，其中 `N` 是数字，且无法重命名。

```
lvconvert --splitmirrors 1 --trackchanges vg00/lv_raid1
```

将之前从镜像中临时分离并带有 `--trackchanges` 参数的镜像合并回原始镜像，并将其内容更新为最新。

```
lvconvert --merge vg00/lv_raid1_image_1
```

将 RAID1 逻辑卷 "`my_raid1`" 中的物理卷 "`/dev/sdb1`" 替换为指定的物理卷 "`/dev/sdf1`"。如果未提供参数 "`/dev/sdf1`"，`lvconvert` 将尝试从卷组的可用设备中寻找合适的设备。

```
lvconvert --replace/dev vg00/my_raid1 /dev/sdf1
```

将逻辑卷 "`vg00/lvpool`" 转换为块大小为 `128KiB` 的精池，并将 "`vg00/lv1`" 转换为使用该池的精卷。原始的 "`vg00/lv1`" 用作外部只读源，所有对该卷的写入将存储在 "`vg00/lvpool`" 中。

```
lvconvert --type --thin vg00/lvpool -c 128 lv1
```

将逻辑卷 "`vg00/origin`" 转换为来自精池 "`vg00/lvpool`" 的精卷。该卷将使用 "`vg00/origin`" 作为该卷未分配区域的外部卷。只读源使用新名称 "`vg00/external`"。

```
lvconvert --T --thin vg00/lvpool --originname external vg00/origin
```

使用给定的缓存元数据将现有逻辑卷转换为缓存池 LV。



## `lvconvert --type cache-pool --poolmetadata vg00/lvx_meta vg00/lvx_data lvarename vg00/lvx_data vg00/lvx_cachepool`

使用给定的缓存池块大小 `128KiB` 将现有逻辑卷转换为缓存 LV。

## `lvconvert --cache --cachepool vg00/lvx_cachepool -c 128 vg00/lvx`

从现有的缓存卷 "`vg00/lvol1`" 中分离缓存池并留空缓存池。

## `lvconvert --splitcache vg00/lvol1`

从现有的缓存逻辑卷 "`vg00/lvol1`" 中删除缓存池。

## 参见

`lvm(8)`, `lvmconf(5)`, `lvmcache(7)`, `lvthin(7)`, `lvdisplay(8)`, `lvxtend(8)`, `lvreduce(8)`, `lvremove(8)`, `lvrename(8)`, `lvscan(8)`, `vgcreate(8)`, `cache_dump(8)`, `cache_repair(8)`, `cache_restore(8)`, `thin_dump(8)`, `thin_repair(8)`, `thin_restore(8)`

## LVCREATE

### 名称

`lvcreate` - 在现有的卷组中创建一个逻辑卷

### 概要

```
lvcreate [-a|activate {e|j}{yn}] [--addag Tag] [--alloc AllocationPolicy] [-A|--autobackup {yn}] [-H|-cache] [--cachemode {passthrough|writethrough}] [--cachepolicy] [--cachepoolCacheLogicalVolume{Name|Path}] [--cachecheets key=value] [-c-chunkSize Size[bBsSkKmMgG]] [--commandProfile Name] [-C|--continuous {yn}] [-d|debug] [--discards [ignore|nopassdownpassword]] [--errwhenfull {yn}] [-l|--extentsNumber%{FREEPVS|VG}] | -L|--size Size[bBsSkKmMgGtpPeE]] [-i|--stripes Size [-I|--stripize Size]] [-h|--help] [-k|--ignoreactivation] [-m|--minor {-j|major major}] [--metadataProfile Name] [-m|--mirrors {core}] [--nosync] [-R|--regionize MirrorLogSize[bBsSkKmMgG]] [--monitor {yn}] [-n|--name LogicalVolume{Name|Path}] [--noudevysnc] [-p|--permission {r|jw}] [-M|--persistent {yn}] [--poolmetadata MetadataSize[bBsSkKmMgG] --pooldatataresize {yn}] [--raid|minrecovery Rate] [-r|--ahead [ReadAheadSectors(auto)none]] [-k|--setationkip {yn}] [-s|--snapshot] [-V|--virtualize VirtualSize[bBsSkKmMgGtpPeE]] [-t|--test] [-thin|thinPoolLogicalVolume{Name|Path}] [--type SegmentType] [-v|--verbose] [-W|--wipesignatures {yn}] [-Z|--zero {yn}] [VolumeGroup{Name|Path} [/ExternalOrigin|Origin|Pool]LogicalVolume[PhysicalPath[:PE-PE]].....]

lvcreate [-l|--extentsNumber%{FREEORIGIN|VG}] | -L|--size Size[bBsSkKmMgGtpPeE]] [-c|--chunksize chunkSize[bBsSkKmMgG]] [--commandProfile Filename [--noudevysnc] [--ignoremonitoring] [--metadataProfile Name] [--monitor {yn}] [-n|--name SnapshotLogicalVolume{Name|Path}] [-s|--snapshot] [-H|--cache {{VolumeGroup{Name|Path}/OriginalLogicalVolume---virtualize VirtualSize[bBsSkKmGtpPeE]]
```

### 说明

`lvcreate` 通过从卷组的空闲物理区分配逻辑区（见 `vgcreate(8)`）创建一个新的逻辑卷。如果没有足够的空闲物理区，可以通过其他物理卷（见 `vgextend(8)`）或通过缩小现有逻辑卷的大小（见 `lvreduce(8)`）来扩展卷组。如果你指定了一个或多个物理卷，逻辑区的分配将限制在这些卷中。第二种形式支持用于备份目的的保留原始卷内容的快照。

### 选项

常用选项请参阅 `lvm(8)`。

- `-a`, `--activate` 控制命令完成后逻辑卷的可用性。默认情况下，逻辑卷会被激活 `-ay`。如果可能，`-an` 将让新逻辑卷处于未激活状态。但例如，源的快照只能在激活状态下创建，`-an` 不能用于 `--type snapshot`。通常需要提供 zero 参数，因为默认的零行为需要激活。如果使用了自动激活选项 `-ay`，只有在与 `lvmconf(5)` 中的激活列表项匹配时逻辑卷才会激活。对于激活的卷，`--zero n` 始终被认为且无法覆盖。`-ay` 将仅在一个节点上激活，`-ay` 将在本地节点激活。

- `-H`, `--cache` 创建缓存卷、逻辑卷或两者。指定 `--size` 参数将创建缓存卷。当指定卷组名称和一个非缓存池逻辑卷时，将其视为源卷并创建缓存池。在这种情况下，`--size` 用于指定缓存池。有关缓存的信息请参阅 `lvmcache(7)`。注意缓存段类型需要 dm-cache 模块 1.3 或更高版本。

- `-cachemode {passthrough|writeback|writethrough}` 指定何时认为缓存卷完成。如果指定 `writeback`，一旦存储在缓存池中即被视为完成。如果指定 `writethrough`，只有当存储在缓存 LV 和源 LV 中时才被视为完成。虽然 `writethrough` 对于写入可能较慢，但如果缓存池关联设备发生某些情况，它更具韧性。

- `-cachepolicy` 仅应用于缓存 LV；另参阅 `lvmcache(7)`。设置缓存策略。`mq` 是基本策略，较新的内核中提供了高级版本。

- `-cachepool CacheLogicalVolume[Name|Path]` 指定池卷的名称。指定池名称的另一种方法是附加到卷组参数后面。

- `-cachesettings key=value` 仅应用于缓存 LV；另参阅 `lvmcache(7)`。设置缓存可调设置。在大多数情况下，默认值是足够的。特殊值切换回其默认内核值并从 lvm2 元数据的设置列表中移除。

- `-c,--chunksize ChunkSize[bBsSkKmMgG]` 提供快照、缓存池和精池卷的区块大小。默认单位为 KB。对于快照，值必须在 `4KiB` 到 `512KiB` 之间，默认值为 `4KiB`。对于缓存池，该值必须是 `32KiB` 到 `1GiB` 之间 `32KiB` 的倍数。默认值为 `64KiB`。对于精池，该值必须是 `64KiB` 到 `1GiB` 之间 `64KiB` 的倍数。如果没有指定池元数据大小，默认值从 `64KiB` 开始增长到 `128Mi`。见 `lvm.conf(5)` 设置 `allocation/thin_chunk_size_policy` 选择不同的计算策略。精池目标版本 <1.4 不支持 2 的幂次方。对于目标版本 <1.5 不支持 2 的幂次方 discarded。

- `-C,--contiguous [y/n]` 设置或重置逻辑卷的连续分配策略。默认是基于下一个空闲原则的连续分配。

- `-corelog` 是选项 `--mirrorlog` 的快捷方式。

- `-discards [ignore|nopassdown|passdown]` 设置精池的删除行为。默认是 `passdown`。

- `-errorwhenfull [y/n]` 配置数据空间耗尽时精池的行为。默认是 `no`。设备将队列 I/O 操作直到目标超时（见 dm-thin-pool 模块 `no_space_timeout`）过期。此配置的系统有时间来扩展精池数据设备的大小。设置为 `yes`，I/O 操作立即报错。

- `-K,--ignoreactivationskip` 忽略激活期间跳过逻辑卷的标记。`--setactivationskip` 用于持久地设置或重置逻辑卷的激活标记。

- `-ignoremonitor` 除非指定了 `--logicalExtentNumber[%VG|PVS|FREE|ORIGIN]]` 否则不尝试扩展。

- `-L,--logicalExtentsNumber[%VG|PVS|FREE|ORIGIN]]` 给为新逻辑卷分配的逻辑区数量。分配的物理区总数将大于此，例如，如果卷是镜像的。该数字也可以表示为卷组总空间的百分比（带有后缀 `%VG`）、卷组剩余空闲空间的百分比（带有后缀 `%FREE`）、物理卷剩余空间的百分比（带有后缀 `%PVS`），或者（对于快照）作为源卷总空间的百分比（带有后缀 `%ORIGIN`，即为 `100%ORIGIN` 为整个源卷提供空间）。当以百分比表示时，该数字被视为分配物理区总数的上限（包括任何镜像使用的物理区，例如）。

- `-j,—major major` 设置主号。池卷不支持主号。此选项仅在旧系统（内核 2.4）上支持，在动态分配主号的现代 Linux 系统上会被忽略。

### metadatprofile ProfileName

将 `ProfileName` 配置配置文件附加到逻辑卷的元数据中。每当下次处理该逻辑卷时，该配置将自动应用。如果卷组附加了另一个配置，则优先使用逻辑卷的配置。有关元数据配置的更多信息，请参考 `llvm.conf(5)`。

- `-minor minor`

设置次设备号。池卷（pool volumes）不支持次设备号。

- `-m, --mirrors Mirrors`

创建一个具有 `Mirrors` 数量副本的镜像逻辑卷。例如，指定 `-m1` 将产生一个双侧镜像；即一个线性卷加上一个副本。

指定可选参数 `--nosync-sync` 将导致在创建镜像时跳过初始重同步。任何写入的数据都将进行镜像，但原始内容不会被复制。这对于跳过空设备可能潜在的耗时且耗资源的初始同步非常有用。

镜像有两种实现方式可以使用，分别对应于 `raid` 和 `mirror` 分段类型。默认是 `raid1`。如果你想使用旧的 "mirror" 分段类型，请参阅 `--type` 选项获取更多信息。参阅 `llvm.conf(5)` 中的 `global_mirror_segtype_default` 来配置镜像分段类型。`global/raid10_log_fault_policy_default` 以及 `--mirrorlog` 和 `--core` 适用于旧的 "mirror" 分段类型。

- `-mirror <disk|mirrored>`

为使用旧 "mirror" 分段类型的逻辑卷指定使用的日志类型。默认是 `disk`，它是持久的且需要少量的存储空间，并存储在与镜像数据不同的独立设备上。使用 `core` 意味着每次逻辑卷激活时（例如每次重启后），都会通过从第一个设备复制数据来重新生成镜像。使用 `mirrored` 将创建一个本身也是被镜像的持久性日志。

- `-monitor {y|n}`

启动或避免监控镜像、快照或精简逻辑卷 devent 设备（如果它已安装）。如果用于镜像监控的设备报告 I/O 错误，将根据 `llvm.conf(5)` 中设置的 `activation/mirror_image_fault_policy` 和 `activation/mirror_log_fault_policy` 处理故障。

- `-n, --name LogicalVolume{Name|Path}`

设置新逻辑卷的名称。如果没有此选项，将生成默认名称 `"Ivol0"` # 逻辑卷的 LVM 内部编号。

- `-nosync`

导致创建镜像时跳过初始重同步。

- `-nudevsync`

禁用 udev同步。进程不会等待 udev 的通知。无论后台是否有任何可能的 udev 处理，它都会继续。只有当 udev 未运行或其规则忽略 LVM2 创建的设备时，你才应该使用它。

- `-permission {r|rw}`

设置权限只读 `r` 或读写 `rw`。默认是读写。

- `-persistent {y|n}`

设置为 `y` 以使指定的次设备号持久化。池卷无法使主次设备号持久化。当指定主或次设备号时，默认是 `yes`。否则为 `no`。

- `-poolmetadatasize MetadataVolumeSize[bBskKmMgG]`

设置池元数据卷的大小。精简池支持的值范围在 `2MiB` 到 `16GiB` 之间，缓存池支持最高 `16GB`。最小值根据精简池的数据大小计算为 `(Pool_LV_size / Pool_LV_chunk_size * 64b)`。默认单位是兆字节。

- `-poolmetadatasize {y|n}`

控制池元数据稀疏逻辑卷的恢复和维护。在一个卷组内仅维护一个大于最大池元数据卷大小的卷。默认是 `yes`。

- `-raidmaxrecoveryrate Rate[bBskKmMgG]`

设置 RAID 逻辑卷的最大恢复速率。速率指定为数组中每个设备每秒的数量。如果没有给出后缀，则默认为 `KiB/sec`。将恢复速率设置为 `0` 意味着无限制。

- `-minrecoveryrate[bBskKmMgG]`

设置 RAID 逻辑卷的最小恢复速率。速率指定为数组中每个设备每秒的数量。如果没有给出后缀，则默认为 `KiB/sec`。将恢复速率设置为 `0` 意味着无限制。

- `-r,readahead {ReadAheadSectorsauto|}`

设置此逻辑卷的预读扇区数。对于使用 lvm 格式元数据的卷组，该值必须是 `2` 到 `120` 之间的一个值。默认值是 `auto`，它允许内核自动选择合适的值。`None` 等同于指定零。

- `-R,regsize MirrorLogRegionSize[bBskKmMgG]`

镜像被分为此大小（MiB）的区域，镜像日志使用粒度来跟踪哪些区域是同步的。

- `-k,setactivationskip {y|n}`

控制是否持久化地标记逻辑卷以跳过激活。默认情况下，快照卷被标记为跳过激活。

`Lvm.conf(5)` 中的 `activation/auto_self_activation_skip` 显示如何更改其默认行为。要激活此类卷，必须使用额外的 `-K|ignoreactivation` 选项。该标记在去激活期间不起作用。使用 `lvchange—setactivationskip {y|n}` 命令可以更改现有卷的跳过标记。查看标记是否已附加，可以使用 `lvs` 命令，该标记在 `lv_attr` 位中中报告。

- `-L,sizeLogicalVolumeSize[bBskKmGtPeE]`

为新逻辑卷分配大小。大小后缀 `B` 为字节、`S` 为扇区、`K` 为千字节、`M` 为兆字节、`G` 为吉字节、`T` 为太字节、`P` 为拍字节，`E` 可。默认单位是兆字节。

- `--snapshot LogicalVolume(NamePath)`

为源创建一个快照逻辑卷（或快照）。快照在源可以更新时提供内容的“冻结”镜像。15-20% 可能足够。如果快照空间不足，使用 `lxtend(8)` 扩展它。`reduce(8)` 也支持缩小快照。对快照使用 `lvs(8)` 可以检查分配了多少数据。监控快照的增长速率以避免空间耗尽。如果指定了 thinpool 将创建一个使用给定源作为外部源的精简卷。参考 `lvconvert(8)` 在线转换为精简卷。

- `-i,--stripes`

给出条带的数量。这等于散射逻辑卷的物理卷数量。创建 RAID 4/5/6 逻辑卷时，额外的设备将被完全考虑。`-i3` 将交叉逻辑卷使用 3 个设备，为 RAID 4/5 使用 4 个设备，为 RAID 6 使用 5 个设备。或者，如果省略 `-i` 参数，RAID 4/5/6 将使用卷组中的所有 PV 或指定的 PV。

- `-i,--stripeStripeSize`

给出带粒度的千字节数。对于 LVM 格式的元数据，条带大小必须是 `2^n`（n = 2 到 9）。对于 LVM 格式的元数据，条带大小可以是更大的 2 的幂，但不能超过物理区的大小。

- `-T,--thin`

创建精简池或精简逻辑卷或两者。指定可选参数 `size` 或 `—extents —virtualize` 将创建精简池逻辑卷。指定可选参数将从精简池卷创建精简逻辑卷。指定两个参数将创建精简池以及使用该池的精简卷。更多关于精简配置的信息请参考 `lvmthin(7)`。精简配置需要内核 3.2 或更高版本的设备映射驱动程序。

- `--thinPoolThinLogicalVolume(NamePath)`

指定池卷的名称。另一种指定池名称是将名称附加到卷组参数之后。



cache, cache-pool, error, linear, mirror, raid1, raid4, raid5_la, raid5_ls =(raid5), raid5_ra, raid5_rs, raid6_nc, raid6_zr =(raid6), raid10, snapshot, striped, thin-pool or zero。段类型有一个命令行别名，可以启用它。当未显式指定类型时，将从选项组合中选择隐含类型：`--h—cache --cachepool (cache or cachepool)`, `--T|—|thin (thin or pool)`, `--mirrors (raid1 or mirror)`, `--s—snapshot`

| 选项 | 说明 | 默认值 |
| :--- | :--- | :--- |
| `-V,--virtualize` | 虚拟化 VirtualSize | 默认类型为 linear（线性）。 |

`-V,--virtualize` 创建一个给定大小的配置设备或设备（默认为 MiB）。查看 `lvm.conf(5)` 设置中的 `global/sparse_getype_default` 以配置稀疏段类型。查看 `lvmint(7)` 了解更多关于精细置备（thinning provision）的信息。写入稀疏快照的任何内容在读取时都会被返回。设备的其他区域将返回零块。虚拟快照通过使用零目标创建请求大小的隐藏虚拟设备来实现。该设备使用 `_origin` 后缀。注意：对于较大的设备（GiB），使用稀疏快照效率不高，这种情况下应使用置备（provisioning）。

`-W,--wipesignatures {yn}` 控制在新创建的逻辑卷上检测到的签名进行擦除。如果未指定此选项，则默认每次执行置零（`-Z/zero`）时都会进行签名擦除。此默认行为可以通过 `lvm.conf(5)` 中的 `allocation/wipe_signatures_when_zeroing_new_lv` 设置来控制。如果 LVM2 编译时带有 blkid 擦除支持，则使用 `blkid(8)` 库来检测签名（使用 `blkid -k` 命令列出已识别的签名）。否则，使用原生的 LVM2 代码检测签名（MD RAID、swap 和 LUKS 签名仅在此情况下被检测到）。逻辑卷是（此处）。

`-Z,--zero {yn}` 控制新逻辑卷前 4KiB 的置零。默认是 yes。快照 COW 卷始终会被置零。如果只设置了标记，则逻辑卷不会置零。

警告：尝试挂载未置零的逻辑卷可能会导致系统挂起。

## 示例

在名为 `vg00` 的卷组创建一个具有 3 个条带、条带大小为 8KiB 且为 100MiB 的条带逻辑卷。逻辑卷名称将由 `lvcreate` 选择：

```
lvcreate -i 3 -I 8 -L 100M vg00
```

创建一个可用大小为 500 MiB 的双路镜像逻辑卷。此操作需要 3 个设备（或使用 `--alloc anywhere` 选项）——两个用于镜像设备，一个用于磁盘日志：

```
lvcreate -m1 -L 500M vg00
```

创建一个可用大小为 500 MiB 的双路镜像逻辑卷。此操作需要 2 个设备——日志存储在“内存”中：

```
lvcreate -m1 --mirrorlog -L 500M vg00
```

创建一个名为 "vg00/snap" 的快照逻辑卷，在快照逻辑卷创建时访问名为 "vg00/lv01" 的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录，以便访问文件系统内容进行备份，同时原始文件系统继续更新：

```
lvcreate --size 100M --snapshot --name snap /dev/vg00/lv01
```

创建一个名为 "vg00/snap" 的快照逻辑卷，用于覆盖原始逻辑卷的 20%，原始逻辑卷名为 "vg00/lv01"：

```
lvcreate -s -L 20%ORIGIN --name snap
```

创建一个名为 `/dev/vg1/sparse` 的 1Ti 稀疏设备，为 100MiB 的实际数据提供空间：

```
lvcreate --virtualize 1T --size 100M --snapshot vg1
```

使用物理设备 `/dev/sda:0-7` 和 `/dev/sdb:0-7` 创建名为 "vg00/lv01" 的线性卷，用于分配段：

```
lvcreate -L 64M -n lv01 vg00 /dev/sda:0-7 /dev/sdb:0-7
```

创建一个名为 "vg00/my_lv" 的 5GiB RAID5 卷，具有 3 个条带（以及 4 个设备的校验）和 64KiB 的条带大小：

使用 VG 中的所有空闲空间和所有 PV 创建名为 "vg00/my_lv" 的 RAID5 卷：

```
lvcreate --type raid5 -L 100%FREE -n my_lv vg00
```

创建一个名为 "vg00/my_lv" 的 5GiB RAID10 卷，具有 2 个条带镜像。注意 `-i` 和 `-m` 参数的行为不同。`-i` 指定条带数量。`-m` 指定额外副本的数量：

```
lvcreate --type raid10 -L 5G -i 2 -m 1 -n my_lv vg00
```

创建一个 100MiB 的逻辑卷，具有 2 个条带、64KiB 的块大小 256KiB 以及 1TiB 置备逻辑卷 "vg00/thin_lv"：

```
lvcreate -i 2 -I 64 -c 25 -L 100M -T vg00/pool
```

创建卷 "thinvol" 的精细快照卷 "snap"，它将共享精细池内的相同块。注意：必须指定大小，否则将创建非精细快照：

```
lvcreate -s vg00/thinvol --name snap
```

创建一个只读卷 "origin" 的精细快照卷，该卷将成为使用现有池 "vg00/pool" 的精细快照卷的源：

```
lvcreate -s --thinpool vg00/pool
```

创建一个以后可以缓存逻辑卷的缓存池。

```
lvcreate --type cache-pool -L 1G -n my_lv_cachepool /dev/fast1
```

如果存在缓存池，则创建较大的慢速设备（即源 LV）并将其链接到提供的缓存池，创建一个缓存 LV。

```
lvcreate --cache -L 100G -n my_lv_cachepool vg/lv_cachepool/slow
```

如果存在逻辑卷，则创建小型快速缓存池并将其链接到提供的逻辑卷（即源 LV），创建一个缓存 LV。

```
lvcreate --type cache -L 1G -n my_lv_cachepool vg/my_lv /dev/fast1
```

## 另见

`lvm(8)`, `lvm.conf(5)`, `lvmcache(7)`, `lvmthin(7)`, `lvconvert(8)`, `lvchange(8)`, `lvextend(8)`, `lvreduce(8)`, `lvremove(8)`, `lvrename(8)`, `lvs(8)`, `lvscan(8)`, `vgcreate(8)`, `blkid(8)`

| 外部源 | 源 | 池逻辑卷名称 | 物理卷路径 |
| :--- | :--- | :--- | :--- |

```
lvcreate [-l|extents LogicalExtentsNumber{FREE|ORIGIN|PVS|VG}] | -L|--size LogicalSize[KB|MB|GB|TB]] [-c|chunksize ChunkSize[KB|MB|GB|TB]] [--commandprofile Filename] [--nodesync] [--ignoremonitoring] [--metadataProfile ProfileName] [--monitor {y|n}] [-n--name SnapshotLogicalVolume{Name|Path}/ -s|snapshot--cache [[VolumeGroup{Name|Path}/OriginalLogicalName -V|virtualSize[KB|MB|GB|TB]]]
```

## 描述

`lvcreate` 通过从卷组的空闲段池分配逻辑段，在卷组创建一个新的逻辑卷（见 `vgcreate(8)`, `vgchange(8)`）。如果没有足够的物理段，可以通过其他物理卷扩展卷组（见 `vgxtend(8)`），或者通过减小该卷组现有逻辑卷的大小（见 `lvreduce(8)`）。如果你指定了一个或多个物理卷，物理段的分配将限制在这些卷中。第二种形式支持创建快照逻辑卷，用于备份保留原始逻辑卷的内容。

## `-C,--chunksizeChunkSize[lbsSkkmMgG]`

指定快照、缓存池和精简池卷的块大小。默认单位为字节。对于快照，该值必须在 4KiB 到 512KiB 之间，默认值为 4KiB。对于缓存池，该值必须是 32KiB 到 1Gi 之间 32KiB 的倍数。默认值为 64KiB。对于精简池，该值必须是 64KiB 到 1Gi 之间 64KiB 的倍数。默认值从 64KiB 开始，如果未指定池元数据大小，它将增长到 128Mi 以内的池元数据大小。使用 `lvm_config(5)` 中的设置 `allocation/thin_pool_chunk_size_policy` 来选择不同的计算策略。精简池目标版本 <1.4 要求此值为 2 的幂。目标版本 <1.5 不支持非 2 的幂值。

## `-C,--contiguous[y/n]`

设置逻辑卷的连续分配策略。默认基于下一个原则不进行连续分配。

## `-corelog`

这是选项 `--mirrorlog core` 的快捷方式。

## `-discards[ignore|nopassdownpassdown]`

设置精简池的丢弃（discard）行为。默认是传递（passdown）。

## `-errorwhenfull[y/n]`

配置数据耗尽时精简池的行为。默认不启用。设备将队列 I/O 操作，直到目标超时（dm-thin-pool 内核模块 `no_space_timeout`）过期。此配置系统有时间来扩展精简池数据的大小。当设置为 yes 时，I/O 操作立即被拒绝。

## `-K,--ignoreactivation`

忽略激活期间跳过逻辑卷的标记。使用 `--setactivations` 选项可以持久地设置或重置逻辑卷的激活标记。

## `-ignoremonitoring`

除非指定 `--monitor`，否则不会尝试与 dmevent 交互。

## `-L,--extentsLogicalExtents%{VGVS[FREE]ORIGIN]`

指定为新逻辑卷分配的逻辑区（logical extents）数量。如果卷是镜像的，则分配的物理区总数将大于此值。该数量也可以以百分比表示：卷组总空间的百分比（带有后缀 `%VG`）、卷组剩余空闲空间的百分比（带有后缀 `%FREE`）、指定物理卷（或多个物理卷）剩余空间的百分比（带有后缀 `%VS`），或者（对于快照）作为源卷总空间的百分比（带有后缀 `%ORIGIN`，例如 `100%ORIGIN` 将为整个源卷提供空间）。当以百分比表示时，该数字被视为分配的物理区总数的上限（包括任何镜像所使用的区，例如）。

## `-j,--majornumber`

设置主号（major number）。卷池不支持主号。此选项仅支持旧系统（内核版本 2.4），在动态分配主号的现代 Linux 系统上会被忽略。

## `-metadataprofileName configuration profile to the logical volume`

在逻辑卷上使用并绑定 `ProfileName` 配置。每下次处理该逻辑卷时，将自动应用该配置。如果逻辑卷附加了另一个配置，则优先使用逻辑卷配置。有关元数据配置更多信息，请参阅 `llvm.conf(5)`。

`-minor minor`

设置次号（minor number）。池卷不支持次号。

`-m--mirrorsMirrors`

创建一个具有 `Mirrors` 个副本的镜像逻辑卷。例如，指定 `-m1` 将产生一个有两个侧的镜像；即一个线性卷加一个副本。

指定可选参数 `-nosync` 将导致镜像的创建跳过初始重同步。之后写入的数据将进行镜像处理，但原始内容不会被复制。这对于跳过空设备可能存在的耗时且耗资源的同步非常有用。

镜像有两种实现方式可以使用，并分别对应 `raid1` 和 `mirror` 段类型。默认是 `raid1`。如果你想使用遗留的 "mirror" 段类型，请参阅 `-type` 选项获取更多信息。参阅 `llvm.conf(5)` 设置 `global_mirror_setype_default` 以配置默认镜像段类型。`global/raid10_setype_default`、`-mirrorlog` 和 `-corelog` 适用于旧的 "mirror" 段类型。

`-mirrorlog(disk|coremirrored)`

为使用旧 "mirror" 段类型的逻辑卷指定日志类型。默认是 `disk`，它是持久的，需要少量的存储空间，通常位于与镜像数据不同的设备上。使用 `core` 意味着每次逻辑卷激活（每次重启后）通过从第一个设备复制数据来重新生成镜像。使用 `mirrored` 将创建一个本身经过镜像的持久日志。

`-monitor(yn)`

如果安装了 devent，则启动或避免监控镜像、快照或精简逻辑卷。如果被监控报告使用的设备发生 I/O 错误，将根据 `llvm.conf(5)` 中的 `activation/mirror_image_fault_policy` 和 `activation/mirror_log_fault_policy` 处理故障。

`-n,nameLogicalVolume{Name}`

为新逻辑卷设置名称。如果没有此选项，将生成默认名称 "Ivol1"，其中 `#` 是逻辑卷的 LVM 内部编号。

`-nosync`

导致镜像创建跳过初始重同步。

`-nudevvsync`

禁用 udev 同步。进程将不会等待 udev 的通知。只有在 udev 未运行时才应使用此项。

`-p,permission{rw}`

设置读取 (r) 或写入 (rw) 的访问权限。默认是读和写。

`-M,persistent{yn}`

设置为 y 以使次号持久化。仅在指定主号时默认为 yes。否则为 no。

`-pooladatatasMetadataSize{bBsSkMgG}`

设置池的元数据大小。精简池的支持值范围在 2MiB 到 16GiB 之间，缓存池最高支持 16GiB。默认单位为兆字节。

`-poolmetadataspare{\yn}`

控制用于自动池恢复的稀疏逻辑卷的创建和维护。卷组内仅维护这样一个卷，其大小为最大的池元数据。默认是 yes。

`-raidmaxrecoveryRate{bBsSkMgG}`

设置 RAID 逻辑卷的最大恢复速率。速率指定为数组中每个设备的数量。如果没有给出后缀，则假设为 KiB/sec/device。将恢复速率设置为 0 意味着无限制。

`-minrecoveryRate{bBsSkMgG}`

设置 RAID 逻辑卷的最小恢复速率。速率指定为数组中每个设备的数量。如果没有给出后缀，则假设为 KiB/sec/device。将恢复速率设置为 0 意味着无限制。

`-r,readhead{ReadAectors|auto}`

设置此逻辑卷的读取扇区数。对于 svm 格式数据的卷组，该值必须在 2 到 120 之间。默认值为 auto，允许内核自动选择合适的卷。

`-R,resizeMirrorLogRegionSize{bBsSkMgG}`

镜像被分为此大小（MiB）的区域，镜像日志利用颗粒跟踪哪些区域已同步。

`-k,setactivations{yn}`

控制逻辑卷是否持久地标记为激活期间跳过。默认情况下，快照卷被标记为跳过激活。`lvm.conf(5)` `activation/auto_set_activation` 如何更改默认行为。要激活卷，必须使用额外的 `-K|ignoreactivation` 选项。激活期间不会应用该标记。使用 `changesetactivation{yn}` 命令跳过现有卷的标记。是否附加了标记，使用 `vs` 命令在 `lv_attr` 位中报告。

`-L,sizeLogicalVolumeSize{bBsSkMgGtpPeE}`

指定为新逻辑卷分配的大小。后缀 B 表示 512 字节扇区，K 表示千字节，M 表示兆字节，G 表示吉字节，T 表示拍字节或 E 表示艾字节。默认单位为兆字节。

## `--snapshotOriginalLogicalVolume{Name|Path}`

为现有原始逻辑卷（或源）创建一个快照逻辑卷（或快照）。快照提供了源内容的“冻结镜像”，而源卷仍然可以进行更新。它们实现了一致性备份以及对已删除/覆盖的数据/文件的在线恢复。当源卷为精简卷且未指定大时，将创建精简快照。精简快照与精简池卷共享块。指定大小的非精简卷快照不需要等量的存储源。在典型场景下，15-20% 可能就足够。如果快照空间不足，使用 `extend` 来扩展。`lvreduce(8)` 也支持缩小快照。在快照上运行 `lvs(8)` 以检查为其分配了多少数据。

注意：分配给快照的一小部分空间用于跟踪数据块的位置——监控快照的增长速率，以避免空间耗尽。如果指定了 `--thinpool`，将创建一个精简卷，并将原始逻辑卷作为其外部源使用。只有只读卷可以作为外部源。要创建外部源，lvm 期望该卷处于非活动状态。外部源可用于/共享许多精简卷，即使它们来自不同的池。参见 `lvconvert(8)` 在转换为带有外部源的精简卷。

## `--stripesStripes`



提供条带数量。这等于分散逻辑卷的物理卷数量。在创建 RAID 4/5/6 逻辑卷时，用于校验所需的额外设备已完全考虑在内。使用 `-i3` 将为条带逻辑卷使用 3 个设备，为 RAID 4/5 使用 4 个设备，为 RAID 6 使用 5 个设备。或者，如果省略 `-i` 参数，RAID 4/5/6 将对卷组中的所有 PV 或指定的所有 PV 进行分散。

## --stripesSize

提供条带粒度的千字节数。为了符合 LVM 格式的元数据，条带大小必须是 2^n（n = 2 到 9）。对于元数据 LVM 格式，条带大小可以是 2 的更大幂，但不能超过物理范围区大小。

## --thin

创建精简池或精简逻辑卷或两者都有。指定可选参数 `--size` 或 `--extents virtualsize` 将导致从精简池卷创建精简逻辑卷。指定两个参数将导致使用该池创建精简池和精简卷。使用 `lvthin(7)` 获取更多关于精简配置的支持信息。精简配置需要 device mapper 内核版本 3.2 或更高。

## --thinpoolThinPoolLogicalVolume{Name|Path}

指定精简池卷的名称。另一种方法是在卷组参数后指定池名称。

## --type SegmentType

创建一个指定段类型的逻辑卷。支持的类型有：

`cache`, `cache-pool`, `error`, `linear`, `mirror`, `raid1`, `raid4`, `raid5_la`, `raid5_ls=(raid5)`, `raid5_ra`, `raid5_rs`, `raid6_nr`, `raid6_zr=(raid6)`, `raid10`, `snapshot`, `striped`, `thin-pool(or zero)`。段类型具有命令行别名以启用其使用。当未显式指定类型时，将从选项组合中选择：`-h|--cache--cachepool(cache or cachepool)`, `-T|--thin--thin-pool(thin or thinpool)`, `-m|--mirrors(raid1 or mirror)`, `-s|--snapshot|-V|--virtualSizeVirtualSize(bSSkkmMgGtTtpPeE)`

创建一个精简配置的设备或指定大小的设备（默认为 MiB）。参见 `lvm.conf(5)` 设置 `global/sparse_type_default` 以配置稀疏段类型。参见 `lvthin(7)` 获取更多关于配置支持的信息。写入稀疏快照的任何内容在从其读取时都会返回。从设备的其他区域读取将返回零块。虚拟快照通过使用零目标创建一个具有所请求大小的隐藏虚拟设备来实现。该设备使用 `_origin` 后缀。注意：使用稀疏快照对于较大的设备尺寸（GiB）是高效的，在这种情况下应使用精简配置。

## -W,--wipesignatures(y|n)

控制在新建的逻辑卷上擦除检测到的签名。如果未指定此选项，默认每次执行置零（`-Z--zero`）时都会擦除签名。此默认行为可以通过 `lvm.conf(5)` 中的 `allocation/wipe_signatures_when_zeroing_new_ls` 设置来控制。如果 blkid 擦除在使用 `lvm.conf(5)` 中的 `allocation/use_blkid_wiping` 设置且 LVM2 编译了 blkid 擦除支持，则使用 `blkid(8)` 库来检测签名（使用 `blkid -k` 命令列出识别的签名）。否则，使用原生 LVM2 代码检测签名（仅在此情况下会检测 MD RAID、swap 和 LUKS 签名）。如果仅设置了标志，则逻辑卷不会被擦除。

## -Z,--zero(y|n)

控制新建逻辑卷前 4KiB 数据置零。默认为 yes。快照 COW 卷始终置零。如果仅设置了标志，则逻辑卷不会被置零。

警告：尝试挂载未置零的逻辑卷可能会导致系统挂起。

## EXAMPLES

在名为 `vg00` 的卷组创建一个具有 3 个条带、条带大小为 8KiB 且大小为 100MiB 的条带逻辑卷。逻辑卷的名称将由 `lvcreate` 选择：

```
lvcreate -i 3 -I 8 -L 100M vg00
```

创建一个具有 2 个侧、可用大小为 500 MiB 的镜像逻辑卷。此操作需要 3 个设备（或选项 `--alloc anywhere`）——两个用于镜像设备，一个用于日志：

```
lvcreate -m1 -L 500M vg00
```

创建一个具有 2 个侧、可用大小为 500 MiB 的镜像逻辑卷。此操作需要 2 个设备——日志是“内存中”的：

```
lvcreate -m1--mirrorlog -L 500M vg00
```

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -s vg00/lvol1 --name vg00/snap
```

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -L 20% -s vg00/lvol1 --name snap
```

创建一个精简配置的设备或指定大小的设备（默认为 MiB）。参见 `lvm.conf(5)` 设置 `global/sparse_type_default` 以配置稀疏段类型。

创建一个名为“`vg00/snap`”的快照逻辑卷，在快照创建时访问名为“`vg00/lvol1`”的原始逻辑卷的内容。如果原始逻辑卷包含文件系统，你可以将快照逻辑卷挂载到任意目录以访问文件系统内容运行备份，同时原始文件系统继续。

```
lvcreate -s vg00/thinvol --name snap
```

另参见

`lvm(8)`, `lvm.conf(5)`, `lvmcache(7)`, `lvmthin(7)`, `lvconvert(8)`, `lvchange(8)`, `lvextend(8)`, `lvreduce(8)`, `lvremove(8)`, `lvrename(8)`, `lvs(8)`, `lvscan(8)`, `vgcreate(8)`, `blkid(8)`

# LVDISPLAY

## 名称

`lvdisplay` – 显示逻辑卷的属性

## 概要览

```
lvdisplay [-a|--all] [-c|--colon] [--commandprofile ProfileName] [-d|--debug] [-h|?|--help] [--ignorelockingfailure] [--ignoreskipcluster] [--maps] [--nosuffix] [-P|--partial] [-S|--select Selection] [--units hHbBsSkKmMgGtTpPeE] [-v|--verbose] [--version] [VolumeGroupNameLogicalVolume{Name|Path} ...]
```

```
lvdisplay -C|--columns [--aligned] [--binary] [-a|--all] [--commandprofile ProfileName] [-d|--debug] [-h|?|--help] [--ignorelockingfailure] [--ignoreskipcluster] [--headings] [--nosuffix] [-o|--options] [+|Field,Field...]] [-O|--sort] [+|Key1[+|Key2...]] [-P|--partial] [--segments] [-S|--select Selection] [--separator Separator] [--unbuffered] [--units hHbBsSkKmMgGtTpPeE] [-v|--verbose] [--version] [VolumeGroupNameLogicalVolume{Name|Path} ...]
```

`lvdisplay` 允许你查看逻辑卷的属性，如大小、读/写状态、快照信息等。

`lvs(8)` 是替代方案，以 ps(1) 的风格提供相同的信息。相比 `lvdisplay`，推荐使用 `lvs(8)`。

## 选项

常用选项参见 `lvm(8)`，使用 `--columns--all` 提供的选项参见 `lvs`。

- `-a` 在输出中包含关于内部逻辑卷的信息，这些卷是普通访问逻辑卷的组成部分（例如镜像），但无法独立访问（例如不可挂载）。例如，在使用 `lvcreate -ml --mirrorlog disk` 创建镜像后，此选项将显示三个带有后缀 `imageage_0`、`imageage_1` 和 `mlog` 的内部逻辑卷。

- `-columns` 以列输出，等同于 `lvs(8)`。列出的选项与 `lvs(8)` 中分隔的选项相同。

- `-c, colon` 生成用冒号分隔的输出，以便在脚本或程序中进行解析。注意：`lvs(8)` 对输出提供了更多的控制。其取值为：逻辑卷名称 | 卷组名称 | 逻辑卷访问权限 | 逻辑卷状态 | 内部卷编号 | 以扇区为单位的逻辑卷打开计数 | 与逻辑卷关联的逻辑区 | 逻辑卷的逻辑区 | 逻辑卷分配策略 | 逻辑卷预读扇区 | 逻辑卷设备 | 逻辑卷次设备号

- `-m,maps` 显示逻辑区到物理卷和物理区的映射。要将物理区映射到逻辑区，请使用：`pvs --segments -o+lv_name,seg_start_pe,segtype`

## 示例

显示该逻辑卷的属性。如果为此原始逻辑卷创建了快照逻辑卷，此命令将显示所有快照逻辑卷及其状态（活动或非活动）：

```
lvdisplay -v vg00/lvol2
```

显示此快照逻辑卷的属性以及它关联的原始逻辑卷：

```
lvdisplay vg00/snapshot
```

## 另参见

`lvm(8)`, `lvcreate(8)`, `lvs(8)`, `lvscan(8)`, `pvs(8)`

# LVEXTEND

## 名称

`lvextend` – 扩展逻辑卷的大小

## 概要览

```
lvextend [--alloc AllocationPolicy] [-A|--autobackup {yn}] [--commandprofile ProfileName] [-d|--debug] [-h|--help] [-f|--force] [-i|--stripes Stripes [-I|--stripe]] [-L|--extents [+LogicalExtentsNumber[%{VG|LV|PVS|FREE|ORIGIN}] -L|--size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]] [-n|--nofckk] [-r|--noudevsync|--resizefs] [--use-policies] [-t|--test] [-v|--verbose] LogicalVolumePath[PhysicalVolumePath[:PE[-PE]]...
```

`lvextend` 允许你扩展逻辑卷的大小。支持扩展快照逻辑卷（创建快照的信息参见 `lvcreate(8)`）。但要更改镜像逻辑卷中的副本数量，请使用 `lvconvert(8)`。

## 选项

常用选项参见 `lvm(8)`。

- `-force` 无需提示直接进行大小扩展。

- `-size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]` 允许你扩展逻辑卷的大小。

- `-stripes` 指定条带数量。

- `-I|--stripe` 指定条带数量。

- `-L|--extents [+LogicalExtentsNumber[%{VG|LV|PVS|FREE|ORIGIN}] -L|--size[+]LogicalVolumeSize[bBsSkKmMgGtptpPeE]]` 允许扩展逻辑卷。

- `-n|--nofckk` 在扩展文件系统时不执行 fsck。

- `-r|--noudevsync|--resizefs` 随逻辑卷调整底层文件系统的大小。

- `--use-policies` 根据策略调整逻辑卷的大小。

- `-t|--test` 执行空运行。

- `-v|--verbose` 详细输出。

## 示例

将物理卷 `/dev/sdk3` 逻辑卷 `vg01/lvol10` 扩展 54MiB。这只有在 `/dev/sdk3` 是卷组 `vg01` 成员且其中有空闲区的情况下可行：

```
lvextend -L+54 /vg01/lvol10 /dev/sdk3
```

根据物理卷 `/dev/sdk3` 的可用空间扩展逻辑卷 `vg01/lvol01`。这等同于在命令行中指定 `-100%PVS`：

```
lvextend /vg01/lvol01 /dev/sdk3
```

使用物理区 `/dev/sda-9` 和 `/dev/sdb-9` 将逻辑卷 `vg01/lvol01` 扩展 16MiB：

```
lvextend -L+16M vg01/lvol01 /dev/sda-9 /dev/sdb-9
```

# 说明

`lvmconfig` 根据 LVM 配置树生成格式化后的输出。该命令在发布 2.02.119 版本中添加，并有一个完全相同的长形式 `lvm dumpconfig`。

## 选项

- `-f`, `--file filename`

将输出发送到名为‘`filename`’的文件。

- `-l`, `--list`

列出带有摘要性注释的配置设置。这等同于使用 `lvmconfig --type list --summary`。

`--type {current|default|diff|full|missing|new}profilable|profilable-command|profilable-metadata`

选择要显示的配置类型。所显示的配置设置将根据所选的类型分配默认值或当前使用的值。如果未选择类型，则默认使用 `--type current`。每当带有默认值的配置设置被注释掉时，即意味着该设置没有定义任何具体的默认值。输出可以保存并用作适当的 `lvm.conf(5)` 文件。

`current`

显示当前的 `lvm.conf` 配置，并合并了已使用的任何标签配置（tag config）。有关关于 LVM 配置方法的更多信息，请参阅 `lvm.conf(5)`。

`default`

显示所有分配了默认值的配置设置。

`diff`

显示所有值与默认值不同的配置设置。每个配置设置分配的值为当前使用的值。这实际上是极简的 LVM 配置，可以在不更改当前配置行为的情况下使用。

`full`



显示所有完整的配置树 - 当前配置树（`--type current`）与使用默认值的设置树（`--type missing`）的组合。这正是 LVM 在执行命令执行期间所使用的配置树。使用此类型还意味着使用 `--mergedconfig --summary` 选项，以便为每个设置查找现有的配置，并且对于没有使用默认值的设置，会打印一条额外的注释行来标明这一点。

### `list`
显示所有配置设置的纯列表。

### `missing`
显示所有在当前使用的配置中缺失且分配了默认值的配置设置，LVM 会自动回退使用这些默认值。

### `new`
显示当前 LVM 版本或通过 `--atversion` 选项指定的特定版本引入的所有新配置设置。

### `profilable`
显示所有分配了默认值的可分析（profilable）配置设置。有关配置方法的更多信息，请参阅 `lvm-conf(5)`。

显示所有分配了默认值且可用在命令配置文件（command profile）中的可分析配置设置。这是 `--type profilable-metadata` 显示的设置的子集。

显示所有分配了默认值且可用在元数据配置文件（metadata profile）中的可分析配置设置。这是 `--type profilable` 显示的设置的子集。

`--atversion version` 以 `x.y.z` 格式指定 LVM 版本，其中 `x` 是主版本号，`y` 是次版本号，`z` 是补丁版本号（patchlevel）（例如 `2.2.106`）。当显示配置时，将仅考虑被此 LVM 版本识别的配置设置。这可以用于显示特定 LVM 能够理解且不包含任何新设置的配置，否则当 LVM 检查配置时遇到新设置将会发出警告信息。

`--ignoreadvanced` 从输出中排除高级配置设置。

`--ignoreunsupported` 从输出中排除不支持的配置设置。这些设置仅用于调试和开发目的，或者其支持尚不，不用于生产环境。`current` 和 `diff` 类型默认在输出中包含不支持的设置，所有其他类型均忽略这些设置。

`--ignorelocal` 本地部分（Local section）。

`--configConfigurationString` 使用 `ConfigurationString` 覆盖现有配置。该配置随后应用于 `lvm` 命令本身。有关配置级联的更多信息，请另参阅 `lvm-conf(5)`。

`--commandprofile ProfileName` 使用 `ProfileName` 覆盖现有配置。该配置随后应用于 `lvm` 命令本身。有关配置级联的更多信息，请参阅 `--mergedconfig` 选项和 `lvm-conf(5)`。

`--profile ProfileName` 与使用 `--commandprofile` 相同，但配置不会应用于 `lvm` 命令本身。

`--metadataprofile ProfileName` 使用 `ProfileName` 覆盖现有配置。元数据配置文件中的定义对 `lvm` 命令本身没有影响。`lvmconfig` 仅显示配置。有关配置级联的更多信息，请参阅 `--mergedconfig` 选项和 `lvm-conf(5)`。

`--mergedconfig` 当运行 `LVMCOMMAND` 且带有 `--config` 和/或 `--commandprofile`（或使用 `LVM_COMMAND_PROFILE` 环境变量）、`profile` 或 `--metadataprofile` 选项时，在显示之前合并配置级联的所有内容。如果不使用 `--mergedconfig` 选项，则仅显示级联前端的配置。有关配置级联的更多信息，请另参阅 `lvm-conf(5)`。

`--showdeprecated` 在输出中包含已弃用的配置设置。这些设置总是弃用的，因为如果通过 `--atversion` 选项指定版本，当指定的版本低于这些设置被弃用的版本时，会自动包含这些弃用设置。`current` 和 `diff` 类型默认在输出中包含弃用设置，所有其他类型均忽略弃用设置。

`--showunsupported` 在输出中包含不支持的配置设置。这些设置用于调试或开发目的，或者其支持尚不完整，不用于生产环境。`current` 和 `diff` 类型默认在输出中包含不支持的设置，所有其他类型均忽略不支持设置。

`--validate` 验证当前使用的配置并带有返回码退出。

# 相关

`lvm(8)` `lvm.conf(5)`

# LVP POLL

> 名称

`lvpoll` – `lvmpolld` 用来完成某些逻辑卷操作的内部命令。

## 概要

```
lvm lvpoll --operation {pvmove|convert|merge|merge_thin} [--abort] [-A|--autobackup {yn}] [--commandprofile ProfileName] [-d|--debug] [-h|?|--help] [--handlemissingpvs] [-i|--interval Seconds] [-t|--test] [-v|--verbose] [--version] LogicalVolume[Path]
```

# 说明

`lvpoll` 是 `lvmpolld(8)` 用来监控并完成 `lvconvert(8)` 和 `pvmove(8)` 操作的内部命令。`lvpoll` 本身不启动这些操作，你不应该直接调用它。

`LogicalVolume` 正在转换的逻辑卷，或者在 `pvmove` 的情况下，内部 `pvmove` 逻辑卷的名称（参见示例）。

# 通用选项

参见 `lvm(8)` `{convert|merge|merge_thin|pvmove}`

- 的操作，`pvmove` 指移动数据的 `pvmove` 操作。`convert` 指增加数据卷冗副本数量的操作。`merge`, `merge_thin` 表示涉及镜像维护的快照的合并操作。`merge` `pvmove(8)` 和 `lvconvert(8)` 说明如何启动这些操作。

- `--abort` 正在进行的 `pvmove`。参见 `pvmove(8)`。

- `--handlemissingpvs` 当轮询操作需要处理的 PV 才能继续时使用。这发生在 `lvconvert(8)` 修复带有多个故障设备的镜像时。

- `--i`, `--interval Seconds` 按隔时间报告进度。

## 示例

恢复由逻辑卷 `vg00/pvmove` 标识的 `pvmove` 操作轮询：

```
lvm lpvoll --polloperation pvmove vg00/pvmove
```

取消同一个 `pvmove` 操作：

```
lvm lpvoll --polloperation pvmove --abort vg00/pvmove
```

若要查找由原始 `pvmove /dev/sda1` 命令产生的 `pvmove` 逻辑卷名称，可以使用以下 `lvs` 命令。（去掉 LV 名称上的括号。）

```
lvs a -S move_pv=/dev/sda1
```

恢复镜像转换 `vg00/lvmmirror` 的轮询：

```
lvm lpvoll --polloperation conversion vg00/lvmmirror
```

完成镜像修复：

```
lvm lpvoll --polloperation conversion vg/damaged_mirror --handlemissingpvs
```

处理快照合并：

```
lvm lpvoll --polloperation merge vg/snapshot_old
```

完成精细卷快照合并：

```
lvm lpvoll --polloperation merge_thin vg/thin_snapshot
```

# 另参见

`lvconvert(8)`, `lvm(8)`, `lvmpold(8)`, `lvs(8)`, `pvmove(8)`

# LVM

## 名称

`lvm` – LVM2 工具

## 概要

```
lvm [command | file]
```

## 描述

`lvm` 提供了 LVM2 的命令行工具。单独的手册页详细描述了每个命令。

如果调用 `lvm` 时不带参数，它将显示一个 `readline` 提示符（假设其编译时带有 `readline` 支持）。可以在此提示符下通过 `readline` 功能交互式输入 LVM 命令，包括历史记录、命令名和选项补全。详情请参阅 `readline(3)`。

如果调用 `lvm` 时将 `arg[0]` 设置为特定 LVM 命令的（例如通过使用硬链接或软链接），它将作为该命令运行。

在调用时，`lvm` 要求只有标准文件描述符 `stdin`、`stdout` 和 `stderr` 可用。如果发现其他描述符，它们将被关闭，并发出关于泄露的警告信息。可以通过设置环境变量 `LVM_SUPPRESS_FD_WARNINGS` 来抑制此警告。

当将 VG 或 LV 名称作为参数时，全路径名是可选的。在名为 `"vg0"` 的 VG 中名为 `"lv0"` 的 LV 可以被指定为 `"vg0/lv0"`。当需要 VG 列表但留空时，将用所有 VG 的列表替换。当需要 LV 列表但给出一个 VG 时，将用该 VG 中所有 LV 的列表替换。因此 `lvdisplay vg0` 将显示 `"vg0"` 中的所有 LV。也可以使用标签——详见下文 `addtag`。

使用内置 shell 的一个优势是配置信息会在命令之间在内部进行缓存。

也可以在命令行中提供一个包含每行一个命令的简单脚本文件。如果第一行是 `#!` 后跟 `lvm` 的绝对路径，则也可以直接执行该脚本。

# 内置命令

以下命令内置在 `lvm` 中，通常不会在文件系统中为它们创建链接。

**`config`** – 与下文 `llvmconfig(8)` 相同。

**`devtypes`** – 显示识别的内置块设备类型。

**`dumpconfig`** – 与下文 `llvmconfig(8)` 相同。

**`formats`** – 显示识别的元数据格式。

**`help`** – 显示帮助文本。

**`lvpoll`** – `lvpolld` 用于完成某些逻辑卷操作的内部命令。

**`pvdata`** – LVM2 中未实现。

**`segtypes`** – 显示识别的逻辑卷段类型。

**`systemid`** – 显示当前在此主机上设置的系统 ID（如果有）。

**`tags`** – 显示在此主机上定义的任何标签。

**`version`** – 显示版本信息。

# 命令

以下命令实现了 LVM 的核心功能。

- **`pvchange`** - 更改物理卷的属性。
- **`pvck`** - 检查物理卷的元数据。
- **`pvcreate`** - 初始化磁盘或分区供 LVM 使用。
- **`pvdisplay`** - 显示物理卷的属性。
- **`pvmove`** - 移动物理范围区。
- **`pvremove`** - 移除物理卷。
- **`pvresize`** - 通过 LVM2 调整磁盘或分区的大小。
- **`pvs`** - 报告物理卷的信息。
- **`pvscan`** - 扫描所有磁盘以查找物理卷。
- **`vgcfbackup`** - 备份卷组描述区。
- **`vgcfstore`** - 恢复卷组描述区。
- **`vgchange`** - 更改卷组的属性。
- **`vgck`** - 检查卷组的元数据。
- **`vgconvert`** - 转换卷组元数据格式。
- **`vgcreate`** - 创建卷组。
- **`vgdisplay`** - 显示卷组的属性。
- **`vgexport`** - 使卷组对系统未知。
- **`vgxtend`** - 向卷组添加物理卷。
- **`vgimport`** - 使已导出的卷组对系统已知。
- **`vgmerge`** - 合并卷组。
- **`vgreduce`** - 缩小卷组。
- **`vgremove`** - 移除卷组。
- **`vgname`** - 重命名卷组。
- **`vgs`** - 报告所有卷组。
- **`vgsplit`** - 将卷组拆分为两个。
- **`lvchange`** - 更改逻辑卷的属性。
- **`lvconvert`** - 将逻辑卷转换为快照。
- **`lvcreate`** - 创建逻辑卷。
- **`lvdisplay`** - 显示逻辑卷的属性。
- **`lvextend`** - 扩展逻辑卷的大小。
- **`lvmconfig`** - 显示配置。
- **`lvscan`** - 扫描所有设备以查找逻辑卷。
- **`lvump`** - 为诊断目的创建转储。
- **`lvremove`** - 移除逻辑卷。
- **`lvrename`** - 重命名逻辑卷。
- **`lvresize`** - 调整逻辑卷的大小。
- **`lvs`** - 报告所有逻辑卷。
- **`lvscan`** - 扫描所有磁盘以查找逻辑卷。

## 选项

以下选项适用于许多命令。它们通用地记录在这里，而不是在手册页中重复。

选项名称额外的连字符会被忽略。例如，`--readonly` 是被接受的。

- **`h, --help`** - 显示帮助文本。
- **`--version`** - 显示版本信息。
- **`-v, --verbose`** - 设置详细级别。重复1到3次以增加发送到 `stdout` 和 `stderr` 的细节。覆盖配置设置。
- **`-d, --debug`** - 设置调试标记。重复1到6次以增加发送到日志文件和或 `syslog`（如果配置）的细节。覆盖配置设置。
- **`q, --quiet`** - 抑制输出和日志消息。覆盖 `-d` 和 `-v`。重复一次还可以抑制任何带有“no”的提示。
- **`--yes`** - 不进行交互式确认，而是假设答案为“是”。使用此项时要小心！
- **`-t, --test`** - 以测试模式运行。命令不会更新元数据。通过禁用所有元数据写入但仍返回调用函数来实现。如果工具依赖读取它更改的元数据，在多阶段操作中可能会导致异常错误。
- **`--driverloaded {y/n}`** - 是否加载设备映射内核驱动程序。将其设置为 `no`，则不会尝试连接驱动程序。
- **`-A, --autobackup {y/n}`** - 更改后是否自动备份元数据。我们强烈建议不要禁用此项！参见 `vgcfbackup(8)`。

`--partial`

设置后，工具将尽力提供对部分可用卷组的访问（一个多个物理卷缺失）。逻辑卷的部分缺失，将用 **`/dev/ioerror`** 替换，您可以使用 **`dmsetup`** 设置其在访问时返回 I/O 错误。要插入相同或更大的替换物理卷，请使用 **`pvcreate -u`** 设置 `uuid` 以匹配原始值，然后运行 **`vgcfrestore(8)`**。

`select` 用于报告命令，仅显示匹配选择标准的行。所有行都会被显示，并带有一个额外的“selected”（已选择）列（`-o selected`），如果该行匹配选择则显示为 `1`，否则显示为 `0`。对于非报告类进程（如 LVM 实体），可以使用选择来匹配要处理的项。有关选择标准构建方式的更多信息，请参见本页的 `SELECTION CRITERIA` 部分。

`metadata` 指定要使用的磁盘元数据类型，例如 `lvm1` 或 `lvm2`，可以分别缩写为 `1` 或 `2`。默认（`lvm2`）可以通过设置配置文件全局部分中的 `format` 来更改。

`lockingfailure` 允许在锁定模块失败时也能继续执行 `lvchange -ay` 和 `vgchange -ay` 等只读元数据操作。一种情况是当脚本运行时，如果锁定目录被挂载为只读，就会发生在系统初始化。

`skipped` 在没有集群锁定的情况下运行命令且某些集群卷组（Volume Groups）需要跳过时，用于避免返回非零状态码。

`readonly` 以特殊的只读模式运行命令，该模式将读取磁盘元数据而无需获取任何锁。这可以用于在虚拟机运行时查看虚拟机内部内部元数据。它也可以用于在未配置或运行锁定的情况下，查看集群卷组的元数据。此选项不会尝试与 `devicemapper` 驱动程序通信，因此无法报告逻辑卷是否激活。

`foreign` 访问通常会被跳过的外部卷组（VGs）。它可以报告或显示由另一个主机拥有的 VG。由于未使用元数据缓存和磁盘元数据，此选项可能会导致命令执行性能不佳。

`shared` 访问通常会被跳过的共享卷组（VGs）。在未使用锁定的情况下，它可以报告或显示未被锁定的 VG。

`Tag` 为 PV、VG 或 LV 添加标签。多次提供此参数可一次性添加多个标签。标签是一个单词，可用于对相同类型的 LVM 对象分组。标签可以在 PV、VG 或 LV 的命令行中给出。标签应以 `@` 为前缀以避免歧义。每个标签都会通过替换所有拥有该标签的对象进行扩展。PV 仅在作为卷组的一部分时才能拥有标签：如果 PV 从 VG 中移除，则标签将被丢弃。例如，你可以将 LV 标记为 `database`，将其他的标记为 `userdata`。对象可以同时拥有多个标签。只有 LVM2 元数据格式不支持标记。标签允许的字符为：`A-Z a-z 0-9 _ +`。从 `2.7` 版本开始接受以下字符：`/ = ! # &`

`Tag` 从 PV、VG 或 LV 中删除标签。多次提供此参数可移除多个标签。

`-alloc (anywhere|contiguous|cling|normal)` 当命令需要从卷组分配物理区（Extents）时选择策略。每个卷组和逻辑卷都有定义的分配策略。卷组的默认策略是 `normal`，除非在同一物理卷上放置条带。逻辑卷的默认策略是 `inherit`，与卷组策略相同。可以使用 `lvchange(8)` 和 `vgchange(8)` 在命令行上更改这些策略。`contiguous` 策略要求任何非逻辑卷第一个物理区的物理位置必须与其前一个物理位置相邻。`cling` 策略将新的物理区放在逻辑卷的同一条带上。如果有足够的物理区满足分配请求但 `normal` 未使用它们，`anywhere` 即使在同一物理卷上放置两个条带也会降低性能。

`-commandprofile ProfileName` 在处理 LVM 命令时选择使用的配置配置文件。另见 `lvm.conf(5)` 获取有关命令配置及其如何与其他 LVM 配置方法配合的信息。使用 `commandprofile` 选项将覆盖环境变量 `LVM_COMMAND_PROFILE` 指定任何命令配置。



`-metadataprofile ProfileName` 在处理 LVM 命令时选择使用的元数据配置。。在创建卷组或逻辑卷时使用元数据配置文件，名称会保存在元数据中。当下次处理卷组或逻辑卷时，会自动应用元数据，无需使用 `-metadataprofile` 选项。另见 `lvm.conf(5)` 获取有关元数据配置及其如何与其他 LVM 配置方法配合的信息。

`-profile ProfileName` `vgcreate`、`lvcreate`、`vgchange` 和 `lvchange` 命令的 `-metadataprofile` 简写，以及其他命令的 `-commandprofile` 简写（`lvmconfig` 命令的 `-profile` 有特殊含义，更多信息见 `lvmconfig(8)`）。

`-config ConfigurationString` 使用 `ConfigurationString` 作为配置的直接字符串表示来覆盖现有配置。`ConfigurationString` 的格式与任何 LVM 配置文件使用的格式相同。有关**命令行上的直接配置覆盖**以及如何与其他 LVM 配置方法配合的更多信息，请参见 `lvm.conf(5)`。

### VALID NAMES

VG 和 LV 名称的有效字符为：`a-z A-Z 0-9 + _`

VG 和 LV 名称不能以连字符开头。还有许多内部使用的各种保留名称不能作为 LV 或 VG 名称。VG 不能命名为 `.`、`..`、`snapshot` 或 `move`。LV 名称可能包含以下任何字符串：`_cdata`、`_cmeta`、`_corig`、`_mlog`、`_mimage`、`_mspare`、`_rimage`、`_rlog`、`_tdata` 或 `_meta`。创建时不能任何已存在的名称。如果你需要处理 `/dev/mapper` 中的节点，可以使用 `VolumeGroupName/LogicalName`，精确格式可能会随版本变化。

### ALLOCATION

当操作需要为一个或多个逻辑卷分配物理区（Extents）时，步骤如下：

首先，生成卷组中所有未分配物理区的集合。如果在命令行末尾提供了任何物理区范围，则仅考虑指定物理卷上这些范围内的未分配物理区。

然后，依次尝试每种分配策略，从最严格的策略（`contiguous`）开始，以使用 `alloc` 指定或设置为特定逻辑卷默认的分配策略结束。对于每种策略，从需要填充的空卷空间中编号最低的物理区开始，根据策略限制尽可能多分配。如果需要更多空间，则移动到下一种策略。

限制如下：

`contiguous` 要求任何非逻辑卷第一个物理区的逻辑区物理位置与其紧邻的逻辑区物理位置相邻。

`cling` 要求添加到现有逻辑卷的任何逻辑区的物理卷已被该卷之前的至少一个物理区占用。如果定义了配置 `allocation/cling_tag_list`，则两个物理卷匹配列表中的任何标签时被认为是匹配的。这允许具有相似属性（如物理位置）的物理卷组被标记并在分配时视为等同。

当逻辑卷进行条带化或镜像时，上述限制独立应用于每个需要空间的条带或镜像单元（leg）。

`normal` 不会选择与并行逻辑卷（即不同条带或镜像单元/leg）在相同偏移处已分配的逻辑区共享同一物理卷的物理区。

在与持有数据的逻辑卷同时分配镜像日志时，`normal` 会首先尝试为日志和数据选择不同的物理卷。如果不可行且 `allocation/mirror_logs_require_separate_pvs` 配置参数设置为 0，则允许日志与部分数据共享物理卷。

在分配精简池元数据时，根据 `allocation/thin_pool_metadata_require_separate_pvs` 配置的值，类似于最后一段中关于镜像日志的考虑因素。

如果你依赖此处记录的任何布局行为，请注意它是可能会在未来的版本中发生变化。

例如，如果你在命令行中提供了两个物理卷（Physical Volumes），且它们具有相同数量的可分配可用物理区（Physical Extents），当前程序会按照列出的顺序考虑每一个卷，但不能保证未来的版本会维持这一特性。如果对于特定的逻辑卷（Logical Volume）获取特定的布局很重要，你应该通过一系列 `lvcreate(8)` 和 `lvconvert(8)` 步骤来构建，使得上述限制应用于每个步骤时，工具对布局没有裁量权。

要查看任何特定情况下分配过程当前的工作方式，请读取调试日志输出，例如通过向命令添加 `-vvvv`。

# 逻辑卷类型

某些逻辑卷类型的创建非常简单，可以通过单个 `lvcreate(8)` 命令完成。线性逻辑卷和条带逻辑卷类型就是此类示例。其他逻辑卷类型可能需要多个命令来创建。缓存 `lvmcache(7)` 和精简配置 `lvmthin(7)` 类型就是此类示例。

# 选择标准

选择标准是一组通过逻辑运算符和分组运算符组合的语句。语句由列名组成，使用比较运算符定义一组值。有关可用于选择的列名（字段）的完整列表，请参见 `<lvm reporting command>-S` 帮助的输出。

比较运算符 `cmp_op`:

- `=~` 匹配正则表达式。
- `!~` 不匹配正则表达式。
- `=` 等于。
- `!=` 不等于。
- `>=` 大于或等于。
- `>` 大于。
- `<=` 小于等于。
- `<` 小于。

二进制逻辑运算符 `cmp_log`:

- `&&` - 所有字段必须匹配
- `,` - 所有字段必须匹配
- `||` - 至少有一个字段匹配
- `#` - 至少有一个字段匹配

一元逻辑运算符：

- `!` - 逻辑否定

分组运算符：

- `(` - 左括号
- `)` - 右括号
- `[` - 列表开始
- `]` - 列表结束
- `{` - 列表子集开始
- `}` - 列表子集结束

非正式语法规范：

```
STATEMENT = column cmp_op VALUE | STATEMENT log_op STATEMENT |
(STATEMENT) | {STATEMENT}
VALUE = [VALUE log_op VALUE] 对于基于列表的类型：字符串列表。严格匹配。log_op 在整个值中必须始终为一种类型。
VALUE = {VALUE log_op VALUE} 对于基于列表的类型：字符串列表。匹配子集。log_op 在整个值中必须始终为一种类型。
VALUE = value 对于标量类型：数字（整数）、大小（带有单位后缀的浮点数）、百分比（带有或不带 % 后的浮点数）、字符串。
```

# 诊断

所有工具在成功时返回状态码零，失败时返回非零。

# 环境变量

### `HOME`

如果调用了内部 readline shell，该目录包含 `.lvm_history`。

### `LVM_COMMAND_PROFILE`

用于 LVM 命令的默认命令配置名称。此配置可以通过直接使用 `--commandprofile` 命令行选项进行覆盖。

### `LVM_SYSTEM_DIR`

包含 `lvm.conf(5)` 和其他 LVM 系统文件的目录。默认认为 `/etc/lvm/`。

### `LVM_SUPPRESS_FD_WARNINGS`

抑制关于传递 LVM 的意外文件描述符的警告。

### `LVM_VG_NAME`

对于未指定路径的逻辑卷引用，假设卷组名称。默认不设置。

### `LVM_LVETAD_PIDFILE`

存储 lvmetad 进程 ID 的文件路径。

### `LVM_LVMETAD_SOCKET`

用于与 lvmetad 通信的套接字路径。

### `LVM_LVMPOLLD_PIDFILE`

存储 lvmpold 进程 ID 的文件路径。

### `LVM_LVMPOLLD_SOCKET`

用于与 lvmpolld 通信的套接字路径。

### `LVM_LOG_FILE_EPOCH`

附加到日志文件名后的3位字母字符串，随后是进程 ID 和时间戳。设置后，每个进程将记录到单独的文件。

### `LVM_EXPECTED_EXIT_STATUS`

进程退出时的预期状态。`">N"` 表示匹配大于 N 的任何状态。如果实际退出状态匹配生成的日志文件，则将其删除。

`LVM_LOG_FILE_EPOCH` 和 `LVM_EXPECTED_EXIT_STATUS` 允许自动化测试丢弃无关的日志数据。

### `LVM_SUPPRESS_LOCKING_FAILURE_MESSAGES`

用于已知配置锁定不可用时抑制警告消息。

### `DM_ABORT_ON_INTERNAL_ERRORS`

如果代码检测到非致命内部错误，则中止处理。

### `DM_DISABLE_UDEU`

避免与 udev 交互。LVM 将直接管理 `/dev` 中的相关节点。

## 文件

```
/etc/lvm/lvm.conf $HOME/.lvm_history
```

## 参见

`lvmconf(5)`, `lvmcache(7)`, `lvmthin(7)`, `lvmconfig(5)`, `lvmcache(7)`, `thinsetup(8)`, `thincreate(8)`, `lvcreate(8)`, `lvchange(8)`, `lvdisplay(8)`, `lvconvert(8)`, `lvactivate(8)`, `lvremove(8)`, `lvmerge(8)`, `lvextend(8)`, `lvresize(8)`, `vgmove(8)`, `vgremove(8)`, `vgresize(8)`, `vgcreate(8)`, `vgcreate(8)`, `vgchange(8)`, `vgdisplay(8)`, `vgconvert(8)`, `vgmove(8)`, `vgactivate(8)`, `vgremove(8)`, `vgmerge(8)`, `vgextend(8)`, `vgresize(8)`, `pvmove(8)`, `pvremove(8)`, `pvresize(8)`, `pvcreate(8)`, `pvchange(8)`, `pvdisplay(8)`, `pvconvert(8)`, `pvmove(8)`, `pvactivate(8)`, `pvremove(8)`, `pvmerge(8)`, `pvextend(8)`, `pvresize(8)`, `pscan(8)`, `vgscan(8)`, `pvscan(8)`, `thinsetup(8)`, `thincreate(8)`, `udev(7)`, `systemd(1)`, `systemd.target(5)`, `systemd.special(7)`

## 摘要

```
lvmconf [--disable-cluster] [--enable-cluster] [--enable-halvm] [--disable-halvm] [--file <configfile>] [--lockinglib <lib>] [--lockinglibdir <dir>] [--services] [--mirrorservice] [--startstopservices]
```

# or

`lvmconf` 是一个用于修改 lvm 配置文件中锁定配置的脚本。请参考 `lvm.conf(5)`。此外，如果需要，它还可以根据 lvm 配置的变化设置 Systemd 或 SysV 服务。

## 选项

### `--disable-cluster`

将 `locking_type` 设置为默认的非集群类型。还将将 `lvmetad use` 重置为默认值。

### `--enable-cluster`

将 `locking_type` 设置为本系统的默认集群类型。同时禁用 `lvmetad use`，因为集群环境尚未不支持。

### `--disable-halvm`

将 `locking_type` 设置为默认的非集群类型。还将将 `lvmetad use` 重置为默认值。

### `--enable-halvm`

将 `locking_type` 设置为适用于 HA LVM 的类型。同时禁用 `lvmetad use`，因为 HA LVM 环境尚未不支持。

### `--file <logfile>`

将更改应用于 `configfile` 而不是默认的 `/etc/lvm/lvm.conf`。

### `--lockinglib <lib>`

如果使用外部锁定类型，设置要加载的外部锁定库。

### `--lockinglibdir <dir>`

### `--services`

在设置 lvm 配置的同时，还启用或禁用相关的 Systemd 或 SysV clvmd 和 lvmetad 服务。此脚本不配置由集群资源代理提供的服务。

### `--mirrorservice`

在处理服务时，同时也启用或禁用可选的 `cm-irrod` 服务（仅适用于 `--services`）。

### `--startstopservices`

在启用或禁用相关服务的同时，立即启动或停止它们（仅适用于 `--services`）。

## 文件

`/etc/lvm/lvm.conf`

## 参见

`lvm(8)`, `lvm.conf(5)`

# LVMCONFIG

## 名称

`lvmconfig`, `svm dumpconfig`, `svm config` – 显示 LVM 配置

## 摘要

```
lvmconfig [-f|filename] [--type{current|default|diff|full|missing|new|profilable|profilable-metadata}] [--atversion version] [--ignoreadvanced] [--ignoreunsupported] [--ignorelocal] [-l|--list] [--config ConfigurationString] [--commandprofile ProfileName] [--profile ProfileName] [--metataprofile ProfileName] [--mergedconfig] [--showdeprecated] [--showunsupported] [--validate] [--withsummary] [--withcomments] [--withpaces] [--withversions] [ConfigurationNode...]
```

## 描述

`lvmconfig` 从 LVM 配置树生成格式化输出。该命令在 2.02.119 版本中引入，并具有相同的长形式 `lvm dumpconfig`。

## 选项

### `-f`, `--file filename`

将输出发送到名为‘filename’的文件。

### `-l`, `--list`

列出带有摘要注释的配置设置。这与使用 `lvmconfig --type list --summary` 相同。

### `--type {current|default|diff|full|missing|new|profilable|profilable-command|metadata}`

选择要显示的配置类型。显示的配置设置将根据所选类型分配默认值或当前使用的值。如果未选择类型，则默认使用 `--type current`。每当带有默认值的配置设置被注释掉时，意味着该设置没有定义任何具体的默认值。输出可以保存并用作标准的 `lvm.conf(5)` 文件。

#### current

显示当前的 lvmconf 配置，并合并了任何使用的 **tag config**。有关 LVM 配置方法的更多信息，请参阅 `lvm.conf(5)`。

#### default

显示所有分配了默认值的可能配置设置。

#### diff

显示所有值与默认值不同的配置设置。每个配置设置分配的值为当前使用的值。这实际上是极简 LVM 配置，可以在不改变当前配置行为的情况下使用。

#### full

显示所有配置设置。

#### missing

显示当前配置中缺失的配置设置。

#### new

显示当前 LVM 版本中引入的新配置设置。

#### profilable

显示可分析的配置设置。

#### profilable-command

显示可分析的命令设置。

#### metadata

显示与元数据相关的配置设置。

`--showdeprecated` 在输出中包含已弃用的配置设置。由于通过 `--atversion` 选项指定了具体版本，这些设置始终是已弃用的；如果指定的版本低于设置被弃用时的版本，则会自动包含已弃用设置。**current** 和 **diff** 类型默认会包含已弃用设置。

`--showunsupported` 在输出中包含不支持的配置设置。这些设置要么用于调试或开发目的，要么尚未完善，不应用于生产环境。**current** 和 **diff** 类型默认会包含不支持的设置。

`--validate` 验证当前配置并带有适当的退出码。要验证合并后的配置树，请使用 `--merged` 选项。即使禁用了 `lvm.conf(5)` 中的检查，也会进行验证。

`--withsummary` 为每个配置节点显示一行摘要注释。

`--withcomments` 为每个配置节点显示完整的注释。对于已弃用的设置，还会显示关于弃用的注释信息。

`--withpaces` 在适当的地方，在输出中添加更多空格以提高可读性。

`--withversions` 显示包含配置节点版本信息的注释。如果该设置已弃用，还会显示其弃用版本。

# 另请参

`lvm(8)` `lvmconf(8)` `lvm.conf(5)`

# LVDISKSCAN

## 名称

`lvmdiskscan` – 扫描所有 LVM 可见的设备

# 用法

```
lvmdiskscan [--commandprofile] [-d|debug] [-h|--help] [-l|lvpartition] [-v|--verbose]
```

## 描述

`lvmdiskscan` 扫描所有 SCSI、IDE 磁盘以及系统中的其他块设备以寻找 LVM 物理卷。报告的是实际设备大小。在 `lvm.conf` 中定义过滤器以限制扫描 CD-ROM 等磁盘。

## 选项

查看 `lvm(8)` 获取常用选项。

`-l,--lvpartition` 仅报告物理卷。

# 另请参

`lvm(8)`, `lvm.conf(5)`, `pvscan(8)`, `vgscan(8)`

# LVMDUMP

## 名称

`lvmdump` – 为诊断目的创建 LVM 信息转储

# 用法



```
lvmdump [-a] [-c] [-d directory] [-h] [-l] [-m] [-p] [-s] [-u]
```

## 描述

`lvdump` 是一个用于转储 LVM2 相关信息的工具。默认情况下，它创建一个适用于提交问题报告的压缩 tar 包。

tar 包的内容如下：

- `dmset` 信息
- 当前运行的进程表
- 来自 `/var/log/messages`（包含系统消息）
- 完整的 lvm 配置和缓存（来自 `/etc/lvm`）
- `/dev` 中的设备列表
- `/sys/block` 中的文件列表
- `/sys/devices/virtual/block` 中的文件列表
- 如果启用了 `-m`，包含元数据转储
- 如果启用了 `-a`，`vgscan`、`pvscan` 以及可用卷组、物理卷和逻辑卷的调试输出
- 如果启用了 `-c`，集群状态信息
- 如果启用了 `-l`，`lvmetad` 状态
- 如果启用了 `-p`，`lvmold` 状态
- 如果启用了 `-s`，系统信息和上下文
- 如果启用了 `-u`，`udev` 信息和上下文

## 选项

`-a` 高级收集。警告：如果 lvm 已经挂起，使用 `-a` 时脚本也可能挂起。

`-c` 如果 `lvmdump` 正在运行，也收集集群数据。

`-d directory` 将转储到目录而不是 tar 包：默认情况下，`lvmdump` 会产生包含所有信息的 tar 包。使用此选项可以指示其只产生根于目录的原始转储树。

`-h` 打印帮助消息。

`-l` 如果 `lvmetad(8)` 守护进程正在运行，包含当前存储在 `lmetad` 中的缓存信息：VG 元数据、PV 元数据以及这些元数据之间的各种映射。

`-m` 从 PVs 获取 LVM 元数据。此选项会对系统可见的所有 PV 的元数据区域生成 1:1 的转储，这会导致转储大小大幅增加。然而，元数据转储可能是宝贵的诊断资源。

`-p` 如果 `lvmpold(8)` 守护进程正在运行，包含守护进程正在监控的所有进行中的操作以及已完成轮询的部分历史。

`-s` 收集系统信息和上下文

`-u` 收集 `udev` 信息和上下文

## 环境变量

`LVM_BINARY`

使用的 lvm 二进制文件。默认为 `"lvm"`。

`DMSETUP_BINARY`

使用的 dmsetup 二进制文件。默认为 `"dmsetup"`。

## 另请参

`lvm(8)`

# LVMETAD

## 名称

`lvmetad` – LVM 元数据缓存

## 用法

```
lvmetad [-l {all|wire|debug}] [-p pidfile] [-s socket_path] [-f] [-V]
```

## 描述

`lvmetad` 守护进程缓存 LVM 元数据，以便 LVM 命令避免扫描。元数据缓存是一种优势，因为扫描非常耗时且可能干扰正常工作。`lvmetad` 本身并不读取元数据。`pvscan—cache` 命令扫描磁盘。系统中新增磁盘会被 `lvmetad` 自动更新。当从系统中移除磁盘时，必须运行 `pvscan—cache` 来更新缓存。如果不使用 `lvmetad`，LVM 命令将恢复为扫描。`lvmetad` 的启用/禁用由 `lvm.conf(5)` `global/uselvmad` 控制有关此设置的更多信息，请参见 `lvmconfig—withcomments` `global/uselvmad`

要在系统级别忽略 LVM 的磁盘（例如 lvmmetadata、pvscan），使用：`LVM.conf(5)` `global_filter`

## 选项

要在测试环境中运行守护进程，应从默认值修改 `pidfile_path` 和 `socket_path`。

`-f` 不派子进程，而在前台运行。

`-h`, `-?` 显示帮助信息。

`-l (all|wire|debug)` 选择要生成的日志消息类型。消息由 syslog 记录。此外，当给出 `-f` 时，消息也会发送到标准错误。从 0.02.98 版本开始，两者等同于逗号分隔的列表 `-l wire,debug`。在 0.02.98 版本之前，重复 `-d 1` 到 `3` 次（即 `-d, -dd, -ddd`）会增加消息的详细程度。

`-p pidfile_path` pid 文件的路径。这会覆盖内置默认值 (`/run/lvmetad.pid`) 和环境变量 `LVM_LVMAD_PIDFILE`。该文件用于防止同时运行多个守护进程实例。

`-s socket_path` socket 文件的路径。这会覆盖内置默认值 (`/run/Lvm/lvmetad.socket`) 和环境变量 `LVM_LVMAD_SOCKET`。为了与 `lvmetad` 成功通信，所有 LVM2 进程应使用相同的 socket 路径。

`-v` 显示 `lvmetad` 守护进程的版本。

## 环境变量

`LVM_LVVMETAD_PIDFILE`

pid 文件的路径。

`LVM_LVVMETAD_SOCKET`

socket 文件的路径。

## 参见

`lvm(8)`, `lvmconfig(8)`, `lvm.conf(5)`, `pvscan(8)`

# LVMPOLLD

## 名称

`lvmpold` – LVM 轮询守护进程

## 概要

```
lvmpoldd [-l|log {all|wire|debug}] [-p|pidfile pidfile_path] [-s|socket socket_path] [-B|binary lvm_binary_path] [-t|timeout timeout_value] [-f|foreground] [-h|help] [-V|version]
lvmpoldd [--dump]
```

## 描述

`lvmpold` 是 LVM 的轮询守护进程。该进程接收来自 LVM2 命令行工具的已初始化操作的轮询请求。轮询请求源于 `lvconvert`、`pvmove`、`lvchange` 或 `vgchange` LVM2 命令。

`lvmpold` 的目的是减少每个唯一轮询操作所产生的后台进程数量。理想应该只有一个。它还消除了外部因素导致后台进程意外终止的可能性。

只有当在 `lvm.conf(5)` 中通过指定 `global/use_lvmpold` 设置时，LVM 才会使用 `lvmpold`。如果 LVM 配置中未显式定义，则使用默认设置（参见 `lvmconfig` 的输出——输入 `default global/use_lvmpold` 命令）。

## 选项

要在测试环境中运行守护进程，应将 `pidfile_path` 和 `socket_path` 从默认值修改。

`-f`, `--foreground`

不派生，而在前台运行。

`-h`, `--help`

显示帮助信息。

`-l`, `--log {all|wire|debug}`

选择要生成的日志消息类型。消息通过 syslog 记录。此外，当使用 `-l` 时，消息也会发送到标准错误。共有两类消息：`wire` 和 `debug`。选择 `'all'` 会提供两种类型，并等同于逗号分隔的列表 `-l wire,debug`。

`-p`, `--pidfile pidfile_path`

pid 文件的路径。这会覆盖内置的 (`/run/lvmpoldd.pid`) 和环境变量 `LVMMPOLLD_PIDFILE`。此文件用于防止多个进程实例同时运行。

`-s`, `--socket_path`

socket 文件的路径。这会覆盖默认的 (`/run/lvm/lvmpold.socket`) 和环境变量 `LVMMPOLLD_SOCKET`。

`-t`, `--timeout timeout_value`

守护进程在空闲指定时间（秒）后可能会关闭。如果省略该选项或给定的值为零，则守护进程在空闲时不会关闭。

`-B`, `--binary svm_binary_path`

替代 LVM 二进制文件的可选路径（默认：`/usr/sbin/lvm`）。仅用于测试。

`-V`, `--version`

显示 `lvmpold` 守护进程的版本。

`--dump`

联系运行中的 `lvmpold` 守护进程以获取完整状态并以原始格式打印。

## 环境变量

`LVM_LVMPPOLLD_PIDFILE`

pid 文件的路径。

`LVM_LVMPPOLLD_SOCKET`

socket 文件的路径。

## 参见

`lvm(8)`, `lvm.conf(5)`

# LVMSADC

## 名称

`lvmsadc` – LVM 系统活动数据收集器

## 概要

`lvmsadc`

## 描述

`lvmsadc` 目前在 LVM2 下不支持。

## 参见

`lvm(8)`

# LVMSAR

## 名称

`lvmsar` – LVM 系统活动报告器

## 概要

```
lvmsar
```

## 描述

`lvmsar` 目前在 LVM2 下不支持。

## 参见

`lvm(8)`

# LVREDUCE

## 名称

`lvreduce` – 减小设备大小

## 概要

```
lvreduce [-A|autobackup {y|n}] [--commandprofile Name] [-d|debug] [-h|help] [-t|test] [-v|verbose] [-f|force] [-ndevsync]
```

## 参见

`fsadm(8)`, `lvchange(8)`, `lvconvert(8)`, `lvcreate(8)`, `lvxtend(8)`, `svm(8)`, `lvresize(8)`, `vgreduce(8)`

## 描述

`lvreduce` 允许你减小设备的大小。在未来的版本中，将支持缩小快照。在减小设备时要小心，因为可能会导致数据丢失。

## 选项

`-f,--force`

强制减小，即使可能导致数据丢失也不进行提示。

`-l,--extents`

以区（extents）为单位减小大小。

`-L,--size`

以字节为单位减小或设置大小。后缀 k 表示千字节，m 表示兆，g 表示吉，T 表示区的数量。

`-n,--fsck`

在调整文件系统大小时如果需要，则不执行 fsck。

`-nodevsync`

禁用 udev 同步。该进程将不会等待 udev 的通知。

`-r,--resize`

使用 `fsadm(8)` 调整底层文件系统的大小。

## 选项

常用选项请参阅 `lvm(8)`。

`-f`, `--force` 在不提示的情况下强制移除激活的逻辑卷。工具将尝试停用未使用的卷。若要对损坏的池继续操作，请使用 `-ff`

`--nodevsync` 禁用 udev 同步。进程将不会等待 udev 的通知。它将忽略后台任何可能的 udev 处理并继续运行。只有当 udev 未运行或具有忽略 LVM2 创建的设备的规则时，才应使用此选项。

## 示例

在不询问确认的情况下，移除卷组 `vg00` 中的激活逻辑卷 `lvol1`：

```
lvremove -f vg00/lvol1
```

移除卷组 `vg00` 中的所有逻辑卷：

```
lvremove vg00
```

## 另见

`lvcreate(8)`, `lvdisplay(8)`, `lvchange(8)`, `lvm(8)`, `lvs(8)`, `lvscan(8)`, `vgremove(8)`

# LVRENAME

## 名称

`lvrename` – 重命名逻辑卷

## 语法

```
lvrename [-A|autobackup {y|n}] [--profile ProfileName] [-d|debug] [-h|--help] [-t|test] [-v|verbose] [--version] [-f|force] [--noudevsync] {OldLogicalVolume{Name|Path} NewLogicalVolume{Name|Path} | VolumeGroupName OldLogicalVolume NewLogicalVolume}
```

`lvrename` 将现有逻辑卷从 `OldLogicalVolume{Name|Path}` 重命名为 `NewLogicalVolume{Name|Path}`。

## 选项

常用选项请参阅 `lvm(8)`。

`--nodevsync`

禁用 udev 同步。进程将不会等待 udev 的通知。它将忽略后台任何可能的 udev 处理并继续运行。只有当 udev 未运行或具有忽略 LVM2 创建的设备的规则时，才应使用此选项。

## 示例

将卷组 `vg02` 中的 `lvold` 重命名为 `lvnew`：

```
lvrename /dev/vg02/lvold vg02/lvnew
```

重命名此逻辑卷的另一种语法是：

```
lvrename vg02 lvold lvnew
```

## 另见

`lvm(8)`, `lvchange(8)`, `vgcreate(8)`, `vgrename(8)`

# LVRESIZE

## 名称

`lvresize` – 调整逻辑卷的大小

## 语法

```
lvresize [--alloc AllocationPolicy] [--nodedevs] [--commandprofile ProfileName] [-i|--stripes Stripes [-I|--stripes Stripe]] ([-l|--extents [+-] LogicalExtentNumber{%VG|LV|PVS][FREE|ORIGIN}] | [-L|--size [+-] LogicalVolumeSize{bBsSkKmMgGtpPeE}] [--poolmetadatasize [+]MetadataVolumeSize{bBsSkKmMgG}] [-f|--force] [-n|--nofck] [-r|--resizesfs] LogicalVolume{Name[:Path]} {PhysicalVolumePath[:PE[-PE]]...}
```

## 描述

`lvresize` 允许你调整逻辑卷的大小。在缩小逻辑卷大时要小心，因为缩小部分的数据将会丢失！！！因此，你应该确保先缩小卷上的任何文件系统，以确保要移除的区（extents）未被使用。同样支持调整快照逻辑卷的大小（参见 `lvcreate(8)` 获取有关创建快照的信息）。但若要更改镜像逻辑卷中的副本数量，请使用 `lvconvert(8)`。

## 选项

常用选项请参阅 `lvm(8)`。

`-f`, `--force` 在可能导致数据丢失时强制调整大小而不进行提示。

`-n`, `--nofck` 在文件系统需要检查时，在调整文件系统前不执行 fsck。你可能需要使用 `--force` 来执行此选项。

`-r`, `--resizesfs` 使用 `fsadm(8)` 在调整逻辑卷大小的同时调整文件系统。

`-l`, `--extents [+|-LogicalExtentNumber[%{VG|LV|PVS|FREE|ORIGIN}]`

以逻辑区为单位更改或规定逻辑大小。使用 + 或 - 符号，值将在逻辑卷的实际大小上增加或减少；如果不加符号，则值被视为绝对值。受影响的物理区总数将大于此值，例如，卷是镜像的。该数量也可以以卷组的百分比表示（后缀为 `%LV`）、逻辑卷剩余剩余的百分比表示（后缀为 `%PVS`）、卷组剩余空闲空间的百分比表示（后缀为 `%FREE`），或作为快照占逻辑卷总空间的百分比表示（后缀为 `%ORIGIN`）。结果值将向下取整，否则将向上取整。在未来的发行版本中，当以 PVS 或 FREE 的百分比表示时，该数字将被视为分配或释放的物理区的近似值（包括任何镜像使用的区）。目前代码可能会分配或移除比你预期的更多的空间。

`-l`, `--logicalSize[bBsSkKmMgGt]`

以兆字节为单位更改或规定逻辑大小。可选后缀 M（兆字节）、G（千字节）、T（太字节）、P（拍字节）和 E（艾字节）。带有 + 或 - 符号时，值将在逻辑卷的实际大小上增加或减少，并对齐到完整的逻辑区；如果不加符号，则值被视为绝对值。

`-i`, `--stripes`

给出扩展逻辑卷时使用的条带（stripes）数量。默认值为该逻辑卷使用的最后段。不适用于使用原始元数据的逻辑卷（LVs）。



给出扩展逻辑卷时使用的条带（stripes）数量。默认值为该逻辑卷使用的最后段。不适用于使用原始元数据的逻辑卷（LVs）。

`-i, --stripes`

给出扩展逻辑卷时使用的条带（stripes）数量。默认值为该逻辑卷使用的最后段。不适用于使用原始元数据的逻辑卷（LVs）。

`--poolmetadatasize[+]MetadataVolumeSize{bBsSkKmMgG}]` 更改或规定元数据卷的大小。带有 `+` 符号，值将在元数据卷的大小上增加；如果不加符号，则值被视为绝对值。

`-f, --force` 在可能导致数据丢失时强制调整大小而不进行提示。

`-n, --nofck` 在文件系统需要检查时，在调整文件系统前不执行 `fsck`。你可能需要使用 `--force` 来执行此选项。

`-r, --resizesfs` 使用 `fsadm(8)` 在调整逻辑卷大小的同时调整文件系统。

`-l, --extents [+|-LogicalExtentNumber[%{VG|LV|PVS|FREE|ORIGIN}]` 以逻辑区为单位更改或规定逻辑大小。使用 `+` 或 `-` 符号，值将在逻辑卷的实际大小上增加或减少；如果不加符号，则值被视为绝对值。受影响的物理区总数将大于此值，例如，卷是镜像的。该数量也可以以卷组的百分比表示（后缀为 `%LV`）、逻辑卷剩余的百分比表示（后缀为 `%PVS`）、卷组剩余空闲空间的百分比表示（后缀为 `%FREE`），或作为快照占逻辑卷总空间的百分比表示（后缀为 `%ORIGIN`）。结果值将向下取整，否则将向上取整。在未来的发行版本中，当以 PVS 或 FREE 的百分比表示时，该数字将被视为分配或释放的物理区的近似值（包括任何镜像使用的区）。目前代码可能会分配或移除比你预期的更多的空间。

`-l, --logicalSize[bBsSkKmMgGt]` 以兆字节为单位更改或规定逻辑大小。可选后缀 `M`（兆字节）、`G`（千字节）、`T`（太字节）、`P`（拍字节）和 `E`（艾字节）。带有 `+` 或 `-` 符号时，值将在逻辑卷的实际大小上增加或减少，并对齐到完整的逻辑区；如果不加符号，则值被视为绝对值。

`-i, --stripes` 给出扩展逻辑卷时使用的条带（stripes）数量。默认值为该逻辑卷使用的最后段。不适用于使用原始元数据的逻辑卷（LVs）。

卷类型：`(C)ache`（缓存）、`(M)irrored`（镜像）、`(M)irrored without initial sync`（无初始同步镜像）、`(o)rig`（原始）、`(R)origin with merging snapshot`（带合并快照的原始）、`(r)aid without initial sync`（无初始同步 RAID）、`(s)nap merging`（快照合并）、`(S)snapshot`（快照）、`(p)move`（移动）、`(v)irtual`（虚拟）、mirror or raid `(i)mage`（镜像或 RAID ）、mirror or raid `(I)image-out of sync`（不同步镜像）、mirror `(i)log device`（镜像日志设备）、under `(c)onversion`（转换中）、thin `(V)olume`（精简卷）、`(t)hin pool`（精简池）、`(T)hin pool data` 或 raid pool `(m)etadata` 或 pool metadata（元数据）。

权限：`(w)ritable`（可写）、`(r)ead-only`（只读）、非只读卷的只读激活

分配策略：`(a)nywhere`（随处）、`(c)ontiguous`（连续）、`(i)nherited`（继承）、`c(ling,(n)ormal`（如果卷当前锁定不允许分配更改，则显示为大写，例如在 `pmove(8)` 期间）。

固定 `(m)inor`（次号）

状态：`(a)ctive`（活动）、`(s)uspended`（挂起）、`(I)nvalid snapshot`（无效快照）、invalid `(S)uspended snapshot`（无效挂起快照）、snapshot `(m)erge failed`（快照合并失败）、suspended snapshot `(M)erge failed`（挂起快照合并失败）、mapped `(d)evice without tables`（无表的映射设备）、mapped device with `(i)active table`（有活动表的映射设备）、`(X) unknown device(o)pen`（未知打开设备）、`(X) unknown`

目标类型：`(C)ache,(m)irror,(r)aid,(s)nap,(hin),(u)known,(v)irtual`。这将与内核目标相关的逻辑卷分组。例如，镜像映像、镜像日志以及镜像本身，如果使用原始 device-mapper 镜像内核驱动程序，则显示为 `(m)`；而等同于 md 内核驱动程序的 RAID 则都显示为 `(r)`。使用原始 device-mapper 驱动程序的快照显示为 `(s)`；而使用新配额驱动程序的精简卷快照显示为 `(t)`。

新分配的数据块在使用前会被 `(z)eros` 覆盖。

卷健康状况：`(p)artial`（部分）、`(r)efresh needed`（需要刷新）、`(m)ismatches exist`（存在不匹配）、`(w)ritemost`（大部分写入）、`(X) unknown`（未知）。`(p)artition` 表示该逻辑卷使用的一个或多个物理卷系统中缺失。`(r)Refresh` 表示该 RAID 逻辑卷使用的一个或多个物理卷遭受了写入错误。该错误可能是由于该物理卷的临时故障，或表明其正在发生故障。应更换设备或替换。`(m)ismatches` 表示 RAID 逻辑卷某些部分不正确。通过对 RAID 逻辑卷启动“check”（检查）可以检测不一致性。可以通过 `(w)lvchange` 命令在 RAID 逻辑卷上执行清理、“check”和“repair”操作。`(w)ritemost`标识 RAID 1 逻辑卷中被标记为大部分写入的设备。

`s(k)ip activation`（跳过激活）：此卷被标记为激活期间被跳过。

`--sort` 用于排序的列逗号分隔列表。替换默认选择。在列名前加 `'-'` 可对该列进行反向排序。`--rows` 将列输出为行。`-S,--select` 只显示符合 Selection（选择）标准的行。所有行都会显示，并带有一个额外的“selected”列 `-o selected`，如果行匹配 Selection 则显示为 1，否则为 0。Selection 通过指定列名及其有效值（可包含预留值）并使用支持的比较操作符来定义。有关构建 Selection 标准的详细信息，请参见 `lvm(8)` 和 `-S, --select` 描述。要快速查看 Selection 可使用的完整列名列表（包括预留值列表和支持的选择操作符集），请检查 `lvs -S help` 命令的输出。`--segments` 使用强调段信息的默认列。`--separator` 用于分隔每列的字符串。如果需要正确 grep 这些列则很有用。`--unbuffered` 立即输出，而不进行排序或正确对齐列。`--units hHBssKmMgGtpEeE` 所有大小均以这些单位输出：`(h)human-readable`（人类可读）、`(b)bytes`（字节）、`(s)sectors`（扇区）、`(k)kilobytes`（千字节）、`(m)megabytes`（兆字节）、`(g)gigabytes`（吉字节）、`(t)terabytes`（太字节）、`(p)petabytes`（拍字节）、`(e)exabytes`（艾字节）。大写使用 1000 的倍数（S.I.）代替 1024。也可以指定自定义单位，例如`---units 3M ---unquoted` 与 `--nameprefix` 使用时，field=value 对中的值不加引号。

## 参见

`lvm(8)`, `lvdisplay(8)`, `pvs(8)`, `vgs(8)`

# LVSCAN

## 名称

`lvscan` – 扫描（所有磁盘）逻辑卷

## 概要

```
lvscan [-a|--all] [-b|--device] [--commandprofile ProfileName] [-d|--debug] [-h|--help] [--ignorelockingfailure] [-P|--partial] [-v|--verbose]
```

## 说明

`lvscan` 扫描系统中所有已卷组或所有支持的 LVM 块设备的逻辑卷。输出每个逻辑卷占一行，指示其是否活动、是否为快照或原始、设备的大小及其分配策略。使用 `lvs(8)` 或 `lvdisplay(8)` 获取有关逻辑卷的更全面信息。

## 选项

常用选项请参见 `lvm(8)`。

`--all` 包含逻辑卷信息，例如镜像，但无法访问。

`--blockdevice` 此选项现在被忽略。相反，使用 `lvs(8)` 或 `lvdisplay(8)` 获取设备。

`--cache` 仅在使用 `lvmetad` 时适用。只有在卷未被监控时才需要。

`--monitor` 当 RAID 卷降级时可以使用此项。

## 参见

`lvm(8)`, `lvcreate(8)`, `lvdisplay(8)`, `lvs(8)`

# MAKEDeltarpm

## 名称

`makedeltarp` - 从两个 rpm 创建 deltarp

## 概要

```
makedeltarp [-v] [-V version] [-z compression] [-m mbytes] [-s seqfile] [-r] [-u] oldrpm newrpm
makedeltarp [-v] [-V version] [-z compression] [-m mbytes] [-s seqfile] [-u] -p oldrpm patchrpm
```

## 说明

`makedeltarp` 从两个 rpm 创建一个 deltarp。该 deltarp 稍后可以从文件系统数据或旧 rpm 重建新 rpm。使用 `-v` 选项让 `makedeltarp` 的工作输出更详细（使用两次会更详尽）。

`Makedeltarp` 通常产生 V3 格式的 deltarp，如果需要，使用 `-V` 选项指定不同的版本。可以使用 `-z` 选项指定不同的压缩方法，默认使用与新 rpm 相同的压缩方法。

`-s` 选项让 `makedeltarp` 将序列 ID 写入指定的文件 `seqfile`。

如果你还修补 rpms，则应使用 `-p` 选项指定 `oldrpm` 的 rpm-print 和创建的 `patch rpm`。此选项告诉 `makedeltarp` 排除未包含在 `patch rpm` 中但在字节上与 `oldrpm` 中的文件不相同的文件。

`makedeltarp` 还可以通过添加 `-u` 切换创建“标识”（identity）deltarp。在这种情况下，只需指定一个 rpm。标识 deltarp 对于仅替换 rpm 的签名头或从文件系统重建 rpm 很有用。

## 内存考虑

`makedeltarp` 通常需要 rpm 未解压缩负载大小的三到到四倍。你可以使用 `-m` 选项启用需要 `mbytes` 内存的滑动块。这用内存使用换取创建的 `deltartpm` 的大小。此外，在使用此选项时，未压缩的 `deltartpm` 负载也存储在内存中，但在大多数情况下它通常很小。

## 另参见

`applydeltarpm(8)` `combineddeltarpm(8)`

## 作者

Michael Schroeder <mls@suse.de>

# MAKEDUMPFILE

## 名称

`makedumpfile` - 为 kdump 创建一个小型的转储文件

## 概要

```
makedumpfile [OPTION] [-x VMLINUX]-i VMCOREINFO VMCORE DUMPFILE
makedumpfile -F [OPTION] [-x VMLINUX]-i VMCOREINFO] VMCORE
makedumpfile [OPTION] -x VMLINUX [--config FILTERCONFIGFILE] [--epic EPICMACRO] VMCORE DUMPFILE
makedumpfile -R DUMPFILE
makedumpfile--split [OPTION] [-x VMLINUX]-i VMCOREINFO] VMCORE DUMPFILE1 DUMPFILE2 [DUMPFILE3 ..]
makedumpfile--reassemble VMCOREINFO-VMCORE -x VMLINUX
makedumpfile -E [--xen-syms XEN-SYMS]--xen-vmcoreinfo VMCOREINFO VMCORE DUMPFILE
makedumpfile--dumpdmesg [-x VMLINUX]-i VMCOREINFO] VMCORE LOGFILE
makedumpfile [OPTION] -x VMLINUX--diskset=VMCORE1--diskset=VMCORE2 [--diskset=VMCORE3 ..] DUMPFILE
makedumpfile -h
makedumpfile -v
```

## 描述

使用 kdump 时，第一个内核（称为“崩溃内核”）的 `/proc/vmcore` 镜像可以作为 `/proc/vmcore` 在在第二个内核（称为“kdump 内核”或“捕获内核”）运行时被获取。本文档代表 `/proc/vmcore` VMCORE。`makedumpfile` 通过排除分析中不需要的页面来压缩转储数据，创建一个小型 DUMPFILE；或者 `makedumpfile` 需要第一个内核的调试信息，通过分析第一个内核如何使用内存来区分不需要的页面。信息可以从 `VMLINUX` 或 `VMCOREINFO` 获取。

`makedumpfile` 在将 VMCORE 复制到 DUMPFILE 时，可以排除以下类型的页面，用户可以选择排除哪些类型的页面。

- 全零填充页
- 缓存私有页
- 所有带有私有页的缓存
- 用户进程页
- 空闲页

`makedumpfile` 提供两种 DUMPFILE 格式（ELF 格式和 kdump 压缩格式）。默认情况下，`makedumpfile` 创建 kdump 压缩格式的 DUMPFILE。kdump 压缩格式仅能用 crash 工具读取，并且由于支持压缩，它可以比 ELF 格式更小。ELF 格式可以使用 GDB 和 crash 工具读取。如果用户想使用 GDB，必须显式指定 DUMPFILE 格式为 ELF。

除了上述排除不需要的页面外，`makedumpfile` 还允许用户过滤目标内核。过滤器配置（filter config）可以使用错误命令语法来指定需要过滤的内核/模块符号及其成员。`makedumpfile` 读取过滤器配置并在处理过滤命令后构建内存地址及其大小的列表。需要过滤的内存位置将用字符 'X'（十六进制为 58）进行污染处理。文件格式请参阅 `makedumpfile.conf(5)`。



Epic 宏也可以用于指定需要过滤的内核符号及其成员。Epic 提供了 C 语义，包括语言结构（如条件语句、逻辑和算术操作、嵌套循环），用于遍历和擦除内核数据。`--epic` 需要 `epic_makedumpfile.so` 和 `epic` 库。`__makedumpfile.so` 可以从 `makedumpfile` 源码构建。参阅 `http://code.google.com/p/epic/` 以构建 `epic` 库 `libepepic.a` 并获取编写 `epic` 宏的更多信息。

为了分析第一个内核的内存使用，`makedumpfile` 可以引用包含第一个内核信息（结构大小、文件偏移等）的 `VMCOREINFO`，而 `VMCOREINFO` 足够小可以包含在第二个内核的 `initrd` 中。如果第二个内核在没有根文件系统的情况下在 `initrd` 上运行，`makedumpfile` 将无法引用 `VMLINUX` 来解决问题，`makedumpfile` 会预先 `VMCOREINFO`，并在第二个内核运行时引用 `VMCOREINFO` 而不是 `VMLINUX`。自 `linux-2.6.24` 起，`VMCORE` 已包含了 `VMCOREINFO`，用户不需要指定 `-x` 或 `-i` 。

如果第二个内核在没有挂载任何文件系统的 `initrd` 上运行，用户需要将转储数据传输到远程主机。要通过 `SSH` 传输转储数据，`makedumpfile` 将中间格式（扁平格式）的数据输出到标准输出。通过将输出数据管道到 `SSH`，用户可以将转储传输到远程主机。请注意，分析工具（5.1.2 之前的 `crash` 工具或 `GDB`）无法直接读取扁平格式，因此在远程主机上，接收到的扁平格式数据需要通过 `makedumpfile`（或 `makedumpfile-R.pl`）重新排列为可读的 `DUMPFILE` 格式。

`makedumpfile` 可以读取 `kdump` 压缩格式的 `DUMPFILE` 而不是 `VMCORE` 并重新过滤。此功能在用户需要通过 `ftp/scp/etc` 等减小 `DUMPFILE` 文件大小的情况下非常有用（如果原始 `DUMPFILE` 已经排除了由新 `dump_level` 指定的所有页面类型，则新 `DUMPFILE` 的级别将与原始 `DUMPFILE` 相同）。例如，`makedumpfile` 可以从如下 `dump_level` 中创建一个 `dump_level` 3 的 `DUMPFILE`：

示例：

```
# makedumpfile -c 3 /proc/vmcore dumpfile.1
# makedumpfile -c 3 dumpfile.2
```

`makedumpfile` 可以读取三种格式的 `VMCORE(s)`：单分区格式、磁盘格式和备份格式，并经过过滤和压缩处理将每一个转换为 `kdump` 压缩格式。请注意，对于由单个创建的 `VMCORE`，始终需要通过 `-x` 传递 `VMLINUX`。此外，要传递在磁盘配置上创建的多个 `VMCORE`，你需要使用 `disk` 选项。

## 选项

### `-c,-l,-p`

使用 `zlib`（`-c` 选项）、`lzo`（`-l` 选项）或 `snappy`（`-p` 选项）按页压缩数据。（`-l` 选项需要 `LZO=on`，`-p` 选项需要 `SNAPPY=on`）。用户无法通过 `-E` 选项指定此选项，因为 `ELF` 格式不支持压缩数据。示例： 
```
# makedumpfile -c 3 -x vmlinux/proc/vmfile
```

### `-d dump_level`

指定分析时不需要的页面类型。指定类型的页面将被排除在 `DUMPFILE` 中。用户可以通过设置 `dump_level` 中每个页面类型的总和来指定多个页面类型。`dump_level` 的最大值为 3。注意，在 `x86_64` 其他机器上，过滤的 `dump_level` 为 0 或 1。在 `x86_64` 机器上，如果通过 `-x` 指定 `domain-0` 的 `vmlinux`，即使是 2 或更大的 `dump level` 也是有效的。如果使用逗号 `','` 指定多个级别，`makedumpfile` 在遇到“设备空间不足”错误时将尝试用其他 `dump_level` 重试创建 `DUMPFILE`。例如，如果 `dump_level` 为 `"11,3"` `makedumpfile` 以 `dump_level` 11 重试，则 `makedumpfile` 将用 `dump_level` 重试。示例： 
```
# makedumpfile -d 11,3 -x vmlinux/proc/vmfile
```

| level | cache | dump | zero | user | free |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 0 | | | | | |
| 1 | X | | | | |
| 2 | | X | | | |
| 3 | X | X | | | |
| 4 | | | | X | |
| 5 | | | | | X |
| 6 | X | | | | |
| 7 | | X | | | |
| 8 | | | X | | |
| 9 | | | | X | |
| 10 | | | | | X |
| 11 | X | X | | | |
| 12 | | | | | | |
| 13 | | | | | | |
| 14 | | | | | | |
| 15 | | | | | | |
| 16 | | | | | | |
| 17 | | | | | | |
| 18 | | | | | | |
| 19 | | | | | | |
| 20 | | | | | | |
| 21 | X | X | | | | |
| 22 | | | | | | |
| 23 | | | | | | |
| 24 | | | | | | |
| 25 | | | | | | |
| 26 | | | | | | |
| 27 | | | | | | |
| 28 | | | | | | |
| 29 | | | | | | |
| 30 | | | | | | |
| 31 | | | | | | |

### `-E`

以 `ELF` 格式创建 `DUMPFILE`。此选项不能与 `-c` 选项或 `-l` 选项一同指定，因为 `ELF` 格式不支持压缩数据。示例： 
```
# makedumpfile -d 31 -x vmlinux/proc/vmfile
```

### `-f`

强制覆盖现有 `DUMPFILE`。示例： 
```
# makedumpfile -f 31 -x vmlinux/proc/vmcore dumpfile
```
该命令即使 `DUMPFILE` 已存在也会覆盖它。

### `-x VMLINUX`

指定带有调试信息的第一个内核 `VMLINUX` 以分析第一个内核的内存使用。如果 `VMCORE` 不包含 `VMCOREINFO`、未指定 `-i VMCOREINFO` 且 `dump_level` 为 2 或更大，则需要此选项。第一个内核和第二个内核的页大小应匹配。示例： 
```
# makedumpfile -d 31 -x vmlinux/proc/vmcore dumpfile
```

### `-i VMCOREINFO`

指定 `VMCOREINFO` 而不是 `VMCORE` 来分析第一个内核的内存使用。`VMCOREINFO` 预先通过 `makedumpfile` 的 `-g` 选项生成，包含了第一个内核的信息。如果 `VMCORE` 不包含 `VMCOREINFO`、未指定 `-x VMLINUX` 且 `dump_level` 为 2 或更大，则需要此选项。示例： 
```
# makedumpfile -d 31 -i vmcore/proc/vmfile
```

### `-g VMCOREINFO`

从带有调试信息的第一个内核 `VMLINUX` 生成 `VMCOREINFO`。`VMCOREINFO` 必须在运行第一个内核的系统上生成。通过 `-i` 选项，用户可以指定运行相同第一个内核的其他系统上生成的 `VMCOREINFO`。必须指定 `-x VMLINUX`。示例： 
```
# makedumpfile -g vmcoreinfo -x vmlinux
```

示例：`# makedupfile -F -d 31 -x vmlinux /proc/vmcore | ssh user@host`

`"cat > dumpfile.tmp # makedupfile -F -d 31 -x vmlinux /proc/vmcore | ssh user@host"makedupfile -R dumpfile" # makedupfile -E -d 31 -i vmcoreinfo /proc/vmcore | ssh user@host"makedupfile -R dumpfile" # makedupfile -F -E --xen-vmcoreinfo VMCOREINFO /proc/vmcore | ssh user@host"makedupfile -R dumpfile"`

## `-R`

将来自标准输入的扁平格式（flattened format）重新排列为正常的 `DUMPFILE`（可以使用分析工具读取）。示例：`# makedupfile -R dumpfile dumpfile.tmp # makedupfile -F -d 31 -x vmlinux /proc/vmcore | ssh user@host"makedupfile -R dumpfile"`

与其使用 `-R` 选项，不如 `perl` 脚本 `makedupfile-R.pl` 将扁平格式的转储数据重新排列为正常的 `DUMPFILE`，该 `perl` 脚本不依赖架构，且大多数系统都安装了 `perl`。即使远程主机没有 `makedupfile`，也可以通过运行此脚本在远程主机上将扁平格式的数据重新排列为可读的 `DUMPFILE`。示例：`# makedupfile -F -d 31 -x vmlinux /proc/vmcore | ssh user@host"makedupfile-R.pl dumpfile"`

## `-split`

将转储数据并行拆分为多个 `DUMPFILES`。通过在不同的存储设备上指定 `DUMPFILES`，设备可以与其他设备共享 `I/O`，从而减少保存转储数据的时间。每个 `DUMPFILE` 的小于系统内存除以 `DUMPFILES` 的数量。此功能目前支持 `kdump` 压缩格式。示例：`# makedupfile --split -d 31 -x vmlinux /proc/vmcore dumpfile12`

## `-reassemble`

将由 `-split` 选项创建的多个 `dumpfile` 合并为一个 `DUMPFILE`。将 `dumpfile12` 合并为 `dumpfile`。示例：`# makedupfile --reassemble dumpfile12 dumpfile`

## `-b <order>`

在写入输出 `DUMPFILE` 之前，在内存中缓存指定阶数的页。默认值为 4。

## `-cyclic-buffer size`

在循环模式（cyclic mode）下以 `KB` 指定缓冲区大小。在循环模式下，循环次数表示为：

```
num_of_cycles = memory_size / (buffer_size * page_size)
```

次数越少，预期速度越快。默认情况下，`buffer_size` 根据系统内存自动计算，因此普通用户不需要指定此选项。示例：`# makedupfile --cyclic-buffer 1024 -d 31 -x vuxuxproc/vmcore`

`--splitblocksizesize` 在带 `--split` 的循环模式下以 `KB` 指定 `splitblock` 大小。如果指定了 `--split N`，每个 `split dumpfile` 的最大为 `N KB`。示例：`# makedupfile --splitblock-size 1024 -d 31 -x vux/proc//corecore`

## `--non-cyclic`

以非循环模式运行，此模式使用旧过滤逻辑。如果你觉得循环模式太慢，请尝试此模式。示例：`# makedupfile --non-cyclic -d 31 -x vux/proc/vmcore`

## `--non-mmap`

如果支持 `mmap(2)`，则永远使用 `mmap(2)` 读取 `VMCORE`。通常，使用 `mmap(2)` 读取 `VMCORE` 更快，因此普通用户不需要指定此选项。示例：`# makedupfile --non-mmap -d 31 -x vux/proc/vmcore`

## `--xen-syms`

带有调试信息的 `XEN-SYMS` 以分析 `xen` 的内存使用。此选项提取 `xen` 和 `domain-0` 的部分。必须配合 `-E` 选项使用。示例：`# makedupfile -E --xen-syms xen-syms/proc/vmcore`

## `--xen-vmcoreinfo`

使用 `VMCOREINFO` 代替 `XEN-SYMS` 分析 `xen` 的内存使用。`VMCOREINFO` 应该由 `makedumpfile` 使用 `-g` 选项提前创建，并包含了 `xen` 的信息。必须配合 `-E` 选项使用。示例：`# makedupfile -E --xen-vmcoreinfo VMCOREINFO/proc/vmcore`

## `-X`

从 `Xen kdumps VMCORE` 中排除所有用户域页，提取 `xen` 和 `domain-0` 的部分。如果 `VMCORE` 包含 `Xen` 的 `VMCOREINFO`，则没有必要指定 `--xen-syms` 和 `--xen-vmcoreinfo`。必须配合 `-E` 选项使用。示例：`# makedupfile -E -X/proc/vmcore`

## `--xen_phys_start xen_phys_start_address`

此选项用于 `x86_64`。如果代码/数据是可重位的且 `VMCORE` 的 `CR` 寄存器中包含 `xen_phys_start_address`，则指定 `xen_phys_start_address`。示例：`# makedupfile -E -X/proc/vmcore --xen_phys_start 0x00000000 --xen_phys_start 0x10000000 --xen_phys_start 0x20000000 --xen_phys_start 0x30000000 --xen_phys_start 0x40000000 --xen_phys_start 0x50000000 --xen_phys_start 0x60000000 --xen_phys_start 0x70000000 --xen_phys_start 0x80000000 --xen_phys_start 0x90000000 --xen_phys_start 0xa0000000 --xen_phys_start 0xb0000000 --xen_phys_start 0xc0000000 --xen_phys_start 0xd0000000 --xen_phys_start 0xe0000000 --xen_phys_start 0xf0000000 --xen_phys_start 0x100000000 --xen_phys_start 0x200000000 --xen_phys_start 0x300000000 --xen_phys_start 0x400000000`

## `--message-level message_level`

指定 `message_level`。可以通过指定 `message_level` 来限制输出。注意默认值如下表所示：

| 进度 | 常见 | 错误 |
| :--- | :--- | :--- |
| 0 | | |
| 2 | | |
| 4 | | |
| 6 | | |
| 8 | | |
| 10 | | |
| 12 | | |
| 14 | | |
| 16 | | |
| 18 | | |
| 20 | | |
| 22 | | |
| 24 | | |
| 26 | | |
| 28 | | |
| 30 | | |

# 诊断

`makedumpfile` 以以下值退出。

**0** : `makedumpfile` 执行成功。

**1** : `makedumpfile` 失败，且并非下述原因。

**2** : `makedumpfile` 由于 `VMLINUX` 和 `VMCORE` 之间的版本不同而失败。

**3** : `makedumpfile` 由于内存分析错误而失败。

## 作者

由 `Masaki Tachibana` 和 `Ken’ichi Ohmichi` 编写。

## 参见

`crash(8)`, `gdb(1)`, `kexec(8)`, `makedumpfile.conf(5)`

# MANDB

# 节点

`mandb` - 创建或更新手册页索引缓存

# {览

```
mandb [-dqsucpt?V] [-C file] [manpath] mandb [-dqsut] [-C file] -f filename ...
```

## 描述

`mandb` 用于初始化或手动更新通常由 `man` 维护的索引数据库缓存。这些缓存包含了与手册页系统当前状态相关的信息，其中存储的信息被 `man-db` 工具用于以增强其速度和功能性。

在创建或更新索引时，`mandb` 会对错误的 `ROFF .so` 请求、虚的手的手页文件名以及无法解析 `whatis` 的手册页发出警告。

为 `mandb` 提供一个可选的冒号分隔路径将覆盖内部系统手册页层级搜索路径，该路径根据 `man-db` 配置文件中找到的信息确定。

# 数据库缓存

`mandb` 编译时可以支持以下数据库类型中的任一种。

| 名称 | 类型 | 异步文件名 |
| --- | --- | --- |
| Berkeley db | 二叉树 | 是 index.bt |
| GNU gdbm v >= 1.6 | 哈希表 | 是 index.db |
| GNU gdbm v < 1.6 | 哈希表 | 否 index.db |
| UNIX ndbm | 哈希表 | 否 index.dirdir |

那些支持异步更新的数据库类型提供了更快的速度，但代价是在发生异常终止时可能会发生损坏。在发生此类情况的异常情况下，可能需要使用 `-e` 选项重新运行 `mandb` 以从头创建数据库。

## 选项

- **-d**, --debug

  打印调试信息。

- **-q**, --quiet

  不产生警告。

- **-s**, --no-straycats

  不要花费时间查找或向数据库添加有关散乱猫的信息。



- `-p`, `--no-purge`

不要花费时间检查已删除的手册页并从数据库中清除。

- `-c`, `--create`

默认情况下，`mandb` 将尝试更新任何之前创建的数据库。如果数据库不存在，它将创建。此选项强制 `mandb` 删除之前的数据库并从头重新创建，并隐含 `no-purge`。如果数据库变得损坏或未来引入了新的数据库存储方案，这可能是必要的。

- `-u`, `--user-db`

创建用户数据库，即使具有创建系统数据库所需的写权限。

- `-t`, `--test`

对层级搜索路径中的手册页进行正确性检查。使用此选项，`mandb` 将不会更改现有数据库。

- `-f`, `--filename`

仅更新指定文件的条目。此选项不用于通用场景；它是 `man` 在编译时带有 `MAN_DB_UPDATES` 选项且发现页面过时时在内部使用的。它隐含 `-p` 并禁用 `-c` 和 `-s`。

- `-file`, `--config-file=file`

使用此配置文件而非默认的 `~/.manpath`。

- `-?`, `--help`

显示用法信息，然后退出。

- `-usage`

打印简短的用法信息并退出。

- `-V`, `--version`

显示版本，然后退出。

## 退出状态

- `0` - 执行成功。
- `1` - 用法错误或配置文件错误。
- `2` - 操作错误。
- `3` - 子进程失败。

# 统计信息

在构建数据库期间，可能会发出以下警告信息：

`<filename>`: whatis parse for page failed

尝试从给定的 `<filename>` 提取 whatis(s) 失败。这通常是由于手册页编写不当导致的，但如果输出了许多信息，很可能是系统中包含与 man-db 解析器不兼容的非标准页。参见 `manrog(1)` 中的 WHATIS PARSING 章节。

`<filename>`: is a dangling symlink

`<filename>` 不存在但被符号链接引用。通常会发出进一步的诊断信息以识别链接的 `<filename>`。

`<filename>`: bad symlink or ROFF request

`<filename>` 是指向不存在文件的符号链接，或包含指向该不存在文件的 ROFF include。

`<filename>`: bogus filename

`<filename>` 可能是也可能是有效的手册页，但其名称无效。这通常是因为扩展为 `<x>` 的手册页被放在了章节 `<y>` 中。

`<filename_mask>`: competing extensions

通配符 `<filename_mask>` 是唯一的。这通常是因为存在一个压缩和一个未压缩的版本。

## 文件

`/etc/man-db.conf`

`man-db` 配置文件。

`/var/cache/man/index.(bt|dir)`

FHS 标准索引缓存。

`/usr/man/index.(bt|dir)`

数据库缓存：

`/var/catman/index.(bt|dir)`

符合 FHS 标准的索引缓存。

## 参见

`manrog(1)`, `man(1)`, `manpath(5)`, `catman(8)`

手册页中的 WHATIS PARSING 章节。

## 作者

Wolf G. Taylor (`ford@surrey.ac.uk`). Fabrizio Polacco (`polacco@debian.org`). Colin Watson (`watson@debian.org`)。

# MAPSCRN

## 名称

`mapscrn` - 加载屏幕映射表

## 概要

```
mapscrn [-v] [-o map.orig] mapfile
```

## 描述

`mapscrn` 命令已过时 - 其功能已内置到 `setfont`。然而，为了向下兼容，它仍然作为一个单独命令可用。

`mapscrn` 命令将自定义字符映射表加载到控制设备。控制设备可以通过输出特殊的转义序列进入自定义映射模式。对于 G0 字符集使用 `<K`，对于 G1 字符集使用 `)K`。当给出 `-o` 选项时，旧映射将保存在 `map.orig`。

# 使用

有两种类型的映射表：直接到字体表（为每个字节提供字体位置）以及用户到 Unicode 表（为每个用户字节提供 Unicode 值）。相应的字形现在通过 Unicode 索引找到。

该命令

```
mapscrn trivial
```

设置一个一一对应的直接到字体表，用户字节直接访问字体。这对于字符集顺序相同的字体非常有用。类似

```
mapscrn 8859-2
```

的命令设置一个用户到 Unicode 表，假设用户使用 ISO 8859-2。

# 输入格式

`mapscrn` 可以按两种格式之一读取映射：

1. 256 或 512 字节二进制数据
2. 两列文本文件

格式 (1) 是翻译表的直接映像。256 字节表是直接到字体的，512 字节表是用户到 Unicode 的。格式 (2) 用于如下方式填充表：第一列提到的偏移量单元由第二列提到的值填充。当出现大于 255 的值或使用 `U+xxxx` 表示法编写值时，表被假设为用户到 Unicode 表，否则它是直接到字体的表。

文件中的值可以使用几种格式之一指定：

**1. 十进制：** 不以 `'0'` 开头的进制数字字符串。
**2. 八进制：** 以 `'0'` 开头的八进制数字字符串。
**3. 十进制：** 前带有 `"0x"` 的十六进制数字。
**4. Unicode：** 前带有 `"U+"` 的四个十六进制数字。
**5. 字符：** 包在单引号内的单个字符。（并使用二进制值。）注意空格、逗号、制表符和 `'#'` 无法使用这种格式指定。
**6. UTF-8 字符：** 包在单引号内的单个（可能是多字节的）UTF-8 字符。

## 文件

`/lib/kbd/consoletrans` 是屏幕映射的默认目录。

# 另请

`setfont(8)`

## 作者

Copyright (C) 1993 Eugene G. Crosser <crosser@pcc.msk.su> 此软件和文档可以自由分发。

# 主进程

## 名称

`master` - Postfix 主进程

## 概要

```
master [-Ddtvw] [-c config_dir] [-e exit_time]
```

## 描述

`master(8)` 守护进程是驻留进程，根据需要运行 Postfix 守护进程：通过网络发送或接收消息的守护进程、本地投递邮件的守护进程等。这些守护进程按需创建，每个服务的最大数量是可以配置的。

Postfix 守护进程会自愿终止，是在空置了配置的时间后，或者处理了配置数量请求后。此规则的例外是驻留队列管理器、地址验证服务器以及 TLS 会话缓存和伪随机数生成器。

`master(8)` 守护进程的行为由 `master.cf` 配置文件控制，见 `master(5)`。

选项：

- `-c config_dir`

在指定的目录中读取 `main.cf` 和 `master.cf` 配置文件，而不是默认配置目录。这将覆盖其他 Postfix 守护进程的配置文件。

- `-D`

初始化后，在 `master` 进程上运行调试器。调试命令通过 `main.cf` 全局配置中的 `debugger_command` 指定。

- `-d`

不要将 `stdin`、`stdout` 或 `stderr` 重定向到 `/dev/null`，并且不要丢弃控制终端。这仅用于调试。

- `-e exit_time`

在 `exit_time` 秒后终止 `master` 进程。子进程将在它们方便时终止。

- `-t`

测试模式。当 `master.pid` 锁文件不存在或该文件未锁定时，返回零退出状态。这证明 `master(8)` 守护进程未运行的证据。

- `-v`

为了调试目的启用详细日志。此选项将传递给子进程。多个 `-v` 选项会使软件的输出变得越来越详细。

- `-w`

在虚拟的前台进程中等待，同时真实的 `master` 守护进程在后台进程中初始化。只有当 `master` 守护进程初始化成功且在合理时间内完成时，虚拟前台进程才会返回零退出状态。

此功能在 Postfix 2.10 及更高版本可用。

信号：

# SIGHUP

接收到 HUP 信号后（例如在执行 `"postfix reload"` 后），`master` 进程重新加载其配置文件。如果服务已从 `master.cf` 文件中删除，其运行进程将立即终止。否则，允许运行进程在方便时终止，以便配置设置的变化仅影响新的服务请求。

# SIGTERM

接收到 TERM 信号后（例如在执行 `"postfix abort"` 后），`master` 进程将信号传递给其子进程并终止。这对于紧急关闭很有用。通常情况下只需终止主进程（`postfix stop`）并允许运行进程完成它们正在的操作即可。

# 诊断

问题将报告给 `syslogd(8)`。如果发生问题，退出状态为非零，包括在后台作为主守护进程初始化时发生的问题。

# 环境变量

`MAIL_DEBUG`

初始化后，按照 `main.cf` 配置文件中 `debugger_command` 参数指定的启动调试器。

`MAIL_CONFIG`

包含 Postfix 配置文件的目录。

# 配置参数

与大多数 Postfix 守护进程不同，`master(8)` 服务器不会自动获取 `main.cf` 的更改。`master.cf` 的更改绝不会自动获取。在更改配置后使用“`postfix reload`”命令。

# 资源和速率控制

`default_process_limit (100)`

Postfix 进程的默认数量。

`max_idle (100)`

空闲服务在终止前等待的时间。

`max_use (100)`

服务将限制的传入连接的最大数量。

`throttle_time (60s)`

`master` 在 `fork` 之前等待的时间。

在 Postfix 版本 2.6 中可用：

`service_disable (empty)`

按类型或名称选择性地禁用服务。

# 其他控制

`config_directory`

`main.cf` 和 `master.cf` 文件的位置。

`debugger_command (empty)`

指定时执行的外部命令。

`inet_interfaces (all)`

Postfix 接收连接的网络接口。

`inet_protocols (all)`

`master` 将导入的 Internet 协议。

`process_id (只读)`

`master` 的进程 ID。

`process_name (只读)`

`master` 的进程名。

`queue_directory (只读)`

队列目录。

`syslog_facility (mail)`

`master` 的 syslog 设施。

`syslog_name (见 ‘postconf -d’)`

附加在前面的系统名称，例如“`smtpd`”。

## 文件

使用命令“`postconf -d`”将以下名称扩展为实际值：

`main.cf`, `master.cf`, `master.pid`, `master.lock`。

# 另请

`qmgr(8)`, `address verify(8)`, `master(5)`, `main.cf`, `syslogd(8)`, `system logging`

# 许可证

必须随此软件分发 Secure Mailer 许可证。

## 作者

Wietse Venema IBM T.J. Watson Research P.O. Box 704 Yorktown Heights, NY 10598, USA

# matchpathcon

## 名称

`matchpathcon` - 从文件上下获取指定路径的 SELinux 安全上下文

## 概要

```
matchpathcon [-V] [-N] [-n] [-m type] [-f file_contexts_file] [-p prefix] [-P policy_root_path] filepath...
```

## 描述

`matchpathcon` 查询系统策略并输出与 `filepath` 关联的默认安全上下文。

注意：相同的路径可能有不同的安全上下文，取决于文件类型（普通文件、目录、链接文件、字符文件 ...）。

如果文件存在，`matchpathcon` 在确定默认安全上下文还会考虑文件类型。如果文件不存在，则不会发生文件类型匹配。

## 选项

`-m type`

强制指定查找的文件类型。有效类型为 `file, dir, chr_file, blk_file, lnk_file, sock_file.`

`-n`

不显示路径。

`-N`

不使用翻译。

`-f file_contexts_file`

使用备用的 `file_contexts_file`

`-p prefix`

使用前缀加速翻译

`-P policy_root_path`

使用备用的策略根路径

`-V`

验证磁盘上的文件上下文是否与默认值匹配

## 作者

本手册页由 Dan Walsh <dwalsh@redhat.com> 编写。

## 参见

`selinux(8)`, `matchpathcon(3)`

# MDADM

## 名称

`mdadm` - 管理 MD 设备*又称* 软件 RAID

```
mdadm [mode] <raiddevice> [options] <component-devices>
```

## 描述

RAID 设备是由两个或多个物理设备创建的虚拟设备。这允许将多个设备（通常是磁盘驱动器或其分区）合并为一个设备，用于存储单个文件。某些 RAID 级别包含冗余，能够应对某种程度的设备故障。

Linux 软件 RAID 通过 `md`（多设备）驱动程序实现。

目前，Linux 支持 LINEAR 设备、RAID0（条带）、RAID1（镜像）、RAID4, RAID5, RAID6, RAID10、MULTIPATH、FAULTY 和 CONTAINER。

MULTIPATH 并不是软件 RAID 机制，但它涉及多个设备：每个设备都是通往一个物理存储设备的路径。新安装不应使用 `md/multipath`，因为它支持得良好且没有持续开发。请改用基于 Device Mapper 的 `multipath-tools`。

FAULTY 也不是真正的 RAID，它只涉及一个设备。它在真实设备之上提供了一个层，可用于注入故障。

CONTAINER 则完全不同。CONTAINER 是一组设备，它们被作为一个集合进行管理。这类似于连接到硬件 RAID 控制器的设备集。该设备集可能包含多个 RAID 阵列，每个阵列利用集合中若干个设备的某些（或全部）区块。例如，5 个设备集中的两个设备可以使用整个设备形成一个 RAID1。剩余的三个设备可能在每个设备的前半部分形成一个 RAID5，在后半部分形成一个 RAID0。

对于 CONTAINER，有一份元数据描述了容器中的所有的阵列。因此，当 `mdadm` 创建一个 CONTAINER 设备时，该设备仅代表元数据。其他普通阵列（如 RAID1 等）可以在容器内部创建。

## 模式

`mdadm` 有几种主要的操作模式：

### Assemble（组装）

将之前创建的阵列的组件组装为活动阵列。可以显式给出组件，也可以进行搜索。`mdadm` 会检查组件是否形成了一个可靠阵列，并根据请求修改超级块信息以组装故障阵列。

### Build（构建）

构建一个没有设备级元数据（超级块）的阵列。对于这类阵列，`mdadm` 无法区分初始创建和随后的阵列组装。它无法执行任何检查是否请求合适的组件。因此，Build 模式应仅在完全理解所操作的情况下使用。

### Create（创建）

创建一个带有设备级元数据（超级块）的新阵列。适当的元数据会被写入每个设备，然后激活由这些设备组成的阵列。启动 'resync'（同步）过程以确保阵列的一致性（例如，镜像的两侧包含相同的数据），但设备的内容保持不变。阵列一旦创建即可使用，无需等待同步完成。

### Follow or Monitor（跟踪或监控）

监控一个或多个 md 设备并对任何状态变化采取行动。这对于 RAID1, 4, 5, 6, 10 或 multipath 阵列才有意义，因为它们只有这些有意义的状态。RAID0 或 Linear 永远不会缺失、备用或损坏驱动器，因此没有可监控的内容。

### Grow（扩展）

扩展（或缩小）阵列，或以其他方式对其进行重构。目前支持的增长选项包括更改组件设备的活动大小、更改 Linear 和 RAID 0/1/4/5/6 级别中活动设备的数量、更改 0, 1, 5 和 6 之间的 RAID 级别、更改 RAID 0,4,5,6,10 的大小和布局，以及添加或删除写入意图位图。

### Incremental Assembly（增量组装）

向相应的阵列添加单个设备。如果添加设备后阵列可以启动。这将为热插系统提供了一个方便的接口。当检测到每个设备时，`mdadm` 有机会将其包含在某些阵列中。可选地，当传递 `--fail` 标志时，我们将设备从任何活动阵列中移除而不是添加。

如果在此模式下向 `mdadm` 传递 CONTAINER，则该容器内的任何阵列都将被组装并启动。

### Manage（管理）

用于对阵列的特定组件进行操作，例如添加新备用设备和移除故障设备。

### Misc（杂项）

这是一个“其他”模式，支持对活动阵列的操作、对组件设备的操作（如擦除旧超级块）以及信息收集操作。

### Auto-detect（自动检测）

此模式不对特定设备或阵列操作，而是请求 Linux 内核激活任何自动检测的阵列。

## 选项

## 选择模式的选项：

- `--assemble`: 组装已存在的阵列。
- `--build`: 构建没有超级块的阵列。
- `--create`: 创建新阵列。
- `--monitor`: 监控模式。
- `--grow`: 更改活动阵列的大小或形状。
- `--incremental`: 从相应的阵列中添加/移除设备。
- `--auto-detect`: 请求内核启动任何自动检测的设备。

## 不特定于模式的选项：

- `-h`, `--help`: 显示通用帮助信息或在执行上述某个选项后显示模式特有的帮助信息。
- `--help-options`: 显示关于命令行解析和某些常用选项的更详细帮助。



`-V`, `--version`: 打印 `mdadm` 版本信息。

`-v`, `--verbose`: 详细说明发生的情况。可以使用两次来增加详细程度。额外的详细性目前影响 `--detail` `--scan`。

`-q`, `--quiet`: 避免纯信息性消息。使用此项，除非有重要报告，否则 `mdadm` 将保持静默。

`-f`, `--force`: 对某些操作强制执行。请查看各种模式下此选项在不同上下文中的具体含义。

`-c`, `--config=`: 指定配置文件或目录。默认使用 `/etc/mdadm.conf` 和 `/etc/mdadm.conf.d`，如果缺失则使用 `/etc/mdadm/mdadm.conf` 和 `/etc/mdadm.conf.d`。如果指定的配置文件是 `partitions`，则不读取任何内容，`mdadm` 将认为文件仅包含 `DEVICE` 分区，并读取 `/proc/partitions` 查找扫描设备列表，读取 `/proc/mdstat` 查找要枚举的容器列表。如果给出的配置文件为 `none`，`mdadm` 将像文件为空一样操作。如果给出目录名称，`mdadm` 将收集目录中所有以 `.conf` 结尾的文件，按字母顺序排序，并将所有这些文件作为配置文件处理。

`-s`, `--scan`: 扫描配置文件或 `/proc/mdstat` 以查找缺失信息。通常，此选项允许 `mdadm` 从配置获取任何缺失信息，如组件设备、阵列设备告警目标；一个例外是 `MISC` 使用 `--detail` `--stop` 时，此时 `--scan` 表示从 `/proc/mdstat` 获取阵列设备列表。

`-e`, `--metadata=`: 声明使用的 RAID 元数据（超级块）样式。对于 `--create`，默认值为 `1.2`，对于其他操作则猜测。可以通过设置覆盖默认值

`mdadm.conf` 中 `CREATE` 关键字的元数据值。

可选项有：

- `0`, `0.90`，默认
- `0`, `0.90`

使用原始的 `0.90` 格式超级块。该格式将数组限制为 28 个组件设备，并将级别为 级及以上的组件设备限制为 2 ter字节。如果分区在 64K 边界处起始，可能会产生超级块是适用于整个设备还是仅适用于最后一个分区的疑惑。

- `1`, `1.0`, `1.1`, `1.2`
- `1`, `1.0`, `1.1`, `1.2` 默认

使用新版本的格式超级块。这种格式的限制更少。它可以轻松地在不同字节序的主机之间移动，并且恢复操作可以检查点并恢复。不同的子版本将超级块存储在设备的不同位置：末尾（针对 `1.0`）、开头（针对 `1.1`）或从起始 4K 处（针对 `1.2`）。“1”等同于“1.2”。“default”等同于“1.2”。

使用 SNIA 定义的“行业标准”DDF（磁盘数据格式）格式。创建时将创建一个 DDF CONTAINER，并可以在该容器中创建普通数组。

使用 Intel(R) Matrix Storage Manager 元数据格式。这会创建一个以类似于 DDF 的方式管理的 CONTAINER，并在某些平台上通过 `option-from` 选项支持：

`http://www.intel.com/design/chipsets/matrixstorage_sb.htm`

`--homehost`：这将覆盖配置文件中的任何 `HOMEHOST` 设置，并提供应被视为任何数组主节点的主机标识。

在创建数组时，`homehost` 将记录在元数据中。对于版本-1 的超级块，它将作为前缀放在数组名前。对于版本-0.90 的超级块，主机名的 SHA1 哈希值的部分部分将存储在 UUID 的后半部分。

在报告数组信息时，任何标记为给定 `homehost` 的数组都将进行此类报告。

在使用自动组装时，只有标记为给定 `homehost` 的数组才允许使用“local”名称，即不以“_”后跟数字字符串结尾。请参见下方 Auto-Assembly 部分。

`--prefer`：当 `mdadm` 需要打印找到设备的名称时，它会在 `/dev` 中查找指向该设备且最短的名称。如果在使用 `/dev` 的同时提供了路径组件，`mdadm` 将优先选择包含该组件的名称。例如，`--prefer=by-uuid` 将优先选择 `/dev` 下名为 `by-uuid` 子目录中的名称。

此功能目前仅由 `--detail` 和 `--monitor` 提供。

### 用于 CREATE、BUILD 或 GROW：

`-n`, `--raid-devices=`: 指定数组中活动设备的数量，该数量加上备用设备的数量必须等于命令行 `--create` 中列出的组件设备数量。将值设置为 1 可能是一个错误，因此通常需要先指定 `--force`。随后将允许为线型、多路径、RAID0 和 RAID1 使用值 1。RAID4、RAID5 或 RAID6 不允许。此数字只能对 RAID1、RAID4、RAID5 和 RAID6 数组通过 `--grow` 更改，且仅在提供必要支持的内核上进行。

`-x`, `--spare-devices=`: 指定初始数组中备用设备的数量。备用设备以后也可以添加和删除。命令行列出的组件设备数量必须等于 RAID 设备的数量加上备用设备的数量。

`-z`, `--size=`: 在 RAID 级别 1/4/5/6 中从每块驱动器使用的空间，单位为 Kibibytes。这必须是块大小的倍数，并且必须在驱动器末尾留出约128Kb 的空间用于 RAID 超级块。如果没有指定，则由最小设置大小，如果驱动器之间的差异大于 1，会发出警告。

可以给出 `'M'` 或 `'G'` 后缀分别表示兆字节或千字节。有时替换设备会比原始设备小一点，尽管根据 IDEMA 标准这种情况应降至最低。`md` 将拒绝替换驱动器。为了防止这种情况，将初始大小设置得比设备略小可能有用。

对于基于 CONTAINER 的 RAID 级别 1/4/5/6 数组，可以使用 `--grow` 设置此值，因为带有 IMSM 元数据的数组可能无法支持此项。如果数组是用比活动设备更小的尺寸创建的，可以使用 `--grow` 访问该空间。大小可以指定为 `max`，意味着选择适合所有设备的最大尺寸。

在缩小数组大小之前，您应该确保不需要该空间。如果设备持有文件系统，您需要调整文件系统大小以使用空间。

缩小数组大小后，您应该检查设备中存储的数据仍然可用。如果设备持有文件系统，则对文件系统进行“fsck”是最低要求。如果出现问题，可以通过另一个 `--grow` `--size=` 命令重新创建数组而不丢失数据。

`-Z`, `--size=`: 对于基于 CONTAINER 的 RAID 级别 1/4/5/6 数组，可以使用 `--grow` 设置此值，因为带有 IMSM 元数据的数组可能无法支持此项。如果数组是用比活动设备更小的尺寸创建的，可以使用 `--grow` 访问该空间。大小可以指定为 `max`，意味着选择适合所有设备的最大尺寸。

在缩小数组大小之前，您应该确保不需要该空间。如果设备持有文件系统，您需要调整文件系统大小以使用空间。

缩小数组大小后，您应该检查设备中存储的数据仍然可用。如果设备持有文件系统，则对文件系统进行“fsck”是最低要求。如果出现问题，可以通过另一个 `--grow` `--size=` 命令重新创建数组而不丢失数据。

`-C`, `--chunk=`: 指定以 kibibytes 为单位的块大小。用于 RAID4、RAID5 和 RAID6。块大小必须是 2 的幂。默认值为 64K。

`-l`, `--level=`: 设置数组的 RAID 级别。支持的级别有 `0`, `1`, `2`, `4`, `5`, `6`, `linear`, `multipath`。

`-p`, `--layout=`: 设置数组的布局。支持的布局有左异步、左对称、右异步、右对称、镜像。

`-m`, `--metadata=`: 设置数组使用的元数据类型。支持的类型有 DDF、IMSM 和 `none`。

`-n`, `--name=`: 设置数组的名称。

`-r`, `--rounding=`: 设置数组的对齐因子。

`-s`, `--size=`: 设置数组的大小。

`-w`, `--spare=`: 设置数组中备用设备的数量。

`-Z`, `--size=`: 设置数组的大小。

`f` 信号表示‘far’副本。更多详情参见 `md(4)` 中的‘near’‘offset’和‘far’。

数字是每个数据块的副本数量。2 是正常的，3 可能很有用。这个数字可以等于数组中的设备数量。它不需要能整除该数字，例如，对于具有奇数个设备的数组，使用‘n2’也是完全合法的。

当数组在 RAID5 和 RAID6 之间转换时，会使用一个中间 RAID6 布局，其中第二个部分块 `Q` 始终位于最后一个设备上。要将 RAID5 转换为 RAID6 并保留在此新布局中，请使用 `--layout=preserve`。这会尝试避免任何重条带。

此 `--layout=normalise` 的反向操作会将非标准的 RAID6 布局转换为更标准的排列。

与 `--layout` 相同。

### `-b`, `--bitmap=`

指定一个用于存储写入意图位图的文件。除非给出 `force` 参数，否则该文件不应存在。组装数组时应提供相同的文件。如果给出单词 `internal`，则位图将存储在数组的元数据中，并在所有设备上复制。当给出单词 `none` 且处于 `--grow` 模式时，将删除任何存在的位图。

为了帮助捕捉拼写错误，如果文件名是真实文件，则必须包含至少一个斜杠 `'/'`。

注意：外部位图已知仅在 ext2 和 ext3 上有效。在其他文件系统上存储位图文件可能会导致严重问题。

在 100G 或更大的设备上创建数组时，`mdadm` 会自动添加内部位图。可以通过 `--bitmap-chunk=` 抑制。

设置位图的块大小。每个位对应千字节的存储。使用文件位图时，默认使用至少为 4 且需要超过 2^21 个块的最小大小。使用内部位图时，`chunksize` 默认为 64Meg，如果需要为了将位图放入可用空间，则会更大。

可以使用后缀‘M’或‘G’分别表示兆字节或吉字节。

`-W`, `--write-mostly`: 在 `--build`、`--create` 或 `--add` 命令列出的后续设备将被标记为‘write-mostly’。这仅对 RAID1 有效，意味着‘md’驱动程序将尽可能避免从这些设备读取数据。这在通过慢速链路进行镜像时可能很有用。

`--write-behind=`: 指定启用后写模式，仅对 RAID1 有效。如果指定了参数，将设置允许的最大未完成写入数。默认值为 256。使用 write-behind 模式需要写入意图位图，且仅在标记为 write-mostly 的驱动器上尝试 write-behind。

告诉 `mdadm` 数组已存在且已知是干净的。这在从重大故障中恢复时非常有用，因为你确定除非实际向数组写入数据，否则数据不会受到影响。在创建 RAID1 或 RAID10 时，如果你想避免初始同步，也可以使用它。然而，这种做法虽然通常是安全的，但不建议这样做。

当将成为新数组部分的设备被填充为零时，操作员知道数组实际上是干净的。如果是这种情况，例如在运行 `badblocks` 后，可以使用此参数来告诉 `mdadm` 操作员已知的事实。

当使用 `--grow` `--size=` 将数组调整为更大的尺寸时，新空间的同步方式通常与创建时同步整个数组的方式相同。从 Linux 3.0 版本开始，可以在命令中配合 `--assume-clean` 来避免自动同步。

`--backup-file=`: 这是一个备份文件。

此项用于：当数组在 RAID5 和 RAID6 之间转换时，会使用一个中间 RAID6 布局，其中第二个部分块 `Q` 始终位于最后一个设备上。要将 RAID5 转换为 RAID6 并保留在此新布局中，请使用 `--layout=preserve`。这会尝试避免任何重条带。

此 `--layout=normalise` 的反向操作会将非标准的 RAID6 布局转换为更标准的排列。

与 `--layout` 相同。

`f` 信号表示‘far’副本。更多详情参见 `md(4)` 中的‘near’‘offset’和‘far’。

数字是每个数据块的副本数量。2 是正常的，3 可能很有用。这个数字可以等于数组中的设备数量。它不需要能整除该数字，例如，对于具有奇数个设备的数组，使用‘n2’也是完全合法的。



当数组在 RAID5 和 RAID6 之间转换时，会使用一个中间 RAID6 布局，其中第二个部分块 (Q) 始终位于最后一个设备上。要将 RAID5 转换为 RAID6 并保留在此新布局中（这不需要重新条带化），请使用 `--layout=preserve`。这会尝试避免任何重条带。

此 `--layout=normalise` 的反向操作会将非标准的 RAID6 布局转换为更标准的排列。

与 `--layout` 相同（因此解释了 -p 中的 p）。

## `-b, --bitmap=`

指定一个用于存储写入意图位图（write-intent bitmap）的文件。除非给出 force 参数，否则该文件不应存在。组装数组时应提供相同的文件。如果给出单词 `internal`，则位图将存储在数组的元数据中，并在所有设备上复制。当给出单词 `none` 且处于 `--grow` 模式时，将删除任何存在的位图。

为了帮助捕捉拼写错误，如果文件名是真实文件（`internal` 或 `none`），则必须包含至少一个斜杠 (`/`)。

注意：外部位图已知仅在 ext2 和 ext3 上有效。在其他文件系统上存储位图文件可能会导致严重问题。

在 100G 或更大的设备上创建数组时，`mdadm` 会自动添加内部位图，因为这通常是有益的。可以通过 `--bitmap-chunk=` 抑制。

设置位图的块大小（chunksize）。每个位对应千字节的存储。使用文件位图时，默认使用至少为 4 且需要超过 2^21 个块的最小大小。使用内部位图时，chunksize 默认<|message|>为 64Meg，如果需要为了将位图放入可用空间，则会更大。

可以使用后缀 `M` 或 `G` 分别表示兆字节（Megabytes）或吉字节（Gigabytes）。

`-W, --write-mostly` 在 `--build`、`--create` 或 `--add` 命令列出的后续设备将被标记为 `write-mostly`。这仅对 RAID1 有效，意味着 `md` 驱动程序将尽可能避免从这些设备读取数据。这在通过慢速链路进行镜像时可能很有用。

## `--write-behind=`

指定启用后写（write-behind）模式（仅对 RAID1 有效）。如果指定了参数，将设置允许的最大未完成写入数。默认值为 256。使用 write-behind 模式需要写入意图位图，且仅在标记为 write-mostly 的驱动器上尝试 write-behind。

告诉 `mdadm` 数组已存在且已知是干净的（clean）。这在从重大故障中恢复时非常有用，因为你确定除非实际向数组写入数据，否则数据不会受到影响。在创建 RAID1 或 RAID10 时，如果你想避免初始同步，也可以使用它。然而，这种做法虽然通常是安全的，但不建议这样做。这只有在你清楚自己在做什么时才有用。

当将成为新数组部分的设备被填充为零时，操作员知道数组实际上是干净的。如果是这种情况（例如在运行 `badblocks` 后），可以使用此参数来告诉 `mdadm` 操作员已知的事实。

当使用 `--grow --size=` 将数组调整为更大的尺寸时，新空间的同步方式通常与创建时同步整个数组的方式相同。从 Linux 3.0 版本开始，可以在命令中配合 `--assume-clean` 来避免自动同步。

## `--backup-file=`

## 用于组装 (ASSEMBLE):

- `-u, --uuid=`

要装数组的 uuid。不包含此 uuid 的设备将被排除。

- `-m, --super-minor=`

创建数组时对应的设备次设备（Minor）。不包含此次设备数的设备将被排除。如果你创建了一个数组 `/dev/md1`，那么所有超级块（superblocks）将包含设备设备 1，即使该数组随后被组装为 `/dev/md2`。

为 `--super-minor` 传递字面量 `dev` 将使 `mdadm` 使用正在组装的 md 设备的编号。例如，在组装 `/dev/md0` 时，`--super-minor-dev` 将查找次设备号为 0 的超级块。

`--super-minor` 仅适用于 v0.90 元数据，通常不应使用。使用 `--uuid` 要安全得多。

- `-N, --name=`

指定要组装数组的名称。这必须是创建数组时指定的名称。它必须与超级块中存储的名称完全匹配，或者与以当前主机（homehost）为前缀的给定名称匹配。

- `-f, --force`

即使某些设备上的元数据看起来已过时，也组装数组。如果 `mdadm` 无法找到启动数组的正常设备，但可以找到某些记录为失败的设备，它会将这些设备标记为正常，以便启动数组。需要 `--force` 才能启动的数组可能包含数据损坏。请谨慎使用。

- `-R, --run`

如果提供的驱动器数量少于数组上次活动时存在的数量，则尝试启动数组。通常情况下，如果没有找到所有预期的驱动器且没有使用 `--scan`，数组将会被组装但不会启动。使用 `--run` 后将会尝试启动。

- `--no-degraded`

这是 `--run` 的反向，它在所有预期驱动器未就绪的情况下抑制数组的启动。这仅在配合 `--scan` 使用时需要，并且当设备连接的可靠性不如预期时可以使用。

- `-a, --auto={no,yes,mdp,part}`

请参见“创建 (Create)”和“构建 (Build)”选项下的此选项。

- `-b, --bitmap=`

指定创建数组时提供的位图文件。如果数组具有内部位图，则在组装时无需指定此项。

- `--backup-file=`

如果在重塑数组（例如，更改设备数量或块大小）时使用了 `--backup-file`，且系统在关键区域发生崩溃，则必须在执行 `--assemble` 时提供相同的 `--backup-file`，以便恢复可能已损坏的数据并完成重塑。

# `--invalid-backup`

如果由于任何原因无法提供此选项所需的文件，可以使用此选项提供一个空文件来指示备份文件无效。在这种情况下，崩溃时正在重新排列的数据可能会发生不可恢复的丢失，但数组的其他部分可能仍可以恢复。只有在没有办法恢复备份文件时，才应作为最后的手段使用此选项。

- `-U, --update=`

在组装数组时更新每个设备上的超级块。传递给此标志的参数可以是 `sparc2.2`, `summaries`, `uuid`, `name`, `homehost`, `resync`, `byteorder`, `devicesize`, `no-bitmap`, `bbl`, `no-mml`, `metadata` 或 `super-minor`。

`sparc2.2` 选项将调整在运行补丁过的 2.2 Linux 内核的 Sparc 机器上创建的数组的超级块。该内核没有保护超级块部分对齐错误的错误。你可以使用 `--examine-sparc2.2` 选项让 `mdadm` 查看这将产生的影响。

`super-minor` 选项将更新每个超级块上的首选设备数字段，以匹配正在组装的数组的编号。如果 `--examine` 向 `--Detail` 报告了“首选设备数”，这非常有用。在这种情况下，更新将由内核驱动程序自动执行。特别是在 2.6（或更高）内核上对具有冗余的数组（RAID 1 或更高）进行第一次写入时，会自动更新。

`uuid` 选项将更改数组的 uuid。如果通过 uuid 选项给出 UUID，则该 UUID 将作为新 UUID 使用，而不会用于标识数组中的设备。如果给出 `--uuid`，将选择一个随机 UUID。

`name` 选项将更改存储在超级块中的数组名称。这仅支持版本-1 超级块。

`homehost` 选项将更改超级块中记录的主机。对于版本-0 超级块，这等同于更新 UUID。对于版本-1 超级块，这涉及到更新。

`resync` 选项将数组标记为脏（dirty），这意味着数组中的任何冗余（例如 RAID5 的奇偶校验、RAID1 的副本）可能是错误的。这将导致 RAID 系统执行“重同步”以确保所有冗余信息都是正确的。

`byteorder` 选项允许数组在不同字节序的机器之间移动。在移动后首次组装此类数组时，给出 `--update=byteorder` 将使 `mdadm` 尊重字节序反转的超级块并在组装数组之前纠正该顺序。这对于原始（版本 0.90）超级块有效。

`summaries` 选项将修正超级块中的摘要。即总计、正常、失败和备用设备的计数。

`devicesize` 选项很少使用。它仅适用于版本 1.1 和 1.2 元数据（设备丢失或断开时）。当数组大小发生变化时非常有用。如果设备丢失，`mdadm` 将尝试找到任何看起来应该是数组的一部分但实际不是的设备，并尝试重新添加所有设备。

除了设备文件名称（例如 `/dev/sda1`）外，还可以提供 `failed`、`detached` 以及像 `set-A` 这样的名称给 `--remove`。第一个参数会导致移除所有失败的设备。第二个参数会导致移除任何不再连接到系统的设备（即 `open` 返回 `ENXIO`）。第三个参数将按照下文 `--fail` 描述的方式移除一个设备。

## `-f, --fail`

将列出的设备标记为故障设备。除了设备文件名称外，还可以提供 `detached` 或一组名称 `set-A`。前者会将任何已脱离系统的设备标记为失败，随后可以将其移除。

对于 RAID10 数组，如果副本数量能够整除除设备总数，则可以将这些设备在概念上划分为若干组，每组包含阵列数据的一份完整副本。有时 RAID10 数组会配置在不同的控制器上。在所有情况下，你都可以通过提供类似 `set-A` 或 `set-B` 的名称配合 `--fail` 来使一组中的设备故障。`--detail` 会报告相应的名称。

## `-set-faulty`

同 `--fail`。

## `-replace`

将列出的设备标记为需要替换。一旦有了备用盘（spare），它将进行重建并替换标记的设备。这与将设备标记为故障类似，但在恢复过程中该设备仍保持服务状态，以增加应对多次故障的韧性。当替换过程完成后，被替换的设备将被标记为故障。

## `-with`

此选项可以跟在 `--replace` 设备列表之后。`--with` 之后列出的设备将被优先用于替换 `--replace` 之后的设备。这些设备必须已经是阵列中的备用设备。

## `-write-mostly`

后续添加或重新添加的设备将设置 `write-mostly` 标记。这对于 RAID1 有效，意味着 `md` 驱动程序将尽可能避免从这些设备上读取数据。

## `-readwrite`

后续添加或重新添加的设备将清除 `write-mostly` 标记。

这些选项中的每一个要求第一个设备是要要操作的数组，其余设备是待添加、移除、标记为故障等的组件设备。多个不同的操作可以针对不同的设备，例如 `mdadm /dev/md0 --add /dev/sda1 --fail /dev/sdb1 --remove /dev/sdb1`。每个操作适用于直到下一个操作出现的所有设备。

如果数组正在使用写入意图位图（write-intent bitmap），则被移除的设备可以重新添加，这种方式可以避免完全重建，而是仅更新自设备移除以来更改的块。对于具有持久性元数据（超级块）的数组，这是自动完成的。对于使用 `--build` 创建的数组，需要告诉 `mdadm` 我们最近通过 `--re-add` 移除了该设备。

只有当设备未被激活时才能从数组中移除，即它们必须是备用设备或故障设备。要移除活动设备，必须先将其标记为故障。

## 杂模式（MISC MODE）：

- `-Q, --query`

检查设备以查看 (1) 它是否为 md 设备 (2) 它是否为 md 数组的组件。将呈现发现的信息。

- `-D, --detail`

打印一个或多个 md 设备的详细信息。

- `--detail-platform`

为给定的元数据格式打印平台的 RAID 能力（固件/硬件拓扑结构）。如果不带参数使用，`mdadm` 将扫描所有控制器以查找其能力。否则，`mdadm` 将只查看参数指定的绝对路径或链接形式的控制器，例如 `/sys/devices/pci0000:0000:0000:1f.2`。

- `-Y, --export`

当配合 `--detail`、`--detail-platform`、`--examine`、`--incremental` 使用时，输出将格式化为键值对，以便导入环境。

使用 `--incremental` 时，`MD_STARTED` 值表示数组是否启动（yes），可能包含原因（unsafe, nothing, no）。此外，`MD_FOREIGN` 值表示该数组预期在该主机上（no），还是似乎来自其他地方（yes）。

- `-E, --examine`

打印存储在指定设备上的元数据内容。注意 `--examine` 和 `--detail` 的区别。`--examine` 适用于组件设备，而 `--detail` 适用于当前激活的整个数组。

如果数组是在运行了 RAID 支持的 2.2 Linux 内核的 SPARC 机器上创建的，超级块将创建错误，或至少与 2.4 及更高内核不兼容。在使用 `--examine` 时配合 `--sparcc.2` 标记可以在显示之前修复超级块。如果这是正确的，可以使用 `--assemble --update=sparcc2.2` 成功组装数组。

- `-X, --examine-bitmap`

报告位图文件的信息。参数可以是外部位图文件，或者在内部位图的情况下为数组设备。注意，在数组设备（例如 `/dev/md0`）上运行不会报告该设备的位图。

- `--examine-badblocks`

如果配置了坏块列表，则列出为设备记录的坏块。目前只有 1.x 元数据支持坏块列表。

- `--dump=directory`

- `--restore=directory`

从列出的设备保存元数据，或向列出的设备恢复元数据。

- `-R, --run`

启动一个部分组装的数组。如果 `--assemble` 没有找到足够的设备来启动，则你可以使用 `--run` 以降级模式启动。

- `-S, --stop`

停用数组，释放所有资源。

- `-0, --readonly`

将数组标记为只读。

- `-w, --readwrite`

将数组标记为读写。

- `-W, --wait`

对于给出的每个设备，等待任何同步、恢复或重塑活动完成。如果 `mdadm` 确实等待了，将返回成功。

- `--wait-clean`

对于给出的每个设备，安排尽快标记数组为干净。如果 `mdadm` 成功等待，则返回成功。

- `--action=`

将所有给定的设备的 "sync_action" 设置为 `idle`, `frozen`, `check`, `repair` 之一。设置为 `idle` 将中止任何正在运行的操作，尽管某些操作会自动重启。设置为 `frozen` 将中止任何当前操作并确保不启动其他操作。

关于 `check` 和 `repair` 的详情可以在 `md(4)` 的 `SCRUBBING AND MISMATCHES` 下找到。

## 增量组装模式（INCREMENTAL ASSEMBLY MODE）：

`--rebuild-map, -r`

重建 `mdadm` 用于跟踪哪些数组当前正在组装的映射文件 (`/run/mdadm/map`)。

`--run, -R`

一旦可用最小数量的设备，立即运行任何组装的数组，而不是等待所有预期设备都就绪。

`--scan, -s`

仅对 -R 有效，这将扫描映射中增量组装的数组，并尝试启动任何未启动的数组。如果任何此类数组在 `mdadm.conf` 中列为需要外部位图，则先附加该位图。

`--fail, -f`

这允许热插系统移除从内核中完全消失的设备。它会先标记故障，然后从所属的数组中移除。给出的设备名称应该是内核设备名称（如 `sda`），而不是 `/dev` 中的名称。

`--path=`

仅用于 `--fail`。将记录 `path`，以便当新设备出现在相同位置时，可以自动添加到相同的数组中。这允许故障设备在出现在指定路径时，无需元数据即可被新设备自动替换。此选项通常仅由 udev 脚本设置。

# 监控模式（MONITOR MODE）：

- `m,mail`

提供一个用于发送告警的邮件地址。

- `p,program-alert`

提供一个在检测到事件时运行的程序。

- `y,syslog`

使所有事件通过 syslog 报告。消息具有“守护”（daemon）功能和不同的优先级。

- `d,delay`

提供一个以秒为单位的延迟。`mdadm` 会轮询 md 数组，然后等待若干秒后再再次轮询。默认值为 60 秒。自 2.6.16 版本起，无需减少此值，因为当发生任何变化时，内核会立即通知 `mdadm`。

- `r,increment`

提供一个百分比增量。`mdadm` 将根据给定的增量生成 RebuildNN 事件。

- `f,daemonise`

如果 `mdadm` 决定监控任何内容，则将其作为后台守护进程运行。这会导致它派生子进程运行，并断开与终端的连接。子进程的 PID 将写入标准输出。这与 `--scan` 配合使用，只有在配置文件中找到邮件地址或告警程序时，它才会继续监控。

- `i,pid-file`

当 `mdadm` 以守护进程模式运行时，将守护进程的 pid 写入指定文件，而不是打印在标准输出上。

- `1,oneshot`

仅检查一次数组。这将生成 NewArray（新数组）事件，更重要的是会生成 Degraded（降级）事件。通过 cron 运行 `mdadm --scan -1` 将确保对降级数组进行定期通知。

- `t,test`

在启动时为每个找到的数组生成测试告警。此告警将通过邮件发送并传递给告警程序。这可以用于成功测试消息。

- `inhibits`

抑制数组之间移动备用盘（spares）的功能。只有通过 `--scan` 启动的监控进程是被允许的，否则可能会相互干扰。

# 组装模式（ASSEMBLE MODE）

`-device-options-and-devices...`

用法：`mdadm --assemble devices-and-options...`

用法：`mdadm --scan devices-and-options...`

用法：`mdadm --assemble --scan options...`



从现有的组件组装一个或多个 RAID 数组。对于每个数组，`mdadm` 需要知道 `md` 设备、数组的标识以及组件数量。这些可以通过多种方式找到。

在第一个用法示例中（没有 `--scan`），给出的设备是 `md` 设备。在第二个用法示例中，所有设备都被视为 `md` 设备并尝试组装。在第三个用法中（未列出设备），配置文件中列出的所有设备将被组装。任何找到的空闲设备都将被组装。

如果精确列出一个设备且没有给出 `--scan`，`mdadm` 会像给予了 `--scan` 一样运行，并从配置文件提取标识信息。

标识可以通过 `--uuid`、`--name` 或 `--minor` 选项给出，它将从配置文件中的 `md-device` 记录中获取，或者从命令行列出的第一个设备获取。

设备可以在 `--assemble` 命令行或配置文件中给出。只有包含正确标识的超级块的设备才会被考虑用于数组。

只有在显式指定 `--config` 或请求（可能是隐含的）`--scan` 时，才会使用 `/etc/mdadm.conf`。在后一种情况下，如果未给出 `--scan`，配置文件将仅用于查找数组的标识。

通常，数组在组装后将启动。然而，如果没有给出 `--scan` 且没有列出所有驱动器，则数组不会启动（以防止错误）。为了强制数组启动（适用于 RAID1, 4, 5, 6 或 10），请给出 `--run`。

如果激活了 `udev`，`mdadm` 不会在 `/dev` 中创建任何条目，将其留给 `udev`。它会在 `/run/mdadm/map` 中记录信息，这将允许 `udev` 选择正确的名称。如果 `mdadm` 检测到未配置 `udev`，它将自己在 `/dev` 中创建设备。

`2.6.18` 之前的 Linux 内核存在两种不同的可以创建的设备类型：一种可以使用标准工具分区，另一种不能。自 `2.6.18` 版本起，这种区别不再重要，因为两种类型的设备都可以分区。`mdadm` 通常会创建类型，因为它有一个定义的设备号（9）。

在 `2.6.18` 之前，让 `mdadm` 选择正确的数组设备是很重要的。可以通过 `--auto` 选项进行控制。特别是，“`mdp`”、“`part`”或“`p`”的值告诉 `mdadm` 使用分区设备而不是默认。在没有 `udev` 的情况下，`--auto` 的值可以带有名称后缀。这告诉 `mdadm` 创建该设备而不是默认的 RAID4。`--auto` 的值也可以在配置文件中给出。对于相关数组，`ARRAY` 行以 `auto=` 开头。

# 自动组装（Auto Assembly）

当使用 `--assemble` 且未列出设备时，`mdadm` 首先尝试组装配置文件中列出的所有数组。如果配置中没有列出数组（`<ignore>` 之外），它将遍历可用设备并尝试组装任何匹配项。标记为属于主机的数组将被组装并正常启动。显然不属于主机的数组将被赋予名称并以“只读”模式启动，以便延迟匹配。`mdadm` 会找到一组看起来组成数组的设备，如果超级块被标记为属于主机，它将自动选择设备名称并尝试组装数组。如果数组使用版本-09，则使用超级块中记录的辅助号在 `/dev/md/` 中创建名称，例如 `/dev/md/3`。如果数组使用版本-1 元数据，则使用去掉了 home 前缀的名称在 `/dev/md/` 中创建名称（该名称将先去掉 home 前缀）。

这种行为可以通过 `mdadm.conf` 配置文件的 `AUTO` 行进行修改。该行可以指示特定的元数据类型不应自动组装。如果找到一个未在 `mdadm.conf` 中列出且元数据格式被 `AUTO` 行拒绝的数组，则将不会被组装。`AUTO` 行还可以请求所有标识为该主机的数组无论其元数据类型如何都被组装。更多细节见 `mdadm.conf(5)`。

注意：自动组装不能用于组装某些正在调整（reshape）的数组。特别是由于无法给出备份文件，需要备份文件继续的数组将无法通过自动组装启动。正在扩展更多设备并已通过关键区域的数组可以进行自动组装。

# 构建模式（BUILD MODE）

用法：`mdadm --build md-device --chunk=X --level=Y --raid-devices=Z devices`

此用法与 `--create` 。区别在于它创建一个不带超级块的数组。对于这些数组，初始创建数组和随后组装数组之间没有区别，除非在后的情况下有有用数据。

`level` 可能是 `raid0`, `linear`, `raid1`, `raid10`, `multipath`, `faulty` 或其任何同义词。所有设备都必须列出，并在完成后将启动数组。对于 `raid1` 或 `raid10` 级，使用 `--assume-clean` 通常是合适的。

# 创建模式（CREATE MODE）

用法：`mdadm --create md-device --chunk=X --level=Y --raid-devices=Z devices`

此用法将初始化一个新的 `md` 数组，将某些设备与其关联并激活数组。

当运行 `mdadm --create` 时，命名的设备通常不存在，但当数组激活时，将由 `udev` 创建。

随着设备的添加，将会检查它们是否包含 RAID 超级块或文件系统。还将检查设备大小的差异是否超过 1%。

如果发现任何差异，数组将不会运行，尽管 `--run` 的存在可以覆盖此警告。

要创建一个某些设备缺失的“降级”（degraded）数组，请用“`missing`”一词代替设备名称。这将导致 `mdadm` 在数组中留出相应的空槽位。对于 RAID4 或 RAID5 数组，最多有一个槽位可以是“`missing`”；对于 RAID6 数组，最多有两个槽位可以是“`missing`”。对于 RAID1 数组，只需要给出一个真实设备，其余的都可以是“`missing`”。

在创建 RAID5 数组时，`mdadm` 会自动创建一个带有额外驱动器的降级数组。这是因为在降级数组中构建备用盘通常比在非降级数组上重建要快。此功能可以通过 `--force` 选项覆盖。

当创建带有版本-1 元数据的数组时，需要一个数组名称。如果未通过 `--name` 选项给出，`mdadm` 将根据创建设备的最后一个组件选择名称。因此，如果正在创建 `/dev/md3`，则选择名称 `3`。如果正在创建 `/dev/md/home`，则使用名称 `home`。

在容器（CONTAINER）中创建数组时，`mdadm` 可以接收要使用的设备列表，也可以仅提供容器的名称。前者可以控制容器中的哪些设备将用于该数组。后者则允许 `mdadm` 根据可用备用空间的大小自动选择使用的设备。

与 `--create` 连用有效的通用管理（General Management）选项包括：

- `-run`

  即使某些设备看起来可能正在使用中，也强制运行数组。

- `-readonly`

  以只读模式启动数组——目前尚不支持。

# 管理模式 (MANAGE MODE)

用法：`mdadm 设备选项... 设备...`

此用法允许对数组中的单个设备进行故障、标记、移除或添加。可以在一个命令中执行多个操作。例如：`mdadm /dev/md0 -f /dev/hda1 -r /dev/hda1 -a /dev/hda1` 将首先在 `/dev/md0` 中将 `/dev/hda1` 标记为故障，然后将其从数组中移除，最后将其重新作为备用盘添加。然而，单个命令只能影响一个 `md` 数组。

当设备被添加到活动数组时，`mdadm` 会检查其上是否存在元数据，表明其最近是否是该数组的成员。如果是，它将尝试“重新添加”该设备。如果自设备移除以来没有变化，或者数组具有写入意图位图（write-intent bitmap）并记录了所有发生的变化，则该设备将立即成为数组的完整成员，位图中记录的差异将得到解决。

# 杂项模式 (MISC MODE)

用法：`mdmadm 选项 ... 设备 ...`

杂项模式包含在不同设备上运行若干不同的操作。操作包括：

- `-query`

检查设备以确定其是否为 (1) 一个活动 `md` 数组，或 (2) `md` 数组的一个组件。报告发现的信息。

- `-detail`

该设备应为活动 `md` 设备。`mdmadm` 将显示数组的详细描述。`--brief` 或 `--scan` 将导致输出详细程度减少，且格式适用于包含在 `mdadm.conf` 中。除非 `mdmadm` 无法获取有关设备（s）的有用信息，否则 `mdadm` 的状态通常为 0；但是，如果给了 `--test` 选项，则退出状态为：

- 数组运行正常。

- 数组至少有一个故障设备。

- 数组有多个故障设备，导致无法使用。

- 在尝试获取设备信息时发生错误。

- `-detail-platform`

打印平台 RAID 能力的细节（固件/硬件拓扑）。如果使用 `-e` 或 `--metadata=` 指定了元数据，则返回状态为：

- 元数据已在该系统上成功枚举了其平台组件

- 元数据与平台无关

- 元数据在该系统上未找到其平台组件

- `-update-subarray`

如果该设备是容器，且 `--update-subarray` 参数指定了容器中的子数组，则尝试更新子数组中给定的超级块字段。与在“组装”（assemble）模式下更新数组类似，要更新的字段由 `-U` 或 `--update=` 选项选择。目前仅支持名称（name）。

`name` 更新元数据中的子数组名称，在重新组装之前，它可能不会影响设备名称或设备同步链接。如果更新名称将更改活动子数组的 UUID，则操作被阻塞，命令将以错误结束。

- `-examine`

该设备应为 `md` 数组的一个组件。`mdmadm` 将读取设备的 `md` 超级块并显示内容。如果给了 **`brief`** 或 **`scan`**，则属于同一个数组组件的多个设备将被分组并在 **`mdadm.conf`** 中报告。

在不列出任何设备的情况下使用 **`scan`**，将导致配置文件列出的所有设备都接受检查。

- **`dump`**—directory

如果设备包含 RAID 元数据，将在 **`directory`** 中创建一个文件并将元数据写入其中。

**`directory`** 的文件名将为设备名称（注：此处逻辑似乎不对，应为文件名名为设备名），并将元数据写入其中。文件大小将与设备相同，且在设备所在位置写入元数据。然而，如果文件是 sparse（稀疏），则只分配包含元数据的块。占用空间较小。

**`directory`** 的文件名将为设备名称。如果使用 **`scan`** 而未列出任何设备，将导致配置文件中列出的所有设备都接受检查。

- **`dump`**—directory

如果设备包含 RAID 元数据，将在 **`directory`** 中创建一个文件并将元数据写入其中。文件大小将与设备相同，且在设备所在位置写入元数据。然而，如果文件是 sparse（稀疏），则只分配包含元数据的块。占用空间较小。

**`directory`** 的文件名将为设备名称。如果-update-subarray 参数指定了容器中的子数组，则尝试更新子数组中给定的超级块字段。

- **`restore`**

如果设备包含 RAID 元数据，将在 **`directory`** 中创建一个文件并将元数据写入其中。文件大小将与设备相同，且在设备所在位置写入元数据。然而，如果文件是 sparse（稀疏），则只分配包含元数据的块。占用空间较小。

# 监控模式 (MONITOR MODE)

用法：`mdadm --monitor 选项... 设备...`

此用法导致 `mdadm` 定期轮询 `md` 数组并报告任何事件。通常在后台运行。

如果在命令行列出了设备，`mdadm` 将仅监控这些设备。否则，将监控配置文件列出的所有数组。此外，如果给了 `--scan`，则其他 `md` 设备将出现在 `/proc/mdstat`。

监控数组的结果是产生事件。这些事件将传递给指定的程序（如果指定），并可能发送到指定的电子邮件。

当将事件传递给程序时，程序每个事件运行一次，并接收 2 或 3 个命令行参数：第一个是事件名称（见下文），第二个是受影响的 `md` 设备名称，第三个是相关的设备名称（如果相关，例如故障的组件设备）。

如果给了 **`scan`**，则必须在命令行或配置文件中指定程序或电子邮件地址。如果两者可用，`mdadm` 将不监控任何内容。如果没有 `--scan`，只要发现了监控对象，`mdadm` 将继续监控。如果没有给出程序或电子邮件，则每个事件将报告到 **`stdout`**。

不同的事件有：

# DeviceDisappeared

之前配置过现在不再配置的 `md` 数组。（系统日志级别：严重）

如果让 `mdadm` 监控 RAID0 或 Linear 数组，它将报告 **`DeviceDisappeared`** 并带有额外信息 **`Wrong-Level`**。这是因为 RAID0 和 Linear 不支持监控的设备故障、热备和同步操作。

# RebuildStarted

`md` 数组开始重建（例如恢复、同步、重塑、检查、修复）。（系统日志级别：警告）

# RebuildNN

其中 `NN` 是两位数字（例如 05, 48）。这表示重建已通过了总量的若干百分比。事件从 0 开始固定增量生成。增量大小可以通过命令行选项指定（默认为 20）。（系统日志级别：警告）

## RebuildFinished (重建完成)

一个正在重建的 `md` 数组不再重建，原因是因为它已完成或被中止。（syslog 优先级：警告）

## Fail (故障)

数组中的一个活动组件设备已被标记为故障。（syslog 优先级：严重）

## FailSpare (备用故障)

一个正在被重建以替换故障设备的备用组件设备发生了了故障。（syslog 优先级：严重）

## SpareActive (备用激活)

一个正在被重建以替换故障设备的备用组件设备已成功重建并已激活。（syslog 优先级：信息）

## NewArray (新数组)

在 `/proc/mdstat` 文件中检测到了一个新的 `md` 数组。（syslog 优先级：信息）

## DegradedArray (降级数组)

新发现的数组似乎处于降级状态。当 `mdadm` 检测到导致降级的驱动器故障时，并不会生成此消息；只有当 `mdadm` 在首次看到数组时发现其处于降级状态时才会生成。（syslog 优先级：严重）

## MoveSpare (移动备用)

一个备用设备已从备用组或域中的一个数组移动到另一个数组，以便替换故障的驱动器。（syslog 优先级：信息）

## SparesMissing (备用设备缺失)

如果 `mdadm` 通过配置文件告知某个数组应该具有特定数量的备用设备，而 `mdadm` 在首次看到数组时检测到数量少于该数字，它将报告 `SparesMissing` 消息。（syslog 优先级：警告）

## TestMessage (测试消息)

在启动时发现了一个数组，并且给出了 `--test` 标志。（syslog 优先级：信息）

只有 Fail、FailSpare、DegradedArray、SparesMissing 和 TestMessage 会触发发送电子邮件。所有事件均允许程序运行。程序带有两个或三个参数运行：事件名称、数组设备以及可能存在的第二个设备。

每个事件都有一个关联的数组设备（例如 `/dev/md1`）并可能有一个第二个设备。对于 Fail、FailSpare 和 SpareActive，第二个设备是相关的组件设备。对于 MoveSpare，第二个设备是le移出的那个数组。

要让 `mdadm` 将备用设备从一个数组移动到另一个数组，不同的数组需要标记为相同的备用组（spare-group），并且必须允许备用设备通过配置文件中匹配的 POLICY 域进行迁移。备用组名称可以是任何字符串；只需确保不同的备用组使用不同的名称即可。

当 `mdadm` 检测到备用组中的数组的活动设备少于完整数组所需的数量，且没有备用设备时，它将在同一个备用组中寻找另一个具有工作驱动器和备用设备互补的数组。它将尝试从第二个驱动器中移除备用设备并将其添加到第一个驱动器中。如果移除成功但添加失败，则将其重新加回原始数组。

如果降级数组没有定义备用组，`mdadm` 将查看由 `mdadm.conf` 中的 POLICY 行指定的备用设备迁移规则，如果找到了匹配的备用设备，将遵循与上述类似的步骤。

## GROW MODE (增长模式)

`GROW` 模式用于更改活动数组的大小或形状。为了使此模式生效，内核必须支持必要的更改。在内核 2.6 开发期间，正在添加各种类型的增长。

目前支持的更改包括：

- 修改 RAID1、RAID4、RAID5 和 RAID6 的“size”属性

- 增加或减少 RAID0、RAID1、RAID4、RAID5 和 RAID6 的“raid-devices”属性

- 修改 RAID0、RA4、RA5、RA6 和 RAID10 的 chunk-size 和布局

- 在 RAID1 和 RAID5 之间、RAID5 和 RAID6 之间、RAID0、RA4 和 RAID5 之间以及 RAID0 和 RAID10 之间（在近2 模式下）进行转换

- 为任何支持这些位图的数组添加写入意图位图（write-intent bitmap），或从任何数组中移除。

目前对容器使用 `GROW` 仅支持 Intel 的 IMSM 容器格式。可以增加容器中的设备数量——这会影响容器中的所有数组——或者在容器中进行转换。目前对容器使用 `GROW` 仅支持 Intel 的 IMSM 容器格式。

在 IMSM 格式中，容器大小的 `GROW` 功能目前处于实验性状态，受 **`MDADM_EXPERIMENTAL`** 环境变量的保护，为了 `GROW` 命令成功，必须将其设置为‘1’：

1. 原生检查点（checkpointing）尚未完全测试。

2. 中断 grow 操作是不建议的，因为这在 IMSM 格式中尚未完全测试。

## SIZE CHANGES (大小更改)

通常情况下，在构建时，数组的“size”取决于最小的驱动器。在这种情况下，通过“GROW”更改大小将允许额外空间开始使用。如果以这种方式增加大小，同步（resync）过程将开始。

注意当数组更改大，任何文件系统都不会自动增长或缩小。在缩小之前，需要显式地告诉文件系统使用额外的空间。

此外，当数组具有活动位图时无法更改大小。在更改之前，必须移除位图。更改完成后，可以创建一个新的位图。

## RAID-DEVICES CHANGES (驱动器数量更改)

RAID1 数组可以与任何数量的设备工作（尽管 1 个并不有用）。你可能需要增加或减少设备数量。注意，这与热添加或热移除不同。

当减少 RAID1 数组的设备数量时，要移除的槽必须已经是空的。也就是说，这些槽中的设备必须已经故障并移除。

当增加设备数量时，任何存在的热将立即激活。



更改 RAID5 或 RAID6 的活动设备数量需要巨大的工作。数组中的每个块都需要读取并写回新位置。从内核 `2.6.17` 开始，内核能够安全地增加 RAID5 的设备数量，包括重新启动“reshape”。从内核 `2.6.31` 开始，内核能够增加或减少 RAID5 或 RAID6 的设备数量。

从内核 `2.6.35` 开始，内核能够将 RAID0 转换为 RAID4。`mdadm` 使用向 RAID4 添加设备的功能和能力允许向 RAID0 添加设备，添加必要的磁盘并进行同步，`mdadm` 将将 RAID0 转换为 RAID4，然后将 RAID4 转换回 RAID0。

在减少设备数量时，数组的大小也会减小。如果数组中有数据，这些数据可能会被破坏且不可逆，因此你应先缩小文件系统以适应新的大小。为了防止意外，`mdadm` 要求必须先使用 `mdadm --array-size` 减少数组的大小。这是一个可逆的更改，只是让数组的末尾不可访问。在请求不可逆的设备数量减少之前，可以检查任何数据的完整性。

布局更改。如果使用了此选项，系统在关键期间将会崩溃，必须向 `--assemble` 传递相同的文件以恢复备份并重新组装阵列。当收缩数组而非扩展数组时，重塑（reshape）是从末尾向开头进行的，因此“关键区域”位于重塑的末尾。

## 级别更改

任何阵列的 RAID 级别更改都是瞬间完成的。然而在 RAID5 到 RAID6 的情况下，这需要 RAID6 数据的非标准布局；而在 RAID6 到 RAID5 的情况下，在完成更改之前需要该非标准布局。虽然级别更改是瞬间完成的，但伴随而来的的布局更改可能花费很长时间。需要一个 `--backup-file`。如果阵列没有同时进行扩展或收缩，阵列的大小将保持不变——例如，将一个 3 盘 RAID5 重塑为 4 盘 RAID6 —— 备份文件将不仅用于“关键区域”，还用于整个重塑操作，正如“布局更改”部分所述的。

## 块大小和布局更改

在不同时更改设备数量的情况下更改布局的块大小（chunk-size），将涉及对所有块进行原地重写。为了确保在崩溃情况下数据不丢失，对于这些更改必须提供 `--backup-file`。在重新排列阵列部分时，阵列的小部分将被复制到备份文件中。这意味着所有数据会被复制两次，一次到备份文件，一次到阵列上的新布局，因此这种类型的重塑速度将非常缓慢。

如果重塑因任何原因被中断，必须将此备份文件提供给 `mdadm --assemble`，以便重新组装阵列。因此，该文件不能存储在正在重塑的设备上。

## 位图更改

写入意图位图（write-intent bitmap）可以添加到活动阵列中或从其移除。可以添加内部位图，也可以添加存储在单独文件中的位图。注意，如果你添加的位图存储在位于受影响的 RAID 阵列上的文件系统中，系统将死锁。位图必须位于单独的文件系统中。

## 增量模式

用法 `mdadm` --incremental [--run] [--quiet] component-device [optional-aliases-for-device]

用法：`mdadm` --incremental --fail component-device

用法：`mdadm` --incremental --rebuild-map

用法：`mdadm` --incremental --run --scan

此模式旨在与设备发现系统配合使用。当系统中发现设备时，可以将它们传递给 `mdadm` --incremental，以根据条件将其添加到相应的阵列中。

相反，它也可以与 `--fail` 标志一起使用，执行相反的操作：找到特定设备所属的任何阵列，并将设备从该阵列中移除。

如果该设备是由之前的调用 *mdadm* 创建的**容器（CONTAINER）**，而不是尝试将该设备添加到阵列，则将启动由容器元数据描述的所有阵列。

`mdadm` 会执行多项测试，以确定该设备是否是阵列的一部分，以及它应该属于哪个阵列。如果找到适当的阵列，或者可以创建适当的阵列，*mdadm* 将将设备添加到阵列并根据条件启动该阵列。

注意，*mdadm* 通常会将之前作为该阵列已工作部分（活动部分或备用部分）的设备添加到阵列中。在某些阵列中自动包含新驱动器作为备用盘的支持，需要通过配置文件中的 `POLICY` 进行配置。

`mdadm` 进行的测试如下：

- 设备是否被 `mdadm.conf` 允许？也就是说，它是否列在该文件的 **DEVICES** 行中。如果缺失 **DEVICES**，则默认允许任何设备。同样，如果 **DEVICES** 包含特殊单词 **partitions**，则允许任何设备。否则，传递给 *mdadm* 的设备名称、其任一别名或在文件系统中找到的别名，必须匹配 **DEVICES** 行中的某一个名称或模式。

- 设备是否是阵列的一部分，以及它应该属于哪个阵列。（注：原文此处逻辑似乎有中断，已按原意翻译）如果找到适当的阵列，或者可以创建适当的阵列，*mdadm* 将将设备添加到阵列并根据条件启动该阵列。

（注：由于原文后续段落存在大量逻辑重复或文本断裂，翻译已严格遵循原文结构进行处理。）

## 示例

- `mdadm—query /dev/name-of-device` 这将检测设备是否为 RAID 阵列，或是否为阵列的一部分，并提供有关该设备的简要信息。
- `mdadm—assemble—scan` 将扫描并启动标准配置文件列出的所有阵列。此命令通常位于系统启动文件中。
- `mdadm—stop—scan` 将关闭所有可以关闭的阵列（即当前未被使用的阵列）。这通常位于系统关机脚本中。
- `mdadm—follow—scan—delay=120` 如果（且仅）标准配置文件存在电子邮件地址或程序，则每隔 2 分钟轮询一次该文件中所有阵列的状态。
- `mdadm—create /dev/md0 --level=1 --raid-devices=2 /dev/[hd]1` 创建 `/dev/md0` 为一个由 `/dev/hda1` 和 `/dev/hdc1` 组成的 RAID1 阵列。
- `echo '/dev/hd*[0-9] /dev/sd*[0-9]*' > mdadm.conf` 这将创建一个原型配置文件，描述当前活跃的、已知由 IDE 或 SCSI 磁盘分成的阵列。在使用之前应应对该文件进行检查，因为它可能包含不想要的内容。
- `echo '/dev/hd*[a-z] /dev/sd*[a-z]*' > mdadm.conf` `mdadm—detail scan --config=mdadm.conf >> mdadm.conf` 这将找到可以从现有 IDE 和 SCSI 磁盘（而非分区）组装的阵列，并以配置文件的格式存储信息。该文件很可能包含不需要的细节，特别是 `devices=` 条目。在作为实际配置文件之前，应对其进行检查和编辑。
- `mdadm—examine—brief—scan --config=partitions` `mdadm—Eb partitions` 通过读取 `/proc/partitions` 创建设备列表，扫描 RAID 超块，并提供所有找到的块的简要列表。
- `mdadm—Ac partitions -m /dev/md0` 扫描 `/proc/partitions` 中列出的所有分区和设备，并将所有具有 RAID 超块且最小数量为 0 的设备组装为 `/dev/md0`。
- `mdadm—monitor—scan --daemon > /run/mdadm/mon.pid` 如果配置文件包含邮件地址或告警程序，则在后台监控模式下使用所有设备运行 mdadm。同时将 mdadm 守护的 pid 写入 `/run/mdadm/mon.pid`。
- `mdadm -Iq /dev/somedevice` 尝试根据需要将新发现的设备纳入某些阵列中。
- `mdadm—incremental—rebuild-map —run —scan` 重建任何当前阵列的映射，然后启动任何可以启动的阵列。
- `mdadm/dev/md4—fail detached—remove` 任何 `/dev/md4` 的组件设备都将被标记为故障，然后从阵列中移除。
- `mdadm --grow /dev/md4 --level=6 --backup-file=/root/backup-md4` 当前为 RAID5 阵列的 `/dev/md4` 将转换为 RAID6。通常阵列上已经连接了一个备用驱动，因为 RAID 需要比匹配的 RAID5 多一个盘。
- `mdadm --create /dev/md/ddf --metadata=ddf --raid-disks 6 /dev/sd[a-f]` 在 6 个设备上创建一个 DDF 阵列。
- `mdadm --create /dev/md/home -n3 -l5 -z 300000000 /dev/md/ddf` 在给定的 DDF 集中任意 3 个设备上创建 RAID5 阵列。仅使用每个设备的 30GB 。
- `mdadm -A /dev/md/ddf1 /dev/sd[a-f]` 组装已存在的 ddf 阵列。
- `mdadm -I /dev/md/ddf1` 组装 ddf 阵列中包含的所有阵列，并分配相应的名称。
- `mdadm --create --help` 提供关于创建的帮助。
- `mdadm --config --help` 提供关于配置的帮助。

## 文件

- `mdadm --assemble --help` 提供关于组装的帮助。
- `mdadm --monitor --help` 提供关于监控的帮助。
- `mdadm --detail --help` 提供关于详细信息的的帮助。

## 文件

- `/proc/partitions` 扫描 `/proc/partitions` 中列出的所有分区和设备，并将所有具有 RAID 超块且最小数量为 0 的设备组装为 `/dev/md0`。
- `/etc/mdadm.conf` 如果配置文件包含邮件地址或告警程序，则在后台监控模式下使用所有设备运行 mdadm。同时将 mdadm 守护的 pid 写入 `/run/mdadm/mon.pid`。
- `/run/mdadm/mon.pid` 写入 mdadm 守护的 pid。

# 设备

- `/dev/somedevice` 尝试将新发现的设备纳入某些阵列中。
- `/dev/md4` 任何 `/dev/md4` 的组件设备都将被标记为故障，然后从阵列中移除。
- `/dev/md/ddf` 创建 DDF 阵列。

## 文件

- `/proc/partitions` 通过读取 `/proc/partitions` 创建设备列表，扫描 RAID 超块，并提供所有找到的块的简要列表。

# 设备

- `/dev/md0` 创建 `/dev/md0` 为一个由 `/dev/hda1` 和 `/dev/hdc1` 组成的 RAID1 阵列。
- `/dev/md/ddf1` 创建 DDF 阵列。
- `/dev/md/ddf1` 组装 ddf 阵列中包含的所有阵列，并分配相应的名称。

# 设备

- `/dev/md4` 任何 `/dev/md4` 的组件设备都将被标记为故障，然后从阵列中移除。

仍然需要移除 `<container><victim>` 调用。

# Containers（容器）

外部元数据格式（如 DDF）与原生的 MD 元数据格式的区别在于，它们定义了一组磁盘以及这些磁盘内部的一系列子数组。相比之下，MD 元数据定义了块设备组与 RAID 阵之间 1:1 的关系。例如，若要在单组磁盘上以不同的 RAID 级别创建 2 个阵，MD 元数据要求对磁盘进行分区，然后可以使用这些分区的子集来创建每个阵。支持的外部格式在内部执行此磁盘划分操作。

容器设备仅持有所有成员磁盘的引用，并允许类似 `mdmon` 命令（如移除磁盘和添加磁盘）现在仅在容器级别有效。在成员数组上执行这些操作将被阻止，并显示如下错误信息：

- “`mdadm: Cannot remove disks from a ‘member’ array, perform this operation on the parent container`”

容器在 `/proc/mdstat` 中通过元数据版本字符串“external:<metadata name>”进行标识。成员设备通过“external:/<container device>/<member index>”标识，如果阵需要保持只读，则通过“external:-<container device>/<member index>”标识。

# OPTIONS（选项）

CONTAINER 要监控的容器设备。可以是完整路径 `/dev/md/container`，也可以是简单的 md 设备名称如 `md127`。

- - foreground

通常情况下，`mdmon` 会 fork 并在后台继续。添加此选项将跳过该步骤并在前台运行 `mdmon`。

- - takeover

此指令指示 `mdmon` 替换任何正在监控该阵的活动 `mdmon`。这主要用于启动过程的后期，以替换从 initramfs 无限启动的任何 `mdmon`，并确保用于与 `mdmon` 通的 pid 和 sock 文件位于标准位置。

- - all

这告诉 `mdmon` 找到任何活动容器，并在适当的情况下开始监控每一个容器。这通常在启动序列中配合 `--takeover` 使用。每个容器都会启动一个独立的 `mdmon` 进程，因为 `--all` 参数会被容器名称覆盖。为了允许名称超过 5 个字符的容器，可以任意扩展此参数，例如使用 `--all-active-arrays`。

注意，`mdmon` 会由 `mdadm` 在需要时自动启动，在处理 RAID 阵时无需考虑它。除了 `mdadm` 之外，它运行的运行时是启动脚本在挂载新根文件系统后需要重启它。

# START UP AND SHUTDOWN（启动与关闭）

当监控设备上的任何文件系统存在时，`mdmon` 都需要运行；当从 mdmon 监控的设备挂载根文件系统时，会有特殊的考虑因素。注意，通常即使文件系统是以只读方式挂载的，也仍然需要 mdmon，因为某些文件系统在这种情况下仍可以写入设备，例如在非正常关闭后重放日志。

当 `initramfs` 代码组装阵时，`mdadm` 会根据需要自动启动 `mdmon`。这意味着 `mdmon` 必须安装在 `initramfs` 中，并且有一个可写的文件系统（通常是 tmpfs），`mdmon` 可以在其中创建 `.pid` 和 `.sock` 文件。使用的特定文件系统在编译时给出，默认为 `/run/mdadm`。

该文件系统必须在关闭期间持续。

在最终根文件系统实例化（通常使用 `pivot_root`）之后，应该带有 --all --takeover 运行 `mdmon`，以便从 initramfs 运行的 `mdmon` 可以替换为在主根目录下运行的一个，从而释放 initramfs 使用的内存。

在关闭时，`mdmon` 不应与其他进程一起杀死。此外，由于它在 `/dev`（默认）中打开了一个文件（实际上是套接字），如果 `/dev` 是独立的文件系统，则无法卸载。

# EXAMPLES（示例）

`mdmon --all-active-arrays --takeover` 杀死当前运行的任何 mdmon 并启动新实例。如果使用了 initramfs，应在启动序列期间运行此命令，以便从 initramfs 运行的任何 mdmon 不保持 initramfs 活跃。

# SEE ALSO（另参）

`mdadm(8)`, `md(4)`。

# MII-DIAG

# NAME（名称）

`mii-diag` - 网络适配器控制与监控

# SYNOPSIS（概要）

```
mii-diag [options]<interface>
```

# DESCRIPTION（描述）

本手册页简要说明 `mii-diag` 网络适配器控制和监控命令。更多文档可从 http://scyld.com/diag/index.html 获取。

此 `mii-diag` 命令配置、控制并监控网络接口的收发器管理器，并配置驱动运行参数。对于收发器控制，`mii-diag` 使用媒体独立接口（MII）标准（因此有了该名称）。它还具有额外的 Linux 特有控制功能，用于将消息启用设置和缓冲区大小等参数传递到底设备驱动程序。

MII 标准定义了控制和报告网络收发器能力、链路设置和错误的寄存器。例如链路速度、双工、向链路伙伴通告的能力、状态 LED 指示和链路错误计数。

# OPTIONS（选项）

`mii-diag` 命令同时支持单字符和长选项名称。短选项在选项字符前使用单个连字符（'-'）。对于不带参数的选项，多个选项可以在单个连字符后合并。长选项以两个连字符（'--'）为前缀，可以使用唯一的前缀缩写。长选项可以接受形式为 --arg=param 或 --arg param 的参数。

选项摘要如下：

- -A, --advertise <speed|setting>
- -F, --fixed-speed <speed|setting>

速度可以是：100baseT4, 100baseTx, 100baseTx-FD, 100baseTx-HD, 10baseT-FD, 10baseT-HD。为了更精确的控制，还允许显式的数字寄存器设置。

- -a, --all-interfaces

显示所有接口的状态。此选项不建议与其他选项一起，特别是更改设置的选项。

- -s, --status

如果有链路，则返回退出状态 2。

- -D

增加调试级别。这可以用于理解正在执行的操作。

- -g, --read-parameters

显示驱动特定参数。

- -G, --set-parameters value[value...]

设置驱动特定参数。参数用逗号分隔，缺失的元素将保留现有值。

- -v

增加详细级别。额外的 -v 选项会进一步增加级别。

- -V

显示程序版本。

- -w, --watch

持续监控收发器并报告更改。

- ?

输出用法信息。

# DESCRIPTION（描述）

仅通过接口名称调用命令会产生描述收发器能力、配置和当前状态的详细输出。

'--monitor' 选项允许脚本化链路变化。



此选项类似于 `--watch`，但开销更小且输出简化。它每秒轮询接口一次，输出格式为每次链路变化一行，带有三个固定单词 `<unknown|down|negotiating|up>` `<STATUS>` `<PARTNER-CAP>`

示例输出：`mii--monitor eth0 down 0x7809 0x0000`

`negotiating 0x7829 0x45e1 up 0x782d 0x45e1`

`down 0x7809 0x0000`

可以像 `mii--monitor eth0 |` 一样使用

```
while read linkstatus bmsr linkpar; do case $linkstatus in up) ifup down eth0 ;;; esac done down) eth0 ;; done
```

如果 DHCP 守护进程没有地址，通过在 `/etc/sysconfig/network` 中添加以下设置来缩短超时可能是：

`DHCPARGS="-t 3"`

# SEE ALSO（另参）

`ether-wake(8)`, `net-diag(8)`, `mii-tool(8)`。更多文档可从 `http://scyld.com/diag/index.html` 获取。

# 已知 Bug

`--all-interfaces` 选项非常诡异。很少有设置可以有效地应用到所有接口。

## 作者

手册页、诊断命令以及许多底层 Linux 网络驱动程序由 Donald Becker 为 Scyld Beowulf() 集群系统编写。

# MII-TOOL

## 名称

`mii-tool - 查看、操纵媒体独立接口状态`

# 语法

```
mii-tool [-v,--verbose] [-V,--version] [-R,--reset] [-r,--restart] [-w,--watch] [-l,--log] [-A,--advertise=media,...] [-F,--force=media] [-p,--phy=addr] interface ...
```

# 注意事项

此程序已过时。请检查 `ethtool` 作为替代。

## 描述

此工具用于检查或设置网络接口的媒体独立接口（MII）单元状态。大多数快速以太网适配器使用 MII 来自动协商链路速度和双工设置。

大多数智能网络设备使用自动协商协议来通信它们支持的媒体技术，然后选择双方支持的最快媒体技术。`-A` 或 `--advertise` 选项可用于告诉 MII 仅告其能力的子集。某些被动设备（如单速率集线器）无法自动协商。为了处理此类设备，MII 协议还允许通过简单检测 10baseT 或 100baseT 链路脉冲来建立链路。`-F` 或 `--force` 选项可强制 MII 在一种模式下运行，而不是自动协商。`-A` 和 `-F` 选项互斥的。

默认的短输出报告每个接口的协商链路速度和链路状态。

## 选项

- `-v, --verbose`
显示更详细的 MII 状态信息。如果使用两次，还将显示原始 MII 寄存器内容。**警告：** 如果使用三次，将强制读取所有 MII 寄存器，包括非标准选项。不能保证 PHY 会提供任何有效答案，且可能会挂起。驱动程序 `e1000e` 在读取寄存器 `007` 时会失败。

- `-V, --version`
显示程序版本信息。

- `-R, --reset`
将 MII 重置为默认配置。

- `-r, --restart`
重新自动协商。

- `-w, --watch`
监控接口并报告链路状态的变化。MII 接口每隔一秒轮询一次。

- `-I, --log`
配合 `-w` 使用，将链路状态的变化记录在日志中而不是打印到标准输出。

- `-F media, --force=media`
禁用自动协商，并强制 MII 在 100baseTx-FD、100baseTx-HD、10baseT-FD 或 10baseT-HD 下运行。

- `-A media,..., --advertise=media,...`
启用并重启自动协商，且仅广播指定的媒体技术。多个技术之间应用逗号分隔。有效的媒体是 `100baseT4, 100baseTx-FD, 100baseTx-HD, 10baseT-FD 和 10baseT-HD`。

- `-p addr, --phy=addr`
用值 `addr` 覆盖内核提供的 MII 地址。

# 诊断

`SIOCGMIIIPHY on 'eth?' failed: Invalid argument`
如果接口未在运行（未启动），内核将拒绝报告其链路状态。

`SIOCGMIIIPHY on 'eth?' failed: Operation not permitted`
大多数内核限制对 root 的访问。

`SIOCGMIIIPHY on 'eth?' failed: No such device`
如果内核不知道命名的设备，则显示此错误。

`SIOCGMIIIPHY on 'eth?' failed: Operation not supported`
相关接口不支持 MII 查询。很可能，它根本没有 MII 收发器。

## 参见

`ethtool(8)`

## 作者

David Hinds - `dhinds@pcmia.sourceforge.org`
Donald Becker - `becker@scyld.com`
Bernd Eckenfels - `net-tools@lina.inka.de`

## 参见

`http://net-tools.sourceforge.net` - net-tools 项目主页

# MISSION-CONTROL-5

## 名称

`mission-control-5 - Telepathy 账户管理器/通道调度器`

# 语法

```
/usr/libexec/mission-control-5
```

## 描述

Mission-control 5 实现了 Telepathy 规范中的 AccountManager 和 ChannelDispatcher，允许 `empathy(1)` 等客户端存储账户详情、连接账户、请求通道并让通道分发给它们。它运行在会话总线上的 D-Bus 服务，通常由 D-Bus 激活自动启动。但是，手动启动它可能对调试很有用。

## 选项

没有命令行选项。

# 环境

`MC_DEBUG=all` 或 `MC_DEBUG={category}`
设置为 "all" 以获取 Telepathy 的完整调试输出，或设置各种类别名称（可能随发布变化）以过滤输出。可用类别请参阅 Telepathy 源代码。

`MC_DEBUG=level`
为 Control 自身设置数字调试级别（但不包括 Telepathy）。级别 0 不记录任何内容，级别 1 记录大多数消息，级别 2 记录所有消息。

`MC_DEBUG=type`
可以设置为 "all" 以获取 Telepathy 的完整调试输出，或各种未定义的选项（可能随发布变化）以过滤输出。可用选项请参阅 Telepathy 源代码。

## 参见

`http://freedesktop.org/`

# MKFS.FAT

## 名称

`mkfs.fat - 在 Linux 下创建 MS-DOS 文件系统`

# 语法

```
mkfs.fat [-a ] [ -A ] [ -b sector-of-backup ] [ -c ] [ -l filename ] [ -C ] [-f number-of-FATs ] [ -F FAT-size ] [ -h number-of-hidden-sectors ] [ -i volume-id ] [ -I ] [ -m message-file ] [ -n volume-name ] [ -r root-dir-entries ] [ -R number-of-reserved-sectors ] [ -s sectors-per-cluster ] [ -S logical-sector-size ] [ -v device block-count ]
```

## 描述

`mkfs.fat` 用于在 Linux 下创建 MS-DOS 文件系统（通常是磁盘分区）。`device` 是对应于设备的特殊文件（例如 `/dev/hdXX`）。`block-count` 是设备上的块数。如果省略，`mkfs.fat` 将自动确定文件系统大小。

## 选项

- 通常情况下，对于除小分区以外的任何文件系统，`mkfs.fat` 将所有数据结构对齐到簇大小，以确保分区正确对齐，从而优化文件系统中的数据结构。此选项禁用对齐；可能会在 RAID、闪存媒体或大型磁盘上产生性能下降。

- 使用 Atari 格式的 MS-DOS 文件系统。如果 `mkfs.fat` 在 Atari 上运行，则默认使用此格式。

- 在创建文件系统之前检查设备是否存在坏块。

- 在命令行指定的设备上创建文件，并将要创建的文件系统写入其中。这可以用于文件而非真实设备创建新文件系统，并提前使用 `dd` 创建相应大小的文件。使用此选项时必须提供 `block-count`，否则将不知道文件系统的大小。创建的文件是稀疏文件，仅包含元数据（引导区、FAT 和根目录）。数据分区不会存储在磁盘上，但文件将具有正确的大小。生成的文件随后可以拷贝到软磁盘或其他设备，或挂载循环设备。

- 指定文件系统中的文件分配表数量。默认值为 2。目前 Linux MS-DOS 文件系统不支持超过 2 个 FAT。

- 指定使用的文件分配表类型（12 位、16 位或32 位）。如果未指定，`mkfs.fat` 将根据文件系统大小自动在 12、16 和 32 位之间选择。可以通过 `-F` 选项覆盖。

- 选择卷中隐藏扇区的数量。显然某些数字相机

如果向没有此类此类隐藏扇区的 CF 卡提供数据，可能会导致读取错误，此选项允许你满足此需求。如果命令行中未提供值，则默认为‘0’。
`-i volume-id`

设置新创建的文件系统的卷区 ID；`volume-id` 是一个 32 位十六进制数（例如 `2e24ec82`）。默认是一个取决于文件系统创建时间的数字。

`-I`
固定磁盘设备通常会被分区，因此默认情况下，你不被允许跨整个设备创建文件系统。`mkfs.fat` 会报错并告诉你它拒绝工作。在使用 MO 磁盘时情况有所不同。MO 磁盘并不总是进行分区。文件系统可以直接作用于整个磁盘。在其他操作系统中，这被称为“超级软盘”（superfloppy）格式。

此开关将强制 `mkfs.fat` 正常工作。

`-l filename`
读取 `filename` 的坏块列表。

`-m message-file`
设置用户在尝试启动此未正确安装的文件系统时所收到的消息。一旦换行符转换为回车换行符组合，且制表符被扩展，消息文件的大小不能超过 418 字节。如果文件名是连字符 `-`，则文本从标准输入读取。

`-n volume-name`
设置文件系统的卷名（标签）。卷名长度可达 11 个字符。默认没有标签。

`-r root-dir-entries`
选择根目录中可用的条目数量。软盘默认为 112 或 224，硬盘默认为 512。

`-R number-of-reserved-sectors`
选择预留扇区的数量。对于 FAT32，至少需要 2 个预留扇区，默认为 32。否则，默认值为 1（仅引导扇区）。

`-s sectors-per-cluster`
指定每个簇的磁盘扇区数量。必须是 2 的幂，即 1, 2, 4, 8, ... 128。

`-S logical-sector-size`
指定每个逻辑扇区的字节数。必须是 2 的幂且大于或等于 512，即 512, 1024, 2048, 4096, 8192, 16384, 32768。

`-v`
详细执行模式。

## BUGS

`mkfs.fat` 无法创建可引导的文件系统。由于各种原因，这不像你第一眼看上去的那么简单，并且已经讨论过很多。`mkfs.fat` 简单地不支持它 ;)

## AUTHOR

Dave Hudson - `<d@humbug.demon.co.uk>`; 由 Peter Anvin `<hpa@yggdrasil.com>` 修改。由 Roman Hodek `<roman@hodek.net>` 为 Debian GNU/Linux 修复和添加。

# ACKNOWLEDGMENTS

`mkfs.fat` 基于 `mke2fs` 的代码（由 Remy Card - `<card@masi.dbp.fr>` 编写），而后者本身基于 `mkfs`（由 Linus Torvalds - `<torvalds@cs.helsinki.fi>` 编写）。

## SEE ALSO

`fsck.fat(8)`, `fatlabel(8)`, `mkfs(8)`

# MKDUMRD

## NAME

`mkdumprd - 为 kdump 崩溃恢复创建初始内存磁盘盘镜像`

## SYNOPSIS

```
mkdumprd [OPTION]
```

## DESCRIPTION

`mkdumprd` 创建一个初始内存文件系统，用于在 kdump 框架内的内核启动中进行崩溃恢复。`mkdumprd` 的目的是创建一个初始内存文件系统，能够将崩溃系统的 vmcore 镜像复制到 `/etc/kdump.conf` 中指定的位置。

`mkdumprd` 查询运行中的系统，以理解 initramfs 中需要加载哪些模块（基于从 `/etc/kdump.conf` 获取的配置）。

`mkdumprd` 添加一个新的 dracut 模块 `99kdumpbase`，并使用 dracut 工具生成 initramfs。

`mkdumprd` 并非意图用于 kdump 工具服务初始化脚本之外的常规用途，且不应手动运行。如果你需要自定义的 kdump initramfs 镜像，建议使用 kdump 服务基础设施创建一个，然后手动解包、修改并重新打包镜像。

## OPTIONS

此处的所有选项都直接传递给 dracut，相关信息请参考 dracut 文档。

## SEE ALSO

`dracut(8)`

# MKE2FS

## NAME

`mke2fs - 创建 ext2/ext3/ext4 文件系统`

## SYNOPSIS

```
mke2fs [OPTION]
```

```
mke2fs [OPTION] [-c] [-C] [-D] [-E] [-f] [-g] [-G] [-h] [-i] [-I] [-j] [-J] [-k] [-l] [-m] [-M] [-n] [-N] [-o] [-O] [-p] [-P] [-q] [-R] [-s] [-S] [-t] [-T] [-u] [-U] [-v] [-V]
```



```
（注：由于原文中包含大量重复的 OCR 描述，以下针对 MKE2FS 选项的翻译将基于第 2053 页后的清晰文本。）
```

# MKE2FS 选项

## `-c`
在创建系统之前检查设备的坏块。如果指定了此选项，将使用较慢的读写测试代替快速只读测试。

## `-C cluster-size`
指定使用 bigalloc 功能的文件系统的簇大小（字节）。有效的簇大小值为 2048 到 256M。这只有在启用 bigalloc 功能时才能指定。如果启用了 bigalloc，默认簇大小为块大小的 16 倍。

## `-D`
使用直接 I/O 写入磁盘。这会使 `mke2fs` 产生大量的缓冲区内存缓存，可能会影响服务器上运行的其他应用程序。此选项会导致 `mke2fs` 运行速度慢得多，因此使用直接 I/O 是一种权衡。

## `-E extended-options`
设置文件系统的扩展选项。扩展选项用逗号分隔，并可以使用等号 `''` 接受参数。`-E` 选项在早期 `mke2fs` 中用于 `-R`。`-R` 选项仍被接受，但已弃用。支持以下扩展选项：

`mnt_update_interval=interval`
调整初始 mmp 更新间隔（秒）。指定间隔为 0 表示默认间隔。指定的间隔必须小于 300 秒。需要启用 mmp 功能。

`stride`
为具有步长大小块的 RAID 配置文件系统。这是在移动到下一个磁盘之前读取或写入的块数，有时被称为块大小。这主要影响 mkfs 时的文件系统元数据（位图），以避免将其放置在单个磁盘上，这会损害性能。它也可以被块分配器使用。

`stripe_width=stripe-width`
为具有每带条宽块的 RAID 配置文件系统。这通常是 `stride-size * N`，其中 N 是 RAID 中数据磁盘的数量（例如，对于 RAID 5，有一个奇校验磁盘，因此 N 将是阵列磁盘数减 1）。这允许块分配器防止读-修改-在写入数据时，尽可能在 RAID 跨带中写入校验位。

`resize=max-online-resize`
预留足够的空间，以便块描述表能够增长以支持具有 `max-online-resize` 块的文件系统。

`lazy_inode_init[<0 禁用, 1 启用>`
如果启用了 uninit_bg 特性，`m2kfs` 将不会完全初始化 inode 表格。这将显著加快文件系统的初始化速度，但需要内核在首次挂载文件系统时在后台完成文件系统的初始化。如果省略该选项，默认值为 1，即启用惰性 inode 清零。

`lazy_journal_init[<0 禁用, 1 启用>`
如果启用，`m2kfs` 将不会完全清零日志 inode。这会显著加快文件系统的初始化速度，但如果系统在日志被完全覆盖写写之前发生崩溃，可能会带来一些微小的风险。如果省略该选项，默认值为 1，即启用惰性 inode 清零。

`root_owner[=uid:gid]`
指定根目录的数字用户和组 ID。如果未指定 UID:GID，则使用运行 `m2kfs` 的用户和组 ID。在 `m2kfs` 1.42 及之前的版本中，根目录的 UID 和 GID 默认设置为运行 `m2kfs` 命令的用户的 UID 和 GID。`root_owner=` 选项允许显式指定这些值，避免对预期文件系统内容因运行 `m2kfs` 的用户而改变的用户副作用。

`test_fs`
在文件系统超级块中设置一个标志，指示其可以使用实验性内核代码挂载，例如 ext4 文件系统。

`discard`
在 mkfs 阶段尝试丢弃块（这在固态设备和稀疏/精简配置的存储上很有用）。当设备声明丢弃也会清零数据时（在设备操作和返回之前的任何后续读取将返回零），则将所有未清零的 inode 表格标记为已清零。这显著加快了文件系统的初始化。此选项默认开启。

`nodiscard`
在 mkfs 时不丢弃块。

## `- fragment-size`
指定碎片的大小（单位为字节）。

## `-F`
强制 `m2kfs` 创建文件系统，即使设备不是特殊分区，或者其他参数不合理。为了在文件系统似乎在使用或已挂载时仍强制 `m2kfs` 创建文件系统，此选项必须指定两次。

## `-g blocks-per-group`
指定每个组的块数。用户通常没有理由设置此参数，因为默认值对文件系统是最优的（对于在 RAID 阵列上创建文件系统的管理员，最好使用 `-E` 参数，而不是手动操作每组的块数）。此选项通常用于开发测试用例的开发者。如果启用了 bigalloc 特性，`-g` 选项将指定块组中的簇数。

## `-G number-of-groups`
指定在 ext4 文件系统中创建一个更大的虚拟块组（或 "flex-bg group"）。这改进了元数据的局部性和元数据负载的性能。组的数量必须是 2 的幂，且只有在启用了 flex_bg 特性时才能指定。

## `-i bytes-per-inode`
指定每个 inode 的字节比例。`m2kfs` 为磁盘上的每 `bytes-per-inode` 空间创建一个 inode。`bytes-per-inode` 比例越大，创建的 inode 就越少。此值不小于文件系统的块大小，否则创建的 inode 将比预期的多。注意，文件系统创建后无法更改此比例，因此在决定此参数值时要小心。

## `-i inode-size`
指定每个 inode 的大小。`inode-size` 值必须是 2 的幂或大于 128。`inode-size` 越大，inode 表格消耗的空间越多，这会减少文件系统的可用空间并影响性能。在 2.6.10 较旧内核中，可以使用大于 128 字节的 inode 来存储扩展属性，但此类文件系统与旧内核不兼容。大多数文件系统的默认 inode 大小由 `m2fs.conf` 文件 控制，小系统为 128 字节。

## `-j`
创建带有 ext3 日志的文件系统。如果未指定 `-J` 选项，将使用默认的文件系统参数创建一个大小合适的日志（存储在文件系统内部）。注意，你必须使用支持 ext3 的内核来实际创建日志。

## `-J journal-options`
使用命令行指定的选项创建 ext3 日志。日志选项用逗号分隔，并可以使用等号 `=` 取值。支持以下日志选项：

`size=journal-size` 创建内部日志（存储在文件系统内部），大小为 `journal-size` 兆。日志的大小必须至少为 1024 文件系统块（例如使用 1k 块时 1MB，使用 4k 块时 4MB 等），且不能超过 240000 块或文件系统总大小的一半（以较者为准）。

`device=external-journal` 将文件系统附加到外部日志设备。外部日志必须使用与文件系统相同的块大小创建。此外，支持将多个文件系统附加到单个外部日志，Linux 内核和 `e2fsck(8)` 目前尚未共享外部日志。与其指定设备名称，也可以通过 `LABEL=label` 或 `UUID=UUID` 通过超级块中的卷标签或 UUID 定位外部日志。使用 `dumpe2fs(8)` 显示外部日志的卷标签和 UUID。文件系统只能提供 size 或 device 选项之一。

## `-l`
从文件名读取坏块列表。注意坏块列表中的块号必须使用与 `mmfs` 相同的块大小生成。因此，`mmfs` 的 `-c` 选项是格式化前检查磁盘坏块更简单且更不易出错的方法，因为 `mmfs` 会自动将正确参数传递给 `badblocks` 程序。

## `-L new-volume-label`
将文件系统的卷标签设置为 `new-volume-label`。卷标签的最大长度为 16 字节。

## `-m reserved-blocks-percentage`
设置超级用户预留的文件系统百分比。这避免了碎片，并允许在非特权进程写入文件系统后，`syslog(8)` 等 root 守护进程继续运行。默认百分比为 5%。

## `-M last-directory`
设置文件系统的挂载目录。这对于通过检查最后一个目录来确定文件系统位置的工具可能有用。

## `-n`
使 `mmfs` 不创建文件系统，而是显示它创建文件系统将执行的操作。这可以用于确定特定文件备份超级块的位置，只要再次使用原始创建文件系统时传递的 `mke2fs` 参数（当然要带有 `-n` 选项！）。

## `-N number-of-inodes`
覆盖为根预留 inode 数量的默认计算（基于块数和 bytes-per-inode 比例）。这允许用户指定所需的 inode 密度。

## `-o creator-os`
覆盖文件系统“创建操作系统”字段的默认值。`creator` 字段默认设置为编译 `mmfs` 可执行文件时的目标 OS 名称。

## `-O feature`
使用给定的特性（文件系统选项）创建文件系统，覆盖默认选项。启用的特性由 `base_features` 关系设置，该关系位于 `/etc/mmfs.conf` 配置文件的 `[defaults]` 部分，或由 `-T` 选项指定的用例 `[fs_types]` 子节，并由文件系统和用例 `[fs_types]` 子节中的特性进一步修改。详情请参阅 `mmfs(5)` 手册。

文件系统特性将通过编辑器设置，如果未给出此选项，则由正在创建的文件系统类型的 `default_features` 关系或配置文件中的 `[defaults]` 部分设置。文件系统特性由一组用逗号分隔的特性组成，可以启用。要禁用某个特性，只需在特性名称前加脱字符 `'^'` 或减号 `'-'`。具有依赖关系的特性无法移除。伪文件系统特性 `"none"` 将清除所有文件系统特性。

有关可以设置的特性的更多信息，请参 `ext4(5)` 手册。

## `-q`
静默退出。对于在脚本中运行 `mmfs` 。

## `-r revision`
设置新文件系统的版本号。注意 1.2 内核仅支持版本 0。默认创建版本 1 文件系统。

## `-S`
写入超级块和组仅包含描述符。如果所有的超级 和备份 superblock 都损坏，并且需要最后的恢复方法，则此项非常有用。`mke2fs` 会重新初始化 superblock 和组描述符，但不会触碰 inode 表以及块和 inode 位图。在使用此选项后应立即运行 `ef2ck` 程序，且无法保证任何数据可以被恢复。使用此选项时，指定正确的块大小（blocksize）至关重要，否则没有恢复的机会。

## `-t fs-type`
指定要创建的文件系统类型（例如 ext2、ext3、ext4 等）。如果没有指定此选项，`mke2fs` 将根据运行命令的方式（例如使用类似 `mkfs.ext2`、`mkfs.ext3` 等形式的名称）或通过 `/etc/mk2fs.conf` 文件定义的默认值来选择默认类型。这控制了默认使用哪些文件系统选项，该选项基于 `/etc/mk2fs.conf` 中的 `ftypes` 配置段（stanza）来决定的。

如果使用 `-O` 来显式添加或删除应在新创建的文件系统中设置的文件系统选项，则生成的文件系统将不支持所请求的 fs-type。（例如，`mke2fs -t ext3 -O extent /dev/sdXX` 将创建一个 Linux 内核中 ext3 实现不支持的文件系统；而 `mke2fs-ext3 -O ^journal /dev/hdXX` 将创建一个没有日志且不支持 Linux 内核中 ext3 文件系统代码支持的文件系统）。

## `-T usage-type[...]`
指定文件系统的使用方式，以便 `mke2fs` 能够为该用途选择最佳的文件系统参数。使用类型在配置文件 `/etc/mk2fs.conf` 中定义。用户可以使用逗号分隔的列表指定一个或多个使用类型。

如果未指定此选项，`mke2fs` 将根据要创建的文件系统的大小选择单一默认使用类型。如果文件系统大小小于等于 3 兆，`mke2fs` 将使用 floppy 文件系统类型。如果文件系统大小大于 3 兆但小于或等于 512 兆，`mke2fs(8)` 将使用 small 文件系统类型。如果文件系统大小大于或等于 4 字节但小于 16 字节，`mke2fs(8)` 将使用 big 文件系统类型。如果文件系统大小大于或等于 16 字节，`mke2fs(8)` 将使用 huge 文件系统类型。否则，`mke2fs(8)` 将使用 default 文件系统类型。

## `-U UUID`
使用指定的 UUID 创建文件系统。

## `-v`
详细执行。

## `-V`
打印 `mke2fs` 的版本号并退出。

# 环境变量

## `MKE2FS_SYNC`
如果设置为非零整数值，其值将用于确定在 inode 表初始化期间调用 `sync(2)` 的频率。

## `MKE2FS_CONFIG`
确定配置文件的位置（参见 `mke2fs.conf(5)`）。

## `MKE2FS_FIRST_META_BG`
如果设置为非零整数值，其值将用于确定第一个元数据块组（meta block group）。这主要用于调试目的。

## `MKE2FS_DEVICE_SECTSIZ`
如果设置为非零整数值，其值将用于确定设备的物理扇区大小。

## `MKE2FS_SKIP_CHECK_MSG`
如果设置，不显示由于挂载次数或检查间隔引起的文件系统自动检查消息。

# 作者
此版本的 `mke2fs` 由 Theodore Ts’o <tytso@mit.edu> 编写。

# 缺陷
`mke2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统尚未支持碎片（fragments）。可能还有其他。请向作者报告。

# 可用性
**`mke2fs`** 是 `e2fsprogs` 软件包的一部分，可以从 http://e2fsprogs.sourceforge.net 获取。

## 参见
`mke2fs.conf(5)`, `badblocks(8)`, `dumpe2fs(8)`, `e2fsck(8)`, `tune2fs(8)`, `ext4(5)`

# MKFS.BTRFS

## 名称
`mkfs.btrfs` - 创建一个 btrfs 文件系统

# 语法
```
mkfs.btrfs [-A|--alloc <alloc-start>] [-b|--byte-count <byte-count>] [-d|--data <data-profile>] [-f|--force] [-n|--nodesize <nodesize>] [-l|--leafsize <leafsize>] [-L|--label>] [-m|--metadata <metadata profile>] [-M|--mixed] [-s|--sectorsize <sectors>] [-r|--rootdir <rootdir>] [-K|--nodiscard] [-O|--features <feature1>, <feature2...>]
```

## 描述
`mkfs.btrfs` 用于在设备或设备分区上创建 btrfs 文件系统。如果指定了多个设备，btrfs 将使用所有设备。

## 选项
`-A|--alloc <alloc-start>` 指定从开始分配的偏移量。默认值为零。

`-b|--byte-count <byte-count>` 指定文件系统的大小。

`-d|--data <type>` 指定数据如何跨设备分布。有效值为 raid0, raid1, raid5, raid6, raid10 或 single。

`-f|--force` 当检测到现有文件系统时强制覆盖。

`-l|--leafsize <size>` 指定叶节点大小（leafsize）。默认值为 16KB `16384`。

`-L|--label <name>` 为文件系统指定标签。注意名称应小于 256 个字符。

`-m|--metadata <profile>` 指定元数据如何跨设备分布。有效值为 raid0, raid1, raid5, raid6, raid10 或 single。

`-M|--mixed` 将数据块混合在一起以更有效地利用空间。这在较大的文件系统中会产生性能损失。建议用于 1 GiB 或更小的文件系统。

`-s|--sectorsize <size>` 指定扇区大小，即最小分配单元。默认值为页大小。如果扇区大小与页大小不同，创建的文件系统可能无法被内核挂载。因此，除非要在相应页大小的系统上挂载，否则不建议使用此选项。

`-r|--rootdir <rootdir>` 指定复制到新创建的 btrfs 文件系统的目录。注意 `-r` 选项完全在用户态完成，挂载文件系统不需要 root 权限。

`-K|--nodiscard` 默认不执行整个设备的 TRIM 操作。

`-O|--features <feature1>,<feature2...>` 开启的文件系统功能列表。旧内核不支持所有功能。要查看所有功能，请运行 `mkfs.btrfs -O list-all`

`-U|--uuid <UUID>` 使用指定的 UUID 创建文件系统，该 UUID 不得已存在于系统中。

`-V|--version` 打印 `mkfs.btrfs` 版本并退出。

`-h` 打印帮助。

`-n|--nodesize <size>` 指定节点大小，即树块大小。默认值为页大小。`leafsize` 的别名。

# 单位
默认情况下单位是字节，但可以在参数后附加后缀，如 `k` 代表 KBytes，`m` 代表 MBytes...

# 可用性
**`btrfs`** 是 `btrfs-progs` 的一部分。更多信息请参阅 btrfs wiki http://btrfs.wiki.kernel.org/。

# 另
`btrfs(8)`

# mkfs.cramfs

## 名称
`mkfs.cramfs` - 创建压缩 ROM 文件系统

# 语法
```
mkfs.cramfs [options] directory file
```



## 描述

`cramfs` 文件系统上的文件每次对一页进行 `zlib` 压缩，允许随机读取访问。元数据不压缩，但采用一种简洁的表示方式呈现，比传统文件系统更节省空间。

该文件系统故意设计为只读以简化其设计；压缩文件的随机写访问很难实现。`cramfs` 附带了一个工具 (`mkramfs`)，用于将文件打包成新的 `cramfs` 镜像。

文件大小限制在 `16MB` 以下。

文件系统最大大小略小于 `272MB`。（文件系统上的最后一个文件必须在 `256MB` 块之前开始，但可以延伸到之外。）

# 参数

目录即我们想要生成压缩文件系统的目录树的根目录。

文件将包含 `cram` 文件系统，稍后可以挂载。

## 选项

- `-v` 启用详细输出。
- `-E` 将所有警告视为错误，并反映在命令返回值中。
- `-b blocksize` 使用定义的块大小，该大小必须是页大小的倍数。
- `-e edition` 在超级块中使用定义的文件系统版本号。
- `-N big, little, host` 使用定义的字节序。值默认为主机字节 (`host`)。
- `-i file` 将文件插入 `cramfs` 文件系统。
- `-n name` 设置 `cramfs` 文件系统的名称。
- `-p Pad` 按 `512` 字节对齐以启动代码。
- `-s` 此选项被忽略。最初的 `-s` 用于开启目录条目排序。
- `-z` 创建显式空洞。使用此选项需要 `2.3.39` 或更高版本的内核。
- `-V` 显示版本信息并退出。
- `-h` 显示帮助信息并退出。

## 退出状态

`0` 成功
`8` 操作错误，例如无法分配内存

# 另

`mount(8)`, `fsck.cramfs(8)`

# 可用性

示例命令是 `util-linux` 包的一部分，可从 Linux 内核存档中获取

# MKE2FS

## 名称
`mke2fs` - 创建 `ext2`/`ext3`/`ext4` 文件系统

## 语法

```
mke2fs [ -c ] [ -b block-size ] [ -D ] [ -f fragment-size ] [ -g blocks-per-group ] [ -G number-of-groups ] [ -i bytes-per-inode ] [ -I inode ] [ -j ] [ -J journal-options ] [ -N number-of-inodes ] [ -n ] [ -m reserved-blocks-percentage ] [ -o creator-os ] [ -O feature,... ] [ -q ] [ -r fs-revision-level ] [ -E extended-options ] [ -v ] [ -F ] [ -L volume-label ] [ -M last-mounted-directory ] [ -S ] [ -t fs-type ] [ -T usage-type ] [ -U UUID ] [ -V ] device [ blocks-count ]
```

```
mke2fs -O journal_dev [ -b block-size ] [ -L volume-label ] [ -n ] [ -q ] [ -v ] external-journal [ blocks-count ]
```

## 描述

`mke2fs` 用于创建 `ext2`、`ext3` 或 `ext4` 文件系统，通常在磁盘分区中创建。`device` 是对应设备的特殊文件（例如 `/dev/sda`），`blocks-count` 是设备上的块数。如果省略，`mke2fs` 会自动计算文件系统大小。如果用作 `mkfs.ext3` 调用，且指定了 `-j` 选项，则创建一个日志。新创建的文件系统的参数默认值如果未被下面的选项覆盖，将由 `/etc/mke2fs.conf` 文件控制。详见 `mke2fs.conf(5)`。

## 选项

- `-b block-size` 指定以字节为单位的块大小。有效的 `block-size` 值为每块 `1024`、`2048` 和 `4096` 字节。如果省略，`block-size` 将根据文件系统大小和对文件系统的预期用途通过启发式方法确定（见 `-T` 选项）。如果 `block-size` 前有负号（`'-'`），`mke2fs` 将使用启发式方法确定合适的块大小，条件是块大小至少是 `block-size` 的倍数。
- `-c` 在创建文件系统之前检查设备是否有坏块。如果指定了此选项，将使用较慢的读写测试代替快速只读测试。
- `-C cluster-size` 为使用 `bigalloc` 功能的文件系统指定以字节为单位的簇大小。有效的 `cluster-size` 值为 `2048` 到 `256M`。只有在启用 `bigalloc` 时才能指定此值。如果启用了 `bigalloc`，默认簇大小为块大小的 `16` 倍。
- `-D` 在写入磁盘时使用直接 I/O。这可以节省大量的缓冲区缓存内存，可能会影响运行在繁忙服务器上的其他应用程序。然而，此选项将使 `mke2fs` 运行慢得多，使用直接 I/O 是一种权衡。
- `-E extended-options` 为文件系统设置扩展选项。扩展选项用逗号分隔并可以使用等号（`'='`）带任何参数。`-E` 选项在早期 `mke2fs` 版本中使用 `-R`。为了向后兼容，仍然接受 `-R` 选项，但已弃用。支持的扩展选项如下：
  - `mmp_update_interval=interval` 调整初始 MMP 更新间隔（秒）。指定 `0` 使用默认间隔。指定的间隔必须小于 `300` 秒。需要启用 MMP 功能。
  - `stride=stride` 为具有步长的文件系统设置 `stride`。这是在移动到下一个磁盘之前读取或写入的块数，有时被称为块大小。这在单个磁盘上放置文件系统位图时会影响块分配器。
  - `stripe_width=stripe-width` 为具有带宽的文件系统设置带宽。这通常是 `stripe-size * N`，其中 `N` 是 RAID 中数据磁盘的数量（例如 RAID 5 有一个奇校验磁盘，因此 `N` 将是磁盘数减 `1`）。这允许块分配器在写入数据时尽可能避免对 RAID 带宽进行读改写。
  - `resize=max-online-resize` 保留足够的空间，以支持具有在线调整功能的文件组描述符。
  - `lazy_inode_init=<0 禁用, 1 启用>` 如果启用了 `uninit_bg` 功能，节点不会被 `mke2fs` 完全初始化。这会显著加快文件系统的初始化，但需要内核在首次挂载时在后台完成文件系统的初始化。如果省略选项值，默认为 `1` 以启用延迟清零。
  - `lazy_journal_init=<0 禁用, 1 启用>` 如果启用，节点日志不会被 `mke2fs` 完全清零。这会显著加快文件系统的初始化，如果系统在日志被完全覆盖之前崩溃存在微小风险。如果省略选项值，默认为 `1` 以启用延迟日志。
  - `discard` 在 `mkfs` 时尝试释放块（初始释放块对于固态设备和稀疏精制存储很有用）。当设备宣布释放也会清零数据时（释放后的任何读取都会返回零），将所有未清零的节点表标记为已清零。这大大加快了文件系统的初始化。这是默认。
  - `nodiscard` 不在 `mkfs` 时尝试释放块。
- `-f fragment-size` 指定以字节为单位的分块。
- `-F` 强制 `mke2fs` 创建文件系统，即使设备不是块设备上的分区，或者其他参数不合理。为了强制 `mke2fs` 在即使文件系统似乎在使用或已挂载的情况下创建文件系统（非常危险的操作），必须指定两次此选项。
- `-g blocks-per-group` 指定块组中的块数。用户通常没有设置此参数，因为默认值对文件系统是最优的。（对于在 RAID 阵列上创建文件系统的管理员来说，使用 `-E` 选项指定带 RAID 参数比操作每组块数要好。）此选项通常供开发测试用例的开发者。如果启用了 `bigalloc` 功能，则 `-g` 将指定块组中包含的簇数量。
- `-G number-of-groups` 指定在 `ext4` 文件系统中打包的块的数量以创建一个更大的虚拟块组（或 "`flex_bg`"）。这改进了元数据密集型工作负载的局域性（locality）和性能。块组的数量必须是 `2` 的幂，且只有在启用了 `flex_bg` 文件系统时才能指定。
- `-i bytes-per-inode` 指定每个 `inode` 的字节数。`mke2fs` 为磁盘上每 `bytes-per-inode` 字节的空间创建一个 `inode`。`bytes-per-inode` 比例越大，创建的 `inode` 越少。此值不应小于文件系统的块大小，否则创建的 `inode` 数量将超过限制。注意，文件系统创建后无法更改此比例，因此在决定该值时要小心。调整文件系统会更改 `inode` 的数量。
- `-I inode-size` 指定每个 `inode` 的大小。`inode-size` 值必须是 `2` 的幂或等于 `128`。`inode-size` 越大，`inode` 表消耗的空间越多，从而减少文件系统中的可用空间。文件系统创建后无法更改此值。在 `2.6.10` 及更早的内核中，可以使用比 `128` 字节更大的 `inode` 来存储扩展属性以提高性能。在旧内核中，大 `inode` 中的扩展属性不可见，且 `2.4` 内核将不支持此类文件。默认 `inode` 大小由 `mk2fs.conf` 文件控制（对于大多数系统为 `256` 字节，小系统除外）。
- `-j` 创建带有 `ext3` 日志的文件系统。如果未指定 `-J` 选项，将使用默认日志参数创建合适大小的日志（取决于文件系统的大小）存储在文件系统中。注意，你必须使用支持 `ext3` 的内核来实际使用日志。
- `-J journal-options` 使用命令行上指定的选项创建 `ext3` 日志。日志选项用逗号分隔，并可以使用等号（`'='`）带参数。支持以下日志选项：
  - `size=journal-size` 创建一个内部日志（即存储在文件系统内部），大小为 `journal-size` 兆字节。日志的大小至少为 `1024` 块（例如，使用 `1k` 块，`4MB` 使用 `4k` 块等），并且可能不超过 `240,000` 块或文件系统大小的一半（以较小者为准）。
  - `device=external` 将文件系统附加到位于外部的日志。日志可能已经使用与文件系统相同的块大小创建。此外，支持将多个文件系统附加到单个外部日志，Linux 内核和 `efsck(8)` 目前尚未共享外部日志。
  - 与其指定设备名称，也可以通过 `LABEL=label` 或 `UUID=UUID` 通过 `ext2` 超头存储的卷标签或 UUID 来指定外部日志。使用 `dumpe2fs(8)` 显示日志设备的卷标签和 UUID。另见 `tune2fs(8)` 的 `-L` 选项。
  - 文件系统只能给出 `size` 或 `device` 选项之一。
- `-l filename` 从文件名读取坏块列表。注意，块列表中的块号必须使用与 `mke2fs` 相同的块大小生成。因此，`mke2fs` 的 `-c` 选项是格式化之前检查坏块更简单不易出错的方法，`mke2fs` 会将正确的参数传递给 `badblocks` 程序。
- `-L new-volume-label` 设置文件系统的卷标签为 `new-volume-label`。卷标签的最大长度为 `16` 字节。
- `-m reserved-blocks-percentage` 设置为超级用户保留的文件系统块百分比。这避免了碎片，并允许 `root` 所有的守护进程（如 `syslog(8)`）在非特权进程写入文件系统后继续正常运行。默认百分比为 `5%`。
- `-M last-mounted-directory` 设置文件系统的挂载目录。这对于某些保持挂载目录可能有用，确定文件系统应该挂载在哪里。
- `-n` 使 `mke2fs` 不创建文件系统，而是显示如果创建它将会做什么。这可以确定特定文件系统备份超头的位置，只要再次使用最初创建文件系统时传递的 `mke2fs` 参数（在加上 `-n` 选项的情况下！）。
- `-N number-of-inodes` 覆盖文件系统保留 `inode` 数量的计算（基于块数量和 `bytes-per-inode` 比例）。这允许用户指定所需的 `inode` 数量。
- `-o creator-os` 覆盖文件系统“操作系统”字段的默认值。`creator` 字段默认设置为用于编译的 `mke2fs` 可执行文件名称。
- `-O feature[...]` 使用给定的特征（文件系统选项）创建文件系统，覆盖默认特征。默认启用的特征由 `base_features` 关系设置，该关系位于 `/etc/m2fs.conf` 配置文件的 `[defaults]` 节中，或由 `T` 选项指定的用例 `[fs_types]` 子节中，进一步修改文件系统和用例 `[fs_types]` 子节中的特征。更多细节请参 `mke2fs(5)` 手册。`[fs_types]` 节中的文件系统类型特定设置将覆盖 `[defaults]` 中的全局默认值。
- 文件系统特征将使用此选项指定的特征进行进一步编辑；如果没有给出此选项，则使用正在创建的文件系统类型的 `default_features` 关系或配置文件中的 `[defaults]` 节。
- 文件系统特征由一组用逗号分隔的可启用特征列表组成。要禁用某项特征，只需在名称前加脱字符（`^`）或减号（`-'`）。具有依赖关系的特征将无法成功删除。伪文件系统特征“`none`”将清除所有文件系统特征。
- 有关可以设置的特征的更多信息，请参 `ext4(5)` 手册。
- `-q` 静默执行。当 `mke2fs` 在脚本中运行时非常有用。
- `-r revision` 设置新文件系统的修订版本。注意，`1` 内核仅支持 `0` 版本的文件系统。默认创建版本为 `1` 的文件系统。
- `-S` 仅写入超头和组描述符。这在超头和组描述符损坏且需要恢复时非常有用。它会导致 `mke2fs` 不初始化 `inode` 表和块位图。在使用此选项后应立即运行 `efsck` 程序，且不保证数据可以挽救。
- `-fs-type` 指定要创建的文件系统类型（例如 `ext2`, `ext3`, `ext4` 等）。如果未指定此选项，`mke2fs` 将根据运行方式（例如使用 `mk2fs.ext2`、`mk2fs.ext3` 等名称）或通过 `/etc/mk2fs.conf` 定义的默认值来选择。这控制了默认使用的文件系统选项。
- 如果使用 `-O` 选项添加或删除文件系统选项，新创建的文件系统可能不支持请求的 `fs-type`（例如，“`mk2fs -t ext3 -O extent /dev/sdXX` 将创建一个被 Linux 内核 `ext3` 实现不支持的文件系统；而 `mk2fs-ext3 -O ^journal /dev/hdXX` 将创建一个不带日志的文件系统）。
- `-T usage-type[...]` 指定文件系统的用途，以便 `mke2fs` 为该用途选择最优的文件系统参数。支持的用例定义在配置文件 `/etc/mk2fs.conf` 中。用户可以使用逗号分隔列表指定一个或多个用例。
- 如果未指定此选项，`mke2fs` 将根据要创建的文件系统的大小选择单一默认用例。如果文件大小小于或等于 `3 MB`，`mke2fs` 将使用 `floppy` 文件系统类型。如果文件大小大于 `3 MB` 且小于等于 `512 MB`，`mke2fs(8)` 将使用 `small` 文件系统类型。如果文件大小大于或等于 `4 TB` 但小于 `16 TB`，`mke2fs(8)` 将使用 `big` 文件系统类型。如果文件大小大于等于 `16 TB`，`mke2fs(8)` 将使用 `huge` 文件系统类型。否则，`mke2fs(8)` 将使用默认文件系统类型 `default`。
- `-U` 使用指定的 UUID 创建文件系统。
- `-v` 详细执行。
- `-V` 打印 `mk2fs` 的版本号并退出。

# 环境

## `MKE2FS_SYNC`

如果设置为非零整数值，其值将用于确定在初始化 `inode` 表格期间调用 `sync(2)` 的频率。

## `MKE2FS_CONFIG`

确定配置文件的位置（参见 `mke2fs.conf(5)`）。

## `MKE2FS_FIRST_META_BG`

如果设置为非零整数值，其值将用于确定第一个元数据块组（`meta block group`）。
这主要用于调试目的。

## `MKE2FS_DEVICE_SESIZE`

如果设置为非零整数值，其值将用于确定设备的物理扇区大小。

## `MKE2FS_SKIP_CHECK_MSG`

如果设置，则显示因挂载次数或检查间隔引起的文件系统自动检查的消息。

## 作者

此版本的 `mke2fs` 由 Theodore Ts’o <`tytso@mit.edu`> 编写。

# 缺陷

`mke2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统尚未支持碎片（`fragments`）。可能存在其他缺陷。请向作者报告。

# 可用性

`mke2fs` 是 `e2fsprogs` 软件包的一部分，可以从 `http://e2fsprogs.sourceforge.net` 获取。

## 参见

`mke2fs.conf(5)`, `badblocks(8)`, `dumpe2fs(8)`, `e2fsck(8)`, `tune2fs(8)`, `ext4(5)`

# MKE2FS

> 名称

`mke2fs` - 创建 `ext2`/`ext3`/`ext4` 文件系统

## 概要

```
mke2fs [-c] [ -b block-size ] [ -D ] [ -f fragment-size ] [ -g blocks-per-group ] [ -G number-of-groups ] [ -i bytes-per-inode ] [ -I inode ] [ -j ] [ -J journal-options ] [ -N number-of-inodes ] [ -n ] [ -m reserved-blocks-percentage ] [ -o creator-os ] [ -O feature,... ] [ -q ] [ -r fs-revision-level ] [ -E extended-options ] [ -v ] [ -F ] [ -L volume-label ] [ -M last-mounted-directory ] [ -S ] [ -t fs-type ] [ -T usage-type ] [ -U UUID ] [ -V ] device [ blocks-count ]
```

```
mke2fs -O journal_dev [ -b block-size ] [ -L volume-label ] [ -n ] [ -q ] [ -v ] external-journal [ blocks-count ]
```



## 描述

`mke2fs` 用于创建 ext2、ext3 或 ext4 文件系统，通常在磁盘分区中创建。`*device*` 是对应于设备的特殊文件（例如 `/dev/hdXX`），`*blocks-count*` 是设备上的块数。如果省略，`mke2fs` 将自动计算文件系统大小。如果作为 `mkfs.ext3` 调用，则会创建一个日志，就像指定了 `-j` 选项一样。

新创建的文件系统的参数默认值，如果没有被下面列出的选项覆盖，将由 `/etc/mke2fs.conf` 配置文件控制。更多信息请参见 `mke2fs.conf(5)` 手册页。

## 选项

`-b block-size`

以字节为单位指定块的大小。有效的 `block-size` 值为每块 1024、2048 和 4096 字节。如果省略，则根据文件系统大小和文件系统的预期用途启发式确定 `block-size`（参见 `-T` 选项）。如果 `block-size` 前面带有负号（'-'），`mke2fs` 将确定块大小。

`-c`

在创建文件系统之前检查设备是否有坏块。如果指定了此选项，速度将慢得多。

`-C cluster-size`

以字节为单位指定簇的大小。如果启用了 bigalloc 功能，有效的 `cluster-size` 值范围为 2048 到 256M。（详情请参见 `ext4(5)` 手册。）

`-D`

在创建文件系统时使用直接 I/O。这对于稀疏文件和存储很有用。

`-E extended-options`

设置扩展选项。扩展选项用逗号分隔。`-E` 选项仍然支持：

`mp_update_interval`

调整初始更新。指定的间隔必须小于 300 秒。

`stride`

为条带（stripe）配置文件系统。这是每个条带中的块数。

`stripe_width`

为条带宽度（stripe-width）配置文件系统。这是 RAID 中承载数据的磁盘数量（对于 RAID 5，有一个校验盘）。

`resize=max-online-resize`

预留足够的空间以便块组描述符可以增长。

`lazy_atomic_init=<0 禁用, 1 启用>`

如果启用了 uninit_bg 功能，inode 表将不会完全初始化。这加快了文件系统的初始化，但需要内核在后台完成文件系统的初始化。如果省略了该选项，默认为 1。

`lazy_journal_init=<0 禁用, 1 启用>`

如果启用，`mke2fs` 将不会对 inode 进行完全清零。这加快了文件系统的初始化，但系统在此之前崩溃会有很小的风险。如果省略了该选项，默认为 1。

`root_owner=<uid:gid>`

指定根目录的数字用户 ID 和组 ID。如果没有指定 UID:GID，将使用运行 `mke2fs` 的用户和组 ID。在 `mke2fs` 1.42 及之前的版本中，根目录的 UID 和组 ID 默认设置为运行 `mke2fs` 的用户的 UID 和组 ID。`root_owner=` 选项允许显式指定这些值，并为不期望文件系统内容发生的用户避免副作用。

`test_fs`

在文件系统分区中设置标记，指示其可能使用实验性内核代码（例如 ext4 文件系统）挂载。

`discard`

在 mkfs 时尝试丢弃块，这对于固态设备和精简存储很有用。当设备宣布丢弃也会清零（随后的读取返回零），则会将所有未清零的 inode 表标记为清零。这显著加快了文件系统的初始化。这是默认设置。

`nodiscard`

在 mkfs 时不丢弃块。

`-f fragment-size` 以字节为单位指定碎片的大小。

`-F` 即使设备不在分区或块设备上，或者其他参数不合理也强制 `mke2fs` 创建文件系统。为了让 `mke2fs` 即使在文件系统在使用或挂载的情况下也能创建（这是一个非常危险的操作），必须指定两次此选项。

`-g blocks-per-group` 指定块组中的块数。用户通常没有设置此参数的理由，因为默认值是最优的。此选项通常供开发测试用例的开发者。如果启用了 bigalloc 功能，`-g` 选项

将指定块组中的簇数量。

`-G number-of-groups` 在 ext4 文件系统中创建一个更大的虚拟块组（或“flex-bg 组”）。这可以提高元数据的局部性，并提升元数据工作负载下的性能。组组的数量必须是 2 的幂次，且只有在启用了 `flex_bg` 文件系统功能时才能指定。

`-bytes-per-inode` 指定每个索引的字节数。`mkefs` 会为磁盘上每 `bytes-per-inode` 字节的空间创建一个索引（inode）。`bytes-per-inode` 比例越大，创建的索引数量就越少。此值不应小于文件系统的块大小（blocksize），因为这样创建的索引数量将超过实际使用的数量。请注意，在文件系统创建后无法更改此比例，因此在决定此参数的值时要小心。

`-i inode-size` 指定每个索引的大小。`inode-size` 值必须是 2 的幂次，且大于或等于 128。`inode-size` 越大，索引表消耗的空间就越多，这会减少文件系统的可用空间并可能对性能产生负面影响。文件系统创建后无法更改此值。在内核 2.6.10 和某些早期内核中，可以使用大于 128 字节的索引来存储扩展属性以提高性能。旧版内核不可见大索引中的扩展属性，且 2.4 内核将不支持此类文件。默认索引大小由 `mkefs.conf` 文件控制。大多数文件系统的默认大小为 256 字节，小型文件系统除外，其大小为 128 字节。

`-j` 使用 ext3 日志创建文件系统。如果未指定 `-J` 选项，将使用默认日志参数来根据文件系统的大小创建一个合适大小的日志，并存储在文件系统内部。请注意，你必须使用支持 ext3 的内核才能实际利用日志功能。

`-J journal-options` 使用命令行上指定的选项创建 ext3 日志。日志选项用逗号分隔，并可以使用等号（'='）带入参数。支持以下日志选项：
    - `size=journal-size`：创建一个大小为 `journal-size` MB 的内部日志（即存储在文件系统内部）。日志的大小至少为 1024 个文件系统块（例如，如果使用 1kb 则为 1MB，使用 4ks 则为 4MB 等），且不能超过 10,240,000 个文件系统块或总文件大小的一半（以较者为准）。
    - `device=external-journal`：将文件系统挂载到位于 `external-journal` 的日志块设备。外部日志必须已使用 `mkefs -O journal external-journal` 命令创建。注意，`external-journal` 创建时使用的块大小必须与新文件系统相同。此外，支持将多个文件系统挂接到单个外部日志，但 Linux 内核和 `e2fsck(8)` 目前尚未共享外部日志。

`external-journal` 也可以通过 `LABEL=label` 或 `UUID=UUID` 指定，以便通过日志开始处 ext2 超数据块中存储的卷卷标或 UUID 来定位外部日志。使用 `dumpe2fs(8)` 显示设备的卷标和 UUID。另见 `tune2fs(8)` 的 `-L` 选项。

一个文件系统只能提供 `size` 或 `device` 选项中的一个。

`-l` 从文件名读取坏块列表。注意，坏块列表中的块号必须使用与 `m2fs` 相同的块大小生成。因此，`m2fs` 的 `-c` 选项是在格式前检查磁盘坏块的一种更简单且不易出错的方法，因为 `m2fs` 会自动为 `badblocks` 程序解析正确的参数。

`-L new-volume-label` 将文件系统的卷标设置为 `new-volume-label`。卷标的最大长度为 16 字节。

`-m` 设置 `reserved-blocks-percentage` 指定预留给超级用户的文件系统百分比。这可以避免碎片，并确保 root 拥有的守护进程（如 `syslog(8)`）在非特权进程被阻止写入文件系统后仍能正常运行。默认百分比为 5%。

`-M last-mounted-directory` 设置文件系统的挂载目录。这对于某些通过避开挂载目录来确定文件系统应该挂载在何处的工具可能有用。

`-n` 使 `m2fs` 不创建文件系统，而是显示如果创建将执行的操作。这可以用于确定特定文件系统的备份超数据块（superblock）的位置，前提是再次使用原始创建文件系统时传递的 `m2fs` 参数（当然，还要加上 `-n` 选项！）。

`-N number-of-inodes` 覆盖文件系统预留索引数量的默认计算（基于块数量和 `bytes-per-inode` 比例）。这允许用户指定所需的索引数量。

`-o creator-os` 覆盖文件系统“操作系统”特性的默认值。`creator` 字段由编译 `m2fs` 可执行文件时的目标操作系统名称设置。

`-O feature[...]` 使用给定的特征（文件系统选项）创建文件系统，覆盖默认选项。启用的特征由 `base_features` 关系设置，该关系可能位于 `/etc/m2fs.conf` 配置文件的 `[defaults]` 部分，也可能位于 `-T` 选项指定的用法页的 `[fs_types]` 子节中，并由文件系统和用例的 `[fs_types]` 节中发现的特征进一步修改。详情请参阅 `m2fs(5)` 手册。在 `[fs_types]` 节中找到的文件系统特定设置将覆盖 `[defaults]` 中的默认设置。

特征集由一组用逗号分隔的待启用特征组成。要禁用某个特征，只需在特征名称前加上插入符号（'^'）或减号（'-'）。特征“none”将清除所有特征。有关可设置的特征的更多详细信息，请参阅 `ext4` 手册页。

`-q` 静默退出。适用于 `m2fs` 在脚本中运行。

`-r revision` 设置新文件系统的版本。注意，2内核支持版本 0。默认创建版本 1。

`-S` 仅写入超数据块和组描述符。当超数据块和组位图损坏时非常有用。在使用此选项后应立即运行 `e2fsck` 程序并指定正确的块大小。

`-fstype` 指定要创建的文件系统类型（例如 ext2, ext3, ext4 等）。如果未指定此选项，`mk2fs` 将根据运行命令（例如使用 `mkfs.ext2`、`mkfs.ext3` 等名称）或 `/etc/mk2fs.conf` 文件定义的默认值来选择类型。

如果使用 `-O` 选项添加或删除新创建文件系统的文件系统选项，生成的文件系统可能不支持请求的 `fstype`（例如，“mk2fs -t ext3 -O extent /dev/sdXX”创建的文件系统不支持内核中的 ext3 实现；而“mkfs.ext3 -O ^journal /dev/hdXX”创建的文件系统没有日志，不支持内核中的 ext3 文件系统）。

`-T usage-type[...]` 指定文件系统的用途，以便 `mk2fs` 为该用途选择最优的文件系统参数。`/etc/mk2fs.conf` 中支持的用法类型。用户可以使用逗号列表指定一个或多个用法。如果未指定此选项，`mk2fs` 将根据要创建的文件系统的大小选择单一默认用法。如果文件系统大小小于或等于 3 MB，`mk2fs` 将使用 `floppy` 类型。如果文件系统大小大于 3 MB 且小于等于 512 MB，`mk2fs(8)` 将使用 `small` 类型。如果文件系统大小大于或等于 4 TB 且小于 16 TB，`mk2fs(8)` 将使用 `big` 类型。如果文件系统大小大于或等于 16 TB，`mk2fs(8)` 将使用 `huge` 类型。否则，`mk2fs(8)` 将使用默认类型 `default`。

`-U UUID` 使用指定的 UUID 创建文件系统。

`-v` 详细执行。

`-V` 打印 `mk2fs` 的版本并退出。

# 环境

## `MKE2FS_SYNC`

如果设置为非零整数值，则该值将用于确定在 inode 格初始化期间调用 `sync(2)` 的频率。

## `MKE2FS_CONFIG`

确定配置文件的位置（参见 `mke2fs.conf(5)`）。

## `MKE2FS_FIRST_META_BG`

如果设置为非零整数值，则该值将用于确定第一个元数据块组（meta block group）。
这主要用于调试。

## `MKE2FS_DEVICE_SESIZE`

如果设置为非零整数值，则该值将用于确定设备的物理扇区大小。

## `MKE2FS_SKIP_CHECK_MSG`

如果设置，则不显示由于挂载次数或检查间隔导致的文件系统自动检查的消息。

# way

此版本的 `mke2fs` 由 Theodore Ts’o <tytso@mit.edu> 编写。

# 缺陷

`mke2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统尚不支持碎片（fragments）。可能还有其他此类问题。请向作者报告。

# 可用性

`mke2fs` 是 e2fsprogs 包的组件，可以在 http://e2fsprogs.sourceforge.net 获取。

## 参见

`mke2fs.conf(5)`, `badblocks(8)`, `dumpe2fs(8)`, `e2fsck(8)`, `tune2fs(8)`, `ext4(5)`

# MKFS

### 名字

`mkfs` - 构建 Linux 文件系统

## 概要

```
mkfs [options] [-t type] [fs-options] device [size]
```

## 描述

`mkfs` 用于在设备（通常是硬盘分区）上构建 Linux 文件系统。`*device*` 参数可以是设备名称（例如 `/dev/hda1`, `/dev/sdb2`），也可以是包含该文件系统的普通文件。`*size*` 参数是用于文件系统的块分数。

`mkfs` 返回的退出码在成功时为 0，失败时为 1。

实际上，`mkfs` 仅仅是 Linux 下可用的各种文件系统构建器（`mkfs./type`）的前端。程序在查找特定于文件系统的构建器时，会在多个目录中进行，例如 `/sbin`, `/sbin/fs`, `/sbin/fs.d`, `/etc/fs` 等（精确列表在编译时定义，但至少包含 `/sbin` 和 `/sbin/fs`），最后在 `PATH` 环境变量列出的目录中查找。更多细节请参见特定构建器的手册页。

## 选项

`-t, --type` 指定要构建的文件系统类型。如果没有指定，则使用默认文件系统类型（当前为 ext2）。

`fs-options` 传递给实际文件系统构建器的特定系统选项。虽然不保证，但大多数文件系统构建器都支持以下选项。

`-V, --verbose` 生成详细输出，包括执行的所有特定于文件系统的命令。多次指定此选项将抑制任何特定文件系统命令的执行。这实际上对于测试非常有用。

`-V, --version` 显示版本信息并退出。（当 `-V` 是唯一参数时，它仅显示版本信息，否则它将作为 --verbose 运行。）

`-h, --help` 显示帮助并退出。

# 缺陷

所有通用选项必须位于特定文件系统选项之前，且不能与之合并。某些特定文件系统的程序不支持 `-V`（详细）选项，且不返回有意义的退出码。此外，某些特定文件系统的程序不会自动检测设备大小，并要求指定 `size` 参数。

## 作者

David Engel (`david@ods.com`) Fred N. van Kempen (`waltje@uwalt.nl.mugnet.org`) Ron Sommeling (`sommel@sci.kun.nl`) 本手册页页廉耻地改用了 Remy Card 针对 ext2 文件系统的版本。

## 参见

`fs(5)`, `badblocks(8)`, `fschk(8)`, `mkdosfs(8)`, `mke2fs(8)`, `mkfs.bfs(8)`, `mkfs.ext2(8)`, `mkfs.ext3(8)`, `mkfs.ext4(8)`, `mkfs.minix(8)`, `mkfs.msdos(8)`, `mkfs.vfat(8)`, `mkfs.xfs(8)`, `mkfs.xiafs(8)`

# 可用性

`mkfs` 命令是 util-linux 包的组成，可以在 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# MKFS.MINIX

### 名字

`mkfs.minix` - 创建 Minix 文件系统

## 概要

```
mkfs.minix [-c|-l filename] [-n length] [-i inodecount] [-v] device [size-in-blocks]
```

## 描述

`mkfs.minix` 在设备（通常是磁盘分区）上创建一个 MINIX 文件系统。设备通常如下形式：

- `/dev/hda1-8` (IDE 磁盘 1)
- `/dev/hdb1-8` (IDE 磁盘 2)
- `/dev/sda1-8` (SCSI 磁盘 1)
- `/dev/sdb1-8` (SCSI 磁盘 2)

`size-blocks` 参数是所需的文件系统大小，以块为单位。它仅为了向下兼容。如果忽略，大小将自动确定。仅允许大于 10 且小于 65536 的块数。

## 选项

`-c` 在创建文件系统之前检查设备的坏块。如果发现任何坏块，将打印计数。

`-n length` 指定文件系统的最大长度。允许的值只有 14 和 30。默认值为 30。

`-i inodecount` 指定文件系统的 inode 数量。

`-l filename` 从文件中读取坏块列表。

`-1` 创建 Minix 1 版本的文件系统。

`-2` 创建 Minix 2 版本的文件系统。

`-3` 创建 Minix 3 版本的文件系统。

# 退出码

`mkfs.minix` 返回的退出码之一如下：

- `0` 无错误
- `8` 操作错误
- `16` 语法错误

## 参见

`mkfs(8)`, `fsck(8)`, `reboot(8)`

# 可用性

`mkfs.minix` 命令是 util-linux 包的组件，可以在 `util-linux/` 处（同上）获取。

# MKFS.FAT

### 名字

`mkfs.fat` - 在 Linux 下创建 MS-DOS 文件系统

## 概要
```



`mkfs.fat` `[-a ]` `[-A ]` `[-b sector-of-backup ]` `[-c ]` `[-l filename ]` `[-C ]` `[-f number-of-FATs ]` `[-F FAT-size ]` `[-h number-of-hidden-sectors ]` `[-I ]` `[-m message-file ]` `[-v volume-id ]` `[-n volume-name ]` `[-r root-dir-entries ]` `[-R number-reserved-sectors ]` `[-s sectors-per-cluster ]` `[-S logical-sector-size ]` `[-v device ]` `[ block-count ]`

## 描述

**`mkfs.fat`** 用于设备（通常是磁盘分区）上创建 MS-DOS 文件系统。`*device*` 是对应的设备（例如 `/dev/XX`）。`*block-count*` 是设备上的块数。如果忽略，**`mkfs.fat`** 将自动确定文件系统的大小。

## 选项

`-a` 使用 Atari 变体创建 MS-DOS 文件系统。如果 `mkfs.fat` 在 Atari 上运行，则启用此项；此选项禁用 Atari 格式。

`-b sector-of-backup` 选择 FAT32 备份引导扇区的位置。取决于保留扇区的数量，但通常为 6。备份必须在保留扇区的范围内。

`-c` 在创建文件系统之前检查坏块。

`-C` 创建命令行给的文件，并将要创建的文件系统写入。这可以用于在文件而非真实设备上创建新文件系统，并提前使用 **`dd`** 创建大小合适的文件。使用此选项时必须给出 `*block-count*`，否则将不知道文件系统的预期大小。生成的文件是一个稀疏文件，仅包含元数据区域（引导扇区、FAT 和根目录）。数据部分不会存储在磁盘，但文件将具有正确的大小。生成的文件以后可以拷贝到软盘或其他设备，或者挂载循环设备。

`-f number-of-FATs` 指定 FAT 的数量。

`-F FAT-size` 指定簇大小。可以通过 **`-F`** 选项进行覆盖。

`-h number-of-hidden-sectors` 选择卷中隐藏扇区的数量。显然某些数字相机带有

`-I` 通常对于除了小文件系统以外的文件系统，**`mkfs.fat`** 将所有数据结构对齐到簇大小，这在 RAID、闪存媒体或大型硬盘上可能会导致性能下降。较大的文件系统通过增加簇大小来管理。在 Atari 格式下，会生成一个兼容 Atari 的文件系统序列号，且12 位 FAT 仅用于软盘大小（720k, 1.2M, 1.44M, 2.88M）的文件系统，否则使用 16 位 FAT。

`-m message-file` 忽略引导消息。

`-n volume-id` 指定卷 ID。

`-n volume-name` 指定卷名。

`- root-dir-entries` 指定根目录项。

`-R number-reserved-sectors` 指定保留扇区的数量。

`-s sectors-per-cluster` 指定每个簇的扇区数。

`-S logical-sector-size` 指定逻辑扇区大小。

`-v` 指定设备。

## `-i volume-id`
设置新创建的文件系统的卷 ID；`volume-id` 是一个 32 位十六进制数（例如 `2e24ec82`）。默认值是一个取决于文件系统创建时间的数字。

固定磁盘设备通常会被分区，默认情况下，你不允许在整个设备上创建文件系统。`mkfs.fat` 会报错并告诉你它拒绝工作。在 MO 磁盘（光刻写磁盘）上情况有所不同。MO 磁盘并不总是需要分区的，文件系统可以直接作用于整个磁盘。在其他操作系统中，这被称为“超级软盘”（superfloppy）格式。

此开关将强制 `mkfs.fat` 正常工作。

## `-l filename`
读取 `filename` 的坏块列表。

## `-m message-file`
设置用户在尝试在没有正确安装操作系统的情况下启动此文件系统时收到的消息。一旦换行符转换为回车换行符组合并扩展制表符后，消息文件不得超过 418 字节。如果文件名为连字符 (`-`)，则从标准输入读取文本。

## `-n volume-name`
设置文件系统的卷名（标签）。卷名长度最多可达 11 个字符。默认情况下没有标签。

## `-r root-dir-entries`
选择根目录中可用条目的数量。软盘默认为 112 或 224，硬盘默认为 512。

## `-R number-of-reserved-sectors`
选择预留扇的数量。对于 FAT32，至少需要 2 个预留分区，默认值为 32。否则，默认值为 1（仅限引导区）。

## `-s sectors-per-cluster`
指定每个簇的磁盘扇区数。必须是 2 的幂，即 1, 2, 4, 8, ... 128。

## `-S logical-sector-size`
指定每个逻辑扇区的字节数。必须是 2 的幂且大于或等于 512，例如 512, 1024, 2048, 4096, 8192, 16384, 32768。

## `-v`
详细执行。

## BUGS
`mkfs.fat` 无法创建可引导的文件系统。由于各种原因，这并不像你乍初看起来那么简单，并且已经讨论讨论过了。`mkfs.fat` 简单就是不支持它。;)

## AUTHOR
Dave Hudson - `<d@humbug.demon.co.uk>`; 由 Peter Anvin `<hpa@yggdrasil.com>` 修改。由 Roman Hodek `<roman@hodek.net>` 为 Debian GNU/Linux 修复和新增。

# ACKNOWLEDGMENTS
`mkfs.fat` 基于 `mke2fs` 的代码（由 Remy Card - `<card@masi.dbp.fr>` 编写），而该代码本身基于 `mkfs`（由 Linus Torvalds - `<torvalds@cs.helsinki.fi>` 编写）。

## SEE ALSO
`fsck.fat(8)`, `fatlabel(8)`, `mkfs(8)`

# MKFS.FAT
## NAME
`mkfs.fat` - 在 Linux 下创建 MS-DOS 文件系统

## SYNOPSIS
`mkfs.fat [-a ] [ -A ] [ -b sector-of-backup ] [ -c ] [ -l filename ] [ -C ] [ -f number-of-FATs ] [ -F FAT-size ] [ -h number-of-hidden-sectors ] [ -i volume-id ] [ -I ] [ -m message-file ] [ -n volume-name ] [ -r root-dir-entries ] [ -R number-of-reserved-sectors ] [ -s sectors-per-cluster ] [ -S logical-sector-size ] [ -v ] device [ block-count ]`

## DESCRIPTION
**`mkfs.fat`** 用于在 Linux 的设备（通常是磁盘分区）上创建 MS-DOS 文件系统。`*device*` 是对应设备的特殊文件（例如 `/dev/hdXX`）。`*block-count*` 是设备上的块数。如果省略，`mkfs.fat` 会自动确定文件系统的大小。

## OPTIONS
通常情况下，对于除小文件系统以外的所有文件系统，`mkfs.fat` 将所有数据结构与簇大小对齐，以确保只要分区对齐，文件系统中的所有数据结构也会对齐。此选项将禁用对齐；可能会提供额外的簇存储帮助，但代价是 RAID、闪存介质或大扇区硬盘上的性能大幅下降。

# 错误

**`mkfs.fat`** 无法创建可引导的文件系统。由于各种原因，这并不如你初看时那么简单，并且已经经过过很多讨论。**`mkfs.fat`** 简单地不支持它 ;)

## 作者

Dave Hudson - `<d@humbug.demon.co.uk>`；由 Peter Anvin `<hpa@yggdrasil.com>` 修改。Debian GNU/Linux 由 Roman Hodek `<roman@hodek.net>` 修复和添加。

# 致谢

`mkfs.fat` 基于 `mke2fs` 的代码（由 Remy Card 编写 - `<card@masi.dbp.fr>`），而该代码又基于 `mkfs`（由 Linus Torvalds 编写 - `<torvalds@cs.helsinki.fi>`）。

## 参见

`fsck.fat(8)`, `fatlabel(8)`, `mkfs(8)`

# mkfs.xfs

> 名字

`mkfs.xfs` - 构建 XFS 文件系统

## 概要

```
mkfs.xfs [ -b block_size ] [ -m global_metadata_options ] [ -d data_section_options ] [ -f ] [ -i inode_options ] [ -l log_section_options ] [ -n naming_options ] [ -p profile ] [ -q ] [ -r realtime_section_options ] [ -s sector_size ] [ -L label ] [ -N -K ] device mkfs.xfs -V
```

## 描述

`mkfs.xfs` 通过使用命令行参数中的值写入一个特殊文件来构建 XFS 文件系统。当 `mkfs(8)` 收到 `-t xfs` 选项时，会自动调用它。

在最简单（也是最常用）的形式中，文件系统的大小由驱动器决定。例如，要在第一个 SCSI 磁盘的第一个分区上创建一个带有内部日志的文件系统，请使用：

`mkfs.xfs /dev/sda1`

元数据日志可以放置在任何其他设备上以减少磁盘寻道次数。要在第一个 SCSI 磁盘的第一个分区上创建一个文件系统，其 10000 块大小日志位于第二个 SCSI 磁盘的第一个分区上，请使用：

`mkfs.xfs -logdev=/dev/sdb1,size=10000b /dev/sda1`

参数列表中的每个选项元素如果有多个子选项适用于同一个选项，则可以多个用逗号分隔的子选项给出。等价地，每个主选项可以多次给出并带有不同的子选项。例如，`-i internal,size=10000b` 和 `-i internal -l size=10000b` 是等价的。

在下面的描述中，大小以扇区、字节、块、KB、MB、GB 等为单位给出。如果以 `0x` 或 `0X` 开头，则大小被视为十六进制；如果以 `0` 开头，则视为八进制；否则被视为十进制。以下列表列出了可能的乘法后缀：

- `s` - 乘以扇区大小（默认 = 512，下方的 `-s` 选项）。
- `b` - 乘以文件系统块大小（默认 = 4K，下方的 `-b` 选项）。
- `k` - 乘以一个千字节（1,024 字节）。
- `m` - 乘以一个兆字节（1,048,576 字节）。
- `g` - 乘以一个吉字节（1,073,741,824 字节）。
- `t` - 乘以一个太字节（1,099,511,627,776 字节）。
- `p` - 乘以一个拍字节（1,024 太字节）。
- `e` - 乘以一个艾字节（1,048,576 太字节）。

## 选项

`-b block_size_options`
此选项指定基本块大小。有效的块大小为 512、1024、2048 或 4096 字节。

`-m global_metadata_options`
此选项指定全局元数据选项。有效的元数据选项有：

`-d data_section_options`
此选项指定数据分区选项。有效的选项有：

- `-f`
强制在设备上创建文件系统。

- `-i inode_options`
此选项指定 inode 选项。有效的选项有：

- `-l log_section_options`
此选项指定日志分区选项。有效的选项有：

- `-n naming_options`
此选项指定命名选项。有效的选项有：

- `-p profile`
此选项指定配置（profile）。有效的配置有：

- `-q`
静默模式。

- `-r realtime_section_options`
此选项指定实时分区选项。有效的选项有：

- `-s sector_size`
此选项指定扇区大小。有效的扇区大小为：

- `-L label`
此选项设置文件系统的标签。

- `-N`
不初始化日志。

- `-K`
不初始化数据块。

`-V`
显示版本信息并退出。

- 当设备上检测到现有系统时，强制覆盖。默认情况下，如果 `mkfs.xfs` 怀疑设备上存在文件系统或分区，它将不会写入该设备。

- `-i inode_options` 此选项指定文件系统的 inode 大小以及其他 inode 分配参数。XFS inode 包含一个固定大小的部分和一个可变大小的部分。可变部分的大小受此选项的影响，可以包含：目录数据（用于小型目录）；属性数据（用于小型属性集）；符号链接数据（用于小型链接）；文件的 extent 列表（用于 extent 较的文件）；以及描述文件 extent 位置的树根（用于 extent 多的文件）。有效的 `inode_options` 有：

  `size=value | log=value | perblock=value`

`inode` 大小可以通过 `size=` 指定为一个值，或者通过 `log=` 指定一个以 2 为底的对数值，或者通过 `perblock=` 指定与文件系统块大小匹配的数值。最小（也是默认）值为 256 字节。最大值为 2048 (KiB)，但受限于 inode 大小不能超过文件系统块大小的一半。

XFS 内部使用 64 位 inode 编号；然而，inode 编号的位数受文件系统几何结构的影响。实践中，文件系统的大小和 inode 大小是主要因素。Linux 内核（32 位硬件平台）和大多数应用程序目前无法处理大于 32 位的 inode 编号，因此如果命令行没有给出 inode 大小，`mkfs.xfs` 将尝试选择一个使 inode 小于 32 位的大小。如果指定了 inode 大小，或者文件系统足够大，`mkfs.xfs` 将在这将创建大于 32 位的 inode 编号时发出警告。

  `maxpct=value`

  `align=value` 用于指定 inode 分配是否对齐。该值为 0 或 1，1 表示分配了 inode。如果省略该值，则默认为 1。默认情况下 inode 是对齐的。对齐的 inode 访问比未对齐的访问通常更高效；对齐必须在创建文件系统时确定，因为当文件系统需要由没有 inode 对齐功能的 IRIX 版本挂载时，可以用来关闭 inode 对齐（6.2 之前的任何版本的 IRIX，以及没有 XFS 补丁的 IRIX 6.2）。

### # `attr=value`

这用于指定要使用的扩展属性内联分配策略版本。默认为 2，它使用一种高效算法来管理属性和 extent 数据之间的可用内联 inode 空间。

之前的版本 1 为属性和 extent 数据保留了固定区域，用于与比 2.6.16 更旧的内核后兼容。

### # `proj32bit=value`

这用于启用 32 位项目配额标识符。该值为 0 或 1，1 表示启用 32 位 projoid。如果省略该值，则默认为 1。（此默认值在 3.2.0 版本中已更改）。

- `-log_section_options` 这些选项指定文件系统日志区（log section）的位置、大小和其他参数。有效的 `log_section_options` 有：

### # `internal=value`

这用于指定日志区是数据区的一部分，而不是另一个设备或逻辑卷。该值为 0 或 1，1 表示日志是内部的。如果省略该值，则默认为 1。

### # `logdev=device`

这用于指定日志区应位于与数据区分离的设备上。`internal=1` 和 `logdev` 选项互斥斥。

### # `size=value`

这用于指定日志区的大小。
如果日志包含数据区内且未指定 `size`，`mkfs.xfs` 将尝试根据文件系统的大小选择合适的日志大小。实际日志取决于文件系统块大小和目录块大小。
否则，只有当文件系统日志区占据的空间小于文件空间时，才需要 `size` 子选项。该值以字节或块为单位指定，带有 `b` 后缀表示乘以文件系统块大小，如上所述。日志的覆盖最大值为 512。在某些文件系统块大小、inode 大和小目录块大小的组合下，最小日志大小大于 512。

### # `version=value`

这指定日志的版本。当前默认值为 2，它允许更大的日志缓冲区，并支持条带对齐日志写入（下文的 `sunit` 和 `options`）。

之前的版本 1 限于 32k 日志缓冲区且不支持条带对齐写入，用于与非常旧的 2.4 内核后兼容。

### # `sunit=value`

这指定了用于日志的对齐方式。该值必须以 512 字节块为单位指定。使用 `su` 子选项以字节为单位指定日志单元大小。日志写入将在此边界上对齐并向上取整到该边界。在某些配置下（如软件 RAID5），当 `sunit` 指定为文件系统块大时，性能会有提高。等的字节值必须是文件系统块大小的倍数。如果指定了日志 `junit` 子选项，将自动选择版本 2 日志。
`su` 子选项是使用 `junit` 的替代方案。

```
su=value
```

这用于指定日志条带。该值必须以字节指定（通常带有 `s` 或 `b` 后缀）。该值必须是文件系统块大小的倍数。如果指定了日志 `su` 子选项，将自动选择版本 2 日志。

```
lazy_count=value
```

这更改了在 superblock 中记录持久化计数器的方法。在元数据密集型工作负载下，这些计数器的更新频率足够到会导致 superblock 更新成为瓶颈。该值可以是 0 或 1。使用 `lazy_count=1` 时，每次更改都不会修改或记录 superblock。相反，在文件系统的其他部分保留了足够的信息，以便在不需要在 superblock 中它们的情况下维护持久化计数器值。这在某些配置上显著提升了性能。默认值为 1（开启），因此对于不支持该旧旧内核，你必须指定 `lazy_count=0` 来禁用此功能。

- `-n naming_options` 这些选项指定文件系统命名区（目录区）的版本和大小参数。有效的 `naming_options` 有：

```
size=value | log=value
```



块大小通过 `size=` 指定为字节值，或通过 `log=` 指定为以 2 为底的对数。它必须是 2 的幂且不能小于文件系统块大小。版本 2 的默认值为 4096 字节 (4 KiB)，除非文件系统块大小大于 4096，此时 `size` 与文件系统块大小相同。

`version=value`

命名（目录）值可以是 `ci` 或不指定。对于版本 2 目录，块大小可以是从文件系统块大小到 65536 的任意 2 的幂。`version=ci` 启用 ASCII 不区分大小写的文件查找，且文件名保留大小写。注意：不支持版本 1 目录。

`ftype=value`

此功能允许将 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。此功能允许 inode 存储在目录结构中。该值可以是 0 或 1。通过 `ftype` 启用时，此功能可以关闭。- -n `naming_options` 这些选项指定文件系统命名（目录）区的版本和大小参数。有效的 `naming_options` 有：-p `protofile` 这里的 `protofile` 内容：

```
1 /dev/disk
2 872
3 d--777
4 usr--777
5 /bin/sh
6 n--755
7 8--644
9 0 c--644
10 slink d644
11 /a/symbolic/link
12 : This is a content line
13 $
14 $
```

当文件是一个目录时，`mkfs.xfs` 命令会创建点 `.` 和双点 `..` 条目，并在一个递归管理器中读取目录内所有条目的名称列表和文件规范。配置文件的扫描始终会以美元符号 `$` 结束。

## -q

安静选项。通常情况下，`mkfs.xfs` 会打印要构建的文件系统参数；`-q` 标志会抑制此输出。

## -r realtime_section_options

这些选项指定文件系统实时区域（real-time section）的位置、大小和其他参数。有效的 `realtime_section_options` 如下：

### rtdev=device

此用于指定包含文件系统实时区域的设备。子选项值是块设备的名称。

### extsize=value

此用于指定文件系统实时区域块的大小。此值必须是文件系统块大小的倍数。允许的最小大小为文件系统块大小或 4 KiB（以较大者为准）；默认大小为条带卷的条带宽度，或非条带卷的 64 KiB；允许的最大大小为 1 GiB。应应仔细选择实时范围（extent）大小，以匹配所用物理介质的参数。

### size=value

此用于指定实时区域的大小。只有当文件系统实时区域应该小于包含该区域的分区或逻辑卷的大小时，才需要此子选项。

### noalign

此选项禁用条带大小检测，强制使用无条带结构的实时设备。

- -s `sector_size` 此选项指定文件系统的基本扇区大小。`sector_size` 可以通过 `size=value` 以字节值的形式指定，也可以通过 `log=value` 以基对数值的形式指定。默认 `sector_size` 为 512 字节。`size` 的最小值为 512；最大值为 32768 (32 KiB)。`sector_size` 必须是 2 的幂，且不能大于文件系统块大小。
- -L 设置文件系统标签。XFS 文件系统标签长度为 12 个字符；如果标签超过 12 个字符，`mkfs.xfs` 将不会继续创建文件系统。请参考 `mount(8)` 和 `xfs_admin(8)` 手册页获取更多信息。
- -N 打印文件系统参数而不实际创建文件系统。
- -K 不在 `mkfs` 期间尝试丢弃块。
- -V 打印版本号并退出。

## SEE ALSO

`xfs(5)`, `mkfs(8)`, `mount(8)`, `xfs_info(8)`, `xfs_admin(8)`。

## BUGS

使用原型文件时，无法指定硬链接。

## MKHOMEDIR_HELPER

### NAME

`mkhomedir_helper` - 创建主目录的辅助二进制文件

## SYNOPSIS

```
mkhomedir_helper {user} [umask [ path-to-skel ]
```

## DESCRIPTION

`mkhomedir_helper` 是 `mkhomedir` 模块的辅助程序，用于创建主目录并填充指定的 `skel` 目录内容。

`umask` 的默认值为 022，`path-to-skel` 的默认值为 `/etc/skel`。辅助程序与模块分离，以便允许 SELinux 作用域直接访问主目录的内容。在执行 `mkhomedir` 时发生 SELinux 作用域转换。

如果主目录已存在，辅助程序将不会触碰。

## SEE ALSO

`mkhomedir(8)`

## AUTHOR

由 Tomas Mraz 编写。

## MKINITRD

### NAME

`mkinitrd` - 是一个调用 `dracut` 生成 initramfs 的兼容封装

## SYNOPSIS

```
mkinitrd [OPTION...] [<initrd-image>] <kernel-version>
```

## DESCRIPTION

`mkinitrd` 通过调用 `dracut` 为版本 `<kernel-version>` 的内核创建 initramfs 镜像 `<initrd-image>`

## Important

如果需要对生成的镜像进行细粒度控制，应直接调用 `dracut`。

## OPTIONS

- `--version` 打印版本信息
- `-v` 增加详细程度
- `-f` 强制覆盖现有的 initramfs 文件
- `--image-version` 将内核版本附加到镜像 `<initrd-image>-kernel-version>`
- `--with=<module>` 向 initramfs 添加内核模块 `<module>`
- `--preload=<module>` 在加载其他模块之前在 initramfs 中预加载内核模块 `<module>`。这可以确保设备命名，建议在 `/dev` 中使用符号链接。
- `--nocompress` 不压缩生成的镜像。
- `--help` 显示帮助信息并退出。

## AVAILABILITY

`mkinitrd` 命令是 `dracut` 包的一部分，可在 https://dracut.org 获取。

## AUTHORS

Harald Hoyer

## SEE ALSO

`dracut(8)`

## MKAP

### NAME

`mkswap` - 设置 Linux 区域

## SYNOPSIS

```
mkswap [options] device [size]
```

## DESCRIPTION

`mkswap` 在设备或文件中设置 Linux 交换区域。`device` 参数通常是一个分区（如 `/dev/sdb`），但也可以是一个文件。Linux 内核不查看分区 ID，但许多安装脚本会假设类型为 LINUX_SWAP 的分区是交换交换。（警告：Solaris 也使用这种类型。小心不要杀死你的 Solaris。）`size` 参数是多余的，但为了向后兼容而保留。它指定以 1024 字节块为单位的交换区域大小。如果省略，`mkswap` 将使用整个分区或文件。创建交换区域后，需要使用 `swapon` 命令启动它。通常交换区域会在 `/etc/fstab` 中列出，以便在某些启动脚本通过 `swapon -a` 使用。

## WARNING

交换头不会触碰第一个块。那里可以是引导加载程序或磁盘标签，但这不是推荐的设置。推荐的设置是使用独立分区作为 Linux 交换区域。`mkswap` 与许多其他 `mkfs` 类工具一样，擦除第一个分区以使文件系统不可见。然而，`mkswap` 拒绝擦除带有磁盘标签（SUN, BSD, ...）的设备的第一个块。

- `-c` 在创建交换区域之前检查设备（如果是块设备）是否有坏块。如果发现任何坏块，将打印计数。
- `-f --force` 即使命令很愚蠢也继续。这允许创建一个比所在的文件或分区更大的交换区域。此外，如果没有此选项，`mkswap` 将拒绝擦除带有分区表的设备的第一个块。
- `-L --label` 为设备指定标签，允许通过标签 `swapon`。
- `-p --pagesize` 指定使用的页大小（字节）。此选项通常是不必要的；`mkswap` 从内核读取大小。
- `-U --uuid` 指定要使用的 UUID。默认生成一个 UUID。
- `-v --swapversion 1` 指定交换空间版本。（此选项目前没有意义，因为旧的 `-v 0` 选项已过时，现在仅支持 `-v 1`。内核自 2.5.22（2002年6月）起不再支持 v0 交换空间格式。新版本 v1 自 2.1.117（1998年8月）起受到支持。）
- `-h --help` 显示帮助文本并退出。
- `-V --version` 版本信息并退出。

## NOTES

交换区域的最大有效大小取决于架构和内核版本。在 i386, PPC, m68k 和 ARM 上约为 2GiB，在 sparc 上为 1GiB，在 mips 上为 512MiB，在 alpha 上为 128GiB，在 sparc64 上为 3TiB。2.3.3（1999年5月）之后的内核没有这种限制。

注意，2.1.117版本之前内核为每个页分配一个字节，而现在分配两个字节，因此使用 2 GiB 的交换区域可能需要 2 MiB 的内核内存。

目前 Linux 允许 32 个交换区域（在 2.4.10（2001年9月）之前是 8 个）。使用的区域可以在 `/proc/swaps` 文件中查看（自 2.1.25（1997年9月）起）。

`mkswap` 拒绝小于 10 页的区域。

如果你不知道机器使用的页大小，可能可以通过 `/cat /proc/cpuinfo` 查询（也可能不能——文件内容取决于架构和内核版本）。

要设置交换文件，必须在用 `mkswap` 初始化之前先创建该文件，例如使用类似命令

```
# allocate --length 8GiB swapfile
```

注意，交换文件不能包含任何空洞（因此，使用 `cp(1)` 创建文件是不可接受的）。

# 环境

`LIBBLKID_DEBUG=0ffff` 可启用调试输出。

# 另请参

`fdisk(8)`, `swapon(8)`

# 可用性

`mkswap` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获得。

# mmcli

+ > 名字

`mmcli` - 控制和监控 ModemManager

## 概要

```
mmcli [OPTION...]
```



## 描述

ModemManager 是一个基于 DBus 的 Linux 守护进程，为与（移动宽带）调制调器的通信提供统一的高层 API。它作为一个标准的 RIL（无线接口层），可以被 NetworkManager 等不同的连接管理器使用。得益于内置的插件架构，ModemManager 可以与具有不同端口的不同类型的调制调器通信。除了标准的 AT 串口端口外，还支持基于高通的 QCDM 和 QMI 端口。

# 帮助选项

`-h`, `--help`

按分组显示选项摘要。

`--help-all`

显示所有组和选项。

`--help-manager`

显示特定管理器的选项。

`--help-common`

显示常用选项。这些选项用于定义选项操作的设备。
例如：调制调器、承载、SIM 卡、SMS' 等。

`--help-modem`

显示调制调器特定选项。

`--help-3gpp`

显示 3GPP 特定选项。

`--help-cdma`

显示 CDMA 特定选项。

`--help-simple`

显示简单选项。这些选项对于快速理解连接和断开连接的状态非常有用，而无需过多担心细节。

`--help-location`

显示位置或定位特定选项。

`--help-messaging`

显示消息特定选项。另请参见相关的 `--help-sms`。

`--help-time`

显示时间特定选项。

`--help-firmware`

显示固件特定选项。

`--help-oma`

显示 OMA 特定选项。

`--help-sim`

显示 SIM 卡特定选项。

`--help-bearer`

显示承载特定选项。

`--help-sms`

显示 SMS 特定选项。另请参见相关的 `--help-messaging`。

# 管理器选项

`-G`, `--set-logging=[ERR|WARN|INFO|DEBUG]`
设置 ModemManager 守护进程中的日志级别。对于调试信息，可以提供 DEBUG。DEBUG 以上的每个值提供的细节较少。在大多数情况下，ERR（显示错误）是重要消息。

默认模式为 ERR。

`-L`, `--list-modems`
列出可用调制调器。

`-M`, `--monitor-modems`
列出可用调制调器并监控添加或删除的调制调器。

`-S`, `--scan-modems`
扫描任何潜在的新调制调器。这在预期纯 RS232 调制调器时有用，因为内核不会自动通知它们。

# 通用选项

下方所有选项都接受 `PATH` 或 `INDEX` 参数。如果没有提供操作，则将显示调制调器、承载等的默认信息。

`PATH` 和 `INDEX` 在调制调器插入时自动创建。可以使用 `mmcli -L` 找到它们。这会产生类似的内容（仅限调制调器）：

```
Found 1 modems: /org/freedeskop/ModemManager1/Modem/4
```

在这种情况下，`INDEX` 是 `4`，`PATH` 是上述整个字符串。

然而，对于承载、SIM 卡和 SMS 情况，`PATH` 略有不同。Modem 被替换为正在使用的对象名称，例如 Bearer。例如：

```
/org/freedeskop/ModemManager1/Bearer/4
```

`-m`, `--modem=[PATH|INDEX]`
指定一个调制调器。

`-b`, `--bearer=[PATH|INDEX]`
指定一个承载。

`-i`, `--sim=[PATH|INDEX]`
指定一个 SIM 卡。

`-s`, `--sms=[PATH|INDEX]`
指定一条 SMS。

# 调制调器选项

下方所有的调制调器选项都使用 `-modem` 或 `-m` 来指定要操作的调制调器。

某些操作需要 `MODE`。`MODE` 可以调制调器实际支持的任何模式组合。在理想情况下，以下是可能的：

- `2G` - 2G 技术，例如 EDGE；CDMA1x 3G - 3G 技术，例如 HSPA；EV-D0 4G - 4G 技术，例如 LTE；ANY 用于所有支持模式。

`-w,--monitor-state`

监控给定调制调器的状态。

`-e,--enable`

启用指定的调制调器。

这将为天线供电，启动自动注册过程，并通用的准备调制调器以连接。

`-d,--disable`

禁用指定的调制调器。

这将断开调制调器的现有连接并将其置于低功率模式。

`-r,--reset`

将调制调器重置为电源循环时的设置。

`-factory-reset=--CODE`

将调制调器重置为原始出厂默认设置。

提供的 `CODE` 是厂商特定的。如果没有正确的厂商代码，此操作不太可能成功。这不是常见的用户操作。

`-command=COMMAND`

向指定的调制调器发送 AT `COMMAND`。例如，`COMMAND` 可以是 ‘AT+GMM’用以探测手机型号信息。此操作仅在 ModemManager 以调试模式运行时可用。

`-list-bearers`

列出给定调制调器可用的分组数据包承载。

`-create-bearer=[[KEY1=VALUE1,KEY2=VALUE2,...']`

为指定的调制调器创建一个新的分组数据包承载。`KEYs` 和一些 `VALUES` 如下所示：

- `apn`
接入点名称。3GPP 需要。

- `ip-type`
地址类型。由 MBearer 值提供（例如 'ipv4', 'ipv6'）。

- `allowed-auth`
使用的身份验证方法。由 MBearer 值提供（例如 ‘pap|chap|mschap2|mschap’）。

- `user name`
网络需要的用户名（如果有）。

- `password`
网络需要的密码（如果有）。

- `allow-roaming`
指示漫游期间允许连接，由布尔值提供（即 ‘yes’ 或 ‘no’）。

- `rm-protocol`
Rm 接口协议，由 MMCdma 值提供（例如 ‘async’, ‘packet-relay’, ‘network-slip’）。

- `number` 拨号号码。

`-delete-bearer=PATH` 从指定的调制调器删除承载。此选项显式使用 `PATH`，无法使用 `INDEX`。

`-set-bands=[BAND1|BAND2...]` 为指定的调制调器设置频段。支持的频段很多，列出全部将详细。详情请参见 MMemBand 文档。

示例为：‘egsm|dcs|pcs|g50’选择所有 GSM 频段。

`-set-preferred-mode=MODE` 为调制调器设置首选 `MODE`。`MODE` 必须是 `--set-allowed-modes` 中的允许模式之一。可能的模式在本节开头介绍。

# 3GPP 选项

第三代伙伴计划 (3GPP) 是电信协会小组之间的协作。这些选项适用于支持 3GPP 的设备。包含的选项用于控制 USSD（非结构化附加数据）会话。

下方所有的的3GPP 选项都使用 —modem 或 -m 来指定操作的调制调器。

`-3gpp-scan` 扫描可用的 3GPP 网络。

`-3gpp-register-home` 请求指定的调制调器注册到其主网络。这将注册到调制调器指定的默认网络。

`-register-in-operator=MCCNC` 请求指定的调制调器注册到指定的 MCCNC（移动国家代码、移动网络代码）运营商的网络。此代码用于 GSM/LTE、CDMA、IDEN、TETRA 和 UMTS 公用移动网络以及卫星移动网络。ITU-T 建议 E.212 定义了移动国家代码。

`-3gpp-ussd-status` 请求任何进行的 USSD 会话的状态。

`-3gpp-ussd-initiate=COMMAND` 请求指定的调制调器使用 `COMMAND` 启动 USSD 会话。

例如，`COMMAND` 可以是 '*101#'用以获取当前的预付费余额。

`-3gpp-ussd-respond=RESPONSE` 在启动 USSD 会话时，网络发起的请求可能需要响应。此选项允许这样做。

`-3gpp-ussd-cancel` 取消指定调制调器正在进行的 USSD 会话。

# CDMA 选项

所有 CDMA（码分多址接入）选项都需要使用 `--modem` 或 `-m` 选项。

```
--cdma-activate=CARRIER
```

使用 OTA（空中无线）设置激活指定的调制调器。`CARRIER` 是由网络提供的代码，用于它们所提供的默认设置。

# 简单选项

所有简单选项必须配合 `--modem` 或 `-m` 使用。
`--simple-connect=['KEY1=VALUE1,KEY2=VALUE2,...']`

使用 KEY / VALUE值对运行完整的连接序列。你可以使用 `--create-bearer` 选项，以及以下任何一个选项：

- `- SIM-PIN` 解锁码。
- `operator-id` 强制指定网络 ETSI MCC-MNC，用于强制注册。
- `--simple-disconnect` 断开指定调制调器所有已连接的承载（bearers）。
- `--simple-status` 显示指定调制调器的状态。

# 位置选项（LOCATION）

这些选项详细说明了如何使用全球定位系统（GPS）或直接从移动网络基础设施（3GPP 或 3GPP2）发现你的位置。

所有位置选项必须配合 `--modem` 或 `-m` 使用。

`-location-status` 显示发现位置的当前状态。
`-location-get` 显示所有可用的位置信息。
`-location-enable-3gpp` 启用使用 3GPP 网络发现位置。
`-location-disable-3gpp` 禁用使用 3GPP 网络发现位置。
`-location-get-3gpp` 显示基于 3GPP 的位置信息（MCC, MNC, LAC, CI）。
`-location-enable-nmea` 启用使用 GPS 发现位置并使用 NMEA 轨迹报告。
`-location-disable-gps-nmea` 禁用使用 GPS 和 NMEA 轨迹发现位置。
`-location-get-gps-nmea` 显示带有 NMEA 轨迹信息的 GPS 基位置。
`-location-enable-gps-raw` 启用使用 GPS 发现位置并使用原始值（即经度/纬度）报告。
`-location-disable-gps-raw` 禁用使用 GPS 和原始值发现位置。
`-location-get-gps-raw` 显示带有原始值的 GPS 基位置信息（例如纬度、经度）。
`-location-enable-cdma-bs` 启用使用 3GPP2 网络发现位置。
`-location-disable-cdma-bs` 禁用使用 3GPP2 网络发现位置。
`-location-get-cdma-bs` 显示基于 3GPP2 的位置信息（CDMA 基站位置）。

# 消息选项（MESSAGING）

所有消息选项必须配合 `--modem` 或 `-m` 使用。

`--messaging-status`
显示消息支持状态。

`--messaging-list-sms`
列出指定调制调器上可 SMS 消息。

`--messaging-create-sms=['KEY1=VALUE1,...']`

在指定的调制调器上创建新的 SMS。键可以是以下任何一个：

- `number`: 消息接收的号码。
- `text`: 消息文本，格式为 UTF-8。在发送时，如果文本超过技术或调制调器的限制，消息将拆分成多个部分或多条消息。注意，文本和数据永远不会提供。
- `smsc`: 指定 SMS 服务中心号码。
- `validity`: 指定 SMS 在 SMSC 中的过期时间。
- `class`: 3GPP 消息类型 (0..3)。
- `delivery-report-request`: 指定发送 SMS 时是否请求投递报告（‘yes’ 或‘no’）。
- `storage`: 指定保存此消息的位置。存储位置可以是‘sm’‘me’‘mt’‘sr’‘bm’‘ta’。

`--messaging-create-sms-with-data=PATH` 使用文件名路径作为数据创建新的 SMS。
`--messaging-delete-sms=PATH` 从指定的调制调器上删除 SMS。
`PATH` 表示 SMS 路径。

# 时间选项（TIME）

所有时间操作都需要 `--modem` 或 `-m` 选项。

`--time`
显示来自运营商的当前网络时间。这包括通常很重要的时区。

# 固件选项（FIRMWARE）

所有固件选项都需要 `--modem` 或 `-m` 选项。

`-firmware-list`
列出指定调制调器上安装的所有固件镜像。

`-firmware-select=ID`
从指定调制调器安装的固件镜像中选择一个。可以使用 `--firmware-list` 选项查看可用固件镜像列表。
提供的 `ID` 是固件的唯一标识符。

# OMA 选项

所有 OMA 选项都需要 `--modem` 或 `-m` 选项。

`-oma-status`
显示 OMA 设备管理子系统的状态。
`-oma-start-client-initiated-session=[SESSION TYPE]`
请求启动客户端发起会话。
指定的会话类型必须是以下之一：‘client-initiated-device-configure’‘client-initiated-prl-update’‘client-initiated-hands-free-activation’

`-oma-accept-network-initiated-session=[SESSION ID]`
请求接受网络发起会话。
`-oma-reject-network-initiated-session=[SESSION ID]`
请求拒绝网络发起会话。
`-oma-cancel-session`
请求取消当前的 OMA 会话（如果有）。

# SIM 选项

`-pin=PIN`
将 PIN 码发送到指定的 SIM 卡。
`-puk=PUK`
将 PUK 码发送指定的 SIM 卡。这必须配合 `--pin` 使用。
`-enable-pin`
启用指定 SIM 卡的 PIN 请求。这必须配合 `--pin` 使用。
`-disable-pin`
禁用指定 SIM 卡的 PIN 请求。这必须配合 `--pin` 使用。
`-change-pin=PIN`
更改 PIN 码。

# 承载选项（BEARER）

所有承载选项都需要 `--bearer` 或 b。

`-c`, `--connect`
连接承载。
`-x`, `--disconnect`
断开连接承载。

# SMS 选项

所有 SMS 选项都需要 `--sms` 或 s。

`-send`
发送 SMS。
`-store`
在指定的调制调器上存储 SMS。
要知道存储在哪个位置，请查看 `--messaging-status` 所示 存储位置。
`--store-in-storage=STORAGE`
指定保存消息的位置。可能的存储位置包括：
- `sm`: SIM。
- `me`: 内存。
- `mt`: 接收的消息。
- `sr`: 服务回复。
- `bm`: 广播。
- `ta`: 终端。
`--create-file-with-data=PATH` 使用文件路径作为数据创建文件。

# 应用程序选项（APPLICATION）

`-v`, `--verbose`
执行更多详细操作。
`-V`, `--version`
返回版本。
`-a`, `--async`
使用异步方法。
`--timeout=SECONDS`
用于操作超时。

# 示例（EXAMPLES）

# 发送 PIN 码到 SIM
首先需要知道 SIM 卡的正确路径：
```
$ mmcli -m 0 | grep SIM
path='/org/freedesktop/Modem1/SIM/0'
```

# 简单连接和断开
你可以启动连接过程：
```
$ mmcli -m 0 --simple-connect="pin=1234, apn=internet"
```
成功连接调制调器
然后你可以断开：
```
$ mmcli -m 0 --simple-disconnect
```
成功断开所有承载

# 3GPP 网络扫描
扫描 3GPP 网络可能需要长时间，因此需要特定的超时时间：
```
$ mmcli -m 0 --3g-scan --timeout=300
```
找到 4 个网络：
21404 Yoigo (可用)
21407 Movistar (当前)
21401 Vodafone ES (禁止)
21403 Orange (禁止)

# 创建并存储新 SMS
使用“sm”（SIM），你可以这样做：
```
$ mmcli -m 0 --messaging-create-sms --text="Hello world",number=+123456780
```
创建了新的 SMS: `/org/freedesktop/ModemManager1/SMS/21` (unknown)

```
sudo mmcli -s 21 store-in-storage=sm
```
成功存储了 SMS

```
$ sudo mmcli -s 21 /org/freedesktop/ModemManager1/SMS/21/
```
- 内容 | '+123456780' | text: Hello world

- 属性 | PDU 类型: 'submit' | 状态: 'stored' | smsc: 'unknown' | 有效: '0' | 类型: 'sm'

- 投递报告: '未请求' | 引用: '0'

```
$ sudo mmcli -m 0 --messaging-status /org/freedesktop/ModemManager1/Modem/0
```
- 消息 | 支持存储：'sm, me' | 默认存储：'me'

# 从文件发送 SMS
如你所示，关键部分是 `--messaging-create-sms-with-data` 和提供的路径。
```
$ sudo mmcli -m 0 --messaging-create-sms --number='+123456780' --messaging-create-sms-with-data=/path/to/your/file
```
成功创建新的 SMS: `/org/freedesktop/ModemManager1/SMS/22` (unknown)

```
$ sudo mmcli -s 22 --send
```
成功发送了 SMS



# 列出 SMS 消息

当接收者收到消息的所有部分时，现在可以使用其 ModemManager 设置中的另一个 `mmcli` 命令来恢复发送的文件：

```
$> mmcli -m 0 --messaging-list-sms Found 1 SMS messages:

/org/freesktop/ModemManager1/SMS/0 $ sudo mmcli -s 0 --create-file-data=/path/to/the/output/file
```

# GPS 位置状态

你首先需要检查调制解器是否具有特定的 GPS 定位能力。请注意，我们假设调制解器显示为索引 `0`；如果你有多个调制解器，请使用 `--list-mods` 来检查正确的调制解器索引：

```
$ mmcli -m 0 --location-status /org/freesktop/ModemManager1/Modem/0-Location | capabilities: '3ggg-lac-ci, gps-raw, gps-nmea' | enabled: 'none' | signals: 'no'
```

输出显示调制解器支持 3GPP 区域小区 ID (Cell ID)、GPS 原始和 GPS-NMEA 定位源。目前尚未启用任何一项，因为我们还没有启用调制解器，我们可以对其进行启用：

```
$ sudo mmcli -m 0 --enable successfully enabled the modem mmcli -m 0 --location-status /org/freesktop/ModemManager1/Modem/0-Location | capabilities: '3ggg-lac-ci, gps-raw, gps-nmea' | enabled: '3ggg-lac-ci' | signals: 'no'
```

# 启用 GPS 位置技术

我们可以使用以下命令启用 RAW 和 NMEA GPS 定位源：

```
$ sudo mmcli -m 0 --location-enable-gps-raw --location-enable-gps-nmea successfully setup location gathering
```

如果我们再次检查状态，将看到特定的 GPS 位置已启用：

```
$ mmcli -m 0 --location-status /org/freesktop/ModemManager1/Modem/0-Location | capabilities: '3ggg-lac-ci, gps-raw, gps-nmea' | enabled: '3ggg-lac-ci, gps-raw, gps-nmea' | signals: 'no'
```

# 获取 GPS 位置

你可以使用 `--location-get-3ggg`、`location-get-gps-raw` 和 `--location-get-gps-raw` 查询特定的位置信息；但一次性获取所有：

```
$ mmcli -m 0 --location-get /org/freesktop/ModemManager1/Modem/0 3PPP location | Mobile country code: '214' | Cell ID: '70337377' GPS NMEA traces :

GPGGA,,,,,,,, *66 | |GPRMC,,V, *N*53

GPSSA,A1,,,,,,,, *16 | |GPGSV,4,1,16,24,,29,,05,,18,,*7A

GPSV,4, 2,16,22,,14,,,11,,,17*T

$GPGSV, 4, 3, 03,,, 12,,, 30,,, 13,,,*78 |

$GPGSV, 4, 4, 16, 23,,, 15,,, 27,,, 07,,,*79 | $GPVTG,,T,,M,,N,,N,,K,N*2C
```

| Raw GPS | 不可用 |
| :--- | :--- |
| CDMA BS | 不可用 |

RAW GPS 位置信息的示例：

```
$ sudo mmcli -m 0 --location-get-gps-raw /org/freedesktop/ModemManager1/Modem/0  Raw GPS | UTC time: '155142.2' | Longitude: '-3.513941' | Latitude: '40.502603' | Altitude: '18.000000'
```

## 作者

Martyn Russell <martyn@lanedo.com>

# 另请参考

- `ModemManager(8)`, `NetworkManager(8)`
- AT (http://en.wikipedia.org/wiki/AT_commands).
- 3GPP (http://en.wikipedia.org/wiki/3GPP).
- MCCNC (http://en.wikipedia.org/wiki/Mobile_Network_Code).
- USSD (http://en.wikipedia.org/wiki/Supplementary_Service_Data).
- CDMA (http://en.wikipedia.org/wiki/CDMA_division_access).
- OTA (http://en.wikipedia.org/wiki/Over-the-air_programming).
- GPS (http://en.wikipedia.org/wiki/Global_Positioning_System)
- NMEA (http://en.wikipedia.org/wiki/NMEA_0183)

# MODINFO

## 名称
`modinfo` - 显示关于 Linux 模块的信息

## 概要

```
modinfo [-V] [-F field] [-k kernel] [modulename|filename...]
```

## 描述

`modinfo` 从命令行给 Linux 内核模块中提取信息。如果模块名不是文件名，则会搜索 `/lib/modules` 目录，这与 `modprobe(8)` 在加载模块时所做的相同。`modinfo` 默认以“字段: 值”的形式列出模块的每个属性，以便阅读。文件名也以相同的方式列出（尽管它并不真的是一个属性）。此版本的 `modinfo` 可以理解任何 Linux 内核架构。

## 选项

`-V`, `--version`
打印版本。

`-F`, `--field`
仅打印指定的字段。`modinfo` 默认以“字段: 值”的形式列出模块的每个属性，以便阅读。文件名也以相同的方式列出（尽管它并不真的是一个属性）。此版本的 `modinfo` 可以理解任何 Linux 内核架构。

`-b`, `--basedir`
模块的根目录，默认为 `/`。

`-k`, `kernel`
提供内核信息。

`-0`, `--null`
使用零字符来分隔字段值。

`-a`, `--author`
作者。

`-d`, `--description`
描述。

`-l`, `--license`
许可证。

`-p`, `--parameters`
参数。

`-n`
别名。

# 版权

本手册最初版权 2003 年 Martyn Russell 所有。

# 另请参考

- `modprobe(8)`

## 作者

Jon Masters <jcm@masters.org.com>
开发者

Lucas Marchi <demarchi@gmail.com>
开发者

# MODPROBE

## 名称
`modprobe` - 从内核中添加或移除模块

# 语法

```
modprobe [-v] [-C config-file] [-n] [-i] [-b] [modulename]

modprobe [-r] [-v]

modprobe [-v] [-C config-file] [-n] [-i] [-b] [modulename...]

modprobe [-c] [filename]
```

## 描述

`modprobe` 智能地添加或移除模块。如果模块需要其他模块（任何一个），`modprobe` 会自动添加或移除这些依赖项。

`modprobe` 期望由相应的 `depmod` 工具生成的最新的 `modules.dep` 文件（见 `depmod(8)`）。该文件列出了每个模块所需的模块，`modprobe` 使用它来执行此操作。

如果在 `modulename` 之后给出任何参数，它们将传递给内核（除了配置文件中的任何选项）。

## 选项

`-a`, `--all`
插入命令行上的所有模块名。

`-b`, `--use-blacklist`
此选项导致 `modprobe` 将配置文件中的黑名单命令（如果有）也应用于模块名。它通常用于 `udev(7)`。

`-C`, `--config`
此选项覆盖默认配置目录 (`/etc/modprobe.d`)。此选项会通过 `MODPROBE_OPTIONS` 环境变量传递给 install 和 remove 命令。

`-c`, `--showmodversions`
导出配置目录中的有效配置并退出。

`--dump-modversions`
打印模块所需的模块版本信息列表。此选项通常由发行版用于使用模块版本打包 Linux 内核。

`-d`, `--dirname`
模块的根目录，默认为 `/`。

`--first-time`
通常情况下，如果被要求插入已存在的模块或移除不存在的模块，`modprobe` 将成功（但什么都不做）。这对于简单的脚本非常理想；然而复杂的脚本通常想知道 `modprobe` 是否真的执行了操作：此选项会让 `modprobe` 在实际上未执行任何操作时失败。

`--force-vermagic`
每个模块都包含一个包含重要信息的小字符串，例如内核和编译器版本。如果模块加载失败且内核抱怨“版本魔法”不匹配，你可以使用此选项来移除它。自然地，这种检查是为了你的安全，除非你确定自己在做什么，否则使用此选项是危险的。

这适用于任何插入的模块：包括命令行上的模块（或别名）以及它依赖的任何模块。

`--force-modversions`
当模块使用 `CONFIG_MODVERSIONS` 编译时，会包含一个详细说明

为由模块使用（或由模块提供）的每个接口创建了版本信息。如果模块加载失败，且内核抱怨该模块与某些接口的版本不一致，你可以使用“force-modversion”来完全移除版本信息。自然，这种检查是为了保护你的安全，因此除非你清楚自己在做什么，否则使用此选项是危险的。

这适用于任何插入的模块：包括命令行上的模块（或别名）以及它所依赖的任何模块。

## `-f`, `--force`

尝试从模块中剥除可能阻止其加载的任何版本信息；这等同于 `--force-vermagic` 和 `--force-modversion`。自然地，这些检查是为了你的你的安全，因此除非你清楚自己在做什么，否则使用此选项是危险的。

这适用于任何插入的模块：包括命令行上的模块（或别名）以及它依赖的任何模块。

## `-i`, `--ignore-install`, `--ignore-remove`

此选项会导致 `modprobe` 忽略命令行上指定模块的配置文件（如果有）中的 install 和 remove 命令（任何依赖模块仍受配置文件中为它们设置的命令影响）。在使用此选项时，无论请求是否指定了另一个（而非两者）`--ignore-install` 或 `--ignore-remove`，所有的 install 和 remove 命令都会被忽略。参见 `modprobe.d(5)`。

## `-n`, `--dry-run`, `--show`

此选项执行除实际插入或删除模块（或安装或移除命令）之外的所有操作。结合 `-v` 使用时对调试非常有用。由于历史原因，dry-run 和 show 的含义相同且可以互换。

## `-q`, `--quiet`

使用此标志后，如果尝试移除或插入一个找不到模块（且不是别名或 insert 命令），`modprobe` 将不会打印错误信息。但它仍会返回非零状态。内核利用此通过 request 机会性地探测可能存在的模块。

## `-R`, `--resolve-alias`

打印所有匹配别名的模块名。这对于调试问题很有用。

## `-r`, `--remove`

此选项导致 `modprobe` 移除而不是插入模块。如果它依赖的模块也没有被使用，`modprobe` 将尝试一移除它们。与插入不同，命令行上可以指定多个模块；在移除模块时指定模块参数是有意义的。你的发行版可能没有构建支持移除所有模块。

## `-S`, `--set-version`

设置内核版本，而不是使用 `uname(2)` 来决定内核版本（决定了查找模块的位置）。

## `-s`, `--show-depends`

列出模块（或别名）的依赖关系，包括模块本身。这将产生一组（可能是空的）文件名，每行一个，每个以 `insmod` 开头，通常用于发行版确定生成 initrd/initramfs 镜像时包含哪些模块。应用的 install 命令不会运行任何命令。注意，`modinfo(8)` 可以从模块本身提取依赖项，但它不知道别名或 install 选项。

## `-s`, `--syslog`

此选项通过 install 或 remove 命令传递给环境变量 `MODPROBE_OPTIONS` 中的其他 `modprobe` 命令。

## `-V`, `--version`

显示程序版本并退出。

## `-v`, `--verbose`

打印有关程序正在执行操作的消息。通常 `modprobe` 仅在发生错误时打印消息。此选项通过 install 或 remove 命令传递给环境变量 `MODPROBE_OPTIONS` 中的其他 `modprobe` 命令。

## ENVIRONMENT

环境变量 `MODPROBE_OPTIONS` 也可以向 `modprobe` 传递参数。

## COPYRIGHT

本帮助页原始版权所有 © 2002, Rusty Russell, IBM Corporation。由 Jon Masters 等人维护。

## SEE ALSO

`modprobe.d(5)`, `insmod(8)`, `rmmod(8)`, `lsmod(8)`, `modinfo(8)`

## AUTHORS

Jon Masters <jcm@jonmasters.org> 开发者

Robby Workman <rworkman@slackware.com> 开发者

Lucas De Marchi <lucas.marchi@gmail.com> 开发者

# MOUNT.CIFS

### NAME

`mount.cifs` - 使用通用网络文件系统 (CIFS) 进行挂载

## SYNOPSIS

```
mount.cifs {service} {mount-point} [-o options]
```

## DESCRIPTION

此工具是 `cifs-utils` 套件的一部分。`mount.cifs` 用于挂载 Linux CIFS 文件系统。它通常在使用“-t cifs”选项时通过 `mount(8)` 命令间接调用。该命令仅作用于 Linux，且内核必须支持 cifs 文件系统。CIFS 协议是 SMB 协议的继承者，被大多数 Windows 服务器以及许多其他商业服务器、网络附属存储设备以及流行的开源服务器 Samba 所支持。`mount.cifs` 工具将指定的 service 的 UNC 名称（导出的网络资源，使用 `//server/share` 语法，其中“server”是服务器名称或 IP 地址，“share”是共享名称）挂载到本地目录 `mount-point`。

`mount.cifs` 的选项以逗号分隔的键值对列表指定。假设 cifs 文件系统内核模块 (`cifs.ko`) 支持，可以发送列出的其他选项。传递给 cifs vfs 内核的不识别 cifs 挂载选项将记录在内核日志中。

`mount.cifs` 会导致 cifs vfs 启动一个名为 `cifsd` 的线程。挂载后它一直运行直到挂载资源被卸载（通常通过 `umount` 工具）。

`mount.cifs -V` 命令显示 cifs 挂载辅助程序的版本。

`modinfo cifs` 命令显示 cifs 模块的版本。

## OPTIONS

`username=arg`

连接时使用的用户名。如果没有给出，则使用环境变量 `USER`。

早期版本的 `mount.cifs` 还允许用户在“user%%password”或“workgroup/user”或“workgroup/user%%password”中指定用户名，以便将密码和工作组作为用户名的一部分指定。对备用户名格式的支持现在已弃用，不应再次使用。用户应使用独立的“password=”和“domain=”来指定这些值。虽然某些版本的 cifs 内核模块建议使用“accept”作为其选项的缩写，可能会误导标准 mount 程序认为这是一个非超级用户挂载。建议使用完整的“username=”名称。

`password=arg`

指定 CIFS 密码。如果没有给出此选项，则使用环境变量 `PASSWD`。如果未通过 `mount.cifs` 的参数直接或间接指定密码，将提示密码，除非指定了 guest 选项。

注意包含分隔符字符（即逗号 ','）的密码在命令行上无法正确解析。然而，在 `PASSWD` 环境变量或通过凭据文件（见下文）定义或在密码提示输入的密码将被正确读取。

`credentials=filename`

指定一个包含用户名和或密码以及可选工作组名称的文件。文件格式为：

username=value password=value domain=value

这比在共享文件（如 `/etc/fstab`）中使用明文密码要好。请确保妥善保护任何凭据文件。

`uid=arg`

当服务器未提供所有权信息时，设置挂载文件系统中所有文件或目录的 uid。可以是用户名或数字 uid 指定。当未指定时，默认为 uid 0。`mount.cifs` 辅助程序必须为 1.10 或更高版本才能支持以非数字形式指定 uid。更多信息请见下文的 FILE AND DIRECTORY OWNERSHIP AND PERMISSIONS 部分。

`forceuid` 指示客户端忽略服务器为文件和目录提供的任何 uid

并始终将所有者指定为 `uid=` 选项的值。更多信息请参见下文“文件和目录所有权与权限”章节。



### 挂载选项

`cuid=arg`

设置凭据缓存所有者的 uid。这在使用 `sec=krb5` 时特别有用。默认值是执行挂载操作的进程的 uid。设置此参数将引导上调用（upcall）去查找由该用户拥有的凭据缓存。

`gid=arg`

当服务器不提供所有权信息时，设置挂载文件系统上所有文件或目录的 gid。它可以指定为组名或数字 gid。如果未指定，默认值为 gid 0。`mount.cifs` 辅助程序必须是 1.10 或更高版本才能支持以非数字形式指定 gid。更多信息请参见下文“文件和目录所有权与权限”章节。

`forcegid=arg`

指示客户端忽略服务器为文件和目录提供的任何 gid，并始终将所有者指定为 `gid=` 选项的值的值。更多信息请参见下文“文件和目录所有权与权限”章节。

`port=arg`

设置客户端尝试连接 CIFS 服务器的端口号。如果指定了此值，将查找具有此端口的现有连接，如果存在则使用它。如果不存在，则尝试在该端口上创建新连接。如果连接失败，则返回错误。如果未指定此值，将查找端口 445 或 139 上的现有连接。如果不存在此类连接，则尝试先连接 445 端口，如果失败再尝试连接 139 端口。如果两者都失败，则返回错误。

`servernetbiosname=arg`

指定在尝试建立服务器会话时使用的服务器 NetBIOS 节点 `RFC1001`。虽然挂载较新的服务器时很少需要此选项，但在通过端口 139 连接到某些较旧的服务器（如 OS/2 或 Windows 98）时需要此选项，因为较新的服务器不支持默认的服务器名称。服务器名称长度可达 15 个字符，且通常全大写。

`server=arg`

`servernetbiosname` 的同义词。

`netbiosname=arg`

当通过端口 139 挂载服务器时，指定在进行 `RFC1001` NetBIOS 会话初始化时使用的 `RFC1001` 源名称来表示客户端 NetBIOS 机器名。

`file_mode=arg`

如果服务器不支持 CIFS Unix 扩展，此选项将覆盖默认的文件模式。

`dir_mode=arg`

如果服务器不支持 CIFS Unix 扩展，此选项将覆盖目录的默认模式。

`ip=arg`

设置目标 IP 地址。如果请求的 UNC 名称中的服务器部分可以解析，则此选项会自动设置，因此用户很少需要指定。

`domain=arg`

设置用户的域（工作组）

`guest`

不提示密码

`iocharset`

字符集用于将路径名转换为 Unicode。如果服务器支持，网络路径名默认使用 Unicode。如果未指定 `iocharset`，则将使用本地客户端内核编译时指定的 `nls_default`。如果服务器不支持 Unicode，此参数无效。

`ro`

只读挂载

`rw`

读写挂载

`setuids`

如果与服务器建立了 CIFS Unix 扩展，客户端将尝试在新创建的文件、目录和设备（create, mkdir, knod）上设置本地进程的有效 uid 和 gid。如果没有协商 CIFS Unix 扩展，对于新创建的文件和目录，将不再使用挂载时指定的默认 uid 和 gid，而是在缓存新文件的 uid 和 gid，这意味着当 inode 重新加载（或用户重新挂载共享）时，文件的 uid 可能会发生。

`noseuids`

客户端将不会尝试在新创建的文件、目录和设备（create, mkdir, knod）上设置 uid 和 gid，这会导致服务器将 uid 和 gid 设置为默认值（通常是挂载共享的用户的服务器 uid）。让服务器（而非客户端）设置 uid 和 gid 是默认行为。如果未协商 CIFS 扩展，则新文件的 uid 和 gid 将将是挂载时的 uid (gid) 或挂载时指定的 uid (gid) 参数。

`perm`

客户端进行权限检查（根据文件的 uid 和 gid 结合模式和所需操作进行 `vfs_permission` 检查），注意，这是在服务器软件在目标机器上执行的正常 ACL 检查之外的额外检查。客户端权限检查默认启用。

`nperm`

客户端不进行权限检查。这可能会导致此访问的文件暴露给本地客户端系统的其他用户。这通常在服务器支持 CIFS Unix 扩展，但客户端和服务器系统上的 UIDs/GIDs 不够匹配以允许执行挂载的用户访问时需要。注意，这不会影响服务器软件在目标机器上执行的正常 ACL 检查（根据挂载时提供的用户名对服务器 ACL 进行检查）。

`dynperm`

指示服务器在内存中维护无法存储在服务器上的所有权权限。这些信息可能会随时消失（当 inode 从缓存中刷新时），因此虽然这有助于某些应用程序运行，但其行为具有不可靠性。更多信息请参见下文“文件和目录所有权与权限”章节。

`cache=`

缓存模式。详情请参见下文“缓存一致性”章节。允许的值为：

- `none`: 完全不缓存文件
- `strict`: 严格遵循 CIFS/SMB2 协议
- `loose`: 允许松散缓存

3.7 之前的内核默认为“loose”。从 3.7 内核开始默认为“strict”。

`directio`

对挂载的文件不进行内联缓存。这阻止了对此挂载的文件进行映射（mmapping）。在某些快速网络且客户端缓存收益较小的情况下（当应用程序执行无重复的大规模读取时），性能可能比默认行为更好，默认行为在授予并持有 oplock（缓存令牌）时通过客户端页面缓存预读（reahead）和后写（writebehind）。注意大于页面的直接写入将发送到服务器。在某些内核上，这要求编译 `cifs.ko` 模块时带有 `CIFS_EXPERIMENTAL` 选项。此选项将在 3.7 中废弃。用户应使用 `cache=none`。

`strictcache`

用于开启严格缓存模式。在此模式下，当客户端持有 oplock II 时，始终从缓存读取，否则从服务器读取。对于写入，在独占 oplock 情况下客户端将数据存储在缓存中，否则直接写入服务器。此选项将在 3.7 中废弃。用户应使用 `cache=strict`。

`rwpidforward`

将打开文件的进程 pid 转发到该文件的任何读写操作。这可以防止 WINE 等应用程序在性强制块模式时读写失败。

`mapchars`

将七个保留字符中的六个（不反斜杠，但包括冒号、问号、管道、星号、大于和小于号）转换为重映射范围（0xF000 以上），这也允许 CIFS 客户端识别由 Windows 使用此类字符创建的文件。当挂载某些版本的 Samba（其禁止创建和打开名称包含这七个字符的文件）时，这非常有用。如果服务器在链路上不支持 Unicode，则没有影响。请注意，使用 mapchars 挂载选项创建的文件在没有该选项挂载共享时可能无法访问。

`nomapchars`

不翻译这七个字符中的任何一个（默认）

`intr`

尚未实现

`nointr`

（默认）尚未实现

`hard`

当服务器崩溃时，访问 cifs 挂载文件系统的程序将挂起。

`soft`（默认）当服务器崩溃时，访问 cifs 挂载文件系统的程序不会挂起，并将向用户应用程序返回错误。

`noacl`

即使服务器支持，也不允许 POSIX ACL 操作。

CIFS 客户端可以针对版本 3.0.10 及更高版本的 Samba 服务器获取和设置 POSIX ACL (`getfacl`, `setfacl`)。在构建 CIFS 模块时，需要在 CIFS 配置选项中同时启用 `CIFS_XATTR` 和 `CIFS_POSIX` 支持，才能设置 POSIX ACL。可以通过在挂载时指定“noacl”来禁用单个挂载的 POSIX ACL 支持。

`cifsacl`

此选项用于将 CIFS/NTFS ACL 映射到/从 Linux 权限位，将 SID 映射到/从 UID 和 GID，并获取和设置安全描述符（Security Descriptors）。

更多信息请参阅 CIFS/NTFS ACL、SID/UID/GID MAPPING、SECURITY DESCRIPTORS 章节。

`backupid=arg`

将具有备份意图的文件访问限制给特定用户。需要提供名称或 ID 作为参数，没有默认值。

更多细节请参见 ACCESSING FILES WITH BACKUP INTENT 章节。

`backupgid=arg`

将具有备份意图的文件访问限制给特定组。需要提供名称或 ID 作为参数，没有默认值。

更多细节请参见 ACCESSING FILES WITH BACKUP INTENT 章节。

`nocase`

请求路径名不区分大小匹配（如果服务器支持，默认是区分大小的）。

`ignorecase`

`nocase` 的同义词。

`sec=`

安全模式。允许的值有：

- `none` - 尝试作为空用户（无名称）连接
- `krb5` - 使用 Kerberos 版本 5 认证
- `krb5i` - 使用 Kerberos 认证并强制启用数据包签名
- `tl` - 使用 NTLM 密码哈希
- `tlmmi` - 使用 NTLM 密码哈希并强制数据包签名
- `tlmv2` - 使用 NTLM2 密码哈希
- `tlmv2i` - 使用 NTLM2 密码哈希并强制数据包签名
- `ntlmssp` - 使用封装在 Raw NTLMSSP 消息中的 NTLMV2 密码哈希
- `tlmsp` - 使用封装在 Raw NTLMSSP 消息中的 NTLMV2 密码哈希，并强制数据包签名

v3.8 之前的内联内核版本默认值为 `sec=ntlmsp`。在 v3.8 中，默认值更改为 `sec=ntlmsp`。

如果服务器在协议期间期间签名，则可能会自动启用。如果 `/proc/fcs/cifs/SecurityFlags` 中启用了数据包签名，数据包签名也可能自动启用。

`nobrl`

- 不向服务器发送字节范围请求。对于某些因 cifs 样式强制字节范围锁而崩溃的应用程序是必要的（且大多数 cifs 服务器尚未支持请求建议性字节范围锁）。

`sfu`

当未协商 CIFS Unix 扩展时，尝试创建与 Services for Unix (SFU) 兼容的设备文件和 inode。此外，通过 SETFILEBITS 扩展属性检索模式的第 10-12 字节（如 SFU 所示）。未来，模式的高 9 位也将通过查询安全描述符 (ACL) 进行模拟。[注：需要 CIFS VFS 1.39 或更高版本。需要 1.40 或更高版本的 CIFS VFS 内核模块以识别符号链接并能够创建 SFU 兼容格式的符号链接。]

`serverino`

使用服务器返回的 inode （唯一持久性文件标识符），而不是在客户端自动生成临时 inode 号。虽然服务器 inode 号更容易识别硬链接文件（因为它们具有相同的 inode 号），且 inode 号可能是持久的（这对比某些软件有用），但服务器不保证在单个共享项下导出的多个服务器端挂载中，inode 号是唯一的（因为如果多个文件系统挂载在同一个共享高层目录下，服务器上的 inode 号可能是不唯一的）。注意，并非所有返回服务器 inode 号的服务器都支持 CIFS 扩展，但 Windows 2000 及之后的服务器通常会这样做（但不一定在每个本地服务器文件系统上）。如果服务器不支持返回 inode 号或等效项，则参数无效。此行为默认启用。

`noserverino`

- 客户端自行生成 inode 号，而不是使用服务器的实际 inode。

更多信息请参见 INODE NUMBERS 章节。

`nounix`

禁用此挂载的 CIFS Unix 扩展。这可以用于一次关闭多个设置。这包括 POSIX acls、POSIX 锁、POSIX 路径、符号链接支持以及从服务器检索 uids/gids/mode。这对于规避支持 Unix 扩展的服务器中的 bug 很有用。

更多信息请参见 INODE NUMBERS 章节。

`nouser_xattr`

不允许 getattr/setattr 获取/设置扩展属性 (xattrs)，即使服务器本身支持。。默认启用 xattr 支持。

`rsize=bytes`

内核在读取请求中请求的最大数据量（单位：字节）。在内核 3.2.0 之前，默认值为 16k，最大值受 `CIFSMaxBufSize` 模块的限制。从内核 3.2.0 开始，行为取决于挂载上启用了哪些 POSIX 扩展以及服务器是否支持 POSIX 扩展。如果支持，则默认值为 1M，最大为 16M。如果服务器不支持，则默认值为 60k，最大约为 127k。60k 的原因是它是 Windows 服务器能够填充的最大大小。注意，该值是最大值，客户端可能会选择较小的值。

`wsize=bytes`

内核在写入请求中发送的最大数据量（单位：字节）。在内核 3.2.0 之前，默认值为 16k，最大值受 `CIFSMaxBufSize` 模块的限制。从内核 3.2.0 开始，行为取决于挂载上启用了哪些 POSIX 扩展以及服务器是否支持 POSIX 扩展。如果支持，则默认值为 1M，最大为 16M。如果服务器不支持，则默认值为 60k，最大约为 127k。60k 的原因是它是 Windows 服务器能够填充的最大大小。注意，该值是最大值，客户端可能会选择较小的值。

`fsc`

使用 FS-Cache 启用磁盘缓存。此选项可能对于提高慢链路性能有用。注意：此功能仅适用于编译了内核配置 `CONFIG_CIFS_FSCACHE` 的近期内核。你还需要安装并运行 `cachefilesd` 守护进程使缓存生效。

`multiuser`

访问服务器时将用户访问映射到单独凭据。默认情况下，CIFS 挂载在访问共享时仅使用一组用户凭据（挂载凭据）。使用此选项，当新用户访问挂载时，客户端将使用用户的凭据与服务器建立新话。该用户的后续访问也将使用这些凭据。由于内核无法提示密码，多用户挂载限制用于不需要密码的 sec= 选项。

`1.0` - 经典的 CIFS/SMBv1 协议。这是默认选项。

`2.0` - SMBv2.002 协议。最初引入于 Windows Vista Service Pack 1 和 Windows Server 2008 中。注意，Windows Vista 的初始版本使用的是略不同的方言 (2.000)，该版本不受支持。

`2.1` - SMBv2.1 协议，引入于 Microsoft Windows 7 和 Windows Server 2008R2 中。

`3.0` - SMBv3.0 协议，引入于 Microsoft Windows 8 和 Windows Server 2012 中。

注意，虽然此选项控制了使用的协议版本，但并非每个版本的所有功能都可用。

`--verbose`

为挂载打印额外的调试信息。注意，此参数必须在 `-o` 之前指定。例如：

```
mount -t cifs //server/share/mnt --verbose -o user=username
```

### 服务格式化与分隔符

在服务名称中，通常推荐使用斜杠 (`/`) 作为分隔符。它们被认为是“通用分隔符”，因为在 Windows 机器通常不允许在路径组件中嵌入斜杠，且客户端可以无条件地将其转换为反斜杠 (`\`)。相反，POSIX 允许反斜杠字符作为路径组件的一部分，且无法以相同的方式自动转换。

`mount.cifs` 会尝试在可行的情况下将反斜杠转换为斜杠，但在共享名称之后的任何路径组件中均无法做到。

### INODE 数字

当启用 Unix 扩展（Unix Extensions）时，我们使用服务器响应 POSIX 调用时提供的实际 inode 号作为 inode 号。

当禁用 Unix 扩展并启用了 “serverino”挂载选项时，将无法获取服务器 inode 号。客户端通常将服务器分配的 “UniqueID” 映射到 inode 号。

注意，UniqueID 与服务器 inode 号是不同的值。UniqueID 值在整个服务器范围内是唯一的，且通常大于 2^32。此值经常会导致未使用 LFS（大文件支持）结构编译的程序在处理文件结构字段时出现问题。强烈建议使用 LFS 支持编译你的程序（即使用 `-D_FILE_OFFSET_BITS=64`）以防止此问题。你也可以使用 “noserverino”挂载选项在客户端上生成小于 2^32 的 inode 号。但你可能无法正确检测硬链接。

### 缓存一致性 (CACHE COHERENCY)

对于使用 CIFS 或 NFS 的网络文件系统，客户端必须面对事实：其他客户端或服务器上的活动可能会在客户端感知的情况下更改文件的内容或属性。处理此类问题的方法之一是强制所有文件访问直接到达服务器。然而，这在性能上是不可接受的，大多数协议都有某些允许客户端本地缓存数据的机制。

CIFS 协议（实际上）强制客户端除非持有乐观锁（flock）或租约（lease），否则不应缓存文件数据。这两个实体都允许客户端保证对文件的某些类型的排他性访问，使其在无需持续与服务器交互的情况下访问其内容。当服务器需要撤销其中任何一个时，将回调客户端，并允许客户端一定的时间来刷新任何缓存数据。

c 客户端使用内核的 pagecache 来缓存文件数据。通过 pagecache 进行任何 I/O 通常都是页对齐的。这与字节范围锁结合时可能会出现问题，因为 Windows 的锁定是强制性的，并在发生时会阻塞读取和写入。

`cache=none` 意味着客户端在普通读写时从不利用缓存。它总是直接访问服务器以满足读或写请求。

`cache=strict` 意味着客户端将尝试严格遵循 CIFS/SMB2 协议。也就是说，只有当客户端持有 oplock 时，缓存才是可靠的。当客户端不持有 oplock 时，客户端将跳过缓存并直接访问服务器以满足读或写请求。通过这种方式，客户端避免了字节范围锁的问题。此外，当客户端持有 oplock 时，字节范围锁会被缓存在客户端上，并在 oplock 被撤回时被“推”到服务器。

`cache=loose` 允许客户端使用较宽松的协议语义，这有时可以以牺牲缓存一致性为代价提供更好的性能。文件访问涉及 pagecache。当未持有 oplock 或租约时，客户端将尝试在对文件写入后不久刷新缓存。注意，刷新并不一定在系统调用返回之前发生。



在不持有 oplock 的情况下进行读取时，客户端将尝试定期检查文件的属性，以确定其是否已更改以及缓存可能不再有效。这种机制与 NFS2/3 使用缓存一致性的机制非常相似，并且在 CIFS 中特别棘手。Windows 在更新客户端用于验证此点的点的 `LastWriteTime` 字段方面非常“懒惰”。结果是，当多个读取者和写入者处理相同文件时，`cache=loose` 可能会导致数据损坏。

因此，当多个客户端访问同一组文件时，建议使用 `cache=strict`。这通过更严格地遵循 CIFS/SMB2 协议有助于消除缓存一致性问题。

注意，无论使用何种缓存模型，客户端始终将使用 pagecache 处理 mmap'ed 文件。mmap'ed 文件的写入在调用 `close()` 时才保证刷新到服务器。3.7 之前的默认是 `loose`。3.7 之后，默认是 `strict`。

*(注：原文后续部分存在大量重复段落，根据注意事项“不要重复输出原文”的要求，此处仅翻译核心差异差异部分)*

# 文件和目录所有权与权限

核心 CIFS 协议不为文件和目录提供 Unix 所有权信息或模式（mode）。因此，文件和目录通常显示为 `uid=` 或 `dir_mode` 选项设置的值的所有，并且权限被设置为挂载时的默认 `file_mode`。尝试通过 `chmod/chown` 更改这些值将返回成功，但没有实际效果。

当客户端和服务器协商 Unix 扩展时，文件和目录将被分配服务器提供的 `uid`、`gid` 和模式。由于 CIFS 通常是单用户的，且无论哪个用户访问挂载都会使用相同的凭据，新创建的文件和目录的所有权通常将与挂载共享时使用的任何凭据对应。

如果客户端和服务器使用的 `uid` 和 `gid` 不匹配，`forceuid` 和 `forcegid` 选项可能会有所帮助。但请注意，没有相应的选项来覆盖模式。当 `forceuid` 或 `forcegid` 生效时，分配给文件的权限可能无法反映真实的权限。

在未协商 Unix 扩展的情况下，也可以使用 `dynperm` 挂载选项在服务器上本地模拟它们。当此挂载选项生效时，新创建的文件和目录将获得看似正确的权限。然而，这些权限并不存储在服务器上，并可能在未来的任何时间消失（取决于内核刷新 inode 缓存的随机性）。通常，不建议使用此挂载选项。

也可以通过 `noperm` 选项完全在客户端上覆盖权限检查。服务器端的权限检查无法被覆盖。服务器执行的权限检查始终对应于挂载共享时使用的凭据，而不一定对应于访问共享的用户。

# 环境变量

`USER` 变量可能包含用于向服务器身份验证的用户名。该变量可以使用 `username%password` 格式同时设置用户名和密码。

`PASSWD` 变量可能包含使用客户端的人的密码。

`PASSWD_FILE` 变量可能包含用于读取密码的文件路径。将读取单行输入并用作密码。

# 注意事项

此命令仅可由 root 使用，除非安装了 `setuid`，在这种情况下将启用 `noeexec` 和 `nosiduid` 挂载标志。当作为 `setuid` 程序安装时，程序将遵循 `mount` 程序为用户挂载设立约定，并增加了一个限制：用户必须在挂载之前能够 `chdir()` 进入挂载点，才能在其上挂载。

某些 samba 客户端工具如 `smbclient(8)` 会尊重 `smb.conf` 中的客户端配置参数。与这些客户端工具不同，`mount.cifs` 完全忽略 `smb.conf`。

# 配置

为 cifs vfs 更改配置和读取调试信息的主要机制是通过 Linux 的 `/proc` 文件系统。在 `/proc/fs/cifs` 目录下有各种配置文件和伪文件，它们可以显示调试信息。还有额外的启动选项，例如最大缓冲区大小和缓冲区数量，这些选项仅在内核 cifs vfs（`cifs.ko` 模块）加载时可以设置。可以通过对 `cifs.ko` 文件运行 `modinfo` 工具来查看，这将列出在模块安装（设备驱动加载）期间可以传递给 cifs 的选项。更多信息信息请参阅内核文件 `fs/cifs/README`。

# 缺陷

目前不支持使用 CIFS URL 规范进行挂载。

凭据文件不支持处理带有空格的用户名或密码。

注意，对错误报告的典型响应是建议先尝试最新版本。因此，请先尝试这样做，并在报告错误时务必包含你使用的相关软件版本（最低：`mount.cifs`（尝试 `mount.cifs -V`）、内核（查看 `/proc/version`）以及你尝试联系的服务器类型）。

# 版本

此手册页适用于 cifs vfs 文件系统的 1.74 版本（大约对应 Linux 内核 3.0）。

## 参见

`cifs.upcall(8)`, `getcifsacl(1)`, `setcifsacl(1)`

linux 内核源源码树中的 `Documentation/filesystems/cifs.txt` 和 `fs/cifs/README` 可能包含额外的选项和信息。

## 作者

Steve French

语法和手册页大致基于 `smbmount`。由 Jelmer Vernooij 转换为 Docbook/XML。

Linux cifs vfs 的维护者和用户态工具 `mount.cifs` 的维护者是 Steve French。Linux CIFS 邮件列表是询问此类程序问题的首选场所。

# fuse

## 名称

`fuse` - fuse 文件系统的格式和选项

## 描述

FUSE（用户空间文件系统）是用户空间程序向 Linux 内核导出虚拟文件系统的简单接口。FUSE 旨在为非特权用户提供一种安全方法，来创建和挂载自己的文件系统实现。

# 配置

某些关于挂载策略的选项可以在文件 `/etc/fuse.conf` 中设置。目前：

- `mount_max = NNN`: 设置允许非 root 用户的最大 FUSE 挂载数。默认值为 1000。
- `user_allow_other`: 允许非 root 用户指定 `allow_other`

## 选项

支持 `mount` 中描述的大多数通用挂载选项（`ro`, `rw`, `suid`, `nosuid`, `dev`, `nodev`, `noexec`, `atime`, `noatime`, `sync`, `async`, `dirsync`）。文件系统默认以 `nodev`、`nosuid` 挂载，这只能由特权用户覆盖。

通用挂载选项：

这些是可以为所有文件系统指定的 FUSE 特有挂载选项：

- `default_permissions`: 默认情况下，FUSE 不检查访问权限，文件系统可以自由实现其访问策略，或将其留给底层文件机制（针对网络文件系统）。此选项启用权限检查，根据文件模式限制访问。此选项通常与 `allow_other` 选项配合使用。
- `allow_other`: 选项覆盖了文件访问对挂载文件系统的用户的限制。因此所有用户（包括 root）都可以访问文件。此选项默认仅允许 root 使用，但可以通过上一节描述的配置选项移除此限制。
- `allow_root`: 此选项类似于 `allow_other`，但文件访问被限制为挂载文件系统的用户和 root。此选项和 `allow_other` 是互斥的。
- `kernel_cache`: 此选项禁用了每次 `open(2)` 时刷新文件缓存。这应仅在文件数据从未从外部更改（不通过挂载的 FUSE 文件系统）的文件上启用。它不适用于网络文件和其他中间文件系统。注意：如果没有指定此选项（也没有 `direct_io`），数据在 `open(2)` 后会被缓存，因此 `read(2)` 系统调用不会总是发起读取操作。
- `auto_cache`: 此选项在 `open(2)` 时原子刷新缓存。只有当文件的修改时间或大小发生变化时，才会刷新缓存。
- `large_read`: 发出大的读取请求。这可以提高某些文件系统的性能，但也可能降低性能。此选项仅对 2.4.X 内核有用，在 2.6 内核上请求大小会自动确定最佳性能。
- `direct_io`: 此选项禁用内核对该文件系统的页缓存（文件内容缓存）。这产生若干影响：

    + 每次 `read(2)` 或 `write(2)` 系统调用将发起一个或多个读取或写入操作，数据将不会在内核中缓存。
    + `read()` 和 `write()` 系统调用的返回值将与 `read` 和 `write` 操作的返回值对应。这非常有用，例如当提前不知道文件大小（在读取之前）时。

`max_read=N`

通过此选项可以设置读取操作的最大尺寸。默认值为无限。请注意，读取请求的大小被限制为最多 32 页（在 i386 上为 128 字节）。

`max_readahead=N`

设置预读的最大字节数。默认值由内核决定。在 linux-2.6.22 或更早版本上，它为 131072 (128k 字节)。

`max_write=N`

设置单次写入操作的最大字节数。默认为 128k 字节。注意，由于各种限制，写入请求的大小要小得多（4k 字节）。该限制将在未来移除。

`async_read`

异步执行读取。这是默认设置。

`sync_read`

同步执行所有读取（包括预读）。

`hard_remove`

默认行为是：如果一个打开的文件被删除，该文件将被重命名为隐藏文件 (`.fuse_hiddenXXX`)，只有当文件最终释放时才会删除。这减轻了文件系统实现处理此问题的压力。该选项禁用隐藏行为，文件将在 unlink 操作（或覆盖现有文件的 rename 操作）中立即删除。

建议不要使用 `hard_remove` 选项。当设置了 `hard_remove` 时，将遵循 libc 函数对取消链接文件的处理方式（返回 ENOENT 错误码）：

`read(2)`, `write(2)`, `fsync(2)`, `close(2)`, `f*xattr(2)`, `ftruncate(2)`, `fstat(2)`, `chmod(2)`, `fchown(2)`

`debug`

开启库调试信息的打印。

`filename=NAME`

设置文件系统源（`/etc/mtab` 中的第一个字段）。默认值是挂载程序名。

`subtype=TYPE`

设置文件系统类型（`/etc/mtab` 中的第三个字段）。如果内核支持，默认值为挂载程序；`/etc/mtab` 和 `/proc/mounts` 将显示文件系统类型为 `fuse.TYPE`。

如果内核不支持子类型，源文件将为 `TYPE#NAME`，或者如果没有指定 `filename` 选项，则仅为 `TYPE`。

`use_ino`

尊重内核函数 `getattr()` 和 `fill_dir()` 中的 `st_ino` 字段。此值用于填充 `stat(2)` `lstat(2)` `fstat(2)` 函数中的 st_ino 字段以及 `readdir(2)` 函数中的 d_ino 字段。文件系统并不保证其唯一性，但某些应用程序依赖于该值在整个文件系统中是唯一的。

# readdir__ino

如果没有给出 `use_ino` 选项，仍会尝试填充 `readdir(2)` 中的 d_ino 字段。如果该名称之前被查找过且仍在缓存中，将使用找到的 inode 号。否则将将其设置为 -1。如果提供了 `use_ino` 选项，则忽略此选项。

# nonempty

允许在非空文件或目录上挂载。默认情况下这些挂载会被拒绝，以防止意外覆盖数据（这可能会阻止自动备份）。

# umask=M

覆盖文件系统通过 `st_mode` 设置的权限位。生成的权限位是相对于给定 `umask` 值缺失的位。该值以八进制给出。

`uid=N`

覆盖文件系统设置的 uid 字段。

`gid=N`

覆盖文件系统设置的 gid 字段。

`blkdev`

挂载由块设备支持的文件系统。

# entry_timeout=T

设置预读的最大字节数。默认值由内核决定。在 linux-2.6.22 或更早版本上，它为 131072 (128k 字节)。

# negative_timeout=T

设置负缓存的超时秒数。

# attr_timeout=T

设置属性缓存的超时秒数。

`congestion-threshold=N`

将 fuse 模块的拥塞阈值设置为 N [默认值: 48]

`backup-volfile-servers=SERVERLIST`

按照以下格式提供备份卷file 服务器列表 [默认值: None]

```
$ mount -t glusterfs -obackupvolfile-servers=<server2>:<server3>...:<serverN>:<server1>:/</volname> <mount_point>
```

`backup-volfile-server=SERVER`

按照以下格式提供备份卷file 服务器 [默认值: None]

```
$ mount -t glusterfs -obackupvolfile-server=<server2> <server1>:/</volname><mount_point>
```

`fetch-attempts=N`

已弃选项 - 为了向后兼容放置此处 [默认值: 1]

`background-qlen=N`

将 fuse 模块的后台队列长度设置为 N [默认值: 64]

`no-root-squash=BOOL`

对信任的客户端禁用 root 压缩（root squashing） [默认值: off]

`root-squash=BOOL`

对信任的客户端启用 root 压缩（root squashing） [默认值: on]

`use-readdirp=BOOL`

在 fuse 内核模块中使用 readdirp() 模式 [默认值: on]

## 文件

`/etc/fstab`

`/etc/fstab` 中典型的 GlusterFS 条目如下

```
server1:/mirror /mnt/mirror glusterfs log-file=/var/log/mirror.log,acl,selinux 0 0
```

`/proc/mounts`

`/proc/mounts` 中 GlusterFS 挂载点的示例项如下

```
server1:/mirror /mnt/glusterfs fuse.glusterfs
rw,allow_other,default_permissions,max_read=131072 0 0
```

# 另

`glusterfs(8)`, `mount(8)`, `gluster(8)`

# 版权

Copyright(c) 2006-2013 Red Hat, Inc. <http://www.redhat.com>

# 挂载 mount

## 名称

`mount` - 挂载文件系统

# 语法

```
mount [-lhV]
```

```
mount -a [-Ffnrvw] [-t vftype] [-O optlist]
```

```
mount [-fnrvw] [-o option[,option...] device|dir
```

```
mount [-fnrvw] [-t vftype] [-o options] device dir
```

## 描述

Unix 系统中可访问的所有文件排列在一个巨大的树中，即文件层次结构，以 / 为根。这些文件可以分布在多个设备上。`mount` 命令的作用是将某些设备上找到的文件系统挂载到大文件树上。相反，`unmount(8)` 命令将再次将其卸载。

`mount` 命令的标准形式是

```
mount -t type device dir
```

这告诉内核将设备 device（类型为 type）上的文件系统挂载到目录 dir。dir 原有的内容（如果有）以及所有者和模式将变得不可见，只要该文件系统保持挂载状态，路径名 dir 就指向设备上文件系统的根目录。

如果只给出目录或设备，例如：

```
mount /dir
```

则 mount 会查找挂载点，如果未找到，则在 `/etc/fstab` 文件中查找设备。可以使用 `--target` 或 `--source` 选项避免对给定参数的歧义解释。例如

```
mount --target /mountpoint
```

# 列出与帮助。

列出模式仅为了向后兼容而维护。为了获得更健壮且定义的输出，请使用 `findmnt(8)`，特别是在脚本中。注意，挂载点名称中的控制字符会被替换为 ‘?’。

```
mount [-l] [-t type]
```

列出所有挂载的文件系统（类型为 type）。选项 `-l` 会在此列表中添加标签。见下文。

# 设备指示。

大多数设备通过文件名（块特殊设备）指示。

在 `/etc/fstab` 文件中推荐的设置是标签（例如 `LABEL=<label>`）而不是 `/dev/disk-[label,uuid,partuuid,partlabel]` dev 符号链接。标签更具可读性、健壮性和可移植性。`mount(8)` 命令内部使用 dev 符号链接，因此 `/etc/fstab` 中的符号链接没有标签的优势。更多细节请参阅 `libblkid(3)`。

注意 `mount(8)` 使用 UUID 作为字符串。来自命令行或 `fstab(5)` 的 UUID 不会转换为内部二进制表示。UUID 的字符串表示应基于小写字母。

proc 文件系统未与特殊设备关联，挂载它时，可以使用任意关键字（如 proc）代替设备规范。习惯性的选择 none 较不理想：`unmount` 产生的错误信息 `now busy` 可能会引起混义。

# /etc/fstab, /etc/mtab 和 /proc/mounts 文件。

文件 `/etc/fstab`（参见 `fstab(5)`）可能包含描述哪些设备通常挂载在何处以及使用哪些选项的行。`fstab(5)` 文件的默认位置可以被覆盖。

文件 `/etc/fstab`（参见 `fstab(5)`）可能包含描述哪些设备通常挂载在何处以及使用哪些选项的行。`fstab(5)` 文件的默认位置可以被覆盖。

文件 `/etc/fstab`（参见 `fstab(5)`）可能包含描述哪些设备通常挂载在何处以及使用哪些选项的行。`fstab(5)` 文件的默认位置可以被覆盖。

文件 `/etc/fstab`（参见 `fstab(5)`）可能包含描述哪些设备通常挂载在何处以及使用哪些选项的行。`fstab(5)` 文件的默认位置可以被覆盖。



文件 `/etc/fstab`（参见 `fstab(5)`）可能包含描述哪些设备通常挂载在何处以及使用哪些选项的行。`fstab(5)` 文件的默认位置可以被覆盖。

# 非超级用户挂载

通常，只有超级用户才能挂载文件系统。然而，当 `fstab` 包含 `user` 选项时，任何人都可以挂载系统。

# 绑定挂载

自 Linux 2.4.0 开始，可以将文件层次结构部分重新挂载到其他地方。调用为

```
mount --bind olddir newdir
```

或 `fstab` 条目为：

```
/olddir /newdir none bind
```

来自文件的标志。如果你的系统没有 `/etc/mtab` 文件，或者你在 `remount` 命令中显式地定义了源和目标（此时 `mount(8)` 不会读取 `/etc/mtab`），那么你必须对 `remount` 命令也使用 `bind` 标志（或选项）。例如：

```
mount --bind olddir newdir -o remount,ro,bind olddir newdir
```

注意，`remount,ro,bind` 将创建一个只读的挂载点（VFS 条目），但原始的文件子块仍然是可写的，这意味着 `olddir` 是可写的，而 `newdir` 是只读的。

## 移动操作 (The move operation)

自 Linux 2.5.1 起，可以原子地将挂载的树移动到另一个地方。

该命令为：

```
mount --move olddir newdir
```

或使用短选项：

```
mount -M olddir newdir
```

这将导致之前出现在 `olddir` 下的内容通过 `newdir` 访问。文件的物理位置不会改变。请注意，`olddir` 必须是一个挂载点。

注意，移动位于共享挂载下的挂载点是无效且不受支持的。使用 `findmnt -TARGET,PROPAGATION` 查看当前的传播标志。

## 共享子树树操作 (The shared subtrees operations)

自 Linux 2.6.15 起，可以将挂载点及其子挂载标记为共享（shared）、私有（private）、从属（slave）或不可绑定（unbindable）。共享挂载提供了创建该挂载镜像的能力，任何镜像中的此类挂载以及镜像内的挂载都会传播到另一个镜像。从属挂载从其主挂载接收传播，但反之亦然。私有挂载不具备传播能力。不可绑定挂载是一种无法通过 `bind` 操作进行克隆的私有挂载。详细的语义在内核源码树的 `Documentation/filesystems/sharedsubtree.txt` 中有记录。

支持的操作：

```
mount --make-shared mountpoint mount --make-slave mountpoint mount --make-private mountpoint mount --make-unbindable mountpoint
```

以下命令允许递归地更改给定挂载点下所有挂载的类型。

```
mount --make-rshared mountpoint mount --make-rslave mountpoint mount --make-rprivate mountpoint mount --make-runbindable mountpoint
```

当请求 `mount-*` 操作时，`mount(8)` 不读取 `fstab(5)`。所有必要信息都必须在命令行中指定。

注意，Linux 内核不允许通过单次 `mount(2)` 系统调用更改多个传播标志，且这些标志无法与其他 `mount` 选项混合使用。

自 `util-linux` 2.23 起，`mount` 命令允许一起使用多个传播标志并与其他挂载操作结合使用。此功能是**实验性的**（EXPERIMENTAL）。传播标志是在之前的挂载操作成功后，通过额外的 `mount(2)` 系统调用应用的。请注意，这种用例不是原子的。传播标志可以在 `fstab(5)` 中作为 `mount` 选项（`private`, `slave`, `shared`, `unbindable`, `rprivate`, `rslave`, `rshared`, `runbindable`）。

例如：

```
mount --make-private --make-unbindable /dev/sda1 /A
```

等同于

```
mount /dev/sda1 /A mount --make-private /A mount --make-unbindable /A
```

## 命令行选项 (COMMAND LINE OPTIONS)

`mount` 调用时使用的完整 `mount` 选项集由以下步骤确定：首先从 `fstab` 表中提取文件系统的 `mount` 选项，然后应用 `-o` 参数指定的任何选项，最后如果存在则应用 `-r` 或 `-w` 选项。

`mount` 命令可命令行选项：

- `-V`, `--version`

  输出版本。

- `-h`, `--help`

  打印帮助信息。

- `-v`, `--verbose`

  详细模式。

- `-a`, `--all`

  挂载 `fstab` 中提到的所有（给定类型的）系统。

- `-F`, `--fork`

  （与 `-a` 配合使用。）为每个设备 `fork` 出一个新的 `mount` 实例。这将并行在不同设备上执行挂载。优点是速度更快；同时也并行处理 NFS 超时。缺点是挂载顺序是未定义的。因此，如果你想同时挂载 `/usr` 和 `/usr/spool`，不能使用此选项。

- `-f`, `--fake`

  除了实际系统调用外执行所有操作；如果不是，则“假挂载”文件系统。此选项通常与 `-v` 标志配合使用，以确定 `mount` 命令尝试的操作。对于之前使用 `-n` 选项挂载的设备，`-f` 会检查 `/etc/mtab` 中是否存在记录（对于普通假挂载，此检查由内核完成）。

- `-i`, `--internal-only`

  即使存在，也不调用 `/sbin/mount.<filesystem>` 辅助程序。

- `-l`, `--show-labels`

  在挂载输出中添加标签（labels）。挂载必须具有读取磁盘的权限（例如 sudo root）才能工作。可以使用 `e2label(8)` 为 ext2、ext3 或 ext4 设置标签，使用 `xfs_admin(8)` 设置 XFS，使用 `reunir(8)` 设置 reiserfs。

- `-n`, `--no-mtab`

  不写入 `/etc/mtab` 挂载。当 `/etc` 是只读文件系统时这是必要的。

- `-c`, `--no-canonicalize`

  不规范化路径。`mount` 命令会将所有路径（来自命令行或 `fstab`）规范化并存储到 `/etc/mtab`。此选项可以配合 `-f` 用于用于已规范化的路径。

- `-s`, `--sloppy`

  容忍糟糕的挂载选项而不是失败。这将忽略文件系统类型不支持的 `mount` 选项。此选项用于支持自动挂载。

- `--source`

  如果只给 `mount` 提供一个参数，该参数可能被解释为目标（挂载点）或源（设备）。此选项允许显式定义参数为源。

- `-r,--read-only`

  只读挂载文件系统。等同于 `-o ro`。注意，取决于文件系统类型和内核行为，系统仍然写入设备。为了防止这种写入访问，你可能需要使用“只读”选项挂载 ext3 或 ext4，参见 `blockdev(8)`。

- `-w,--read-write`

  读写挂载文件系统。这是默认设置。等同于 `-o rw`。

- `-L,--label`

  挂载具有指定标签的分区。

- `-U,--uuid`

  挂载具有指定 uuid 的分区。这些选项需要 `/proc/partitions`（Linux 2.1.1 起存在）。

- `-T,--fstab`

  指定 `fstab` 文件。如果路径是目录，目录中的文件按 `strcmp(3)` 排序，以 `.` 开头的文件将被忽略。该选项可以指定多次。主要为 initramfs 或 chroot 脚本设计。

- `-t,--types`

  `-t` 用于指示文件系统类型。目前支持的类型包括：`adfs`, `affs`, `autofs`, `cifs`, `coda`, `coherent`, `cramf`, `debugfs`, `devpts`, `ext`, `ext2`, `ext3`, `ext4`, `hfs`, `hfsplus`, `iso9660`, `jextfs`, `minos`, `cpfs`, `nfs`, `nfs4`, `proc`, `rafs`, `reiserfs`, `squashfs`, `smbfs`, `sysv`, `tmpfs`, `ubifs`, `udb`, `ufs`, `umsdos`, `usbfs`, `vfat`, `xenix`, `xiafs`。早期的 `ubfs` 被称为 `usdevfs`。所有支持的文件系统取决于你的内核。`mount` 和 `umount` 程序支持文件系统类型。子类型由后缀‘subtype’定义，例如‘fuse.sshfs’。建议使用子类型而不是任何前缀（例如 `sshfs@example.com` 已弃用）。对于大多数类型，`mount` 程序只需要执行简单的 `mount(2)` 系统调用，不需要详细系统的知识。但对于少数类型（如 `nfs`, `nfs4`, `cifs`, `smbfs`, `cpfs`），需要特制代码。`nfs`、`cifs`、`smbfs` 和 `cpfs` 文件系统有独立的 `mount` 程序。为了能够以统一的方式尝试所有类型，当带有类型 `TYPE` 被调用时，`mount` 将执行 `/sbin/mount.TYPE`（如果存在）。由于不同版本的 `mount` 程序有不同的调用约定，`/sbin/mount.smbfs` 可能是一个设置所需调用的 shell 脚本。如果给了 `-t` 选项，或指定了自动类型，`mount` 将尝试猜测所需的类型。`mount` 使用 `blkid` 库查询文件系统；如果没有返回任何熟悉的内核，`mount` 将读取 `/etc/filesystems` 文件，如果不存在则读取 `/proc/filesystems`。列出的所有文件系统类型都将被尝试，除非标记为“nodev”的（例如 `devpts`, `proc` 和 `nfs`）。如果 `/etc/filesystems` 以星号 `*` 结尾，`mount` 之后会读取 `/proc/filesystems`。所有文件系统将使用 `mount` 选项“silent”挂载。

自动类型对用户挂载软盘有用。如果你使用内核自动加载器，创建 `/etc/filesystems` 文件有助于更改探测顺序（例如在尝试 `ext2` 之前尝试 `vfat msdos` 或 `ext3`）。

可以指定多个类型，用逗号分隔列表。文件系统类型列表可以以前 `-n` 前缀，以指定不采取操作的文件系统类型。这在 `-a` 选项上是有意义的。）例如，命令：

```
mount -a -t msdos,ext
```

挂载除 `msdos` 和 `ext` 类型以外的所有系统。

- `--target dir`

如果 `mount` 只提供一个参数，该参数可能被解释为目标（挂载点）或源（设备）。此选项允许显式定义参数为目标。

- `-O, --test-opts opts`

与 `-a` 配合使用，限制应用 `-a` 的系统集。`-t` 在这方面由于在 `-a` 的上下文中是没用的。例如，命令：

```
mount -a -O no_netdev
```

挂载所有在 `/etc/fstab` 文件的选项字段中指定了 `-netdev` 的系统。它与 `-t` 的区别在于每个选项都精确匹配；选项开头的 `no` 不会抵消剩余部分。`-t` 和 `-O` 选项的效果是累积的；即，命令

```
mount -a ext2 -O _netdev
```

使用 `_netdev` 选项挂载所有 `ext2` 文件系统，而不是挂载所有 `ext2` 或指定了 `_netdev` 选项的文件系统 `-o,--opts` 选项通过 `-o` 标志指定，后跟用逗号分隔的选项字符串。例如：

```bash
mount LABEL=mydisk noatime,nouser
```

详细信息请参阅 FILESYSTEM INDEPENDENT MOUNT OPTIONS（文件系统独立挂载选项）和 FILESYSTEM SPECIFIC MOUNT OPTIONS（文件系统特定挂载选项）章节。

`-B,--bind` 将子树重新挂载到其他地方（使其内容在两个地方都可用）。见上文。`-R,--bind` 将子树及所有可能的子挂载点重新挂载到其他地方（使其内容在两个地方都可用）。见上文。`-M,--move` 将子树移动到其他地方。见上文。

# 文件系统独立挂载选项

这些选项中的某些仅在出现在 `/etc/fstab` 文件时才有用。

某些选项可能在系统内核中默认启用或禁用。使用 `/proc/mounts` 中的选项来检查当前设置。注意，文件系统还有每个文件系统特定的默认挂载选项（例如查看 ext2N 系统的 `tune2fs -1` 输出）。

以下选项适用于任何正在挂载的文件系统，但并非每个文件系统都会实际遵循它们——例如，如今 `sync` 选项仅对 ext2、ext3、fat、vfat 和 ufs 有效：

### async

到文件系统的所有 I/O 都应异步进行。（另见 `sync` 选项。）

### atime

如果不使用 `noatime`，则 inode 访问时间将由内核默认值控制。另见对 `strictatime` 和 `relatime` 挂载选项的描述。

### noatime

不要在此文件系统上更新 inode 访问时间（例如，为了加快新闻队列的访问速度以提高服务器性能）。

### auto

可以使用 `-a` 选项挂载。

### noauto

只能显式挂载（即 `-a` 选项不会导致该文件系统被挂载）。

### context=context, fscontext=context,context=context and rootcontext=context

在挂载不支持扩展属性的文件系统时，`context=` 选项非常有用，例如软盘或格式化为 FAT 的硬硬盘，或者通常不在 SELinux 下运行的文件系统（例如来自非 Linux 工作站的 ext3 格式磁盘）。你也可以在不信任的文件系统（如软盘）上使用 `context=`。它也与早期 2.4.x 内核版本中支持 xattr 的文件系统兼容。即使在支持 xattrs，你也可以通过分配单一安全上下文来节省为每个文件标记标签的时间。

可移动介质常用的选项是 `context=system_u:object_r:removable_t`。

另外两个选项是 `fscontext` 和 `context=`，它们与 `context` 选项互斥。这意味着你可以配合使用 `fscontext` 和 `defcontext`，但这两者都不能与 `context` 同时使用。

`fscontext` 选项适用于所有文件系统，无论其是否支持 xattr。`fscontext` 选项将全局文件系统标签设置为特定的安全上下文。此文件系统标签与文件上的单个标签是分开的。对于某些类型的权限检查（如挂载或创建文件），它代表整个文件系统。单个文件的文件标签仍然从文件自身的 xattr 中获取。onode 的 context 实际上设置了 `fscontext` 提供的聚合上下文，同时为单个文件提供相同的标签。

### 使用 `defcontext=` 选项为未标记的文件设置默认上下文。这会覆盖策略中为未标记文件设置的值，并需要支持 xattr 的文件系统。

`rootcontext=` 选项允许你在挂载的文件系统对用户空间可见之前，显式地为其根索引标记。这被发现对于静态 linux 等内容有用。

注意，内核会拒绝任何包含 `context` 选项的挂载请求，即使其与当前上下文相同。

**警告：** `context` 值可能包含逗号，在这种情况下值必须被正确引用，**`mount(8)`** 将把逗号解释为挂载选项之间的分隔符。不要忘记 shell 会去掉引号，因此**必须使用双引号**。例如：

```bash
mount -t tmpfs node /mnt -o 'context=system_u:object=tmp:s0:c127,c456,noexec'
```

**defaults** 使用默认选项：**`rw, suid, dev, exec, auto, nouser 和 async`。**

注意，所有默认挂载选项的实际集合取决于内核和文件系统类型。更多信息请参阅本节开头。



`dev` 解析文件系统上的字符或块特殊设备。`nodev` 不要解析文件系统上的字符或块特殊设备。`diratime` 更新此文件系统上的目录访问时间。这是 `nodiratime` 不在此文件系统上更新 inode 访问时间。`dirsync` 文件系统内的所有更新都应同步进行。这允许 `create`, `link`, `unlink`, `symlink`, `mkdir`, `rmdir`, `rename` 和 `rename`。`exec` 允许执行二进制文件。`noexec` 不允许在挂载的文件系统上直接执行二进制文件。（直到最近，还可以使用命令如 `/lib/ld.so` `/mnt/` 来运行二进制文件）。`group` 允许普通用户（即非 root）挂载文件系统，如果其所属的某个组与设备匹配。这包括 `nosuid` 和 `node`（除非被后续选项覆盖，如选项行中的 `version` 每次修改 inode 时，`noatime` 不在此文件系统上更新 inode 访问时间。`nosuid` 不允许设置用户标识位。`nodev` 不允许设置用户标识位。`_netdev` 该文件系统位于网络上。`nofail` 如果设备不存在则不报告错误。`relatime` 更新 inode 访问时间。`sync` 到文件系统的所有 I/O 都应同步进行。

建议的格式为 `x-<appname>.<option>`（例如 `x-systemd.automount`）。`x-mount.mkdir[<mode>]` 允许创建一个目标目录（挂载点）。可选参数 `<mode>` 指定了以八进制表示的用于 `mkdir(2)` 的文件系统访问模式。默认模式为 0755。此功能仅支持 root 用户。

# 特定于文件系统的挂载选项

以下选项仅适用于某些文件系统。我们按照文件系统对其进行排序。

它们都遵循 `-o` 标志。

支持哪些选项取决于运行的内核。更多信息可以在内核源码子目录 `Documentation/filesystems` 中找到。

# ADFS 的挂载选项

`uid=value` 和 `gid=value`

设置文件系统中文件的所有者和组（默认：`uid=gid=0`）。

`ownmask=value` 和 `othmask=value`

分别为 ADFS 的“所有者”权限和“其他”权限设置权限掩码（默认分别为 0700 和 0077）。另请参见 `/usr/src/linux/Documentation/filesystems/adfs.txt`。

# AFFS 的挂载选项

`uid=value` 和 `gid=value`

设置文件系统根的所有者和组（默认：`uid=gid=0`，但如果使用了未指定具体值的 uid 或 gid 选项，则采用当前进程的 uid 和 gid）。

`setuid=value` 和 `setgid=value`

设置所有文件的所有者和组。

`mode=value`

将所有文件的所有者设置为 `value & 0777`，忽略原始权限。为具有读取权限的目录添加搜索权限。该值以八进制给出。

`protect`

不允许允许对文件系统上的保护位进行任何更改。

`usemp`

在第一次同步或卸载时，将文件系统根的 uid 和 gid 设置为挂载点的 uid 和 gid，然后清除此选项。很奇怪……

`verbose`

为每次成功挂载打印一条信息消息。

`prefix=string`

在跟随链接时，在卷名之前使用的前缀。

`volume=string`

在跟随符号链接时，在 '/' 之前使用的前缀（长度最多 30）。

`reserved=value`

（默认：2。）设备开头未使用的块块数。

`root=value`

显式指定根块的位置。

`bs=value`

指定块大小。允许的值为 512, 1024, 2048, 4096。

`grpquota|noquota|quota|usrquota`

这些选项会被接受但被忽略。（然而，quota 工具可能会对 `/etc/fstab` 中的字符串做出反应）。

# CIFS 的挂载选项

请参见 `mount.cifs(8)` 手页的选项部分（必须安装 cifs-utils 包）。

# COHERENT 的挂载选项

无。

# DEBUFS 的挂载选项

`debugfs` 文件系统是一个伪文件系统，传统挂载在 `/sys/kernel/debug`。从内核版本 3.4 开始，`debugfs` 具有以下选项：

`uid=n`, `gid=n`

设置挂载点的所有者和组。

`mode=value`

设置挂载点的模式。

# DEVPTS 的挂载选项

`devpts` 文件系统是一个伪终端，传统挂载在 `/dev/pts`。为了获取伪终端，进程打开 `/dev/ptmx`；随后伪终端的编号将提供给该进程，伪终端从可以通过 `/dev/pts/<number>` 访问。

这会将新创建的 PTY 的所有者或组设置为指定值。如果未指定，它们将设置为创建进程的 UID 和 GID。例如，如果有一个设备为 5 的 tty 组，`gid=5` 将导致新创建的 PTY 属于 tty 组。

将新创建的 PTY 的模式设置为指定值。默认为 0600。`mode=620` 和 `gid=5` 的值使得 "mesgy" 成为新创建 PTY 上的默认值。

创建一个 `devpts` 文件系统的私有实例，使得在此新实例中分配的 pty 索引独立于 `devpts` 其他实例中创建的索引。

所有不带此 `newinstance` 选项的 `devpts` 挂载都共享同一组 pty 索引（即旧模式）。每个带有 `newinstance` 选项的 `devpts` 挂载都有私有的 pty 索引集。

此选项主要用于支持 Linux 内核中的容器。它从 2.6.29 版本的 Linux 内核开始实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

要有效使用此选项，`/dev/ptmx` 必须是指向 `pts/ptmx` 的符号链接。详情请参见 Linux 内源码中的 `Documentation/filesystems/devpts.txt`。

为 `devpts` 文件系统中新的 `ptmx` 设备设置模式。

为了兼容旧内核，`newinstance` 选项在从 2.6.29 开始的 Linux 内核版本中不再实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

此选项主要用于支持 Linux 内核中的容器。它从 2.6.29 版本的 Linux 内核开始实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

# EXT 的挂载选项

无。注意，`ext4` 不支持，但 `mfs2fs(8)` 支持。

# EXT2 的挂载选项

`ext2` 文件系统预留了可用空间的百分比（默认为 5%，见 `mke2fs(8)` 和 `tune2fs(8)`）。这些选项决定了谁可以使用预留块。（大致：具有指定 uid 或属于指定组的用户。）

# EXT3 的挂载选项

`ext3` 文件系统是日志文件系统。默认启用日志（见 `mke2fs(8)` 和 `tune2fs(8)`）。

# EXT4 的挂载选项

`ext4` 文件系统是大多数现代 Linux 发行版的默认选择。它支持许多功能，如 extents 和延迟分配（见 `mke2fs(8)` 和 `tune2fs(8)`）。

# EXT3 挂载选项

`ext3` 文件系统是 `ext2` 文件系统的一个版本，增加了日志（journaling）功能。它支持 `ext2` 的所有选项，以及以下新增选项：

- `journal=update`

将 `ext3` 文件系统的日志更新为当前格式。

- `journal=inum`

当日志已存在时，此选项将被忽略。否则，它指定了代表 `ext3` 文件系统日志文件的 inode 编号；`ext3` 将创建一个新日志，并覆盖编号为 `inum` 的文件的旧内容。

- `journal_dev=devnum`

当外部日志设备的主设备号/次设备号发生变化时，此选项允许用户指定新的日志位置。日志设备通过其编码在 `devnum` 中的新主设备/次设备号来识别。

- `norecovery=noload`

挂载时不加载日志。请注意，如果文件系统不是以干净的方式卸载的，跳过日志重放（replay）将导致文件系统包含不一致的内容，从而引发各种问题。

- `data={journal=ordered|writeback}`

指定文件数据的日志模式。元数据记录日志。若要在根文件系统上除 `ordered` 以外的模式，请将该模式传递给内核，例如 `rootflags=data=journal`。

- `journal`

所有数据在写入主文件系统之前都会提交到日志中。

- `ordered`

这是默认模式。在元数据提交到日志之前，所有数据都会被强制直接写入主文件系统。

- `writeback`

不保留数据顺序 - 数据可能在元数据提交到日志后才写入主文件系统。据传这是吞吐量最高的选项。尽管，它保证了文件系统内部的完整性，但可能允许在崩溃和日志恢复后，文件中出现旧数据。

- `barrier=0` / `barrier=1`

启用/禁用屏障（barriers）。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

# EXT4 挂载选项

`ext4` 文件系统是 `ext3` 文件系统的高级版本，它结合了扩展性和可靠性增强，以支持大文件系统。

选项 `journal_dev`, `noload`, `data`, `commit`, `orlov`, `oldalloc`, `[nouser_xattr]` `[noacl]`, `bsdmf`, `minid`, `debug`, `errors`, `data_err`, `grpid`, `bsgrroups`, `nogprid`, `sysgroups`, `resgid`, `resid`, `sb`, `quota`, `noquota`, `grpquota`, `usrjquota`, `jrpquota` 和 `jqfmnt` 与 `ext3` 和 `ext2` 向后兼容。

- `journal_checksum`

启用日志事务的校验和检查。这将允许 `e2fsck` 中的恢复代码和内核检测内核中的损坏。这是一个兼容性更改，旧版本的内核会忽略它。

- `journal_async_commit`

提交块可以在不等待描述符块（descriptor blocks）的情况下直接写入磁盘。如果启用，旧版本内核将无法挂载该设备。这将内部启用 `journal_checksum`。

- `barrier=0`/`barrier=1`

这启用/禁用屏障。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

- `journal_checksum`

启用日志事务的校验和检查。这将允许 `e2fsck` 中的恢复代码和内核检测内核中的损坏。这是一个兼容性更改，旧版本的内核会忽略它。

- `journal_async_commit`

提交块可以在不等待描述符块的情况下直接写入磁盘。如果启用，旧版本内核将无法挂载该设备。这将内部启用 `journal_checksum`。

- `barrier=0`/`barrier=1`

这启用/禁用屏障。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

## FAT 挂载选项

(注意：`fat` 并不是独立的文件系统，而是 `mdsdos`、`umsdos` 和 `vfat` 文件系统的共同部分。)

`blockSize={512|1024|2048}`

设置块大小（默认值为 512）。此选项已过时。

`uid=value` and `gid=value` 设置所有文件的所有者和组。（默认值：当前进程的 uid 和 gid）

`umask=value`

设置 `umask`（未包含的权限位）。默认值为当前进程的 `umask`。值以八进制形式给出。

`dmask=value`

设置仅应用于目录的 `umask`。默认值为当前进程的 `umask`。值以八进制形式给出。

`fmask=value`

设置仅应用于普通文件的 `umask`。默认值为当前进程的 `umask`。值以八进制形式给出。

`allow_utime=value`

此选项控制 `mtime.atime` 的权限检查。

如果当前进程是文件组 ID 的成员，则你可以更改时间戳。

其他用户也可以更改时间戳。默认取决于 `dmask` 选项设置。如果目录可写，也允许 `utime(2)`。即 `-dmask & 22`。

通常 `utime(2)` 检查当前进程是否为文件所有者或具有 `CAP_FOWNER` 权限。FAT 文件系统在磁盘上没有 uid/gid，因此普通检查缺乏活性。通过此选项你可以放宽限制。

`check=value` 可以选择三种严格程度的检查：

- `r[relaxed]`: 接受并等同大小写，长文件名部分会被截断（例如，`verylongname.foobar` 变为 `verylong.foo`），每个名称部分（文件名和扩展名）允许前导和嵌入空格。

- `n[normal]`: 与 `relaxed` 类似，但拒绝许多特殊字符（*、?、空格等）。这是默认值。

- `s[strict]`: 与 `normal` 类似，但名称可能包含 Linux 使用但 MS-DOS 不接受的长部分和某些特殊字符（+、=、空格等）。

`value=value` 设置在 FAT 和 VFAT 文件系统上转换为短名称时使用的代码页。默认使用代码页 437。

`conv={b[binary]|[ext][auto]}` Fat 文件系统可以在内核中执行 CRLF<->NL（MS-DOS 文本格式到 UNIX 格式）转换。可用以下转换模式：

- 不进行任何翻译。这是默认值。

- `text`: 对所有文件进行 CRLF<->NL 翻译。

- `auto`: 对所有没有“已知”扩展名的文件进行 CRLF<->NL 翻译。已知扩展名列表可以在 `sfs/misc.c` 的开头找到（从 2.0 开始，列表为：`exe, com, bin, app, sys, drv, ovl, ovr, obj, bib, dll, pif, arc, zip, lha, lzha, zoo, tar, z, arj, tz, tzp, ptz, gz, tgz, def, gib, mtif, gl, jpg, pxcm, tfm, vf, gf, pk, pxl, dvi`）。

使用 `Iseeks` 而不是内核文本转换的程序。某些人的数据因这种翻译而损坏了。请小心！

对于以二进制模式挂载的文件系统，提供了转换工具（`fromdos/tomdos`）。此选项已过时。

`cvf_format=module` 强制驱动程序使用 CVF（压缩卷文件）模块而不是自动检测。内核支持它们，`cvf_format=xxx` 选项也控制按需加载 CVF 模块。此选项已过时。

`debug` `cvf_option=option` 传递给 CVF 模块。此选项已过时。开启调试标志。打印字符串和文件系统参数列表（如果参数看起来一致，也会打印这些参数）。如果设置，当块空闲时向块设备发出丢/TRIM 命令。这对于 SSD 设备和稀疏/稀填充 LUN 很有用。



`fat={12|16|32}` 指定 12、16 或 32 位。这将覆盖自动 FAT 类型检测。请谨慎使用！

`charset=value` 用于转换 8 位字符和 16 位 Unicode 的字符集。默认是 `utf8859-1`。长文件名以 Unicode 格式存储。

`Nfs` 如果设置，将启用目录项的内存索引，以减少 NFS 客户端操作中 `EXTALE` 错误的范围。仅在文件系统通过 NTFS 导出时使用。

`UTC` 此选项禁用从本地时间（Windows 在 FAT 上使用）到 UTC（Linux 内部使用）的时间戳转换。这在挂载设置为 UTC 的设备（如数字相机）时特别有用，可以避免本地时间的陷阱。

`Quiet` 开启静默标志。尝试检查子文件会返回错误，尽管它们会失败。请谨慎使用！

`showexec` 如果设置，只有当文件的扩展部分为 `.EXE`、`.COM` 或 `.BAT` 时，才允许文件的执行权限位。默认关闭。

`FAT` 上的 `sysATTR_SYS` 属性被处理为 Linux `IMMUTABLE`（不可变）标志。默认关闭。

如果设置，文件系统将尝试比通常频繁地刷新磁盘。默认关闭。

`usefree` `FSINFO` 的“空闲簇”视图。它将用于确定空闲簇的数量。对于 Rock Ridge 无意义。

如果文件长度的高字节包含其他垃圾数据，设置此挂载选项以忽略文件长度的高位位。这意味着文件不能大于 16MB。

```
session=x
```

在多会话 CD 上选择会话数量。（自 2.3.4 版本起）

```
sbsector=xxx
```

Session 从扇区 `xxx` 开始。（自 2.3.4 版本起）

以下选项与 `vfat` 相同，只有在使用使用微软 Joliet 扩展进行编码的光盘时，指定这些选项才有意义。

```
iocharset=value
```

用于将 CD 上的 16 位 Unicode 字符转换为 8 位字符的字符集。默认值为 `iso8859-1`。

```
utf8
```

将 CD 上的 16 位 Unicode 字符转换为 UTF-8。

# JFS 挂载选项

`iocharset=name`

用于从 Unicode 转换为 ASCII 的字符集。默认不进行转换。使用 `charset=utf8` 进行 UTF8 翻译。这需要在内核内核的 `.config` 文件中设置 `CONFIG_NLS_UTF8`。

`resize=value`

将卷调整大小为块。JFS 只支持扩展卷，不支持缩小卷。此选项仅在以读写模式挂载卷的重新挂载期间有效。`resize` 若不带值，将卷扩展到整个分区的大小。

`nointegrity`

不写入日志。此选项的主要用途是允许在从备份介质恢复卷时获得更高的性能。如果系统异常结束，则无法保证卷的完整性。

`integrity`

默认值。将元数据更改提交到日志。使用此选项重新挂载之前指定了 `nointegrity` 选项的卷，以恢复正常行为。

`errors={continue|ro|panic}`

定义遇到错误时的行为。（忽略错误并仅标记文件系统为错误并继续，或将文件系统重新挂载为只读，或发生恐慌并停止系统。）

`noquota|quota|usrquota|grpquota`

这些选项会被接受但忽略。

# MINIX 挂载选项

无。

# MSDOS 挂载选项

参见 `fat` 的挂载选项。如果 `msdos` 文件系统检测到不一致，它会报告错误并将文件系统设置为只读。可以通过重新挂载使文件系统恢复为可写。

# NCPFS 挂载选项

与 `nfs` 一样，`ncpfs` 实现向 `mount` 系统调用期望一个二进制参数（`struct nfs_mount_data`）。该参数由 `mount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `ncpfs` 的信息。

# NFS 和 NFS4 挂载选项

参见 `nfs(5)` 手页的选项部分（必须安装 `nfs-utils` 包）。`nfs` 和 `nfs4` 实现向 `mount` 系统调用期望一个二进制参数（`struct nfs_mount_data`）。该参数由 `mount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `nfs` 和 `nfs4` 的信息。

# NTFS 挂载选项

`iocharset=name`

返回文件名时使用的字符集。与 VFAT 不同，NTFS 会抑制包含不可读字符的名称。已废用。

`nls=name`

早名为 `iocharset` 的选项的新名称。

`utf8`

使用 UTF-8 转换文件名。

`uni_xlate=[0|1|2]`

对于 0（或 'no' 或 'false'），对未知字符不使用转义序列。对于 1（或 'yes' 或 'true'）或 2，使用以 "." 开头的 `vfat` 式四字节转义序列。

`posix=[0|1]`

如果启用（`posix=1`），文件系统将区分大小写名称，并以硬链接形式呈现而非抑制。

`uid=value`, `gid=value` and `umask=value`

设置文件系统上的文件权限。默认以八进制形式给出文件。由 root 拥有，其他人不可读。

# PROC 挂载选项

```
uid=value and gid=value
```

这些选项被识别，但据我所知它们没有影响。

# RAMFS 挂载选项

`Ramfs` 是一个基于内存的文件系统。挂载它就拥有它。卸载它就消失了。自 Linux 2.3.9 起存在。没有挂载选项。

# REISERFS 挂载选项

`Reiserfs` 是一个日志文件系统。指示 3.6 版本的 `reiserfs` 软件挂载 3.5 版本的系统系统，使用 3.6 格式处理新创建的对象。该文件系统将不再与 `reiserfs` 工具兼容。

`hash={reiserfs|r5|detect}`

选择 `reiserfs` 使用何种哈希函数在目录内查找文件。

由 Yuki Yu 发明的 `reiserfs` 哈希函数。它速度快且保留局部性，将字典顺序上接近的文件名映射到接近的哈希值。不应使用此选项，因为它会导致高概率的冲突。

由 Jeremy Fitzhardinge 实现的 Davis-Meyer 文件系统。它使用哈希排列名称中的位。它具有高随机性，因此在某些 CPU 开销下具有低哈希冲突概率。如果在使用 `r5` 哈希时遇到 `HASHISION` 错误，可以使用此项。

修改后的 `reiserfs` 哈希。默认使用它，除非文件系统具有巨大的目录和异常的文件名模式，否则最佳选择。

通过检查正在挂载的文件系统来检测使用的是何种哈希函数，并将此信息写入 `reiserfs` 超数据块（`superblock`）。这仅在首次挂载旧文件系统时有用。

`hashed_relocation` 调整块分配器。这在某些情况下可能提供性能改进。

`no_unhashed_relocation` 调整块分配器。这在某些情况下可能提供性能改进。

`noborder` 禁用 Yuki Yu 发明的边界算法。这在某些情况下可能提供性能改进，但代价是失去 `reiserfs` 从崩溃中恢复的能力。开启此选项时，`reiserfs` 执行所有的日志操作，写入其日志区域的除外。`nolog` 的实现正在进行中。

`notail` 默认情况下，`reiserfs` 将小文件和“文件尾部”（`file tails`）直接存储在树中。

`replay` 使用 `reiserfsck` 重放日志中的事务。

`resize=number` 重新挂载选项，允许分区在线扩展。用于逻辑卷管理（LVM）。`user_xattr` 扩展属性。`attr(5)` 手页。

`enable` POSIX 访问控制列表。`acl(5)` 手页。

`barrier=none/flush` 启用或禁用日志代码中的写入屏障，以强制磁盘提交的正确顺序。`reiserfs` 文件系统默认不启用屏障。除非你的磁盘有电池保护，否则掉电时会导致文件系统损坏。

# ROMFS 挂载选项

无。

# QUASHFS 挂载选项

无。

# SMBFS 挂载选项

与 `nfs` 一样，`smbfs` 实现向 `mount` 系统调用期望一个二进制参数（`struct smb_mount_data`）。该参数由 `smount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `smbfs` 的信息。

# SYSV 挂载选项

无。

# TMPFS 挂载选项

`size=nbytes` 覆盖文件系统的默认大小。大小以字节给出，并向上对齐到整页。默认是内存的一半。当未指定 `size` 或 `nr_blocks` 时，`size` 参数也接受后缀 `%` 以将此 `tmpfs` 实例限制为物理内存的百分比：默认为 `size=50`

`nr_blocks=` 与 `size` 相同，但单位是 `PAGE_CACHE_SIZE`

`nr_inodes=` 该实例的最大 inode 数量。默认是物理内存页数，或（在具有高内存的机器上）低内存页数，取两者较小者。

`tmpfs` 尺寸挂载选项（`size`, `nr_blocks` 和 `nr_inodes`）接受后缀 `k`, `m` 或 `g`（对应二进制单位 klo, mega 和 giga），并可以在重新挂载时更改。

`mode=` 设置根目录的初始权限。

`uid=` 用户 ID。

`gid=` 组 ID。

`mpol=[default[prefer:Node|bind:NodeList|interleave|interleave:NodeList]]` 为该实例中的所有文件设置 NUMA 内存分配策略（如果内核启用了 `CONFIG_NUMA`）——动态调整：`mount remount ...`

`default` 优先从本地节点分配内存

`prefer:Node` 优先从给定的 Node 分配内存

`bind:NodeList` 仅从 NodeList 中的节点分配内存

`interleave` 交替从每个节点分配

`interleave:NodeList` 交替从 NodeList 中的每个节点分配

`NodeList` 格式为逗号分隔的数字和范围列表，范围是两个由连字符分隔的数字，表示范围内最小和最大的节点编号。例如，`mpol=bind:0-3,5,7-95`

因此，建议从自动挂载选项中省略 `mpol` 选项。当 `tmpfs` 已经挂载到 `MountPoint` 时，可以通过 `mount -o remount,mpol=Policy:NodeList MountPoint` 将其添加。

# UBIFS 挂载选项

`UBIFS` 是一种运行在 `UBI` 卷之上的闪存文件系统。注意，不支持 `atime` 且始终处于关闭状态。设备名称可以指定为：

- `ubiX_Y`：设备号 X，卷号 Y
- `ubiY`：设备号 0，卷号 Y
- `ubiX:NAME`：设备号 X，名为 NAME 的卷
- `ubi:NAME`：设备号 0，名为 NAME 的卷

可以使用替代的分隔符 `!` 代替 `:`。以下是可用的挂载选项：

- `bulk_read`: 启用批量读取。禁用 VFS 预读，因为会减慢文件系统。批量读取是一种内部优化。如果数据位于一个 0 而不是分散在多个读取请求中，某些闪存的读取可能会更快。例如，OneNand 在读取超过一个 NAND 页时会执行“边读边加载”。
- `no_bulk_read`: 不进行批量读取。这是默认值。
- `chk_data_crc`: 检查数据 CRC-32 校验和。这是默认值。
- `no_chk_data_crc`: 不检查 CRC-32 校验和。使用此选项时，文件系统在读取时不检查 CRC-32，但会在内部索引信息上进行检查。此选项仅影响读取，不影响写入。写入数据时始终会计算 CRC-32。
- `compr={none|lzo|zlib}`: 选择在写入新文件时使用的默认压缩器。如果使用 `none` 选项挂载，仍然可以读取压缩文件。

# UDF 挂载选项

`udf` 是由光存储技术协会定义的“通用磁盘格式”文件系统，通常用于 DVD-ROM。另请参考 `iso9660`。

- `gid=`: 设置默认组。
- `umask=`: 设置默认 umask。值为八进制表示。
- `uid=`: 设置默认用户。
- `hide=`: 显示原本隐藏的文件。
- `ndelete`: 在列表中显示已删除的文件。
- `nostrict`: 取消严格一致性。
- `iocharset`: 设置 NLS 字符集。
- `bs=`: 设置块大小。（除非为 2048，否则可能无效）。
- `novrs`: 跳过卷序列识别。
- `session=`: 设置 CDROM 会话从 0 开始计数。默认值：最后一个会话。
- `anchor=`: 覆盖标准的锚点位置。默认值：256。
- `volume=`: 覆盖 VolumeDesc 的位置。（未使用）。
- `partition=`: 覆盖 PartitionDesc 的位置。（未使用）。
- `lastblock=`: 设置文件系统的最后一个块。
- `fileset=`: 覆盖 fileset 块位置。（未使用）。
- `rootdir=`: 覆盖根目录位置。（未使用）。

# UFS 挂载选项

`ufstype=value`

`UFS` 是一种广泛用于不同操作系统的文件系统。问题在于不同实现之间的差异。某些实现实现的功能没有文档说明，因此很难通过挂载选项识别 `ufs` 的类型。这就是为什么用户必须通过挂载选项指定 `ufs` 的类型。可能的值有：

- `old`: `ufs` 的旧格式，这是默认值，只读。（不要忘记提供 `-r` 选项。）
- `44bsd`: 用于由类 BSD 系统（NetBSD, FreeBSD, OpenBSD）创建的文件系统。
- `ufs2`: 用于 FreeBSD 5.x，支持读读写。
- `5xbsd`: `ufs2` 的别名。
- `sun`: 用于在 Sparc 上由 SunOS 或 Solaris 创建的文件系统。
- `sunx86`: 用于在 x86 上由 Solaris 创建的文件系统。
- `hp`: 用于 HP-UX 创建的文件系统，只读。
- `nextstep`: 用于由 NeXTStep（在 NeXT 工作站上）创建的文件系统（目前为只读）。
- `nextstep-cd`: 用于 NextStep CDROM（`block_size == 2048`），只读。
- `openstep`: 用于 OpenStep 创建的文件系统（目前为只读）。Mac OS X 也使用相同的文件系统类型。
- `onerror=value`: 设置发生错误时的行为。
- `panic`: 如果遇到错误，导致内核恐慌（`kernel panic`）。
- `[lock|umount|repair]`: 这些挂载选项目前不起作用；当遇到错误时，会在控制台打印消息。

# UMSDOS 挂载选项

请参考 `msdos` 的挂载选项。`dotsOK` 选项会被 `umsdos` 显式禁用。

# VFAT 挂载选项

首先，`fat` 的挂载选项会被识别。`dotsOK` 选项会被 `vfat` 显式禁用。此外还有

- `uni_xlate`: 将未处理的 Unicode 字符翻译为特殊的转义序列。这允许你备份和恢复用 Unicode 字符创建的文件名。如果没有此选项，在可以翻译时将使用 '?'。转义字符是 ':'；因为否则在 `vfat` 文件系统上是非合法的。使用的转义序列（其中 u 是 Unicode 字符）为：':', `(u & 0x3f), ((u>>6) & 0x3f), (u>>12)`。
- `posix`: 允许两个文件名大小不同的文件。此选项已过时。
- `nonumalt`: 在尝试 `name~name.ext` 之前，先尝试创建一个没有序列的短名称。
- `utf8`: UTF8 是控制台使用的 Unicode 文件系统 8 位编码。可以通过此选项为文件系统启用它。
- `shortname={lower|win95|mixed}`: 定义了符合 8.3 字符的文件名在创建和显示时的行为。如果启用 `utf8`，有四种模式：
    - `lower`: 强制短名称为小写，存储时短文件名不为大写。
    - `win95`: 强制短名称为大写，存储时短文件名不为大写。
    - `mixed`: 以原始方式显示，存储时短文件名不为大写。从 2.6.32 起即为默认值。

# USBFS 挂载选项

- `devuid=devgid=devmode=`: 定义新创建的文件获取的组 ID。当设置了 `devgid` 时，它获取所在目录的组 ID；否则它获取当前进程的 fgid，除非目录设置了 setgid 位。
- `busuid=busgid=busmode=`: 设置文件系统中 bus 目录的所有者、组和模式（默认值：`uid=0, mode=0644`）。
- `listuid=listgid=listmode=`: 设置 list 设备的所有者、组和模式（默认值：`uid=0, mode=0555`）。

# XENIX 挂载选项

无。

# XFS 挂载选项

- `allocsize=size`: 在进行延迟分配时设置缓冲 I/O 的尾文件预分配大小。此选项的有效值为页大小（通常为 4KiB）到 1GiB，按 2 的幂增加。默认行为是动态尾文件预分配大小，它根据文件内部模式使用启发式方法优化预分配大小。
- `attr2|noattr`: 这些选项启用/禁用对内联扩展属性存储方式的一种改进。当选择 `attr2` 时（在设置或删除扩展属性时）首次使用新格式，磁盘特性字段将更新以反映使用该格式。默认行为由磁盘特性指示 `attr2` 行为是否激活决定。如果设置了任何一个挂载选项，它将成为文件系统的新默认。启用 CRC 的文件系统始终使用 `attr2` ，因此将拒绝 `noattr` 挂载选项。
- `barrier|nobabler`: 启用/禁用用于日志和数据完整性操作的块层写入屏障。这允许支持写入屏障的设备驱动级缓存。
- `discard|nodiscard`: 向块设备发送命令以回收文件系统释放的空间。这对于 SSD 设备、精简的 LUN 和虚拟机镜像有用，可能会对性能产生。注意：目前建议使用 `fstrim` 应用程序通过 `discard` 挂载选项删除不需要的块，因为该选项对性能影响非常严重。
- `filestreams`: 让数据分配器在整个文件系统使用 filestreams 分配模式，而不仅仅是配置它的目录。当指定了 `keepib` 时，XFS 不删除空 簇并保留它们 ...磁盘。当未指定 `noed` 时，会将空 inode 簇返回到空闲空间。

## `inode32|inode64`

当指定 `inode32` 时，表示 XFS 将 inode 的创建限制在不会导致 inode 号的有效位 超过 32 位的位置。

当指定 `inode64` 时，表示 XFS 允许在文件系统的任何位置创建 inode，包括那些会导致 inode 号占用超过 32 位有效位的位置。



提供 `inode32` 是为了与旧系统和应用程序向后兼容，因为 64 位 inode 可能会给某些无法处理大 inode 号的应用程序带来问题。如果使用的应用程序不支持大于 32 位的 inode 号，则应该指定 `inode32` 选项。

## largeio|nolarargeio

如果指定 `nolarargeio`，则 `stat(2)` 在 `stat_blks` 中报告的最优 I/O 将尽可能减小，以允许用户应用程序避免低效的读/写 I/O。这通常是机器的页大小，因为这是页缓存的粒度。

如果指定 `largeio`，则使用指定了 `swidth` 创建的文件系统将在 `stat_blks` 中返回 `swidth` 值（单位为字节）。如果文件系统没有 `swidth` 但指定了 `allocsize`（单位为字节），则返回后者。否则，行为与指定了 `nolarargeio` 相同。

## logbuffs=value

设置内存中日志缓冲区的数量。有效数字范围为 2-8（包含）。

默认值为 8 个缓冲区。

如果在小型系统上 8 个日志缓冲器的内存成本过高，可以减少数量，但以牺牲元数据密集型工作负载的性能为代价。`logsize` 选项控制每个缓冲区的大小并并此情况相关。

## logsize=value

设置每个内存日志缓冲区的大小。大小可以以字节指定，也可以带有“k”后缀指定。版本 1 和版本 2 日志的有效大小包括 65536 (64k)、32768 (32k)、131072 (128k) 和 262144 (256k)。`logsize` 必须是 `mkfs` 时配置的日志条带单元的整数倍。版本 1 的默认值为 32768，而版本 2 的默认值为 MAX(32768, log_unit)。

## logdev=device|dev=device

使用外部日志（元数据日志）或实时设备。XFS 文件系统最多有三个部分：数据段、日志段和实时段。实时段是可选的，日志段可以与数据段分离，也可以包含在其中。

## noalign

数据分配将不在条带边界处对齐。这仅对于使用 `mkfs` 创建了非零对齐参数（unit, width）的文件系统相关。

## norecovery

挂载文件系统时不运行日志恢复程序。如果文件系统没有干净地卸载，那么在 "norecovery" 模式下挂载时可能是不一致的。由于此，某些文件或目录可能无法访问。挂载 "norecovery" 文件系统必须是只读的，否则挂载将失败。

## nouuid

不检查双 uuid。这对于结合 "norecovery" 挂载只读快照有用。

## noquota

强制关闭文件系统内的所有配额计算和强制执行。

## uquota|usrquota|nogquota

启用用户磁盘计数，并（可选地）强制限制。更多细节请参阅 `xfs_quota(8)`。

## gquota|grpquota|nogquota

启用组磁盘计数，并（可选地）强制限制。更多细节请参阅 `xfs_quota(8)`。

## pquota|prquota|noproquota

启用项目磁盘计数，并（可选地）强制限制。更多细节请参阅 `xfs_quota(8)`。

## unit=value and width=value

用于指定 RAID 设备或条带卷的条带单元和宽度。"value" 必须以 512 字节为单位指定。这些仅对于创建了非零数据对齐的文件系统相关。`unit` 和 `width` 参数必须与现有的文件系统对齐兼容。通常，有效的 `width` 值是整数倍。通常在修改底层 RAID 设备的几何结构后（例如向 RAID5 添加新磁盘并进行重塑），仅需要这些挂载选项。

## swalloc

当扩展当前文件末尾且且文件大小大于条带宽度时，数据分配将向上取整到条带边界。

## wsync

指定时，所有文件系统命名空间操作将同步执行。这确保了当命名空间操作（创建、取消链接等）完成时，命名空间的更改已在稳定存储上。这对于 HA 集合非常有用，因为故障转移不能导致客户端在故障转移事件后看到不一致的命名空间呈现。

## MOUNT OPTIONS FOR XIAFS

无。虽然 xiafs 没有问题，但它并不常用，且没有被维护。可能不应该使用它。自 Linux 版本 2.1.21 起，xiafs 不再是内核源码的一部分。

## LOOP DEVICE

另一种可能的类型是通过回环设备挂载。例如，命令 `mount /tmp/disk.img /mnt -t vfat -o loop=/dev/loop` 将设置回环设备 `/dev/loop` 对应文件 `/tmp/disk.img`，然后将该设备挂载到 `/mnt`。

如果没有显式提到设备（仅给出 `-o loop`），则 `mount` 将尝试查找未使用的回环设备，例如：

`mount /tmp/disk.img /mnt -o loop`

如果未指定文件系统类型（对于 libblkid 已知的文件系统），或者未指定文件系统类型，`mount` 会自动从普通文件创建回环设备，例如：

```
mount /tmp/disk.img
```

```
mount -t ext3 /tmp/disk.img
```

这种类型的 `mount` 知道 `loop`、`offset` 和 `size` 等选项，这些是 `loopup(8)` 的选项。（对于特定于文件系统的选项。）自 Linux 2.6.25 起支持自动销毁回环设备，可以使用 `loopup -d` 或 `umount -d` 手动释放回环设备。

## RETURN CODES

`mount` 有以下返回码（可以进行位或）：

- 0 成功
- 1 错误的调用或权限
- 2 系统错误（内存不足、无法 fork、无更多回环设备）
- 4 `mount` 内部错误
- 8 用户中断
- 16 写入或锁定 `/etc/itab`
- 32 挂载失败
- 64 部分挂载成功

命令 `mount -a` 返回 0（全部成功）、32（全部失败）或 64（部分失败，部分成功）。

## NOTES

外部挂载辅助程序的语法为：

```
/bin/mount.<suffix> spec dir [-sfnvo] [-o options] [-t type.subtype]
```

其中 `<type>` 是文件系统类型，`sfnvo` 的含义与标准挂载选项相同。`-t` 选项用于支持子类型的文件系统（例如 `/sbin/mount.fuse.sshfs`）。

## FILES

- `/etc/fstab`: 文件系统表
- `/etc/mtab`: 挂载的文件系统
- `/etc/mtab~`: 锁文件
- `/etc/mtab.tmp`: 临时文件
- `/etc/filesystems`: 可尝试的文件类型列表

## ENVIRONMENT

`LIBMOUNT_FSTAB=<path>`

覆盖 `fstab` 默认位置

`LIBMOUNT_MTAB=<path>`

覆盖 `mtab` 默认位置

`LIBMOUNT_DEBUG=0xffff`

启用调试输出

## SEE ALSO

`mount(2)`, `umount(2)`, `fstab(5)`, `umount(8)`, `swapon(8)`, `findmnt(8)`, `nfs(5)`, `xfs(5)`, `e2label(8)`, `xfs_admin(8)`, `mountd(8)`, `nfsd(8)`, `mke2fs(8)`, `tune2fs(8)`, `losetup(8)`

# 错误 (BUGS)

损坏的文件系统导致崩溃。

某些 Linux 文件系统不支持 `-o sync` 和 `-o dirsync`（ext2、ext3 和 vfat 文件系统在带有 `sync` 选项挂载时，支持同步更新（类似于 BSD 的方式））。

`-o remount` 可能无法更改挂载参数（例如，除 sb 以外，所有 ext2fs 专有的参数都可以通过 remount 更改，但你无法为 fatfs 更改 gid 或 umask）。

文件 `/etc/mtab` 和 `/proc/mounts` 可能不一致。第一个文件仅基于 `mount` 命令的选项，而第二个文件的内容取决于内核和其他设置（例如远程 NFS 服务器）。在特定情况下，`mount` 命令报告的 NFS 挂载点信息可能不可靠，而 `/proc/mounts` 文件通常包含更可靠的信息。

通过文件描述符（即 `fcntl` 和 `ioctl` 系列函数）检查 NFS 文件系统上的文件，可能会导致不一致的结果，因为即使使用了 `noac`，内核中也缺乏一致性检查。

当在较较旧的内核时，如果使用的带有 `offset` 或 `sizelimit` 选项的 `loop` 选项由于 `mount` 命令无法确认块设备的大小已按要求配置，可能会失败。这种情况可以通过在调用配置了 loop 设备的 `mount` 之前手动使用 `losetup` 命令来绕过。

# 历史 (HISTORY)

AT&T UNIX 第 5 版本已存在 `mount` 命令。

# 作者 (AUTHORS)

Karel Zak <kzak@redhat.com>

# 可用性 (AVAILABILITY)

`mount` 命令是 `util-linux` 包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# MOUNT.NFS

## 名称 (NAME)

`mount.nfs`, `mount.nfs4` - 挂载网络文件系统

## 概要 (SYNOPSIS)

```
mount.nfs remotarget dir [-rvVwfnsh ] [-o options]
```

## 描述 (DESCRIPTION)

`mount.nfs` 是 `nfs(5)` 工具包的一部分，提供了 NFS 客户端功能。

`mount.nfs` 旨在供 `mount(8)` 命令用于挂载 NFS 共享。然而，此子命令也可以作为独立命令使用，但功能有限。

`mount.nfs4` 用于挂载 NFSV4 文件系统，而 `mount.nfs` 用于挂载版本 3 或 2 的 NFS 文件系统。`remotarget` 通常是 `servername:/path/to/share` 形式。`dir` 是要挂载文件系统的目录。

## 选项 (OPTIONS)

- `-r` 只读挂载文件系统。
- `-v` 详细模式。
- `-V` 打印版本。
- `-w` 读写模式挂载文件系统。
- `-f` 伪挂载。不实际调用 `mount` 系统调用。
- `-n` 不更新 `/etc/mtab`。默认情况下，每个挂载的文件系统都会 `/etc/mtab` 中创建一个条目。使用此选项可跳过创建条目。
- `-s` 容忍宽松的挂载选项而非失败。
- `-h` 打印帮助信息。

`nfsoptions` 请参考 `nfs(5)` 或 `mount(8)` 手册页。

## 注意 (NOTE)

有关更多信息请参阅 `nfs(5)` 和 `mount(8)` 手册页。

## 文件 (FILES)

`/etc/fstab`

文件系统表

`/etc/mtab`

已挂载文件系统表

`/etc/nfsmount.conf`

NFS 挂载配置文件

## 另参 (SEE ALSO)

`nfs(5)`, `nfsmount.conf(5)`, `mount(8)`

## 作者 (AUTHOR)

Amit Gud <agud@redhat.com>

# rpc.mountd

## 名称 (NAME)

`rpc.mountd` - NFS 挂载守护进程

## 概要 (SYNOPSIS)

```
/usr/sbin/rpc.mountd [options]
```

## 描述 (DESCRIPTION)

`rpc.mount` 守护进程（此处为 rpc.mount）实现了 NFS MOUNT 协议的服务端，这是 NFS 版本 2 [RFC1094] 和 NFS 版本 3 [RFC1813] 使用的 NFS 端。

NFS 服务器维护一个本地文件系统表，供 NFS 客户端访问。此表中的每个文件系统被称为导出的文件系统，简称 export。

此表中的每个文件系统都有一个访问列表。`rpc.mount` 使用这些访问列表来确定客户端是否允许挂载。

## 挂载的文件系统 (Mounted File Systems)

NFS 协议有几个过程。其中最重要的的是 MNT (挂载) 和 UMNT (卸载)。

一个 MNT 请求有两个参数：一个包含根目录路径的显式参数，以及作为服务器句柄的隐式参数。

当从客户端接收 MNT 请求时，`rpc.mount` 会同时检查路径和导出。

## rmtab 文件 (The rmtab File)

`rpc.mount` 守护进程通过向 `rtab` 添加条目来注册每个 MNT 请求。当从客户端接收 UMNT 请求时，`rpc.mount` 从 `rtab` 中删除该条目。

客户端可以使用 `showmount(8)` 发现服务器当前导出的文件系统列表。`showmount(8)` 使用 NFS 协议。然而，并不能保证 `rtab` 内容的准确性。如果客户端在没有发送 UMNT 请求的情况下重启，该客户端将遗留过期的条目。

## 选项 (OPTIONS)

- `-d kind --debug` 有效的种类包括 all, auth, call, general 和 parse。开启调试。
- `-F --foreground` 在前台运行（不守护进程化）
- `-f export-file --exports-file` 此选项指定导出文件，列出此服务器准备好服务的客户端以及应用到每个挂载的参数。默认情况下，从 `/etc/exports` 读取导出信息。
- `-h --help` 显示用法信息。
- `-o num --descriptors num` 设置打开的文件描述符数量。默认保持不变。
- `-N mountd-version --nfs-version mountd-version` 此选项可请求 rpcmount 不提供某些 NFS 版本。当前版本的 rpcmount 支持 NFS 版本 2、3 和 4。如果不应提供这些版本之一，则必须使用 `-nfs-version <vers>` 选项调用 rpcmount。
- `-n --no-tcp` 不为你的挂载发布 TCP。
- `-P` 忽略
- `-p num --port num` 指定用于 RPC 套接字的端口号。如果未指定此选项，rpcmount 将尝试计算 `/etc/services`，如果成功则为所有监听套字设置相同的端口，否则为每个监听套字选择随机端口。当 NFS 必须穿越客户端和服务器之间的防火墙时，可以使用此选项来固定 rpcmount 监听器的端口值。
- `-H prog --ha-callout prog` 指定高可用性回调程序。该程序接收所有 MO 和 UMNT 请求的回调。用于高可用 NFS (HA-NFS) 环境的 rpcmount。回调程序带有 4 个参数运行。第一个根据回调原因是 mount 或 unmount。第二个是执行挂载的客户端名称。第三个是客户端挂载的路径。最后一个是我们认为客户端对该路径的并发挂载数量。在 2.6 及以后的内核中不需要此回调。相反，将 nfsd 文件系统挂载到 `/proc/fs/nfs`。
- `-s --state-directory-path directory` 指定用于放置状态信息的目录。如果未指定此选项，则使用默认路径 `/var/lib/nfs`。
- `-r, --reverse-lookup`

`rpc.mountd` 会跟踪 `rmtab` 文件中的 IP 地址。当某些运行中的程序（例如 `showmount -a`）发出 DUMP 请求时，它默认返回 IP 地址而不是主机名。此选项导致 rpcmountd 对 IP 地址进行反向查找并返回主机名。在某些情况下，启用此选项可能会对性能产生重大的负面影响。

- `-t N or --num-threads=N or --num-threads N`

此选项指定 `rpc.mountd` 启动的工作线程数。默认为 1 个线程，这可能足够了。对于需要在几秒内处理数百个 NFS 挂载突发流量的 NFS 服务器，或者当你的 DNS 服务器缓慢或不可靠时，通常需要更多的线程。

- `-u or --no-udp`

不为挂载发布 UDP 服务

- `-V version or --nfs-version version`

此选项可用于请求 `rpc.mountd` 提供特定版本的 NFS。

- `-v v or --version`

打印 `rpc.mountd` 的版本号并退出。

- `-g or --manage-gids`

接受用于访问控制的请求。一个 NFS 请求通常包含一个用户 ID 和一组组 ID（除非在使用 Kerberos 或其他加密认证时将用户 ID 转换为组 ID 列表除外）。由于 NFS 协议的限制，最多可以列出 16 个组 ID。如果你使用 `-g` 标志，则从客户端接收到的组 ID 列表将被通过服务器上适当的查找命令确定的组 ID 列表替换。注意，“主”组 ID不受影响，因此客户端上的 newgroup 命令仍然有效。此功能需要版本至少为 2.6.21 的 Linux 内核。

## TCP_WRAPPERS 支持

你可以使用 `tcp_wrapper` 库或 `iptables(8)` 来保护你的 `rpc_mountd` 监听器。

注意 `tcp_wrapper` 库仅支持 IPv4 网络。

将允许访问 `rpc_mountd` 的 NFS 节点主机名添加到 `/etc/hosts.allow`。即使 `rpc_mountd` 二进制文件的名称不同，也请使用守护名 `mount`。

当访问文件中使用的主机名无法解析为 IP 地址时，它们将被忽略。更多信息请参阅 `tcpd(8)` 和 `hosts_access(5)` 手页。

## IPv6 和 TI-RPC 支持

TI-RPC 是在 IPv6 上支持 NFS 的前提条件。如果 `rpc_mountd` 构建了 TI-RPC 支持，它将尝试在 `/etc/netconfig` 中标记为“visible”的网络传输上启动监听器。只要至少有一个网络传输监听器启动成功，`rpc_mountd` 就会运行。

## 文件

- `/etc/exports`

  - `exportfs` 的输入文件，列出导出、导出选项和访问控制列表
- `/var/lib/nfs/rmmtab`

  - 访问服务器导出内容的客户端表

## 查看



`exportfs(8)`, `exports(5)`, `showmount(8)`, `rpc.nfsd(8)`, `rpc.rquotad(8)`, `nfs(5)`, `tcpd(8)`, `hosts_access(5)`, `iptables(8)`, `netconfig(5)`

RFC 1094 - "NFS: 网络文件系统协议规范" RFC 1813 - "NFS 第 3 版协议规范"

## 作者

Olaf Kirch, H. J. Lu, G. Allan Morris III 以及其他许多人。

# mountstats

## 名称

`mountstats` - 显示各种 NFS 客户端的挂载统计数据

## 概要

```
mountstats [-h|help] [-v|version] [-f|file infile] [-S|sincefile] [-n|nfs] [-r|rpc] [-R|raw] [mountpoint]...
```

```
mountstats iostat [-h|help] [-v|version] [-f|file infile] [-S|sincefile] [interval] [count] [mountpoint]...
```

```
mountstats nfsstat [-h|help] [-v|version] [-f|file infile] [-S|sincefile] [-3] [-4] [mountpoint]...
```

## 描述

`mountstats` 命令为每个给定的挂载点显示各种 NFS 客户端统计数据。

如果没有给出挂载点，将显示客户端上所有 NFS 挂载点的统计数据。

# 子命令

有效的 `mountstats(8)` 子命令有：

### mountstats

显示每个操作 RPC 统计数据、NFS 事件计数和 NFS 字节数的组合。这是在未给出子命令时将执行的默认子命令。

### iostat

显示类似 iostat 的统计数据。

### nfsstat

显示类似 nfsstat 的统计数据。

## 选项

适用于所有子命令的选项

- `-h`, `--help`

显示帮助信息并退出

- `-v`, `--version`

显示程序版本号并退出

- `-f infile`, `--file infile`

从 `infile` 而不是 `/proc/self/mountstats` 读取。`infile` 的格式必须与 `/proc/self/mountstats` 相同。这可以与 `-S|since` 配合使用，以显示两个不同时间点之间的增量。这不能与 iostat 子命令的 interval 或 count 选项配合。

- `-S sincefile`, `--since sincefile`

显示当前统计数据与 `sincefile` 中数据的差异。`sincefile` 的格式必须与 `/proc/self/mountstats` 相同。这可以与 `-f|file` 选项配合使用，以显示两个不同时间点之间的增量。这不能与 iostat 的 interval 或 count 选项配合。

`mountstats` 子命令特定选项

- `-n`, `--nfs`

仅显示 NFS 统计数据

- `-r`, `--rpc`

仅显示 RPC 统计数据

- `-R`, `--raw`

仅显示原始统计数据。这旨在与 `-f|file` 和 `-S|since` 配合使用。

iostat 命令特定选项

- `-interval`

指定每个报告之间的秒数。

- `-count`

确定报告的数量。

nfsstat 命令特定选项

- `-3`

仅显示 NFS 3。

- `-4`

仅显示 NFS 4。

## 文件

- `/proc/self/mountstats`

# 查看

`iostat(8)`, `nfs(8)`, `nfsstat(8)`

## 作者

Chuck Lever <chuck.lever@oracle.com>

# MPATHCONF

## 名称

`mpathconf` - device-mapper-multipath 的工具

# 语法

```
mpathconf [commands] [options]
```

## 描述

`multipathconf` 是一个创建或修改 `/etc/` 的工具。它可以启用多路径并配置一些常用选项。`multipathconf` 还可以加载 `dm_multipath` 模块，启动和停止 `multipath`，并配置 `multipathd` 服务是否自动启动。如果没有命令调用 `multipathconf`，它将显示当前配置。

`multipathconf` 的默认选项是 `--with_module multipath` 模块，但不会立即启动。这样用户可以在启动 `multipath` 之前手动编辑其配置文件。

如果 `/etc/multipath.conf` 已经存在，`multipathconf` 将编辑它。如果不存在，`multipathconf` 将使用 `/usr/share/doc/device-mapper-multipath-0.4.9/multipath.conf` 作为起始文件。该文件设置了 `user_friendly_names`。如果此文件不存在，`multipathconf` 将从头创建 `/etc/multipath.conf`。对于大多数用户，除非他们使用 `--user-friendly-names` 命令，否则 `user_friendly_names` 将被设置。

# 命令

- `-enable`

从 `/etc/multipath.conf` 黑色列表中移除任何禁用所有节点的行。

- `-disable`

在 `/etc/multipath.conf` 黑色列表中添加禁用所有节点的行。如果不存在黑列表，它将创建一个。

- `-user_friendly_name { y | n }`

如果设置为 y，则在 `/etc/multipath.conf` 默认部分添加 `user_friendly_names yes`。如果设置为 n，则删除该行（如果存在）。此命令可以与其他任何命令一起使用。

- `-find_multipaths { y | n }`

如果设置为 y，则在 `/etc/multipath.conf` 部分添加 `find_multipaths yes`。如果设置为 n，则删除该行（如果存在）。此命令可以与其他任何命令一起使用。

## OPTIONS

- `--with_module { y | n }`

如果设置为 y，将运行 `modprobe dm_multipath` 来安装多路径模块。此选项仅在使用 `--enable` 命令时有效。此选项默认设置为 y。

- `--with_multipathd { y | n }`

如果设置为 y，则在 `--enable` 时运行 `service multipathd start` 启动多路径守护进程；在 `--disable` 时运行 `service multipathd stop` 停止 `multipathd` 守护进程；在 `--user_frindly_names` 和 `--find_multipaths` 时运行 `service multipathd reload` 重新配置 `multipathd`。此选项默认设置为 n。

## FILES

```
/etc/multipath.conf
```

## SEE ALSO

`multipath.conf(5)`, `modprobe(8)`, `multipath(8)`, `multipathd(8)`, `service(8)`

## AUTHOR

Benjamin Marzinski <bmarzins@redhat.com>

# MPATHPERSIST

## NAME

`mpathpersist`

## SYNOPSIS

```
mpathpersist [OPTIONS] [DEVICE]
```

## DESCRIPTION

选项:

- `--verbose|-v level`

详细程度级别

- `0`

关键和错误消息

- `1`

警告消息

- `2`

信息消息

- `3`

启用跟踪时的信息消息

- `--clear|-C`

PR Out: 清空

- `--device=DEVICE|-d DEVICE`

查询或跟踪 `DEVICE`

- `--help|-h`

输出此用例信息

- `--hex|-H`

以十六进制格式输出响应

- `--in|-i`

请求 PR In 命令

- `--out|-o`

请求 PR Out 命令

- `--param-aptl|-Z`

PR Out 参数 ‘APTPL’

- `--read-keys|-k`

PR In: 读取密钥 (Read Keys)

- `--param-sark=SARK|-S SARK`

PR Out 参数服务操作保留密钥 (SARK 为十六进制)

- `--preempt|-P`

PR Out: 抢占

- `--preempt-abort|-A`

PR Out: 抢占并中止

- `--prout-type=TYPE|-T TYPE`

PR Out 命令类型

- `--read-status|-s`

PR In: 读取完整状态 (Read Full Status)

- `--read-keys|-k`

PR In: 读取密钥 (Read Keys)

- `--read-reservation|-r`

PR In: 读取保留 (Read Reservation)

- `--register|-G`

PR Out: 注册 (Register)

- `--register-ignore|-I`

PR Out: 注册并忽略 (Register and Ignore)

- `--release|-L`

PR Out: 释放 (Release)

- `--report-capabilities|-c`

PR In: 报告 (Report Capabilities)

- `--reserve|-R`

PR Out: 保留 (Reserve)

- `--transport-id=TIDS|-X TIDS`

传输层 ID 可以以多种形式提及

示例:

```
mpathpersist --out --register --param-sark=123abc --prout-type=5
/dev/mapper/mpath9 mpathpersist -i -k /dev/mapper/mpath9
```

# MTR

## NAME

`mtr` - 一个网络诊断工具

## SYNOPSIS

```
mtr [-BfhvrctglxspQemniuTP46] [--help] [--version] [--report] [--report-wide] [--report-cycles COUNT] [--curses] [--split] [--raw] [--xml] [--mpls] [--no-dns] [--show-gtk] [--address IP.ADD.RE.SS] [--interval SECONDS] [--max-ttl NUM] [--first-ttl NUM] [--bitpattern NUM] [--tos NUM] [--psize BYTES | -s BYTES] [--tcp] [--udp] [--port PORT] [--timeout SECONDS] HOSTNAME [PACKETSIZE]
```

## DESCRIPTION

`mtr` 将 `traceroute` 和 `ping` 程序的功能结合在一个网络诊断工具中。

当 `mtr` 启动时，它会调查 `mtr` 运行的主机与 `HOSTNAME` 之间的网络连接。通过发送带有低 TTL 的包，它继续发送低 TTL 包，并记录中间路由器的响应时间。这允许 `mtr` 打印通往 `HOSTNAME` 的互联网路由的响应百分比和响应时间。丢包或响应时间的突然增加通常是链路不良（或仅仅是过载）的迹象。

结果通常以毫秒为往返响应时间和丢包百分比的形式报告。

## OPTIONS

- `-h`

`--help`

打印命令行参数选项的摘要。

- `-v`

`--version`

打印已安装的 `mtr` 版本。

- `-r`

`--report`

此选项将 `mtr` 置于报告模式。在此模式下，`mtr` 将按照 `-c` 选项指定的循环次数运行，然后打印统计并退出。此模式用于生成有关网络质量的统计数据。注意，每个运行的 `mtr` 实例都会产生大量的网络流量。使用 `mtr` 测量网络质量可能会导致网络性能下降。

- `-w`

`--report-wide`

此选项将 `mtr` 置于宽报告模式。在此模式下，`mtr` 不会在报告中截断主机名。

- `-c COUNT`

`--report-cycles COUNT`

使用此选项设置发送的 ping 数量，以确定所有机器。

- `-s BYTES`

`--psize BYTES`

`PACKETSIZE`

使用此选项设置包大小。

- `-w`

`--split`

使用此选项设置 `mtr` 拆分任何任何的显示方法。

- `-t`

`--curses`

使用此选项强制 `mtr` 使用 curses 终端界面。

- `-e`

`--mpls`

使用此选项强制 `mtr` 使用 RFC 4950 扩展。

- `-n`

`--no-dns`

使用此选项强制 `mtr` 不解析名称。

- `-a IP.ADD.RE.SS`

`--address IP.ADD.RE.SS`

使用此选项绑定到特定接口。

- `-i SECONDS`

`--interval SECONDS`

指定请求之间的间隔秒数。默认值为一秒。

- `-m NUM`

`--max-ttl NUM`

指定最大跳数（TTL 值）。默认值为 30。

- `-f NUM`

`--first-ttl NUM`

指定起始 TTL。默认值为 1。

- `-B NUM`

`--bitpattern NUM`

指定用于负载的位模式（bit pattern）。

- `-Q NUM`

`--tos NUM`

指定 IP 头中的服务类型值。范围 0-255。

- `-u`

`--udp`

使用 UDP 数据报文代替 ICMP。

- `-T`

`--tcp`

使用 TCP SYN 包代替 ICMP。SYN 包不包含数据。

- `-P PORT`

`--port PORT`

TCP 目标端口号。

- `-timeout SECONDS`

放弃连接前保持 TCP socket 打开的秒数。这将影响最后一跳。对于较大的值，特别是结合短间隔时，会消耗大量的文件描述符。

- `-b`

`--show-gtk`

使用此选项强制 `mtr` 使用 GTK 终端界面（如果可用）。在构建 `mtr` 时系统必须有 GTK+。信息请参考 GTK+ 网页。

- `-l`

`--raw`

使用此选项使用原始格式。该格式适用于自动化处理。

- `-x`

`--xml`

使用此选项让 `mtr` 使用 XML 输出格式。该格式更适合自动化处理。

- `-s`

`--split`

使用此选项设置 `mtr` 拆分任何其他显示方法。

- `-w`

`--report-wide`

使用此选项将 `mtr` 置于宽报告模式。

- `-o`

`--order`

使用此选项指定字段顺序。可用：

| | |
| :--- | :--- |
| h | 丢包率 |
| D | 丢包 |
| R | 接收到的包 |
| S | 发出的包 |
| N | 最新 RTT(ms) |
| B | 最佳 RTT(ms) |
| A | 平均 RTT(ms) |
| W | 最差 RTT(ms) |
| V | 标准差 |
| G | 几何平均值 |
| J | 当前抖动 |
| X | 最差抖动 |
| I | 间隔抖动 |

- `-4` 仅 IPv4。

- `-6` 仅 IPv6。

# 错误 (BUGS)

某些现代路由器对 ICMP ECHO 数据包的优先级低于其他网络流量。因此，`mtr` 报告的这些路由器可靠性将显著低于这些路由器的实际可靠性。

# 联系信息 (CONTACT INFORMATION)

最新版本请参阅 mtr 网页：`http://www.bitwizard.nl/mtr/`。

`mtr` 邮件列表很少被使用且已不再活跃。

错误报告和功能请求应提交至 launchpad mtr 跟踪器。

# 参见 (SEE ALSO)

`traceroute(8)`, `ping(8)` TCP/IP Illustrated (Stevens, ISBN 0201633469)。

# 多路路径 (MULTIPATH)

## 名称 (NAME)

`multipath` - 设备映射器目标自动配置

# 摘要 (SYNOPSIS)

```
multipath [-v verbosity] [-b bindings_file] [-d] [-h|-l|-ll|-f|-t|-F|-B|-c|-q-r|-r|-a|-A-]] [-p failover|multibus|group_by_serial|group_by_prio|group_by_node_name] [device]
```

# 描述 (DESCRIPTION)

`multipath` 用于出于故障转移或性能考虑检测指向设备的多个路径并对其进行合并。

# 选项 (OPTIONS)

`-v verbosity`，详细程度，打印所有路径和多路路径

`0` 无输出

`1` 仅打印创建或更新的多路路径名称，用于向其他工具 kpartx 输入

`2 +` 输出信息：检测到的路径、合并的路径（即多路路径）和设备映射

`-h` 打印用法

`-d` 空运行运行，不创建或更新 devmaps

`-l` 从所有可用信息显示当前的多路路径拓扑（sysfs, 设备映射器 -LL 显示当前多路路径拓扑）

`-d` dry run, do not create or update devmaps

(注：原文此处存在大量重复内容，如 `1 print the created or updated multipath names only...` 以及 `2 + print info : detected paths, coalesced paths (ie multipaths) and device maps` 之后的内容已按要求完成翻译)

`-h` print usage

`-d` dry run, do not create or update devmaps



# 多路路径 (MULTIPATH)

## 名称 (NAME)

`multipath` - Device mapper target autoconfig

## 摘要 (SYNOPSIS)

```
multipath [-v verbosity] [-b bindings_file] [-d] [-h|-l|-ll|-f|-t|-F|-B|-c|-q-r|-r|-a|-A-]] [-p failover|multibus|group_by_serial|group_by_prio|group_by_node_name] [device]
```

## 描述 (DESCRIPTION)

`multipath` 用于出于故障转移或性能考虑检测指向设备的多个路径并对其进行合并。

## 选项 (OPTIONS)

`-v verbosity`，详细程度，打印所有路径和多路路径

`0` 无输出

`1` 仅打印创建或更新的多路路径名称，用于向其他工具 `kpartx` 输入

`2` + 输出信息：检测到的路径、合并的路径（即多路路径）和设备映射

`-h` 打印用法

`-d` 空运行运行，不创建或更新 devmaps

`-l` 从所有可用信息显示当前的多路路径拓扑（sysfs, 设备映射器 `-LL` 显示当前多路路径拓扑）

## 参见 (SEE ALSO)

`traceroute(8)`, `ping(8)` TCP/IP Illustrated (Stevens, ISBN 0201633469).

## 作者 (AUTHORS)

`multipath` 由 Christophe Varoqui <christophe.varoqui@opensvc.com> 和其他人开发。

# 守护进程 (MULTIPATHD)

## 名称 (NAME)

`multipathd` - 多路守护进程

## 摘要 (SYNOPSIS)

```
multipathd [options]
```

## 描述 (DESCRIPTION)

`multipathd` 进程负责检查故障路径。当发生这种情况时，它将重新配置所属的多路映射，以便该映射恢复最大的性能和冗余。

该守护进程在事件发生时执行外部 `multipath` 工具。反之，`multipath` 工具在完成 devmap 重配置后信号 `multipathd` 进程，以便其刷新故障路径列表。

## 选项 (OPTIONS)

`-d` 空运行运行，不创建或更新 devmaps，并将所有消息输出到 stdout 和 stderr。

`-v verbosity`，详细程度，在运行 `multipathd` 时打印额外信息。级别 `0` 表示仅打印错误。级别 `3` 或更高将打印调试信息。

`-k` `multipathd` 将进入交互模式。在此模式下，可以通过输入 `help` 查看可用命令。

## 命令 (COMMANDS)

可以查看以下命令：

- `show paths`
- `show format`
- `show daemon`
- `show group`
- `show status`
- `show stats`
- `show topology`
- `show map`
- `show wildcards`
- `show config`
- `show blacklist`
- `show devices`
- `add`
- `remove`
- `resize`
- `switch switchgroup`
- `reconfigure`
- `suspend`
- `resume`
- `reset`
- `reload`
- `fail`
- `reinstate`
- `disablequeueing`
- `restorequeueing`
- `forcequeueing`
- `map|multipath $map setprstatus`

```
map|multipath $map unsetprastatus
禁用 $map 上的持久保留管理
```

```
map|multipath $map getprastatus
获取 $map 当前的持久保留管理状态
```

```
quit|exit
结束交互会话。
```

```
shutdown
停止 multipathd。
```

### 另参

`multipath(8)` `kpartx(8)` `hotplug(8)`

### 作者

`multipathd` 由 Christophe Varoqui, <christophe.varoqui@opensvc.com> 等人开发。

# 名称IF

## 名称

`nameif` - 根据 MAC 地址重命名网络接口

## 概要

```
nameif [-c configfile] [-s] nameif [-c configfile] [-s] {interface macaddress}
```

## 注意事项

此程序已过时。请检查 `ip link` 作为替代方案。此功能也可以通过 udev 方法更好地提供。

## 描述

`nameif` 根据 mac 地址重命名网络接口。在未提供参数时，将读取 `/etc/mactab`。该文件的每行包含一个接口名称和一个以太网 MAC 地址。允许以 `#` 开头的注释。否则，将处理命令行上指定的接口。`nameif` 查找具有给定 MAC 地址的接口并将其重命名为指定的名称。

当给出 `-s` 参数时，所有错误信息将发送到 syslog。

当给出 `-c` 参数并指定文件名时，将读取该文件而不是 `/etc/mactab`。

## 备注

`nameif` 应该在接口启动之前运行，否则将失败。

## 文件

`/etc/mactab`

## 另参

`ip(8)`, `udev(7)`

## 缺陷

目前仅对以太网起作用。

# ndptool

## 名称

`ndptool` – 邻居发现协议工具

## 概要

```
ndptool -h
ndptool [OPTIONS] COMMAND
```

## 描述

`ndptool` 是一个为邻居发现协议消息提供封装的工具。

## 选项

`-h`, `--help`

向控制台打印帮助文本并退出。

`-v`, `--verbose`

增加输出的详细程度。

`-t type`, `--msg-type type`

指定消息类型。支持以下类型：

- `rs` - 路由器请求 (Router Solicitation)。
- `ra` - 路由器公告 (Router Advertisement)。
- `ns` - 邻居请求 (Neighbor Solicitation)。
- `na` - 邻居公告 (Neighbor Advertisement)。

`-i ifname`, `--idname ifname`

指定接口名称。

## 命令

`monitor`

监控传入的 NDP 消息并将其打印。

`send`

发送指定类型的 NDP 消息。

## 作者

Jiri Pirko 是 libndp 的作者和当前维护者。

# 网络

## 名称

`net` - 管理 Samba 和远程 CIFS 服务器的工具。

## 概要

```
net {<ads|rap|rpc>} [-h|help] [-w|workgroup workgroup] [-W|—myworkgroup myworkgroup] [-U|user user] [-I|ipaddress ip-address] [-p|—port port] [-n myname] [-s confile] [-S|—server] [-l|long] [-v|verbose] [-f|—force] [-P|—machine-pass] [-d debuglevel] [-V|—request-timeout seconds] [-t|—timeout seconds] [-i|stdin] [--allocreport]
```

## 描述

该工具是 `samba(7)` 软件包组的一部分。

Samba `net` 工具的作用方式与 Windows 和 DOS 中的 net 工具完全相同。第一个参数应用于指定执行特定命令时使用的协议。ADS 用于 ActiveDirectory，RAP 用于旧版 (Win9x/NT3) 客户端，RPC 可用于 NT4 和 Windows 2000。如果省略此参数，net 将尝试自动确定它。并不是所有命令在所有协议上都可用。

## 选项

`-?|help`

打印命令行选项的摘要。

`-k|kerberos`

尝试使用 kerberos 进行身份验证。仅在 Active Directory 环境下有用。

`-w|workgroup target-workgroup`

设置工作组或域。你必须指定此选项或服务器的 IP 地址或名称。

`-W|myworkgroup workgroup`

设置客户端工作组或域。

`-U|user user`

要使用的用户名。

`-I|ipaddress ip-address`

要使用的目标服务器 IP 地址。你必须指定此选项或工作组或目标服务器。

`-p|port port`

连接到目标服务器的端口（通常为 139 或 445）。默认首先为 445，然后是 139。

`-n|netbiosname NetBIOS 名称`

此选项允许覆盖 Samba 自身使用的 NetBIOS 名称。这与在 smb.conf 中设置 netbios name 相同。然而，命令行设置将优先于 smb.conf 中的设置。

`-s|configfile=<configuration file`

指定的文件包含服务器所需的配置细节。文件中的信息包括服务器特定的有信息，例如使用哪个 printcap，以及所有将提供的服务的描述。默认配置名称在编译时确定。

`-S|server`

目标服务器的名称。你应该指定此选项或工作组或目标 IP 地址。

`-l|long`

在列出数据时，为每个项目提供更多信息。

`-v|verbose`

在列出数据时，为每个项目提供详细信息。

`-f|force`

强制执行 net 命令。

`-P|machine-pass`

使用本地服务器的机器账户对外部服务器进行查询。

`-request-timeout seconds`

让客户端请求在秒后超时，默认为 10 秒。

`-t|timeout seconds`

设置客户端操作的超时时间（秒）。

`-use-cache`

尝试使用 winbind 缓存的凭据。

`-i|stdin`

从标准输入获取 net 命令的输入。

`-allocreport`

在处理 net 命令时生成 talloc 报告。

`-T|test`

仅测试命令序列，空运行。

`-F|flags`

将整数标志传递给 net 子命令。

`-C|comment`

将注释字符串传递给 net 子命令。

`-n|myname MYNAME`

使用 MYNAME 作为 net 子命令的请求者名称。

`-c|container`

为 net 操作特定的 AD 容器。

`-M|maxusers MAXUSERS`

在 net rpc share 操作中填充 maxusers 字段。

`-r|reboot`

在命令成功执行后重启远程机器（例如在远程加入操作中）。

`-force-full-repl`

在调用 `net rpc keytab` 时，此选项强制重新创建生成的 keytab 文件。

`-single-obj-repl`

在调用 `net rpc keytab` 时，此选项允许仅同步对象到生成的 keytab 文件。

`-clean-old-entries`

在调用 `net rpc keytab` 时，此选项清理生成的 keytab 文件中的旧条目。

`-db`

为 `net idmap` 命令定义 dbfile。

`-lock`

激活 dbfile 的锁定。

`-a|auto`

在 `net idmap check` 中激活非交互模式。

`-repair`

在 `net idmap check` 中激活修复模式。

`-acls`

在 `net rpc migrate` 中包含 ACL。

`-atts`

在 `net rpc migrate` 中包含属性。

`-timestamps`

在 `net rpc migrate` 中包含时间戳。

`-X|exclude DIRECT`

在使用 `net rpc migrate` 时排除目录。

`-destinationSERVERNAME`

定义迁移的目标服务器名称（默认 localhost）。

`-L|local`

将映射类型设置为本地（用于 `net groupmap set`）。

`-D|domain`

将映射类型设置为域（用于 `net groupmap set`）。

`-N|ntname NTNAME`

设置映射的 ntame（用于 `net groupmap set`）。

设置映射的 rid（用于 `net groupmap set`）。

`reg-version REG_VERSION`

假设数据库版本 {1,2,3}（用于 `net registry check`）。

`output FILENAME`

输出数据库文件（用于 `net registry check`）。

`wipe`

从头创建一个新数据库（用于 `net registry check`）。

`precheck_DB_FILENAME`

定义用于数据库预检查的文件（用于 `net registry import`）。

`encrypt`

此命令行需要远程服务器支持 UNIX 扩展或选择了 SMB3 协议。请求加密连接。使用 SMB3 或通过 GSSAPI 使用 POSIX 扩展协商加密。使用给定的凭据进行加密协商（如果是 de域/用户名/密码三元组则使用 kerberos）。如果无法协商加密则连接失败。

`debuglevel=level`

level 为 0 到 10 的整数。如果没有指定此参数，默认值为 1。

此值越高，日志文件中记录的服务器活动详细信息就越多。在级别 0，仅记录关键错误和严重警告。级别 1 是日常运行的合理水平——它产生有关执行操作的少量信息。1以上的级别将产生大量的日志数据，应仅在调查问题时使用。3以上的级别专为开发者设计，并产生巨大的日志数据，其中大部分极其晦涩。注意，在此指定此参数将覆盖 smb.conf 文件中的 log level[] 参数。

`--version`

打印程序版本号。

更多信息请参阅 smb.conf。默认配置文件名是在编译时确定的。

`-l|log-basename=logdirectory`

日志/调试文件的基础目录名称。将附加后缀 `.progname`（例如 log.smbclient, log.smbd, 等...）。客户端永远不会删除日志文件。

`--option=<name>=<value>`

从命令行中将 smb.conf(5) 选项 "<name>" 设置为值 "<value>"。这将覆盖编译的默认值和从配置文件读取的选项。

## 命令 (COMMANDS)

# CHANGESECRETP



此命令允许从外部应用程序将 Samba 机器账户密码设置为已存储在 Active Directory（目录）中的机器账户密码。除非你完全清楚自己在做什么，否则**请勿使用**此命令。此命令要求必须使用强制标志 (`-f`)。不会有命令提示符。通过命令行输入或其他方式管道到 `stdin` 的任何信息都将作为字面密码存储。**请务必谨慎、仔细地使用此命令**，因为它会在没有任何警告的情况下覆盖合法的机器密码。**你已收到警告。**

# 时间 (TIME)

`NET TIME` 允许你查看远程服务器的时间，或将本地服务器的时间与远程服务器的时间同步。

## 时间 (TIME)

在不带任何选项的情况下，`NET TIME` 命令显示远程服务器的时间。必须使用 `-S` 选项指定远程服务器。

## 时间系统 (TIME SYSTEM)

以适用于 `/bin/date` 的格式显示远程服务器的时间。必须使用 `-S` 选项指定远程服务器。

## 设置时间 (TIME SET)

尝试使用 `/bin/date` 将本地服务器的日期和时间设置为远程服务器的时间。必须使用 `-S` 选项指定远程服务器。

## 时区 (TIME ZONE)

显示远程服务器上相对于 GMT 以小时为单位的时区。必须使用 `-S` 选项指定远程服务器。

```
[RPC|ADS] JOIN [TYPE] [-U username[%password]] [createupn=UPN] [createcomputer=OU] [machinepass=PASS] [string osVer=string] [options]
```

加入域。如果该账户在服务器上存在且 `[TYPE]` 为 `MEMBER`，则机器将尝试自动加入。（假设机器已经在服务器管理器中创建）。否则，将提示输入密码并可能会创建一个新账户。

`[TYPE]` 可以是 `PDC`、`BDC` 或 `MEMBER`，用于指定加入域的服务器类型。

`[UPN]` (仅限 ADS) 在加入期间设置 `principalname` 属性。默认格式为 `host/netbios@REALM`。

`[OU]` (仅限 ADS) 在特定的 OU 中预创建计算机账户。OU 字符串从上到下读取，不包含 DN，并以 `'/'` 分隔。请注意，它被 shell 和 ldap 均用于转义，因此可能需要双倍或四倍才能通过，且它不作为分隔符。

`[PASS]` (仅限 ADS) 为加入时创建的计算机账户设置特定密码。

`[osName=string osVer=String]` (仅限 ADS) 在加入期间设置 `operatingSystem` 和 `operatingSystemVersion` 属性。必须同时指定这两个参数才能生效。

# [RPC] OLDJOIN [options]

加入域。使用 `OLDJOIN` 选项以旧的域加入风格加入域——你必须先在服务器管理器中创建一个信任账户。

# [RPC|ADS] USER

## [RPC|ADS] USER

列出所有用户

## [RPC|ADS] USER DELETE target

删除指定用户

## [RPC|ADS] USER INFO target

列出指定用户的域组。

## [RPC|ADS] USER RENAME oldname newname

重命名指定用户。

## [RPC|ADS] USER ADD name [password] [-F user flags] [-C comment]

添加指定用户。

# [RPC|ADS] GROUP

## [RPC|ADS] GROUP [misc options] [targets]

列出用户组。

## [RPC|ADS] GROUP DELETE name [misc. options]

删除指定组。

## [RPC|ADS] GROUP ADD name [-C comment]

创建指定组。

# [RAP|RPC] SHARE

## [RAP|RPC] SHARE [misc. options] [targets]

枚举目标服务器上所有导出的资源（网络共享）。

## [RAP|RPC] SHARE ADD name=serverpath [-C comment] [-M maxusers] [targets]

从服务器添加共享（使其可用）。

## [RPC|ADS] SHARE DELETE

删除指定共享。

# [RPC|ADS] SHARE

## [RAP|RPC] SHARE ADD name=serverpath [-C comment] [-M maxusers] [targets]

从服务器添加共享（使其可用）。

## [RPC|ADS] SHARE DELETE

删除指定共享。

# [RPC|ADS] SHARE

## [RAP|RPC] SHARE ADD name=serverpath [-C comment] [-M maxusers] [targets]

从服务器添加共享（使其可用）。

## [RPC|ADS] SHARE DELETE

删除指定共享。

# [RPC|ADS] SHARE

## [RAP|RPC] SHARE ADD name=serverpath [-C comment] [-M maxusers] [targets]

从服务器添加共享（使其可用）。

## [RPC|ADS] SHARE DELETE

删除指定共享。

列出现有的组映射条目。

`net groupmap list [verbose][ntgroup=string][sid=SID]`

# MAXRID

打印本地服务器上当前使用的最高 RID（由活动‘passdb backend’提供）。

# RPC INFO

打印有关远程服务器域的信息，例如域名、域 SID 以及用户和组的数量。

# [RPC|ADS] TEST.JOIN

检查加入域的参与是否仍然有效。

# [RPC|ADS] CHANGETRUSTPW

强制更改域信任密码。

# RPC TRUSTDOM

## RPC TRUSTDOM ADD DOMAIN

为 `DOMAIN` 添加一个域间信任账户。这实际上是一个名为 `DOMAIN$s` 的 Samba 账户，该账户的标志为 `I`（域间信任账户）。这对于入站信任的工作是必需的。它使 Samba 成为外部（信任方）域的受信任域。Samba 域的用户将在外部域中可用。如果对本地主机使用此命令，其效果与 `smpasswd -a i DOMAIN` 相同。请注意，这两个命令都要求适当的 UNIX 账户。

## RPC TRUSTDOM DEL DOMAIN

移除 `DOMAIN` 的域间信任账户。如果对本地主机使用，其效果与 `smpasswd -x DOMAIN$` 相同。

## RPC TRUSTDOM ESTABLISH DOMAIN

与受信任域建立信任关系。域间账户必须在远程 PDC 上已创建。这对于出站信任的工作是必需的。它使 Samba 成为外部（受信任方）域的信任域。外部域的用户将在我们的域中可用。你需要 `winbind` 和工作正常的 `idmap` 配置来让它们出现在你的系统里。

## RPC TRUSTDOM REVOKE DOMAIN

放弃与受信任域的关系

## RPC TRUSTDOM LIST

列出所有域间信任关系。

# RPC TRUST

## RPC TRUSTCreateTrustedDomainEx2

通过调用 `LsaCreateTrustedDomainEx2` 创建信任对象。可以在单个服务器上完成，也可以同时在两台服务器上完成，并可以使用随机信任密码。

选项：

- `- otherserver`
  - 第二个域的域控制器
- `otheruser`
  - 第二个域的管理员用户
- `otherdomainsid`
  - 第二个域的 SID
- `other_netbios_domain`
  - 第二个域的 NetBIOS（短）名称
- `otherdomain`
  - 第二个域的 DNS（全）名称
- `trustpw`
  - 信任密码

示例：

在 `sr1.dom1.dom` 上为域 `dom2` 创建信任对象

```
net rpc trust create \ otherdomains=S-x-x-xx-xxxxxxxx-xxxxxxxx-
xxxxxxxxx \ other_netbios_dom2 \ otherdomain=dom2.dom \
trustpw=1234567 \ -S sr1.dom1.dom
```

在 `dom1` 和 `dom2` 之间建立信任关系

```
net rpc trust create \ otherserver=srv2.dom2.test \ otheruser=dom2adm \
-S sr1.dom1.dom
```

# RPC TRUST DELETE

通过调用 `LsaDeleteTrustedDomain` 删除信任对象。可以在单个服务器上完成，也可以同时在两台服务器上完成。

选项：

- `otherserver`
  - 第二个域的域控制器
- `otheruser`
  - 第二个域的管理员用户
- `otherdomainsid`
  - 第二个域的 SID

示例：

```
在 srv1.dom1.dom 上为域 dom2 删除信任对象
net rpc trust delete \ othersdomainsid=S-x-x-xxxxxxxxxxxx-xxxxxxxxxxxx \-S srv1.dom1.dom
```

```
在 dom1 和 dom2 之间删除信任关系
net rpc trust delete \ otherserver=srv2.dom2.test \ otheruser=dom2adm \-S sr1.dom1.dom
```

# RPC RIGHTS

此子命令用于查看和管理 Samba 的权利分配（也称为权限）。目前有三个可用选项：`list`、`grant` 和 `revoke`。关于 Samba 权限模型及其使用的更多详细信息可以在 Samba-HOWTO-Collection 中找到。

# RPC ABORTSHUTDOWN

终止远程服务器的关机。

# RPC SHUTDOWN [-t timeout] [-f] [-C message]

关闭远程服务器。

- `-r`
  关机后重启。
- `-f`
  强制关闭所有应用程序。
- `-t timeout`
  系统关机前的超时时间。系统的交互用户可以使用这段时间取消关机。
- `-C message`
  在屏幕上显示指定的的消息以宣布关机。

# RPC SAMDUMP

打印远程服务器的 `sam` 数据库。你需要从已加入 BDC 的 Samba 机器对 PDC 运行此命令。

# RPC VAMPIRE

将用户、别名和组从远程服务器导出到本地服务器。你需要从已加入 BDC 的 Samba 机器对 PDC 运行此命令。此 `vampire` 命令不能用于 Active Directory，只能对 NT4 域控制器使用。

# RPC VAMPIRE KEYTAB

将远程 SAM 数据库转到本地 Kerberos `keytab` 文件。

# RPC VAMPIRE LDIF

将远程 SAM 数据库转储本地 LDIF 文件或标准输出。

# RPC GETSID

获取域 SID 并将其存储在本地 `secrets.tdb`（或 `secrets.ntdb`）中。

# ADS LEAVE

让远程主机离开所在的域。

# ADS STATUS

打印本地机器在 ADS 中的机器账户状态。打印大量的调试信息。面向开发者，普通用户应使用 `NET ADS TESTJOIN`。

# ADS PRINTER

## ADS PRINTER INFO [PRINTER] [SERVER]

在 `SERVER` 上查找 `PRINTER`。打印机名称默认为 `"*"`, 服务器名称默认位本地主机。

## ADS PRINTER PUBL PRINTER

使用 ADS 发布指定的打印机。

## ADS PRINTER REMOVE PRINTER

从 ADS 目录删除指定的打印机。

# ADS SEARCH EXPRESSION ATTRIBUTES...

在 ADS 服务器上执行原始 LDAP 搜索并转储结果。表达式是标准的 LDAP 搜索表达式，属性是显示结果的 LDAP 字段列表。

示例：`net ads search 'objectCategory=group' sAMAAccountName`

# ADS DN DN (attributes)

在 ADS 服务器上执行原始 LDAP 搜索并转储结果。DN 是标准的 LDAP DN，属性是显示结果的 LDAP 字段列表。

示例：`net ads dn 'CN=administrator,CN=Users,DC=my,DC=domain' SAMAccountName`

# ADS WORKGROUP

打印指定 kerberos 区域的工作组名称。

# ADS ENCTYPE

列出、修改或删除 AD 中账户的 `msDS-SupportedTypes` 属性值。此属性允许控制使用哪些 Kerberos 加密类型来生成票据。该值由以下值的位掩码组成：

- `0x00000001` DES-CBC
- `0x00000002` DES-CBC-MD5
- `0x00000004` RC4-HMAC
- `0x00000008` AES128-CTS-HMAC-SHA196
- `0x00000010` AES256-CTS-HMAC-SHA196

## ADS ENCTYPE LIST <ACCOUNTNAME>

列出账户的 `msDS-SupportedTypes` 属性值。

示例：`net ads list Computername`

## ADS ENCTYPE SET <ACCOUNTNAME>

将 LDAP 对象的 `msDS-SupportedTypes` 属性设置为给定值。如果省略该值，则将其设置为 31，启用所有当前的加密类型。

示例：`net ads set Computername 24`

## ADS ENCTYPE DELETE <ACCOUNTNAME>

删除 LDAP 对象的 `msDS-SupportedTypes` 属性。

示例：`net ads set Computername24`

# SAM CREATEBUILDGROUP <NAME>

（重）创建 BUILTIN 组。只有一组特定的 BUILTIN 组可以使用此命令创建。这些组的列表如下：`Administrators`, `Users`, `Guests`, `Power Users`, `Account Operators`, `Server Operators`, `Replicator`, `RAS Servers`, `Pre-Windows 2000 compatible Access`。此命令需要运行 `winbind` 且 `idmap` 配置正常。组 `gid` 将从 `winbind` 范围分配。

# SAM CREATLOCALGROUP <NAME>

创建一个本地组（也称为别名）。此命令需要运行 `winbind` 且 `idmap` 配置正常。组 `gid` 将从 `winbind` 范围分配。

# SAM DELETELOCGROUP <NAME>

删除现有的本地组（也称为别名）。

# SAM MAPUNIXGROUP <NAME>

映射现有的 Unix 组并使其成为域组，域组将具有相同的名称。

# SAM UNMAPUNIXGROUP <NAME>

移除现有的组映射条目。

# SAM ADDMEM <GROUP> <MEMBER>

向本地组添加成员。组只能通过名称指定，成员可以按名称或 SID 指定。

# SAM DELMEM <GROUP> <MEMBER>

从本地组中删除成员。组和成员都必须通过名称指定。

# SAM LISTMEM <GROUP>

列出本地组的成员。组必须通过名称指定。

# SAM LIST <users|localgroups|builtin|workstations> [verbose]

按名称列出指定的账户集。如果指定了 `verbose`（详细），还将为每个账户提供 `rid` 和描述。

# SAM RIGHTS LIST

列出所有可用的权限。

# SAM RIGHTS GRANT <NAME> <PRIVILEGE>

向用户授予一个或多个权限。

# SAM RIGHTS REVOKE <NAME> <PRIVILEGE>

从用户处撤销一个或多个权限。

# SAM SHOW <NAME>

显示对应账户的完整 `DOMAIN\NAME`、`SID` 和类型。

# SAM SET HOMEDIR <NAME> <DIRECTORY>

为用户账户设置主目录。

# SAM SET PROFILEPATH <NAME> <PATH>

为用户账户设置配置文件路径。

# SAM SET COMMENT <NAME> <COMMENT>

为用户或组账户设置注释。

# SAM SET FULLNAME <NAME> <FULL NAME>

为用户账户设置全名。

# SAM SET LOGONSCRIPT <NAME> <SCRIPT>

为用户账户设置登录脚本。

# SAM SET HOMEDRIVE <NAME> <DRIVE>

为用户账户设置主驱动器。

# SAM SET WORKSTATIONS <NAME> <WORKSTATIONS>

设置允许用户账户登录的工作站。

# SAM SET DISABLE <NAME>

为用户账户设置“禁用（disabled）”标记。

# SAM SET PWNOTREQ <NAME>

为用户账户设置“不需要密码（password not required）”标记。

# SAM SET AUTOLOCK <NAME>

为用户账户设置“自动锁定（autolock）”标记。

# SAM SET PWNNOEXP <NAME>

为用户账户设置“密码永久（password do not expire）”标记。

# SAM SET PWDMUSTCHANGENOW <NAME> [yes|no]

为用户账户设置或取消“必须密码（password must change）”标记。

# SAM POLICY LIST

列出可用账户策略。

# SAM POLICY SHOW <account policy>

显示账户策略的值。



# `SAM POLICY SET <account policy> <value>`

设置账户策略的值。有效值可以是：`“forever”`、`“never”`、`“off”`或数字。

# `SAM PROVISION`

仅在设置 `ldaps:editpolicy` 且 `winbindd` 运行时可用。它在 `idap` 树上正确地填充基本账户（`Administrator`）和组（`Domain Users`, `Domain Admins`, `Domain Guests`）。

# `IDMAP DUMP <local tdb file name>`

转储指定的本地 `tdb` 文件包含的映射。此命令用于仅转储由 `idmap_tdb` 后端产生的映射。

# `IDMAP RESTORE [input file]`

从指定的文件或标准输入恢复映射。

# `IDMAP SET SECRET <DOMAIN> <secret>`

为指定的域存储密钥，主要用于使用 `idmap_ldap` 作为后端的域。在这种情况下，该密钥被用作绑定到 `ldap` 服务器的用户 `DN` 的密码。

# `IDMAP SET RANGE <RANGE> <SID> [index] [--db=<DB>]`

在 `autorid` 数据库中为指定的域（及索引）存储域范围映射。

# `IDMAP SET CONFIG <config> [--db=<DB>]`

从 `autorid` 数据库更新 `CONFIG` 条目。

# `IDMAP GET RANGE <SID> [index] [--db=<DB>]`

从 `autorid` 数据库中获取指定域和索引的范围。

# `IDMAP GET RANGES <SID> [--db=<DB>]`

获取所有域或由给定 `SID` 标识的域的范围。

# `IDMAP GET CONFIG [--db=<DB>]`

从 `autorid` 数据库获取 `CONFIG` 条目。

# `IDMAP DELETE MAPPING [-f] [--db=<DB>] <ID>`

从 `IDMAP` 数据库中删除映射 `<ID> -> gid <-> uid`。映射由 `<ID>` 提供，其可能是一个 `sid: S-x...` 一个 `gid: "GID number"` 或一个 `uid: "UID number"`。使用 `-f` 删除无效的部分映射 `<ID> -> xx`

使用 `"smcontrol idmap ..."` 通知正在运行的 `smbd` 实例。详情请参考 `smbcontrol(1)` 手页。

# `IDMAP DELETE RANGE [-f] [--db=<TDB>] <RANGE>|<SID> <INDEX>]`

从 `autorid` 数据库中删除由 `'RANGE'` 或 `"domain SID 和 INDEX"` 标识的域范围映射。使用 `-f` 删除无效映射。

# `IDMAP DELETE RANGES [-f] [--db=<TDB>] <SID>`

删除由 `SID` 标识的域的所有域范围映射。使用 `-f` 删除无效映射。

# `IDMAP CHECK [-v] [-r] [-a] [-T] [-f] [-l] [--db=<DB>]`

检查并修复 `IDMAP` 数据库。如果没有提供任何选项，则对数据库进行只读检查。此外，可以选择以下选项之一的交互或自动修复模式：

- `repair`

交互式修复模式，会提出很多问题。

- `auto`

非交互式修复模式，使用默认答案。

- `verbose`

产生更多输出。

- `force`

尝试应用更改，即使它们无法干净地应用。

- `test`

空运行，显示将进行哪些更改但不触碰任何内容。

- `lock`

在检查时锁定数据库。

- `<db < >`

检查指定的数据库。

它将报告发现的以下错误：

缺失反向映射（Missing reverse mapping）：

存在映射 `A->B` 的记录，但没有 `B->A`。修复映射的默认操作是通过添加反向映射来“修复”此问题。

无效映射（Invalid mapping）：

存在映射 `A->B` 的记录，其中 `B->C`。默认操作是“修复”。

缺失高水位线（Missing HWM）：

未设置高水位线。默认操作是“修复”。

无效记录（Invalid record）：

解析失败。默认操作是“修复”。

从 `3.0` 版本开始，Samba 现在支持非根用户使用 `smb.conf` 参数：`“usershare owner only”`、`“usershare allow list”`和`“usershare deny list”`创建定义的共享。设置如下：

# `USERSHARE add <path> [comment] [acl] [guest_ok=[y|n]]`

添加或替换名为 `"sharename"` 的新定义共享。`"path"` 指定了系统上要导出的绝对路径。可以对该路径进行限制，请使用全局 `smb.conf` 参数：`“usershare owner only”`，并设置为。

可选的 `"comment"` 参数是客户端浏览时在共享上显示的注释。

可选的 `"acl"` 字段指定哪些用户对整个共享具有读写权限。请注意，除非设置了 `smb.conf` 参数 `"usershare allow guests"`，否则不允许访客连接。用户共享 `acl` 的定义为：`“user:permission”`，其中 `user` 是系统上的有效用户名，`permission` 可以 `"F"`、`R"` 或 `"D"`。

- `F`: 完全权限，即读和写权限。

- `D`: 拒绝某个用户，即防止该用户访问此共享。

- `R`: 只读，即对此共享仅有读取访问权限（无法创建新文件或目录或写入文件）。

在未给出 `"acl"` 的情况下，默认值为 `"Everyone:R"`，这意味着任何经过身份验证的用户都有只读访问权限。

可选的 `"guest_ok"` 与 `smb.conf` 中的同名参数具有相同效果，即允许访问此用户共享。只有在 `smb.conf` 中将全局参数 `"usershare allow guests"` 设置为 `true` 时该参数才有效。命令如下：

- `net ushare add <path> [comment] [acl] [guest_ok=[y|n]]`

添加或更改定义的共享，使用与要修改相同的 `sharename`。

- `net ushare delete <sharename>`

删除定义的共享。

- `net ushare info [-l|long] <wildcard sharename>`

打印关于用户共享的信息。

- `net ushare list [-l|long] <wildcard sharename>`

列出定义的共享。

没有单独修改现有定义共享的命令，只需使用 `"net ushare add [sharename]"` 命令，使用与要修改相同的 `sharename` 并指定你想要的新选项即可。Samba `smbd` 在连接时感知用户定义共享的修改，因此可以立即生效，无需在添加、删除或更改定义共享时重启 `smbd`。

# `USERSHARE DELETE sharename`

按名称删除自定义共享。Samba `smbd` 进程会立即检测到此更改，尽管它不会断开当前连接到已删除共享的用户。

# `USERSHARE INFO [-l|--long [wildcard sharename]`

获取当前用户拥的所有匹配给定模式的自定义共享信息，或所有用户的信息。

`net ushare info` 命令本身会列出当前用户创建的共享信息，或限制为匹配给定通配符模式的共享名称（`*` 匹配一个或多个字符，`?` 仅匹配一个字符）。如果给出了 `-l` 或 `--long` 选项，它将打印其他用户创建的共享信息。

关于共享提供的信息所示：`[foobar] path=/home/jeremy comment=testme_acl=Everyone:F guest ok=n`。这是自定义共享的当前设置列表，可以通过 `net ushare add` 命令进行修改。

# `USERSHARE LIST [-l|--long wildcard sharename`

列出当前用户拥有的所有匹配给定模式的自定义共享，或所有用户的信息。

`net ushare list` 命令本身会列出当前用户创建的共享名称，或限制为匹配通配符模式的共享名称（`*` 匹配一个或多个字符，`?` 仅匹配一个字符）。如果给出了 `-l` 或 `--long` 选项，它将列出其他用户创建的共享名称。

# `[RPC] CONF`

从 `3.2.0` 版本开始，Samba 服务器可以通过存储在注册表的数据进行配置。这些配置数据可以使用新的 `net conf` 命令进行编辑。此外还可以通过启用 `RPC` 模式并指定远程服务器的地址来配置远程 Samba 服务器。

此类配置数据的部署可以在 `smb.conf` 文件中两个级别激活：注册表共享定义通过在 `[global]` 部分将注册表共享设置为 `"yes"` 来激活；全局选项则通过在 `[global]` 部分中设置 `include = registry[]` 来激活混合配置，或者通过在 `[global]` 部分中设置 `config backend = registry[]` 来激活仅限注册表的配置。详细信息请参 `smb.conf(5)` 手册。

命令如下：

- `[rpc] conf list` - 以类似 `smb.conf` 的格式转储完整配置。

- `net [rpc] conf import` - 从 `smb.conf` 格式的文件导入配置。

- `net [rpc] conf listshares` - 列出注册表共享。

- `net [rpc] conf drop` - 删除注册表中完整配置。

- `net [rpc] conf showshare` - 显示注册表共享的定义。

- `net [rpc] conf addshare` - 创建一个新的注册表共享。

- `net [rpc] conf delete` - 删除注册表共享。

- `net [rpc] conf setparam` - 存储一个参数。

- `net [rpc] conf getparam` - 获取参数值。

- `net [rpc] conf delparam` - 删除一个参数。

- `net [rpc] conf getincludes` - 显示共享定义的包含项。

- `net [rpc] conf setincludes` - 设置共享的包含项。

- `net [rpc] conf delincludes` - 删除共享定义中的包含项。

# `[RPC] CONF LIST`

将存储在注册表中的配置数据以类似 `smb.conf` 的格式打印到标准输出。

# `[RPC] CONF IMPORT—[test]-[T] filename [section]`

此命令从 `smb.conf` 格式的文件导入。如果输入文件中遇到的节在注册表中存在，则其内容将被替换。注册表中在输入文件中没有对应项的节将不受影响。如果你想删除这些项，则必须使用 `net conf drop` 或 `net conf delshare` 命令。可以选择指定一个节以将导入命令的影响限制在该特定节内。通过在命令行上指定参数 `-T` 可启用测试模式。在测试模式下，注册表不会发生任何更改，而是将结果配置打印到标准输出。

# `[RPC] CONF LISTSHARES`

列出注册表中定义的共享名称。

# `[RPC] CONF DROP`

删除注册表中的完整配置数据。

# `[RPC] CONF SHOWSHARE sharename`

显示指定的共享或节的定义。指定 `“global”` 作为共享名称从注册表中检索全局配置选项是有效的。

# `[RPC] CONF ADDSHARE sharename path [writeable={y|N} [guest_ok={y|N} [comment]]`

创建一个新的注册表共享。指定的 `sharename` 和 `path` 是有效的。可以指定 `writeable={y|N}`、`guest_ok={y|N}` 和 `comment`。通过 `net conf setparm` 命令可以获得相同的结果。

# `[RPC] CONF DELSHARE sharename`

删除注册表中的共享定义。

# `[RPC] CONF SETPARM section value`

在注册表中存储参数。节可以是 `global` 或特定的 `sharename`。如果节不存在，则创建它。

# `[RPC] CONF GETPARM section`

显示存储在注册表中的参数。

# `[RPC] CONF DELPARM section`

删除注册表中的参数。

# `[RPC] CONF GETINCLUDES section`

获取节的包含项列表。由于注册表的性质和包含指令的性质，包含项需要特殊处理：参数按参数名称存储在注册表中，因此每个参数只有一个实例。

# `[RPC] CONF SETINCLUDES section`

设置节的包含项列表。

# `[RPC] CONF DELINCLUDES section`

从共享定义中删除包含。

# `REGISTRY`

操作 Samba 的注册表。注册表命令有：

- `enumerate` - 枚举键值。

- `enumerate_recursive` - 枚举值和子键。

- `createkey` - 如果不存在则创建新键。

- `deletekey` - 在没有子键的情况下删除键。

- `deletekey_recursive` - 删除指定的键及其所有子键。

- `getvalue` - 输出键值的类型和实际值。

- `getvaluer` - 输出值的实际值。

- `setvalue` - 设置现有键的值名。类型可以是 `sz`、`multi_sz` 或 `dword`。对于 `multi_sz`，值可以多次给定。

- `increment` - 在锁定期间将键的 `DWORD` 值增加 `inc`。`inc` 默认为 `1`。

- `deletevalue` - 删除键的值名。

- `getsdl` - 获取键的安全描述符。

- `getsdl_sdl` - 以安全描述定义语言（`SDDL`）字符串格式获取键的安全描述符。

- `setsdl_sdl` - 从安全描述定义语言（`SDDL`）字符串设置键的安全描述符。

# `REGISTRY IMPORT file [—precheck <precheck-file>] [opt]`

导入注册表项（`.reg`）文件。可用选项包括：

- `precheck check-file`: 这在应用导入文件之前，检查预检查文件中指定的某些键或值是否存在的机制。只有在预检查成功时，才会应用导入文件。

预检查遵循标准的注册表文件语法，具有以下语义：

- `<value name=><value>` 检查值是否存在且具有给定的值。

- `<value name>=-` 检查值不存在。

- `[key]` 检查键是否存在。

- `[-key]` 检查键不存在。

# `REGISTRY EXPORT keyfile[opt]`

将键导出到注册表项（`.reg`）文件。

# `REGISTRY CONVERT in out [inopt] optout`

转换输入的注册表项（`.reg`）文件。

# `REGISTRY CHECK [-ravTl] [-o <ODB>] [--wipe] [<ODB>]`

检查并修复注册表数据库。如果没有提供任何选项，则将对数据库进行只读检查。可以通过以下选项选择交互式或自动修复模式：

- `-r|repair`

交互式修复模式，会提出许多问题。

- `-a|auto`

非交互式修复模式，使用默认答案。

- `-v|verbose`

产生更多输出。

- `-T|test`

空运行，显示将进行哪些更改，但不触动任何内容。

- `-l|lock`

在执行检查时锁定数据库。

- `-reg-version={1,2,3}`

指定注册表数据库的格式。如果没有指定，则默认为二进制文件的值；或者如果命令行中显式指定了 `registry.tdb`，则默认为 `INFO/version` 记录中的值。

- `--db|<ODB>`

检查指定的数据库。

- `-o|output <ODB>`

创建一个新的注册表数据库 `<ODB>` 而不是修改输入。如果 `<ODB>` 已存在，则可能会覆盖它。

- `--wipe`

替换注册表数据库，而不是修改输入或覆盖现有的输出数据库。

# `EVENTLOG`

从 `3.4.0` 版本的 `net` 开始，可以读取、转储、导入和导出原生 `win32` 事件日志文件（通常为 `*.evt`）。`evt` 文件由原生 Windows 事件查看器工具使用。

只有当 `smb.conf` 中使用了 `eventlog list` 时，`evt` 文件的导入和导出才能成功。详情请参阅 `smb.conf(5)` 手页。

`eventlog` 命令有：

- `- eventlog dump` - 将事件 `*.evt` 文件打印到屏幕。

- `eventlog import` - 将事件 `*.evt` 导入 `samba` 内部事件日志的 `tdb` 表示。

- `eventlog export` - 将 `samba` 内部事件日志的 `tdb` 表示导出为事件 `*.evt` 文件。

# `EVENTLOG DUMP filename`

将事件日志 `*.evt` 文件打印到标准输出。

# `EVENTLOG IMPORT filename`

将由 `filename` 定义的事件 `*.evt` 文件导入由 `eventlog` 定义的 `samba` 内部事件日志 `tdb` 表示。`eventlog` 需要 `smb.conf` 中定义的 `eventlog list` 部分。详情请参阅 `smb.conf(5)` 手页。

# `EVENTLOG EXPORT filename eventlog`

将由 `eventlog` 定义的 `samba` 内部事件日志 `tdb` 表示导出为由 `filename` 定义的事件 `*.evt` 文件。`eventlog` 需要 `smb.conf` 中定义的 `eventlog list` 部分。详情请参阅 `smb.conf(5)` 手页。

# `DOM`

从 `3.2.0` 版本开始，Samba 支持远程加入和退出 `API`，涵盖客户端和服务端。Windows 从 Windows `2000` 开始就支持远程加入功能。

为了让 Samba 远程加入或退出域，必须使用属于 `Domain Admins` 组成员、`Local Administrators` 组成员或被授予 `SeMachineAccountPrivilege` 权限的用户账户。



远程加入的客户端支持实现在 `net` 命令中，这些命令有：

- `dom join` - 将远程计算机加入域。
- `dom unjoin` - 将远程计算机退出域。
- `dom renamecomputer` - 重命名已加入域的远程计算机。

### `DOM JOIN domain=DOMAIN ou=OU=ACCOUNT password=PASSWORD reboot`

将计算机加入域。此命令支持以下额外参数：

- `DOMAIN` 可以是 NetBIOS 域名（也称为短域名）或 Active Directory 域的 DNS 域名。在 Windows 中，还可以控制使用哪个域控制器。这可以通过使用 `\` 分隔符附加 DC 名称来实现。例如：`MYDOM\MYDC`。`DOMAIN` 参数不能为 NULL。
- `OU` 可以是一个 RFC 1779 LDAP DN，例如 `ou=mymachine,cn=Users,dc=example,dc=com`，以便在非默认 LDAP 容器中创建机器帐户。此可选参数仅在加入活动域（Active Domains）时支持。
- `ACCOUNT` 定义了用于将机器加入域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功加入域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要加入的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom join -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

此示例将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并将该计算机加入名为 `MYDOM` 的域，管理员账户和密码为 `secret`。加入成功后，计算机将重启。

### `DOM UNJOIN account=ACCOUNT password=PASSWORD reboot`

将计算机退出域。此命令支持以下额外参数：

- `ACCOUNT` 定义了用于将机器退出域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功退出域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要退出的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom unjoin -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

这将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并使用 `MYDOM` 管理员账户和密码 `secret` 将计算机退出域。退出成功后，计算机将重启。

### `DOM RENAMECOMPUTER newname=NEWNAME ACCOUNT=PASSWORD reboot`

重命名已加入域的计算机。此命令支持以下额外参数：

- `NEWNAME` 定义机器的新名称。
- `ACCOUNT` 定义了用于将机器加入域的域账户。该域账户需要足够的权限来加入机器。
- `PASSWORD` 定义了由 `ACCOUNT` 指定域账户的密码。
- `REBOOT` 是可选参数，可以设置为在成功加入域后重启远程机器。

注意，你还需要使用标准参数来连接并验证你想要加入域的远程机器。这些额外参数包括：`-S computer` 和 `-U user`。

示例：`net dom join -S xp -U XP,administrator*secret domain=MYDOM account=MYDOM\administrator password=topsecret reboot`。

这将使用密码 `secret` 以本地管理员身份连接到名为 `XP` 的计算机，并将该计算机加入名为 `MYDOM` 的域，管理员账户和密码为 `secret`。加入成功后，计算机将重启。

## `G_LOCK`

管理全局锁。

### `G_LOCK timeout command`

在全局锁下执行 shell 命令。这可能用于定义 shell 命令的执行顺序。锁定信息存储在 `g_lock.tdb` 文件。在运行 CTDB 的设置中，锁定信息将在所有节点可用。

- `LOCKNAME` 定义全局锁的名称。
- `TIMEOUT` 定义超时时间。
- `COMMAND` 定义要执行的 shell 命令。

### `G_LOCK LOCKS`

列出所有现有 `lockname` 的列表。

### `G_LOCK DUMP lockname`

转储特定全局锁的锁定表。

## `HELP [COMMAND]`

提供指定命令的使用信息。

## `VERSION`

本手页对于 Samba 套件版本 3 是完整的。

### AUTHOR

原始 Samba 及相关工具由 Andrew Tridjell 创建。Samba 现在由 Samba 团队作为一个开源项目开发，类似于 Linux 内核的开发方式。

`net` 手由 Jelmer Vernooij 编写。
