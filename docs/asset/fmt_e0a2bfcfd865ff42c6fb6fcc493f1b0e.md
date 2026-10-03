
```c
// 代码路径: fs/pipe.c
int write_pipe(struct m_inode *inode, char *buf, int count) // 写入管道函数
{
    int chars, size, written = 0;
    while (count > 0)
    {
        size = PIPE_HEAD(*inode); // chars
        size = PAGE_SIZE - PIPE_HEAD(*inode);
        if (size > 0) {
            wake_up(&inode->i_wait);
        }
    }
}
```

### 8.1 管道机制

所有可写空间已完全写入，写入指针循环一圈。写入指针比读取指针快一个位置。Linux 1 定义函数 `sys_write()` 如下。写入进程一次最多可以写入 4095 字节。

现在，我们将介绍示例 1 中管道进程的操作过程。

**读取管道进程开始操作管道文件。** 在示例 1 中，父进程在创建管道后开始创建作为读取进程的子进程。当进程创建后，我们假设系统中只有两个进程，即读取管道进程和写入进程处于系统状态。读取管道进程首先执行，它将执行示例 1 中的源代码 `"read(fd[0], str2, strlen(str2))"`。`read()` 函数被映射到系统函数 `sys_read()` 并执行。最终，它将执行到 `read_pipe()` 函数。由于目前管道没有数据，系统将挂起读取进程并切换到写入管道进程执行。具体代码如下：

```c
// 代码路径: fs/read_write.c
int sys_read(unsigned int fd, char *buf, int count)
{
    verify_area(buf, count);
    inode = file->inode;
    if (inode->i_pipe)
        return (inode->f_mode & S_IFREG) ? read_pipe(inode, buf, count) - EIO : function;
    if (S_ISCHR(inode->i_mode))
        return wr_char(READ, inode->i_zone[0], buf, count, &inode->f_pos);
}

// 代码路径: fs/read_pipe.c
int read_pipe(struct m_inode *inode, char *buf, int count)
{
    int chars, size = 0;
    while ((size < PIPE_SIZE(*inode))) { // 管道中没有数据，进入此循环并执行
        wake_up(inode->i_wait);
        if (inode->i_count == 0) { // 还有写入者吗？
            return 0;
            sleep_on(&inode->i_wait); // 挂起读取进程并切换到读取进程（假设操作管道中只有两个进程处于就绪状态！）
        }
        chars = PAGE_SIZE - PIPE_TAIL(*inode);
        if (chars > count)
            chars = count;
    }
}
```

目前管道中没有任何数据，读取进程被挂起。进程的状态如图 8.7 所示。

**写入进程将数据写入管道。** 写入管道进程将执行，它将循环地将 `str` 数组中指定的 1024 字节数据写入管道。该进程正在执行源代码 `"write(fd, str, strlen(str))"`。`write()` 函数将映射到系统调用 `sys_write()` 执行，最终，它将执行到 `write_pipe()` 函数。写入后，管道获得了已读的数据。然后 `wake_up` 并不意味着读取管道进程（读取进程已被唤醒）会立即执行。

![](img/f661d64b7eb54840fcb4d65765a4e933_457_0.png)

**图 8.7** 进程开始操作管道；挂起读取进程。

因此，写入管道的操作完成。具体代码如下。

```c
// 代码路径: fs/read_write.c
int sys_write(unsigned int fd, char *buf, int count)
{
    if (count < 0)
        return 0;
    inode = file->f_inode;
    if (inode->i_pipe)
        return (file->f_mode & 2) ? write_pipe(inode, buf, count) : -EIO; // 调用写入管道函数
    if (S_ISCHR(inode->i_mode))
        return rw_char(WRITE, inode->i_zone[0], buf, count, &f_pos);
}
```

```c
// 代码路径: fs/pipe.c
int write_pipe(struct m_inode *inode, char *buf, int count) // 写入管道函数
{
    int chars, size, written = 0;
    while (count > 0)
    {
        size = PIPE_HEAD(*inode); // chars
        size = PAGE_SIZE - PIPE_HEAD(*inode);
        if (size > 0) {
            wake_up(&inode->i_wait);
        }
    }
}
```

