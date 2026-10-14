Kmod is not designed to automatically upload modules. The potential saving in memory is only marginal for the RAM capacity of computers today. See also `/usr/src/linux/Documentation/kmod.txt`. For reasons of performance, it is better for server machines, which have special tasks to perform and need only a few drivers, to have a “monolithic” kernel.

# Kernel Configuration

The configuration of the kernel that was installed or updated is saved in the file `/usr/src/linux/.config`.

The kernel can be configured at the command line, in a menu in text mode, or in a menu in the X Window System. Here is a short overview of these three methods.

> **Tip**
> 
> To use an already existing `.config`, just type `make oldconfig` then proceed as described in Section *Compiling the Kernel* on the next page.

# Configuration on the Command Line

To configure the kernel, change to `/usr/src/linux` and enter `make config`. You are asked to choose the options you want supported by the kernel to build. There are two or three possible answers here: `Y`, `N`, or `M`. `n` means that this device is not compiled directly into the kernel, but as a module instead. Any driver needed to boot the system should be integrated into the kernel, not loaded as a module. If you press any other key, get a short help text about the current option.

# Configuration in Text Mode

A much more convenient way of configuring the kernel can be achieved by typing `make menuconfig`. With menuconfig you do not have to go through all the questions: just make the few changes you want.