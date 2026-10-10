The third form of the command can only be used from the command line of an X terminal window during an active X session. The command will present an X window dialog box with buttons and check boxes that represent yes, no, or if possible, build a module. Start the configuration like this:

```
```
# make xconfig
```
```

After you press Enter, you will see the dialog box, as shown in Figure 14.19.

The order in which to proceed through the menus is not as obvious using a script or console-based dialog box. If you are building a new kernel for the first time, make sure you understand exactly what you would like to enable or disable in your new kernel. Also, make sure to proceed through all the menus so that you have a better understanding of the capabilities that the Linux kernel offers.

Save the file and exit after you have finished the configuration. Next, use the *make* command to create dependencies in the source tree (so that the compiler and linker know what elements to build and put together in the kernel), like this:

```
```
# make dep
```
```

After the dependencies have been created, you can then build the kernel like this:

```
```
# make vmlinux
```
```

After you press Enter, the compilation process will start. Depending on the speed of your system, you will find two new files in the `/usr/src/linux` directory: `vmlinux`, a new kernel; and `System.map`, a memory map of the new kernel. Your next step is to build any required kernel modules. Again, use the *make* command:

```
```
# make modules
```
```

After the modules are built, you can then install them with:

```
```
# make modules_install
```
```

![](bbox=[0.15, 0.8, 0.68, 0.88])

*Figure 14.19 Configuring the build during an active X session allows the use of your X pointing device in a graphical X window and configuration dialog boxes.*