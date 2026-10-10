As shown in Listing 8-1, the exit routine is specified using the module_exit() macro.

That's all there is to a skeletal device driver capable of live insertion in an actual kernel. In the sections to follow, we introduce additional functionality to our loadable device driver module that illustrates how a user space program would interact with a device driver module.

# 8.2 Module Utilities

We had a brief introduction to module utilities in Listing 8-5. There we used the module utility modprobe to insert and remove a device driver module from a Linux kernel. A number of small utilities are used to manage device driver modules. This section introduces them. You are encouraged to refer to the man page for each utility, for complete details. In fact, those interested in a greater knowledge of Linux loadable modules should consult the source code for these utilities. Section 8.6.1, "Suggestions for Additional Reading" at the end of this chapter contains a reference for where they can be found.

# 8.2.1 insmod

The insmod utility is the simplest way to insert a module into a running kernel. You supply a complete pathname, and insmod does the work. For example:

```
$ insmod /lib/modules/2.6.14/kernel/drivers/char/examples/hello1.ko
```

This loads the module hello1.ko into the kernel. The output would be the same as shown in Listing 8-5—namely, the Hello message. The insmod utility is a simple program that does not require or accept any options. It requires a full pathname because it has no logic for searching for the module. Most often, you will use modprobe, described shortly, because it has many more features and capabilities.

# 8.2.2 Module Parameters

Many device driver modules can accept parameters to modify their behavior. Examples include enabling debug mode, setting verbose reporting, or specifying module-specific options. The insmod utility accepts parameters (also called options in some contexts) by specifying them after the module name. Listing 8-6 shows our