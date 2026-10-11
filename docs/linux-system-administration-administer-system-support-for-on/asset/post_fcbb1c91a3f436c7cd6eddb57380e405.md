
## The core kernel functions

The core kernel functions are in the `/usr/src/linux/kernel` directory. The C program files in that directory are listed as follows.

```bash
$ ls /usr/src/linux/kernel/*.c

    dma.c   fork.c    ksyms.c   printk.c  signal.c  systcl.c
    exec.c  info.c    module.c  resource.c softirq.c time.c
    exit.c  itimer.c  panic.c   sched.c   sys.c
```

![](img/8ad518fddafc7f5e73715a2604b61d50_181_0.png)

Linux is really cool because the source code is free. You can learn a lot just by examining the source code (provided you can read C). Because some key files in the `/usr/src/linux/kernel` explain how the kernel works, you may want to look over some code not covered in this chapter. This section defines a kernel panic, fork, and other important system functions so you may have a better understanding of how the kernel works with the hardware and the user environment.

## panic.c

A *kernel panic* happens when something goes wrong with the kernel. For example, if you are using the wrong kernel to boot from, you may have a kernel panic. Another thing that may cause a kernel panic is a corrupted file system or device file. When a kernel panics, generally it will try to reboot, and create its own timeout countdown before rebooting. However, sometimes the system will just come to a halt.

Listing 6-1 is a *panic.c* code listing that shows the kernel starting a timer and trying to reboot to correct the problem. As you examine it, pay particular attention to the comments.

### Listing 6-1: Examining the kernel during a panic

```c
/*
 *  linux/kernel/panic.c
 *
 *  Copyright (C) 1991, 1992 Linus Torvalds
 */

/*
 * This function is used through-out the kernel (including mm and fs)
 * to indicate a major problem.
 */
#include <stdarg.h>

#include <linux/kernel.h>
#include <linux/sched.h>
#include <linux/delay.h>

asm("linkage void sys_sync(void);.../* it's really int */
extern void hard_reset_now(void);
extern void do_unblank_screen(void);
extern void gdth_halt(void);
extern int C_A_D;

int panic_timeout = 0;

void panic_setup(char *str, int *ints)
{
	if (ints[0] == 1)
		panic_timeout = ints[1];
}

NORET_TYPE void panic(const char * fmt, ...)
{
	static char buf[1024];
	va_list args;
	int i;

	va_start(args, fmt);
	vsprintf(buf, fmt, args);
	va_end(args);
	printk(KERN_EMERG "Kernel panic: %s\n", buf);
	if (current == task[0])
		printk(KERN_EMERG "In swapper task - not syncing\n");
	else
{
	sys_sync();
	do_unblank_screen();

	if (panic_timeout > 0)
	{
		/*
		 * Delay timeout seconds before rebooting the machine.
		 * We can't use the "normal" timers since we just panicked..
		 */
		printk(KERN_EMERG "Rebooting in %d seconds.",panic_timeout);
		for(i = 0; i < (panic_timeout*1000); i++)
			udelay(1000);
	#ifdef CONFIG_SCSI_GDTH
		gdth_halt();
	#endif
		hard_reset_now();
	}
	for(;;);
}
}
/*
 * GCC 2.5.8 doesn't always optimize correctly; see include/asm/segment.h
 */

int bad_user_access_length(void)
{
		/* GCC 2.5.8 doesn't always optimize correctly; see include/asm/segment.h */
		/* actually the comment above is for the function, but here we just keep it as is */
		/* Original text had a comment inside the function body, likely misplaced in OCR */
		/* Based on OCR: */
		/*
		 * GCC 2.5.8 doesn't always optimize correctly; see include/asm/segment.h
		 */
		panic("bad_user_access_length executed (not cool, dude)");
}
```

## fork.c

Processes are the heart of running applications on Linux or other UNIX operating systems. When a new process is created, it is forked. The fork() function is defined in the code of fork.c. This way you can see how Linux creates new processes. Listing 6-2 shows how Linux handles forking processes.

### Listing 6-2: Handling forking processes

