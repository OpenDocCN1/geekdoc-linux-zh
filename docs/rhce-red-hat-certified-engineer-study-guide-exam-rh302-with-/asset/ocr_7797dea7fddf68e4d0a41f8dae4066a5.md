+   Kernel hacking, which lets you configure support for kernel testing. Enabling this option impairs security, so you should generally not enable it.

# Step #5: Building the Kernel and Modules

To build the kernel and modules, issue the following sequence of commands:

```
make bzImage
make modules
```

The commands perform the following operations:

+   * make bzImage compiles the kernel
* make modules compiles loadable modules

The commands generally take some time to execute. You may prefer, then, to execute them as a single command so you need not monitor the system to see when it's time to enter the next command. Here's how to do so:

```
make bzImage modules
```

After building a kernel for the first time, you can use an alternative set of commands. First, create your kernel configuration in the usual way by using config, make menuconfig, make xconfig, or make oldconfig. Then, issue the commands

```
make dep
make clean
make bzImage
make modules
```

or issue the single command

```
make dep clean bzImage modules
```

The make dep propagates your configuration choices through the source tree and the make clean removes the results of previous builds. The order in which these two commands are given does not matter. The remaining two commands have their usual effect.