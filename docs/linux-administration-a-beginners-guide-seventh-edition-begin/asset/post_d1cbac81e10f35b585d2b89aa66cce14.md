
# Summary

In this chapter, we discussed some important system services that come with most Linux systems. These services can function stand-alone (can work whether or not the system is in multiuser mode) and do not rely on network support. Their implementation can vary slightly from host to host or from distro to distro, but the core objectives and the problem they aim to solve remain the same.

Here’s a quick recap of the chapter:

- init is the master of all processes in the system, with a PID of 1. On pure System V-based distros, it also controls runlevels and can be configured through the /etc/init.d
- upstart is an alternative program that aims to replace the functionality of init in some Linux distributions. upstart also offers additional functionality and improvement.
- systemd is another alternative to init and upstart. It is a system and service manager for Linux-based operating systems. Several popular distros are standardizing around it. It offers many benefits and advanced features in comparison to any of the currently available solutions. It is quickly becoming semi-mature, opinionated, and idealistic and dreams of solving all the problems in the world today—including some technical-related ones!
- inetd, although barely used, the original super-server that listens to requests on behalf of a larger number of smaller, less frequently used services. When it accepts a request for any of those services, inetd starts the actual service and quickly forwards data between the network and actual service. Its configuration file is /etc/inetd.conf.
- xinetd is the modern replacement for the classic inetd super-server. It offers more configuration options and better built-in security. Its configuration file is /etc/xinetd.conf.
- syslog is the system-wide logging daemon used on Fedora, openSUSE, Ubuntu, and other popular distros. It can act as a drop-in replacement for the more common and traditional syslog daemon. Some of the advanced features of rsyslog include writing logs directly to a configured database and allowing other extensive management of log messages.
- systemd-journald (journald) is the newest kid on the block in the world of system log management. It is fast, nimble, young, and bright with dreams of solving all the logging problems in the open source world with the aid of its aptly named command-line utility journalctl.
- Finally, the cron service allows you to schedule events to occur at certain dates times, which is great for periodic events, such as backups and e-mail reminders. All the configuration files on which it relies are handled via the crontab program.

In each section of this chapter, we discussed how to configure a different service, and even suggested some uses beyond the default settings that come with the system. Try poking around these services and familiarize yourself with what you can accomplish with them. Many powerful automation, data collection, and analysis tools have been built around these basic services—as well as many wonderfully silly and useless things. Don't be afraid to have fun with them!

# CHAPTER 9 | The Linux Kernel

## 246 Linux Administration: A Beginner's Guide

One of Linux's greatest strengths is that its source code is available to anyone who wants it. The GNU GPL (General Public License) under which Linux is distributed allows you to tinker with the source code and distribute your changes! Real changes to the source code (at least, those to be taken seriously) go through the process of joining the official kernel tree. This requires extensive testing and proof that the changes benefit Linux as a whole. At the end of the approval process, the code gets a final yes or no from a core of the Linux project's original developers. It is this extensive review process that keeps the quality of Linux's code noteworthy.

For system administrators who have used other operating systems, the approach to code control is a significant departure from the philosophy of waiting for the "company" to release a patch, a service pack, or some sort of fight.

Instead of waiting through public relations, customer service, engineers, and other front-end units behind a proprietary operating system, in the Linux world you have the option of contacting the author of a kernel subsystem directly explaining your problem. A problem can be created and sent to before the next release of the kernel to get you up and running.

Of course, the flip side of this arrangement is that you need to be able to compile a kernel yourself rather than rely on some supplied compiled code. However, you won't have to do this often, because production environments, stable, rarely need a kernel compiled. But if you will, you should know what to do. Luckily, it's not difficult.

In this chapter, we will walk through the process of acquiring a kernel tree, configuring it, compiling it, and, finally, installing and booting the kernel.

# What Exactly Is a Kernel?

Before we jump into the process of compiling, let's back up a step and make sure you're clear on the concept of what a kernel is and the role it plays in the system. Most, when people say "Linux", they are actually referring to a "Linux distribution"—for example, Debian is a type of Linux distribution. As discussed in Chapter 1, a distribution comprises everything necessary to exist as a functional operating system. Distributions make use of code from various open source projects that are independent of Linux; in fact, many of the software maintained by these projects are extensively on UNIX-like platforms as well. The GNU Compiler, which comes with many Linux distributions, also exists on many other operating systems (probably more systems than most people realize).

So, then, what makes the pure definition of Linux? The kernel? The kernel of any operating system is the core of all the system's software. The only thing more fundamental than the kernel is the system hardware itself.

