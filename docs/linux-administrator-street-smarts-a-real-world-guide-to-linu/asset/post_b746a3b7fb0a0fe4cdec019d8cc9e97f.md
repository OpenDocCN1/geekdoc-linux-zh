
## Starting the Log Book

  You should begin the log book with basic identifying information on the computer—where it was bought, where it resides, what hardware it includes, and so on. You may be able to use some of the hardware identification commands described in Phase 2, “Managing Hardware and the Kernel,” to fill in some of this information.

  You should also include basic software information, such as the Linux distribution you’ve installed, the kernel you’re running (including whether it’s a kernel delivered with the distribution or one you compiled yourself), and any important nonstandard software packages you’ve installed (such as commercial programs or programs developed in-house).

  One type of hardware and software information that may become vital is partition information. You may want to print the output of the partition tables for your hard disks, as revealed by `fdisk -l /dev/hda` and similar commands for other disks, and include those printouts in the log book. Writing the mount points for these partitions next to their printout entries can be a handy addition. This information can become critical if your partition table is ever overwritten; if you’re lucky, you can re-create your existing partition tables based on the printouts.

  You may want to include notes about intended uses for the machine, perhaps including descriptions of particular files and directories. For instance, you might make a note of the fact that `/var/htm1` contains the Web pages served by a Web server computer. Likewise, the fact that the computer uses Apache to serve these Web pages may be a useful addition. Such information may be very well known to you, but if somebody else needs to administer the computer, its presence in the log book could be useful.

  **TIP** Ask yourself if information you record might be helpful in recovering the system in an emergency situation. This could be an attempt to recover an existing system (such as restoring an accidentally wiped partition table) or an attempt to re-create the system from scratch (such as installing Linux from scratch on a new computer if the original was stolen). If information would be helpful, record it. If not, omit it.

## Adding Log Book Entries

  As you administer the system, you should add log book entries. You don’t need to record every trivial thing you do, but you should record information that affects how the computer works in a basic way. For instance, you should probably mention alterations to configuration files, security-related software upgrades, and changes to the hardware installed in the computer.

  **TIP** Rather than record line-by-line changes to configuration files, back up your configuration files to a convenient medium, such as a Zip disk or CD-R. You should have no problem backing up the entire `/etc` directory tree to such media. You can store this configuration backup with your log book so that you can access it easily if the need arises.

### Using the Log Books

  System log books can be helpful in various situations. Some of these are emergency situations, but others involve more mundane and routine operations:

- **Disaster recovery** Most dramatically, if your system is damaged in some way, the log book can be invaluable for learning how it was configured before it was damaged. This can help you bring the system back to a working state by reproducing partition tables, directory layouts, installed software sets, major configuration options, and so on. Of course, proper backups (described in Phase 3) are even more important for disaster recovery, but sometimes log book data can enable you to recover more quickly than restoring a backup would require or can help you determine how to recover the backup (such as how large to make various partitions).
- **System checks** Log books can help you verify that your system is (or is not) working correctly. Recording benchmarks, such as those described in Task 4.2, “Monitor System Performance,” in a log book will enable you to spot when your system begins operating sluggishly. You can also verify that the correct packages are installed. Keeping backups of configuration files can help you spot accidental or malicious changes to those files.
- **System reproduction** Sometimes it’s desirable to reproduce a system without copying it file-by-file. For instance, you might want to give workstations to new employees and configure them in the way that existing workstations are configured. A system log book will help you in this task.
- **Personnel training** When new administrators are hired, system log books can help them become familiar with existing systems and administrative policies.

### Criteria for Completion

  To complete this task, you should create a system log book for your Linux computer. Be sure it includes basic identifying information and major system options. Keeping a disk with the `/etc` directory tree on it with the log book is also helpful. In a real-world situation, the log book will never be complete; it will change as the system changes.

## Task 4.2: Monitor System Performance

  “The computer is slow!” This complaint is a common one in offices and computer centers around the world. Frequently, users aren’t more specific than this, so it becomes your job to figure out precisely where the bottleneck exists—does the computer have too little RAM, are runaway processes sapping CPU speed, has the disk kicked itself into a low-performance mode, or is something else wrong? Keeping track of basic system benchmarks will help you quickly identify the cause of problems when they occur.

### Scenario

  To help you identify problems in the future, you want to record baseline information on your system’s overall performance. You also want to set up a procedure to perform similar tests on a regular basis so you can track system performance and, perhaps, spot trends that might lead to trouble down the road if left uncorrected.

## Scope of Task

  This task involves running several benchmark programs and system information utilities and recording the results in your system log book. You’ll also need to set up a procedure to help you run these tasks on a regular basis in the future.

### Duration

  This task should take about half an hour or an hour to complete. Ongoing performance testing will take a few minutes per test, but you can use `cron` to help automate this task.

### Setup

  Some of the commands described in this task can be performed as an ordinary user, but others require `root` access. Thus, you should log in and acquire `root` privileges. You should have your system log book, which you prepared in Task 4.1, “Maintain a System Log Book,” ready. You may want to print some of these test results rather than copy them by hand, in which case having a working printer will be necessary.

### Caveats

  The usual caveats about working as `root` apply to the commands that require this level of access. Performance tests, although useful, can sometimes be misleading, so you should be alert to results that seem weird—they might indicate a mistyped command or a failure of the utility to produce meaningful results.

### Procedure

  To monitor your system performance, you should be prepared to run a number of different types of tests. Broadly speaking, system performance is determined by three types of hardware: your CPU, your memory (RAM), and your disks (particularly your hard disks). After you perform these tests, you should devise a system to help you perform new tests on a regular basis.

## Testing Your CPU

  Two factors influence your CPU performance: the overall CPU speed and system load. The CPU’s speed is determined by its hardware design and, to a lesser extent, motherboard BIOS settings. Although it’s a poor CPU benchmark, the Linux kernel includes a test of CPU speed, which it calls BogoMIPS. You can find it by searching for that string in the `dmesg` output:

```
$ dmesg | grep Bogo
Calibrating delay using timer specific routine.. 4005.24 BogoMIPS (1pj=2002621)
```
