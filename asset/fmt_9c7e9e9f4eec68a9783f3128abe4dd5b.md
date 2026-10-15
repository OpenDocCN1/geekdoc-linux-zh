
与调度类相关的结构如图 9.3 所示。展示了系统类数组，其中包含指向类操作向量数组、类名称以及类特定初始化例程的指针。还展示了内核线程列表的粗粒度视图，每个线程都链接到其自身的类特定数据结构。该结构维护了调度器用于管理 `kthread` 执行时间和调度调度的位信息；该结构还维护一个指向类操作数组的指针。

# 系统类数组

| cl_name | "SYS" | sys_classfuncs |
|---|---|---|
| cl_init | sys_init() | |
| cl_funcs | | |
| cl_lock | | |
| cl_count | | |
| cl_size | | |
| cl_name | "TS" | ts_classfuncs |
| cl_init | ts_init() | |
| cl_funcs | | |
| cl_lock | | |
| cl_count | | |
| cl_size | | |
| cl_name | "IA" | ia_classfuncs |
| cl_init | ia_init() | |
| cl_funcs | rt_classfuncs | |
| cl_lock | | |
| cl_count | | |
| cl_size | | |
| cl_name | "RT" | rt_init() | |
| cl_init | | |
| cl_funcs | | |
| cl_lock | | |
| cl_count | | |
| cl_size | | |
| t_clfuncs | t_clfuncs | t_clfuncs | t_clfuncs | | | |
| t_clidata | t_clidata | t_clidata | t_clidata | | | |
| rt_pquantum | rt_pquantum | ts_timeleft | ts_timeleft | ts_timeleft |
| rt_timeleft | rt_timeleft | ts_diswait | ts_diswait | ts_diswait |
| rt_pri | rt_pri | ts_cpuprn | ts_cpuprn | ts_cpuprn |
| rt_flags | rt_flags | ts_uprlim | ts_uprlim | ts_uprlim |
| rt_tp | rt_tp | ts_nice | ts_nice | ts_nice |
| rt_pstatp | rt_pstatp | ts_boost | ts_boost | ts_boost |
| rt_rip | rt_pprip | ts_flags | ts_flags | ts_flags |
| rt_pffago | rt_pffago | ts_tp | ts_tp | ts_tp |
| rt_next | rt_next | ts_next | ts_next | ts_next |
| rt_prev | rt_prev | ts_prev | ts_prev | ts_prev |
| struct rtsproc | struct rtsproc | struct tssproc | | struct tssproc |

## RT 类线程

TS/IA 类线程

> 图 9.3 调度类数据结构

### 9.1.2 调度表

除了 `SYS` 类外，每个调度类加载时都会加载相应的调度表，包含优先级和优先级调整的默认值；在 `SYS` 类中，优先级定义在一个简单的数组和中断，这并不是真正的调度类。你可以通过以下命令检查并修改调度表：

```
# dispadmin -g TS
```

#### 分享调度调度器配置

`RES=1000`

| ts_quantum | ts_tqexp | ts_slpret | ts_maxwait | ts_lwisat | 优先级级别 |
|---|---|---|---|---|---|
| 200 | 0 | 50 | 0 | 50 | #0 |
| 200 | 0 | 50 | 0 | 50 | #1 |
| 40 | 48 | 58 | 0 | 59 | #58 |
| 20 | 49 | 59 | 32000 | 59 | #59 |

表 9-2 显示了选定的分时/交互组的默认值。为了空间和可读性，我们没有列出所有 60 个（0–59）优先级，因为此讨论只需要一个代表性样本。

#### 表 9-2 分享调度和交互调度表

| RES | ts_globpri | ts_quantum | ts_tqexp | ts_slpret | ts_maxwait | ts_lwait | PRI |
|---|---|---|---|---|---|---|---|
| 1000 | 0 | 200 | 0 | 50 | 0 | 50 | 0 |
| 5 | 200 | 0 | 50 | 0 | 50 | 5 |
| 10 | 160 | 0 | 51 | 0 | 51 | 10 |
| 11 | 160 | 1 | 51 | 0 | 51 | 15 |
| 15 | 160 | 5 | 51 | 0 | 51 | 20 |
| 20 | 120 | 10 | 52 | 0 | 52 | 25 |
| 25 | 120 | 15 | 52 | 0 | 52 | 30 |
| 30 | 80 | 20 | 53 | 0 | 53 | 35 |
| 35 | 80 | 25 | 54 | 0 | 54 | 40 |
| 40 | 40 | 30 | 55 | 0 | 55 | 45 |
| 45 | 40 | 35 | 56 | 0 | 56 | 45 |
| 50 | 40 | 40 | 58 | 0 | 59 | 50 |
| 55 | 40 | 45 | 58 | 0 | 59 | 55 |
| 59 | 20 | 49 | 59 | 32000 | 59 | 59 |

TS/IA 调度表中的每个项都由 `tsdpent`（分享项）结构定义，如下：

```c
/* 分享调度表项 */
struct tsdpent {
    int ts_globpri;    /* 全局（类无关）优先级 */
    int ts_quantum;    /* 给此级别进程的时间片 */
    short ts_tqexp;    /* 此级别进程分配的新优先级 */
    short ts_slpret;   /* 此级别分配的睡眠优先级 */
    short ts_maxwait;  /* 如果超过 ts_maxwait，增加到 ts_lwait */
    short ts_lwait;    /* 如果满足 ts_maxwait，在接收完整时间片前的服务 */
};
```

#### 头文件 <sys/ts.h>

`RES` 和 `PRI` 未在调度中定义。这些字段以及结构中定义的成员描述如下：

- `RES`（分辨率值）解释调度表中的 `ts_quantum` 列。`RES` 的倒数决定了 `ts_quantum` 字段的的粒度。随着 `RES` 值的增加，`ts_quantum` 列的值按相同的数量增加。更多信息请参见 `ts_quantum`。
- `PRI` 类相关优先级，系统全局优先级。`PRI` 列定义为调度表中的行数。调度表与其他表一样具有行和列。每一行对应调度类内的一个唯一优先级级别，每一列包含运行在该优先级上的线程的优先级调整值。这与 `ts_globpri` 不同。
- `ts_globpri` 是 `dispadmin(1)` 命令输出未显示的唯一表参数（`tsdpent` 结构成员），也是唯一不可调优的值，`ts_globpri` 是对应分时优先级（最右列）的类无关全局优先级。

Solaris 内的调度类具有优先级范围，0 表示该类的最低优先级。`TS` 和 `IA` 类有 60 个优先级，0–59。内核实现了一种全局优先级方案，每个调度类中的每个优先级级别都可以用整数值唯一标识。请参考第 354 页的图 9.2 获取所有组合调度类加载时的全局优先级列表。

由于 `TS/IA` 是最低类，内核全局优先级 0–59 对应 `TS/IA` 类优先级 0–59。内核在启动时计算全局优先级，如果在运行系统中加载了新类，则将重新计算。例如，再次参考图 9.2，如果没有加载 `RT` 类，中断线程的全局优先级将为 100–109，高于系统 (`SYS`)。如果加载了 `RT` 类，`RT` 的全局优先级将变为 100–159，中断将提升到 160–169。`ts_globpri` 是设置和调整优先级时，分时内核线程的 `t_pri` 字段。
