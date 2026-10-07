# ## Motherboard Requirements

The hardware required to set up a Linux system mirrors a typical PC installation. It starts with the motherboard, which should be an Intel 80386 or later (or one of the Intel workalikes such as AMD). Remarkably, Linux will run even on a slow 80386SX, although “slow” is the operative word whenever you try to do anything on these old systems.

For application development work, though, an 80486DX or later is recommended because of the high CPU usage of the compiler and linker. The same is true of X users, since X is a notorious CPU hog. You can compile applications on an 80386, just as you can run X on one, but the performance can sometimes deteriorate to the point of annoyance.

Linux can make use of a floating point unit if you have one (they are built into the DX and Pentium series chips). If an FPU is not installed, Linux will provide a memory-based emulator that has reasonable performance. Either Intel or workalike add-on FPUs are supported, although some problems have been reported with third-party floating point units, such as the Weitek chip.

Linux supports ISA (Industry Standard Architecture), EISA (Extended Industry Standard Architecture), and PCI (Periphereal Component Interconnect) motherboards, but not MCA (IBM’s MicroChannel Architecture). VESA Local Bus motherboards, which allow periphereal cards direct access to the motherboard components, are also supported if you have one of these earlier units lying around.

RAM requirements vary depending on the size of the Linux system you want to run. A minimum Linux system executes quite well in 2MB, although there is a great deal of swapping involved. 4MB of RAM should be considered an effective minimum, with more memory resulting in faster performance. For development work and X users, 8MB is a good working minimum (although X functions with 4MB with a lot of swapping). Reasonable performance requires 16MB to avoid swapping.

Linux systems that will have more than one user should increase the amount of RAM. Each user’s load dictates the amount of RAM required. For example, 8MB easily supports two users, even both running X. With a third-party multiport multiprocessor board supporting eight users, 16MB RAM is a good choice, although they cannot run X. For X users, a good rule of thumb is 4MB per user minimum, unless the Linux machine can offload the X processing to the user’s machine in a client-server layout.

Linux uses all the available RAM in your machine. It does not impose any architectural limitations on memory as DOS and some other operating systems do. Any available memory is completely used.

![](bbox=[0.85, 0.1, 0.99, 0.28])