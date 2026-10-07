
几年前，当 Linux 内核开发者开始探索在内核中实现额外安全功能的方法时，AppArmor 和 SELinux 都使用了 LSM。Linus 在内核中……，他们很快意识到挑战将是支持兼容 LSM 的不同安全技术，具体取决于使用场景。我将在本文稍后为你详细介绍锁定模式的完整性（integrity）和机密性（confidentiality）模式。

通用的 LSM 接口允许其他代码在内核的某些点挂钩并实现安全策略。更棘手的是，还需要确保该解决方案允许不同的发行版继续开发。

在原则上，可以通过调用 `echo integrity` 或 `confidentiality` 在运行时激活锁定模式。`lockdown` 参数有两个参数：integrity 和 confidentiality。

只需在现有参数后添加用逗号分隔的 `lockdown` 和 `yama` 即可。

### 高级 LSM 特性

`Lsm` 参数激活 LSM 子系统，并期望设置为 `Lsm=lockdown,yama`。为了实现锁定模式，内核受到了限制。你无法再使用 `kexec` 参数来执行锁定。如果其他模块已经激活了 LSM，内核开发人员必须扩展 LSM 以允许系统直接启动到新内核。

在之前的版本中，LSM 仅设计用于在用户空间（即为内核提供策略的环境）处于活动后处理问题。然而，攻击者可以修改系统，使其在运行后立即加载恶意代码。

图 2：虽然你可以在系统启动时启用锁定模式，但这种选项并不安全。

```c
const char *const lockdown_reasons[LOCKDOWN_CONFIDENTIALITY_MAX+1] = {
[LOCKDOWN_NONE] = "none",
[LOCKDOWN_MODULE_LOAD] = "unsigned module loading",
[LOCKDOWN_DEV_MEM] = "/dev/mem,kmem,port",
[LOCKDOWN_AF_INET] = "/dev/sda raw access",
[LOCKDOWN_KEXEC] = "kexec of unsigned images",
[LOCKDOWN_REBIRTHATION] = "liberation",
[LOCKDOWN_PC_ACCESS] = "direct port access",
[LOCKDOWN_IOCTL] = "raw to port access",
[LOCKDOWN_READ] = "raw mem access",
[LOCKDOWN_ACPI_TABLE] = "modifying ACPI tables",
[LOCKDOWN_PCCI_STORAGE] = "linux PCI storage",
[LOCKDOWN_TICKERSERIAL] = "reconfiguration of serial port 10",
[LOCKDOWN_MODULE_PARAMETERS] = "unsafe module parameters",
[LOCKDOWN_MIGRATE] = "unsafe mlo",
[LOCKDOWN_SERF] = "unsafe access",
[LOCKDOWN_CREATING] = "integrity",
[LOCKDOWN_CORE] = "/proc/core access",
[LOCKDOWN_DEBUGS] = "use of debugfs",
[LOCKDOWN_BPF_READ] = "use of bpf to read kernel RAM",
[LOCKDOWN_PFS] = "unsafe use of part",
[LOCKDOWN_TRACEFS] = "use of tracefs",
[LOCKDOWN_KMEM_RW] = "mmon read and write access",
[LOCKDOWN_CONFIDENTIALITY_MAX] = "confidentiality",
};
```

## 锁定模式 (Lockdown Mode)

Linux 内核中的某些模块甚至存在了几十年。事实是，各种软件工具已经开始依赖被显式标记为“不安全”的功能。在**完整性模式（integrity mode）**下，内核防止 root 用户使用加载此类模块的参数。如果 root 用户尝试使用该参数，`/proc/line` 文件中定义了锁定参数，并取决于它是否具有适用锁定模式的值。因此，内核开发人员认为锁定模块加载了不安全的模块，用户将立即看到内核返回的“拒绝访问”（Permission Denied）响应。

### 锁定模式（续）

内核开发人员不得不扩展 LSM 以允许系统直接启动到新内核。

被识别为不安全的 MMIO 操作会被内核阻止，某些使用 `perf` 的方式也是如此。另一个重要事实是：如果系统意外重启，所有警报都应该响。这对于**机密性模式（confidentiality mode）**尤为如此。如果机密性模式不适合你的系统，你可以使用完整性模式，它可以防止攻击者有系统地打开安全漏洞。这解释了为什么完整性模式也会全面禁用这些操作。对于移动系统来说也很有趣的是：锁定模式禁用了休眠功能。

大多数情况下，突然重启是由于硬件设备或驱动程序损坏。但你需要快速明确根源。问题也可能是攻击者在更改引导加载程序后重启了系统。如果你想使用锁定模式，我建议监控系统配置的几个额外因素。

该功能在 Linux 5.4 中进入内核，即锁定模式（lockdown mode）。在 2020 年 6 月，这种模式对于由 root 加载的现在已包含在许多桌面系统的 Linux 中。例如，当 ACPI 项目中的漏洞最终导致安全术语变得毫无意义时。然而，企业级发行版允许内核代码绕过 UEFI 安全启动接口——例如 UEFI。

