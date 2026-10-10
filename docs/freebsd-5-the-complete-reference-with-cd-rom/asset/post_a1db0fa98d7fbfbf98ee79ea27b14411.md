
time or with input designed to stress the program. Such tests can help reassure you that the problem really is solved and won’t recur.

Some problems can be difficult to diagnose and solve because they’re sporadic. Such problems may require extensive testing after you’ve made a change that you believe will solve the problem. Sometimes these tests can be as simple as leaving the computer running in a normal manner and hoping it doesn’t crash. Other times you may need to monitor log files, CPU load, or other system performance metrics. You may want to create a cron job or use a tool such as the Simple Watcher (SWATCH), which monitors log files for patterns you specify, to help in this process.

If a solution doesn’t work out as you expect, you may have to return to the starting point. Of course, you’ll have learned something in the process, but tracking down another solution can still be a daunting process. Occasionally your original solution really was the correct one but it didn’t work because it wasn’t extreme enough. For instance, if you replace the fan on an overheating CPU with a model that’s better than the original but still not good enough, your system crashes may drop in frequency but not disappear completely. A still more powerful heat sink or fan may finally solve the problem. Similarly, an update might be available for a buggy program, but if that update doesn’t fix the bug in question, it won’t do you much good.

## Using an Emergency Boot System

Some problems are so extreme that they prevent FreeBSD from booting at all, or they require editing files in a way that’s not possible when FreeBSD is running normally. In such cases, an emergency boot system comes in handy. Such a system gives you access to the FreeBSD system without booting it. Emergency boot systems can also be useful in performing certain types of upgrades and maintenance, such as resizing your system’s root partition. Such a system can take any of several different forms:

- **Alternative OS installation**: For some functions, an OS other than FreeBSD can be useful for emergency recovery. For example, you can use a disk partitioning tool in just about any OS to check the x86 partition table, for instance. (Free non-UNIX OSs can understand FreeBSD partitions within the FreeBSD slice, though.) If your Stage 0 boot loader is damaged, you can replace it with various non-FreeBSD boot loaders, such as Linux’s LILO or the commercial BootMagic from PowerQuest (`http://www.powerquest.com`).

> **Caution**: _A few OSs, such as Linux, provide support for FreeBSD’s filesystems. You should be cautious about using this support to write to a FreeBSD partition, though. Linux’s FFS/UFS support, in particular, is immature and may damage the filesystem._

- **Alternative FreeBSD installation**: You can install FreeBSD twice on a single computer. Make one installation small, containing only the minimal set of tools, and use the second installation as your main system. You can then boot the first system for emergency or low-level maintenance work.
- **Second hard disk installation**: You can install FreeBSD on a second hard disk and use it to perform maintenance on the main hard disk. If the second hard disk is permanently installed, this is just a variant of the previous option; but you can install FreeBSD on a second disk installed for emergency purposes even if you don't prepare this configuration from the start.
- **Removable disk installation**: A variant of the preceding option is to install FreeBSD on a high-capacity removable disk device, such as a Zip, LS-120, or Jaz disk. You can prepare and test such a system, then remove the disk and store it for emergencies. One difficulty with this approach is that these devices may not be bootable, so you may need to play games with boot loaders to get it to work.
- **FreeBSD recovery CD-ROM**: In a multi-CD-ROM version of FreeBSD, the second CD-ROM is usually a bootable recovery CD-ROM. The system boots into what looks like a normal FreeBSD installation, but if you select the `Fixit` option, you can launch a full FreeBSD system that's based on a custom set of tools on a floppy disk or the standard tools included on the CD-ROM. You'll need to mount your normal system, whereupon you can edit files, run testing utilities, and so on.

As a general rule, this last option is a good one for general use. The FreeBSD recovery CD-ROM contains a small but usable system, including the vi and ee editors, standard disk tools and commands such as mount and fsck, and archiving and backup tools such as tar. After you mount your normal FreeBSD installation, you can use at least some programs from it, although programs that load libraries may pose problems because they may not be able to find them.

Unless you install a full FreeBSD system with all your favorite tools to use as an emergency system, chances are you'll find an emergency system to be rather spartan. Nonetheless, if you're familiar with the basic command-line tools you should be able to get by well enough to perform emergency repairs.

> Tip: Become familiar with whatever emergency system is available to you. Try booting it and using it to read and alter a few noncritical files on your system (or, for added safety, on a test system). Familiarity with emergency tools will speed recovery and make it less likely that you'll do more damage when a real emergency presents itself.

## Summary

Troubleshooting is largely synonymous with problem-solving. As such, various heuristics and rules of thumb can help guide you through the process. The number of specific problems and solutions is so large that this chapter is only long enough to present a few guiding principles and symptoms of some of the more common problems and problem classes. If you run into a real stumper, you can avail yourself of various resources to get help, including books, web pages, and Usenet newsgroups.

![](img/f34d37e3abe9f4517128e54f80ab2616_834_0.png)

## The Complete Reference

## Glossary

**account** A set of data structures that enable a person to use a FreeBSD system.

**AGP bus** A hardware standard for connecting video cards to motherboards. Most x86 motherboards sold in 2002 have precisely one AGP bus, but some include video hardware on the motherboard itself, which uses an internal AGP bus. Older motherboards used the PCI bus or the ISA bus for video hardware.

**anti-aliasing** A technique for font display in which curves and diagonal lines use gray pixels in addition to the usual black and white. Some people find that anti-aliasing can improve the readability of some fonts at certain sizes, but other people dislike the effect. Also known as font smoothing.

**ASCII** The American Standard Code for Information Interchange is the standard mapping of alphanumeric characters, punctuation characters, and certain control characters into numbers understandable by computers.

**assembler** A program that converts assembly language into machine language.

**assembly language** A representation of machine language using mnemonic codes for the benefit of humans. Programmers can write software in assembly language and produce machine code using an assembler program. Assembly language is a lower-level language than the more popular high-level languages such as C, Pascal, and Perl.

**ATA** The Advanced Technology Attachment standard, a hardware standard for connecting hard disks and similar devices to their controller cards or motherboards. Also known as EIDE.

**ATAPI** The ATA Packet Interface, a standard used by CD-ROMs, tape drives, and some other devices that use the ATA standard. See also EIDE.

**binary** A base-2 numbering system; each digit may be either 0 or 1. Computers operate on base-2 arithmetic. (2) A file format that holds raw noncontextual data, such as graphics or sound files. (3) A binary data file format for programs. Source code is turned into binary code by being compiled.

**binary code** See machine language. (Binary code is a synonym because the CPU operates on base-2 numbers, although in practice machine language is often represented in base-16 for human consumption.)

**bit** A binary digit—that is, 1 or 0—used in a base-2 number system.

**bitmap** A method of representing data in which individual bits map onto specific pieces of binary information. Bitmaps are frequently used for graphical data, in which the bits map onto pixels on the display. In the case of color graphics, multiple bits define each pixel, so the term bitmap is something of a misnomer, but it’s still used. See also vector graphics.
