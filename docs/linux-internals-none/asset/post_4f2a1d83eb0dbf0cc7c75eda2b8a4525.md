
## Linux内核init与进程创建机制

```c
static int init(void * unused)
{
    lock_kernel();
    do_basic_setup();

    /*
     * Ok, we have completed the initial bootup, and
     * we're essentially up and running. Get rid of the
     * initmem segments and start the user-mode stuff..
     */
    free_initmem();
    unlock_kernel();

    if (open("/dev/console", O_RDWR, 0) < 0)
        printk("Warning: unable to open an initial console.\n");

    (void) dup(0);
    (void) dup(0);

    /*
     * We try each of these until one succeeds.
     *
     * The Bourne shell can be used instead of init if we are
     * trying to recover a really broken machine.
     */
    if (execute_command)
        execve(execute_command, argv_init, envp_init);
    execve("/sbin/init", argv_init, envp_init);
    execve("/etc/init", argv_init, envp_init);
    execve("/bin/init", argv_init, envp_init);
    execve("/bin/sh", argv_init, envp_init);
    panic("No init found.  Try passing init= option to kernel.");
}
```

这里，init作为内核任务被进入，并创建一个名为init的用户空间进程。init函数被声明为unused，因为它不接受任何参数；它只是从磁盘读取用户空间程序的代码并启动它。

init始终被分配进程ID（PID）号1。为什么不是0，就像计算机行业中通常的计数方式那样？因为0已经被在启动时创建的空闲进程占用了。

在上述代码中，你还可以看到启动期间释放部分内存的console消息来源：free_initmem。该函数释放了内核.text.init段中不再需要的函数。这是在512MB RAM系统（此处命名为hatta）上启动时生成的典型消息：

```
Mar 19 09:14:35 hatta kernel: Freeing unused kernel memory: 72k freed
```

### 进程的创建：Fork与Clone

Init，即“父亲”，通过fork其子进程来创造后代。因此，init是无性别的，能够独自繁殖，无需女性伴侣的帮助。严肃地说，用户程序要么从init创建，要么从init的子进程创建。创建子进程的系统调用称为`fork`，虽然在Linux中还有创建子进程的另一种方式，`__clone()`。系统调用名称前的双下划线是为了表明它通常应该由包装它的库函数调用，以提供更友好的用户界面。

Forking是父进程自我复制为精确副本的一种方式，除了PID不同。`fork()`函数在某个时刻必须将新创建的任务添加到`task_struct`中。用于添加和删除任务的内核函数是`add_to_runqueue`和`del_from_runqueue`。你可以在linux/kernel/sched.c中找到它：

```c
static inline void add_to_runqueue(struct task_struct * p)
{
	list_add(&p->run_list, &runqueue_head);
	nr_running++;
}
```

从新任务诞生的那一刻起，它就是完全独立的。

正如我们之前所见，Linux还引入了创建用户进程的另一种手段，`__clone`。与`fork()`不同，`__clone`允许子进程与其父进程共享执行环境的部分，如内存空间、文件描述符表和信号处理程序表。`__clone`的主要用途是实现*线程*。线程是程序中多个控制流，它们在共享内存空间中并发运行。使用`__clone`时要小心，因为它是Linux特定特性，因此不可移植到其他操作系统；而`fork()`是标准函数，存在于许多平台上，包括Windows。

让我们看看极其重要的PID是如何在内核中分配的。实际函数是linux/kernel/中的fork.c里的`get_pid()`：

```c
static int get_pid(unsigned long flags)
{
	static int next_safe = PID_MAX;
	struct task_struct *p;

	if (flags & CLONE_PID)
		return current->pid;

	spin_lock(&lastpid_lock);
	if( (++last_pid) & 0xffff8000) {
		last_pid = 300;
		/* Skip daemons etc. */
		goto inside;
	}
	if(last_pid >= next_safe) {
	inside:
		next_safe = PID_MAX;
		read_lock(&tasklist_lock);
	repeat:
		for_each_task(p) {
			if(p->pid == last_pid ||
			   p->pgrp == last_pid ||
			   p->session == last_pid) {
				if( ++last_pid >= next_safe) {
					if(last_pid & 0xffff8000)
						last_pid = 300;
					next_safe = PID_MAX;
				}
				goto repeat;
			}
			if(p->pid > last_pid && next_safe > p->pid)
				next_safe = p->pid;
			if(p->pgrp > last_pid && next_safe > p->pgrp)
				next_safe = p->pgrp;
			if(p->session > last_pid && next_safe > p->session)
				next_safe = p->session;
		}
		read_unlock(&tasklist_lock);
	}
	spin_unlock(&lastpid_lock);
	return last_pid;
}
```

