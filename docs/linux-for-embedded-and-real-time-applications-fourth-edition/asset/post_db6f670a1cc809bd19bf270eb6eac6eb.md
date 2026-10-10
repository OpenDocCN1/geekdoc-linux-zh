
your primary objective, right? The Yocto Project includes a Software Development Kit (SDK) intended to ease application development.

The major features of the SDK are:
- Cross-tool chain with compiler, debugger, QEMU, and other miscellaneous tools
- Libraries, headers, and symbols
- Eclipse plug-in

There is a separate SDK for each architecture that Yocto supports. These are distributed in the form of very large (around 200 MB) shell scripts. Go to the Yocto downloads page and navigate to `releases/yocto/yocto-2.3//toolchain`. **Then `i686`** if your workstation is 32 bits or `x86_64` **if it is 64 bits.** Download `poky-glibc-x86_64-core-image-minimal-cortexaXhf-neon-toolchain-ext-2.3.sh`. You will need to run `chmod +x` on the file in order to execute it.

The default install location is `/opt/poky/2.3`. You can pass a `-d` option to the script to specify a different location. I chose to install it under `~/poky/2.3`. Like Poky itself, there is a configuration script that must be sourced to set up the environment. Run this command:

```
source environment-setup-cortexaXhf-neon-poky-linux-gnueabi
```

The Yocto Eclipse plug-in only works with the Neon version of Eclipse (notice the neon in the script file name). Installation is a bit different with Neon than with previous versions:
1. Go to the Eclipse web site and download the "installer" tarball
2. Expand that
3. `cd eclipse-installer`
4. Run `eclipse-inst`
5. Select `Eclipse for C/C++ Developers`
6. Specify the `Installation Folder`, and
7. Click `Install`.

Once you have Eclipse Neon running, there are several Eclipse plug-ins we need to install before installing the Yocto plug-in:
1. Select `Install New Software` **from** the Help menu
2. In the `Work with` drop-down, select `Neon-http://download.eclipse.org/releases/neon`
3. Expand `Linux tools`
4. **Check** the boxes for both entries: `C/C++ Remote (Over TCF/TE) Run/Debug Launcher` **and** `TM terminal`
5. Expand `Mobile and Device Development` **and** **check** the following:
   - `C/C++ Remote (Over TCF/TE) Run/Debug Launcher`
   - `Remote System Explorer User Actions`
   - `TCF Remote System Explorer add-in`
   - TCF Target Explorer
   - TM Terminal
6. Expand *Programming Languages* and select `C/C++ Development Tools SDK`
7. Click `Next` twice, accept the license terms and click `Finish`.

You are prompted to restart Eclipse for the changes to take effect. Not yet, because now we want to install the Yocto plug-in. Go back to `Install New Software:`
1. Click `Add...` in the `Work with` area
2. Enter `http://downloads.yoctoproject.org/releases/eclipse-plugin/2.3/` in the `Location` field, and provide some meaningful name in the `Name` field. Click `OK`
3. Check both of the entries that show up, click `Next` twice, accept the license, and click `Finish`. Interestingly enough, a `Security Warning` pops up that says the software is unsigned and its authenticity cannot be established. Go ahead and click `OK`.

Now you can restart Eclipse. You will find a new menu option, `Yocto Project Tools`. Also under `Window` > `Preferences` there is a dialog for `Yocto Project SDK`.

The *Yocto Project Software Development Kit (SDK) Developers' Guide 2.3*, available from the Documentation page of the Yocto Project website, has an excellent chapter on using the Eclipse plug-in. It in turn points to a wiki entry, with more details on setting up the plug-in.

## Personal Observations

Yocto is probably an improvement over OE-Core. At least it has some graphical tools. Nevertheless, like OE-Core, it is very big, very complex, and requires a steep learning curve. If you can invest the time in really learning it, then it is probably useful.

In the next chapter, we will tackle Busybox, the Swiss army knife of embedded Linux.

