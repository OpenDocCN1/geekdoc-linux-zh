![](bbox=[0.13, 0.07, 0.91, 0.53])

# **Figure 13.1**

Buildroot xconfig menu.

Buildroot offers the option of using an existing tool chain, rather than building a new one from source. Since we have a tool chain, that would seem like a sensible choice. In the Toolchain category, select Custom toolchain and Pre-installed toolchain. You can set the Toolchain path to, since the tool chain is in your PATH. Set the Toolchain prefix to arm-unknown-linux-gnueabi.

The External toolchain gcc version is most likely 4.9.x. In the previous chapter we built kernel version 3.8.13, so you would expect to select 3.8.x for External toolchain kernel headers series. It turns out though, that pretty much everything earlier than 4.1.x is no longer supported and if you select it, the build fails. So, even though we already have a Linux kernel source tree, if you want to use Buildroot, you will have to select one of their kernels.

Much of the rest of the Buildroot configuration has to do with selecting packages to install on the target. You will not need to select much here, because most utilities will be provided by Busybox, which we will go into in the next chapter.