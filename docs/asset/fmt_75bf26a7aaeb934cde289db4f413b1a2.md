
```c
// 路径: fs/buffer.c
// NR_HASH 为 157，对于 dev:030, block:0，hashfn(dev_block) 的结果为 154
#define hashfn(dev_block) ((unsigned)dev->block & NR_HASH)
#define hash(dev_block) hash_table[hashfn(dev_block)]

// 在 buffer 中查找具有特定 dev 和 block 的 buffer
static struct buffer_head *find_buffer(int dev, int block)
{
	struct buffer_head *tmp;

	for (tmp = hash(dev, block); tmp != NULL; tmp = tmp->b_next)
		if (tmp->b_dev == dev && tmp->b_blocknr == block) {
		return tmp;
	}
	return NULL;
}
```

函数 `find_buffer()`、`get_hash_table()` 执行到 `getblk()` 函数，并在空闲形式中寻找一个新的空闲 buffer 块。所有的 buffer 块现在都绑定在可遍历的列表中，因此对于空闲表中的新块，如图 3.16 中的第二步所示。

代码如下：

```c
// 路径: fs/buffer.c
#define BADNESS (BH) ((bh)->b_dir<1)+(bh)->b_lock)/b_dir, b_lock 为 0，BADNESS (BH) 为 00
struct buffer_head *getblk(int dev, int block)
{
	struct buffer_head *tmp, *bh;
	repeat:
		if (bh = get_hash_table(dev,block)) {
		return bh;
	}
	tmp = free_list;
	do {
			if (tmp->b_dev == dev) {
				count();
			if (bh | BADNESS(tmp) == BADNESS(bh)) {
				bh = tmp;
				// 如果 BADNESS(tmp) 为 00，获取空闲 buffer:
				tbreak;
			}
		} while (tmp = tmp->b_next) //tmp->b_count 为 0
	} // bh 为 0
	while (tmp = tmp->b_next_free()) // free_list;
		if (!tmp) { // 在这种情况下找不到空闲 buffer
			sleep(&buffer->wait);
		goto repeat;
	}
	wait_on_buffer(bh);//buffer 块已解锁
	if (bh->b_count) //现在，buffer 块未被使用
		goto repeat;
	while (bh->b_dir //buffer 块的内容未被修改
	sync_dev(bh->b_dev);
	} wait_on_buffer(bh);
	if (bh->b_count)
		goto repeat;
}

	if (find_buffer(dev,block))//找到了空闲 buffer，但它没有链接到...
		goto repeat;
	//哈希表
```

在获取 buffer 块后，初始化它并将其挂载到 `hash_table`。代码如下：

```c
// 代码路径:fs/buffer.c
struct buffer_head * getblk(int dev, int block)
{
    if (find_buffer(dev,block)) {
        goto repeat;
        bh->b_count = 1; // 准备使用
        bh->b_dirt = 0;
        bh->b_uptodate = 0;
    }
    remove_from_queues(bh);
    bh->b_dev = dev;
    bh->b_block = block;
    insert_into_queues(bh);
    return bh;
}
```

```c
// 代码路径:fs/buffer.c
static inline void remove_from_queues(struct buffer_head * bh)
{
    /* 从 hash 队列移除 */
    if (bh->b_next) { //bh->b_next 为 NULL
        bh->b_next->b_prev = bh;
    }
    if (bh->b_prev) { //bh->b_prev 存在
        bh->b_prev->b_next = bh;
    }
    bh->b_next = NULL;
    bh->b_prev = NULL;
}
```