```c
int do_fork(unsigned long clone_flags, unsigned long usp, struct pt_regs *regs)
{
    int nr;
    int error = -ENOMEM;
    unsigned long new_stack;
    struct task_struct *p;

    p = (struct task_struct *) kmalloc(sizeof(*p), GFP_KERNEL);
    if (!p)
        goto bad_fork;
    new_stack = alloc_kernel_stack();
    if (!new_stack)
        goto bad_fork_free_p;
    error = -EAGAIN;
    rn = find_empty_process();
    if (nr < 0)
        goto bad_fork_free_stack;

    *p = *current;

    if (p->exec_domain && p->exec_domain->use_count)
        (*p->exec_domain->use_count)++;
    if (p->binfmt && p->binfmt->use_count)
        (*p->binfmt->use_count)++;

    p->did_exec = 0;
    p->swappable = 0;
    p->kernel_stack_page = new_stack;
    *(unsigned long *) p->kernel_stack_page = STACK_MAGIC;
    p->state = TASK_UNINTERRUPTIBLE;
    p->flags &= ~(PF_FTRACED|PF_TRACESYS|PF_SUPERPRIV);
    p->flags |= PF_FORKNOEXEC;
    p->pid = get_pid(clone_flags);
    p->next_run = NULL;
    p->prev_run = NULL;
    p->p_ptr = p->p_opptr = current;
    p->pc_ptr = NULL;
    init_waitqueue(&p->wait_chldexit);
    p->signal = 0;
    p->it_real_value = p->it_virt_value = p->it_prof_value = 0;
    p->it_real_incr = p->it_virt_incr = p->it_prof_incr = 0;
    init_timer(&p->real_timer);
    p->real_timer.data = (unsigned long) p;
    p->leader = 0;.../* session leadership doesn't inherit */
    p->ttypgrp = 0;
    p->utime = p->stime = 0;
    p->cutime = p->cstime = 0;
#ifdef __SMP__
    p->processor = NO_PROC_ID;
    p->lock_depth = 1;
#endif

    p->start_time = jiffies;
    task[nr] = p;
    SET_LINKS(p);
    nr_tasks++;
}
```

In Listing 6-2, the processes are defined by what they inherit from their parent process (the process that the child process was forked from) and all its attributes. These include its time, what the process value is, and how the process interacts with other processes.

Listing 6-3 demonstrates error handling in forking. It copies all the process information in case a process is killed or does not function properly.

### Listing 6-3: Forking error handling

```c
    error = -ENOMEM;
    /* copy all the process information */
    if (copy_files(clone_flags, p))
        goto bad_fork_cleanup;

    if (copy_fs(clone_flags, p))
        goto bad_fork_cleanup_fs;
    if (copy_sighand(clone_flags, p))
        goto bad_fork_cleanup_fs;
    if (copy_mm(clone_flags, p))
        goto bad_fork_cleanup_sighand;
    copy_thread(nr, clone_flags, wsp, p, regs);
    p->semundo = NULL;
    /* ok, now we should be set up.. */
    p->swappable = 1;
    p->exit_signal = clone_flags & CSIGNAL;
    p->counter = (current->counter > 1);
    wake_up_process(p);....../* do this last, just in case */
    ++total_forks;
    return p->pid;

bad_fork_cleanup_sighand:
    exit_sighand(p);

bad_fork_cleanup_fs:
    exit_fs(p);
bad_fork_cleanup_files:
    exit_files(p);
bad_fork_cleanup:
    if (p->exec_domain && p->exec_domain->use_count)
        (*p->exec_domain->use_count)--;
    if (p->binfmt && p->binfmt->use_count)
        (*p->binfmt->use_count)--;
    task[nr] = NULL;
    REMOVE_LINKS(p);
    nr_tasks--;
bad_fork_free_stack:
free_kernel_stack(new_stack);
bad_fork_free_p:
kfree(p);
bad_fork:
return error;
}
```

## resource.c

Another important function of the kernel is how it handles the input/output (I/O) of information to devices. The resource.c handles how the I/O is handled by the kernel. It keeps a table of I/O resources, and places new ones in an empty location on the table. Listing 6-4 opens a device driver for loading. When the driver is loaded, it adds the driver to the iotable, where the device drivers are stored.

### Listing 6-4: Handling I/O

```c
/*
* linux/kernel/resource.c
*
* Copyright (C) 1995 Linus Torvalds
*    David Hinds
*
* Kernel io-region resource management
*/

#include <linux/sched.h>
#include <linux/kernel.h>
#include <linux/errno.h>
#include <linux/types.h>
#include <linux/iport.h>

#define IOTABLE_SIZE 128

typedef struct resource_entry_t {
 u_long from, num;
 const char *name;
 struct resource_entry_t *next;
} resource_entry_t;

static resource_entry_t iolist = { 0, 0, "*", NULL };

static resource_entry_t iotable[IOTABLE_SIZE];

/*
 * This generates the report for /proc/ioports
 */
int get_ioport_list(char *buf)
{
    resource_entry_t *p;
    int len = 0;

    for (p = iolist.next; (p) && (len < 4000); p = p->next)
        len += sprintf(buf+len, "%04X-%041X : %s\n",
            p->from, p->from+p->num-1, p->name);
    if (p)
        len += sprintf(buf+len, "*4K limit reached!\n");
    return len;
}

/*
 * The workhorse function: find where to put a new entry
 */
static resource_entry_t *find_gap(resource_entry_t *root,
        u_long from, u_long num)
{
    unsigned long flags;
    resource_entry_t *p;

    if (from > from+num-1)
        return NULL;
    save_flags(flags);
    cli();
    for (p = root; ; p = p->next) {
        if ((p != root) && (p->from+p->num-1 >= from)) {
            p = NULL;
            break;
        }
        if ((p->next == NULL) || (p->next->from > from+num-1))
            break;
    }
    restore_flags(flags);
    return p;
}
```
