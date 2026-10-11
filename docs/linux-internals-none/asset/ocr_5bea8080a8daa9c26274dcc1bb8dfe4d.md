```
8 #include <linux/binfmts.h>
9 #include <linux/personality.h>
10 #include <linux/threads.h>
11 #include <linux/kernel.h>
12 #include <linux/types.h>
13 #include <linux/times.h>
14 #include <linux/time.h>

16 #include <asm/system.h>
17 #include <asm/semaphore.h>
18 #include <asm/page.h>
19 #include <asm/ptrace.h>

21 #include <linux/smp.h>
22 #include <linux/tty.h>
23 #include <linux/sem.h>
24 #include <linux/signal.h>
25 #include <linux/securebits.h>

27 /**
28 * cloning flags:
29 */
30 #define CSIGNAL    0x000000ff   /* signal mask to be sent at exit */
31 #define CLONE_VM   0x00000100   /* set if VM shared between processes */
32 #define CLONE_FS   0x00000200   /* set if fs info shared between processes */
33 #define CLONE_FILES  0x00000400 /* set if open files shared between processes */
34 #define CLONE_SIGHAND 0x00000800 /* set if signal handlers shared */
35 #define CLONE_PID    0x00001000   /* set if pid shared */
36 #define CLONE_PTRACE  0x00002000 /* set if we want to let tracing continue on the child too */
37 #define CLONE_VFORK  0x00004000   /* set if parent wants the child to wake it up on mm_release */
38 #define CLONE_PARENT  0x00008000  /* set if we want to have the same parent as the cloner */

40 /**
41 * These are the constant used to fake the fixed-point load-average
42 * counting.  Some notes:
43 * - 11 bit fractions expand to 22 bits by the multiplies: this gives
44 * a load-average precision of 10 bits integer + 11 bits fractional
45 * - if you want to count load-averages more often, you need more
46 * precision, or rounding will get you.  With 2-second counting freq,
47 * the EXP_n values would be 1981, 2034 and 2043 if still using only
48 * 11 bit fractions.
49 */
50 extern unsigned long avenrun[];     /* Load averages */
51 
52 #define FSHIFT       11    /* nr of bits of precision */
53 #define FIXED_1      (1<<FSHIFT) /* 1.0 as fixed-point */
54 #define LOAD_FREQ    (5*HZ) /* 5 sec intervals */
55 #define EXP_1        1884   /* 1/exp(5sec/1min) as fixed-point */
56 #define EXP_5        2014   /* 1/exp(5sec/5min) */
```