基于组件的安全活动略显落后。在编写本文时，Ubuntu 20.04 LTS 是唯一一个企业级发行版且已通过锁定模块（lockdown module）。

锁定模式让所有管理员非常清楚地意识到，内核应该使用官方的锁定模式。锁定模式绝非仅仅是在特殊场景下提供额外安全性的抽象安全特性。在 RHEL 系统上，该功能尚不可用；但预计 Red Hat 将在未来的 RHEL 8 版本中提供补丁。SUSE 也计划提供补丁。

难以相信的是，在 2020 年，仍然有谈论安全内部和外部网络的安全概念。在七多年后，首席开发人员 Matthew Garrett 成功地将一项切实的功能集成到 Linux 内核中，该功能可以直接并衡量系统的安全性。一旦攻击者获得了系统未授权的 root 权限，几乎所有的安全措施都是致命无效的。[1] Matthew J. Garrett 关于锁定模式的文章立即提供了实质性的改进-[1]。内核开发人员巧妙地通过锁定的形式提交了补丁来阻止这一点：https://mjg59.dreamwidth.org/55105.html。

## 深度解析

## 查找进程

### 按启动时间查找进程

Ghost Hunter

如何通过启动时间查找 Linux 系统上运行的进程？这个问题听起来很平凡，但答案比表面看起来要复杂。作者：Axel Beckert 和 Frank Hofmann。本文比较了使用 Bash、Python、Perl 脚本以及 Go 编程语言的若干种潜在解决方案。作为一个计算集群 [1] 的维护者，Frank 还为他的用户提供了基于公平使用原则的计算商业软件。该软件提供有限的许可证密钥（例如，MATLAB [2] 仿真软件提供10 个密钥）。其中某些计算可能耗时一周。当计算完成且进程终止时，许可证密钥会自动返回空闲密钥池，并供另一个用户获取。然而，如果用户忘记结束进程，由于所有密钥都已分配，将无法再发放密钥。

我们的目标是找到一种解决方案，能够检测仍在运行且启动至少在 10 天之前的进程，然后以排序后的列表输出结果。

- 你必须设置 `LC_TIME` 环境变量以确保本地月份名称不会突然出现（`env LC_TIME=C`）。

- 日期在单数字前有额外的空格。为了排序，你必须使用 `sed` 参数将其替换为零（列表 1 中的第 5-6 行）。

- 输出还将包含用户的登录名或用户 ID、PID、执行的程序以及相应进程开始的时间。

- 启动日期包含字母月份而非数字；你必须将其转换为数字。这可以通过内置工具完成。对于第 7-18 行所示的基于 Bash 的解决方案，你需要旧的 `procps 3.3.0` 版本或更高版本（早期版本缺乏此处使用的一些功能）。

- 日期组件的顺序是：早于 10 天的日期。如果发现发现不适合排序的项（例如第一个月份、符合此标准的进程），他们可以使用 Bash 来明确对该进程应该发生什么。第一个显而易见的解决方案是基于 `ps` 命令并结合四个组件：`awk`、`date`、`sed` 和 `sort`。

Linux 内核管理进程。`ps` 支持输出字段 `lstart`，它将进程的启动时间（和日期）以统一的长格式列出。`/proc` 文件系统对用户可用可用。在命令行中，`ps` 是进程管理的可靠接口。

遗憾的是，`ps` 最初有几十个选项，特别是因为它还可以根据相对规格计算数据，而且它的输出通常也不清晰。这可以通过一点努力来解决。虽然发现并实现组合解决方案（列表 1）很快，但解析 shell 代码或可能的脚本语言使其变得相对难以读懂且相当孤立。我们在该解决方案中遇到了以下问题：

- “现在起 10 天前”的规格通过调用 `date -d 'now -10 days'` 返回。此日期告诉你自进程启动以来的秒数，在 `sort` 调用中减少了进程数量，显著增加了复杂性，因为你必须指定包括日期在内的所有字段，而可以非常灵活地格式化输出。

- 如果在调用脚本时不指定任何参数，它将显示所有大于 10 天的进程。这缩短了命令，使其可以用单行编写。列表 4 返回了所有超过两天的进程。

- 所有进程都在同一秒内启动，在 `sort` 中识别出的进程号是从头开始重新分配的。

- 所有数字字段必须在 `sort` 中显式指定；否则 `sort` 将仅将第一个字段视为数字。

然而，这种变体也适用于长时间，尽管其限制是 65,535 个进程，但现在列表 1 的输出在没有一秒精度限制的情况下，Linux 也可以处理更大的进程 ID (PID)，这很明显，因为 PID 1 并没有出现在列表的开头。这可以通过读取 `sort` 的输出来修复。

列表 1：第一次尝试

```bash
#!/bin/sh
if [ -n $1 ]; then limit=$1; else limit=10; fi
date="$(date '+%Y %m %d %T' -d "now -$limit days")
env LC_TIME=C ps -eahx pid,lstart,user,cmd |
sed -e 's/^//' |
awk -v d="$date" '$1 < d' |
sort -k2,2 -k3,3 -k4,4 -k5,5 -k6,6 -k7,7
```

列表 3：排序输出

