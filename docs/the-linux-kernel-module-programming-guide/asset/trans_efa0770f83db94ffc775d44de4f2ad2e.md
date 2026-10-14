
wait_event_interruptible。我们本可以使用 wait_event，但那样会导致用户的 Ctrl+C 被忽略，从而让用户极为愤怒。

在这种情况下，我们希望立即返回 -EINTR。这很重要，例如，用户可以在进程收到文件之前将其杀死。

还有一点需要记住。有时进程不想休眠，它们要么想立即得到所需，要么想被告知无法完成。这样的进程在打开文件时会使用 O_NONBLOCK 标志。内核应当从原本会阻塞的操作（例如本例中的打开文件）返回错误码 -EAGAIN 作为响应。程序 cat_nonblock（位于 examples/other 目录中）可用于以 O_NONBLOCK 方式打开文件。

```
$ sudo insmod sleep.ko
$ cat_nonblock /proc/sleep
Last input:
$ tail -f /proc/sleep &
Last input:
Last input:
Last input:
Last input:
Last input:
Last input:
Last input:
Last input:
tail: /proc/sleep: file truncated
[1] 6540
$ cat_nonblock /proc/sleep
Open would block
$ kill %1
[1]+  Terminated      tail -f /proc/sleep
$ cat_nonblock /proc/sleep
Last input:
$
```

```
/*
 * sleep.c - create a /proc file, and if several processes try to open it
 * at the same time, put all but one to sleep.
 */

#include <linux/atomic.h>
#include <linux/fs.h>
#include <linux/kernel.h> /* for sprint() */
#include <linux/module.h> /* Specifically, a module */
#include <linux/printk.h>
#include <linux/proc_fs.h> /* Necessary because we use proc fs */
#include <linux/types.h>
#include <linux/uaccess.h> /* for get_user and put_user */
#include <linux/version.h>
#include <linux/wait.h> /* For putting processes to sleep and
waking them up */
```

```
#include <asm/current.h>
#include <asm/errno.h>

#if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 6, 0)
#define HAVE_PROC_OPS
#endif

/* Here we keep the last message received, to prove that we can process our
 * input.
 */
#define MESSAGE_LENGTH 80
static char message[MESSAGE_LENGTH];

static struct proc_dir_entry *our_proc_file;
#define PROG_ENTRY_FILENAME "sleep"

/* Since we use the file operations struct, we can't use the special proc
 * output provisions - we have to use a standard read function, which is this
 * function.
 */
static ssize_t module_output(struct file *file, /* see include/linux/fs.h */
			     char __user *buf, /* The buffer to put data to
						 (in the user segment) */
			     size_t len, /* The length of the buffer */
			     loff_t *offset)
{
	static int finished = 0;
	int i;
	char output_msg[MESSAGE_LENGTH + 30];

	/* Return 0 to signify end of file - that we have nothing more to say
	 * at this point.
	 */
	if (finished) {
		finished = 0;
		return 0;
	}

	sprintf(output_msg, "Last input:%s\n", message);
	for (i = 0; i < len && output_msg[i]; i++)
		put_user(output_msg[i], buf + i);

	finished = 1;
	return i; /* Return the number of bytes "read" */
}

/* This function receives input from the user when the user writes to the
 * /proc file.
 */
static ssize_t module_input(struct file *file, /* The file itself */
			    const char __user *buf, /* The buffer with input
						 -> */
			    size_t length, /* The buffer's length */
			    loff_t *offset) /* offset to file - ignore */
{
	int i;
```

```
73
74   /* Put the input into message, where module_output will later be able
75    * to use it.
76    */
77   for (i = 0; i < MESSAGE_LENGTH - 1 && i < length; i++)
78       get_user(message[i], buf + i);
79   /* we want a standard, zero terminated string */
80   message[i] = '\0';
81
82   /* We need to return the number of input characters used */
83   return i;
84 }
85
86 /* 1 if the file is currently open by somebody */
87 static atomic_t already_open = ATOMIC_INIT(0);
88
89 /* Queue of processes who want our file */
90 static DECLARE_WAIT_QUEUE_HEAD(waitq);
91
92 /* Called when the /proc file is opened */
93 static int module_open(struct inode *inode, struct file *file)
94 {
95   /* Try to get without blocking */
96   if (atomic_cmpxchg(&already_open, 0, 1)) {
97     /* Success without blocking, allow the access */
98     try_module_get(THIS_MODULE);
99     return 0;
100   }
101   /* If the file's flags include O_NONBLOCK, it means the process does not
102    * want to wait for the file. In this case, because the file is already
103    * open,
104    * we should fail with -EAGAIN, meaning "you will have to try again",
105    * instead of blocking a process which would rather stay awake.
106    */
107   if (file->f_flags & O_NONBLOCK)
108     return -EAGAIN;
109
110  /* This is the correct place for try_module_get(THIS_MODULE) because if
111   * a process is in the loop, which is within the kernel module,
112   * the kernel module must not be removed.
113   */
114  try_module_get(THIS_MODULE);
115
116  while (atomic_cmpxchg(&already_open, 0, 1)) {
117    int i, is_sig = 0;
118
119    /* This function puts the current process, including any system
120     * calls, such as us, to sleep. Execution will be resumed right
121     * after the function call, either because somebody called
122     * wake_up(&waitq) (only module_close does that, when the file
123     * is closed) or when a signal, such as Ctrl-C, is sent
124     * to the process
125     */
126    wait_event_interruptible(waitq, !atomic_read(&already_open));

127  /* If we wake up because we got a signal we're not blocking,
128   * return -EINTR (fail the system call). This allows processes
129   */
```

