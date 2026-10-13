
```c
struct anon_info {

    int ani_max;          /* 物理交换上可预留槽的总数 */

    int ani_free;         /* 未分配物理和内存槽的数量 */

    int ani_phys_res;     /* 已预留物理（磁盘）槽的数量 */

    int ani_mem_res;      /* 已预留内存槽的数量 */

    int ani_locked_swap;  /* 内存中锁定的交换槽数量 */

};
```

### 头文件 `<sys/anon.h>`

`anon_info` 结构记录了物理交换和内存上预留槽位的数量。这些信息用于填充 `swapctl` 系统调用的数据。`swapctl()` 为 `swap` 命令提供数据。交换系统调用使用了稍不同的数据结构，即下所示 `anoninfo` 结构。

```c
struct anoninfo {

    int ani_max;

    int ani_free;

    int ani_res;

};
```

### 头文件 `<sys/anon.h>`

`anoninfo` 结构以平台无关的方式导出交换分配信息。下面的 `swap` 命令输出总结了来自 `anoninfo` 结构的信息。

```bash
# swap -s
total: 108504k allocated + 13688k reserved = 122192k used, 114880k available
```

`swap -s` 的输出可能有点误导性，因为它混淆了交换定义的术语。输出实际上告诉我们，已经使用了 122,192 K字节的虚拟交换空间，108,504 K字节的交换空间分配给了已访问的页面，有 114,880 K字节是空闲的。这些信息反映了图 5.15 中的交换分配阶段。记住，我们在创建虚拟内存时会预留交换空间，当真实页面被分配到地址空间时，那部分交换空间会被分配。剩余的交换空间保持未使用。

![](img/a86367b95bf21add858c99948ac951c_208_0.png)

图 5.15 交换分配状态

你可以使用 MemTool 3.8.1 中的 `prtswap` 脚本（参见第 242 页的“MemTool: Unbundled Memory Tools”）来列出交换的状态并找出交换是从哪里分配的，如下所示。如果只需要交换分配摘要，请使用 `prtswap` 命令。

```bash
# prtswap -l
Swap Reservations:
Total Virtual Swap Configured:          767MB
RAM Swap Configured:                    255MB
Physical Swap Configured:               512MB
Virtual Swap Reserved Against:         513MB
RAM Swap Reserved Against:             1MB
Physical Swap Reserved Against:        512MB
Virtual Swap Unresv. & Avail. for Reservation:  253MB
Physical Swap Unresv. & Avail. for Reservations:  0MB
RAM Swap Unresv. & Avail. for Reservations:  253MB
Swap Allocations: (Reserved and Phys pages allocated)
Total Virtual Swap Configured:          767MB
Total Swap Allocated Against:          467MB
Physical Swap Utilization: (pages swapped out)
Swap Free (should not be zero):         232MB
```

## Solaris 内存架构

```bash
# swap -
Virtual Swap:
Total Virtual Swap Configured:          767MB
Virtual Swap Reserved Against:         513MB
Virtual Swap Unresv. & Avail. for Reservation:  253MB
Physical Swap Utilization: (pages swapped out)
Physical Swap Configured:               512MB
Physical Swap Reserved Against:        512MB
Physical Swap Unresv. & Avail. for Reservations:  0MB
RAM Swap Configured:                    255MB
RAM Swap Reserved Against:             1MB
RAM Swap Unresv. & Avail. for Reservations:  253MB
```

```c
#include <sys/types.h>
#include <sys/fcntl.h>
#include <procfs.h>
typedef struct {
    long cmd;
    prwatch_t prwatch;
} ctl_t;
int main(int argc, char **argv) {
    int ctlfd;
    ctl_t ctl;
    int test;
    if ((ctlfd = open("/proc/self/ctl1", O_WRONLY)) < 0) {
        perror("/open/proc");
        exit(1);
    }
    ctl.cmd = PCOWATCH;
    ctl.prwatch.pr_vaddr = (uintptr_t)test;
    ctl.prwatch.pr_size = sizeof(int);
    ctl.prwatch.pr_wflags = WA_READ|WA_WRITE;
    if (write(ctlfd, &ctl, sizeof(ctl)) != sizeof(ctl)) {
        perror("Set PCOWATCH");
        exit(1);
    }
    test = 0;
}
```

当我们尝试向整数 `test` 写入数据时，会触发断点陷阱（waypoint trap），默认情况下，进程会产生核心储（core dump）。

`$ ./watchpoint`
`Trace/Breakpoint Trap(coredump)`

`/proc` 进程信息文件 `prinfo` 包含了与断点陷阱相关的信息，并可以读取到结构体 `pr_info` 中。特别是特别是，`si_addr` 字段包含触发断点的内存引用的虚拟地址，而 `si_code` 字段包含 `TRAP_WATCH`、`TRAP_WWATCH` 或 `TRAP_XWATCH` 之一，分别表示读、写或执行访问。除非 `WA_TRAPAFTER` 对该监控区域生效，否则 `si_trafter` 字段为零；非零表示当前指令不是引发断点陷阱的指令。`si_pc` 字段包含引发陷阱的指令的虚拟地址。图 5.16 展示了断点数据结构。

## 全局页管理

| `struct proc` | `struct as` |
| :--- | :--- |
| `p_as` | `a_segs` |
| | `a_size` |
| | `a_nsegs` |
| | `a_flags` |
| | `a_hat` |
| | `a_tail` |
| | `a_watchcp` |

| 256-MB Kernel Context |
| :--- |
| Stack |
| Libraries |
| HEAP |
| Executable - DATA |
| Executable - TEXT |

```c
struct watched_page
wp_forw
wp_back
wp_vaddr
wp_prot
```
