# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

management over the desire for "eye-candy", etc. You can also elect to run a Window Manager without a desktop environment. For example, the Enlightenment Window Manager is known for it's eye-candy and can run standalone, or with KDE or GNOME, etc.

Slack no longer comes with GNOME as an option, though it can be installed like any other application. During the base installation, you will be given a choice of KDE, XFCE, and some others. I would like to suggest XFCE. It provides a clearer interface for a beginner to learn. It is leaner and less resource intensive. You still have access to many KDE utilities, if you elected to install KDE during package selection. You can install more than one desktop and switch between them, if you like. The easiest way to switch is with the config command.

# The Linux Kernel

The Linux kernel is the "brain" of the system. It is the base component of the Operating System that allows hardware to interact with and manage other software and resources.

As with all forensic tools, we need to have a clear view of any kernel version we interact with our forensic platforms and subject hardware. Almost all current distributions of Linux already come with a version 4 kernel installed by default, including Slack (4.4).

You can determine your current kernel version with the uname command:

```
root@forensic1# uname -a
Linux forensic 4.4.14 #2 SMP Fri Jun 24 13:38:27 CDT 2016 x86_64 Intel(R) Core(TM) 15-3550 CPU @ 3.30GHz GenuineIntel/Linux
```

The key to the safe forensic use (from an evidentiary standpoint) of ANY system is knowledge of your environment and proper testing. Please keep in mind. You MUST understand how your hardware and software interact with any given operating system before using it in a "production" forensic analysis. If for some reason you feel the need to upgrade your kernel to a newer version (either through automated updates or manually), make sure you read the documentation and changelog so you have an understanding of any significant architectural changes that impact the forensic environment.

One of the greatest strengths Linux provides is "total control". This requires thorough testing and understanding. Don't lose sight of this in pursuit of an "easy" desktop experience.

# Kernel and Hardware Interaction

In this section, we will focus on the minimum configuration knowledge for baseline understanding of a sound forensic environment under current Linux distributions. We will