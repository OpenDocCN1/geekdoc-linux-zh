# # TOPIC C

# ## Create an initrd Image

You configured and customized kernel modules. The initrd image, or the initial ramdisk image, consists of all the kernel modules that were loaded during the boot process. Additional modules that are installed also need to be added to the initrd image to load them automatically at boot time. In this topic, you will create the initrd image to update the kernel.

The existing kernel in your system may have all the necessary modules, but at a later stage, you may need to update the modules when a new set of devices have to be supported. Knowing how to update the existing modules by creating the initrd image will enable you to provide support for new devices.

# ### initrd

![](bbox=[0.05, 0.33, 0.12, 0.42])

*initrd* refers to the initial ramdisk that is temporarily mounted as the root filesystem for loading startup programs and modules. The ramdisk loads along with the kernel, and its functionality is controlled by the kernel. initrd enables the system to be started in two phases. In the first phase, the system is booted with the minimum set of modules required to load the main or the permanent root filesystem. In the second phase, when the main root filesystem is mounted, the previously mounted initrd filesystem is removed and the ramdisk is released for installing additional modules on demand.

![](bbox=[0.38, 0.5, 0.85, 0.74])

Figure 8-6: The initrd starts the system in two phases.