# NEWS

Also, it’s important to note that even though the official release date for Gnome 44 is on March 22, that does not mean your Gnome-based distribution of choice will have the latest update available. The first distribution that will likely get Gnome 44 will be the nightly release of Gnome OS (https://os.gnome.org/). One thing to keep in mind with Gnome OS is that it only runs on bare metal or FlatHub Boxes, so you cannot test the distribution as a virtual machine.
You can follow the news for Gnome 44 on the official Gnome Wiki (https://wiki.gnome.org/).

# Nitrux 2.6 Is Available with Kernel 6.1 and a Major Change

Nitrux 2.6 is available and there are some serious changes to the distribution. First and foremost, dpkg, apt, and PackageKit package managers have been removed in favor of AppImage or Flatpack.

In the release, FlatHub has been enabled by default, and there are plenty of applications that can be installed with that system.

Users of the Live version of Nitrux will notice that the standard package managers are still available, but once the operating system has been installed, those package managers are no longer enabled.

Other changes include PipeWire as the default sound server, and Wayland has been added but not enabled by default. The default desktop environment is KDE Plasma, and Nitrux 2.6 ships with version 5.26.4, KDE Frameworks 5.1.01, and KDE Gear 22.12.

Of version 2.6, Uri Herrera (https://www.linkedin.com/in/uri-herrera/), founder of Nitrux, said “This version of this distribution can be seen as the antithesis of the conventional Linux distribution, where a distribution is entirely devoted to its package manager, but this distribution is not.” Herrera continues to say, “Users can use a container of any Linux distribution (Arch, Fedora, Debian, openSUSE, NixOS, Gentoo, and many more), including multiple containers simultaneously; there’s no limitation whatsoever.”

Read more about Nitrux 2.6 in the official release announcement (https://nxos.org/changelog/release-announcement-nitrux-2-6-0/) and download your copy now (https://sourceforge.net/projects/nitruxos/files/Release/ISO/nitrux-ux-desktop-d5c7odiff-amd64.iso/download).

# Vanilla OS Inital Release Is Now Available

A brand-new Linux distribution is now available with a unique feature you won’t find in many operating systems. This distribution is called Vanilla OS and offers a stock Gnome experience (using Gnome 43), and is based on Ubuntu 22.10.

The key features of Vanilla OS include its own installer (written in GTK4 and libadwaita), a handy first-setup application to guide users through the first steps, an OS Control Center to help you install drivers and run things such as critical updates, and on-demand immutability.

It’s the on-demand immutability that should excite many users. With this feature, core bits of the system are locked to prevent unwanted changes. This is achieved using ABRoot, which works in conjunction with the apt replacement, apx. Apx installs packages inside a managed container without modifying the root file system.

You’ll also find VSO (Vanilla System Operator), which is a tool that periodically checks for an update and then downloads and installs it in the background, but only if the system isn’t under heavy load.

![](bbox=[0.42, 0.83, 0.6, 0.87])

You can read more about Vanilla OS on the official Kinetic announcement page (https://vanillaos.org/2022/12/29/vanilla-os-22-10-kinetic.html) and then download an ISO for installation from the distribution GitHub page (https://github.com/Vanilla-OS/os/releases/tag/22.10-r2).

# MORE ONLINE

**Linux Magazine**
www.linux-magazine.com

**ADMIN HPC**
http://www.admin-magazine.com/HPC/
**Warewulf 4 – Time and Resource Management**
• Jeff Layton
Warewulf installed with a compute node is not really an HPC cluster. You need to ensure precise timekeeping and add a resource manager.

**ADMIN Online**
http://www.admin-magazine.com/
**Statistics and Machine Learning with Weka**
• Manuj Bhardwaj
The open source Weka tool applies a wide variety of analysis methods to data without the need for advanced programming skills and without having to change environments.

**Goodbye Cloud VMs, Hello Laptops VMs**
• Ankur Kumar
Multipass lets you launch and run Ubuntu virtual machines, use cloud-init to configure the VMs, and protottype cloud launches locally in minutes.

**Rancher Manages Lean Kubernetes Workloads**
• Martin Lorschwit
The Rancher lightweight alternative to Red Hat’s OpenShift gives admins a helping hand when entering the world of Kubernetes, but with major differences in architecture.