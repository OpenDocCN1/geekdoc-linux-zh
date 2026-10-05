

# 引导管理 第 3 章 47

## 注意事项

SUSE Linux 提供了在初始 Linux 安装或升级期间安装 LILO 的机会。你还有机会在 LILO 安装过程之前创建一个启动磁盘——执行它吧！即使你不使用这块磁盘，在万一出现问题时，拥有一个小小的保险也会让你获益。如果你没有安装 LILO，你将绝对需要这块磁盘。

在对硬盘进行分区以及将 Linux 及其相关软件拷贝到硬盘之后，LILO 就会被安装。LILO 通常通过以下三种传统方式之一启动 Linux：

- 从你硬盘的主引导记录 (MBR)
- 从你硬盘上根 Linux 分区的超级块 (superblock)
- 从软盘中启动

接下来的章节将向你列出 LILO 的配置参数列表及其命令行参数，并指出的一些特殊功能。

## 安装和配置 LILO

虽然使用 `lilo` 命令（位于 `/bin` 目录下）可以轻松安装 LILO，但你应该先花时间阅读它的文档。你可以在此书 CD-ROM 的 `docs/loadin` 目录下找到它，或者在安装后在 `/usr/doc/packages/lilo` 目录下找到它。LILO 的文档包含了其功能的细节，并为特殊问题提供了重要的提示和替代方案，例如在大容量硬盘上安装引导加载程序或从其他操作系统启动。

## 注意事项

在尝试对 LILO 进行任何操作之前，你应该准备一个紧急启动磁盘（更多信息请参阅 `/usr/doc/howto/en/Bootdisk-HOWTO`）。系统无法启动可不好玩，而且如果你没有启动磁盘，你可能会认为没有办法重新进入系统并更改设置。花费几分钟制作一个启动磁盘可以避免你日后遇到大头疼的麻烦。

![](img/cbac72550c7126a22162e94d91a0c360_82_0.png)

## 手动安装或重新配置 LILO

如果你在安装 SuSE Linux 时没有安装 LILO，你可以通过两个基本步骤（以 root 身份）安装 LILO：

1. 配置 `/etc/lilo.conf`。
2. 运行 `/sbin/lilo` 安装 LILO 并使其生效。

本讨论描述了修改现有的 `lilo.conf` 文件。在进行任何更改之前，请为自己一个忙，在同一目录或单独磁盘上创建该文件的备份。有几个文件对 LILO 非常重要，并且在初始安装期间创建：

- `/sbin/lilo`——一个映射安装器，更多信息请参见 `man lilo`。
- `/boot/boot.b`——一个引导加载程序。
- `/boot/map`——一个包含内核位置的引导映射。
- `/etc/lilo.conf`——LILO 的配置文件。

## 配置 LILO

在 Linux 下，你的硬盘被抽象为（即引用或指为）`/dev` 目录。如果你有一个或多个 IDE 驱动，你的第一块硬盘被称为 `/dev/hda`，第二块硬盘被称为 `/dev/hdb`（硬盘“a”和硬盘“b”）。SCSI 驱动被称为 `/dev/sda` 和 `/dev/sdb`（scsi 驱动“a”和 scsi 驱动“b”）。当你安装 Linux 时，你很可能对硬盘进行了分区（至少为了创建一个交换分区）。你硬盘上的第一个分区将是 `/dev/hda1` 或 `/dev/sda1`，第二个分区将是 `/dev/hda2` 或 `/dev/sda2`，依此类推。

在配置 LILO 之前，你应该知道哪些分区上运行着操作系统。你还应该知道在哪里安装 LILO。在大多数情况下，你都会希望将 LILO 放在 MBR 上。但是，如果你运行的是 OS/2、BootMagic 或类似的产品，就不应该这样做，因为它们使用了 MBR。如果你正在使用这些类型的软件包，LILO 应该安装在根 Linux 分区的超级块上。

你可以通过运行 `df` 命令（`/bin/df`）查看你当前正在使用哪些分区（或在 Linux 内部挂载了哪些分区）：

```
df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1973472 1161391 710070 62% /
/dev/hda3 4036649 2443 3825361 0% /home
/dev/hdc 592892 592892 0 100% /mnt/cdrom
/dev/fd0 1423 57 1366 4% /mnt/floppy
```

