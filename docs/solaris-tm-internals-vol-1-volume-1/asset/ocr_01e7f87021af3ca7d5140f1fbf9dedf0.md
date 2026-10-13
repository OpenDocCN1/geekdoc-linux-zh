from the callout schedule loop; real-time callouts are handled through the interrupt facility by the `sortinit()` interface.

You can examine the callout table on a running system (all releases) with the callout function in the `crash(1M)` utility.

```
```text
# /etc/crash
dumpfile = /dev/mem, namelist = /dev/ksyms, outfile = stdout
> callout
FUNCTION                 ARGUMENT             TIME                 ID
polltime                 00000030008df260     00000000006a4971     7efffffff7f6f0
realtimexpire            000000300009ed60     00000000006afd39     7efffffff79590
setrun                   0000002a10034fd60    000000000069bd97     3efffffff925a31
schedpaging              0000000000000000     000000000069bddf     3efffffff7c618
mi_timer_fire            0000003000a36820     000000000069bd20     3efffffff7c628
sigalarm2proc            0000003000000af40    000000000069be19     3efffffff7c4e8
ts_update                0000000000000000     000000000069bd4c     3efffffff7c658
seq_update               0000000000000000     000000000069c139     3efffffff7c8b8
kmem_update              0000000000000000     000000000069c139     3efffffff7c069
.
.
.
```
```

Note that the example output from the callout function in `crash(1M)` is not a complete listing. Note, too, that the output is from a 64-bit Solaris 7 system, which is why the ARGUMENT, TIME, and ID columns are 8-byte (64-bit) data types. On a 32-bit kernel, they are 32-bit data types.

Some of the kernel functions that you will consistently find on the callout table of a running Solaris system include the following.

+   - **polltime** — A real-time callout. Set from the `poll(2)` system call and based on the poll interval. `polltime()` wakes up a thread waiting on a poll event.
+   - **realtimexpire** — A real-time callout. Used in the real-time interval timer support when a timer is set. Callout ticks are derived from timer value. `realtimexpire()` generates the SIGALRM to the process.
+   - **setrun** — A real-time callout. Placed on the callout queue by sleep/wakeup code (condition variables) to force a thread wakeup when the sleep event has a timeout value; for example, an `aiowait(2)` call can specify a maximum tick count to wait for the I/O to complete. `aiowait(2)` with a timeout specificity uses a timed condition variable, which in turn places a `setrun()` event on the callout queue to force a thread wakeup if the time expires before the I/O has completed.
+   - **schedpaging** — A normal callout. Part of the pageout subsystem in the VM system, used to manage the pageout rate.
+   - **mi_timer_fire** — A normal callout. Part of the STREAMS-based TCP/IP protocol support. `mi_timer_fire()` generates regular message block processing through a STREAMS queue.