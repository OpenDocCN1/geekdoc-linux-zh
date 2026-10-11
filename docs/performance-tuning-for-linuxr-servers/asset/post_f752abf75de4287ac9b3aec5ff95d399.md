
## References

- gnuplot: http://www.gnuplot.org/.
- gprof: http://sources.redhat.com/binutils/docs-2.12/gprof.info/index.html.
- Hinton, Glenn, et al. "The Microarchitecture of the Pentium 4 Processor," http://www.intel.com/technology/iti/q12001/pdf/art_2.pdf.
- Luo, Yue, et al. "Benchmarking Internet Servers on SuperScal ar Machines," Computer, February 2003, pp. 34-40.
- Kernprof: http://oss.sgi.com/projects/kernprof.
- netstat: http://www.ussg.iu.edu/usail/man/linux/netstat.8.html.
- nfsstat: http://www.die.net/doc/linux/man/man8/nfsstat.8.html.
- oprofile: http://oprofile.sourceforge.net/doc.
- Performance Inspector: http://www-124.ibm.com/developerworks/opensource/pii/.
- Readprofile: http://nodevice.com/sections/ManIndex/man1303.html.
- sysstat: http://perso.wanadoo.fr/sebastien/godard/.
- strace: http://sourceforge.net/projects/strace.
- Stallings, William. Computer Organization and ArchitectureDesigning for Performance, Sixth Edition. Prentice Hall, 2003.
- tcpdump: http://www.die.net/doc/linux/man/man8/tcpdump.8.html.
- top: http://nodevice.com/sections/ManIndex/man1818.html.
- Intel VTune: http://www.intel.com/software/products/vtune/.
- vmstat: http://nakula.rvs.uni-bielefeld.de/cgi-bin/man.sh?man=8+vmstat.
- Web resource: http://www.ping127001.com/pingpage.htm.
- Web resource: http://www.ethereal.com/docs/man-pages/tcpdump.8.html.
- Web resource: http://csrc.nist.gov/tools/tools.htm.
- Web resource: http://www.ripe.net/ripepcc/pub-services/db/irrtoolset/.
- Web resource: http://www.insecure.org/tools.html.
- Tanenbaum, Andrew. Computer Networks, Third Edition. Prentice Hall, 1996.

## Chapter FIVE. System Trace Tools

By Ron Cadima, Gerrit Huizenga, Duc J. Vianney, and Peter Wai Yee Wong

### Introduction

When a performance bottleneck or problem occurs, system tracing tools can help you identify the source of the problem. When tracing a system, you need to know not only which tools to use, but when and where to use them.

Generally, system tracing involves multiple steps: With each step, you delve deeper into the problem to ultimately create a solution or optimize the system or the appropriate application. By taking a system-wide view of the problem first, and then zeroing in on a specific application or series of events, you can more reliably determine the true cause of the performance problem. For example, just because the system slows down after a particular application is started does not necessarily mean the application is the cause of the slowdown. The application might be a catalyst that exposes a problem within another application on the system.

A number of Linux tracing tools are available in the open-source community. This chapter discusses several of the most common:

- `top`, which gives an overall picture of what processes are using the system and the system resources they are using
- `strace`, which traces all the system calls from an application
- `Oprofile`, which provides the profile of a running system based on system timer or performance counter support, including the amount of time the system spends within an application
- `Performance Inspector`, which is a suite of tools for identifying performance problems and characteristics

This chapter also discusses requirements that need to be met before you begin tracing a system.

Note that given the dynamic nature of Linux, new system tracing tools are likely to be developed, and existing tools, including the ones discussed in this chapter, will continue to be updated.

### Requirements for System Tracing

To capture useful information for troubleshooting a performance problem, follow these guidelines before you begin to trace a system:

- Use the right tool for the right step of your analysis. If the data that the tool you use is not reliable because it is the wrong tool for the job, your time is wasted analyzing the wrong data or application.
- Ensure that the system that is being traced has enough memory and storage. For example, if there is not enough memory, swapping occurs, which can distort the results.
- Know the overhead of the tool you are using. If the tool is very intrusive into your system, the performance analysis might be inaccurate.
- Use a defined test scenario to make your measurements. It is imperative that you use a consistent set of steps for the measurements and that the results are repeatable. Measure the same functions in the same order during each step of the analysis.
- Use a controlled environment. Do not allow other processes or functions to be performed during the measurements and traces unless they are part of the measurement scenario. After you have applied fixes based on the results of the measurements and traces, you can begin a new round of testing with new applications added to the mix. The best rule of thumb is to keep the scenario simple and know what is running when.