准备好这些信息后，你现在准备好编辑 LILO 的配置文件 `/etc/lilo.conf` 了。

## 编辑 lilo.conf

编辑 `lilo.conf` 很容易。确保你已以 root 身份登录，并将文件加载到你喜喜欢的编辑器中，确保保存你的更改并将文件保存为 ASCII 文本。编辑 `lilo.conf` 有几个原因：

- 你正在测试一个新内核，并希望能够多次启动同一个 Linux 分区。这是通过使用 `lilo.conf` 中 `image` 部分的多个条目来实现。
- 你的分区上可能安装了多个内核，可以通过输入其名称（在 root 中指定）来启动不同的内核。
- 你想为分区添加密码保护。
- 你的硬件设置需要你指定特殊选项。

在尝试对 LILO 进行任何操作之前，你应该准备一个紧急启动磁盘。![](img/cbac72550c7126a22162e94d91a0c360_82_0.png)

如果你在安装 SuSE Linux 时没有安装 LILO，你可以通过两个基本步骤（以 root 身份）安装 LILO：

1. 配置 `/etc/lilo.conf`。
2. 运行 `/sbin/lilo` 安装 LILO 并使其生效。

本讨论描述了修改现有的 `lilo.conf` 文件。在进行任何更改之前，请为自己一个忙，在同一目录或单独磁盘上创建该文件的备份。有几个文件对 LILO 非常重要，并且在初始安装期间创建：

- `/sbin/lilo`——一个映射安装器，更多信息请参见 `man lilo`。
- `/boot/boot.b`——一个引导加载程序。
- `/boot/map`——一个包含内核位置的引导映射。
- `/etc/lilo.conf`——LILO 的配置文件。

## 配置 LILO

在 Linux 下，你的硬盘被抽象为（即引用或指为）`/dev` 目录。如果你有一个或多个 IDE 驱动，你的第一块硬盘被称为 `/dev/hda`，第二块硬盘被称为 `/dev/hdb`（硬盘“a”和硬盘“b”）。SCSI 驱动被称为 `/dev/sda` 和 `/dev/sdb`（scsi 驱动“a”和 scsi 驱动“b”）。当你安装 Linux 时，你很可能对硬盘进行了分区（至少为了创建一个交换分区）。你硬盘上的第一个分区将是 `/dev/hda1` 或 `/dev/sda1`，第二个分区将是 `/dev/hda2` 或 `/dev/sda2`，依此类推。

在配置 LILO 之前，你应该知道哪些分区上运行着操作系统。你还应该知道在哪里安装 LILO。在大多数情况下，你都会希望将 LILO 放在 MBR 上。但是，如果你运行的是 OS/2、BootMagic 或类似的产品，就不应该这样做，因为它们使用了 MBR。如果你正在使用这些类型的软件包，LILO 应该安装在根 Linux 分区的超级块上。

你可以通过运行 `df` 命令（`/bin/df`）查看你当前正在使用哪些分区（或在 Linux 内部挂载了哪些分区）：

```
df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1973472 1161391 710070 62% /
/dev/hda3 4036649 2443 3825361 0% /home
/dev/hdc 592892 592892 0 100% /mnt/cdrom
/dev/fd0 1423 57 1366 4% /mnt/floppy
```

准备好这些信息后，你现在准备好编辑 LILO 的配置文件 `/etc/lilo.conf` 了。

## 编辑 lilo.conf

编辑 `lilo.conf` 很容易。确保你已以 root 身份登录，并将文件加载到你喜喜欢的编辑器中，确保保存你的更改并将文件保存为 ASCII 文本。编辑 `lilo.conf` 有几个原因：

- 你正在测试一个新内核，并希望能够多次启动同一个 Linux 分区。这是通过使用 `lilo.conf` 中 `image` 部分的多个条目来实现。
- 你的分区上可能安装了多个内核，可以通过输入其名称（在 root 中指定）来启动不同的内核。
- 你想为分区添加密码保护。
- 你的硬件设置需要你指定特殊选项。

在尝试对 LILO 进行任何操作之前，你应该准备一个紧急启动磁盘（更多信息请参阅 `/usr/doc/howto/en/Bootdisk-HOWTO`）。![](img/cbac72550c7126a22162e94d91a0c360_82_0.png)

