
## 4.5.1 Suggestions for Additional Reading

Linux Kernel HOWTO:
www.tldp.org/HOWTO/Kernel-HOWTO

Kernel Kbuild documentation:
http://sourceforge.net/projects/kbuild/

The Linux Documentation Project:
www.tldp.org/

*Tool Interface Standard (TIS)* Executable and Linking Format (*ELF*) Specification, Version 1.2
*TIS* Committee, May 1995

Linux kernel source tree:
`…/Documentation/kbuild/makefiles.txt`

Linux kernel source tree:
`…/Documentation/kbuild/kconfig-language.txt`

*Linux Kernel Development*, 2nd Edition
Robert Love
Novell Press, 2005

# Chapter 5

![](img/7a1144833e62564667e7dd9eb4c9f03d_130_0.png)

## Kernel Initialization

### In this chapter
- Composite Kernel Image: Piggy and Friends ... page 100
- Initialization Flow of Control ... page 109
- Kernel Command Line Processing ... page 114
- Subsystem Initialization ... page 121
- The init Thread ... page 123
- Chapter Summary ... page 128

When the power is applied to an embedded Linux system, a complex sequence of events is started. After a few seconds, the Linux kernel is operational and has spawned a series of application programs as specified by the system init scripts. A significant portion of these activities are governed by system configuration and are under the control of the embedded developer.

This chapter examines the initial sequence of events in the Linux kernel. We take a detailed look at the mechanisms and processes used during kernel initialization. We describe the Linux kernel command line and its use to customize the Linux environment on startup. With this knowledge, you will be able to customize and control the initialization sequence to meet the requirements of your particular embedded system.

## 5.1 Composite Kernel Image: Piggy and Friends

At power-on, the bootloader in an embedded system is first to get processor control. After the bootloader has performed some low-level hardware initialization, control is passed to the Linux kernel. This can be a manual sequence of events to facilitate the development process (for example, the user types interactive load/boot commands at the bootloader prompt), or an automated startup sequence typical of a production environment. We have dedicated Chapter 7, “Bootloaders,” to this subject, so we defer any detailed bootloader discussion to that chapter.

In Chapter 4, “The Linux Kernel: A Different Perspective,” we examined the components that make up the Linux kernel image. Recall that one of the common files built for every architecture is the ELF binary named vmlinux. This binary file is the monolithic kernel itself, or what we have been calling the kernel proper. In fact, when we looked at its construction in the link stage of vmlinux, we pointed out where we might look to see where the first line of code might be found. In most architectures, it is found in an assembly language source file called head.S or similar. In the PowerPC (ppc) branch of the kernel, several versions of head.S are present, depending on the processor. For example, the AMCC 440 series processors are initialized from a file called head_44x.S.

Some architectures and bootloaders are capable of directly booting the vmlinux kernel image. For example, platforms based on PowerPC architecture and the U-Boot¹ bootloader can usually boot the vmLinux image directly (after conversion from ELF to binary, as you will shortly see). In other combinations of architecture and bootloader, additional functionality might be needed to set up the proper context and provide the necessary utilities for loading and booting the kernel.

Listing 5-1 details the final sequence of steps in the kernel build process for a hardware platform² based on the ADI Engineering Coyote Reference Platform, which contains an Intel IXP425 network processor. This listing uses the quiet form of output from the kernel build system, which is the default. As pointed out in Chapter 4, it is a useful shorthand notation, allowing more focus on errors and warnings during the build.

```
$ make ARCH=arm CROSS_COMPILE=xscale_be_ zimage
many build steps omitted for clarity
LD
SYMAPP
OBJCOPY
Kernel:
AS
GZIP
AS
CC
AS
LD
OBJCOPY
Kernel:
Building modules (stage 2):
```

### Listing 5-1 Final Kernel Build Sequence: ARM/IXP425 (Coyote)

In the third line of Listing 5-1, the vmlinux image (the kernel proper) is linked. Following that, a number of additional object modules are processed. These include head.o, piggy.o, and the architecture-specific head-xscale.o, among others. (The tags identify what is happening on each line. For example, AS indicates that the assembler is invoked, GZIP indicates compression, and so on.) In general, these object modules are specific to a given architecture (ARM/XScale, in this example) and contain low-level utility routines needed to boot the kernel on this particular architecture. Table 5-1 details the components from Listing 5-1.

### TABLE 5-1 ARM/XScale Low-Level Architecture Objects

| Component | Function/Description |
|---|---|
| vmlinux | Kernel proper, in ELF format, including symbols, comments, debug info (if compiled with -g) and architecture-generic components. |
| System.map | Text-based kernel symbol table for vmlinux module. |
| Image | Binary kernel module, stripped of symbols, notes, and comments. |
| head.o | ARM-specific startup code generic to ARM processors. It is this object that is passed control by the bootloader. |
| piggy.gz | The file Image compressed with gzip. |
| piggy.o | The file piggy.gz in assembly language format so it can be linked with a subsequent object, misc.o (see the text). |
| misc.o | Routines used for decompressing the kernel image (piggy.gz), and the source of the familiar boot message: “Uncompressing Linux... Done” on some architectures. |
| head-xscale.o | Processor initialization specific to the XScale processor family. |
| big-endian.o | Tiny assembly language routine to switch the XScale processor into big-endian mode. |
| vmlinux | Composite kernel image. Note this is an unfortunate choice of names, because it duplicates the name for the kernel proper; the two are not the same. This binary image is the result when the kernel proper is linked with the objects in this table. See the text for an explanation. |
| zImage | Final composite kernel image loaded by bootloader. See the following text. |

> ¹ If the kernel image itself needs additional support, you will need to modify U-Boot. See Chapter 7, “Bootloaders.”
> ² The term piggy was originally used to describe a “piggyback” concept. In this case, the binary kernel image is piggybacked onto the bootstraps loader to produce the composite kernel image.

An illustration will help you understand this structure and the following discussion. Figure 5-1 shows the image components and their metamorphosis during the build process leading up to a bootable kernel image. The following sections describe the components and process in detail.

![](img/7a1144833e62564667e7dd9eb4c9f03d_134_0.png)

### FIGURE 5-1 Composite kernel image construction

### 5.1.1 The Image Object

After the vmlinux kernel ELF file has been built, the kernel build system continues to process the targets described in Table 5-1. The Image object is created from the vmlinux object. Image is basically the vmlinux ELF file stripped of redundant sections (notes and comments) and also stripped of any debugging symbols that might have been present. The following command is used for this:

```
xscale_be-objcopy -O binary -R .note -R .comment -S \
 vmlinux arch/arm/boot/Image
```

In the previous objcopy command, the -O option tells objcopy to generate a binary file, the -R option removes the ELF sections named .note and .comment, and the -S option is the flag to strip debugging symbols. Notice that objcopy takes the vmlinux ELF image as input and generates the target binary file called Image. In summary, Image is nothing more than the kernel proper in binary form stripped of debug symbols and the .note and .comment ELF sections.
