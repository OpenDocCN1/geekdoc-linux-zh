

class threads; 用于 SYS 和 RT 的内核函数返回无效操作。Solaris 中为了兼容性保留了 `nice(1)` 命令。线程优先级调整应通过 `priocntl(1)` 完成。

- **ts_globpri, rt_globpri** — 根据给定的用户模式优先级，返回分配给该线程的全局调度优先级。线程实际调度优先级的计算基于多个因素，包括用户优先级的概念。详情请参阅第 369 页的“线程优先级”（Thread Priorities）。

- **ia_set_process_group** — 为 IA 类线程建立与窗口会话关联进程组。

- **ts_yield, rt_yield** — 当线程让出（让出）处理器时，由 `yield(2)` 系统调用调用。内核线程被放在调度队列的末尾。

与调度类相关的结构如图 9.3 所示。图中显示了系统类数组，包含指向类操作向量数组、类名称和类特定初始化例程的指针。图中还显示了全系统内核线程链表的粗粒度视图，每个内核线程都链接到其自身的类特定数据结构。该结构维护了调度器用于管理 kthread 执行时间和调度的某些位信息；该结构还维护了一个指向类操作数组的指针。

## 系统类数组

```
cl_name --"SYS"--> sys_init()
cl_init
cl_funcs
cl_lock
cl_count
cl_size
cl_name --"TS"--> ts_classfuncs
cl_init
cl_funcs
cl_lock
cl_count
cl_size
cl_name --"IA"--> ia_classfuncs
cl_init
cl_funcs
cl_lock
cl_count
cl_size
cl_name --"RT"--> rt_classfuncs
cl_init
cl_funcs
cl_lock
cl_count
cl_size
```

![](img/a86367b95bf21add858c99948ac951c6_401_0.png)

全系统内核线程链表

| t_clfuncs | t_clfuncs | t_clfuncs | t_clfuncs | t_clfuncs |
|---|---|---|---|---|
| t_cldata | t_cldata | t_cldata | t_cldata | t_cldata |

| rt_pquantum | rt_pquantum | ts_timeleft | ts_timeleft | ts_timeleft |
|---|---|---|---|---|
| rt_timeleft | rt_timeleft | ts_dispwait | ts_dispwait | ts_dispwait |
| rt_pri | rt_pri | ts_cpuprti | ts_cpuprti | ts_cpuprti |
| rt_flags | rt_flags | ts_uplprim | ts_uplprim | ts_uplprim |
| rt_tp | rt_tp | ts_nice | ts_nice | ts_nice |
| rt_pstatlp | rt_pstatlp | ts_boost | ts_boost | ts_boost |
| _pprip | rt_pprip | ts_flags | ts_flags | ts_flags |
| rt_plagfp | rt_plagfp | ts_tp | ts_tp | ts_tp |
| rt_next | rt_next | ts_next | ts_next | ts_next |
| rt_prev | rt_prev | ts_prev | ts_prev | ts_prev |

struct rtproct struct rtproct struct tsproct struct tsproct struct tsproct

RT 类线程 IA 类线程

图 9.3 调度类数据结构

## 9.1.2 调度表

除了 SYS 类外，每个调度类加载时带有一个相应的调度表，包含优先级优先级重新调整的默认值；在 SYS 类中，优先级定义在一个简单的数组和中断中，这并不是一个真正的调度类。你可以使用 `disp_admin(1)` 命令检查并修改调度表，例如，`dispadmin -c TS -g` 将转储你 Solaris 系统上的当前时分 (TS) 类和交互 (IA) 类的调度表。（TS 和 IA 使用相同的调度表。）

```
# dispadmin -g -c TS
# 时分调度器配置
RES=100
# ts_quantum ts_tqexp ts_slpret ts_maxwait ts_lwait PRIORITY LEVEL
200 0 50 50 # 0
200 0 50 0 # 1

40 48 5 0 59 # 58
20 49 59 32000 # 59
```

表 9-2 显示了选定一组时分/交互优先级的默认值。为了空间和可读性，我们没有列出所有的 (00–59) 优先级，因为此讨论只需要一个代表性样本。

