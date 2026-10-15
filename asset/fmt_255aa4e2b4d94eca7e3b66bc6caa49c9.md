
```c
/* proc_read_racetime
 * 此函数返回当前或上一次比赛时间。
 * do_gettimeofday 用当前的秒和微秒填充时间。
 * 这样划分时间需要一些数学计算，因为
 * 微秒值是一个整数（321423 而不是 .321423）。
 * 如果微秒差需要从秒值进位
 */
static int proc_read_racetime(char *page, char **start, off_t off,
    int count, int *eof, void *data)
{
    int len;
    long raceconds, raceuses;
    struct timeval currenttime;

    switch (state) {
    case STATE_Ready:
        raceconds = 0;
        raceuses = 0;
        break;
    case STATE_Set:
        raceconds = 0;
        raceuses = 0;
        break;
    case STATE_Timing: /* 我们正在比赛，提供比赛时间 */
        do_gettimeofday(&currenttime);
        raceconds = currenttime.tv_sec - starttime.tv_sec;
        raceuses = currenttime.tv_use - starttime.tv_use;
        break;
    case STATE_Done: /* 比赛结束，提供比赛时间 */
        raceconds = finishtime.tv_sec - starttime.tv_sec;
        raceuses = finishtime.tv_use - starttime.tv_use;
        break;
    }

    /* 这里需要一些处理，因为 tv_sec 和 tv_use 是独立的 long 类型 */
    if (raceuses < 0) {
        raceuses += 1000000;
        raceconds--;
    }

    len = sprintf(page, "%ld.%06ld\n", raceconds, raceuses);
    return len;
}

static int __init_racetimer(void)
{
    int rv = 0;

    /* 创建 trailblazer 目录 */
    tb_dir = proc_mkdir("trailblazer", NULL);
    if(tb_dir == NULL) {
        return -ENOMEM;
    }
    tb_dir->owner = THIS_MODULE;

    /* 创建 racer 文件 */
    racer_file = create_proc_entry("racer", 0666, tb_dir);
    if(racer_file == NULL) {
        rv = -ENOMEM;
        goto no_racer;
    }
    racer_file->data = NULL;
    racer_file->read_proc = &proc_read_racer;
    racer_file->write_proc = &proc_write_racer;
    racer_file->owner = THIS_MODULE;

    /* 创建 racestatus 文件 */
    racestatus_file = create_proc_entry("racestatus", 0444, tb_dir);
    if(racestatus_file == NULL) {
        rv = -ENOMEM;
        goto no_racestatus;
    }
    racestatus_file->data = NULL;
    racestatus_file->read_proc = &proc_read_racestatus;
    racestatus_file->write_proc = NULL;
    racestatus_file->owner = THIS_MODULE;

    /* 创建 racetime 文件 */
    racetime_file = create_proc_entry("racetime", 0444, tb_dir);
    if(racetime_file == NULL) {
        rv = -ENOMEM;
        goto no_racetime;
    }
    racetime_file->data = NULL;
    racetime_file->read_proc = &proc_read_racetime;
    racetime_file->write_proc = NULL;
    racetime_file->owner = THIS_MODULE;

    return rv;
}

no_racetime:
    // cleanup
no_racestatus:
    // cleanup
no_racer:
    // cleanup

/* 请求中断，SA_INTERRUPT 用于禁用其他中断
 * 在我们运行时
 */

## 列表 11.4 续

```c
rv = request_irq(INTERRUPT, racetimer_interrupt, SA_INTERRUPT,
    "racetimer", NULL);
if (rv) {
    printk("Can't get interrupt %d\n", INTERRUPT);
    goto no_interrupt;
}
```

```c
/* 初始化状态定时器但不要用 add_timer 启动，
 * 让别人来做 */
init_timer(&status_timer);
status_timer.function = status_timer_timed_out;
status_timer.data = (unsigned long)&status;
```

```c
/* 启用并行端口中断报告 */
outb(SPINTERRUPTABLE, SPPCONTROLPORT);
/* 一正常 */
printk(KERN_INFO "%s %s initialized\n", MODULE_NAME, MODULE_VERSION);
return 0;
```

```c
/* 如果过程中发生错误，清理 /proc 目录 */
no_interrupt:
    remove_proc_entry("racetimer", tb_dir);
