
### 各种队列指针和地址
```
0 0 4 0 * work_Q
4 0 4 0 * lv_ready_Q.lv_head
8 0 4 0 * lv_ready_Q.lv_tail
12 0 4 0 int lv_ready_Q.lv_count
```
### 逻辑扩展数组指针（用于重新同步操作期间）
```
16 0 4 0 * lv_lext
```
### 用于映射镜像扩展的三个物理扩展指针映射
```
20 0 4 0 * lv_exts[0]
24 0 4 0 * lv_exts[1]
28 0 4 0 * lv_exts[2]
```
### 指向计划队列、条带数量及条带大小的指针
```
32 0 4 0 * lv_schedule
36 0 2 0 u_short lv_stripes
38 0 2 0 u_short lv_stripesize
```
### 一组锁指针和原语
```
40 0 4 0 * lv_lock.interlock
44 0 4 0 u_int lv_lock.delay
48 0 4 0 int lv_lock.read_count
52 0 1 0 char lv_lock.want_write
53 0 1 0 char lv_lock.want_upgrade
54 0 1 0 char lv_lock.waiting
55 0 1 0 char lv_lock.no_swap
56 0 4 0 * lv_intlock.lvc_slock
60 0 4 0 int lv_complcnt
```
### 累计请求数、挂起请求数和当前状态标志
```
64 0 4 0 int lv_totalcount
68 0 4 0 int lv_requestcount
```
```
72 0 2 0 u_short lv_status 
74 0 2 0 u_short lv_allow_cfgcmd_rslvr 
76 0 2 0 u_short lv_ref 
78 0 2 0 u_short lv_rawavoid 
80 0 2 0 u_short lv_rawoptions
```

`lvol` 的物理扩展数量、逻辑扩展最大数量以及正在使用的逻辑扩展数量
```
84 0 4 0 u_int lv_curpxs 
88 0 2 0 u_short lv_maxlxs 
90 0 2 0 u_short lv_curlxs 
92 0 2 0 u_short lv_flags
```

- `LVM_RESERVED` 组文件 `lvol0` 策略
- `LVM_SEQUENTIAL` 顺序调度标志
- `LVM_PARALLEL` 并行调度标志
- `LVM_STRIPE` 启用条带化
- `LVM_DYNAMIC` 动态调度（当前未使用）
- `LVM_STRIPE_NEW` 新条带（当前未使用）

### 当前调度策略、镜像数量以及指向逻辑卷位分配图的指针
```
94 0 1 0 u_char lv_sched_strat 
95 0 1 0 u_char lv_maxmirrors 
96 0 4 0 * lv_bitmap 
100 0 2 0 u_short lv_partner 
102 0 2 0 u_short lv_mimwhit 
104 0 2 0 u_short lv_mimwcmiss 
108 0 4 0 u_int lv_mirxfers 
112 0 4 0 u_int lv_mircount 
116 0 4 0 u_int lv_mirwxfers 
120 0 4 0 u_int lv_mirwcount 
124 0 4 0 * lv_vg
```

字节偏移 `128` 至 `511` 包含原始缓冲区数据。

字节偏移 `512` 至 `895` 包含逻辑卷磁盘排序信息。

### 请求超时的秒数
```
896 0 4 0 u_int lv_io_timeout
```

## 列表 11.12 q4> 字段结构 pvol

### 指向卷组结构、lvmrec 结构以及此 pvol 的坏块目录的指针
```
0 0 4 0 * pv_vg 
4 0 4 0 * pv_lvmrec 
8 0 4 0 * pv_bbdbr
```

### 坏块目录中条目的最大数量和当前数量
```
12 0 4 0 u_int pv_maxdefects
16 0 4 0 u_int pv_curdefects
20 0 4 0 u_int pv_vgdates[0].tv_sec
24 0 4 0 long pv_vgdates[0].tv_usec
28 0 4 0 u_int pv_vgdates[1].tv_sec
32 0 4 0 long pv_vgdates[1].tv_usec
36 0 4 0 int pv_vgra_psn
40 0 4 0 int pv_data_psn
44 0 4 0 u_int pv_pxs
```

### pvol 的物理扩展总数和空闲扩展数量
```
48 0 2 0 u_short pv_pxcount
50 0 2 0 u_short pv_freepxs
52 0 4 0 * pv_intlock.lvc_slock
56 0 4 0 int pv_armpos
```

### 工作队列指针
```
60 0 4 0 * pv_ready_Q.lv_head
64 0 4 0 * pv_ready_Q.lv_tail
68 0 4 0 int pv_ready_Q.lv_count
```

### 到此 pvol 的累计传输次数、挂起请求数、状态标志以及 pvol 在其卷组中的索引号
```
72 0 4 0 int pv_totxrf
76 0 2 0 short pv_curxfs
78 0 2 0 u_short pv_flags
80 0 1 0 u_char pv_flags2
81 0 1 0 u_char pv_num
84 0 4 0 int pv_sa_psn[0]
88 0 4 0 int pv_sa_psn[1]
92 0 4 0 u_int pv_vgstats[0].tv_sec
96 0 4 0 long pv_vgstats[0].tv_usec
100 0 4 0 u_int pv_vgstats[1].tv_sec
104 0 4 0 long pv_vgstats[1].tv_usec
108 0 4 0 * pv_cache_wait.lv_head
112 0 4 0 * pv_cache_wait.lv_tail
116 0 4 0 int pv_cache_wait.lv_count
120 0 4 0 * pv_cache_next
124 0 4 0 * pvmwc_rec
128 0 4 0 u_int pv_mwc_latest.tv_sec
132 0 4 0 long pv_mwc_latest.tv_usec
140 0 4 0 int pv_mwc_flags
144 0 4 0 int pv_mwc_loc[0]
148 0 4 0 int pv_mwc_loc[1]
152 0 4 0 int altpool_pen
156 0 4 0 int altpool_next
160 0 4 0 int altpool_end
```

### 物理卷缺陷数组
```
160 0 4 0 * pv_defects[0]
-------------------------------------------------------
412 0 4 0 * pv_defects[63]
416 0 4 0 * freelist
420 0 4 0 * freelist_ptr
424 0 4 0 u_int freelistsize
428 0 4 0 u_int bbdresize
```

字节偏移 `432` 至 `523` 包含物理卷属性数据。

### vnode 和 pv-links 信息
```
524 0 4 0 * currentPhysicalLink
528 0 4 0 * pv_wait_Q.lv_head
532 0 4 0 * pv_wait_Q.lv_tail
536 0 4 0 int pv_wait_Q.lv_count
```

字节偏移 `540` 至 `927` 包含物理卷缓冲区数据。

### 读写请求的大小（1 kB 的倍数）
```
928 0 2 0 u_short pv_blkfactor
930 0 2 0 u_short sgio_flags
```

字节偏移 `934` 至 `1011` 包含物理卷备用信息。

现在，内核中已具备所有必要的配置数据，以允许从逻辑卷偏移量转换到物理卷偏移量。

## 单向和双向镜像机制及选项

镜像允许在 `LVM` 控制下对单个逻辑卷进行两个（单向）或三个（双向）镜像。镜像的基本前提非常直接，但幕后机制需要额外考量。

镜像操作的一个主要关注点是确保每个镜像副本具有相同的数据。这在请求写入时尤为关键。为确保数据在所有副本间保持一致，`LVM` 引入了 `MWC` 策略。当逻辑卷被配置为镜像时，可以配置使用三种镜像缓存策略之一。

- `NONE`：选择此策略将禁用所有内部一致性检查。激活时扩展不会被标记为过期，镜像也不会同步。这可能适用于交换卷。
