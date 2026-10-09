the Exit menu item. The kernel configuration system will ask whether to save the new configuration. Choosing Yes saves the new configuration into a new _.config_ file. In addition to creating the _.config_ file, a few header files and symbolic links are created. It is also possible to exit the kernel configuration without making any changes, just answer No to the question.

Apart from the main configuration options, the architecture support within the kernel often includes standard template configurations for certain targets. This is especially true for standard PowerPC and ARM targets. In those cases, the defaults provided with the kernel will be used to generate the _.config_ file. For example, here is how to configure the kernel for a TQM860L ppc target:

```
```
$ make ARCH=ppc CROSS_COMPILE=powerpc-linux- TQM860L_config
$ make ARCH=ppc CROSS_COMPILE=powerpc-linux- oldconfig
```
```

# ### Managing Multiple Configurations

It is often desirable to test different configurations using the same kernel sources. Changing the kernel’s configuration, however, destroys the previous configuration, because all the configuration files are overwritten by the kernel’s configuration utilities. To save a configuration for future use, you need to save the _.config_ files created by the kernel’s configuration. These files can later be reused to restore a previous kernel configuration.

The easiest way to back up and retrieve configurations is to use the kernel’s own configuration procedures. The menus displayed by both the `menuconfig` and `xconfig` Makefile targets allow you to save and restore configurations. In each case, you need to provide an appropriate filename.

You can also save the _.config_ files by hand. In that case, you need to copy the configuration file created by the kernel configuration utilities to an alternative location for future use. To use a saved configuration, you will need to copy the previously saved _.config_ file back into the kernel’s root directory and then use the `make` command with the `oldconfig` Makefile target to configure the kernel using the newly copied _.config_ file. As with the `menuconfig` Makefile target, the `oldconfig` Makefile target creates a few headers files and symbolic links.

Whether you copy the files manually or use the menus provided by the various utilities, store the configurations in an intuitive location and use a meaningful naming scheme for saving your configurations. To identify each configuration file, prepend each filename with the kernel version it relates to, along with a small descriptive comment, a date, or both. Leave the _.config_ extension as-is, nevertheless, to identify the file as a kernel configuration file.