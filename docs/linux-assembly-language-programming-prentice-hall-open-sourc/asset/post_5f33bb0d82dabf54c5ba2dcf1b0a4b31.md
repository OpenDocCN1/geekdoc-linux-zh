
### 11.3.5 Task Switching

The code snippet below illustrates the logic for waking up sleeping processes and managing timers in the context of the `cq` driver.

```c
( ~ _ _ _ )
    cq_area.buffer_offset = 0;
    wake_up(&cq_area.wait_q));
    return; /* No future scheduling done here! */
    }
        add_timer(&cq_timer); /* Continue calling timer handler */
}
```

Processes on the run queue are currently taking turns using the processor. Each time another process on the run queue takes its turn on the processor, there has to be a task switch, of course.

Both `sleep_on()` and `wake_up()` must be called on an argument whose type is `(struct wait_queue **)`, a pointer to a pointer to a wait queue structure. Although this sounds horrible, it is really no problem to set up one of these things. The definition of a `struct wait_queue` is in `/usr/src/linux/include/linux/wait.h`.

But, actually, to use a wait queue, we don’t need to know anything about its internals. As long as we call `wake_up()` on the same pointer that we give to `sleep_on()`, we’re all set. The `wait_q` component of our `struct cq_struct` gives us a (single) pointer to a wait queue structure. Since `cq_write()` uses `sleep_on()` and `cq_timer_handler()` uses `wake_up()`, then the wait queue double pointer must be located in a place where both functions can address it. This is another example where device memory comes in handy. That is why the wait queue pointer is located there. A pointer to this pointer then gives us the argument that we need: `&(&cq_area.wait_q)`.

Program 11.5 shows how the `sleep_on()` and `wake_up()` calls work together. In Program 11.5, `cq_write()` calls `sleep_on()` as soon as it has filled the device buffer in kernel memory. `cq_timer_handler()` wakes up the sleeping `cq_write()` process when it has emptied the device buffer.

Now that we can program the necessary task switches, we are in a position to write a workable driver. Unfortunately, the driver as outlined so far would have a serious failing. It would not respond to what are called *signals*.

### 11.3.6 Signals

Processes in Unix have a handful of different mechanisms available to communicate with each other. One of these is the sending of *signals*. When a process is killed with a Ctrl-C or a `kill` command, the process has received a signal. To explain what a signal is, we need to expand a little on the notion of a task. We have described the task state segment as a region of memory where registers get saved when a task switch occurs. The task state segment is maintained by the hardware. But it is only a *part* of the contextual information that is maintained by Linux for each process. There is a structure called a `struct task_struct` defined in `/usr/src/linux/include/linux/sched.h` which keeps all the information Linux needs on a process. This information is available to the device driver when it is executing in behalf of a process because there is a global variable in kernel memory called `current` whose value is always the task structure for the current process. In the driver for `/dev/cq`, for example, it makes sense to access this variable from `cq_write()` but not from `cq_timer_handler()`. One of the components of `struct task_struct` is `tss`, the hardware’s task state segment. The `pid` component is the Process ID number which shows up when `ps` is run. It is needed when killing jobs from the command line. Another component of `struct task_struct` is `signal`. This component is currently typed as an array of integers. Each bit on each integer in the array can carry a signal. With two 32-bit integers in the array, Linux is configured for a maximum of 64 signals. Whatever the subtle distinctions are between all of these different signals, receiving a signal means just one thing to a device driver: it’s time to quit.

**Drivers that Can’t Be Killed**

The `signal_pending()` call checks the `signal` component of the process for non-zero bits. It is the responsibility of the writer of the device driver to make sure this is done and to go ahead and quit if such bits are found. Failure to do so results in a device driver that can’t be killed. This is an easy mistake to make and a serious one. Multitasking in Linux is sometimes called *cooperative multitasking*. User tasks which execute in the kernel as privileged tasks that are not preemptable. Such a task with kernel privilege, such as `cq_write()`, is expected to yield to the processor voluntarily. If it doesn't, the scheduler won't force it to do so. In order to fulfill this responsibility, the driver must include code such as

```c
if (signal_pending(current))
    return value;
```

at points in the code which will be encountered frequently enough so that waiting for the device driver to arrive at these points as it executes will not cause undue delay.

One more detail needs fixing in order to make sure the driver responds to signals.

### 11.3.7 States of a Process

A very important component of `struct task_struct` is `state`. Its most important values are assigned in `/usr/src/linux/include/linux/sched.h`:

