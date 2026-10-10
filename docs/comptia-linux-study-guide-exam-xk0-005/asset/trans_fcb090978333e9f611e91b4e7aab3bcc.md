
# 探索挂载单元文件

挂载单元文件的内容与其他 systemd 单元文件类似，但包含一些特殊的部分和选项。在列表 6.28 中，使用 /home/temp/ 挂载点，展示了一个挂载单元文件的示例。

**列表 6.28** 显示一个 systemd 挂载单元文件示例

```bash
# cat /etc/systemd/system/home-temp.mount
[Unit]
Description=Test Mount Units

[Mount]
What=/dev/sdo1
Where=/home/temp
Type=ext4
Options=defaults
SloppyOptions=on
TimeoutSec=4

[Install]
WantedBy=multi-user.target
```

请注意，该文件具有单元文件典型的三个部分，其中中间部分 [Mount] 包含特定于挂载类型单元文件的指令。**What** 指令可以使用设备文件名或通用唯一标识符 (UUID)，例如 /dev/disk/by-uuid/UUID。

**SloppyOptions** 指令非常有用，如果设置为 on，它会忽略特定文件系统类型不支持的任何挂载选项。默认情况下，它设置为 off。另一个有用的指令是 **TimeoutSec**。如果挂载命令未在规定时间内完成，则挂载被视为操作失败。

务必包含 [Install] 部分，并将 **WantedBy** 或 **RequiredBy** 指令设置为目标。如果未执行此操作，文件系统将在服务器启动时不会被挂载。

你可以使用标准的 **systemctl** 实用程序命令手动挂载和卸载单元。列表 6.29 包含部署 home-temp.mount 单元文件的示例。

**列表 6.29** 部署 systemd 挂载单元文件

```bash
# systemctl daemon-reload home-temp.mount
#
# systemctl start home-temp.mount
#
# ls /home/temp
lost+found
```

在列表 6.29 中，第一条命令加载新配置的挂载单元文件。第二条命令使 systemd 使用 `home-temp.mount` 单元文件挂载文件系统。第二条命令类似于启动服务的方式，它使用 `start` 命令。虽然你可以省略 `home-temp` 挂载参数且命令仍会工作，但 (a) 该参数为讨论的情境增加了清晰度/教育意义，且 (b) 该参数防止其他服务被重新加载，如果其他服务重启可能会导致问题。

为了确保文件系统正确挂载，就像服务单元一样，你使用 `systemctl` 实用程序获取已挂载文件系统的状态。示例显示在列表 6.30 中。

**列表 6.30** 检查 systemd 挂载单元的状态

```bash
# systemctl status home-temp.mount
 home-temp.mount - Test Mount Units
   Loaded: loaded (/etc/systemd/system/home-temp.mount; [...])
   Active: active (mounted) since Sat 2019-09-14 16:34:2[...])
   Where: /home/temp
   What: /dev/sdo1
   Process: 3990 ExecMount=/bin/mount /dev/sdo1 /home/temp[...])
   [...]
```

还需要一个额外的步骤。为了确保 systemd 持久地挂载文件系统，必须启用挂载单元文件以在启动时启动，就像启用其他 systemd 单元一样。示例显示在列表 6.31 中。

**列表 6.31** 启用 systemd 挂载单元

```bash
# systemctl enable home-temp.mount
 Created symlink from
 /etc/systemd/system/multi-user.target.wants/home-temp.mount to
 /etc/systemd/system/home-temp.mount.
```

这一切看起来应该非常熟悉！请记住，只有当你需要调整持久文件系统配置时，才应使用挂载单元文件。如果不这样做，最好使用 /etc/fstab 记录来持久挂载文件系统。

## 探索自动挂载单元

使用 systemd，你还可以配置按需挂载以及使用自动挂载单元进行并行挂载。此外，你可以设置文件系统在无活动时自动卸载。

自动挂载单元文件的运行机制与挂载单元文件类似。命名约定相同，只是文件扩展名为 .automount。