```c
if (rw == READ)                   //读请求来自 request[32] 的末，写请求
    req = request+NR_REQUEST;               //来自 request [32] 的 2/3 
else
    req = request+((NR_REQUEST*2)/3);
/* 寻找一个空 request *///从尾部查找空 request 项，dev
    while ((--req = request))                   //在 blk_dev_init 中初始化为 -1，表示为空
        if (dev->dev)                            //寻找空 request 项
            break;
/* 如果未找到，则在新的请求上等待：检查 rw_ahead */
    if (req) {
        if (rw->ahead) {
            unlock_buffer(bh);
            return;
        }
        sleep(wait_for_request);
        goto req;
/* 填充请求-队列，并将其加入队列 */
req->dev = bh->dev;                         //设置 request 项
req->cmd = rw;
req->errors = 0;
req->sector = bh->blocknr<<1;
req->sector = 2;
req->buffer = bh->data;
req->waiting = NULL;
req->bh = bh;
req->next = NULL;
add_request(major|blk_dev,req);
```

调用 `add_request` 函数将此请求添加到请求队列。进入 `add_request` 后，首先分析硬盘的工作，然后将此请求设置为当前请求项并调用 `(dev->request_fn)();`，即由 `do_hd_request` 向硬盘发送一个读命令。请求管理系统与 `do_hd_request` 函数之间的对应关系如图 3.24 所示。

代码如下：

```c
//Path.kernel/blk_dev/11_rw_block.c:
static void add_request(struct blk_dev_struct * dev, struct request * req)
{
    req->next = tmp;
    cli();
    if (req->bh)
        req->bh->bb_dirt = 0;
        if ((tmp != dev->current_request)) {
            dev->current_request = req;
            sti();
            (dev->request_fn)();                                      //do_hd_request()
            return;
        }
    for (tmp=tmp->next; tmp=tmp->next)                               //电梯算法的效果是
        使磁盘磁头的移动距离 最小
        if (IN_ORDER(tmp,req)) ||
            IN_ORDER(req,tmp->next) &&
            IN_ORDER(tmp,tmp->next)
                break;
    req->next = tmp->next; //绑定请求项队列
    tmp->next = req;
    sti();
}
```

![](img/f661d64b7eb54840fcb4d65765a4e933_143_0.png)

图 3.24 将请求项与硬盘处理函数绑定。

### 3.3.1.4 读取硬盘

执行 `do_hd_request` 函数为读取硬盘做准备，如图 3.25 所示。

首先，分析请求项的成员以获取磁头、扇区、柱道以及要操作的扇区数量。然后，建立必要的硬盘参数并将磁头移动到 0 柱道。然后，向硬盘发送操作命令（读/写）；现在命令已就绪，读取硬盘启动引导并使用 `hd_out` 函数向硬盘发送操作命令。注意最后两个实参：`WIN_READ` 表示操作和读，`read_intr` 是对应于读操作的中断服务程序，如图 3.25 中的第三步所示。代码如下：

```c
// Code path:kernel/blk/dev/hd.c
void do_hd_request(void)
{
    int i,r;
    unsigned int blk,dev;
    unsigned int sec,head,cyl;
    unsigned int next;

    INIT_REQUEST;
    dev = MINOR(current->dev);
    if (dev >= MAX_HR || block+2 > hd[dev].nr_sects) {
        end_request(0);
        goto repeat;
    }
) block = hd(dev) start_sect;
    dev /= 5;
    asm_ = "div14"* = "a" (block),"0" "1" (0),
    asm_ = (hd_info(dev,sect));
    asm_ = "div14"* = "d" (head):"0", "1" (0),
    asm_ = (hd_info(dev,head));

    nsect++;
    current = nsect->sectors;
    if (reset) {
        //设置，防止多次执行如果 (reset)
        reset = 0;
        recalibrate = 1;
        reset_hd(CURRENT_DEV);
        //向硬盘发送命令 "WIN_SPECIFY"
        //通过磁盘调用 hd_out，并建立
        //读取硬盘所必需的参数
        return;
    }
    if (recalibrate) {
        recalibrate = 0;
        //设置，防止多次执行如果
        //(recalibrate)
        dev_out(CURRENT_DEV,sect,6,0,0);
        //向硬盘发送命令 "WIN_RESTORE"
        //WIN_RESTORE,read_intr;
        //硬盘并将磁头
        //头移动到 0 以读取数据
        return;
    }
    if (CURRENT->cmd == WRITE) {
        dev_out(dev,nsect,sec,cyl,WIN_WRITE,write_intr);
        for (i = 0; i<=3000 && ir != inb(HD_STATUS&DRQ); i++) //超时
        if (ir) {
            bad_rw_intr();
            goto repeat;
        }
        outb(HD_DATA,CURRENT->buffer,256);
    } else if (CURRENT->cmd == READ) {
        dev_out(dev,nsect,sec,cyl,WIN_READ,read_intr);//注意两个参数!
    } else
        panic("unknown command");```

