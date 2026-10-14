
在 `/proc/acpi` 中，你现在可以找到许多提供系统状态信息的文件，或用于激活某些状态的文件。然而，许多功能尚未生效，要么是因为它们仍在开发中，要么是因为厂商尚未实现。

### 注意事项

> 到目前，ACPI 尚未支持挂起到内存（suspend to RAM）或挂起到磁盘（hibernation）。由于内核特定的原因，这些功能将从内核 2.6（或内核 2.5）开始才可用。如果你认为你可以这样做，请在你的内核中集成 `sw-suspend` 补丁。

### 注意事项

所有文件（`dsdt` 和 `fadt` 除外）都可以用 `cat` 读取。在某些文件中，可以使用 `echo X > file` 来修改设置，通过为 X 指定合适的值来完成修改（`/proc` 下的所有对象都 map 不是硬盘上的真实文件，而是内核的接口）。以下是最重要文件的描述：

- `/proc/acpi/info`：关于 ACPI 的通用信息

- `/proc/acpi/alarm`：在这里指定系统应何时从睡眠中唤醒。时间通过 `年-月-日 小:分:秒 > /proc/acpi/alarm` 设置。然而，由于睡眠状态尚未生效，设置闹钟是愚蠢的。

- `/proc/acpi/sleep`：提供可能的睡眠状态信息。未来，将能够激活挂起。目前，可能有效的状态是 S1（待机）和 S5（立即关闭，无正常关机）：`echo 1 > /proc/acpi/sleep`。

- `/proc/acpi/event`：所有事件都报告在这里。这些事件由守护进程处理，如 `acpid` 或 `ospmd`。如果没有守护进程访问此文件，可以使用 `cat /proc/acpi/event` 读取事件（用 Ctrl+C 终止）。短时间按一下电源按钮或关闭盖子都是这些事件中的某些。

- `/proc/acpi/dsdt` 和 `/proc/acpi/fadt`：这些文件包含 ACPI 表 DSDT 和 FADT。这些文件可以使用 `acpidmp`、`acpidasm` 和 `dmcode` 读取。这些程序及其文档位于 `mntools` 软件包中。示例：`acpidmp DSDT | acpidasm`

- `/proc/acpi/ac_adapter/ACState`：AC 电源适配器是否连接？

- `/proc/acpi/BAT*/alarm,info,state`：关于电池状态的详细信息。要读取电池电量，将来自 `info` 的总容量与此文件中的剩余容量进行比较。使用特殊程序会更方便。在 `alarm` 中可以指定触发电池事件的电量水平。

- `/proc/acpi/button`：此目录包含各种开关的信息。

- `/proc/acpi/fan/FAN/state`：显示风扇当前是否处于激活。也可以通过向此文件写入 0（开启）或 3（关闭）来手动开启关闭风扇。然而，内核中的 ACPI 代码和硬件（或 BIOS）在温度过高时都会覆盖此设置。

- `/proc/acpi/processor/CPU0/info`：关于处理器节电可能性的信息。

- `/proc/acpi/processor/CPU0/power`：关于当前处理器状态的信息。C2 旁边的星号表示处理器处于空闲状态。从使用率图可以看出，这是主流状态。

- `/proc/acpi/processor/CPU0/performance`：在这里你可以读取或设置性能——使用 CPU 的 Speedstep 或 PowerNow 能力。

- `/proc/acpi/processor/CPU0/throttling`：此文件允许对处理器进行进一步的节流。

- `/proc/acpi/processor/CPU0/limit`：如果性能和节流由守护进程自动控制，则在此指定不应超过的限制。这里有系统定义的限制和用户定义的限制。通过 `echo 1:5 > /proc/acpi/processor/CPU0/limit`，防止使用 P0 或 T0–T4 状态。

- `/proc/acpi/thermal_zone/`：每个热区都有一个子目录。热区是一个具有相似热性的区域，其数量和名称由硬件制造商选择。然而，ACPI 提供的许多可能性很少被实现。相反，温度控制由 BIOS 直接以传统方式处理。操作系统没有太多干预机会，硬件的寿命会受到影响。因此，以下某些描述仅具有理论价值。

- `/proc/acpi/thermal_zone/*temperature`：热区的当前温度。

