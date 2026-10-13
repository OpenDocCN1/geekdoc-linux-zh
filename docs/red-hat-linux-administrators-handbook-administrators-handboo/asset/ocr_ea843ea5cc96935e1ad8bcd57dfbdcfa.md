You can safely say Y even if your machine doesn’t have MTRRs, you’ll just add about 3k to your kernel.

*See Documentation/mtrr.txt for more information.*

*As you can see, this is quite helpful.*

```
Symmetric multi-processing support (CONFIG_SMP) [Y/n/?]
```

If you have multiple processors on your system and want to turn on symmetric multiprocessing support, choose the default, Y. I don’t have a motherboard with more than one processor on it, so I chose n to not have SMP support.

# Loadable module support

The Linux kernel uses an innovative method for keeping a low profile. It uses features and drivers implemented as external modules. The modules are dynamically loaded and unloaded on an as-needed basis. This allows the kernel to require less memory and become increasingly hardware-independent. The modules typically are loaded with a program called kernel, which in turn uses a program called modprobe to manage available modules. Modules can be device drivers, file systems, binary executable formats, and so on. In this section, you are asked whether or not you want module-related support. The first question is as follows:

```
Enable loadable module support (CONFIG_MODULES) [Y/n/?]
```

This really should not be a prompt, because you definitely want to have loadable module support for almost all scenarios. So, the default, Y, is fine.

```
Set version information on all symbols for modules (CONFIG_MODVERSIONS) [N/y/?]
```

When modules are compiled with version information, they can be reused with newer kernels without needing to be recompiled from scratch. However, the preferred method is to compile the modules along with the new kernel to eliminate compatibility problems. Hence, the default option to not include the version information is sufficient.

```
Kernel module loader (CONFIG_KMOD) [N/y/?]
```