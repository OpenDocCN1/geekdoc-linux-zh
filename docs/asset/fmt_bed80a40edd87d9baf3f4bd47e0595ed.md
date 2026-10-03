
```c
liftoperatorsswitchbase_data,
liftoperatorswitchtop_data,
snowatervalve1_data,
snowatervalve2_data,
snowatervalve3_data,
snowheater1_data;

static struct proc_dir_entry *tb_dir,
    *liftacmains_file,
    *liftmotorcontroller_file,
    *liftslowpeed_file,
    *lifighspeed_file,
    *liftoperatorsswitchbase_file,
    *liftoperatorswitchtop_file,
    *snowatervalve1_file,
    *snowatervalve2_file,
    *snowatervalve3_file,
    *snowheater1_file;

/* proc_read - proc_read_liftmon
 * proc_read_liftmon 是内核对这些 /proc/trailblazer 文件进行读取操作时调用的回调函数
 * liftacmains, liftighspeed, liftmotorcontroller, liftoperatorsswitchbase
 * liftoperatorswitchtop, 和 liftslowpeed。文件指针通过 data 参数传递。
 * 你首先将其转换为 liftmon_snowcon_data_t 结构。
 * 从 io_base 读取 AC 输入状态。结果与位掩码相加
 * 以确定特定的模块是开启还是关闭。
 * 特定的模块是由读取的 /proc/trailblazer/ 文件定义的。
 */
static int proc_read_liftmon(char *page, char **start, off_t off, int count, void *data)
{
    unsigned int v;
    struct liftmon_snowcon_data_t *liftmon_snowcon_data =
        (struct liftmon_snowcon_data_t *)data;

    v = readb(io_base);

/* 根据掩码屏蔽输入值。每个掩码取决于读取了哪个 /proc/trailblazer 文件。
 * 注意：因为 AC 电到输入模块输出低电平，
 * 输入缓冲区不需要反转。 */
    if (v & liftmon_snowcon_data->mask)
        page[0] = '0';
    else
        page[0] = '1';

/* 返回长度 */
    return 1;
}

/* proc_write - proc_write_snowcondata
 * proc_write_snowcondata 是内核对这些 /proc/trailblazer 文件进行写入操作时调用的回调函数
 * snowheater1, snowwater1, snowwatervalve2 和 snowwater3。
 * 文件指针通过 data 参数传递。
 * 你首先将其转换为 liftmon_snowcon_data_t 结构。
 * buffer 参数指向传入的数据。
 * 如果传入的数据是 1 或 0，snowcondata 中的一个位将被设置或清除。
 * 然后将 snowcondata 写入输出锁存器。 */
static int proc_write_snowcondata(struct file *file, const char *buffer,
    unsigned long count, void *data)
{
    struct liftmon_snowcon_data_t *liftmon_snowcon_data =
        (struct liftmon_snowcon_data_t *)data;

/* 检查用户是否在 /proc/trailblazer 文件写入了 1 或 0。
 * 如果是，设置或清除 snowcondata 中的一个位 */
    if (buffer[0] == '0')
        snowcondata |= liftmon_snowcon_data->mask;

    if (buffer[0] == '1')
        snowcondata &= ~liftmon_snowcon_data->mask;

    writeb(snowcondata, io_base + 1);
    return 1;
}
```

## 列表 9.4 继续

```c
/* proc_read - proc_read_snowcondata
 * proc_read_snowcondata 是内核对这些 /proc/trailblazer 文件进行读取操作时调用的回调函数
 * snowheater1, snowwatervalve1, snowwatervalve2 和 snowwatervalve3。
 * 文件指针通过 data 参数传递。
 * 你首先将其转换为 liftman_snowcon_data_t 结构。
 * 使用 snowcondata 和位掩码来确定特定的输出模块是开启还是关闭。
 * 特定的输出模块是由读取的 /proc/trailblazer/ 文件定义的。 */
static int proc_read_snowcondata(char *page, char **pp, off_t off,
    int count, int *eof, void *data)
{
    struct liftman_snowcon_data_t *liftman_snowcon_data =
        (struct liftman_snowcon_data_t) *data;

/* 根据掩码屏蔽 snowcondata 值。每个掩码取决于读取了哪个 /proc/trailblazer 文件。 */
    if (snowcondata & liftman_snowcon_data->mask)
        page[0] = '0';
    else
        page[0] = '1';

/* 返回长度 */
    return 1;
}
```

