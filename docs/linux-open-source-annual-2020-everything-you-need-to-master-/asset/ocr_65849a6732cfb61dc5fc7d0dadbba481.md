# Distros

# # Brimming with features
Remix a Fedora installation into a distributable distribution.

The secret for creating Fedora-based distros is the *livecd-creator* script that’s part of the *livecd-tools* package. Grab it from the Fedora repositories with `dnf install livecd-tools`. Unlike *BoothBuilder*, *livecd-creator* works solely on the command line.

The scripts use a definition in a **Kickstart** file to set up your customized Fedora-based distro. In simple terms, a **Kickstart** file is a text file that contains a list of actions such as the name of packages to install (or remove). The *livecd-creator* tool compiles your distro as per the instructions in this file. To help you get started, you can download the **Kickstart** files for several Fedora spins by grabbing the *spin-kickstarts* package from the Fedora repositories with `dnf install spin-kickstarts`. Once this is installed, you’ll have a bunch of **Kickstart** files under the /usr/share/spin-kickstarts directory. You can customise any of these **Kickstart** files by editing them.

They are well documented and fairly easy to comprehend; browse the Fedora wiki ([http://fedoraproject.org/wiki/Anaconda/Kickstart](http://fedoraproject.org/wiki/Anaconda/Kickstart)) to get a hang of the various options. If you need to generate one from scratch, you can save yourself a lot of time by grabbing the **Kickstart** Configurator tool with `dnf install system-config-kickstart`. This tool has an easy-to-navigate graphical interface to help create a **Kickstart** file.

# ## Kick-start the process

For our purpose we’ll create a Mate-based Fedora remix by modifying the *fedora-live-mate_compiz.ks* file. The three main parameters in a *kickstart* file are `%pre`, `%post` and `%packages`. You can also pull in instructions from another *kickstart* file by specifying its name and location with the `%include` parameter, such as `%include fedora-mate-common.ks`. You’ll notice three such lines at the top of the *fedora-live-mate_compiz.ks* file.

The first one calls the *fedora-live-base.ks* file. This file describes the basic skeleton for creating a Fedora Live CD. The parameters are self-explanatory. There’s one each for the default language, keyboard and timezone followed by security settings that dictate the use of standard shadow passwords and so on. Here, we’d like to note that while the default for SELinux is set to enforcing mode, it hindered with the smooth functioning of some for our builds and we had to change the default SELinux policy for the customised distro to the permissive mode.

The `xconfig` set to `--startxnomode` asks the live CD to boot straight to a graphical login screen. There’s also an entry to create a root (/) partition and another to enable and disable the default services.

Also included in the *fedora-live-mate_compiz.ks* file is the *fedora-mate-common.ks* file that contains a list of packages for the Mate desktop with the Compiz compositor. Any packages you want inside your custom distro needs to be listed under the `%packages` section. In addition to individual packages, you can also specify groups of packages such as `@mate` and `@libreoffice`. If you install a group of packages you can remove individual components inside it by prefixing a minus (-) sign to their name, such as *-fedora-icon-theme*. These packages are

# ## MANUAL REMASTERING

While the scripts covered in this feature simplify the process of converting a Linux installation into a Live distributable medium, it’s pretty simple to step through the process manually. The advantage of this approach is that you can customise any distribution irrespective of the one running on the host. So for example, you can use this to create a customised Ubuntu-based distro using a Fedora installation.

Before you get started, you’ll need the *squashfs-tools* package to compress the filesystem of your custom distro as well as the *genisoimage* package to roll your distro into an ISO image. Both of these are usually available in the official repositories of most distributions. Next, grab the ISO image of the distro you wish to customise and loopback mount it. Then extract its contents into a folder. Use the `unsquashfs` command (part of the *squashfs-tools*) to extract the compressed filesystem. For Ubuntu-based distros like Mint this is the *filesystem.squashfs* file under the *casper* directory. For Fedora it’s *squashfs.img* under the LiveOS directory.

After uncompressed the filesystem, chroot into it. Preparing the chroot environment needs to be done carefully. Once inside the uncompressed filesystem you can use the distro’s package management system to add and remove packages and also modify any configuration file. Then remove any temp files before exiting the chroot environment. Now all you need to do is regenerate the manifest, compress the filesystem and roll it into an ISO image.

![](bbox=[0.06, 0.85, 0.42, 0.98])

Use **LiveCD** to prepare the chroot environment and create custom Debian, Ubuntu and Arch-based distros.

![](bbox=[0.55, 0.85, 0.95, 0.98])

The **Kickstart** Configuration tool is a real time-saver, especially when you want to generate a kick-start file from scratch.