### The top Utility

The `top` utility is shipped on most platforms and with most releases of Linux. `top` reports on processor activity in real time and is most useful for obtaining an overall picture of the processes that are using the system and the resources they are using. `top` lets you specify the delay between measurements and the number of measurements to take. `top` also allows a batch mode of operation that writes the data in a normal text format. Another option to `top` lets you specify that the only processes that are displayed are those that are actually running.

`top` reports the approximate amount of memory a process is using. You can configure `top` to show a process hierarchy.

Use `top` as a first step in your analysis to see which processes are running in the system and how much of the system time they are consuming. By running `top` over a period of time and directing the output to a file, you can see which processes are running when. You can also approximate when a process stops, when large amounts of memory are consumed, and when one or two processes start to consume large amounts of processor time. For example, if `top` output indicates that a particular process is consuming most of the processing time, you can use other tools to identify the location within the application where the time is being consumed. The same holds true for memory usage. If a large amount of memory is suddenly being consumed or a gradual buildup in memory consumption has occurred, use a lower-level trace tool to identify where the increase in memory usage is occurring.

The following is a sample of the `top` report. The display is updated by default every 5 seconds.

```
# top

8:24 am  up 4 days, 19:31,  1 user,  load average: 0.16, 0.06, 0.09
 57 processes:  55 sleeping, 2 running,  0 zombie, 0 stopped
CPU states:  2.1% user,  0.6% system,  4.0% nice,  4.3% idle
  Mem:  252976k av, 21516k used, 41460k free,      0k shrd,  29820k buff
 Swap:  522072k av,  27060k used, 495012k free          76836k cached

  PID USER     PRI   NI SIZE  RSS SHARE STAT %MEM %CPU   TIME COMMAND
 20269 root      16  224  224  188  188  R  98.4  0.0  0:09 pi_watch
 20270 root     10    0 1040 1040  828  R   1.9   0.4  0:00 top
   1 root      9    0  464  428  412  S   0.0   0.1  0:00 init
   2 root      9    0    0    0    0  SW  0.0   0.0  0:00 keventd
   3 root     19   19   0    0    0  SWN 0.0   0.0  0:00 ksoftirqd_CPU0
   4 root      9    0    0    0    0  SW  0.0   0.0  0:09 kswapd
   5 root      9    0    0    0    0  SW  0.0   0.0  0:00 bdflush
   6 root      9    0    0    0    0  SW  0.0   0.0  0:02 updated
   8 root      9    0    0    0    0  SW  0.0   0.0  0:00 khubd
  10 root     -1  -20   0    0    0  SW  0.0   0.0  0:00 mdrecoveryd
  14 root      9    0    0    0    0  SW  0.0   0.0  0:14 kjournald
 127 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 128 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 129 root      9    0    0    0    0  SW  0.0   0.0  0:00 kjournald
 428 root      9    0  536  528  456  S   0.0   0.2  0:00 syslogd
 432 root      9    0  428  412  376  S   0.0   0.1  0:00 klogd
 449 rpc      9    0  560  556  484  S   0.0   0.2  0:00 portmap
 468 rpcuser   9    0  660  576  576  S   0.0   0.2  0:00 rpc.statd
 581 root      9    0  972  732  732  S   0.0   0.2  0:00 sshd
 594 root      9    0  716  588  588  S   0.0   0.2  0:00 xinetd
 615 root      9    0 1644 1260 1068  S   0.0   0.4  0:14 sendmail
 624 smmsp     8    0 1176  772  688  S   0.0   0.3  0:00 sendmail
 634 root      9    0  400  368  352  S   0.0   0.1  0:14 gpm
 643 root      9    0  604  564  528  S   0.0   0.2  0:00 crond
 674 xfs      9    0  6136  4  552 1032  S  0.0  1.7  0:06 xfs
```
