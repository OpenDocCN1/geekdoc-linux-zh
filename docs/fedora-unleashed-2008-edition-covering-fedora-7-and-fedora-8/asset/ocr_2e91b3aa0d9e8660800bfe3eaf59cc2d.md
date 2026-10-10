+   11. Run `make modules_install` to install the modules in `/lib/modules` and create dependency files.

+   12. Run `make install` to automatically copy the kernel to `/boot`, create any other files it needs, and modify the bootloader to boot the new kernel by default.

+   13. Using your favorite text editor, verify the changes made to `/etc/lilo.conf` or `/boot/grub/grub.conf`; fix if necessary and rerun `/sbin/lilo` if needed.

+   14. Reboot and test the new kernel.

+   15. Repeat the process if necessary, choosing a configuration interface.

Over time, the process for configuring the Linux kernel has changed. Originally, you configured the kernel by responding to a series of prompts for each configuration parameter (this is the `make config` utility described shortly). Although you can still configure Linux this way, most users find this type of configuration confusing and inconvenient; moving back through the prompts to correct errors, for instance, is impossible.

The `make config` utility is a command-line tool. The utility presents a question regarding kernel configuration options. The user responds with a Y, N, M, or ? (it is not case sensitive). Choosing `M` configures the option to be compiled as a module. A response of `?` displays context help for that specific option, if available. (If you choose `?` and no help is available, you can turn to the vast Internet resources to find information.) We recommend that you avoid the `make config` utility, shown in Figure 36.1.

![](bbox=[0.05, 0.51, 0.94, 0.83])

**FIGURE 36.1** The `make config` utility in all its Spartan glory.