
main storage pages, and the situation is so severe that it will steal them from any user. Ultimately, whether they are inactive, in queue, or active, it eventually even steals pages from shared segments and the CP system process.

In short, the system is in a critical mess, storage wise. This also covers stealing pages from the monitor and MONDCSS, two critical performance-related entities, and in this event, performance monitoring and reporting may be compromised or interrupted.

| Example 11-9 | Example performance toolkit reporting emergency scanning (ESC) |
|---|---|
| FCX101 | CPU 2094 SER 2991E Interval 03 : 10:00 -- 03 : 49:21 Perf. Monitor |
| TIME > PPA G%ST AL0/S FPGS %FR SHAR #TWC ESCN %P G S L % S P S L XSTAV %XS XAL/S XAG |
| 15 : 58 | 1000k | 105 | 8 | ... | 0 | 66k | 0 | 100 | 14 | 66 | 1024M | 99 | 15 | 476 |
| 15 : 59 | 1000k | 105 | 7 | ... | 0 | 66k | 0 | 100 | 14 | 66 | 1024M | 99 | 22 | 568 |
| 16 : 00 | 1000k | 105 | 54 | ... | 0 | 66k | 0 | 92 | 14 | 66 | 1024M | 99 | 163 | 191 |
| 16 : 01 | 1000k | 105 | 22 | ... | 0 | 66k | 0 | 100 | 14 | 66 | 1024M | 99 | 68 | 200 |
| 16 : 02 | 1000k | 105 | 14 | ... | 0 | 66k | 0 | 100 | 14 | 66 | 1024M | 99 | 38 | 267 |
| 16 : 03 | 1000k | 105 | 5 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 25 | 367 |
| 16 : 04 | 1000k | 105 | 1 | ... | 0 | 67k | 0 | .. | 14 | 66 | 1024M | 99 | 0 | 654 |
| 16 : 05 | 1000k | 105 | 6 | ... | 0 | 67k | 0 | .. | 14 | 66 | 1024M | 99 | 0 | 12 |
| 16 : 06 | 1000k | 105 | 8 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 22 | 928 |
| 16 : 07 | 1000k | 105 | 5 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 14 | 11 |
| 16 : 08 | 1000k | 105 | 4 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 9 | 13 |
| 16 : 09 | 1000k | 105 | 5k | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 10 | 14 |
| 16 : 10 | 999k | 105 | 5 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 17 | 13 |
| 16 : 11 | 1000k | 105 | 6 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 11 | 13 |
| 16 : 12 | 1000k | 105 | 5 | ... | 0 | 67k | 0 | .. | 14 | 66 | 1024M | 99 | 0 | 22 |
| 16 : 13 | 1000k | 105 | 1 | ... | 0 | 67k | 0 | 100 | 14 | 66 | 1024M | 99 | 17 | 16 |

Usually an emergency scanning problem is detected when there are one or two guests (Linux servers) consuming the majority of the system pages available for allocation to the guest.

Also, some parts of VM 64-bit releases were still operating in 31-bit mode, which implies an upper addressability limit of 2 GB. This could cause certain runtime issues when running Linux guests, for example, when they were performing I/O. Linux has the unfortunate tendency to grab and hold on to all of the memory allocated to it, which sometimes leads to a large part of it being misused for internal I/O buffer and cache.

Linux guests, where a virtual storage equal to or greater than 2 GB is defined, are now common on many systems. In order to perform real I/O in this particular scenario prior to VM v5.2.0, the system needed to use areas below the requesting virtual machine 2 GB line, and, as these were already in use by the virtual machine itself, the system had to resort to emergency scanning to find the storage pages that it required to complete the I/O task.

Figure 11-8 shows where there is heavy emergency scanning happening during the same time period as when we noted that there is some expanded storage paging.

![](img/f332344337ca8bf6846cb313a66ee0b3_346_0.png)

*Figure 11-8 Example emergency scanning compared with exp storage page rate*

Figure 11-9 shows an increase in the page rate. At the same time, we can see that z/VM has entered in to emergency scanning mode for release pages.

![](img/f332344337ca8bf6846cb313a66ee0b3_347_0.png)

**Note:** Starting z/VM v5.3.0 introduced more important enhancements to CP storage management. Page management blocks can now be positioned above the 2 GB line. Contiguous frame management has been further refined, and fast available list searching was introduced in this release. For more discussion on this see:

http://www.ibm.com/perf/reports/zvm/html/530stor.html

From the above investigation, it is clear that the Linux guest (application server) is heavily committed in terms of memory within a 3 GB virtual machine, by defining a very large heap size for running the WebSphere Application Server. Some steps that you can take to generally tune your system and help avoid ESCN where it does still arise can be found at:

http://www.vm.com/perf/tips/2gsstorag.html

## Related publications

The publications listed in this section are considered particularly suitable for a more detailed discussion of the topics covered in this book.

### Online resources

These Web sites are also relevant as further information sources:

