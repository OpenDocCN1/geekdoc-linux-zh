
```c
void speaker_off(void);

char *morse_code[40] = {
    "", "-.-...", "-.", "-..", ".", "..-.", "..", "--.", "-..-", "...", "",
    "-.-.", ".-..", "", "", "--", "-.-", "--..", ".", "-", "", "", "--..",
    ".-", ".-..", "", "-", "..-.", "", "--.", ".-.", "", ""
};

/* The empty string, followed by the 26 letter codes, 
   followed by the 10 numeral codes, followed by the comma,
   period, and question mark.  */

struct cq_struct cq_area = {0, 0, 0, {0}, 0, 0, "", NULL};

struct timer_list cq_timer = {NULL, NULL, 0, 0, &cq_timer_handler};

inline char *mcodestring(int asciicode)
{
    char *mc;
    /* This is the mapping from the ASCII code
       into the mcode array of strings.  */

    if(asciicode > 122) /* Past 'z' */
        mc = morse_code[CQ_DEFAULT];
    else if(asciicode > 96) /* Upper case */
        mc = morse_code[asciicode - 96];
    else if(asciicode > 90) /* Uncoded punctuation */
        mc = morse_code[CQ_DEFAULT];
    else if(asciicode > 64) /* Lower case */
        mc = morse_code[asciicode - 64];
    else if(asciicode == 63) /* Question Mark */
        mc = morse_code[39]; /* 36 + 3 */
    else if(asciicode > 57) /* Uncoded punctuation */
        mc = morse_code[CQ_DEFAULT];
    else if(asciicode > 47) /* Numerals */
        mc = morse_code[asciicode - 21]; /* 27 + (asciicode - 48) */
    else if(asciicode == 46) /* Period */
        mc = morse_code[38]; /* 36 + 2 */
    else if(asciicode == 44) /* Comma */
        mc = morse_code[37]; /* 36 + 1 */
    else
        mc = morse_code[CQ_DEFAULT];
    return mc;
}

static int cq_reset(void)
{
    speaker_off();
    cq_set_pitch(CQ_DEF_PITCH);  /* Pitch in Hz */
    cq_set_tempo(CQ_DEF_TEMPO); /* Quarter note equals this */
    return 0;
}

void cq_timer_handler(unsigned long x)
{
    /* This is the function which is called because
       its name is submitted to the timer queue.  */

    int status;
    unsigned int time_value;

    time_value = jiffies + 1; /* Mollify gcc */

    status = cq_area.flags;

    if (((cq_area.mcode) == 0) && (status & CQ_OFF)
        && (cq_area.buffer_offset + 1 == cq_area.buffer_end))
    {
        /* This buffer load is done */
        wake_up_interruptible(&cq_area.cq_wait_q);
        return;
    }
    
    if (((cq_area.mcode) == 0) && (status & CQ_OFF))
    {
        /* This character is done.  Reset mcode.  */
        cq_area.buffer_offset = cq_area.buffer_offset + 1;
        x = cq_area.buffer[cq_area.buffer_offset];
        cq_area.mcode = mcodestring(x);
    }
    
    if (((cq_area.mcode) == 0) && (status & CQ_OFF))
    {
        /* Preceding if-block put in the empty string.  */
        /* Empty string gets a quarter note.  */
        time_value = cq_area.wholenote >> 2;
    }
    else if (status & CQ_OFF)
    {
        /* Speaker is off.  Begin another dot or dash */
        if (*(cq_area.mcode) == '.')
            time_value = cq_area.wholenote >> 2;
        else if (*(cq_area.mcode) == ',')
            time_value = cq_area.wholenote >> 4;
        cq_area.mcode = cq_area.mcode + 1;
        speaker_on();
    }
    else if (*(cq_area.mcode) == 0)
    {
        /* Speaker is on.  End of character.  */
        time_value =
            (cq_area.wholenote >> 3) + (cq_area.wholenote >> 2);
        /* Inter-letter rest */
        speaker_off();
    }
    else /* Speaker is on.  In the midst of a character.  */
    {
        time_value = (cq_area.wholenote >> 3);
        /* Short intra-letter rest */
        speaker_off();
    }
    
    cq_timer.expires = jiffies + time_value;

    /*
        cq_timer.expires = jiffies;
        In case you have seen this elsewhere,
        it does Not Work!
    */

    add_timer(&cq_timer);
    return;
}

static ssize_t cq_write(struct file *file, const char *buf,
                       size_t count, loff_t *ppos)
{
    /* This function fills the buffer and then goes to sleep.  */
    unsigned long copy_size;
    unsigned int time_value;
    ssize_t total_bytes_written = 0;
    time_value = 1;

    total_bytes_written = 0;
    do
    {
        if (signal_pending(current))
            return total_bytes_written;
        copy_size = (count <= CQ_BUFFER_SIZE ? count : CQ_BUFFER_SIZE);
        cq_area.buffer_offset = 0;
        cq_area.buffer_end = copy_size;
        copy_from_user(cq_area.buffer, buf, copy_size);
        cq_area.mcode = mcodestring(cq_area.buffer[0]);

        time_value = cq_area.wholenote >> 4;
        cq_timer.expires = jiffies + time_value;
        add_timer(&cq_timer);
        speaker_off();
        interruptible_sleep_on(&(cq_area.cq_wait_q));
        total_bytes_written = total_bytes_written + copy_size;
        count = count - copy_size;
        buf = buf + copy_size;
    } while (count > 0);
    del_timer(&cq_timer);
    return total_bytes_written;
}

static long long cq_lseek(struct file *file,
                          long long offset, int origin)
{
    return -ESPIPE;
}

static int cq_open(struct inode *inode, struct file *file)
{
    unsigned int minor = MINOR(inode->i_rdev);

    if (minor > 0) /* Stereo No */
        return -ENXIO;
    if ((cq_area.flags & CQ_EXIST) == 0)
        return -ENXIO;
    if (cq_area.flags & CQ_BUSY)
        return -EBUSY;

    cq_area.flags = (cq_area.flags | CQ_BUSY);
    return 0;
}

static int cq_release(struct inode *inode, struct file *file)
{
    cq_area.flags = (cq_area.flags & ~CQ_BUSY);
    return 0;
}

static void cq_set_pitch(unsigned long cps)
{
    cq_area.timerdiv = 1193180 / cps;

    /* Frequency of the OSC signal on the AT bus */
}

static void cq_set_tempo(unsigned long beats_per_minute)
{
    /* Quarter note = 1 beat, timer works in centi seconds */

    cq_area.wholenote = 24000 / beats_per_minute;
}

static int cq_ioctl(struct inode *inode, struct file *file,
                    unsigned int cmd, unsigned long arg)
{
    unsigned int minor = MINOR(inode->i_rdev);
    int retval = 0;

    if (minor > 0)
        return -ENODEV;
    if (((cq_area.flags) & CQ_EXIST) == 0)
        return -ENODEV;
    switch (cmd)
    {
    case CQABORT:
        if (arg)
            cq_area.flags = (cq_area.flags | CQ_ABORT);
        else
            cq_area.flags = (cq_area.flags & ~CQ_ABORT);
        break;
    case CQSETPITCH:
        if (arg)
            cq_set_pitch(arg);
        else
            retval = -EINVAL;
        break;
    case CQSETTEMPO:
        if (arg)
            cq_set_tempo(arg);
        else
            retval = -EINVAL;
        break;
    case CQRESET:
        cq_reset();
        break;
    case CQGETFLAGS:
        retval = verify_area(VERIFY_WRITE,
                             (void *) arg, sizeof(int));
        if (retval)
            return retval;
        else
        {
            int status = cq_area.flags;
            copy_to_user((int *) arg, &status, sizeof(int));
        }
        break;
    default:
        retval = -EINVAL;
    }
    return retval;
}

int cq_init(void)
{
    /* Initialization code like this can be called
       if a call to it is placed in mem.c */
    if (register_chrdev(CQ_MAJOR, "cq", &cq_fops))
    {
        printk(KERN_INFO "cq: unable to get major %d\n", CQ_MAJOR);
        return -EIO;
    }
    cq_area.flags = (CQ_OFF | CQ_EXIST);
    cq_reset();
    return 0;
}
```

