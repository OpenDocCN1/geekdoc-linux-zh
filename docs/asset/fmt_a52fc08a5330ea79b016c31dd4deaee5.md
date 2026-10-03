
#include <linux/proc_fs.h>
#include <linux/sched.h>
#include <asm/uaccess.h>

```c
#define MODULE_VERSION "1.0"
#define MODULE_NAME "liftman_snowcon"
```

# 使用自定义设备驱动 liftmon_snowcon 控制标准并行端口

## 列表 7.5 继续

```c
/* 标准并行端口 (SPP) 定义 */
#define SPDDATORT 0x378
#define SPPSTATUSPORT (SPDDATORT + 1)
#define SPPCONTROLPORT (SPDDATORT + 2)
```

```c
/* SPP 控制位定义 */
#define OUTPUTTPENABLE 0x02
#define OUTPUTLATCH 0x04
#define INPUTABLE 0x08
#define SPSPORTREAD 0x20
```

```c
/* SPP 输入位定义 */
#define LIFTACMAINS 0x01
#define LIFTMOTORROLLER 0x02
#define LIFTSLOWSPEED 0x04
#define LIFTHIGHSPEED 0x08
#define LIFTOATORSSWITCHBASE 0x10
#define LIFTOATORSWITCHHTOP 0x20
```

```c
/* SPP 输出位定义 */
#define SNOWWATERVALVE1 0x01
#define SNOWWATERVALVE2 0x02
#define SNOWWATERVALVE3 0x04
#define SNOWHEATER1 0x08
```

```c
/* 定义一个位掩，每个文件都使用此来确定身份 */
struct liftmon_snowcon_data {
    unsigned char mask;
}

/* snowcondata 是内部存储的锁存值。
 * 用户脚本写入 /proc/trailblazer 条目会导致
 * snowcondata 中的位被清除或设置。每当发生控制时，
 * 我们将 snowcondata 写入输出锁存器 */
unsigned char snowcondata;

/* 这些是持有掩码的数据结构。
 * 当 /proc 文件被读取或写入时，
 * read_proc 或 write_proc 接收指向此结构的指针 */
struct liftmon_snowcon_data
    liftacmains_data,
    liftmotorcontroller_data,
    liftslowpeed_data,
    lifthighspeed_data,
    liftoperatorswitchbase_data,
    liftoperatorswitchtop_data,
    snowwatervalve1_data,
    snowwatervalve2_data,
    snowwatervalve3_data,
    snowheater_data;
```

```c
/* 这些是指向 /proc 目录的指针 */
static struct proc_dir_entry *tb_dir,
    liftacmains_file,
    liftmotorcontroller_file,
    liftslowpeed_file,
    lifthighspeed_file,
    liftoperatorswitchbase_file,
    liftoperatorswitchtop_file,
    snowwatervalve1_file,
    snowwatervalve2_file,
    snowwatervalve3_file,
    snowheater_file;
```

```c
/* proc_read - proc_read_liftman
 * proc_read_liftman 是内核调用的回调函数，
 * 在 /proc/trailblazer 文件上执行读取操作：
 * liftcains, lifthighspeed, liftmotorcontroller, liftoperatorswitch
 * liftoperatorswitchtop 以及 liftslowpeed。
 * 文件数据指针通过 data 参数传递。
 * 输入模块的值是通过配置 SPP 数据输入
 * 并断言输入缓冲区读取的。
 * 使用 inb 读取位，然后与掩码值进行与操作，
 * 确定特定的输入模块是开启还是关闭。
 * 特定的输入模块是由读取的 /proc/trailblazer 定义的。 */
static int proc_read_liftman(char *page, char **start, off_t off, int count,
    int eof, void *data)
{
    unsigned char v;
```

# 使用自定义驱动 liftmon_snowcon 控制标准并行端口

## 列表 7.5 继续