如果你在安装 SuSE Linux 时没有安装 LILO，你可以通过两个基本步骤（以 root 身份）安装 LILO：

1. 配置 `/etc/lilo.conf`。
2. 运行 `/sbin/lilo` 安装 LILO 并使其生效。

本讨论描述了修改现有的 `lilo.conf` 文件。在进行任何更改之前，请为自己一个忙，在同一目录或单独磁盘上创建该文件的备份。有几个文件对 LILO 非常重要，并且在初始安装期间创建：

- `/sbin/lilo`——一个映射安装器，更多信息请参见 `man lilo`。
- `/boot/boot.b`——一个引导加载程序。
- `/boot/map`——一个包含内核位置的引导映射。
- `/etc/lilo.conf`——LILO 的配置文件。

## 配置 LILO

在 Linux 下，你的硬盘被抽象为（即引用或指为）`/dev` 目录。如果你有一个或多个 IDE 驱动，你的第一块硬盘被称为 `/dev/hda`，第二块硬盘被称为 `/dev/hdb`（硬盘“a”和硬盘“b”）。SCSI 驱动被称为 `/dev/sda` 和 `/dev/sdb`（scsi 驱动“a”和 scsi 驱动“b”）。当你安装 Linux 时，你很可能对硬盘进行了分区（至少为了创建一个交换分区）。你硬盘上的第一个分区将是 `/dev/hda1` 或 `/dev/sda1`，第二个分区将是 `/dev/hda2` 或 `/dev/sda2`，依此类推。

在配置 LILO 之前，你应该知道哪些分区上运行着操作系统。你还应该知道在哪里安装 LILO。在大多数情况下，你都会都会将 LILO 放在 MBR 上。但是，如果你运行的是 OS/2、BootMagic 或类似的产品，就不应该这样做，因为它们使用了 MBR。如果你正在使用这些类型的软件包，LILO 应该安装在根 Linux 分区的超级块上。

你可以通过运行 `df` 命令（`/bin/df`）查看你当前正在使用哪些分区（或在 Linux 内部挂载了哪些分区）：

```
df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1973472 1161391 710070 62% /
/dev/hda3 4036649 2443 3825361 0% /home
/dev/hdc 592892 592892 0 100% /mnt/cdrom
/dev/fd0 1423 57 1366 4% /mnt/floppy
```

准备好这些信息后，你现在准备好编辑 LILO 的配置文件 `/etc/lilo.conf` 了。

## 编辑 lilo.conf

编辑 `lilo.conf` 很容易。确保你已以 root 身份登录，并将文件加载到你喜喜欢的编辑器中，确保保存你的更改并将文件保存为 ASCII 文本。编辑 `lilo.conf` 有几个原因：

- 你正在测试一个新内核，并希望能够多次启动同一个 Linux 分区。这是通过使用 `lilo.conf` 中 `image` 部分的多个条目来实现。
- 你的分区上可能安装了多个内核，可以通过输入其名称（在 root 中指定）来启动不同的内核。
- 你想为分区添加密码保护。
- 你的硬件设置需要你指定特殊选项。

在尝试对 LILO 进行任何操作之前，你应该准备一个紧急启动磁盘（更多信息请参阅 `/usr/doc/howto/en/Bootdisk-HOWTO`）。![](img/cbac72550c7126a22162e94d91a0c360_82_0.png)

如果你在安装 SuSE Linux 时没有安装 LILO，你可以通过两个基本步骤（以 root 身份）安装 LILO：

1. 配置 `/etc/lilo.conf`。
2. 运行 `/sbin/lilo` 安装 LILO 并使其生效。

本讨论描述了修改现有的 `lilo.conf` 文件。在进行任何更改之前，请为自己一个忙，在同一目录或单独磁盘上创建该文件的备份。有几个文件对 LILO 非常重要，并且在初始安装期间创建：

- `/sbin/lilo`——一个映射安装器，更多信息请参见 `man lilo`。
- `/boot/boot.b`——一个引导加载程序。
- `/boot/map`——一个包含内核位置的引导映射。
- `/etc/lilo.conf`——LILO 的配置文件。

## 配置 LILO

