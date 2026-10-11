
`struct cq_struct cq_area = {0, 0, 0, {0}, 0, 0, "", NULL};`

```c
struct timer_list cq_timer = {NULL, NULL, 0, 0, &cq_timer_handler};
```

```c
inline char * mcodestring(int asciicode)
{
    char * mc;
     /* 这是从 ASCII 代码到
    到模式字符串数组的映射。 */
    if(asciicode > 122) /* 超过 'z' */
        mc = morse_code[CQ_DEFAULT];
    else if (asciicode > 96) /* 大写 */
        mc = morse_code[asciicode - 96];
    else if (asciicode > 90) /* 未编码的标点符号 */
        mc = morse_code[CQ_DEFAULT];
    else if (asciicode > 64) /* 小写 */
```

```c
mc = morse_code[asciocode - 64];
else if (asciocode == 63) /* 问号 */
mc = morse_code[39]; /* 36 + 3 *//
else if (asciocode > 57) /* 未编码的标点符号 */
mc = morse_code[CQ_DEFAULT]; /* 数字 */
else if (asciocode > 47) /* (asciocode - 21]; /* 27 + (asciocode - 48) */
else if (asciocode == 46) /* 句点 */
mc = morse_code[38]; /* 36 + 2 */
else if (asciocode == 44) /* 逗号 *//
mc = morse_code[37]; /* 36 + 1 *//
else
mc = morse_code[CQ_DEFAULT];
```

```c
static int cq_reset(void)
{
    speaker_off();
    cq_set_pitch(CQ_DEF_PITCH); /* 频率，单位为 Hz */
    cq_set_tempo(CQ_DEF_TEMPO); /* 四分符等于此值 */
    return 0;
}
```

```c
void cq_timer_handler(unsigned long x)
{
    /* 这是被调用的函数，因为
       它被提交到了定时器队列。 */
    int status;
    unsigned int time_value;
    time_value = jiffies + 1; /* 缓解 gcc */
    status = cq_area.flags;
    if ((cq_area.mcode) == 0) && (status & CQ_OFF)
        && (cq_area.buffer.offset + 1 == cq_area.buffer.end) /* 缓冲区满 */
    {
        wake_up_interruptible(&cq_area.cq.wait.q);
        return;
    }
```

## 11.3. 摩斯密码驱动

```c
if ((cq.area.mcode) == 0) && (status)))
    /* 字符完成。重置代码。 */
{
    cq.area.buffer.offset = cq.area.buffer_end;
    x = cq.area.buffer[cq.area.offset];
    cq.area.mcode = mcodestring(x);
}
if ((cq.area.mcode) == 0) && (status))
    /* 前面的缓冲区放入了空字符串。 */
    /* 空字符串获得四分符。 */
{
    time_value = cq.area.wholenote >> 2;
}
else if (status)
    /* 扬器关闭。开始另一个点或划线。 */
{
    if (cq.area.mcode) == '.')
        time_value = cq.area.wholenote >> 2;
    else if (cq.area.mcode) == '-'
        time_value = cq.area.wholenote >> 4;
    cq.area.mcode = (cq.area.mcode) + 1;
    speaker_on();
}
else if (cq.area.mcode) == 0
    /* 字符结束。 */
{
    time_value = (cq.area.wholenote >> 3) + (cq.area.wholenote >> 2);
    /* 字母间间隔 * */
    speaker_off();
}
else /* 扬声器开启。处于字符中。 */
{
    time_value = (cq.area.wholenote >> 3);
    /* 字母内间隔 * */
    speaker_off();
}
cq.timer.expires = jiffies + time_value;
/*
cq.timer.expires = jiffies;
    如果你在其他地方看到这种写法
    它是不起作用！ */
add_timer(&cq.timer);

return;
```

```c
static ssize_t cq_write(struct file * file, const char * buf,
    size_t count, loff_t *ppos)
{
    /* 该函数填充缓冲区后进入睡眠。 */
    unsigned long copy_size;
    unsigned int time_value;
    ssize_t total_written = 0;
    while ((copy_size = cq.area.buffer_end - cq.area.buffer.offset) > 0)
    {
        if (count < copy_size)
        {
            copy_from_user(buf, &cq.area.buffer[cq.area.buffer.offset], count);
            cq.area.buffer.offset += count;
            count = count;
            break;
        }
        else
        {
            copy_from_user(buf, &cq.area.buffer[cq.area.buffer.offset], copy_size);
            cq.area.buffer.offset += copy_size;
            count -= copy_size;
            buf += copy_size;
        }
    }
    if (count == 0)
    {
        cq.area.buffer.offset = cq.area.buffer_end;
        wake_up_interruptible(&cq.area.cq.wait.q);
    }
    return 0;
}
```

# 第 11 章 设备驱动程序

扬声器将鸣叫。为了实现这一点，`/dev` 目录下必须有一个名为 `cq` 的条目，它与程序通过 `cq_write()` 关联。

### 11.3.11 收尾工作

要完成设备驱动程序，只需要处理 `/usr/include/linux/major.h` 文件。

* 为 `/usr/include/linux/major.h` 文件中的设备分配一个数字。
* 使用 `mknod` 命令在 `/dev` 目录中为设备创建一个条目。
* 编写一个 `cq_init()` 函数并在 `mem.c` 文件中包含它的调用。
* 修改驱动程序所在目录的 `Makefile`（在此情况下为 `/usr/src/linux/drivers/char/`），并重新编译内核。