- `/proc/acpi/thermal_zone/*state`：状态表示一切是否“正常”或 ACPI 是否使用“激活”

- `/proc/acpi/thermal_zone/*cooling`：操作系统没有被给予太多干预机会

- `/proc/acpi/thermal_zone/*cooling_mode`：在这里选择冷却方法

- `/proc/acpi/thermal_zone/*trip_points`：ACPI 在 Linux 中的实现

- `/proc/acpi/thermal_zone/*polling_frequency`：每隔 X 秒查询一次温度

### ACPI 守护进程 (acpid)

ACPI 守护进程以类似于 APM 的方式处理事件。所有事件记录在系统日志中。ACPI_POWER 和 ACPI_LID 包含了这些事件。`/usr/sbin/acpid` 可以被修改 与 apmd 不同，这里没有预配置；如果你有任何建议，请发送电子邮件到 feedback@suse.de。

# ospmd

`ospmd`（操作系统电源管理守护进程）是 `acpid` 的替代方案。遗憾的是，它还没有被高度开发。目前更像是一项可行性研究。

有一些更全面的 ACPI 工具。某些是纯信息工具，显示电池状态、温度等（`acpi`, `wmacpi` 等）。某些便于访问 `/proc/acpi` 下的结构（`akpi`）。其他是根据配置、温度和系统负载控制 CPU 的守护进程（`speedtest`）。要查看哪些工具可用，启动 YaST 软件模块并搜索 "acpi"。其中包含在线文档。

### 故障排除

问题有两种类型。一方面，内核 ACPI 核心可能存在未检测到的错误。在这种情况下，将提供可供下载的解决方案。另一方面，计算机的 BIOS 可能存在问题。这种情况更常见且更令人恼。遗憾的是，对 ACPI 规范的偏有时会被正确集成到 BIOS 中，以回避其他流行的操作系统的 ACPI 实现错误。在 ACPI 实现中有严重错误的硬件组件被记录在黑列表中，以防止 Linux 内核对这些组件使用 ACPI。

如果你遇到问题，你应该做的是更新 BIOS。这将解决许多问题。如果计算机无法正常启动，以下启动参数可能有用：

- `pci=noacpi`：不要使用 ACPI 配置 PCI 设备。

- `acpi=oldboot`：只执行简单的资源配置。不要将 ACPI 用于其他目的。

- `acpi=off`：禁用 ACPI。

另一个重要的步骤是仔细查看启动消息。这样做使用命令 `dmesg | grep -i acpi`（或所有其他消息，因为问题可能是 ACPI 以外的原因）计算机已启动。如果在解析 ACPI 表时发生错误，至少可以通过集成改进后的表来替换最重要的表——DSDT。这将导致故障的 DSDT 的

应忽略 BIOS。然而，这并非易事，需要专家的协助。互联网上可以找到某些计算机的修复 Bug 的 DSDTs。

对于内核配置，有一个开关可以激活 ACPI 调试信息。如果你能编译并安装带有 ACPI 调试功能的内核，就可以为寻找错误的专家提供详细信息以供支持。

如果你遇到 BIOS 或硬件问题，建议始终联系设备制造商。尽管制造商并不总是能够为 Linux 提供帮助，但让他们尽可能多地听到“Linux”这个词仍然至关重要。只有当制造商意识到有足够数量的客户在使用 Linux 时，他们才会认真对待它。当然，你也可以联系制造商，告诉他们你正毫无困难地在硬件上使用 Linux。

在以下来源中可以找到额外的文档和帮助：

- http://www.columbia.edu/~ariel/acpi/acpi_howto.txt（稍显过时的 ACPI HowTo，不完整）

- http://www.cplinux.com/acpi-howto.html（更详细的 ACPI HowTo，包含 DSDT 补丁）

- http://www.brode.de/english/pub/acpi/proc/processor.html（子目录 `/proc/acpi/processor` 的描述）

- http://www.intel.com/technology/iapc/acpi/faq.html（Intel 的 ACPI FAQ）

- http://acpi.sourceforge.net/（Sourceforge 上的 ACPILinux 项目）

- http://www.brode.de/english/pub/acpi/index.html（ACPI 补丁）

- http://codecs.home.sapo.pt/acpi/index.html（ACPI 补丁）