如图第一步所示发送硬盘命令。具体代码如下：

```c
//Code path:kernel/blk_dev/hd.c
static void hd_out(unsigned drive, unsigned int nsect, unsigned int sect,
unsigned int head, unsigned int cyl, unsigned int cmd,
void *(addr)(asm("dx"))
{
    if (drive==15) {
        panic("Trying to write bad sector");
    }
    if (!controller_ready) {
        panic("HD controller not ready");
    }//根据参数确定其
    //write intr
    //在此情况下，它是 read_intr
    outb(hd_info(drive).ctl,HD_CMD);
    port = HD_DATA;
    outb(hd_info(drive).count>>2,port);
    outb(nsect,port);
    outb(sect,port);
    outb(cyl,port);
    outb(cyl>>8,port);
    outb(0xA0|(drive<<4)|head,port);
    outb(cmd,port);
}
```

### 3.3 进程 创建与执行

```asm
//Code path:kernel/system_call.s
hd_interrupt:
1:
    xchg $1,do_hd,%edx
    test %edx,%edx
    jne skip
    cmov $unexpected_hd_interrupt,%edx```

`do_hd_intr` 将磁盘服务程序与硬盘中断服务绑定；`do_hd` 是 `hd_interrupt(system_call)` 中 `%xchg_do_hd,%edx` 的内容。

在此情况下，操作是读硬盘，连接到 `read_intr()`；如果是写硬盘，则连接到 `write_intr()` 函数。

读取顺序！硬盘将启动块的数据读取到缓存中；同时，程序返回并调用 `ll_hd_out()`、`do_hd_request()`、`make_request()` 和 `ll_rw_block()`，直到返回函数()。

| 0x00000 | 0x9FFFF | 0x3FFFF | 0x5FFFF | 0xFFFFFF |

| :--- | :--- | :--- | :--- | :--- |

| Kernel | ROM BIOS and VGA | | Enable interrupt |

![](img/f661d64b7eb54840fcb4d65765a4e933_145_0.png)

**图 3.25** 准备读取硬盘。

### 3.3 到进程 I 执行

![](img/f661d64b7eb54840fcb4d65765a4e933_146_0.png)

内核代码区 内核数据区

![](img/f661d64b7eb54840fcb4d65765a4e933_146_1.png)

make_request add_rw_request do_hd_request hd_out

![](img/f661d64b7eb54840fcb4d65765a4e933_146_2.png)

进程状态

![](img/f661d64b7eb54840fcb4d65765a4e933_146_3.png)

图 3.26 向端口寄存器发送参数并挂起当前进程。

现在，硬盘继续读取启动块；如果程序继续执行，它需要操作启动块，但这些数据尚未从硬盘中读取，因此调用 `wait_on_bb_buffer` 函数并挂起进程！执行代码如下：

```c
// path:fs/buffer.c:
struct buffer_head * bread(int dev,int block)
{
    struct buffer_head * bh;

    if ((bh = getblk(dev,block))) {
        panic("bread: getblk returned NULL\n");
        if (bh->b_uptodate) {
            return bh;
        }
        11_rw_block(READ,bh);
        wait_on_buffer(bh);//挂起进程等待
//解锁缓冲区

        if (bh->b_uptodate) {
            return bh;
        }
        brele(bh);
    }
    return NULL;
}
```
