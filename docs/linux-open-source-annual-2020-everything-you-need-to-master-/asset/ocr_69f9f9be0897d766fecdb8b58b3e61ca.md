# Architect your castle

Base your custom spin on the popular DIY Linux distribution.

While both `buildhopper` and `livced-creator` enable you to create a customised spin with a fair amount of tweaks, if you have the patience to hand-craft an installation from scratch, Arch Linux offers a more comprehensive approach. Arch is an ideal platform for cultivating a custom distro without the code bloat and package proliferation that afflicts so many other popular ones. The Archiso package is a collection of bash scripts that you can use to convert your Arch installation into a distributable distro. Like the distro it works on, Archiso has a steep learning curve, but gives you a lot of control over the final result.

The first thing you need before you can use Archiso is an Arch Linux installation. If you're new to Arch, the process is well documented on the project’s wiki page ([https://wiki.archlinux.org/index.php/Installation_guide](https://wiki.archlinux.org/index.php/Installation_guide)). Another option is to use an installation of a pure Arch-based distribution like Antergos, Archolinux, Chakra or Manjaro. In fact, some of these distros, like Manjaro have their own fork of the Archiso script.

![](bbox=[0.52, 0.2, 0.98, 0.35])

> You can use `archiso-offline-releas` to create a custom distro that'll only use locally hosted packages instead of fetching them from online repos.

In any case, once you've installed Arch on your computer, the next step is to customise it to your liking. That includes installing more packages, swapping out the default themes and artwork of your desktop environment and configuring other aspects of the systems such as the network. As usual we'll copy these customisations and configurations from the installed instance of Arch over to the custom distro we're building. When you're done customising the Arch installation, fire up a terminal and install Archiso and its dependencies with

```
make squashfs-tools libisoburn

dfstools patch lfs develos git archiso
```

Next, create a directory where we'll tweak the files for our custom distro with `mkdir ~/archlive`. Make sure you have enough free disk space to accommodate all the programs you wish to install, along with any files you want to copy over to the custom distro. Archiso comes with two predefined profiles.

The baseline profile is useful for creating a basic live system with no pre-installed packages. However, we'll use the releas profile, which enables you to create a fully customised Arch Linux with pre-installed apps. To use these scripts, simply copy them over to the `~/archlive` directory, like so:

```
cp -r /usr/share/archiso/configs/releas/ ~/archlive/
```

# Package 'em up

To put packages on the custom distro all you need to do is list them in the `packages.x86_64` file under the newly created `archlive` directory. The file already contains a list of essential Arch packages and you can manually add to it with a text editor. Since you goal is to mirror your Arch installation, use the `pacman -Qqe > ~/archlive/packages.x86_64` command to dump the name of all the installed packages in that file.

The `airroot` directory inside `~/archlive/` acts as an overlay for what will be the root directory of your new distribution. Any files you add to this directory will be added to your distro's filesystem. So for example, if you want your custom distro to have the same users as your host machine, copy over the relevant files with:

# FROM BOYS TO MEN

The scripts in this feature will help you turn your installed flavour of Linux into a distributable medium that you can then pass around. And there's nothing wrong with that. But if you really want to get a feel for what it takes to create a custom distribution, from the grounds up, then you need to lock yourself in a room for a week with a copy of `Linux From Scratch` ([www.linuxfromscratch.org](www.linuxfromscratch.org)). Linux From Scratch or LFS as its popularly known, is actually a book, which painstakingly hand-holds you through the time-consuming process of putting together your own Linux distribution. The book's offered as a free download and you can even grab a printed edition at the bookstores. Once you're through with LFS, you'll find you with a system that's very secure, very flexible and also very compact.

But the process doesn't stop here. As per the LFS FAQ ([www.linuxfromscratch.org/blfs](www.linuxfromscratch.org/blfs)), "LFS is not intended to create your system as you want it. It's intended to be just enough to allow you to build your system as you want it. It's not an end, it's a beginning. When you're done with LFS, you're just started building your system."

This is where Beyond Linux From Scratch or BLFS ([www.linuxfromscratch.org/blfs](www.linuxfromscratch.org/blfs)) comes into picture. BLFS is a much bigger manual that covers everything from installing system libraries to programming utilities, from network libraries to server applications, from simple and lightweight window managers like `fluxbox` to complex but popular ones such as KDE and Gnome.

The project was started in 1999 when its author, Gerhard Beckmans, wanted to learn how a Linux distro works behind the scenes. While building his system from scratch, Beckmans wrote down the steps and released it as a how-to, thinking that there would probably be other people who would be interested.

LFS has grown quite a bit from its humble start. Besides BLFS, the project has spawned a couple of other books. There's ALFS or Automated LFS, to help automate the process of creating an LFS system, and CLFS or Cross LFS that focuses on cross compiling.