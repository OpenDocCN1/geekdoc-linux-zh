
## Q The printer is very slow. How can I speed it up?

A You might be able to fix this problem by setting the printer to polled mode with the `lptcontrol` program. This can be done with the command `lptcontrol -P`. Don't forget that you need to add this to a startup file if you want it to take effect on each system boot.

## Quiz

- 1. The file that contains printer definitions is
  - A. `/etc/printers`
  - B. `/etc/print.conf`
  - C. `/etc/printcap`
  - D. `/etc/printdef`

- 2. One printer should always be aliased to which of the following?
  - A. `lpc`
  - B. `lpd`
  - C. `lpr`
  - D. `lp`

- 3. Which of the following programs can be used to look at printer queues?
  - A. `lpd`
  - B. `lpr`
  - C. `lpc`
  - D. `lpq`

- 4. Which of the following commands controls printers and their queues?
  - A. `lpd`
  - B. `lpc`
  - C. `lptcontrol`
  - D. None of the above

- 5. Which of the following commands removes a job from the queue?
  - A. `lprremove`
  - B. `lpr`
  - C. `lprm`
  - D. `lpdelete`

![](img/ba0161b65b37e94cffc801ecbacaba5e_185_0.png)

## Answers

- 1. The correct answer is C.
- 2. The correct answer is D. All the other options are names of printer commands and not printers.
- 3. The correct answer is D.
- 4. The correct answer is B. Watch out for answer C, which is the name of the program that configures the printer port, not the name of the program that controls printers and print queues.
- 5. The correct answer is C. Answers A and D do not exist. Answer B sends a job to the queue.

## Hour 10

### The FreeBSD Kernel and Device Tree

We have talked briefly about the role of the kernel in previous hours of the book. In this hour, we will look at the kernel in greater depth. In addition, you will see how to build a new kernel and the reasons why you might want to do so.

In this hour, you will learn:

- What the kernel is and why you need it
- Why you might want to build a new kernel
- How to work with the kernel configuration file
- How to build and install the new kernel
- What you need to know about the device tree

![](img/ba0161b65b37e94cffc801ecbacaba5e_187_0.png)

### The Kernel and Its Purpose

The kernel is a special piece of software that serves as the core of the operating system. Among other things, it controls how users interact with the hardware and how resources are allocated for software. In addition, the kernel implements network communications so that the computer can communicate with other computers over the LAN or the Internet. When a running program misbehaves, it is the kernel’s job to keep it from interfering with the operation of other programs, or from crashing the system. Figure 10.1 shows a simple diagram of how the kernel relates to the hardware and other running software.

FIGURE 10.1
The kernel isolates software and users from the hardware and thus controls access to system resources.

![](img/ba0161b65b37e94cffc801ecbacaba5e_188_0.png)

![](img/ba0161b65b37e94cffc801ecbacaba5e_188_1.png)

> We mentioned that the kernel isolates software from the hardware. This is not always entirely true because in some special cases, software other than the kernel can access the hardware directly. This is primarily for performance reasons. Some examples are programs used for rendering high-end animation and so on. In this case, it is too much of a performance hit to make the program go through the kernel to access the video hardware, so it will usually access it directly.

### Why Build a Custom Kernel?

These days, it is far less common to have to build a custom kernel. In the past, the main reason for doing so was for device support. Usually, one built a custom kernel because the default kernel didn’t have support for a device in her system (a sound card, for example). These days however, sound card support—as well as support for most other devices—can be dynamically loaded as a kernel module. (Rather than being built directly into the kernel, the module can be loaded into the kernel dynamically at boot time.)

However, there are still times when you might want to build a custom kernel. There are generally four possible reasons for doing this:

- You've sysupdated to a newer version of FreeBSD, and you need to rebuild the kernel to sync with the newer version.
- You need to apply a patch to the kernel to fix a bug or security issue.
- You want to remove support for devices you don't have to give the kernel a smaller footprint.
- You want to add support for a device in your kernel, and you don't want to or can't use a dynamically loadable module.

The idea of rebuilding the core of the operating system from source is understandably rather intimidating to new users. However, the process is not nearly as complicated as it sounds, nor does it require any programming knowledge. Anyone can build a custom FreeBSD kernel by following the instructions given in this hour.

### The Kernel Configuration File

Based on what you have learned about FreeBSD configuration up to this point, you are probably guessing that kernel configuration is handled by a plain text file. And you are absolutely right. The kernel configuration file is located in the directory `/usr/src/sys/i386/conf`. The name of the configuration file that is used to build the default kernel (the one you are running after a fresh FreeBSD install, for example) is `GENERIC`. You won't want to edit this file directly. Instead, make a copy of it. You can give the copy whatever name you want, but it usually makes sense to give it a meaningful name. One common naming system is to give the kernel the same name as the system's hostname on a network. If you aren't on a network, you can be as creative as you want, or you can simply call it MYKERNEL or something. For example,

```
cp GENERIC MYKERNEL
```

Note that you will need to be logged in as root to make the copy of the file, as well as to make changes to it (which we will discuss shortly).

### Editing the Configuration File

Once you have made a copy of the file, open the copy you made in a text editor. At the top of the file, after several comments that begin with the pound sign (#), you will see the following lines:

```
machine  i386
cpu      i486_CPU
cpu      i586_CPU
cpu      i686_CPU
```

The first line specifies the machine type, and it will never change unless you are compiling a kernel for an Alpha system, which is currently the only other platform that FreeBSD supports with a production stable version. A discussion of Alpha support is beyond the scope of this book. Assuming that you are using an Intel x86 or compatible system (AMD or Cyrix), you will never need to change this line.

The next three lines provide support for different generations of processors. Because the GENERIC kernel will run on everything from a 486 up to the latest Pentium 4 and AMD Athlon processors, the default kernel has support compiled in for all of them. In the custom kernel, you will want to remove support for all the processors that you don’t have. For example, if you have a Pentium 3 or Pentium 4, you can remove all of the cpu lines except the i686_CPU line. Instead of actually deleting the lines, you can place a pound sign (#) in front of them. # indicates to the kernel building system that the rest of the line should be considered a comment. Comments are ignored by the system and not processed. So any line that starts with a # will not be included in the kernel, accomplishing the same thing as deleting the line altogether.

![](img/ba0161b65b37e94cffc801ecbacaba5e_190_0.png)

> There is the possibility for confusion here because of different naming schemes among CPU vendors. Keep the following guidelines in mind: The original Pentium processor is an i586. The Pentium 2 through Pentium 4 processors are i686. Cyrix processors are even more confusing because the Cyrix 686 is actually an i586 as far as FreeBSD is concerned. AMD K6 processors are also i586, but AMD Athlon processors are i686. If you install a kernel that does not include support for your CPU type, you will be left with a system that cannot start. In the event that this happens to you, see the section near the end of this hour titled “Recovering from Botched Kernel Builds.”

There are several more lines that are important and you might want to change:

```
ident GENERIC
```

This is simply the name of the kernel. It is what will show up when the kernel starts. The name listed here should be the same as the name you gave the new file you created.

```
maxusers 32
```

This option is rather poorly named and can cause a great deal of confusion. It has absolutely nothing to do with the maximum number of users who are allowed on the system. It actually controls the number of resources available in important system parameters. The number it sets will be approximately equal to the number of resources required by the number of users listed here. If you set maxusers to 1, FreeBSD will automatically manage the number of resources available.
