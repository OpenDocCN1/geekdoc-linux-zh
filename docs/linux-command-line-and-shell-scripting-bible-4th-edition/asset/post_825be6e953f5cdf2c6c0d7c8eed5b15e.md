
applications that support features such as word processing, spreadsheets, databases, drawing, and, of course, multimedia support. **Table 1-4** shows some of the smaller Linux graphical desktop environments that can be used on lower-powered PCs and laptops.

![](img/a5025f22e05b92f409563a958cac7312_47_0.png)

**FIGURE 1-5** The Cinnamon desktop from Linux Mint

### TABLE 1-4 Other Linux Graphical Desktops

| Desktop | Description |
| :--- | :--- |
| Fluxbox | A bare-bones desktop that doesn't include a Panel, only a pop-up menu to launch applications |
| Xfce | A desktop that's similar to the GNOME 2 desktop but with less graphics for low-memory environments |
| JWM | Joe's Window Manager, a very lightweight desktop ideal for low-memory and low–disk space environments |
| fvwm | Supports some advanced desktop features such as virtual desktops and Panels, but runs in low-memory environments |
| fvwm95 | Derived from fvwm but made to look like a Windows 95 desktop |

These graphical desktop environments are not as fancy as the KDE Plasma and GNOME 3 desktops, but they provide basic graphical functionality just fine. **Figure 1-6** shows what the Xfce desktop used in the MX Linux distribution looks like.

![](img/a5025f22e05b92f409563a958cac7312_48_0.png)

**FIGURE 1-6** The Xfce desktop as seen in the MX Linux distribution

If you are using an older PC, try a Linux distribution that uses one of these desktops and see what happens. You may be pleasantly surprised.

## Examining Linux Distributions

Now that you have seen the four main components required for a complete Linux system, you may be wondering how you are going to get them all together to make a Linux system. Fortunately, there are people who have already done that for you.

A complete Linux system package is called a *distribution*. Numerous Linux distributions are available to meet just about any computing requirement you could have. Most distributions are customized for a specific user group, such as business users, multimedia enthusiasts, software developers, or average home users. Each customized distribution includes the software packages required to support specialized functions, such as audio- and video-editing software for multimedia enthusiasts, or compilers and integrated development environments (IDEs) for software developers.

The different Linux distributions are often divided into two categories:

- Full-core Linux distributions
- Specialized distributions

The following sections describe these types of Linux distributions and show examples in each category.

### Core Linux distributions

A core Linux distribution contains a kernel, one or more graphical desktop environments, and just about every Linux application that is available, precompiled for the kernel. It provides one-stop shopping for a complete Linux installation. *Table 1-5* shows some popular core Linux distributions.

**TABLE 1-5 Core Linux Distributions**

| Distribution | Description |
| :--- | :--- |
| Slackware | One of the original Linux distribution sets; popular with Linux geeks |
| Red Hat Enterprise | A commercial business distribution used mainly for Internet servers |
| Gentoo | A distribution designed for advanced Linux users, containing only Linux source code |
| openSUSE | Different distributions for business and home use |
| Debian | Popular with Linux experts and commercial Linux |

In the early days of Linux, a distribution was released as a set of floppy disks. You had to download groups of files and then copy them onto disks. It would usually take 20 or more disks to make an entire distribution! Needless to say, this was a painful experience.

Nowadays, Linux distributions are released as an *ISO image file*. The ISO image file is a complete disk image of a DVD as a single file. You use a software application to either burn the ISO image file onto a DVD or create a bootable USB stick. You then just boot your workstation from the DVD or USB stick to install Linux. This makes installing Linux much easier.

However, beginners still often run into problems when they install one of the core Linux distributions. To cover just about any situation in which someone might want to use Linux, a single distribution has to include lots of application software. They include everything from high-end Internet database servers to common games.

Although having lots of options available in a distribution is great for Linux geeks, it can become a nightmare for beginning Linux users. Most core distributions ask a series of questions during the installation process to determine which applications to load by default, what hardware is connected to the PC, and how to configure the hardware. Beginners often find these questions confusing. As a result, they often either load way too many programs on their computer or don’t load enough and later discover that their computer won’t do what they want it to.

Fortunately for beginners, there’s a much simpler way to install Linux.

### Specialized Linux distributions

A new subgroup of Linux distributions has started to appear. These are typically based on one of the main distributions but contain only a subset of applications that would make sense for a specific area of use.

In addition to providing specialized software (such as only office products for business users), customized Linux distributions attempt to help beginning Linux users by autodetecting and autoconfiguring common hardware devices. This makes installing Linux a much more enjoyable process.

Table 1-6 shows some of the specialized Linux distributions available and what they specialize in.

### TABLE 1-6 Specialized Linux Distributions

| Distribution | Description |
| :--- | :--- |
| Fedora | A free distribution built from the Red Hat Enterprise Linux source code |
| Ubuntu | A free distribution for school and home use |
| MX Linux | A free distribution for home use |
| Linux Mint | A free distribution for home entertainment use |
| Puppy Linux | A free small distribution that runs well on older PCs |

That's just a small sampling of specialized Linux distributions. There are literally hundreds of specialized Linux distributions, and more are popping up all the time on the Internet. No matter your specialty, you'll probably find a Linux distribution made for you.

Many of the specialized Linux distributions are based on the Debian Linux distribution. They use the same installation files as Debian but package only a small fraction of a full-blown Debian system.

> **NOTE**
> Most Linux distributions also have a LiveDVD version available. The LiveDVD version is a self-contained ISO image file that you can burn onto a DVD (or USB stick) to boot up a running Linux system directly, without having to install it on your hard drive. Depending on the distribution, the LiveDVD contains either a small subset of applications or, in the case of specialized distributions, the entire system. The benefit of the LiveDVD is that you can test it with your system hardware before going through the trouble of installing the system.

## Summary

This chapter discussed the Linux system and the basics of how it works. The Linux kernel is the core of the system, controlling how memory, programs, and hardware all interact with one another. The GNU utilities are also an important piece in the Linux system. The Linux shell, which is the main focus of this book, is part of the GNU core utilities. The chapter also discussed the final piece of a Linux system, the Linux desktop environment. Things have changed over the years, and Linux now supports several graphical desktop environments.

The chapter also discussed the various Linux distributions. A Linux distribution bundles the various parts of a Linux system into a simple package that you can easily install on your PC. The Linux distribution world consists of full-blown Linux distributions that include just about every application imaginable, as well as specialized Linux distributions that only include applications focused on a special function. The Linux LiveDVD craze has created another group of Linux distributions that allow you to easily test-drive Linux without even having to install it on your hard drive.

In the next chapter, we look at what you need to start command-line and shell scripting experience. You'll see what you have to do to get to the Linux shell utility from your fancy graphical desktop environment. These days, that's not always an easy thing.