```c
struct liftmon_snowata_data *liftmon_snowata_data =
    (struct liftmon_snowata_data*)data;

outb(OUTPUTABLE, SSPCONTROLPORT);
/* 此断言了三项：
 * 1. SSPPORTREAD，将双向数据端口配置为输入
 * 2. INPUTABLE，启用输入缓冲区驱动总线
 * 3. OUTPUTABLE，启用输出锁存器，驱动输出
 * 如果你不断言此项，输出模块将关闭 */
outb(SSPPORTREAD | INPUTABLE | OUTPUTABLE, SSPCONTROLPORT);

/* 输入缓冲区现在驱动总线，因此执行读取 */
v = inb(SPDAPDATA);

/* 取消断言 SPORTREAD 和 INPUTABLE。
 * 使用 OUTPUTABLE 保持输出锁存器启用 */
outb(OUTPUTABLE, SSPCONTROLPORT);

/* 根据掩码对输入值进行掩码处理。每个掩码取决于读取了哪个 /proc/trailblazer 文件。
 * 电路注意：返回反转的值，是因为给输入
 * 模块供电会输出低电，而输入缓冲区 74244 不反转 */
if (v & liftmon_snowcon_data->mask)
    page[0] = '0';
else
    page[0] = '1';

/* 返回 1，即 page 的长度 */
return 1;

/* proc_write - proc_write_snowcondata
 * proc_write_snowcondata 是内核调用的回调函数，
 * 在 /proc/trailblazer 文件上执行写入操作：
 * snowheater, snowwatervalve1, snowwatervalve2 和 snowwatervalve3。
 * 文件数据指针通过 data 参数传递。你首先
 * 将其转换为 liftmon_snowcon_data 。buffer 参数
```

# 第 7 章 并行端口接口

## 列表 7.5 继续

```c
* 指向传入的数据。如果传入的数据是 1 或 0，
* snowcondata 中的某个位会被设置或清除。
* 哪个位是由写入的哪个 /proc/trailblazer 文件定义的。
* snowcondata 被写入输出锁存器。 */
static int proc_write_snowcondata(struct file *file, const char *buffer,
    unsigned long count, void *data)
{
    struct liftmon_snowata_data *liftmon_snowata_data =
        (struct liftmon_snowata_data_t*)data);

    /* 检查用户是否向 /proc/trailblazer 文件写入了 1 或 0。
     * 如果是，则设置或清除 snowcondata 中的一个位 */
    if (buffer[0] == '1')
        snowcondata |= liftmon_snowata_data->mask;
    if (buffer[0] == '0')
        snowcondata &= -liftmon_snowata_data->mask;
```

```c
/* 使用 OUTPUTABLE 保持输出锁存器启用 */
outb(OUTPUTABLE, SSPCONTROLPORT);

/* 将 snowcondata 放入数据线 */
outb(snowcondata, SPPDATORT);

/* 断言 OUTPUTLATCH，将数据线锁存到输出模块架 */
outb(OUTPUTABLE | OUTPUTLATCH, SSPCONTROLPORT);

/* 使用 OUTPUTABLE 保持输出锁存器启用 */
outb(OUTPUTABLE, SSPCONTROLPORT);

return 1;
}
```

* proc_read - proc_read_snowcondata
* proc_read_snowcondata 是内核调用的回调函数，
* 在这些 /proc/trailblazer 文件上执行读取操作：
* snowheater, snowwatervalve1, snowwatervalve2 和 snowwatervalve3。
* 文件数据指针通过 data 参数传递。你首先

# 使用自定义设备驱动程序控制标准并行端口 liftmon_snowcon 195

## 列表 7.5 继续

