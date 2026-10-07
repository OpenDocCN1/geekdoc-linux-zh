
them, and depend on the results. Evaluate the system load, configuration, and appropriateness of the hardware/software combination for the task. Ensure that the systems are as equal as you can make them, and then use the benchmarks for guidance.

## Selecting Hardware

There are many factors that determine how well a computer system will perform. Certainly the hardware plays a large part. Older or less capable hardware generally slows down a system. Anyone who has upgraded from a low-end processor to a top-rated processor can tell you the significance of the upgrade. Everything seems to go faster, even though only some functions have actually sped up. Now try running poorly configured software on a state-of-the-art machine. It runs better than on lesser hardware, but it is not the best that it can be. Reconfiguring will make a great difference provided that the hardware can handle the system load. Optimized software on low-end hardware is similarly disappointing. The trick is to optimize the software on the best hardware for the intended task.

Just as a car's engine can determine how fast it will go, the hardware components in your Linux system determine how it will perform. We'll look at the minimum acceptable hardware for a Linux system and some example architectures for different types of Linux systems. We'll also discuss some issues to consider in achieving optimal performance.

### Minimal Acceptable Hardware

One of the best-known facts about Linux is that it can make use of old computer parts that you have stored away somewhere. Many a high school student has salvaged an old 80386 machine and turned it into a decent print server or mail server. Originally, Linux was designed to install on an 80386 with as little as 4MB of memory, but with the rapid changes in processor speed and memory size, designing anything to work with only 4MB of memory became unnecessary. Red Hat requires at least 32MB of memory (recommends a minimum of 64MB) and 350MB (recommends a minimum of 650MB) of hard drive space (without X) for its 7.3 release. Other distributions have slightly different recommended requirements, but these don't reflect differences in the needs of identically configured systems; rather, they reflect differing default installations and usage assumptions.

Below is some basic information about selecting performance-oriented hardware for a Linux system.

### CPU Performance

One of the most important elements in determining a computer's performance is the Central Processing Unit (CPU). A new CPU seems to hit the market almost weekly. In the Intel-compatible x86 market, there are basically four players: Intel, Advanced Micro Devices, Inc. (AMD), VIA (which bought Cyrix in 1999), and startup Transmeta. New faces are appearing in the microprocessor technology market, but many target architectures other than the x86. Linux is known to run on all of those listed here:

- Intel/AMD/Cyrix 386SX/DX/SL/SLC/SLC
- Intel/AMD/Cyrix 486SX/DX/SL/SX2/DX2/DX4
- IDT WinChip
- NexGen NX586
- Cyrix 6x86, 6x86MX, and M-II
- VIA Cyrix III
- AMD K5, K6, K6-2, K6-III
- AMD K7/Athlon (including the Duron series)
- Transmeta Crusoe
- Intel Pentium and Pentium MX
- Intel Pentium Pro
- Intel Pentium II (including the Celeron series)
- Intel Pentium III
- Intel Pentium IV

Note IDT and NexGen were bought out by VIA and AMD, respectively. Transmeta CPUs have yet to become popular, but they're poised to make inroads in portable devices because of their low power requirements. Many third parties resell CPUs under their own names, often with adapter boards to make the CPUs work on a wider range of motherboards than originally intended.

The current leaders of the market are the Intel Pentium IV and the many varieties of AMD K7 Athlon processors including the Athlon, the Athlon MP, the Athlon XP, and the Athlon 4 for notebooks. For information on Intel processors look at http://www.intel.com/; for AMD, the site is http://www.amd.com. Comparisons between the two are available on each site and independent comparisons may be found using your favorite search engine. Historically, Intel has been the market leader, with AMD playing catch–up, but in some specific applications like video rendering, AMD has been benchmarked as faster. Because the competition between Intel and AMD is ongoing and because each has its strengths and weaknesses, it is better to look at the functions a computer will be asked to perform and read all available comparisons between the processors you are considering before choosing. Although Linux also supports VIA Cyrix chips, they are not really competitive with their AMD and Intel counterparts. VIA Cyrix processors will give you no problems in Linux, but if it's performance you're looking for, look to the Athlon or Intel processors.

