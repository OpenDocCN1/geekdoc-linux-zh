
Administration Status (value)       = up(1)
Operation Status (value)            = up(1)
Last Change                         = 775
Inbound Octets                      = 2101014
Inbound Unicast Packets             = 2830
Inbound Non-Unicast Packets         = 1692
Inbound Discards                    = 0
Inbound Errors                      = 0
Inbound Unknown Protocols           = 72
Outbound Octets                     = 1164028
Outbound Unicast Packets            = 3613
Outbound Non-Unicast Packets        = 8
Outbound Discards                   = 0
Outbound Errors                     = 0
Outbound Queue Length               = 0
Specific                            = 655367

Press <Return> to continue

This `lanadmin` output shows *lan0* as the configured LAN interface on *cable1*. Let's now run `lanadmin` on *cable2* and see for what LAN interface it produces an output:

```
# lanadmin
```

```
         LOCAL AREA NETWORK ONLINE ADMINISTRATION. Version 1.0
                Mon, Oct 15,2001  14:45:23

                        Copyright 1994 Hewlett Packard Company.
                                 All rights are reserved.
```

Test Selection mode.

```
lan     = LAN Interface Administration
menu    = Display this menu
quit    = Terminate the Administration
terse   = Do not display command menu
verbose = Display command menu
```

Enter command: lan

LAN Interface test mode. LAN Interface PPA Number = 1

```
clear   = Clear statistics registers
display = Display LAN Interface status and statistics registers
end     = End LAN Interface Administration, return to Test Selection
menu    = Display this menu
ppa     = PPA Number of the LAN Interface
quit    = Terminate the Administration, return to shell
reset   = Reset LAN Interface to execute its self-test
specific= Go to Driver specific menu
```

Enter command: d

```
                  LAN INTERFACE STATUS DISPLAY
                     Mon, Oct 15,2001  14:40:49
```

Inbound Non-Unicast Packets   = 21708
Inbound Discards              = 0
Inbound Errors                = 0
Inbound Unknown Protocols     = 20720
Outbound Octets               = 401517
Outbound Unicast Packets      = 3189
Outbound Non-Unicast Packets  = 7
Outbound Discards             = 0
Outbound Errors               = 0
Outbound Queue Length         = 0
Specific                      = 655367

Press <Return> to continue

This `lanadmin` output shows *lan1* as the configured LAN interface on *cable2*.

Producing information specific to the vPar in which you issue a command is what you can expect when working at the command line with vPars.

Next, let’s take a look at a couple of GlancePlus/UX outputs.

# HP GlancePlus/UX

Working with Glance in vPars is identical to working with Glance on a non-vPars system, except with vPars you will see in Glance only the components that are assigned to the vPar you are analyzing. This means that if you’re running two vPars on a system, you would run Glance in whatever vPar in which you want to perform analysis.

Figure 12-1 shows a Glance screen shot of vPar *cable1*, which has a hostname of *cvhdccon3*:

![](img/eff8b9287a5f38c5adf538f24aacf29e_773_0.png)

# **Figure 12-1** HP GlancePlus/UX Showing Two CPUs of vPar

Figure 12-1 shows that there are two CPUs present in this vPar. The system on which this vPar is running is a four-processor L-Class system. The vPar was configured with only two CPUs, so even though this is a four-processor system only two are shown in the Glance screen shot of this vPar. Where are the other processors you ask? It may be that the vPart(s) in which the other processors are configured are not even running, so the CPUs may be unused at this time. It may be that the other vPart(s) are up-and-running and one or two additional CPUs, depending on how the additional vPart(s) are configured, are in use. If the other vPart(s) are running, invoking Glance in those vPars would show the additional CPU(s) in use.

The other components of which your vPar is comprised will also be shown in Glance. Figure 12-2 shows the disks of vPar *cable1*:

![](img/eff8b9287a5f38c5adf538f24aacf29e_774_0.png)

