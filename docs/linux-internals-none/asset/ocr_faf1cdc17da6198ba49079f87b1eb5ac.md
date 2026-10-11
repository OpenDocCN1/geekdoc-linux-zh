# Processes

The most central concept in any operating system is the user process: an abstraction of a running program.<sup>1</sup>

As we saw earlier, Linux is a multitasking operating system and is therefore able to run several such user processes at once, even on a uniprocessor system. Every operating system with this capability needs a system to keep track of the various processes. The system makes sure that the processes get all the resources they need on time, but on a fair basis and without jeopardizing overall system stability. It also needs to do this efficiently, to reduce the impact of this managing activity to the lowest level possible. That model and its uses are the subject of this chapter.

The fundamental data structure within the kernel, controlling all processes, is the *process structure*, which grows and shrinks dynamically as processes are forked and finish or are killed. The process structure (called `task_struct` in the kernel source code) is around 1k in size. On a system with 1,300 processes, the `task_struct` table takes about 1,300 KB of real memory. You can get the exact size of the structure with the following simple C program:

```
```
#define __KERNEL__
#include <linux/sched.h>
main()
{
 printf("sizeof(struct task_struct) -> %d\n", sizeof(struct task_struct));
}
```
```

On IA32 (i386) machines the process structure is exactly 960 bytes in size. The data structure of `task_struct` is reported at the end of this chapter for reference. Unlike other UNIX implementations, however,