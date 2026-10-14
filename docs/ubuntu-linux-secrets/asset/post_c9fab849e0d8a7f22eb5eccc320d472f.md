
## Using Network Shares

If you have a Windows network, you can connect to any shared folders available on the network. If Ubuntu detects your network card properly, it’ll automatically attempt to connect to your network. It detects any Windows networks that appear on the network.

You can access your network shared folders from the LiveCD by selecting the Places menu item, then selecting either Network (to browse your Windows network) or Connect to Server (to connect directly to a specific server share). In either case, you’ll see the server and shares, as shown in Figure 2-14.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_71_0.png)

Just double-click on your server, then Share, and you can access files and folders (and write to files and folders) just like on any other Windows network device.

## Running Ubuntu in Windows

The main drawback to running Ubuntu directly from the LiveCD is that it’s slow. Sometimes it’s hard to get a good feel for how the software will run on a particular system because the LiveCD distorts how Ubuntu would run from the hard drive. Ubuntu has a solution for this.

## The Wubi Project

The Windows Ubuntu Installer (Wubi) project was created as an alternative to running Ubuntu from the LiveCD. Wubi creates a complete Ubuntu disk partition as a single file on a Windows operating system, then creates an entry in the standard Windows boot program that enables your PC to boot directly from the Ubuntu file.

This means that you can have a complete, bootable Ubuntu system by installing a single program on your Windows PC. Currently, Wubi supports Windows 95, 98, 2000, XP, and Vista.

## Installing in Windows

The main goal of Wubi is to make installing Ubuntu on an existing Windows PC easy, and they’ve accomplished their task. There are two ways to get Wubi:

- Install it directly from the Ubuntu workstation LiveCD.
- Download it from the Wubi web site.

If you have the Ubuntu workstation LiveCD, you already have the Wubi software. While in Windows, insert the LiveCD into your CD tray and either let the CD autorun or click the Autorun file. The Ubuntu LiveCD menu appears, allowing you to either restart your PC to boot from the LiveCD or to run the Wubi program. Running the Wubi program produces the Wubi setup window, shown in Figure 2-15.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_72_0.png)

Figure 2-15: The Wubi setup window.

## Part 1: Starting Out with Ubuntu

The Ubuntu setup window allows you to select the hard drive to install the Ubuntu files onto and how much disk space to use for your Ubuntu system. You'll want to allow at least 4 GB of space for your Ubuntu distribution files.

If you haven’t already downloaded the Ubuntu LiveCD, there's a great feature in Wubi that you can take advantage of. You can download the Wubi installation file from the Wubi web site and install Ubuntu in Windows without having to burn the LiveCD.

The Wubi web site (`http://wubi-installer.org`) provides a link to download just the Wubi setup program. Once you download the Wubi setup program and start it, it’ll automatically contact the Ubuntu web site and download the appropriate desktop LiveCD ISO image file for your PC. After the download completes, Wubi will mount the ISO image file—just as if it were on a CD—and start the Ubuntu installation.

## Running Ubuntu in Windows

After Ubuntu installs as a Windows application, you’ll see a new menu when you start your Windows PC, as shown in Figure 2-16.

![](img/39e65eeb4f54001ede08c6114ae3cc6c_73_0.png)

**Figure 2-16:** The Windows boot menu with Ubuntu installed.

The default menu item is your original Windows operating system. Selecting this option (or doing nothing and letting the counter count down) starts your Windows system, just as it always did before you installed Ubuntu. If you select the Ubuntu menu option, Ubuntu boots from the installed Ubuntu image file installed on your Windows system.

After the boot-up you'll get the Ubuntu login window, as if Ubuntu were installed on a hard drive partition. When you log in with the account you specified in the Wubi setup program, you’ll be at the Ubuntu desktop, with the entire application available for you to use. If you have a network interface card installed on your PC (and Ubuntu detected it), the Ubuntu software update program (discussed in Chapter 13, “Software Installs and Updates”) will automatically connect to the Ubuntu software repository and offer software updates for you.