- For more information about IBM z/VM:
  - [http://www.vm.ibm.com](http://www.vm.ibm.com)
- The dbginfo.sh script is available for download from IBM developerWorks:
  - [http://www.ibm.com/developerworks/linux/linux390/s390-tools-l.6.1.html](http://www.ibm.com/developerworks/linux/linux390/s390-tools-l.6.1.html)
- System status tool:
  - [http://pagesperso-orange.fr/sebastien.godard/](http://pagesperso-orange.fr/sebastien.godard/)
- Linux man pages:
  - [http://linuxcommand.org](http://linuxcommand.org)
- Installing Oprofile:
  - [http://oprofile.sourceforge.net/doc/install.html](http://oprofile.sourceforge.net/doc/install.html)
- GDB: The GNU Project Debugger:
  - [http://www.gnu.org/software/gdb/](http://www.gnu.org/software/gdb/)
  - [http://sourceware.org/gdb/documentation/](http://sourceware.org/gdb/documentation/)
- For SLES10 information:
  - [http://www.novell.com](http://www.novell.com)
- For RHEL5 information:
  - [http://www.redhat.com](http://www.redhat.com)

## How to get Redbooks

You can search for, view, or download Redbooks, Redpapers, Technotes, draft publications and Additional materials, as well as order hardcopy Redbooks, at this Web site:
`ibm.com/redbooks`

## Help from IBM

IBM Support and downloads
`ibm.com/support`

IBM Global Services
`ibm.com/services`

# Index

**Symbols**
- [[X[GEN_DON[_EDIT]_THIS]! 109–117, 119, 121, 123–125, 127, 131–132, 135–137, 142–143, 146, 151, 153, 157–162

**A**
- Application layer 92

**B**
- barrier-based sync 302
- blks 268, 299
- boot process 267
- boot.multi path 219
- bottom line 41

**C**
- cached 60
- Case study 263
- central storage (CS) 328
- Channel Subsystem 72
- command privilege (CP) 234
- Common I/O Layer 245
- complex problem 16
- configuration file 270
- per-host basis 270
- Consensus term 15
- control program (CP) 22
- Core Dump
  - classic example 88
- Core dump 87
- CP command
  - trace 28
- CPU
  - basis 180
  - time 180
  - type 23
  - utilization 53, 63, 170
- cpu time 235

**D**
- DASD
  - device 80, 213, 292
  - getting I/O statistical information 72
  - statistics option 69
- dasd driver 196
- DASD dump 213
- DASD Static 196
- DASD volume 43, 83
- ordered list 43
- dasdview command 214
- DB2 database 224, 315
- DB2 Server 317
- Dec 18 19
- 19
- 04 xxxxxxxx kernel 257
- default ERP 246
- device 0,0,3600 264
- Device D437 49
- Detailed Analysis 49
- device driver 104, 244–245
- device file 244, 247
- Diag. X98 47, 225
- disk B 34
- disk I/O
  - bottleneck 192
  - operation 192
- disk storage (DS) 188
- dispatch list 26, 234
- dmesg command 297
- dmesg print 298

**E**
- elig 44, 224
- Eligible List
  - class users 235
- eligible list 26, 234
- EME 45, 225
- end user 164, 239
- Environment setup 89
- error message 6, 256, 322
- error recovery 199, 250
  - action 200
- ESA 45
- etc/init.d/boot.script 295
- EXPAN-001 E2-00000 24, 236
- EXPAN-001 E3-00000 24, 236
- Expanded storage
  - comparative chart 326
  - expanded storage (ES) 23, 185, 324
- ext3 filesystem 180, 300
- EXT3 FS 302
- Extended IPv6 support 279
- Extended Link Service (ELS) 259

**F**
- FCP connection 193, 258
- FCP device
  - recognition 261
- FCP LUN 76
  - I/O statistics 80
- FCP port 261
- file system 8, 290, 292
- filesystem cache 189
- filesystems 306
- Firewall rule 279
- follow-up action 1, 17
- fsck command 292

**G**
- granular information 21, 59
- Graphical Data Display Manager (GDDM) 39

**H**
- H/W error 257
- H/W problem 260
- H/W trouble 308
- HCPGIR450W CP 35, 308
- Host Bus Adapter (HBA) 198
- HTTP server 314

**I**
- I/O act 47, 225
- I/O activity 67, 198
- I/O device
  - load 42, 196
  - performance 38
- I/O interruption 246
- I/O load 38
- I/O operation 170, 245, 325
- I/O rate 44, 224
- I/O request 247
- I/O time 70, 197
- IBM Tivoli OMEGAMON XE 52
- IBM z/VM
  - Performance Toolkit 21, 42, 323
- IBM z/VM Performance Toolkit
  - feature 38
  - initial screen 41
  - main menu 50
  - main screen 42
  - menu 45
- IBM z/VM Performance Toolkit commands
  - redisip 60
- Ideal size 228
- Init phase 286, 292
- little bit 293
- Initial Program Loader (IPL) 287
- initial set 43
- Input/output (I/O) 61, 181
- Inter process communication (IPC) 67
- IP address 280
- IP Forwarding 296
- IPL address 308
- IPL device 287
- IWLO046W HTTP 318

**J**
- JVM side 185

**K**
- kernel panic 35, 81
  - system crashes 81
- Kernel phase 290
- kernel space
  - callgraph feature 75
- kernel version
  - 2.6.16.21 76
  - 2.6.5 76
- ksoftirqd 180

**L**
- Linux 4, 21, 55, 59, 163, 211, 243, 270, 286, 313
- Linux commands
  - dasdview 213
  - lscss 212
  - Isdasd 213
