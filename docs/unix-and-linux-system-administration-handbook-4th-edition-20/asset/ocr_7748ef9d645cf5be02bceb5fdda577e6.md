# Chapter 8 Storage

Cycle time: min=120ns recommended=120ns
PIO: pio0 pio1 pio2 pio3 pio4
Cycle time: no flow control=120ns IORDY flow control=120ns
.\.\.

On any modern system, the optimal DMA mode should be selected by default; if this is not the case, check the BIOS and kernel logs for relevant information to determine why not.

Many drives offer acoustic management, which slows down the motion of the read/write head to attenuate the ticking or pinging sounds it makes. Drives that support acoustic management usually come with the feature turned on, but that's probably not what you want for production drives that live in a server room. Disabling this feature with hdparm -M 254.

Most power consumed by hard disks keeps the platters spinning. If drives have only occasional use and you can afford to delay access by 20 seconds or as the motors are restarted, run hdparm -S to turn off the disks' internal power management feature. The argument to -S sets the idle time after which the drive enters standby mode and turns off the motor. It's a one-byte value, so the encoding is nonlinear. For example, values between 1 and 240 are in multiples of 5 seconds, and values from 241 to 251 are in units of 30 minutes. hdparm shows you your interpretation of the value when you run; it's faster to guess, and repeat to look up the detailed coding rules.

hdparm includes a simple drive performance test to evaluate the impact of configuration changes. The -T option reads from the drive's cache and indicates the speed of data transfer on the bus, independent of throughput from the physical disk media. The -t reads from the physical platters. As you might expect, physical reads are a lot slower.

```
$ sudo /sbin/hdparm -T /dev/hdX
```

```
/dev/sdX
Tached reads: 2092 MB in 2.00 seconds = 1046.41 MB/sec
Timing buffered disk reads: 304 MB in 3.00 seconds = 101.30 MB/sec
```

100 MB/s is about the limit of today's mass-market 1TB drives, results (and the information shown by hdparm -I above) confirm that the drive is correctly configured.

# Hard disk monitoring with SMART

Hard disks are fault-tolerant systems that use error-correction and intelligent firmware to hide their imperfections from the operating system. In some cases, an uncorrectable error that the drive is forced to report to the OS is merely the latest event in a long crescendo of correctable but inconspicuous problems. It would be nice to know about those things before the crisis occurs.

ATA devices, including SATA drives, implement a detailed form of status reporting that is sometimes predictive of drive failures. This standard, called SMART for