# Review SparkyLinux 3.0

# New features: Debian 7.0 · Linux kernel 3.9.8 · GNOME 3.8 compatible

![](bbox=[0.06, 0.23, 0.63, 0.59])

+   - Customised desktop environments such as LXDE, Openbox and MATE are available

![](bbox=[0.8, 0.18, 0.96, 0.47])

+   - The preset Conky display gives a lot of information about your system, all of it relevant

+   - The SparkyCenter is a nice little app for controlling your system, although it could do with better navigation

# DISTRO

# SparkyLinux 3.0

**Minimum Specs:** CPU 1GHz 1486 RAM 256MB (128MB for CLI Edition) STORAGE 5GB (2GB for CLI Edition) **Best for:** Home Office

# One of the first distros using Debian 7.0 'Jessie', SparkyLinux is positioning itself as a lightweight system for any user

+   **Pros** Lightweight distro based on new testing branch of Debian; nice aesthetic; great selection of images
+   
+   **Cons** Doesn't play nice with all desktops, some issues with Flash and JS on non-Chrome based browsers

SparkyLinux is a relatively new distro, with its first version only coming out in May of last year. Since then, it's gone through a few minor upgrades and number changes and is now on its third iteration. The idea is to create a lightweight distro that computers both old and new can use – with modern aesthetics and graphical features available for those with high system specs. In case you don't need graphics at all, though, there is a handy CLI image that reduces the space down further – another first for a Debian 7.0-based distro.

Graphical images come in several flavours: the standard lightweight LXDE image, a purely Openbox-based image, a MATE image and a Razor-Qt running edition. These are all customised to fit the needs of Sparky, with a dock added in most cases, along with a nice custom theme. All of the live images include both a graphical and a command-line installer – as used in the CLI version. Both work exactly the same way with the exact same options; however, the command-line version uses cfdisk for partitioning, and the graphical installer used GParted. It's a minor difference that can actually cause a unique issue – SparkyLinux can't detect partitions on a hard drive that uses GPT. This means that systems with UEFI may need to be wiped before installing. As GParted can work with GPT, you may never know that this is an issue, as no warning messages or errors are thrown up.
This also means that partitioning for SparkyLinux is completely manual. It does explain what it needs to run, and