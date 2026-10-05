
*-dkms* packages installed (check with dpkg -l "*-dkms*" | grep ii). The other packages are generally not needed (Unless you know how you need them!)

## 9.3. Building Custom Kali ISO Images

Kali Linux has a ton of functionality and flexibility right out of the box. Once Kali is installed, you can perform sorts of amazing feats with a little guidance, creativity, patience, and practice. However, you can also create a Kali build that it contains specific files or packages (to scale up or down performance and features) and can perform certain functions automatically. For example, the Kali ISO of Doom and the Kali Evil Wireless Access Point are both excellent projects that rely on a custom-built implementation of Kali Linux. Let's take a look at the process of rolling a custom Kali Linux ISO image.

Official Kali ISO images are built with live-build, which is a set of scripts that allows for complete automation and customization of all facets of Kali image creation. The live-build suite uses a directory structure input for its configuration. We store this configuration and some associated helper scripts in a live-build-config Git repository. We will use this repository as a basis for building customized images.

Before going further, you must know that the commands shown in this section are meant to be run on an up-to-date Kali Linux system. They are very likely to fail if run on a non-Kali system or if the system is out of date.

### 9.3.1. Installing Pre-Requisites

The first step is to install the packages needed and to retrieve the Git repository with the Kali live-build configuration:

```
# apt install curl live-build
[...]
# git clone https://gitlab.com/kalinux/build-scripts/live-build-config
# cd live-build-config
# ls
  auto build_all.sh build.sh kali-config README
```

At this point, you can create an updated (but unmodified) Kali ISO image just by running ./build.sh --verbose. The build will take a long time to complete as it will download all the packages to include. When finished, you will find the new ISO in the images directory.

> ^5https://www.offensive-security.com/kali-linux/kali-linux-iso-of-doom
> ⁶https://www.offensive-security.com/kali-linux/kali-linux-evil-wireless-access-port/
> ⁷http://debian-live.alioth.debian.org/live-build/

### 9.3.2. Building Live Images with Different Desktop Environments

The build.sh live-build wrapper that we provide is responsible for setting up the config directory that live-build expects to find. It can put in place different configurations depending on its --variant option.

The wrapper creates the config directory by combining files from kali-config/common and kali-config/variant-x, where X is the name of a variant given with the --variant parameter. When the option is not explicitly given, it uses default as the name of the variant.

The kali-config directory contains directories for the most common desktop environments:

- e17 for Enlightenment;
- gnome for GNOME;
- i3wm for the corresponding window manager;
- kde for KDE;
- lxde for LXDE;
- mate for the Mate Desktop Environment;
- xfce for XFCE.

The light variant is a bit special; it is based on XFCE and is used to generate the official “light” ISO images that contained a reduced set of applications.

You can easily create a live image using KDE as desktop environment with this single command:

```
# ./build.sh --variant kde --verbose
```

This concept of variant allows some high-level-defined customizations but if you take the time to read through the Debian Live System Manual, you will discover many other ways to customize the images, by changing the content of the appropriate sub-directory of kali-config. The following sections will provide more examples.

### 9.3.3. Changing the Set of Installed Packages

Once launched, live-build installs all the packages listed in package-lists/*.list.chroot files. The default configuration that we provide includes a package-lists/kali.list.chroot file, which lists kali-linux-full (the main meta-package pulling all the packages to include). You can comment out this and put another meta-package of your choice or include a precise set of packages. You can also combine both approaches by starting with a meta-package and adding supplementary packages of your choice.

> *https://www.xfce.org/*

> *http://debian-live.alioth.debian.org/live-manual/unstable/manual/live-manual.en.html*

With package-lists, you can only include packages that are already available in the official Kali repository. If you have custom packages, you can include them in the live image by placing the . deb files in a packages.chroot directory (for example kali-config/config-gnome/packages.chroot if you build the GNOME variant).

Meta-packages are empty packages whose sole purpose is to have many dependencies on other packages. They make it easier to install sets of packages that you want to install together. The kali-linux source package builds all the meta-packages provided by Kali Linux:

- kali-linux: the base system (it is pulled by all the other meta-packages)
- kali-linux-full: the default Kali Linux installation
- kali-linux-all: meta-package of all the meta-packages and other packages (almost everything that Kali provides so it is really huge!)
- kali-linux-sdr: Software Defined Radio (SDR) tools
- kali-linux-gpu: GPU-powered tools (tools making of the computing power available in your graphical card)
- kali-linux-wireless: wireless assessment and analysis tools
- kali-linux-web: web applications assessment tools
- kali-linux-forensic: forensic tools (finding evidence of what happened)
- kali-linux-voip: Voice Over IP tools
- kali-linux-pwtools: password cracking tools
- kali-linux-top10: the most popular tools
- kali-linux-rfid: RFID tools

You can learn these meta-packages when you create custom package lists for live-build. The full list of available meta-packages and the tools they include can be found at http://tools.kali.org/kali-metpackages

| Debconf Preseeding of Installed Packages |
| :--- |
| You can provide Debconf preseed files (see section 4.3.2, "Creating a Preseed File" [page 93] for explanations) as preseed/*.cfg files. They will be used to configure the packages installed in the live system |

### 9.3.4. Using Hooks to Tweak the Contents of the Image

live-build offers hooks that can be executed at different steps of the build process. Chroot hooks are executable scripts that you install as hooks/live/*.chroot files in your config tree and that are executed within the chroot. While chroot is the command that lets you changes the operating system’s root directory to a directory of your choice, it is also used by extension to designate a directory hosting a full (alternate) system tree. This is the case with live-build, where the chroot directory is the directory where the live system is being prepared. Since applications started in a chroot cannot see outside of that directory, the same goes with the chroot hooks: you can only use and modify anything available in chroot environment. We rely on those hooks to perform Kali customizations (see kali-config/common/hooks/live/kali-hacks.chroot).

Binary hooks (hooks/*.binary) are executed in the context of the build process (and not rooted anywhere) at the end of the process. You can modify the content of the ISO image built but not the live file system at this point, it has already been generated. We use this feature in Kali to make some changes to the default isolinus configuration.

### 9.3.5. Adding Files in the ISO Image or in the Filesystem

Another very common customization is to add files in the live system or in the ISO..

You can add files to the live system by putting them at their expected location below the includes.chroot directory. For example, we provide kali-config/common/includes.chroot/usr/lib/live/config/0031-root-password, which ends up as /usr/lib/live/config/0031-root-password in the live system.

You can add files to the ISO image by putting them at their expected location below the includes. binary config directory. For example, we provide kali-config/common/includes.binary/isolinus/splash.png to override the background image used by the Isolinus bootloader (which is stored in /isolinus/splash.png in the filesystem of the ISO image).

| Live-Boot Hooks |
| :--- |
| Scripts-in-live-boot- installed as /lib/live/config/XXXX-name are executed by the init script of the live-boot package. They reconfigure many aspects of the system to be suited for a live system. You can add scripts of your own to customize your live system at run-time: it's notably useful to implement a custom boot parameter for example. |

## 9.4. Adding Persistence to the Live ISO with a USB Key

### 9.4.1. The Persistence Feature: Explanations

Next, we will discuss the steps required to add persistence to a Kali USB key. The nature of a live system is to be ephemeral. All data stored on the live system and all the changes made are lost when you reboot. To remedy this, you can use a feature of live-boot called persistence, which is enabled when the boot parameters include the persistence keyword.