通常做法是在包含文件中定义 C 程序中使用的参数。摩斯密码驱动程序的包含文件如下。

```c
#define CQ_EXIST	0x0001
#define CQ_BUSY	0x0002
#define CQ_OFF		0x0004
#define CQ_ABORT	0x0008

/* IOCTL numbers */

#define CQABORT	0x0714
#define CQSETTEMPO  0x0716  /* Store whole note int cq_area.  */
#define CQSETPITCH  0x0719  /* Store a timer divisor into cq_area.   */
#define CQRESET	0x071c  /* reset speaker */
#define CQGETFLAGS  0x071e  /* get status flags */
```

```c
#define CQ_BUFFER_SIZE         256
#define CQ_DEF_CHAR            0      /* Default character */
#define CQ_DEF_PITCH           440    /* Default pitch */
#define CQ_DEF_TEMPO           160    /* Default tempo */
/*
 *  function prototypes
 */
extern int cq_init(void);
```

定义在结构 `cq_struct` 中的函数负责处理驱动程序对内核在执行系统调用时向驱动程序发出的服务请求的响应。`cq_timer_handler()` 函数负责处理驱动程序对定时器中断的响应。这些是主要需要完成的工作。但当设备驱动程序工作时，诸如

```bash
linuxbox$ cat file > /dev/cq
```

