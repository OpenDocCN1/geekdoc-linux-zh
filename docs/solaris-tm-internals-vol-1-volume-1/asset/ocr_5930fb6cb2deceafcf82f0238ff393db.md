ates a watchpoint for read and write access to the bytes occupied by the integer, test.

```
```c
#include <sys/types.h>
#include <sys/fcntl.h>
#include <procf.h>

typedef struct {
        long cmd;
        prwatch_t prwatch;
} ctl_t;

main(int argc, char **argv)
{
        int ctlfd;
        ctl_t ctl;
        int test;

        if ((ctlfd = open("/proc/self/ctl", O_WRONLY)) < 0) {
                perror("open /proc");
                exit (1);
        }

        ctl.cmd = PCWATCH;
        ctl.prwatch.pr_vaddr = (uintptr_t)&test;
        ctl.prwatch.pr_size = sizeof(int);
        ctl.prwatch.pr_wflags = WA_READ|WA_WRITE;

        if (write(ctlfd, &ctl, sizeof (ctl)) != sizeof (ctl)) {
                perror("Set PCWATCH");
                exit (1);
        }

        test = 0;
}
```
```

When we attempt to write to the integer test, we trigger a watchpoint and, by default, the process core dumps.

```
```text
$ ./watchpoint
Trace/Breakpoint Trap (coredump)
```
```

The /proc process information file, prinfo, contains information pertinent to the watchpoint trap and can be read into a struct pr_info. In particular, the si_addr field contains the virtual address of the memory reference that triggered the watchpoint, and the si_code field contains one of TRAP_RWATCH, TRAP_WWATCH, or TRAP_XWATCH, indicating read, write, or execute access, respectively. The si_trapafter field is zero unless WA_TRAPAFTER is in effect for this watched area; nonzero indicates that the current instruction is not the instruction that incurred the watchpoint trap. The si_pc field contains the virtual address of the instruction that incurred the trap. Figure 5.16 illustrates watchpoint data structures.