# 356 Chapter 11 Backing Up and Restoring

For example, consider the fictitious WeAin'tThe Inc., a software company that creates and markets its own operating system. WeAin'tThe has a working (development) version of its software and a copy of the last released version for use in customer support. It does development on a server system, which holds the developing software version (2.5), compilers and libraries that it requires, and the last released version (2.4). As the development of new modules continues, the disk fills up. When the developing software is released, version 2.4 is archived to tape, and a new development version (3.0) is begun. Now the system has versions 2.5 and 3.0 on it, and version 2.4 is safely tucked away in case a customer who had not chosen to upgrade to due hardware incompatibility needs customer support.

# Backup Commands and Utilities

In the next section, we will discuss various backup commands at your disposal. We'll look at utilities that facilitate the handling of the hardware itself, command-line backup commands, and GUI-based backup packages. Most of them are included with the main Linux distributions; the others can be downloaded from Internet sites.

# Tape Utilities

Tape utilities are programs that help manage tape access and usage. They aren't backup programs, in fact they often do not write to the tape at all; instead, they perform functions necessary to the backup process like finding a specific position on the tape or allowing you to retention the tape.

The mt performs a number of tape operations, such as moving or finding a specified position on the tape, setting or checking the tape's tension, setting or checking the tape's compression, setting or checking the block size or density, and erasing the tape. The mt command is used when you need to rewind the tape prior to writing to it, to erase the tape, to reposition the head before a write, or to auto-ject the tape when the backup has been completed.

If you are using QIC tapes, you should always retention the tape before you write to it. For some reason, QIC tapes are much more sensitive to tension than are other tapes. The command to do this with a nonrewinding tape drive is:

```
# mt -f /dev/ntape reten
```