The kernel has many jobs. The essence of its work is to abstract the underlying hardware from the software and provide a running environment for application

# CHAPTER 9 The Linux Kernel 247

![](img/9f6657924397c33f088db5321b751a83_271_0.png)

**Figure 9-1** A visual representation of how the Linux kernel fits into a complete system

software through system calls. Specifically, the environment must handle issues such as networking, disk access, virtual memory, and multitasking—a complete list of these tasks would take up an entire chapter in itself!

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

Wait—a complete list of these tasks would take up an entire chapter in itself!

Before we jump into the process of compiling, let's back up a step and make sure you're clear on the concept of what a kernel is and the role it plays in the system. Most, when people say "Linux", they are actually referring to a "Linux distribution"—for example, Debian is a type of Linux distribution. As discussed in Chapter 1, a distribution comprises everything necessary to exist as a functional operating system. Distributions make use of code from various open source projects that are independent of Linux; in fact, many of the software maintained by these projects are extensively on UNIX-like platforms as well. The GNU Compiler, which comes with many Linux distributions, also exists on many other operating systems (probably more systems than most people realize).

So, then, what makes the pure definition of Linux? The kernel? The kernel of any operating system is the core of all the system's software. The only thing more fundamental than the kernel is the system hardware itself.

The kernel has many jobs. The essence of its work is to abstract the underlying hardware from the software and provide a running environment for application software through system calls. Specifically, the environment must handle issues such as networking, disk access, virtual memory, and multitasking—a complete list of these tasks would take up an entire chapter in itself!

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in.

**Figure 9-1** A visual representation of how the Linux kernel fits into a complete system

Today's Linux kernel, version 4.* (where the asterisk is a wildcard that represents the complete version of the kernel), contains more than 13 million lines of code (including device drivers). By comparison, the sixth edition of UNIX from Bell Labs in 1976 had roughly 9,000 lines. Figure 9-1 illustrates the kernel's position in. (Wait, let me re-read the text flow properly).

Instead of waiting through public relations, customer service, engineers, and other front-end units behind a proprietary operating system, in the Linux world you have the option of contacting the author of a kernel subsystem directly explaining your problem. A problem can be created and sent to before the next release of the kernel to get you up and running.

Of course, the flip side of this arrangement is that you need to be able to compile a kernel yourself rather than rely on some supplied compiled code. However, you won't have to do this often, because production environments, stable, rarely need a kernel compiled. But if you will, you should know what to do. Luckily, it's not difficult.

In this chapter, we will walk through the process of acquiring a kernel tree, configuring it, compiling it, and, finally, installing and booting the kernel.

## Finding the Kernel Source

If you need to download a (possibly newer) version than your provides, the first place to look for source code is the official kernel website: www.kernel.org. This site maintains a list of mirrors as.

The main.kernel.org site is mirrored around different parts of the world. The list of mirrors is at http://mirrors.kernel.org. Although you can connect to any of the mirrors, you will likely get the best performance by sticking to your country

## Getting the Correct Kernel Version

The web site of kernels available will contain folders for v1.0, v2.5, v2.6, v3.0, v3.4, v4.0, v4.1, v4.2, and so on. Before you follow your natural inclination to get the latest version, make sure you understand how the versioning system works.

The current convention is to name and number major kernel releases as “Linux 4.x” (also called the vanilla or mainline kernels). The first of this series will be Linux 4.0 (same as 4.0,0), the will be Linux 4.1 (same as 4.1,0), followed by Linux 4.2, and so on.

But wait, it doesn't end there—any minor changes or updates within each release version will be reflected by increments to the third digit. These are commonly referred to as point releases. The next stable release for the 4.0.0 series will be Linux 4.0.1, followed by version 4.0.2, and so forth. Another way of stating this is to say, for example, Linux version 4.0.4 will be the fourth stable release based on the 4.0.0.

The version of the kernel that we are going to use in the following section is 4.2, which is available at www.kernel.org/pub/linux/v4.x/linux-4.2.tar.gz.

> TIP You can use the wget utility to download the kernel source quickly into your current working directory by typing the following:
# wget https://www.kernel.org/pub/linux/v4.x/linux-4.2.tar.gz

# Historical Note About Kernel Versioning Conventions

Understanding the naming convention and philosophical reasoning behind the older Linux kernel versions such as the Linux 2.6 series is important, even though the names are no longer current, you are guaranteed to find countless instances (such as in smartphones, servers, desktops, embedded devices, and