图 8.11 挂起写管道进程并唤醒读管道进程。

挂起写管道进程并切换到读管道进程的过程如图 8.11 所示。

**读管道进程读取管道数据。** 读管道进程将继续在 `read_pipe()` 函数中执行。根据示例 1 的代码，执行过程将从管道中读取 512 字节数据到读管道进程的用户空间。具体代码如下：

```c
// path/fs/pipe.c
int read_pipe(struct m_inode *inode, char *buf, int count) {
    while (count > 0) { // read 512 bytes of data
        int chars = PAGE_SIZE - PIPE_TAIL(inode);
        if (chars > count)
            chars = count;
        if (chars > size)
            chars = size;
        count = chars;
        read = chars;
        size = PIPE_TAIL(inode) & (char *)count = chars; // the number that the pointer moves is the number that it reads
        PIPE_TAIL(inode) &= (PAGE_SIZE - 1);
        while (chars-- > 0) {
            put_fs_byte((char *)inode->i_size[size++], buf++); // the code of reading data
        }
    }
}
```

### 8.11 管道机制

读取数据意味着管道有剩余空间。现在系统唤醒写管道进程。具体代码如下。

```c
// code path: fs/pipe.c
int read(struct m_inode *inode, char *buf, int count)
{
    while (count > 0) {
        size = PIPE_TAIL(*inode);
        PIPE_TAIL(*inode) += chars;
        PIPE_TAIL(*inode) &= (PAGE_SIZE - 1);
        while (chars-- > 0) {
            put_fs_byte((char *)inode->i_size[size++], buf++);
        }
    }
    wake_up(&inode->i_wait); // wake up the write pipe process
}
```

读管道进程从管道中读取数据的过程如图 8.12 所示。

读管道进程继续执行并不断从管道中读取数据。当前进程是读管道进程。从管道读取数据后将返回到用户空间。根据示例 1 中的代码 `for(j=0; j<20000; j++)`，当读管道进程的时间片未被用完时，读管道应该操作 20,000 次。因此，读取过程应该持续进行。读管道进程不断从管道中读取数据的过程如图 8.13 所示。

| 0x00000 | 0x9FFFF | 0xFFFFFF | 0x3FFFF | 0x5FFFF | 0xFFFFFF |
| :--- | :--- | :--- | :--- | :--- | :--- |
| kernel | ROM BIOS and VGA | | | | |

![](img/f661d64b7eb54840fcb4d65765a4e933_462_0.png)

**图 8.12** 读管道进程从管道中读取数据。

![](img/f661d64b7eb54840fcb4d65765a4e933_463_0.png)

**图 8.13** 管道进程不断从管道中读取数据。

**在读管道进程执行期间发生定时中断。** 假设在执行期间发生了定时中断，且时间片被削减。只要时间片没有减到 0，它就会继续执行。具体代码如下。

```c
// code_path: kernel/sched.c
void do_timer(long cpl)
{
    if (next_timer) {
        next_timer->jiffies--;
        while (next_timer && next_timer->jiffies < 0) {
            void (*fn)(void);
            fn = next_timer->fn;
            next_timer->fn = NULL;
            next_timer = next_timer->next;
            (fn)();
        }
    }
    if (current->DOR & 0xf0) {
        do_floppy_timer();
    }
    if ((--current->counter) > 0) return; // time slice is not 0, return directly
    current->counter = 0;
    if (cpl) return;
    schedule();
}
```

读管道进程执行期间发生定时中断的处理方法如图 8.14 所示。注意图中读管道进程的进程条；其时间片已被削减。

在读管道进程执行期间再次发生定时中断。在读管道进程执行期间再次发生定时中断，且此时读管道进程的时间片为 0。读管道进程将被挂起并切换到写管道进程执行。具体代码如下。

```c
// code path: kernel/sched.c
void do_timer(long cpl)
{
    if (current->DOR & 0xf0)
        do_floppy_timer();
    if ((--current->counter) > 0) return; // time slice becomes 0
    current->counter = 0;
    if (!cpl) return; // process switch
    schedule();
}
```
