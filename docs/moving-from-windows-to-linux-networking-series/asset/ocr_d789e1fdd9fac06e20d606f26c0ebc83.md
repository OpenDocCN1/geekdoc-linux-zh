# ## Continuing with the Installation

Once you have finished with Disk Druid, there are still some steps to take before installation is complete. The next screen will list the operating systems on your PC. If you are not dual booting, you should see just one, Linux. If you are dual booting, you can select which operating system you want to be the default. This is shown in Figure 2.10.

![](bbox=[0.06, 0.19, 0.65, 0.51])

**Figure 2.10: Selecting an operating system.**

When your machine first starts, you will be given a display listing these operating systems, and you will be given a few moments to select one. If you do not make a selection, the default will be selected for you. You should note that what this screen is doing is configuring your *boot loader*. A boot loader is just a small program that loads the operating system into memory. During your boot phase, it loads the operating system, thus the name boot loader. Many Linux distributions use the *LILO* (Linux load) boot loader software. Red Hat 9.0 uses a newer boot loader, *GRUB* (Grand Unified Boot Loader). Among other things, GRUB makes dual booting much easier.

The next stage of the installation is to configure your network adapter. The network adapter, also called a NIC (network interface card), is simply the card that you plug a network cable into. If this is a stand-alone home machine, leave the default settings shown in Figure 2.11.