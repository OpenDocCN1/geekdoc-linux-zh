# Chapter 1 \ Installing SUSE 10 27

One of the most important reasons for editing the default boot loader configuration is to add a Linux kernel option at startup. If your hardware manufacturer has notified that a certain value must be passed to the Linux kernel at boot time, you would append it to the "Other parameters" section of the configuration log box. When you are happy with the boot loader item configuration, click OK to return to the boot loader overview screen.

A few common kernel parameters that we have come in recent years are not and acpi. Both of these parameters are relevant to modern machines. The first, will turn off Linux's support of the Intel processor's threading feature. In certain processor-bound workloads, it is better to turn off hyperthreading to improve performance. The second, acpi, turns off Linux's ACPI infrastructure. ACPI is the Advanced Configuration and Power Interface and is a standardized way for an operating system to control machine power, BIOS settings, and so on. In some situations ACPI actually stops Linux from booting on certain machines. Using the boot loader configuration to set these parameters enables you to control this before a system is installed.

When you make any changes that you want on the Boot Loader setup screen, click the Finish button to return to the standard YaST installer screen.

# Changing the Default Runlevel

Runlevels are discussed in detail in Chapter 4. As a quick summary, a system's runlevel determines the services that are automatically started when your system boots. The YaST Expert Installation Settings screen can be used to change the default runlevel of the system by clicking the Default Runlevel heading in YaST's Installation panel or by clicking the Button and selecting Default Runlevel from the pop-up menu.

As you can see in Figure 1-19, you can choose to boot your SUSE in a variety of different ways: without networking functionality (runlevel 2), multisuser without networking (runlevel 3), or multisuser with X Windows (runlevel 5). The default runlevel in a standard installation is runlevel 5, multisuser with X Windows. You should keep this your default runlevel unless you have a specific reason to change it.

When you make any changes that you want to your system's default runlevel, click OK to set the selected runlevel as your system default. The Set Default Runlevel pop-up closes, and YaST's Installation Setting panel displays.