This is the same list of disks as we saw for *cable1* in the `ioscan -funcC disk` output. Only the first disk shown in Figure 12-2 has been included in the vPar for which the Glance screen shot was produced. The other devices shown are also connected to the SCSI channels that are part of the Core I/O card that was included when the vPar was created with -a `io:0:0:0`. The boot disk was explicitly included when the vPar was created with -a `io:0:0:0.1.1.2:0:BOOT`, so you would expect it to be shown in Glance. The other devices are part of the vPar also because they are part LBA at *0:0*. There are other implied components of this vPar as well, including the LAN interface at *0/0/0/0* and the console at *0/0/4/0*. For more information on how vPars were created please see Chapter 2 as well as the tear-out card included in this book.

The remainder of this chapter includes background information on commands and tools used for performance analysis.

# Non-vPar-Specific Section of Chapter: Introduction

You can take a variety of approaches to performance analysis on your system. These choices range from quick snapshots that take but a few seconds to create, to long-range capacity planning programs that you may want to run for weeks or months before you even begin to analyze the data they produce. This chapter contains examples from a variety of systems, including HP-UX 11i systems. I left in the examples from non-HP-UX systems because some readers of my books are coming from UNIX variants other than HP-UX. Most of the HP-UX examples in this chapter have been updated to reflect 11i systems, however, I'm not aware of any differences between these performance examples on 11i vs. 11.0.

In this chapter, we'll focus on some commonly used UNIX commands and a couple of advanced tools that run on several UNIX variants. These are by no means an exhaustive list of UNIX commands and tools related to performance management; however, I provide enough good information to give you an overview. Your UNIX system may support additional commands and have advanced performance analysis tools. This chapter will give a good overview of performance analysis, including examples of the most commonly used UNIX performance-related commands.

# Standard UNIX Commands

To begin, let's look at some commands you can issue from the UNIX prompt to give you some information about your system. The commands I'll cover are:

- `iostat`
- `vmstat`
- `netstat`
- `ps`
- `kill`
- `showmount`
- `swapinfo` and `swap`
- `sar`

We'll first look at each of these commands so that you get an understanding of the output produced by them and how this output may be used. There are online manual pages for many of the commands covered on your HP-UX system.

Please keep in mind that, like all topics we have covered, the output of these commands may differ somewhat among UNIX variants. The basic information produced on most UNIX variants is the same; however, the format of the outputs may differ somewhat. This usually is not significant if you're viewing the outputs; however, if you're writing programs that accept these outputs and manipulate them in some way, then the format of the outputs is important.

# I/O and CPU Statistics with iostat

The `iostat` command gives you an indication of the level of effort the CPU is putting into I/O and the amount of I/O taking place among your disks and terminals. `iostat` provides a lot of useful information; however, it acts somewhat differently among UNIX variants. The following examples show issuing `iostat` on a Solaris system, an HP-UX system, and an AIX system. `iostat` was not supported on the Linux system I was using for this chapter. Note that on some systems, using the -t option for terminal information produces just terminal information, and on some systems it produces a full output. You will, of course, have to determine the best options for your needs on your UNIX variant. The following examples show the `iostat` command:

Here is a Solaris example executed ten times at five-second intervals:

```
# iostat 5 10
        tty                 fd0                  fd3                  fd6                  cpu
               kps tps serv        kps tps serv        kps tps serv        kps tps serv       us sy wt id
0       0 0 0 0 0 0        0 0 0 0        3 0 57 0        0 79 0 0          7 49 43
0      49 0 0 0 0 0       14 2 75 0 0 0        0 0 0 0        0 2 0 98
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 99
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 100
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 0 0 100
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 1 0 99
0      16 0 0 0 0 0       0 0 0 0        6 1 35 0 0        0 0 0 0        0 4 0 96
0      16 0 0 0 0 0       0 0 0 0        0 0 0 0        0 0 0 0        0 0 0 100
```