| RES | ts_globpri | ts_quantum | ts_tqexp | ts_slpret | ts_maxwait | ts_lwait | PRI |
|---|---|---|---|---|---|---|---|
| 1000 | 0 | 200 | 0 | 50 | 0 | 50 | 0 |
| 5 | | 200 | 0 | 50 | 0 | 50 | 5 |
| 10 | | 160 | 0 | 51 | 0 | 51 | 10 |
| 11 | | 160 | 1 | 51 | 0 | 51 | 11 |
| 15 | | 160 | 5 | 51 | 0 | 51 | 15 |
| 20 | | 120 | 10 | 52 | 0 | 52 | 20 |
| 25 | | 120 | 15 | 52 | 0 | 52 | 25 |
| 30 | | 80 | 20 | 53 | 0 | 53 | 30 |
| 35 | | 80 | 25 | 54 | 0 | 54 | 35 |
| 40 | | 40 | 30 | 55 | 0 | 55 | 40 |
| 45 | | 40 | 35 | 56 | 0 | 56 | 45 |
| 50 | | 40 | 40 | 58 | 0 | 59 | 50 |
| 55 | | 40 | 45 | 58 | 0 | 59 | 55 |
| 59 | | 20 | 49 | 59 | 32000 | 59 |

TS/IA 调度表中的每个项目（每行）由 `tsdpent` 结构（来自 `/usr/include/ts.h`）定义如下：

```
/* 时分调度器项目 */
struct tsdpent {
    pri_t ts_globpri;      /* 全局（类无关）优先级 */
    int   ts_quantum;      /* 给此级别进程的时间片 */
    pri_t ts_tqexp;       /* 进程睡眠时分配的优先级 */
    pri_t ts_slpret;      /* 睡眠后返回用户模式时 */
    short ts_maxwait;      /* 在接收完整时间片之前的时间 */
    short ts_lwait;       /* 如果超过 ts_maxwait 则 */
} tsdpent;
```

## 头文件 <ts.h>

RES 和 PRI 参数没有在 `tsdpent` 中定义。这些字段以及结构中定义的成员描述如下：

- **RES** — （分辨率值）解释调度表中的 `ts_quantum` 列。RES 的倒数决定了 `ts_quantum` 字段显示的粒度。随着 RES 值的增加，`ts_quantum` 列的值按相同的数量增加。更多信息请见 `ts_quantum`。

- **PRI** — 类相关的优先级，全系统优先级。PRI 列源自调度表中的行数。调度表类似于通用表格——具有行和列。每行对应调度类中的一个唯一优先级，每列包含确定在该优先级运行线程的优先级调整值。这与 `ts_globpri` 不同。

- **ts_globpri** — `dispadmin` 命令输出未显示的唯一参数 (tsdpent 成员)，也是唯一可调的值。`ts_globpri` 是对应于时分优先级的类无关全局优先级（最右侧）。Solaris 内的给定调度类优先级范围从0开始，代表该类的最低优先级。TS 和 IA 类有60个优先级，范围0–59。内核实现全局优先级方案，每个调度类中的每个优先级级别都可以用整数值唯一标识。参考第 348 页的图 9.2 所有调度类加载时的优先级列表。由于 TS/IA 是最低类，内核优先级 0–59 对应 TS/IA 类优先级 0–59。内核会计算全局优先级，并在新类加载到运行系统时必要时重新计算。例如，再次参考图 9.2，如果没有加载 RT 类，中断线程的全局优先级将是 100–109，仅高于系统 (SYS)。如果加载了 RT 类，RT 的全局优先级变为 100–159，中断被提升到 160。`ts_globpri` 是优先级设置和重新调整时内核线程的优先级。

- **ts_quantum** — 时间片；该线程在必须放弃处理器之前允许运行的时间。请注意 `ts_dptbl(4)` 手页以及其他引用指出，`ts_quantum` 字段中的值是刻（ticks）。刻 是一个随平台变化的时间单位。在基于 UltraSPARC 的系统上，每秒有100 刻，因此每10毫秒发生一次刻。只有当 RES 为 100 时，`ts_quantum` 中的值才为刻。如果 RES 是任何其他值（默认为 1000），则 `ts_quantum` 代表秒的某部分，该分数由 RES 的倒数决定。在默认 RES = 1000 的情况下，1000 的倒数是 .001，即毫秒。因此，默认情况下，`ts_quantum` 字段代表给定优先级的毫秒时间片。

从第357 页的表 9-2 可以看到，优先级0的内核线程获得200 毫秒（20 刻），优先级10的内核线程获得 160 毫秒，等。随着线程优先级的提高（全局优先级整数值越高），其时间片越短。较差（的）优先级获得更大的时间片，因为它们的调度频率较低。