在 Linux 下，你的硬盘被抽象为（即引用或指为）`/dev` 目录。如果你有一个或多个 IDE 驱动，你的第一块硬盘被称为 `/dev/hda`，第二块硬盘被称为 `/dev/hdb`（硬盘“a”和硬盘“b”）。SCSI 驱动被称为 `/dev/sda` 和 `/dev/sdb`（scsi 驱动“a”和 scsi 驱动“b”）。当你安装 Linux 时，你很可能对硬盘进行了分区（至少为了创建一个交换分区）。你硬盘上的第一个分区将是 `/dev/hda1` 或 `/dev/sda1`，第二个分区将是 `/dev/hda2` 或 `/dev/sda2`，依此类推。

在配置 LILO 之前，你应该知道哪些分区上运行着操作系统。你还应该知道在哪里安装 LILO。在大多数情况下，你都会都会将 LILO 放在 MBR 上。但是，如果你运行的是 OS/2、BootMagic 或类似的产品，就不应该这样做，因为它们使用了 MBR。如果你正在使用这些类型的软件包，LILO 应该安装在根 Linux 分区的超级块上。

你可以通过运行 `df` 命令（`/bin/df`）查看你当前正在使用哪些分区（或在 Linux 内部挂载了哪些分区）：

```
df
Filesystem 1k-blocks Used Available Use% Mounted on
/dev/hda1 1973472 1161391 710070 62% /
/dev/hda3 4036649 2443 3825361 0% /home
/dev/hdc 592892 592892 0 100% /mnt/cdrom
/dev/fd0 1423 57 1366 4% /mnt/floppy
```

准备好这些信息后，你现在准备好编辑 LILO 的配置文件 `/etc/lilo.conf` 了。

## 编辑 lilo.conf

编辑 `lilo.conf` 很容易。确保你已以 root 身份登录，并将文件加载到你喜喜欢的编辑器中，确保保存你的更改并将文件保存为 ASCII 文本。编辑 `lilo.conf` 有几个原因：

- 你正在测试一个新内核，并希望能够多次启动同一个 Linux 分区。这是通过使用 `lilo.conf` 中 `image` 部分的多个条目来实现。
- 你的分区上可能安装了多个内核，可以通过输入其名称（在 root 中指定）来启动不同的内核。
- 你想为分区添加密码保护。
- 你的硬件设置需要你指定特殊选项。

### 表 3.1 LILO 参数

| 参数 | 描述 |
| :--- | :--- |
| boot=<boot_device> | 指定引导扇区的设备。 |
| linear | 生成线性扇区地址，而不是扇区地址。 |
| install=<boot_sector> | 安装指定的扇区。如果省略，则使用默认值。 |
| message=<message_file> | 使用此文件显示消息信息。使用此选项时，LILO 会提示加密信息。 |
| verbose=<level> | 开启进度报告。数字范围为 1 到 5。数字越大输出越详细。请参考 LILO 文档。 |
| backup=<backup_file> | 将原始扇区拷贝到 <backup_file>（可以是设备，如 /dev/null）。 |
| Force-backup<backup_file> | 与 backup 类似，使用 force-backup 选项时会覆盖备份。 |
| prompt | 需要输入提示符。 |
| timeout=<secs> | 设置键盘输入的超时时间（以十分秒为单位），适用于你想立即启动或等待默认五秒的情况。要让 LILO 无限等待按键，使用值 -1。 |
| Ignore | 忽略密码保护引导镜像。 |
| password=<password> | 如果没有将 lilo.conf 设置为只读权限 (-rw-------)，LILO 会发出警告——密码未加密！ |
| unsafe | 放在分区定义之后。该关键字告诉 LILO 不要尝试读取 MBR 或该磁盘的分区表项。 |

## 使用 YaST 命令安装 LILO

使用 SuSE YaST 命令是安装或重新配置 LILO 的一种简单方法。你必须是 root 操作员才能使用 YaST。虽然你可以通过 YaST 菜单导航到 LILO 配置部分，但更简单直接跳转到 LILO 管理的方法是使用 YaST 的 --mask 选项，后跟关键字 lilo，如下：

```
# yast --mask lilo
```

你将看到 LILO 安装对话框，如图 3.1 所示。