Linux also runs on a wide variety of non–x86 CPUs. Of particular interest, the Linux ports to the PowerPC (PPC), Alpha, and SPARC CPUs are all mature, and all these CPUs are supported by several Linux distributions. But unless you need an unusual feature of one of these CPUs (such as extraordinary floating–point power), you're probably better off going with an x86 CPU for Linux use, because x86 hardware is inexpensive and Linux is still best supported on x86 systems. If you've got an existing Macintosh or Alpha box, though, and want to run Linux on it, you can certainly do so.

### Random Access Memory

There are two main categories of Random Access Memory (RAM): system and video. Although video RAM is important in issues of rendering speed and graphic resolution, system RAM affects the performance of all software, whether or not it is graphics-intensive. There are several types of RAM on the market today. Of course, if you have a motherboard selected already, your RAM type will be dictated by the type supported by that motherboard. If you haven't, however, you may find yourself wading through the many subcategories of RAM available today. As of this writing, synchronous dynamic RAM (SDRAM) and Rambus dynamic RAM (RDRAM), and Double Data Rate (DDR) Ram are the most common types of system RAM, DDR being the fastest. Older systems used ordinary dynamic RAM (DRAM) or variants of it.

Whenever possible, you should buy memory modules in the largest amounts that will support your configuration. For instance, if there are four slots that will accept up to 256MB modules, it would be better to buy two 256MB modules than four 128MB modules, since the former allows for system growth without forcing you to replace existing modules. You can later add two more 256MB modules for a total of 1GB instead of having to pull out the four 128MB modules and add four 256MB modules. Plan the most efficient upgrade path when you purchase computer components.

We’ve just outlined the bare–minimum hardware required to run Linux. As a system administrator, your job is to develop systems that are performance–oriented rather than just inexpensive, so you’ll probably want more than the minimum. The next section describes system hardware requirements in terms of the tasks that a given system needs to perform.

## Selecting Hardware by Intended Usage

Now that we’ve seen the minimum hardware required for any Linux system, we can look at three different categories of computer—a low-end workstation, a high-end graphics workstation, and a basic server—and the minimal requirements for serving those roles effectively. These are opinions based on our own experience. As Linux users often say, your mileage may vary. Use our experience as a guideline, keeping in mind that the minimum requirements may be insufficient if the system load becomes unusually high. We have tried to allow for a high system load, but at some point, a more capable CPU, more memory, and/or hard drive space might be required. Always consider the work being done and which parts of the system are being stressed the most. Look to Chapter 16 for more optimization techniques and ways to determine when the current system is overly taxed, and upgrade components as needed.

### Configuration A: A Basic Workstation

The first configuration we’ll look at is pretty much the minimum for any system that you will purchase. Configuration A is a workstation used primarily for word processing:

- Pentium II or AMD K6 CPU
- 64MB of RAM
- CD-ROM drive
- Floppy drive
- 20GB hard drive (IDE or SCSI)
- SCSI disk controller (if appropriate)
- SVGA graphics card with at least 8MB of video RAM
- Ethernet card (10BaseT or as appropriate)
- 15-inch SVGA monitor

The hardware in this configuration is available for very little money overall. There is really no reason to buy less than this. We consider 64MB of memory to be the minimum because most systems come with this amount by default. Sometimes a system will come with only 32MB of memory, but with a little extra effort you can usually find a system with 64MB from a different vendor for close to the same cost. A system used for word processing is not very CPU-intensive. There generally are not multiple tasks waiting to be serviced, so a high-speed CPU is really unnecessary. Similarly, such a system is not generally going to require more than 64MB of memory. Documents are usually broken into small enough pieces as to be manageable on this system. The floppy drive and CD-ROM drive are simply for software update purposes and other general tasks. The 20GB hard drive is the smallest that’s readily available today, and is more than adequate for a basic installation. Certainly storage space should continually be monitored to determine if and when additional space is warranted. You can use either SCSI or IDE hard drives since speed is not critical on such a system. The SVGA graphics card and monitor are the minimum readily available since this system is not geared toward graphic applications. Even a 4MB video card will do if you have one lying around somewhere. The network card need only be suitable to connect this system to the local network. Usually this will be 10BaseT, although 100BaseT is growing more common, and 100BaseT
