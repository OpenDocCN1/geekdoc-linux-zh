
Debian is available for nine different architectures including 32/64-bit PC, ARM64, ARMv7, 64-bit little-endian MIPS, 64-bit little-endian PowerPC, and IBM Z. You can read the full release notes for Debian 12 here and download an ISO from the official Debian download page ([https://www.debian.org/download](https://www.debian.org/download)).

## Armbian 23.05 Now Available

Armbian is almost at its 10-year anniversary and has announced the release of version 23.05. This release is based on Debian and created specifically for ARM and RISC-V architecture. Version 23.05, nicknamed "Suni," is based on a completely refactored build framework that has been in the works for the past three years.

According to the project website, “...many ARM-focused Linux distributions are essentially Armbian under a different name! We are committed to streamlining complexity and offering an exceptional solution for the community.”

The latest version of Armbian offers several improvements which include Armbian bookworm-based images for the latest updates from Debian, i3 support, improvements to the armbian-installer, an optimized package base, consistent application packages, improved Ubuntu-based assembles, fast and safe updates, the inclusion of the armbian-gaming script, and plenty of bug fixes and security patches.

Users without ARM or RISC-V hardware can download a Ubuntu-based image for AMD/Intel machines. This version has much of the Ubuntu-nestness removed (such as the removal of Ubuntu Pro and Snap).

Read the detailed changelog to see what is new to Armbian 23.05 and download an ISO image for installation on the single-board computer of your choice. On the download page, you'll also find links for AMD64 images.

## Linux Mint Finally Receiving Support for Gestures

Getting multitouch gestures for touchscreen and touchpads on Linux has been problematic over the years. Although some distributions have offered it, the support has been fairly weak (at best).

Hopefully, that all changes with the release of Linux Mint 21.2 (and Cinnamon 5.8). When using the default Cinnamon desktop, users will finally get to enjoy gestures that will support media player controls, tiling, and other helpful features.

According to Clement “Clem” Lefebvre ([https://blog.linuxmint.com/?p=4518](https://blog.linuxmint.com/?p=4518)), these gestures will be supported for touchpads, touchscreens, and tablets.

Linux Mint 21.2 (based on Ubuntu 22.04) will also enjoy a few more updates and tweaks, such as Xfce v4.18, global dark mode (thanks to an implementation of xdg-desktop-portal), and the Software Manager was given a UI refresh as well as better scoring/sorting algorithms for applications and a special list for tuned packages, an improved login (that includes support for multiple keyboard layouts and better touchpad support), auto-detection and enabling of tap-to-click, support for Wayland sessions, support for HEIF and AVIF images, an improved Pix image viewing app, better support for Flatpak apps, and improved support for Gnome’s libadwaita library.

Linux Mint 21.2 (Victoria) is slated for release in June 2023. For those wanting to test Linux Mint 21.2, you’ll have to use the Daily Builds ([linuxmint-developer-guide.readthedocs.io/en/latest/daily_builds_ppa.html](http://linuxmint-developer-guide.readthedocs.io/en/latest/daily_builds_ppa.html)) PPA and upgrade from the stable to the unstable version, or you can wait until they release the beta version, which will probably happen a couple weeks before the final release. Make sure to check the official ISO Images page ([https://community.linuxmint.com/iso](https://community.linuxmint.com/iso)) daily.

## An All-Snap Version of Ubuntu is in the Works

It should come as no surprise, given how Canonical is pushing Snap packages for its flagship OS, Ubuntu, that they’d take things to the next level by offering a version of Ubuntu that is comprised completely of Snap packages.

Before anyone gets up in arms, the all-Snap version of Ubuntu will not be the default. When you go to download Ubuntu next year (when the all-Snap version will be available), it will default to the traditional Debian version of the OS.

So, what’s the appeal of the all-Snap version of Ubuntu? It’ll be immutable, which means it was designed so the operating system is mounted read-only, so it can’t be changed. Once the OS has been installed, system files and directories cannot be changed. This isn’t new to Ubuntu, as Ubuntu Core (another immutable version) has been around since 2015. The idea behind immutable operating systems is to make them more secure.

This announcement was subtly dropped in the comments of the CUPS Snap announcement posted on omgubuntu.com ([https://www.omgubuntu.co.uk/2023/05/cups-snap-ubuntu-23-10#comment-6196766355](https://www.omgubuntu.co.uk/2023/05/cups-snap-ubuntu-23-10#comment-6196766355)). Canonical’s Oliver Grawert said, “There will be a desktop release of it with the next LTS (optional though, the classic desktop install will indeed not go away).”

The next LTS version of Ubuntu is 24.04, which will be released in April 2024, so you can bet there will be a slow trickle of information about this new all-Snap version of the Ubuntu Desktop distribution.

## Mageia 9 Beta 2 Ready for Testing

Mageia was forked from Mandriva Linux back in 2011 and, since then, has become something all of its own. This latest release comes three months after the first beta and the team has put in a good amount of time fixing stubborn issues, adding security fixes, and application updates.

Beta 2 features Linux kernel 6.3.3, Glib 2.36, RPM 4.18.0, Chromium 110, Firefox ESR 102.11, LibreOffice 7.5.2, KDE Plasma 5.27.4, Gnome 44, Xfce 4.18.1, LXQt 1.3.0, and Mesa 23.1.0.

Users will find three different repositories included with Mageia: Core (includes free and open-source software), Non-free (contains software that is free to use and distribute but includes proprietary software), and Tainted (contains packages released under a free license, but which infringe on patents and copyright laws in some countries). Mageia does configure 32-bit repositories, but they are disabled on 64-bit systems.

When you download a version of Mageia, make sure to select your desktop environment of choice: KDE Plasma ([https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Plasma-x86_64.iso](https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Plasma-x86_64.iso)), Gnome ([https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-GNOME-x86_64.iso](https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-GNOME-x86_64.iso)), Xfce (32-bit ([https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Xfce-ls86.iso](https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Xfce-ls86.iso)), or 64-bit ([https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Xfce-x86_64.iso](https://www.mageia.org/en/downloads/get/?q=Mageia-9-beta2-Live-Xfce-x86_64.iso)).

To find out more about the new release, check out the official Mageia blog ([https://blog.mageia.org/en/2023/05/24/the-release-of-beta2-brings-mageia-9-stable-closer-to-reality/](https://blog.mageia.org/en/2023/05/24/the-release-of-beta2-brings-mageia-9-stable-closer-to-reality/)). At this time, there is no official release date for Mageia 9, but keep checking the official blog ([https://blog.mageia.org/en/](https://blog.mageia.org/en/)) for more information.

![](img/740bd926461af28ed755753238e647a2_9_0.png)

Get the latest news in your inbox every week

Subscribe FREE to Linux Update bit.ly/Linux-Update

## KDE Plasma 6 Looks to Bring Basic HDR Support

When KDE Plasma 6.0 finally lands, users will find that High Dynamic Range (HDR) support has finally arrived. Because 4K screens are becoming the norm, HDR support has become a necessity.

With HDR, video content can be pushed well beyond the limits of the now out-dated standards media outlets have held onto for decades. Support for HDR in KDE Plasma 6.0 came by way of an HDR hackfest that was organized by Red Hat in May 2023 as well as the Plasma Sprint.

KDE Plasma 6.0 will only offer HDR support for Wayland sessions, which, according to KDE developer Nate Graham ([https://pointiestick.com/2023/05/20/this-week-in-kde-preliminary-hdr-support/](https://pointiestick.com/2023/05/20/this-week-in-kde-preliminary-hdr-support/)), “lays the groundwork for color management on Wayland.”

## MORE ONLINE

- Linux Magazine
  - www.linux-magazine.com
- ADMIN HPC
  - http://www.admin-magazine.com/HPC/
- Saving Storage Space
  - Jeff Layton
  - People often turn to data compression to save storage space, but reducing precision can be a useful technique.
- ADMIN Online
  - http://www.admin-magazine.com/
- Package management tools for Windows
  - Eugeni Strimon
  - Chocolatey and WinGet offer end-full-fledged package management on Windows, but which is best for your environment?
- CrowdSec Crowd security service
  - Thomas Joss
  - Threats can be detected and averted at an early stage with crowd security, in which organizations form a community to take concentrated action against cyberattacks by sharing attack data. We explain how this strategy works with the CrowdSec cloud service.
- Verifying your configuration
  - Ankur Kumar
  - Automated acceptance testing is a powerful tool for catching problems related to misconfiguration. We’ll show you how to implement your own acceptance testing environment with a free tool called goss.
