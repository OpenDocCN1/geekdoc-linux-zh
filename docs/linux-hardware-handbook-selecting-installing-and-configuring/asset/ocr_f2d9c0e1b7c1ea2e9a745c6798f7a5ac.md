![](bbox=[0.25, 0.06, 0.75, 0.35])

# Figure 5.4

*Latencies involved in the movement of hard drive components are responsible for hard disk data transfer rates.*

Seek time, latency, and access time are all measured in milliseconds (ms). Hard disks in 2000 have seek times of 5ms–10ms and spin at between 5,400 and 10,000 rpm, for average latencies of 3ms–6ms (lower latencies being associated with higher spin rates). The main point to keep in mind with respect to seek time, latency, and access time is that smaller numbers are better. Keep in mind the difference between seek time and access time, too. Sometimes you’ll find one vendor advertising seek time while another promotes access time, but these values are not directly comparable. If you know the spin rate of the two drives, you can convert one to the other quite easily, of course, but you must be aware of the difference in the first place.

# ## Disk Transfer Rates

The second major statistic of importance in comparing hard disks is the disk transfer rates—how quickly the disk can transfer data to and from the computer. Note that I referred to disk transfer *rates* (plural). There are two reasons for this:

+   - The disk spins at the same rate no matter what cylinder is being read, but modern hard drive designs place more sectors along outer cylinders than along inner ones. This means that data read from the outer cylinders transfer faster than do data read from inner cylinders. Hence, the internal data transfer rate is variable.
+   - The data transfer rate from the platters is potentially different from the data transfer rate between the hard disk and the computer. The latter rate is determined by the computer’s interface type, such as 66MBps for an Ultra-66 interface. The former is determined by data density on the platter and the speed with which the platter spins.

Hard disk manufacturers generally try to emphasize the external transfer rate—the speed of the hard disk’s interface. This transfer rate, however, is far less important than the *internal* transfer rate—that rate of information transfer from the disk platters to the drive electronics.