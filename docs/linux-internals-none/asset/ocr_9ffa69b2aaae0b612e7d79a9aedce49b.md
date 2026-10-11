moon:~/l> ./lat_sig catch
Signal handler overhead: 3.186 microseconds

Best of all, it scales linearly on SMP:

moon:~/l> ./lat_sig catch & ./lat_sig catch &
Signal handler overhead: 3.264 microseconds
Signal handler overhead: 3.248 microseconds

moon:~/l> ./lat_sig install & ./lat_sig install &
Signal handler installation: 1.721 microseconds
Signal handler installation: 1.689 microseconds

# ## Signals and Interrupts, a Perfect Couple

Signals can be sent from system calls, interrupts, and bottom-half handlers alike; there is no difference. In other words, the Linux signal queue is interrupt safe, as strange and recursive as it sounds. So it’s pretty flexible.

An interesting signal-delivery case, however, is on SMP: imagine a thread is executing on one processor, and it gets an asynchronous event (e.g. synchronous socket I/O signal) from an IRQ handler (or another process) on another CPU. In that case we send a cross-CPU message to that running process, so there is no latency in signal delivery. The speed of cross-CPU delivery is about 5 microseconds on a 350MHz Pentium II.

# ## Data Structure—include/linux/signal.h

```
```
1  #ifndef _LINUX_SIGNAL_H
2  #define _LINUX_SIGNAL_H
3
4  #include <asm/signal.h>
5  #include <asm/siginfo.h>
6
7  #ifdef _KERNEL_
8  /*
9   * Real Time signals may be queued.
10  */
11
12  struct signal_queue
13  {
14          struct signal_queue *next;
15          siginfo_t info;
16  };
17
```
```