```
lsmod
```

Modules are stored within the file `/proc/modules`, so you can also see them with:

```
cat /proc/modules
```

This can be a long list, and you might prefer to search for something particular. To search for the `fat` module:

```
lsmod | grep fat
```

# 1.6 Is there a need to download and compile the kernel?

To effectively follow this guide, there is no obligatory requirement for performing such actions. Nonetheless, a prudent approach involves executing the examples within a test distribution on a virtual machine, thus mitigating any potential risk of disrupting the system.

# 1.7 Before We Begin

Before delving into code, certain matters require attention. Variances exist among individuals' systems, and distinct personal approaches are evident. The achievement of successful compilation and loading of the inaugural "hello world" program may, at times, present challenges. It is reassuring to note that overcoming the initial obstacle in the first attempt paves the way for subsequent endeavors to proceed seamlessly.

+   1. Modversioning. A module compiled for one kernel will not load if a different kernel is booted, unless CONFIG_MODVERSIONS is enabled in the kernel. Module versioning will be discussed later in this guide. Until module versioning is covered, the examples in this guide may not work correctly if running a kernel with modversioning turned on. However, most stock Linux distribution kernels come with modversioning enabled. If difficulties arise when loading the modules due to versioning errors, consider compiling a kernel with modversioning turned off.

+   2. Using X Window System. It is highly recommended to extract, compile, and load all the examples discussed in this guide from a console. Working on these tasks within the X Window System is discouraged. Modules cannot directly print to the screen like printf() can, but they can log information and warnings that are eventually displayed on the screen, specifically within a console. If a module is loaded from an xterm,