no_racetime:
    remove_proc_entry("racestatus", tb_dir);
no_racestatus:
    remove_proc_entry("racer", tb_dir);
no_racer:
    remove_proc_entry("trailblazer", NULL);
}
```

```c
static void __exit_cleanup_racetimer(void)
{
    /* 关闭状态 LED */
    outb(0x00, SPPDATAPORT);
}
```

```c
/* 定时器 */
/* 注意，如果模块被移除而定时器留在
 * 内核定时列表中，内核在执行
 * 定时处理程序时会发生（因为处理程序已不存在，你
 * 从内存中删除了它）。强制将状态设置为 done。然后
 * 使用 del_timer_sync，它会在定义定时器之前等待
 * 定时执行完成。强制将状态设置为 done 会告诉
 * 定时处理程序 status_timer_timed_out 不要重新调度定时器。
 */

state = STATE_Done;
del_timer_sync(&status_timer);
```

```c
/* 禁用并行端口中断报告 */
outb(0x00, SPPCONTROLPORT);
```

```c
/* 释放中断 */
free_irq(INTERRUPT, NULL);
```

```c
/* 移除 /proc 条目 */
remove_proc_entry("racetime", tb_dir);
remove_proc_entry("racestatus", tb_dir);
remove_proc_entry("racer", tb_dir);
remove_proc_entry("trailblazer", NULL);
```

```c
printk(KERN_INFO, "%s % removed\n", MODULE_NAME, MODULE_VERSION);
}
```

```c
module_init(init_racetime);
module_exit(cleanup_racetime);
```

```c
MODULE_AUTHOR("Craig Hollabaugh");
MODULE_DESCRIPTION("racetime proc module");
```

```c
EXPORT_NO_SYMBOLS;
```

你可以通过使用 `tbdev1` 下载、编译并测试 `racetime_x86` 设备。按照以下步骤操作：

1. 使用 `wget` 下载 `tbdev1[509]`: `racetime_x86.c` 源码：

```bash
root@tbdev1[509]: cd /root
root@tbdev1[510]: wget http://www.embeddedlinuxinterfacing.com/chapters/11/racetime_x86.c
```

2. 使用 `gcc` 编译源代码：

```bash
root@tbdev1[511]: gcc -O2 -D__KERNEL__ -DMODULE -I/usr/src/linux/include -c racetimer_x86.o -o racetimer_x86.o
```

3. 使用 `insmod` 插入设备驱动：

```bash
root@tbdev1[512]: insmod racetimer_x86.o
```

4. 使用这些命令查找中断 7 上的注册和 `/proc` 目录条目：

```bash
root@tbdev1[513]: cat /proc/interrupts
```

```text
CPU0
0: 816359      XT-PIC timer
1: 2195         XT-PIC keyboard
2: 0             XT-PIC cascade
4: 6016          XT-PIC serial
7: 0             XT-PIC racetimer
10: 23132        XT-PIC usb-uhci
12: 314011       XT-PIC eth0
14: 54205        XT-PIC ide0
15: 8457         XT-PIC ide1
NMI: 0
ERR: 0
```

```bash
root@tbdev1[514]: ls /proc/trailblazer/
racer racestatus racetimer
```

竞计时定时器注册在中断 7 上，`/proc/trailblazer` 目录包含竞计时定时器文件。

5. 检查竞计时定时器状态的内部状态：

```bash
root@tbdev1[515]: cat /proc/trailblazer/racestatus
R
```

输出 `R` 表示定时器处于就绪状态。

6. 使用此命令模拟赛手进入起跑门来启动赛手：

```bash
root@tbdev1[516]: echo -n "1" > /proc/trailblazer/racer
```

## 扩展阅读

1. Intel, SA-I110 Microprocessor Developer's Manual, www.intel.com/design/strong/manuals/27824.htm.
2. Motorola, MPC860 User Manual, www.motorola.com/brdata/PDFDB/docs/MPC860UM.pdf.

## 系统集成

随着 Project Trailblazer 所有现场硬件接口的开发和测试完成，工程师们已经准备好集成一切了。换句话说，他们已准备好应对系统集成。他们在 bash 提示符下开发并测试了 Project Trailblazer 的各个组件。在最终设计中，这些板卡将不会独立运行。输入设备（如电梯监控设备）将收集信息并存储在其他处。输出设备将根据提供它们的信息控制硬件。例如，温度显示器将从数据库获取要显示的值。信息将通过 Silverjack 网络在现场设备和数据库之间传输。

Project Trailblazer 的系统集成需要在两个领域进行：现场设备和 Silverjack 服务器。工程师们需要将现场硬件连接到数据库。在本章，你将看到工程师们如何使用 bash、Apache HTTP 服务器、MySQL 数据库、`grep` 以及名为 `netcat` 的网络连接实用程序来开发 Project Trailblazer 系统集成。

### 集成概述

集成任务是将数据传输到服务器数据库，然后将这些数据分发回现场和 Web 端。尽管 Project Trailblazer 有许多现场设备，但往返的数据量仅消耗几个字节。存在多种网络通信协议可以将现场设备连接到 Silverjack 数据库。每种协议提供不同的功能、复杂性以及目标板文件系统的使用方式。工程师们决定让 Project Trailblazer 系统集成尽可能简单。他们的方法是在目标板和服务器上的任何地方都使用 bash 脚本。图 12.1 显示了 Project Trailblazer 系统成的软件框图。

### 本章内容

- 集成概述
- 安装系统集成应用
- 创建并测试 Project Trailblazer 数据库
- 开发目标板和 CGI 集成脚本
- 扩展阅读

### 提示

框图显示了系统主要组件、接口和连接的高级表示。它为系统提供了整体视图。

![](img/6d9baeee8ddb96b5248c3d68b6bc0ecb_380_0.png)

图 12.1 目标板和 Silverjack 服务器软件组件。

工程师的方法包括以下组件：

- bash 脚本用于现场设备控制和 Web 服务器通用网关接口 (CGI)。
- 现场设备与运营部门之间的通信使用超文本传输协议 (HTTP)。
- `nc` 程序为 bash 脚本提供网络通信。
- MySQL 数据库存储所有现场数据，图像则存储为服务器上的文件。
- `ggplot` 程序根据需要生成任何所需的数据表。
- Apache HTTP 服务器将数据分发到现场设备和 Web 端。

本章的剩余部分描述了 Project Trailblazer 工程师如何配置 `tbdev` 作为 Silverjack 服务器，并为 Project Trailblazer 提供系统集成功能。本章专注于 Project Trailblazer 的三个系统：

### 安装系统集成应用

- 温度采集与分发
- 图像采集与分发
- 客人电梯访问

这三个系统的实现为所有其他 Project Trailblazer 系统提供了集成基础。

## 安装系统集成应用

工程师需要在 `tbdev1` 上安装以下应用：MySQL、Apache 和 `gnplot`。`nc` 程序运行在目标板上。因此，工程师们需要交叉编译 ARM 和 PowerPC 版本的 `nc`。这些步骤对于安装系统集成应用和交叉编译 `nc` 是必要的：

1. 登录 root 并使用此命令安装 MySQL：

```bash
root@tbdev1[504]: apt-get install mysql-server
```

阅读安全和更新通知并点击 OK。当询问是否删除所有 `/var/lib/mysql` 时，点击 No。

2. 使用 `mysql` 客户端程序进行 MySQL 服务器安装：

```bash
root@tbdev1[505]: mysql
Welcome to the MySQL monitor. Commands end with; or \g.
Your MySQL connection id is 2 to server version: 3.22.32-log
Type 'help' for help.
mysql> show databases;
```

```text
+--------------------+
| Database           |
| mysql               |
| test               |
+--------------------+
2 rows in set (0.00 sec)
```

```bash
mysql> quit
Bye
```