这里的代码可能让你觉得很难理解，因为开发者试图让代码（以及因此的整体进程创建）尽可能快。

如果速度是关键，为什么程序员不直接使用任务结构中进程的索引号？因为许多用户空间程序员仍然假设相同的PID不会在进程使用它之后很快再次出现。他们认为PID在PID编号空间中循环。虽然从未有人做出过这种保证，但内核必须与这些设计不良的程序兼容。该函数确实保留一个指向下一个可能或安全PID的指针，这里称为next_safe。每次创建进程时，last_pid字段增量超过next_safe PID时，上述函数必须遍历整个任务列表以搜索另一个PID候选者。

两个任务可能共享相同的PID，如果它们是同一进程内的线程。在这种情况下，以下代码段：

```c
if (flags & CLONE_PID)
	return current->pid;
```

立即返回相同的PID。

一旦last_pid环绕PID编号空间（32,767），上述代码开始寻找新的PID。然而，它会跳到300之后的下一个数字，因为300以下的许多数字通常被系统守护进程和在启动时启动并运行整个系统生命周期的程序占用。这些PID几乎从未返回到空闲列表。为了节省几个宝贵的时钟周期，内核只是跳过它们。

在配置最大任务数超过32,767的系统中，理论上可能会出现没有可用PID槽位的情况。因此，任务创建将以负返回码失败。

显然，程序员并不总是希望启动原始程序的副本，而是希望在程序执行期间的某个时刻启动一个完全不同的程序。对于这些情况，她必须使用exec()。

用户程序将执行权传递给另一个程序的唯一方式是：

- 使用`fork()` fork到自身的另一个实例。
- 然后使用`exec()`加载另一个二进制程序映像并传递执行权。

实现exec()调用的内核代码位于linux/fs/exec.c。该程序太长而无法在此包含（在2.3.52版本中近一千行）。这是它被调用时所做的：

- `prepare_binprm()`代码定位包含二进制映像的文件，并将前128字节读取到brpm结构体的buf变量中。（参见本章末尾的数据结构。）

```c
int prepare_binprm(struct linux_binprm *bprm)
{
	int mode;
	int retval, id_change, cap_raised;
	struct inode * inode = bprm->dentry->d_inode;

	mode = inode->i_mode;
	if (!S_ISREG(mode)) /* must be regular file */
		return -EACCES;
	if (!(mode & 0111)) /* with at least one execute bit set */
		return -EACCES;
	if (IS_NOEXEC(inode)) /* FS mustn't be mounted noexec */
		return -EACCES;
	if (!inode->i_sb)
		return -EACCES;
	if ((retval = permission(inode, MAY_EXEC)) != 0)
		return retval;
	/* better not execute files which are being written to */
	if (atomic_read(&inode->i_writecount) > 0)
		return -ETXTBSY;

	bprm->e_uid = current->euid;
	bprm->e_gid = current->egid;
	id_change = cap_raised = 0;

	/* Set-uid? */
	if (mode & S_ISUID) {
		bprm->e_uid = inode->i_uid;
		if (bprm->e_uid != current->euid)
			id_change = 1;
	}

	/* Set-gid? */
	/*
	 * If setgid is set but no group execute bit then this
	 * is a candidate for mandatory locking, not a setgid
	 * executable.
	 */
	if ((mode & (S_ISGID | S_IXGRP)) == (S_ISGID | S_IXGRP)) {
		bprm->e_gid = inode->i_gid;
		if (!in_group_p(bprm->e_gid))
			id_change = 1;
	}

	/* We don't have VFS support for capabilities yet */
	cap_clear(bprm->cap_inheritable);
	cap_clear(bprm->cap_permitted);
	cap_clear(bprm->cap_effective);

	/*  To support inheritance of root-permissions and suid-root
	 *  executables under compatibility mode, we raise the
	 *  effective and inherited bitmasks of the executable file
	 *  (translation: we set the executable "capability dumb" and
	 *  set the allowed set to maximum). We don't set any forced
	 *  bits.
	 *
	 *  If only the real uid is 0, we only raise the inheritable
	 *  bitmask of the executable file (translation: we set the
	 *  allowed set to maximum and the application to "capability
	 *  smart").
	 */

	if (!issecure(SECURE_NOROOT)) {
		if (bprm->e_uid == 0 || current->uid == 0)
			cap_set_full(bprm->cap_inheritable);
		if (bprm->e_uid == 0)
			cap_set_full(bprm->cap_permitted);
	}
}
```
