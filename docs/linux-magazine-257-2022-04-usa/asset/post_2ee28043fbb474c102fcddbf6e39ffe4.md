
# NVIDIA Driver Install

In my experience, issues tend to be bugs. Don’t let that deter you, though, from trying some of the different packages out there for your particular NVIDIA card and Intel iGPU combo. However, Optimus itself isn’t something that I intend to get into here. Everything that I will outline here was done on a Supermicro X8STi with an entry-level NVIDIA GeForce GT 710 in the single PCIe X16 slot. (I have done the same on my Dell E6430 with an NVS 5200M and Intel iGPU and have actually gotten Optimus to work in the past; though again, that is not something that I intend to go over here for the reasons already mentioned.) If your machine has NVIDIA and Intel, my suggestion is to simply install the NVIDIA drivers and use the NVIDIA card. For me, there was no advantage to having Optimus working, because the battery was already shut and I was better off simply running NVIDIA full time on that machine for the performance, regardless of the electron abuse. Let’s go over how to find and install the correct drivers and deal with whatever aftermath may exist.

## Determining System Component Information

Once you have the machine up and running, you can check which drivers are being used by simply running the following:

```
lspci -vv
```

![](img/8286bf901ba268fe114d66ada92d1dd6_76_0.png)

This will show all of your PCI devices with details included (Figure 1). If you scroll down a bit, you will see one listed as VGA compatible controller: NVIDIA Corporation GK208B [GeForce GT 710], with the particular of your card listed here, instead of GT 710, obviously. When you look at the last two lines of that entry you will see Kernel driver in use and Kernel modules. Here you will see nouveau listed as the kernel driver in use, which, as mentioned, is the basic open source NVIDIA driver. If you are running Pop!_OS or a similar distribution which came with the proprietary NVIDIA drivers preinstalled, then you may see nvidia listed under Kernel driver in use, in which case this article isn’t for you, but most of you will likely see nouveau. As a side note, after Capabilities you will see access denied. To see this field, simply run the same command with sudo and you will have access to that information. This will give some additional information, such as power management, but isn’t needed for what we are doing.

This will take a few seconds, depending on your system. For me, it normally returns a complete response in about 15 seconds (Figure 2), so be patient here. My setup returns the following:

![](img/8286bf901ba268fe114d66ada92d1dd6_76_1.png)

## Finding Out What Driver Packages Are Available

At this point you have confirmed that the card was recognized and is running with the open source driver. To view which proprietary NVIDIA driver packages are available, you will want to run the following command now.

```
ubuntu-drivers devices
```

![](img/8286bf901ba268fe114d66ada92d1dd6_77_0.png)

### Figure 3: Terminal output of the apt list command.

As you can see here, there is more than one package available from NVIDIA along with the Nouveau open source driver. You can double check if your system has any NVIDIA packages installed by running:

```
$ apt list \*nvidia\* --installed
```

If you have installed any of these, they will be listed along with any dependencies that are required for them to run which are also present on your system, such as libraries and the settings dialog box package (Figure 3).

It is here that things can sometimes get a bit difficult. While all of these packages are available for your card, not all of them will work well, properly, or for that matter, at all, with your specific card. With that in mind you should at this point back up everything that you need to save somewhere safe and on a different machine, external drive, cloud storage, or (better yet) all of the above. Personally, I know that my GT 710 the best functioning package is listed as nvidia-driver-390, though frankly, I only know that through trial and error. Documentation on these packages is good and you can find more information about them at the NVIDIA website [1]. Personally, I had to learn this the hard way, by trying a package, uninstalling it when it failed, trying a different package, rinse and repeat. For that reason I would like to give a bit of a disclaimer here: If you install one of these packages and reboot to a black screen or have some other problem with your display, then be patient and don't fret just yet.

## Device Driver Installation

To install the package that you would like to try, simply run:

```
$ sudo apt update
$ sudo apt install nvidia-driver-390
```

and replacing the nvidia-driver-390 to the package of your choice for your specific GPU. Using the terminal here has the advantage that you can easily see what is going on, as opposed to using the GUI, which often leaves one wondering. Once the installation is completed and all dependencies have been installed, you will want to reboot your machine so that the new software can be loaded at boot. If you are lucky, you will be greeted with the login screen or desktop as you normally would. You can then check that your installation worked by either using the lspci -vv command discussed earlier or by opening settings and looking at the About section to see what is listed for Graphics. Mine shows GeForce GT 710/ PCIe/SS2 while mine the nvidia-driver-390 packages. As mentioned before, using lspci -vv will show nvidia under the Kernel driver in use section. You will also have the NVIDIA control panel installed for changing the particulars of your setup with a graphical interface.

## Troubleshooting and Resolving Issues

If you're not greeted with something graphical but rather a blank screen, then it is likely that the package is not in fact suitable for your GPU and will need to be removed. Don't panic just yet, however. This is a fairly easy and straightforward process as well. Reboot, and at the GRUB loading screen, instead of choosing a normal boot into Ubuntu, choose Advanced Options for Ubuntu and then choose the Ubuntu, with Linux… (recovery mode) option. The… will show the kernel that you are running and you can select the most recent kernel here. Make sure to select the recovery mode option (recovery).

