
## Troubleshooting

Several things can go wrong when you use printers. This section discusses some of the most common problems and their solutions.

### Printer Does Not Receive Data; Jobs Are Sitting in Queue

Check `lpq` and make sure that the spooling daemon is running. If it says `Warning: no daemon present`, you will need to use `lpc` to restart the spooling daemon. Also check `lpc` and make sure that the printer is not disabled.

### Data Light on Printer Flashes, but Printer Will Not Print

This is often a symptom of sending non-PostScript data to a PostScript printer. Check your filter and make sure it is filtering text correctly and converting that text to PostScript.

### Printing an Image File in GIMP or a Web Page Results in Hundreds of Pages of Garbage Being Printed

This can often be a symptom of feeding PostScript data to a printer that doesn't understand PostScript. The non-PostScript printer will try to print this file as plain text. Check out the GhostScript program and also see the section earlier in this chapter titled “Printing PostScript Files on Non-PostScript Printers.”

### The Printer Is Slow

Try setting the printer to polled mode (assuming this printer is on the parallel port). Use the following command:

```
lptcontrol -p
```

Remember that you will need to add this to a startup file if you want it to take effect at each system boot. See the section at the beginning of the chapter on `lptcontrol`.

### Printed Output “Stair Steps”

The symptoms of the stair-step problem look something like this:

```
Line one of the file.
    Line two of the file.
        Line three of the file.
            Line four of the file.
```

This pattern will continue until the text runs off the end of the page. This is a fairly common problem caused by differences in the way Unix and DOS/Windows interpret the linefeed (LF) character. When DOS/Windows advances to a new line, it sends both a carriage return and a linefeed. Unix, on the other hand, sends only a linefeed character and expects a carriage return to be implied. If your printer is expecting DOS-style carriage return and linefeed combinations but is only receiving a linefeed, it will advance the paper but never return the print head to the beginning of the line. There are a few ways you might be able to solve this problem.

The first is to look for an option in your printer's configuration that changes the way it interprets a linefeed character. See your printer documentation to see whether there is a way you can do this.

The second way is to create a filter that converts the LF to a combination of CR and LF. If your printer understands HP-PCL language, the following filter is recommended by the *FreeBSD Handbook* for performing this task:

```
#!/bin/sh
#
# hpif - Simple text input filter for lpd for HP-PCL based printers
# Installed in /usr/local/libexec/hpif
#
# Simply copies stdin to stdout.  Ignores all filter arguments.
# Tells printer to treat LF as CR+LF.  Ejects the page when done.

printf "\033&k2G" && cat && printf "\033&10H" && exit 0
exit 2
```

See the section on text filters earlier in this chapter for more information on how to install a text filter.

If your printer does not understand HP-PCL, you might be able to use the `tr` command to convert the LF into a CR/LF. A filter such as the following may do the trick:

```
#!/bin/sh
# Filter that fixes the stair stepping effect on non PCL printers.
/bin/cat | tr '\13' '\13\10' && exit 0
exit 2
```

Once again, see the section on text filters earlier in this chapter for more information on how to install a text filter.

### All the Text Prints on One Line, Creating a Mess and Writing Over the Top of Existing Text

This is basically the opposite of the stair-stepping problem. This problem is rare, but it does happen occasionally. Basically, the LF is being interpreted as a CR by the printer. The print head is getting returned to the beginning of the line, but the paper is not being advanced.

To fix this problem, you will need to make changes to your printer's configuration settings so that it interprets CR and LF properly. See your printer's documentation for details on how to do this.

If you find that you cannot change the hardware settings of your printer to fix this problem, the same filter used earlier to fix the stair-stepping problem might fix this problem as well.

## CHAPTER 16

# Kernel Configuration

This chapter covers a topic that's likely to be one of the most intimidating to a newcomer to Unix: how to configure and rebuild your kernel. This is a task that simply does not happen in the desktop PC world. However, it's a necessary part of life when dealing with an open-source system under constant development, in a world in which new devices constantly demand more functionality from a kernel. Unfortunately, kernel configuration isn't easy to do.

