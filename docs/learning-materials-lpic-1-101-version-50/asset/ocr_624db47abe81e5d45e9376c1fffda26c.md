# # 101.2 Lesson 1

| | | 
|---|---|
| **Certificate:** | LPIC-1 |
| **Version:** | 5.0 |
| **Topic:** | 101 System Architecture |
| **Objective:** | 101.2 Boot the system |
| **Lesson:** | 1 of 1 |

# ## Introduction

In order to control the machine, the operating system's main component — the kernel — must be loaded by a program called a *bootloader*, which itself is loaded by a pre-installed firmware such as BIOS or UEFI. The bootloader can be customized to pass parameters to the kernel, such as which partition contains the root filesystem or in which mode the operating system should execute. Once loaded the kernel continues the boot process identifying and configuring the hardware. Lastly, the kernel calls the utility responsible for starting and managing the system's services.

> NOTE On some Linux distributions, commands executed in this lesson may require root privileges.

# ## BIOS or UEFI

The procedures executed by x86 machines to run the bootloader are different whether they use