```bash
$ ./list-processes.sh | head
2020 04 03 22:32:34 1 root init
2020 04 03 22:32:34 2 root kthreadd
2020 04 03 22:32:34 3 root [rcu_gp]
2020 04 03 22:32:34 4 root [rcu_par_gp]
2020 04 03 22:32:34 6 root [kworker/0:H-kblockd]
2020 04 03 22:32:34 9 root [mm_percpu_wq]
2020 04 03 22:32:34 10 root [ksoftirqd/0]
2020 04 03 22:32:34 11 root [rcu_sched]
2020 04 03 22:32:34 12 root [migration/0]
```

## 深度解析

## 查找进程

由于年龄（age）相同，因此使用 PID 作为标准。我们没有使用 `ps` 命令，而是尝试从 `/proc` 文件系统获取数据作为基础。详细的规范可以在此处找到：`/proc/<pid>/stat`。它告诉你 Linux 内核启动后的时钟滴数（clock ticks）。此外，该值也可以直接写入 172800 trick；这是基于这样一个假设：在缺少参数的情况下，86400 是每天的秒数。

2*24*60*60 对应两天的时钟滴数，每个时钟频率为 100Hz（即每秒 100 刻 [3]）：

### 列表 4：紧凑 Bash 变体

```bash
ps -eaxah etimes,pid,user,cmd | sort -nr | awk '$1 > 10*2*24*60*60 {print}' | head
```

### 列表 2：列表 1 的输出

```bash
ps -eaxho etimes,pid,user,cmd | sort -k1nr,2n | awk '$1 > 10*2*24*60*60 {print}' | head
```

```text
2020 04 03 22:32:34 1 root init
226597 1 root init [2]
2020 04 03 22:32:34 10 root [ksoftirqd]
226597 2 root [kthreadd]
2020 04 03 22:32:34 104 root [kintegrityd]
226597 3 root [rcu_gp]
2020 04 03 22:32:34 105 root [kblockd]
226597 4 root [rcu_par_gp]
2020 04 03 22:32:34 106 root [blkcg_punt_bio]
226597 6 root [kworker/0:0H-kblockd]
2020 04 03 22:32:34 11 root [rcu_sched]
226597 9 root [mm_percpu_wq]
2020 04 03 22:32:34 12 root [migration/0]
226597 10 root [ksoftirqd/0]
2020 04 03 22:32:34 13 root [cpuhp/0]
226597 11 root [rcu_sched]
2020 04 03 22:32:34 14 root [cpuhp/1]
226597 12 root [migration/0]
2020 04 03 22:32:34 15 root [migration/1]
226597 13 root [cpuhp/0]
```

### 列表 5：改进的紧凑 Bash 变体

```bash
ps -eaxah etimes,pid,user,cmd | sort -n -k1 -k2 -k3 -k4 -k5 | awk "$6" "$3" "$4" "$5" "$1 < "'$date'" {print $6} "$3" "$4" "$5" "$1" "$7" "$8"' | head
```

### 列表 6：以天数作为参数

```bash
#!/bin/sh
if [ -n "$1" ]; then
    limit=$1
else
    limit=10
fi
now=$(awk '{print $2}' /proc/$$stat)
ps -eaxho etimes,pid,user,cmd | sort -k1nr,2n | awk '$1 > '$((now-limit*86400))'{ printf "Sec. since boot: %.0f - PID: %i\n", $1}' /proc/[1-9]*/stat
```

### 列表 7：使用时钟滴数的 Bash 脚本

```bash
#!/bin/sh
if [ -n "$1" ]; then
    limit=$1
else
    limit=10
fi
now=$(awk '{print $2}' /proc/$$stat)
ps -eaxho etimes,pid,user,cmd | sort -k1nr,2n | awk '$1 > '$((now-limit*86400))'{ printf "Sec. since boot: %.0f - PID: %i\n", $1}' /proc/[1-9]*/stat
```

### 列表 8：Python 变体

```python
import psutil
import datetime

## 定义全局变量
listOfProcessNames = []

def getListOfProcesses(createTime=10):
    # 以字典形式交付运行中的进程列表
    # PID、程序名、创建时间和所有者
    for proc in psutil.process_iter(attrs=['pid', 'name', 'create_time', 'username']):
        try:
            plInfoDict = proc.info
        except (psutil.NoSuchProcess, psutil.AccessDenied):
            continue
        # (为了简洁起见省略了其余逻辑)
```

### 列表 9：Python 脚本输出

```text
$ python3 list-processes2.py | grep bash
User name: frank, PID: 3428, Program: bash , created on 08.03.2020 21:49:09
$ getconf CLK_TCK
User name: frank, PID: 10438, Program: bash , created on 16.03.2020 21:12:18
```

## 使用现代的 "say" 代替 "print"

为了简单起见，这里使用了硬编码的值。

`use 5.010;`

由于我们希望输出作为一个 

## 极简参数解析：如果传递一个浮点数作为参数（为了美观），则输出该数量的进程，否则输出 10 个。使用 `printf` 将输出限制在两个小数位——这已经 

```perl
my $max = @ARGV ? $ARGV[0] : 10;
```
