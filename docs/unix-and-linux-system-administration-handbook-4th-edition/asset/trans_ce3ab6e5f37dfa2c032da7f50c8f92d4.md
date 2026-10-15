

最初，如果设备配置信息可用，它位于 /proc 文件系统。尽管 /proc 仍然保存着关于进程和内核的运行时信息，但我们预计所有设备特定的信息最终都会迁移到 /sys。

## 使用 udevadm 探索设备

udevadm 命令用于查询设备信息、触发事件、控制 udevd 守护进程以及监控 udev 和内核事件。对管理员而言，其主要用途是构建和测试规则，这些内容将在下一节中介绍。

udevadm 要求其第一个参数为六个命令之一：info、trigger、settle、control、monitor 或 test。对系统管理员而言，最感兴趣的是 info，它会打印设备特定的信息，以及 control，它可以启动和停止 udev 或强制其重新加载规则文件。monitor 命令会显示事件的发生情况。

以下命令显示设备 sdb 的所有 udev 属性。此处的输出被截断，实际上它会继续列出 sdb 在设备树中的所有父设备——例如 USB 总线。

```
linux$ udevadm info -a -n sdb
...
looking at device '/devices/pci0000:00/0000:00:11.0/0000:02:03.0/usb1/1-1/1-1:1.0/host6/target6:0:0/6:0:0:0/block/sdb':
  KERNEL=="sdb"
  SUBSYSTEM=="block"
  DRIVER==""
  ATTR{range}=="16"
  ATTR{ext_range}=="256"
  ATTR{removable}=="1"
  ATTR{ro}=="0"
  ATTR{size}=="1974271"
  ATTR{capability}=="53"
  ATTR{stat}==" 71   986  1561   860    1    0    1   12    0   592   872"
...
```

udevadm 输出中的所有路径，例如 /devices/pci0000:00/...，都是相对于 /sys 的。

输出的格式设计为可将其反馈给 udev 以便构造规则。例如，如果 ATTR{size}=="1974271" 子句对该设备是唯一的，你可以将该片段复制到规则中作为识别条件。

请参阅 udevadm 的手册页以了解更多选项和语法。

## 构造规则和持久名称

Udev 依赖一组规则来指导其对设备的管理和命名。默认规则位于 /lib/udev/rules.d 目录，但本地规则应放在 /etc/udev/rules.d 中。无需编辑或删除默认规则——你可以通过

在自定义规则目录中创建同名的新文件来忽略或覆盖默认规则文件。

udev 的主配置文件为 /etc/udev/udev.conf；不过默认行为是合理的。我们示例发行版上的 udev.conf 文件仅包含注释，除了一行启用错误日志的配置外。

遗憾的是，由于发行版和开发者之间的政治争吵，不同发行版之间几乎没有规则协同。默认规则目录中的许多文件名在各发行版之间相同，但文件内容差异很大。

规则文件命名遵循 nn-description.rules 模式，其中 nn 通常为两位数字。文件按词法顺序处理，因此数字越小越先处理。来自两个规则目录的文件在 udev 守护进程 udevd 解析它们之前会被合并。.rules 后缀是强制性的；没有该后缀的文件将被忽略。

规则的形式为

```
match_clause, [match_clause, ...] assignment_clause [,assignment_clause ...]
```

match_clauses 定义规则适用的情况。每个匹配子句由一个键、一个运算符和一个值组成。例如，上面提到的 ATTR{size}=="1974271" 子句可作为规则的潜在组成部分；它选择所有 size 属性恰好为 1,974,271 的设备。

大多数匹配键引用设备属性（udevd 从 /sys 文件系统获取），但有些引用其他上下文相关属性，例如正在处理的事件（例如设备添加或移除）。所有匹配子句都必须匹配，规则才会激活。

表 13.8 显示了 udev 理解的匹配键。

### 表 13.8 Udev 匹配键

| Match key | Function |
|---|---|
| ACTION | Matches the event type, e.g., add or remove |
| DEVPATH | Matches a specific device path |
| KERNEL* | Matches the kernel's name for the device |
| SUBSYSTEM* | Matches a specific subsystem |
| DRIVER* | Matches the driver used by a device |
| ATTR{filename}* | Matches a device's sysfs values; the filename is a leaf in the sysfs tree that corresponds to a specific attribute |
| ENV{key} | Matches the value of an environment variable |
| TEST[omask] | Tests whether a file exists; the omask is optional |
| PROGRAM | Runs an external command; matches if the return code is 0 |
| RESULT | Matches the output of the last call through PROGRAM |

a. A plural version is also available. It searches up the device path to match the value.

