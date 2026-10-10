# *DVD or Live CD?*

Most Linux distributions are available in at least three forms: a DVD, a collection of CDs (up to about six side days), or a *Live CD*. A Live CD is a minimal bootable Linux system that gives you an opportunity to play around with a new distribution without actually installing it. Of course you can’t save any data or modify the configuration. Every time it boots it reverts to the default configuration.

One of the options the Live CD offers is to install the distribution. When you select this option, it runs through essentially the same installation process as you would with a DVD or complete set of CDs. The difference is that packages to install are pulled from the network rather than from physical media.

# *Installation Process*

Regardless of which scenarior installation medium you choose, the installation process is pretty much the same. This section describes CentOS installation, but other distributions have a very similar process:

+   - Download the distribution medium (see resources section). This will be a .iso file, an exact image of either a DVD or a Live CD.
+   - Burn the .iso to the corresponding physical medium. You’ll need a disk burning program to transfer the .iso file(s) to physical media. In a virtual machine environment, you can mount the .iso file directly as if it were a CD or DVD.
+   - Boot the computer from the installation medium or click the install icon from a Live CD. You may have to configure your PC’s BIOS to boot from optical media.
+   - Follow the instructions.

The installation process itself is fairly straightforward. With CentOS, you start by selecting a language, which defaults to United States English. Clicking Continue brings up the `INSTALLATION SUMMARY` dialog shown in Fig. 2.4.

Under `SOFTWARE SELECTION`, I suggest selecting `KDE Plasma Workspaces` as your base environment. That’s only because I happen to prefer the KDE graphical desktop environment over GNOME and, to the extent that the remainder of the book displays graphical desktop images, they will be KDE. I just happen to like the KDE presentation better. It’s more “Windows-like.” The truth is, I am most of my day-to-day computing work in Windows (hey, I’m writing this book in Word). If you’ve spent much of your career in front of a Windows screen, I think you’ll find KDE more to your liking. But if you have a strong preference for GNOME, by all means, select it or the `Development and Creative Workstation`. At a minimum, you should select `Development Tools` under `Add-Ons`. If you’re going with the KDE Plasma Workspace you might also want to select `KDE Applications`.