Configuring the kernel is at the heart of customizing FreeBSD and other operating systems like it. A well-tuned kernel will serve 100 percent of the demands that a system and its users place on it, while eliminating all the unnecessary baggage that an unoptimized kernel might have, thus making the system operate significantly faster. This chapter provides enough insight into the kernel-configuration process to eliminate the mystery and enable this kind of customizability.

## The Role of the Kernel

The kernel is the master executable of the system. It's the first thing that is executed from the boot blocks when you power on the system, and it constantly runs throughout the machine's uptime. Its job is to oversee all the processes running on the system, handle TCP/IP and other networking duties, manage access to all the devices on the system, and control memory usage—to name just a few of its tasks.

Every operating system has a kernel—from Ms-DOS, to Windows, to the highest-end mainframe. Some systems take greater pains to hide the kernel from the user than others do. In Windows, it's an executable in `C:\WINDOWS\SYSTEM`; in classic Mac OS, it's hidden from the filesystem entirely. In many Unix systems, the kernel's traditional place is in the root directory at the top of the filesystem. In FreeBSD, the kernel is placed in `/` prior to FreeBSD 5.0 and in `/boot` afterward. With each of these operating systems, a default (or "generic") kernel is part of every released version of the system; when a new version comes out, its changes are mostly additions to accommodate drivers for new devices that the system supports. The kernel is responsible for knowing about every kind of device that can be connected to the system. When you install drivers for a new and previously unsupported device in Windows, you generally have to reboot. That's because the drivers, libraries, and other items used by your kernel have been modified and cannot be incorporated into the system's operation "on the fly." In most cases, the system has to be restarted in order for the new resources to be used.

FreeBSD uses a *microkernel* architecture, which means that the kernel is fairly small and modular. Windows NT and Mach (the kernel upon which Mac OS X is built) are other examples of microkernels in which new devices are more frequently added through kernel modules (which can be loaded and unloaded during runtime) than by recompiling the kernel. Linux and Windows 95/98/Me are instead *monolithic* kernels, in which the kernel's code is more optimized for performance and to minimize context switching. The monolithic kernel architecture makes for kernel code that's cleaner and easier for developers to maintain, but the administrator is required to recompile the kernel every time support for a new device is added.

This isn't a terribly clear delineation—Linux operates fairly heavily on kernel modules today, and FreeBSD's kernel does have to be recompiled for a number of different reasons. The difference between a microkernel and monolithic kernel architecture is largely a philosophical one and has to do with a good deal more than simply device support. The biggest and most fundamental difference is that a microkernel has a *mechanism* for passing certain non-core system calls to a user-level processing level, or ring, instead of handling them all internally and stripping down the core of the kernel to only those functions that require the highest level of supervisor-mode execution status. Keeping only essential functions in the kernel increases runtime robustness and makes the kernel processes more understandable and manageable. This arrangement also provides a measure of inherent security in the form of reduced complexity as well as easier support for modularity when it comes to devices.

Although the ideal of total modularity is all well and good, a kernel in which every possible kind of device and option is modular and loadable during runtime is as theoretical as perpetual motion. Chances are that as you gain experience with FreeBSD, you will come to a point where you can't avoid recompiling your kernel; it's at that time that you'll undergo the rite of passage that initiates you into the circle of kernel hackers.

### IN THIS CHAPTER

- The Role of the Kernel
- Why Configure a Custom Kernel?
- The Kernel Configuration Files
- Creating a Custom Kernel Configuration File
- Compiling and Installing the Custom Kernel
- Adding Device Nodes to the /dev Directory (If Necessary)
- Recovering When Something Goes Wrong

## Why Configure a Custom Kernel?

FreeBSD comes with the GENERIC kernel installed by default. This kernel is tuned to support as wide a user base as possible so that FreeBSD will work "out of the box" on as