```c
/* init - init_liftman_snowcon
 * init_liftman_snowcon 创建 /proc 条目并获取它们的指针。
 * 对于每个文件，将填充字段、data、read_proc、
 * write_proc 和所有者。
 * 随后配置 I/O 控制器，使输出和内存控制器能与 /proc 工作。
 * 它首先通过 printk 向系统写入条目，
 * 然后将输出模块初始化为关闭状态。 */
static int init_liftman_snowcon(void)
{
    int rv = 0;

/* 创建 trailblazer /proc 条目 */
    tb_dir = proc_mkdir("trailblazer", NULL);
    if (tb_dir == NULL) {
        rv = -ENOMEM;
    }
    tb_dir->owner = THIS_MODULE;

/* 创建 liftmains 并允许所有人读取 - 0444 */
    liftmains_file = create_proc_entry("liftmains", 0444, tb_dir);
    if (liftmains_file == NULL) {
        rv = -ENOMEM;
    }
    liftmains_data_mask = LIFTMINS;
    liftmains_file->data = &liftmains_data;
    liftmains_file->read_proc = &proc_read_liftmon;
    liftmains_file->write_proc = NULL;
    liftmains_file->owner = THIS_MODULE;

/* 创建 liftmotorcontroller 并允许所有人读取 - 0444 */
    liftmotorcontroller_file = create_proc_entry("liftmotorcontroller", 0444, tb_dir);
    if (liftmotorcontroller_file == NULL) {
        rv = -ENOMEM;
    }
    liftmotorcontroller_data_mask = LIFTMCONT;
    liftmotorcontroller_file->data = &liftmotorcontroller_data;
    liftmotorcontroller_file->read_proc = &proc_read_liftmon;
    liftmotorcontroller_file->write_proc = NULL;
    liftmotorcontroller_file->owner = THIS_MODULE;

/* 创建 liftslowpeed 并允许所有人读取 - 0444 */
    liftslowpeed_file = create_proc_entry("liftslowpeed", 0444, tb_dir);
    if (liftslowpeed_file == NULL) {
        rv = -ENOMEM;
    }
    liftslowpeed_data_mask = LIFTSLOWPEED;
    liftslowpeed_file->data = &liftslowpeed_data;
    liftslowpeed_file->read_proc = &proc_read_liftmon;
    liftslowpeed_file->write_proc = NULL;
    liftslowpeed_file->owner = THIS_MODULE;

/* 创建 lifighspeed 并允许所有人读取 - 0444 */
    lifighspeed_file = create_proc_entry("lifighspeed", 0444, tb_dir);
    if (lifighspeed_file == NULL) {
        rv = -ENOMEM;
    }
    lifighspeed_data_mask = LIFIGHSPEED;
    lifighspeed_file->data = &lifighspeed_data;
    lifighspeed_file->read_proc = &proc_read_liftmon;
    lifighspeed_file->write_proc = NULL;
    lifighspeed_file->owner = THIS_MODULE;

/* 创建 liftoperatorsswitchbase 并允许所有人读取 - 0444 */
    liftoperatorsswitchbase_file = create_proc_entry("liftoperatorsswitchbase", 0444, tb_dir);
    if (liftoperatorsswitchbase_file == NULL) {
        rv = -ENOMEM;
    }
    liftoperatorsswitchbase_data_mask = LIFOPERATORSBASE;
    liftoperatorsswitchbase_file->data = &liftoperatorsswitchbase_data;
    liftoperatorsswitchbase_file->read_proc = &proc_read_liftmon;
    liftoperatorsswitchbase_file->write_proc = NULL;
    liftoperatorsswitchbase_file->owner = THIS_MODULE;

/* 创建 liftoperatorswitchtop 并允许所有人读取 - 0444 */
    liftoperatorswitchtop_file = create_proc_entry("liftoperatorswitchtop", 0444, tb_dir);
    if (liftoperatorswitchtop_file == NULL) {
        rv = -ENOMEM;
    }
    liftoperatorswitchtop_data_mask = LIFOPERATORSSWITCHTOP;
    liftoperatorswitchtop_file->data = &liftoperatorswitchtop_data;
    liftoperatorswitchtop_file->read_proc = &proc_read_liftmon;
    liftoperatorswitchtop_file->write_proc = NULL;
    liftoperatorswitchtop_file->owner = THIS_MODULE;

/* 创建 snowatervalve1 并允许所有人读、写 - 0444 */
    snowatervalve1_file = create_proc_entry("snowatervalve1", 0444, tb_dir);
    if (snowatervalve1_file == NULL) {
        rv = -ENOMEM;
    }
    snowatervalve1_data_mask = SNOWWATERVALVE1;
    snowatervalve1_file->data = &snowatervalve1_data;
    snowatervalve1_file->read_proc = &proc_read_snowcondata;
    snowatervalve1_file->write_proc = &proc_write_snowcondata;
    snowatervalve1_file->owner = THIS_MODULE;

/* 创建 snowatervalve2 并允许所有人读、写 - 0444 */
    snowatervalve2_file = create_proc_entry("snowatervalve2", 0444, tb_dir);
    if (snowatervalve2_file == NULL) {
        rv = -ENOMEM;
    }
    snowatervalve2_data_mask = SNOWWATERVALVE2;
    snowatervalve2_file->data = &snowatervalve2_data;
    snowatervalve2_file->read_proc = &proc_read_snowcondata;
    snowatervalve2_file->write_proc = &proc_write_snowcondata;
    snowatervalve2_file->owner = THIS_MODULE;

/* 创建 snowatervalve3 并允许所有人读、写 - 0444 */
    snowatervalve3_file = create_proc_entry("snowatervalve3", 0444, tb_dir);
    if (snowatervalve3_file == NULL) {
        rv = -ENOMEM;
    }
    snowatervalve3_data_mask = SNOWWATERVALVE3;
    snowatervalve3_file->data = &snowatervalve3_data;
    snowatervalve3_file->read_proc = &proc_read_snowcondata;
    snowatervalve3_file->write_proc = &proc_write_snowcondata;
    snowatervalve3_file->owner = THIS_MODULE;

/* 创建 snowheater1 并允许所有人读、写 - 0444 */
    snowheater1_file = create_proc_entry("snowheater1", 0444, tb_dir);
    if (snowheater1_file == NULL) {
        rv = -ENOMEM;
        goto no_snowheater1;
    }

    snowheater1_data.mask = SNOWHEATER1;
    snowheater1_file->data = &snowheater1_data;
    snowheater1_file->read_proc = &proc_read_snowcondata;
    snowheater1_file->write_proc = &proc_write_snowcondata;
    snowheater1_file->owner = THIS_MODULE;
}
```
