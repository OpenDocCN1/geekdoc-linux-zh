```
8. \n\n",
ircount);
close(fd);
} /* end main */
```

As with many (but not all) UNIX-based operating systems, the kernel at boot time sets this clock chip to interrupt the kernel every n hundredths of a second. Usually, UNIX machines set this value to 100 times per second. In operating systems like Solaris, this value is a tunable parameter. Although it doesn't make sense in fast hardware to let the clock interrupt the kernel less than 100 times per second, it may make sense to let it do so more often (say 1,000 times per second).

Human-readable timekeeping is kernel based and managed with the `gettimeofday()` and `settimeofday()` system calls (e.g. arch/i386/kernel/timer.c). At bootup, the kernel aligns itself to the BIOS (CMOS) clock and subsequently updates its time of day based on the timer interrupt.

Accurate time of day is extremely important in this globalized Internet world; thus the kernel also has a *Network Time Protocol* (NTP) facility, which in conjunction with `xntpd` enables Linux to keep up with high-precision atomic clocks scattered around the world and accessible through the Internet. The very complex and very accurate NTP protocol itself is implemented by `xntpd`. The kernel provides functionality to speed up and slow down the flow of time without introducing user-visible time warps or time jumps. An example of such a Linux system coupled to an atomic clock is:

```
[mingo@s]$ date
Tue Jan 4 13:22:19 CET 2000
[mingo@s]$ ntptrace
localhost: stratum 4, offset -1.113059, sync distance 0.15135
goliath.eik.bme.hu: stratum 3, offset -1.039804, sync distance 0.05267
maze.bme.hu: stratum 2, offset -1.134906, sync distance 0.06520
hora.cs.tu-berlin.de: stratum 1, offset -1.132075, sync distance 0.00023, refid 'GPS'
```

The Linux box above is synchronized over multiple NTP servers with an atomic clock that sends it an interrupt every *n* milliseconds. On the i386 architecture, this value is usually set to 10 milliseconds. In other words, the kernel will wake up 100 times per second. The accuracy of NTP is to within 100 microseconds.