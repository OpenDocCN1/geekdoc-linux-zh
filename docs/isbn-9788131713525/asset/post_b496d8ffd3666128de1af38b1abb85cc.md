
issues, particularly compiler warnings. In earlier kernel source trees, each compilation or link command was output to the console verbosely, which often required several lines for each step. The end result was virtually unreadable, and compiler warnings slipped by unnoticed in the noise. The new system is definitely an improvement because any anomaly in the build process is easily spotted. If you want or need to see the complete build step, you can force verbose output by defining `V=1` on the make command line.

We have omitted most of the actual compilation and link steps in Listing 4-2, for clarity. (This particular build has more than 900 individual compile and link commands in the build. That would have made for a long listing, indeed.) After all the intermediate files and library archives have been built and compiled, they are put together in one large ELF build target called `vmlinux`. Although it is architecture specific, this `vmlinux` target is a common target—it is produced for all supported Linux architectures.

### 4.2.3 The Kernel Proper: vmlinux

Notice this line in Listing 4-2:

```
LD /arch/arm/boot/compressed/vmlinux
```

The `vmlinux` file is the actual *kernel proper*. It is a fully stand-alone, monolithic image. No unresolved external references exist within the `vmlinux` binary. When caused to execute in the proper context (by a bootloader designed to boot the Linux kernel), it boots the board on which it is running, leaving a completely functional kernel.

In keeping with the philosophy that to understand a system one must first understand its parts, let's look at the construction of the `vmlinux` kernel object.

Listing 4-3 reproduces the actual link stage of the build process that resulted in the vmlinuz ELF object. We have formatted it with line breaks (indicated by the UNIX line-continuation character, `\`) to make it more readable, but otherwise it is the exact output produced by the vmlinuz link step in the build process from Listing 4-2. If you were building the kernel by hand, this is the link command you would issue from the command line.

# Listing 4-3

# Link Stage: vmlinux

```
xscale_be-ld -ES -p --no-undefined -X -o vmlinux \
-T arch/arm/kernel/vmlinux.lds \
arch/arm/kernel/head.o \
arch/arm/kernel/init_task.o \
--start-group \
usr/built-in.o \
arch/arm/kernel/built-in.o \
arch/arm/mm/built-in.o \
arch/arm/common/built-in.o \
arch/arm/mach-lpx4x0/built-in.o \
arch/arm/nwfpe/built-in.o \
kernel/built-in.o \
mm/built-in.o \
fs/built-in.o \
ipc/built-in.o \
security/built-in.o \
crypto/built-in.o \
lib/lib.a \
arch/arm/lib/lib.a \
lib/built-in.o \
arch/arm/lib/built-in.o \
drivers/built-in.o \
sound/built-in.o \
net/built-in.o \
--end-group \
.tmp_kallsyms2.o
```

### 4.2.4 Kernel Image Components

From Listing 4-3, you can see that the vmlinux image consists of several composite binary images. Right now, it is not important to understand the purpose of each component. What is important is to understand the top-level view of what components make up the kernel. The first line of the link command in Listing 4-3 specifies the output file (-o vmlinux.) The second line specifies the *linker script file* (-T vmlinux.lds), a detailed recipe for how the kernel binary image should be linked.^[4]

The third and subsequent lines from Listing 4-3 specify the object modules that form the resulting binary image. Notice that the first object specified is `head.o`. This object was assembled from `/arch/arm/kernel/head.S`, an architecture-specific assembly language source file that performs very low-level kernel initialization. If you were searching for the first line of code to be executed by the kernel, it would make sense to start your search here because it will ultimately be the first code found in the binary image created by this link stage. We examine kernel initialization in detail in Chapter 5.

The next object, `init_task.o`, sets up initial thread and task structures that the kernel requires. Following this is a large collection of object modules, each having a common name: `built-in.o`. You will notice, however, that each `built-in.o` object comes from a specific part of the kernel source tree, as indicated by the path component preceding the `built-in.o` object name. These are the binary objects that are included in the kernel image. An illustration might make this clearer.

> [^4]: The linker script file has a peculiar syntax. The details can be found in the documentation for the GNU linker.

Figure 4-1 illustrates the binary makeup of the `vmlinux` image. It contains a section for each line of the link stage. It’s not to scale because of space considerations, but you can see the relative sizes of each functional component.

![](img/7a1144833e62564667e7dd9eb4c9f03d_107_0.png)

**FIGURE 4-1**
vmlinux image components

It might come as no surprise that the three largest binary components are the file system code, the network code, and all the built-in drivers. If you take the kernel code and the architecture-specific kernel code together, this is the next-largest binary component. Here you find the scheduler, process and thread management, timer management, and other core kernel functionality. Naturally, the kernel contains some architecture-specific functionality, such as low-level context switching, hardware-level interrupt and timer processing, processor exception handling, and more. This is found in .../arch/arm/kernel.

Bear in mind that we are looking at a specific example of a kernel build. In this particular example, we are building a kernel specific to the ARM XScale architecture and, more specifically, the Intel IXP425 network processor on the ADI Engineering reference board. You can see the machine-specific binary components in Figure 4-1 as arch/arm/mach-ixp4xx. Each architecture and machine type (processor/reference board) has different elements in the architecture-specific portions of the kernel, so the makeup of the vmlinux image is slightly different. When you understand one example, you will find it easy to navigate others.

To help you understand the breakdown of functionality in the kernel source tree, Table 4-1 lists each component in Figure 4-1, together with a short description of each binary element that makes up the vmlinux image.

# TABLE 4-1
vmlinux Image Components Description

| Component | Description |
| :--- | :--- |
| arch/arm/kernel/head.o | Kernel architecture-specific startup code. |
| init_task.o | Initial thread and task structs required by kernel. |
| init/built-in.o | Main kernel-initialization code. See Chapter 5. |
| usr/built-in.o | Built-in initramfs image. See Chapter 5. |
| arch/arm/kernel/built-in.o | Architecture-specific kernel code. |
| arch/arm/mm/built-in.o | Architecture-specific memory-management code. |
| arch/arm/common/built-in.o | Architecture-specific generic code. Varies by architecture. |
| arch/arm/mach-ixp4xx/built-in.o | Machine-specific code, usually initialization. |
| arch/arm/nwfpe/built-in.o | Architecture-specific floating point-emulation code. |
| kernel/built-in.o | Common components of the kernel itself. |
| mm/built-in.o | Common components of memory-management code. |
| ipc/built-in.o | Interprocess communications, such as SysV IPC. |
| security/built-in.o | Linux security components. |
| lib/lib.a | Archive of miscellaneous helper functions. |
| arch/arm/lib/lib.a | Architecture-specific common facilities. Varies by architecture. |
| lib/built-in.o | Common kernel helper functions. |
| drivers/built-in.o | All the built-in drivers---not loadable modules. |
| sound/built-in.o | Sound drivers. |
| net/built-in.o | Linux networking. |
| .tmp_kallsyms2.o | Symbol table. |

When we speak of the kernel proper, this vmlinux image is being referenced. As mentioned earlier, very few platforms boot this image directly. For one thing, it is almost universally compressed. At a bare minimum, a bootloader must decompress the image. Many platforms require some type of stub bolted onto the image to perform the decompression. Later in Chapter 5, you will learn how this image is packaged for different architectures, machine types, and bootloaders, and the requirements for booting it.
