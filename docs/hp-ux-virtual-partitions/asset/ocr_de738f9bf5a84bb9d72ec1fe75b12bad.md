File System Swap    Swap space allocated on mounted file systems.

Pseudo-Swap    Use of installed RAM as pseudo-swap, allowing virtual memory space allocation beyond the limit of swap space on disk devices.

Variable Page Sizes    The size of virtual memory pages can be altered to make swap operations more efficient in particular applications.

# Undocumented Kernel Parameters

Some of the configurable parameters that appear in the kernel master file are not documented, and some are not known to or are not supported by SAM for any of several possible reasons:

+   ¸ The parameter is obsolete. It is no longer used in current HP-UX releases, but might appear in an existing kernel configuration. If SAM encounters an obsolete parameter in the current kernel configuration, it does not display it in the list of configurable parameters that can be changed. It also removes that parameter when creating the new configuration file used to build the pending kernel.

+   ¸ The parameter is not supported by SAM. As with obsolete parameters, it is not displayed in the list of configurable parameters, but it is retained in the new kernel configuration file to ensure that no malfunctions are introduced due to a missing parameter.

+   ¸ The parameter is assigned a value by kernel configuration software, which is frequently based on external factors. The assigned value might be used when calculating values for one or more other parameters.

+   ¸ The parameter is for HP factory or support use only. No change from the default value should be made unless specifically directed otherwise by official HP support personnel.

+   ¸ The parameter supports obsolete or obsolescent software. For information about how to select a non-default value, consult the documentation furnished with the software that the parameter supports.