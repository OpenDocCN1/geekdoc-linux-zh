
```
31327 zach 18 0 2092 596 492 R 57 0.0 00:00:38 cp
31311 root 15 0 0 0 16 0.0 00:00:38 pdfflush
6878 zach 27 12 331m 37m R 2 9.4 00:42:98 firefox-bin
31303 root 15 0 0 0 2 0.0 00:00:42 pdfflush
1 root 15 0 2912 1808 488 S 0 0.1 00:01:55 init
```

## 维护系统

本节讨论了对系统管理员重要的几个工具和概念。它涵盖了使用 `parted` 处理硬盘分区的方法、如何避免产生问题，以及如何解决系统问题。

### parted：硬盘分区的报告与分区

`parted`（分区编辑器）工具可以从命令行报告并操作硬盘分区。`paled` 工具（第 77 页）允许你使用图形用户界面（GUI）执行相同的任务。接下来是关于 `/dev/sda/` 上分区的 `parted` 信息：

## parted /dev/sda print
型号: ATA Hitachi HDS12345 (scsi)
磁盘 `/dev/sda`: 165GB
扇区大小逻辑/物理): 512B/512B
分区表: mdos

| 编号 | 起 | 止 | 大小 | 类型 | 文件系统 | 标记 |
|---|---|---|---|---|---|---|
| 1 | 32kb | 1045MB | 1045MB | 主分区 | ext4 | |
| 2 | 1045MB | 12GB | 12GB | 主分区 | ext4 | |
| 3 | 12GB | 22GB | 10GB | 主分区 | ext4 | |
| 4 | 22GB | 165GB | 143GB | 扩展分区 | linux-swap | |
| 5 | 165GB | 236GB | 71GB | 逻辑分区 | ext4 | |
| 6 | 236GB | 418GB | 182GB | 逻辑分区 | ext4 | |
| 7 | 418GB | 165GB | 41GB | 逻辑分区 | ext4 | |

图 16-3 显示了示例中的分区。`print` 命令显示了以下列：

- 设备号（第 517 页）持有分区的设备编号。在示例中，对应 `/dev/sda5`。
- 起：分区在硬盘上的起始位置。`parted` 指定从硬盘开始的距离。分区 3 从硬盘开始 12GB 。
- 止：分区在硬盘上的结束位置。虽然分区 2 在 12GB 结束，但 `parted` 确保分区不会重叠。
- 大小：分区的大小，单位为字节（KB）、兆字节（MB）或千字节（GB）。
- 类型：分区类型：主分区、扩展分区或逻辑分区。有关分区的信息见。
- 文件系统：类型类型：ext2、ext3、ext4、fat32、linux-swap 等。文件系统类型列表见下表。
- 标记：分区开启的标记，包括 boot、raid 和 lvm。在示例中，分区 1 是启动的。

在前面的示例中，分区 4 定义了一个包含 143GB 硬盘空间的扩展分区。你无法在影响所有内部逻辑分区的情况下对扩展分区进行更改。

```
(parted) set 1 boot on
(在分区 1 上开启启动标记)
(parted) print
/dev/sdb 的磁盘几何结构: 0KB - 250GB
磁盘标签类型: mdos
（验证分区是否正确）

| 编号 | 开始 | 结束 | 类型 | 文件系统 | 标记 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 1kB | 300MB | 300MB | 主分区 | ext2 boot |

(parted) quit
信息：必要时不要忘记使用 `/etc/fstab`。
```

在 `parted` 中指定大小时，您可以使用后缀 `k`（千字节）、`m`（兆字节）或 `g`（吉字节）作为后缀。创建分区后，输入 `print` 命令以查看分区的结束位置。在定义下一个连续分区之前执行此任务，以免浪费空间。设置好所有分区后，使用 `quit` 命令退出。

接下来，在每个要包含文件系统（非交换分区）的分区上创建一个文件系统（`mkfs`，第 472 页）。除非类型为 ext4，否则对所有分区进行操作。使用 `mswap`（第 13 页）在分区上设置交换区域。您可以使用 `e2label`（第 470 页）来标记分区。

