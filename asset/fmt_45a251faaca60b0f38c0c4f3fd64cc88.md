
```c
static int check_free_space(struct file *file)

{

    struct statfs sbuf;

    int res;

    int act;

    lock_kernel();

    res = ac_active;

    if (!acct_needcheck)

        goto out;

    unlock_kernel();

    if (vfs_statfs(file->f_entry->d_inode->i_sb, &sbuf))

        return res;

    if (sbuf.f_avail <= SUSPEND*sbuf.f_blocks/100)

        act = -1;

    else if (sbuf.f_avail >= RESUME*sbuf.f_blocks/100)

        act = 1;

    else

        act = 0;

    lock_kernel();

    if (!acct_file) {

        res = act > 0;

        goto out;

    }

    if (acct_active) {

        if (act == 0)

            acct_active = 0;

        printk(KERN_INFO "Process accounting paused\n");

    } else {

        if (act > 0)

            acct_active = 1;

        printk(KERN_INFO "Process accounting resumed\n");

    }

    del_timer(&acct_timer);

    acct_needcheck = 0;

    acct_timer.expires = jiffies + ACCT_TIMEOUT*HZ;

    add_timer(&acct_timer);

    res = acct_active;

out:

    unlock_kernel();

    return res;

}
```

**图 23.5** 检查空闲空间

# 写入核算文件

- 129 标记核算挂起。
- 130 此处以 `KERN_INFO` 优先级打印消息。
- 132–137 如果核算已经挂起，则执行此代码块。
- 133–136 如果空闲空间高于 `RESUME`，我们将核算标记为激活，并以 `KERN_INFO` 优先级打印消息。
- 139–142 定时器必须已经过期才能到达第 101 行，因此在此处对其重置。
- 139 此处将定时器从定时器列表中移除（见第 15.3.2.5 节）。
- 140 该标志在定时器过期时设置。由于已经检查了空闲空间，可以清除此标志。
- 141 此处为下一个间隔设置定时器中的 `expires` 字段。`ACCT_TIMEOUT` 单位为秒；乘以 `HZ` 将其转换为滴答（ticks）。它在 23.1.1 中定义。
- 142 此函数根据到期时间，将定时器插入定时器列表的正确位置（见第 15.3.2.2 节）。
- 143 返回值现在是 `acct_active` 的值。它是之前的值，或者可能在第 129 行或第 134 行被设置。
- 145–146 释放大内核锁并返回 `res` 中的值。

## 23.3 写入核算文件

写入核算文件的实际过程分两个步骤处理。首先，有一个封装函数，它检查是否存在核算文件，并保证在一个进程写入时没有其他进程可以将其移除。它调用第二个函数，由该函数执行写入核算记录的实际工作。

### 23.3.1 检查是否存在核算文件

图 23.6 来自 `kernel/acct.c` 的函数由 `do_exit`（见第 9.1 节）调用。它检查是否存在核算文件，并获取表示该文件的结构指针。

```c

349 int acct_process(long exitcode)
350 {
351 struct *file= NULL;
352 lock_kernel();
353 if (acct_file) {
354 file = acct_file;
355 get_file(file);
356 unlock_kernel();
357 do_acct_process(exitcode, acct_file);
358 fput(file);
359  } else
360      unlock_kernel();
361      return 0;
362 }

```

**图 23.6** 检查是否存在核算文件

- 349 参数是传递给 `exit()` 系统服务的 `exitcode`。
- 352 在检查核算文件是否存在之前就获取了大内核锁（big kernel lock）。该文件可能被另一个进程移除，此锁保证如果发现存在，它将一直存在直到被此进程标记为已使用。该函数在第 5.5 节中解释过。
- 353–360 只有在核算文件处于打开状态时，才会执行任何操作。
- 355 我们原子地增加了表示核算文件的结构体中的 `use count` 字段。该函数是 IO 管理器的一部分。
- 356 现在既然 `use count` 已经增加，即使另一个进程尝试删除核算文件，计数也只会减少，而不会被实际删除，因此可以释放大锁（函数详情见第 5.5 节）。
- 357 此函数是实际向文件写入核算记录的函数（见第 23.3.2 节）。
- 358 此函数减少了 `file` 结构体中的 `use count` 字段，表示此进程已处理完毕。

### 23.3.2 写入核算记录

图 23.7 来自 `kernel/acct.c` 的函数为退出的进程写入核算条目。`acct` 结构体在这里构建并写入核算文件。

```c

275  static void do_acct_process(long exitcode, struct file *file)
276  {
278      struct acct ac;
279      mm_segment_t tfs;
279      unsigned long vsize;
280
285      if (check_free_space(file))
286          return;
292          memset((caddr_t)&ac, 0, sizeof(struct acct));
293
294      strncpy(ac.ac_comm, current->comm, ACCT_COMM);
295      ac.ac_comm[ACCT_COMM-1] = '\0';
296
297      ac_btime = CT_TO_SECS(current->start_time) +
               (time.tv_sec - (jiffies / HZ));
298 ac_ac_utime = encode_comp_t(jiffies -
                    current->start_time);
299 ac_ac_utime = encode_comp_t(current->times.ms_utime);
300 ac_ac_stime = encode_comp_t(current->times.ms_stime);
301 ac_ac_uid = current->uid;
302 ac_ac_gid = current->gid;
303 ac_ac_tty = (current->tty)
                    kdev_to_nr(current->tty) : 0;
304 ac_ac_flag = 0;
305 if (current->flags & PF_FORK)
306     ac_ac_flag |= AFORK;
307 if (current->flags & PF_SUPER)
308     ac_ac_flag |= ASU;
309 if (current->flags & PF_DUMP)
310     ac_ac_flag |= CORE;
311 if (current->flags & PF_SIGNALED)
312     ac_ac_flag |= AXSIG;
314 vsize = 0;
315 if (current->mm) {
316 struct vma_area_struct *vma;
317 down_read(&current->mm->mmap_sem);
318 vma = current->mm->mmap;
319 while (vma) {
320 vsize += vma->vm_end - vma->vm_start;
321 vma = vma->vm_next;
322 }
```