等命令将开始让扬声器发出蜂鸣声。为了实现这一点，必须在 `/dev` 目录中有一个名为 `cq` 的条目，该条目与 `cq_write()` 等程序相关联。

## 11.3.11 收尾工作

为了完善设备驱动程序，只需执行以下操作：

- 在 `/usr/include/linux/major.h` 文件中为该设备添加一个主设备号。
- 使用 `mknod` 命令在 `/dev` 目录中为该设备创建条目。
- 编写 `cq_init()` 函数，并在 `mem.c` 文件中包含对其的调用。
- 修改包含驱动程序的目录（本例中为 `/usr/src/linux/drivers/char`）下的 `Makefile`，并重新编译内核。

`/dev` 目录包含大量文件列表，其中大多数实际上并不是常规文件。`ls -l` 命令通过每一行的第一个字符来区分不同类型的文件。真正的常规文件以 `a -` 开头列出，目录以 `ad` 开头列出，硬链接以 `l` 开头列出，等等。设备根据是块设备还是字符设备，分别以 `b` 或 `c` 列出。块设备以块为单位传输数据，即大小均匀的大数据块。为此，它们与内核的缓冲区缓存进行交互。块设备可以被挂载，即集成到 Unix 的树状文件层次结构中。硬盘是块设备的一个良好示例。字符设备不使用块，也不会被挂载。我们的小扬声器驱动程序是一个字符设备。每个设备条目，无论是块设备还是字符设备，还都列出了主设备号和次设备号。主设备号用作内核字符设备驱动程序数组 `chrdevs` 的索引。

```c
struct device_struct chrdevs[MAX_CHRDEV]
```

每个设备驱动程序仅仅是一个

```c
struct device_struct
{
    const char *name;
    const struct file_operations *fops;
};
```

设备通过定义在 `/usr/src/linux/fs/devices.c` 中的函数 `register_chrdev()` 被放入数组中。该定义中最重要的是以下几行。

### 程序 11.8

```c
int register_chrdev(unsigned int major,
                    const char *name,
                    const struct file_operations *fops)
{
    ...
}
```