### logrotate：管理日志文件

与其删除或截断日志文件，您可能希望保留这些文件，因为需要引用它们。`logrotate` 工具通过轮转（第 16 页）、压缩、邮件和删除每个文件来管理系统日志。`logrotate` 工具由 `/etc/logrotate.conf` 文件控制，该文件设置了默认值，并可以指定要轮转的文件。`logrotate.conf` 包含一个 `include` 语句，指向 `/etc/logrotate.d` 中的特定实用程序规范文件。`logrotate.conf` 文件如下：

```
$ cat /etc/logrotate.conf

# 查看 "logrotate" 详情

# 每周轮转

weekly
```

```
# 保留 4 周的日志

rotate 4
```

```
# 在轮转后创建（空）日志文件

create
```

```
# 使用日期作为轮转文件的后缀

dateext
```

```
# 如果您希望压缩日志文件，请取消注释

compress
```

```
# 将日志轮转信息放入您的目录

include /etc/logrotate.d
```

```
# wtmp 和 btmp 包——我们在这里轮转它们

/var/log/wtmp {

monthly

create 0664 root utmp

minsize 1M

rotate 1

}
```

```
/var/log/btmp {

missingok

monthly

create 0600 root utmp

rotate 1

}
```

特定的日志也可以在此配置。`logrotate.conf` 文件设置了通用参数。每当 `logrotate` 读取这些参数的另一个值时，它会重置默认值。您可以选择每天、每周或每月轮转文件。`rotate`关键字后面的数字指定了想要保留的日志文件数量。`create`关键字让 `logrotate` 创建一个与轮转日志具有相同名称和属性的新日志文件。`dateext`关键字让 `logrotate` 使用日期作为文件名扩展名。`compress`关键字（在默认文件中被注释）导致日志文件使用 `gzip` 压缩。`include`关键字指定了标准的 `/etc/logrotate.d` 目录，用于特定程序的 `logrotate` 规范文件。当您使用 `rpm`（第 50 页）或基于 `rpm` 的工具（如 `yum`，第 13 章）安装程序时，`rpm`会将`logrotate`规范文件放在目录下。

`logrotate.conf` 的最后实例处理 `/var/log/wtmp` 和 `/var/log/btmp` 日志（`wtmp` 存储登录记录，`btmp` 存储登录尝试记录）；您可以使用 `who` 查看这些文件。`missingok`关键字覆盖了该文件的隐含默认 `missingok`。此关键字允许 `logrotate` 在日志文件缺失时继续而不发出错误消息。`monthly`关键字覆盖了该文件的每周默认值。`create`关键字建立了新文件的权限、所有者和组。最后，`rotate` 确保保留一个轮转后的日志。

`/etc/logrotate.d/httpd` 文件是一个特定程序的 `logrotate` 规范文件示例：

```
$ cat /etc/logrotate.d/httpd

/var/log/httpd/log {

missingok

notifempty

sharedscripts

delaycompress

postrotate

/sbin/service httpd reload > /dev/null 2>&null || true

endscript

}
```

# 维护系统 623

此文件由 `httpd` 包安装脚本安装，并由于 `logrotate.conf` 中的 `include` 语句被包含在 `/etc/logrotate.d` 中，它对每个文件有效。带有多个选择的行中的每个选择都会限制匹配，随后的选择会收紧限制。`delaycompress`允许 `logrotate` 延迟压缩。`truncate`关键字允许 `logrotate` 在轮转后截断原始文件。`postrotate`允许 `logrotate` 在所有轮转完成后运行脚本。*:crit:none匹配所有内容。`compress`允许 `logrotate` 使用 `gzip` 压缩文件。`rotate`允许 `logrotate` 轮转日志文件。

`/etc/logrotate.d/httpd` 文件是一个特定程序的 `logrotate` 规范文件示例：

```
$ cat /etc/logrotate.d/httpd

/var/log/httpd/log {

missingok

notifempty

sharedscripts

delaycompress

postrotate
```