```c
#define TASK_RUNNING 0
#define TASK_INTERRUPTIBLE 1
#define TASK_UNINTERRUPTIBLE 2
#define TASK_ZOMBIE 4
#define TASK_STOPPED 8
```

Tasks which are on the run-queue, i.e. those which are now taking turns using the processor, have `TASK_RUNNING` as the value of their `state` component. When a task puts itself onto a wait queue, `state` may take either `TASK_INTERRUPTIBLE` or `TASK_UNINTERRUPTIBLE` as values. And it makes a big difference.

Although we might reasonably suppose that the difference has to do with interrupts, it doesn't. It has to do with signals.

If `state` has the value `TASK_UNINTERRUPTIBLE`, then its `signal` component will not be altered by a Ctrl-C or a `kill`. Unfortunately, this is the value assigned to `state` by the `sleep_on()` function. Fortunately, there is a closely related function called `sleep_on_interruptible()` which assigns the value `TASK_INTERRUPTIBLE` to `state`. Hence in Program 11.5, the calls to `sleep_on()` and `wake_up()` need to be replaced by their interruptible counterparts. Otherwise we would have the same problem that we would get if we omitted the `signal_pending()` check. The definitions of two `sleep_on` functions are defined in `/usr/src/linux/kernel/sched.c` as well as the main part of `wake_up()`. The two `wake_up` macros are defined in `/usr/src/linux/include/linux/sched.h`.

In the digitizer driver in section 11.4, the `wake_up_interruptible()` macro definition must be consulted to find out the actual function call since the gcc preprocessor isn't used by NASM.

The main features of the Morse Code speaker driver are now in place, so we can do the fun part next.

### 11.3.8 Timing the Morse Code

The timing of dots and dashes is an art, not a science. A Morse Code driver has good timing if it sounds right to a Morse Code practitioner. Time values in this driver are based on the following rules:

- All time values are based on the duration of the `wholenote` component of `cq_area`, which is given in hundredths of a second, or `jiffies`.
- A dash is one-fourth of a `wholenote`.
- A dot is one-sixteenth of a `wholenote`.
- Quiet intervals between dots and dashes of a letter are one-eighth of a `wholenote`.
- Quiet intervals between letters are two-eighths of a `wholenote`.
- Quiet intervals between letters are three-eighths of a whole note.
- A character not included in the Morse Code gets a silent interval of one-quarter of a whole note.

### 11.3.9 Assembly Language Speaker Code

To turn the speaker on and off, the two little assembler routines shown in Program 11.6 are used. Although the bulk of the device driver is written in C, this is often the case. Many times, small routines are coded in assembly language and the rest is coded in a higher-level language.

If the file containing Program 11.6 is called speak.asm, it can then be assembled using NASM:

```bash
linuxbox$ nasm -f elf speak.asm
```

The -f elf switch determines the format of the resulting object code file called speak.o. It should be stored in /usr/src/linux/drivers/char.

# Program 11.6

```nasm
global speaker_on
global speaker_off
extern cq_area
SYSP    equ 61h ; System port for controlling speaker feed
DIVREG  equ 42h ; Port for timer divisor

speaker_off:
        IN AL, [SYSP]
        AND AL, 0FCH
        OUT [SYSP], AL
        MOV EAX, [cq_area]
        OR EAX, 4
        MOV [cq_area], EAX
        RET

speaker_on:
        MOV EAX, [cq_area + 4]
; timervid is offset by 4
        OUT [DIVREG], AL
        SHR EAX, 8
        OUT [DIVREG], AL
        IN AL, [SYSP]
        OR AL, 3
        OUT [SYSP], AL
        MOV EAX, [cq_area]
        AND EAX, 0FFFFFFFBh
        MOV [cq_area], EAX
        RET
```

### 11.3.10 C Language Driver Code

# Program 11.7

```c
#include <linux/errno.h> /* Need this for ENODEV, etc. */
#include <linux/kernel.h> /* Need this for printk() */
#include <linux/major.h> /* Need this for CQ_MAJOR */
#include <linux/sched.h> /* Need this for sleeping and waking */
#include <asm/uaccess.h> /* Need this for copy_from_user() */

#include <linux/cq.h> /* Note the cq file. */

void cq_timer_handler(unsigned long);
static void cq_set_pitch(unsigned long);
static void cq_set_tempo(unsigned long);

void speaker_on(void);
```
