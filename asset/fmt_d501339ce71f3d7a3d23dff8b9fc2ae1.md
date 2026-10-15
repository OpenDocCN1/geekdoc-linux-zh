
`cl_name` --"SYS"--> `sys_init()`

`cl_init`

`cl_funcs`

`cl_lock`

`cl_count`

`cl_size`

`cl_name` --"TS"--> `ts_classfuncs`

`cl_init`

`cl_funcs`

`cl_lock`

`cl_count`

`cl_size`

`cl_name` --"IA"--> `ia_classfuncs`

`cl_init`

`cl_funcs`

`cl_lock`

`cl_count`

`cl_size`

`cl_name` --"RT"--> `rt_classfuncs`

`cl_init`

`cl_funcs`

`cl_lock`

`cl_count`

`cl_size`

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

`struct rtproct` `struct rtproct` `struct tsproct` `struct tsproct` `struct tsproct`

RT 类线程 IA 类线程

图 9.3 调度类数据结构

### 9.1.2 调度表

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
