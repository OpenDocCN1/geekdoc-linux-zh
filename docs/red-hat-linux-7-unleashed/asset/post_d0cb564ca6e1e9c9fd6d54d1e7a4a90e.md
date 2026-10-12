
More likely, you may accidentally attempt to load modules out of sequence. For instance, you might configure your network support as a module, forgetting that the **httpd** will hang the boot scripts while trying to resolve the hostname, and then inadvertently assign **httpd** an earlier slot in the */etc/rc.d/rc5.d* boot sequence.

There is only a small overhead in loading and unloading and in the coding of a driver as a module. Unless memory or performance is critical, the code is needed continuously, or the module is required early in the boot process, it can and probably should be compiled as a module.

## New Features in 2.4

If you are coming to this chapter from the 2.2 Kernel reference material, you're in for a ride. Systems have changed all over the place. The following is just a partial list of systems that have been added, rewritten, or rethought in the 2.4 kernel:

- Resource Management Subsystem
- Remapped Device Files
- Numerous Changes to the */proc* Interface
- Support for 4.2 Billion Users
- Memory limit now 16GB
- I2O/PCI Improvements
- Improved Plug-and-Play Support
- Improved Parport Interface
- USB Support
- Extended Joystick Support
- ia64, S/390, and SuperH Ports
- Shared Memory VFS
- Logical Volume Manager
- Single Buffer File Caching
- Raw I/O Devices
- Large-file Filesystems (files >2GB)
- UDF and UFS Filesystems
- SCSI Subsystem
- Module Access Control
- Network Address Translation (NAT)
- DECNet and ARcNet Support
- Direct Rendering Manager
- Voice Synthesizer Support
- Kernel-level HTTPD
- *Documentation/DocBook and doxygen*

## Planned Features for Linux 2.5

Kernels take time to polish for production, and books take time to prepare and print; as a result, there are many features that were either not ready in time to be considered for the 2.4 kernel, or that were not well understood enough to be included in this book prior to press. The following sections are a guess as to some of the directions to be taken with 2.5, but do not be surprised if more than one finds its way into an early revision of 2.4.

### CML2

If you have ever tried to *add* a new kernel feature, you have already seen why Eric Raymond is spending his flight and hotel time redesigning the kernel configuration tools.

CML2 is the Configuration Modeling Language to succeed the current `make xconfig` method with a simpler system, is easier to maintain and to program, and will allow module and service developers to specify all dependencies of their code. It may even be possible to specify your hardware to the CML2 interpreter and have it deduce the kernel options without intervention.

### Frame Buffers (fbdev)

James Simmons has plans for cleaning up the `fbdev` layer with a new API, adding support for cards with multiple frame buffers, and adding real multithread support to the console system.

### Sound System

Although partially present in 2.4, the next kernel will expand the support for the ALSA sound drivers.

### V4L2

The 2.4 kernel contains little in the way of new support for the video and FM radio interface primarily because the developers are reworking the entire system for V4L2; unfortunately, V4L2 was not considered stable enough to be included into the 2.3 development tree and has been pushed back to Linux 2.5.

## PART IV

## Memory Management and Memory Devices

Rik van Riel has plans to support allocating very large continuous memory blocks on system initialization, and improved dcache and other improvements to the VM. David Woodhouse is also calling for adding support for flash and other memory device drivers.

### Journaling Filesystem

The 2.5 TODO list includes merging in the changes for the ReiserFS and ext3, merging in XFS, HFS+, JFS, and NWFS; whether all of these will happen or if some hybrid occurs remains to be seen.

### Configuring the Linux Kernel

Once you know what your new kernel must accomplish and have the sources installed, you are ready to begin creating a customized Linux operating system. Before setting the compile in motion, there are a few last minute details to ensure a successful run, or at least a graceful recovery.

### Preparing lilo.conf for Kernel Updates

Before you begin, double-check your system against the requirements in *Linux/Documentation/Changes*. In particular, ensure you have the correct version of the binutils and the gcc compiler.

