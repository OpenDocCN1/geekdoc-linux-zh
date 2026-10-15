

The directory named scripts contains many of the scripts that make uses. It really does not contain anything of interest to anyone who is not a programmer or a kernel developer (also known as a kernel hacker).

After a kernel is built, all the compiled files will wind up in the arch directory and its subdirectories. Although you can manually move them to their final location, we will show you later in this chapter how the make scripts will do it for you. In the early days of Linux, this post-compilation file relocation was all done by hand; you should be grateful for make.

**NOTE**

The make utility is a very complex program. Complete documentation on the structure of make files, as well as the arguments that it can accept, can be found at http://www.gnu.org/software/make/manual/make.html.

The remainder of the directories in /usr/src/linux-2.6 contain the source code for the kernel and the kernel drivers. When you install the kernel sources, these files are placed there automatically. When you patch kernel sources, these files are altered automatically. When you compile the kernel, these files are accessed automatically. Although you never need to touch the source code files, they can be useful. The kernel source files are nothing more than text files with special formatting, which means that we can look at them and read the programmers' comments. Sometimes, a programmer will write an application, but cannot (or often will not) write the documentation. The comments he puts in the source code are often the only documentation that exists for the code.

Small testing programs are even “hidden” in the comments of some of the code, along with comments and references to other information. Because the source code is written in a language that can be read as easily—almost—as English, a non-programmer might be able to get an idea of what the application or driver is actually doing (see Chapter 30, “C/C++ Programming Tools for Ubuntu”). This information might be of use to an intermediate to advanced Linux user when he is confronted by kernel- and driver-related problems.

**NOTE**

The interaction and control of hardware is handled by a small piece of the kernel called a device driver. The driver tells the computer how to interact with a modem, a SCSI card, a keyboard, a mouse, and so on in response to a user prompt. Without the device driver, the kernel does not know how to interact with the associated device.

## Types of Kernels

In the early days of Linux, kernels were a single block of code containing all the instructions for the processor, the motherboard, and the other hardware. If you changed hardware, you were required to recompile the kernel code to include what you needed and discard what you did not. Including extra, unneeded code carried a penalty since the kernel became larger and occupied more memory. On older systems that had only 4MB–8MB of memory, wasting precious memory for unnecessary code was considered unacceptable. Kernel compiling was something of a “black art” as early Linux users attempted to wring the most performance from their computers. These kernels compiled as a single block of code are called monolithic kernels.

As the kernel code grew larger and the number of devices that could be added to a computer increased, the requirement to recompile became onerous. A new method of building the kernel was developed to make the task of compiling easier. The part of the kernel’s source code that composed the code for the device drivers could be optionally compiled as a module that could be loaded and unloaded into the kernel as required. This is known as the modular approach to building the kernel. Now, all the kernel code could be compiled at once—with most of the code compiled into these modules. Only the required modules would be loaded; the kernel could be kept smaller, and adding hardware was much simpler.

The typical Ubuntu kernel has some drivers compiled as part of the kernel itself (called in-line drivers) and others compiled as modules. Only device drivers compiled in-line are available to the kernel during the boot process; modular drivers are only available after the system has been booted.

**NOTE**

As a common example, drivers for SCSI disk drives must be available to the kernel if you intend to boot from SCSI disks. If the kernel is not compiled with those drivers in-line, the system will not boot because it will not be able to access the disks.

A way around this problem for modular kernels is to use an initial RAM disk (initrd) discussed later in “Creating an Initial RAM Disk Image.” The initrd loads a small kernel and the appropriate device driver, which then can access the device to load the actual kernel you want to run.

Some code can only be one or the other (for technical reasons unimportant to the average user), but most code can be compiled either as modular or in-line. Depending on the application, some system administrators prefer one way over the other, but with fast modern processors and abundant system memory, the performance differences are of little concern to all but the most ardent Linux hackers.

When compiling a kernel, the step in which you make the selection of modular or in-line is part of the make config step that we will detail later in this chapter. Unless you have a specific reason to do otherwise, we suggest that you select the modular option when given a choice. The process of managing modules is addressed in the next section because you will be managing them more frequently than you will be compiling a kernel.