```c
/* 将其转换为 liftmon_snowcon_data_t 结构体。使用带有位掩码的
 * snowcondata 结尾，来确定特定的输出
 * 模块是开启还是关闭状态。特定的输出模块定义取决于
 * 读取了哪一个 /proc/trailblazer/ 文件。 */
static int proc_read_snowcondata(char *page, char **off, off_t off,
    int count, int *eof, void *data)
{
    struct liftmon_snowcon_data_t *liftmon_snowcon_data =
        (struct liftmon_snowcon_data_t *)data;

    /* 根据掩码对 snowcondata 值进行掩码处理。每个掩码取决于
     * 取决了哪个 /proc/trailblazer 文件。 */
    if (snowcondata & liftmon_snowcon_data->mask)
        page[0] = '1';
    else
        page[0] = '0';

    /* 返回长度 */
    return length;
}

/* init _init_liftmon_snowcon
 * init_liftmon_snowcon 创建 /proc 条目文件并获取
 * 它们的指针。对于每个文件，字段、数据、read_proc、init_liftmon_snowcon
 * 将输出模块初始化为关闭状态，然后
 * 通过使用 printk 向系统日志写入条目来完成。 */
static int __init_init_liftmon_snowcon(void)
{
    int rv = 0;

    /* 创建 trailblazer /proc 条目 */
    tb_dir = proc_mkdir("trailblazer", NULL);
    if (tb_dir == NULL) {
        rv = -ENOMEM;
        goto out;
    }

    tb_dir->owner = THIS_MODULE;

    /* 创建 liftacmains 并允许所有人可读 - 0444 */
    liftacmains_file = create_proc_entry("liftacmains", 0444, tb_dir);
    if (liftacmains_file == NULL) {
        rv = -ENOMEM;
        goto no_liftacmains;
    }
    liftacmains_data.mask = LIFTACMAINS;
    liftacmains_file->data = &liftacmains_data;
    liftacmains_file->read_proc = &proc_read_liftmon;
    liftacmains_file->write_proc = NULL;
    liftacmains_file->owner = THIS_MODULE;

    /* 创建 liftmotorcontroller 并允许所有人可读 - 0444 */
    liftmotorcontroller_file = create_proc_entry("liftmotorcontroller", 0444, tb_dir);
    if (liftmotorcontroller_file == NULL) {
        rv = -ENOMEM;
        goto no_liftmotorcontroller;
    }
    liftmotorcontroller_data.mask = LIFTOMOTCONTROLLER;
    liftmotorcontroller_file->data = &liftmotorcontroller_data;
    liftmotorcontroller_file->read_proc = &proc_read_liftmon;
    liftmotorcontroller_file->write_proc = NULL;
    liftmotorcontroller_file->owner = THIS_MODULE;

    /* 创建 liftlowpeed 并允许所有人可读 - 0444 */
    liftlowpeed_file = create_proc_entry("liftlowpeed", 0444, tb_dir);
    if (liftlowpeed_file == NULL) {
        rv = -ENOMEM;
        goto no_liftlowpeed;
    }
    liftlowpeed_data.mask = LIFTLOWPEED;
    liftlowpeed_file->data = &liftlowpeed_data;
    liftlowpeed_file->read_proc = &proc_read_liftmon;
    liftlowpeed_file->write_proc = NULL;
    liftlowpeed_file->owner = THIS_MODULE;

    /* 创建 liftighspeed 并允许所有人可读 - 0444 */
    liftighspeed_file = create_proc_entry("liftighspeed", 0444, tb_dir);
    if (liftighspeed_file == NULL) {
        rv = -ENOMEM;
        goto no_liftmotorcontroller;
    }
    liftighspeed_data.mask = LIFTIGPEED;
    liftighspeed_file->data = &liftighspeed_data;
    liftighspeed_file->read_proc = &proc_read_liftmon;
    liftighspeed_file->write_proc = NULL;
    liftighspeed_file->owner = THIS_MODULE;

    /* 创建 liftatorspeed 并允许所有人可读 - 0444 */
    liftatorspeed_file = create_proc_entry("liftatorspeed", 0444, tb_dir);
    if (liftatorspeed_file == NULL) {
        rv = -ENOMEM;
        goto no_liftmotorcontroller;
    }
    liftatorspeed_data.mask = LIFTATORPEED;
    liftatorspeed_file->data = &liftatorspeed_data;
    liftatorspeed_file->read_proc = &proc_read_liftmon;
    liftatorspeed_file->write_proc = NULL;
    liftatorspeed_file->owner = THIS_MODULE;

    /* 创建 liftatorswitchbase 并允许所有人可读 - 0444 */
    liftatorswitchbase_file = create_proc_entry("liftatorswitchbase", 0444, tb_dir);
    if (liftatorswitchbase_file == NULL) {
        rv = -ENOMEM;
        goto no_liftmotorcontroller;
    }
    liftatorswitchbase_data.mask = LIFTATORSWITCHBASE;
    liftatorswitchbase_file->data = &liftatorswitchbase_data;
    liftatorswitchbase_file->read_proc = &proc_read_liftmon;
    liftatorswitchbase_file->write_proc = NULL;
    liftatorswitchbase_file->owner = THIS_MODULE;
```
