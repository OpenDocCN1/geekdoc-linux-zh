# Configuring the ISDN Card

Like any normal device, the ISDN can be either PnP or non-PnP. This section discusses how to configure both types of cards.

# Non-PnP Controllers

Most non-PnP controllers come with their configuration utilities, which you should use to set up the controllers. You need to know the following:

+   - IRQ
+   - Memory base address
+   - IO port

Those controllers are recognized by the Linux drivers and need no further changes after setup. Remember that you can use dosemu to configure your controller using your controller's DOS software.

# PnP Controllers

PnP cards need special attention because they are not automatically configured. Refer to the section "Setting Up a PnP Modem" earlier in this chapter. The operation should be similar, except for some values that would differ and two extra variables to set (ISAC and H$CX). You must compile HiSax as modules to use PnP controllers if the following are true:

+   - You don't have a PnP BIOS.
+   - You have another operating system on the same system.

As you might know, the kernel is the first thing that loads and starts execution. If HiSax is built in the kernel, it will try to probe the resources in its configuration files on startup. In the case of PnP cards, the settings might change. Thus, HiSax will fail. Remember that isapnp does not start until the kernel boots.

> **NOTE** Some ISDN cards cannot use IRQ 12 or 15, so avoid using these interrupts.
> 
> You should not allow IRQ sharing for the ISDN controllers. This will result in improper connection or a drop in speed.

# Configuring ISDN Hardware via YaST

SuSE Linux made ISDN launching easy using YaST. If you have an active non-PnP card, YaST will do most of the work for you. Even if you don't have one, chances are that YaST will still do the work for you. Follow these steps:

+   1. Log in as root and start YaST.