## Resources
- [www.buildroot.org](http://www.buildroot.org)—Website for the Buildroot project.
- [www.openembedded.org](http://www.openembedded.org)—Website for the Open Embedded project.
- [www.yoctoproject.org](http://www.yoctoproject.org)—Website for the Yocto Project.
- [http://downloads.yoctoproject.org](http://downloads.yoctoproject.org)—Downloads page for the Yocto Project.
- [www.python.org](http://www.python.org)—Website for python.
- [www.embedded.com/design/prototyping-and-development/42184900/Open-Embedded--An-alternative-way-to-build-embedded-Linux-distributions](http://www.embedded.com/design/prototyping-and-development/42184900/Open-Embedded--An-alternative-way-to-build-embedded-Linux-distributions)—An introductory paper on Open Embedded Core. It is a little old, but still useful.
- [https://hwn.net/Articles/682540/](https://hwn.net/Articles/682540/)—*Deciding Between Buildroot and Yocto* reports on a session at the 2016 Embedded Linux Conference that compared and contrasted Buildroot and the Yocto Project.

# BusyBox and Linux initialization

**Chapter Outline**

**Introducing BusyBox** 220

**Configuring and Installing BusyBox** 220

BusyBox Settings 222

Applets 224

Building and Installing 225

**Using BusyBox** 226

**User Space Initialization** 226

Stage 1 Boot Loader 226

Stage 2 MLO 227

U-Boot 227

Linux Kernel 227

Systemd 228

User Space Initialization, the “Old Way” 230

**Resources** 231

> *Linux: the choice of a GNU generation*

*ksh@cis.ufl.edu put this on T-shirts in 1993*

Very often the biggest problem in an embedded environment is the lack of resources, specifically memory and storage space. As you have no doubt observed, either in the course of reading this book, or from other experience, Linux is big! The kernel itself is often in the range of two to four megabytes, and then there is the root file system, with its utility programs and configuration files. Granted, our BBB is running a full Debian distro, but still, we are limited to the 4 GB eMMC, or a microSD card.

In this chapter, we will look at a powerful tool for substantially reducing the overall “footprint” of Linux to make it fit in limited resource embedded devices. The other topic we will address in this chapter is User Space initialization, and specifically the question of how to get our thermostat application to start at boot up.

## Introducing BusyBox

Even if your embedded device is “headless,” that is it has no screen and/or keyboard in the usual sense for user interaction, you still need a minimal set of command line utilities. You will no doubt need *mount*, *ifconfig*, and probably several others to get the system up and running. Remember that every shell command line utility is a separate program, with its own executable file.

The idea behind BusyBox is brilliantly simple. Rather than have every utility be a separate program with its attendant overhead, why not simply write one program that implements *all* the utilities? Well, perhaps not all, but a very large number of the most common utilities. Most utilities require the same set of “helper” functionality, such as parsing command lines and converting ASCII to binary. Rather than duplicating these functions in hundreds of files, BusyBox implements them exactly once.

The BusyBox project began in 1996, with the goal of putting a complete Linux system on a single floppy disk that could serve as a *rescue disk* or an installer for the Debian Linux distribution. A rescue disk is used to repair a Linux system that has become unbootable. This means the rescue disk must be able to boot the system and mount the hard disk file systems, and it must provide sufficient command line tools to bring the hard disk root file system back to a bootable state.

Subsequently, embedded developers figured out that this was an obvious way to reduce the Linux footprint in resource-constrained embedded environments. So the project grew well beyond its Debian roots, and today BusyBox is a part of almost every commercial embedded Linux offering, and is found in a wide array of Linux-based products, including numerous routers, and media players.

BusyBox calls itself the “Swiss army knife” of embedded Linux because, like the knife, it is an all-purpose tool. Technically, the developers refer to it as a “multi-call binary,” meaning that the program is invoked in multiple ways to execute different commands. This is done with symbolic links named for the various utilities. These links then all point to the BusyBox executable.

## Configuring and Installing BusyBox

The version of BusyBox running on my BBB is 1.20.2. Go to the website in the “Resources” section and download that version, or any other one that matches your board or strikes your fancy. Oddly, even though the BBB incorporates BusyBox, it appears there are only two links to it. This may be because we are running a Debian distro, and Debian itself does not use BusyBox.