Once in recovery mode you will want to choose root, with the description of Drop to root shell prompt. This will boot into a command line and from here you can get rid of the offending packages. Run the following to find out which NVIDIA packages are installed:

```
$ apt list \*nvidia\* --installed
```

Once you have seen what packages are there, you can use the following two commands in the following order to rid yourself of the NVIDIA packages. First use:

```
$ apt remove nvidia-driver-390 nvidia-settings nvidia-prime nvidia-dkms ... etc.
```

You will have many NVIDIA packages here, and listing all of them from the driver package itself with a space between them will remove all. This will get rid of dependencies and libraries so that when you try the next option you are starting from a clean slate. In the example above I listed a few of the packages that show up when I run the `ls` command, but there are about 20 or 22 of them in total. Once that is done, you will finalize the uninstallation by running the same but with `purge` instead of `remove`, à la:

```
$ apt purge nvidia-driver-390 nvidia-settings nvidia-prime nvidia-dkms ... etc.
```

This gets rid of any settings and configurations that may still be lingering after removal of the packages themselves. You can also do a quick cleaning with the following command after all of that.

```
$ apt autoremove
```

just to be sure that you have gotten everything out of there that can be removed.

When this is complete, simply type **reboot** and hit Enter to reboot the system. At this point you should see that the *nouveau* drivers are loaded and running instead of the proprietary NVIDIA ones. You can now try a different driver package by listing and installing as you did before, and I would recommend going to the next available lower number. In my experience most of the problems that I have had with installing NVIDIA drivers stem from the fact that my old cards aren't well supported on newer drivers, even though those newer drivers will show up when queried. Going to older available packages one at a time ensures that I have the most up-to-date set of packages available for my card which will run without problems.

## Concluding Remarks

I cannot express the amount of frustration I felt as a beginner around installing one of these only to have a blank screen be the result upon reboot. At that time, my solution was a complete reinstall of the OS, at which point I would try to use the open source driver package with its faults or go to a different NVIDIA driver and cross my fingers and hope for better results. Yes, I have reinstalled Ubuntu more than four times simply trying to get a driver package that worked. That is exactly why I think it is important not only to be comfortable with the terminal and with using the recovery mode, but also simply to know a bit about what is happening under the hood. Now that I have a method for recovery upon failure and have some

![](img/8286bf901ba268fe114d66ada92d1dd6_78_0.png)

confidence that I can get my system back to a working desktop, I can say that I simply find it easier and faster to use the terminal for the entire process. The added benefit here in my opinion is that you can actually see what is happening in the terminal rather than waiting, guessing, and hoping with the GUI equivalent (Figure 4).

Hopefully one day we will see the NVIDIA gang team up with our beloved open source community to produce a non-proprietary solution with the performance and benefits of the closed driver offering that currently exists. Until then I am afraid we are stuck with some of this hassle. Following the advice given above, however, you at least won't have to be stuck at a blank screen for too long after installing their solution onto your machine. I guess it really is as they say: You win some and you lose some.

## Info

- [1] NVIDIA: [https://www.nvidia.com/](https://www.nvidia.com/)
- [2] AMD Radeon graphics cards: [https://www.amd.com/en-us/graphics/radeon-rx-graphics](https://www.amd.com/en-us/graphics/radeon-rx-graphics)
- [3] Ubuntu: [https://ubuntu.com/](https://ubuntu.com/)
- [4] Red Hat Enterprise Linux: [https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux](https://www.redhat.com/en/technologies/linux-platforms/enterprise-linux)
- [5] Fedora Linux: [https://getfedora.org/](https://getfedora.org/)
- [6] Nouveau Xorg driver: [https://launchpad.net/nouveau](https://launchpad.net/nouveau)
- [7] SteamOS and Linux titles: [https://store.steampowered.com/linux](https://store.steampowered.com/linux)
- [8] Pop!\_OS by system76: [https://pop.system76.com/](https://pop.system76.com/)
- [9] YouTube: Gaming on Linux is NOT Rng: [https://www.youtube.com/watch?v=RY4K16ujFw](https://www.youtube.com/watch?v=RY4K16ujFw)
- [10] NVIDIA Optimus technology: [https://www.nvidia.com/en-us/geforce/technologies/optimus-technology/](https://www.nvidia.com/en-us/geforce/technologies/optimus-technology/)
- [11] Intel GPUs: [https://www.intel.com/content/www/us/en/products/discrete-gpus.html](https://www.intel.com/content/www/us/en/products/discrete-gpus.html)
- [12] Supermicro X8STi: [https://www.supermicro.com/products/motherboard/Xeon3000/X58/X8STi.cf](https://www.supermicro.com/products/motherboard/Xeon3000/X58/X8STi.cf)
- [13] Dell Latitude E-series laptops: [https://www.dell.com/](https://www.dell.com/)