在自动挂载单元文件中，对于 [Automount] 部分，只有以下三个指令可用：

- **Where**
- **DirectoryMode**
- **TimeOutIdleSec**

**Where** 指令是必需的。它的配置方式与挂载单元文件中完全相同。使用该指令，你设置挂载点。

**DirectoryMode** 指令不是必需选项。此设置确定自动创建的挂载点和父目录上的权限。默认情况下，它设置为八进制代码 0755。

![](img/c0a399aca0d18f8822d714ad0a173123_255_0.png)

> 你也可以在 /etc/fstab 文件中配置自动挂载点。但是，请记住，如果自动挂载点配置在 /etc/fstab 文件中且它有一个单元文件，则单元文件配置将优先。

**TimeOutIdleSec** 指令也不是必需的。该特定指令允许你设置已挂载文件系统可以空闲的最长时间（以秒为单位）。一旦达到时间限制，文件系统将被卸载。默认情况下，此指令处于禁用状态。

## 关注定时器单元文件

定时器单元文件允许你定义在特定日期或时间发生的事件，类似于 cron 程序的工作方式（参见第 26 章，“自动化任务”）。定时器单元文件允许你微调程序启动的确切时间。

定时器单元文件由 .timer 文件扩展名标识，并包含 [Timer] 部分以定义确定何时启动事件所需的指令。表 6.13 描述了这些指令。

**表 6.13** 常用的定时器单元文件 [Timer] 部分指令

| 指令 | 描述 |
| :--- | :--- |
| AccuracySec | 指定定时器的精度。默认为一分钟。 |
| OnActiveSec | 定义定时器相对于定时器激活时刻的时间。 |
| OnBootSec | 定义定时器相对于系统启动时的时间。 |
| OnCalendar | 将定时器定义为特定的日期/时间值。 |
| OnStartupSec | 定义定时器相对于 systemd 程序启动时的时间。 |
| OnUnitActiveSec | 定义定时器相对于定时器单元最后一次激活时的时间。 |
| OnUnitInactiveSec | 定义定时器相对于定时器单元最后一次非激活时的时间。 |
| Persistent | 当设置时，定时器单元上次触发的时间存储在磁盘上。 |
| RandomizedDelaySec | 延迟定时器激活随机量的时间。 |
| RemainAfterElapse | 当设置时，已过期的定时器单元保持加载状态，允许你使用 `systemctl` 查询其状态。 |
| Unit | 定义定时器过时时启动的单元文件。 |
| WakeSystem | 当设置时，定时器单元将导致系统从挂起状态恢复。 |

如表 6.13 所示，定时器单元提供了设置定时器的多种选项。这允许你选择程序在系统上启动的确切时间。

## 总结

管理服务器最终系统初始化阶段是初始化守护程序的工作。该守护程序必须根据你在适当配置文件中提供的信息确定要启动哪些服务。此外，该守护程序可以在系统运行时管理服务。

经典的系统初始化守护程序 SysV init 仍然存在，但通常仅出现在较旧的发行版上。流行且现代的 systemd 在当前 Linux 发行版中广泛使用。它不仅允许更快的服务器启动时间，还提供其他服务，例如自动挂载文件系统。系统管理员常常发现自己从 SysV init 系统迁移到 systemd 服务器，因此理解这两种系统初始化方法至关重要。

## 考试要点

**描述 init 程序。** *init* 程序或 systemd 是 Linux 系统中每个服务的父进程。它通常具有 PID 1。该程序位于 `/etc/`、`/bin/` 或 `/sbin/` 目录中。在 systemd 服务器上，该程序是指向 `/usr/lib/systemd/systemd` 的符号链接。

**总结 systemd 单元概念。** systemd 单元定义一个服务、一组服务或一个操作，目前共有 12 种不同的 systemd 单元类型。要查看加载的单元，使用 `systemctl list-units` 命令。重点关注的四种 systemd 单元是 service、target、mount 和 automount。

