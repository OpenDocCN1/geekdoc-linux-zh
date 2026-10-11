# # Configuring the Kernel

Because the Linux source code is available, it follows that you can configure and customize it before compiling. Indeed, it is possible to compile support into your kernel for only the specific features and drivers you want. Configuring the kernel is a required step before building it. Because the kernel offers myriad features and supports a varied basket of hardware, there is a lot to configure. Kernel configuration is controlled by configuration options, which are prefixed with CONFIG in the form CONFIG_FEATURE. For example, symmetrical multiprocessing (SMP) is controlled by the configuration option CONFIG_SMP. If this option is set, SMP is enabled; if unset, SMP is disabled. The configure options are used both to decide which files to build and to manipulate code via preprocessor directives. Configuration options that control the build process are either Booleans or tristates. A Boolean option is either yes or no. Kernel features, such as CONFIG_PREEMPT, are usually Booleans. A tristate option is one of yes, no, or module. The module setting represents a configuration option that is set but is to be compiled as a module (that is, a separate dynamically loadable object). In the case of tristates, a yes option explicitly means to compile the code into the main kernel image and not as a module. Drivers are usually represented by tristates.

Configuration options can also be strings or integers. These options do not control the build process but instead specify values that kernel source can access as a preprocessor macro. For example, a configuration option can specify the size of a statically allocated array.

Vendor kernels, such as those provided by Canonical for Ubuntu or Red Hat for Fedora, are precompiled as part of the distribution. Such kernels typically enable a good cross section of the needed kernel features and compile nearly all the drivers as modules. This provides for a great base kernel with support for a wide range of hardware as separate modules. For better or worse, as a kernel hacker, you need to compile your own kernels and learn what modules to include on your own.

Thankfully, the kernel provides multiple tools to facilitate configuration. The simplest tool is a text-based command-line utility:

```
make config
```

This utility goes through each option, one by one, and asks the user to interactively select yes, no, or (for tristates) module. Because this takes a long time, unless you are paid by the hour, you should use an ncurses-based graphical utility:

```
make menuconfig
```

Or a gtk+-based graphical utility:

```
make gconfig
```

These three utilities divide the various configuration options into categories, such as "Processor Type and Features." You can move through the categories, view the kernel options, and of course change their values.