You should also create an entry in your */etc/lilo.conf* to keep your current kernel installed as a backup. In addition to adding a few seconds' delay on the boot prompt with the *delay* parameter (so you can interrupt to add parameters or select an alternate image), add a section for a known stable kernel (such as the original distribution kernel image) and also for the generated backup left behind by the build commands.

```text
image=/boot/vmlinuz.org
   label=stable
   root=/dev/hda3
   append=""
   read-only
image=/boot/vmlinuz.bak
   label=backup
   root=/dev/hda3
   append=""
   read-only
```

Using this configuration, if you have trouble booting from the new kernel, you can enter *stable* at the *Lilo:* prompt and boot your original kernel.

The make bzImage compile command will automatically back up the previous kernel from $(INSTALL_PATH)/vmlinuz to $(INSTALL_PATH)/vmlinuz.old and then run the lilo command to install the new kernels. The preceding /etc/lilo.conf sections give one more line of defense against a kernel that cannot boot. The fourth section, labeled backup, also allows you to make periodic back-ups of particularly stable development kernels in case repeated compile errors leave both vmlinuz and vmlinuz.old unstable and utility upgrades have cut you off from the original vmlinuz.orig. It happens.

Is lilo.conf prepared to find the new kernel? Do you have a backup kernel and a boot disk? Do you have enough disk space? These may seem trivial questions, but they are important. An error in any of these may leave your system in an inoperable state and entirely devour your weekend. Even if all you are doing is setting a few /proc values or adding a network interface at the boot prompt, it is good defensive driving to consider the recovery plan.

### Allow a LILO Delay

While experimenting with kernel options, remember to set the lilo delay parameter to give some grace time where you can select an alternative kernel. If your system has a delay of zero seconds, you will not have the opportunity to pre-empt loading the default kernel, and if that kernel is faulty, your only option is to boot from a floppy disk. For more dangerous experiments, delay set to -1 will wait indefinitely for a boot parameter.

### Configuring with make

The Linux Makefile provides four methods of setting your configuration options:

- `make config`—A command-line terminal program
- `make menuconfig`—An ncurses-based console program
- `make xconfig`—A tk/tcl-based X11 GUI program
- `make oldconfig`—A semi-automatic update program

Why have a command-line interface at all? Suppose you had an autonomous robot submarine or a space probe. Imagine you are in the midst of maneuvers and need a fast kernel reconfig. Simple dumb terminal interfaces can do places other interfaces cannot dream of going! The X11tk interface may be more elegant and esthetically appealing, but it does require that Tk and X11 are both installed and working.

A forms-based interface is often more comfortable, but X11 is sometimes impractical—for example, while doing remote administration over a slow telnet connection or in a Linux machine for blind users. For these situations, we have the ncurses-based menuconfig. Both the X11 and the ncurses configuration tools offer the same options in the same order, and they have roughly the same capability to navigate backward and forward through the configuration options.

### Note

The X and ncurses configuration commands also have the same propensity to allow wildly conflicting kernel options with nary a whisper of dissent... sometime early in 2.5, this will all change with the adoption of Eric Raymond's CML2 Configuration Management Language (see the section “CML2: The Next-Generation Configuration Tool”).

To start the configuration, simply go to the /usr/src/linux directory and enter one of the configuration commands. If you choose either of the ncurses or X11 methods, you will see a brief flurry of compiler activity while the user-interface programs compile, and then you will be greeted by an overview screen with all the categories of kernel options.

Those of you who recoil in horror at the thought of a command line can now rest easy. From this point on, those using the xconfig method will be in carpal-tunnel land (a.k.a. “mouse mode”) until the configuration is done.

### Selecting Configuration Options

Figure 27.2 shows the initial screen as seen in the xconfig display for the 2.4 kernel. 2.2.x kernels are very similar, but with fewer options and minor cosmetic differences. In all of the configuration methods, most kernel options can be set to be included, included as a module, or left out of the compile. On the xconfig and menuconfig screens, there are options to include or exclude complete sections of configuration; disabling these will gray out any dependent options (the dumb-terminal config option will silently skip these sections).

This guide cannot attempt to describe every one of the 1,302 individual options in the Linux kernel; this chapter will only cover the major groups, focus on options of interest to specific applications, and explain some of the implications and configuration options for common Intel-based modules.
