# # CHAPTER 2 Installing Linux in a Server Configuration

The other, more typical method of installation is the use of optical media provided by the vendor. All the commercial distributions of Linux have boxed sets of their brand of Linux that contain the install media. They usually use CD/DVD-ROM ISOs (of the OS available on their FTP and/or HTTP sites). The distros (distributions) that don't make their ISOs available will usually have a stripped-down version of the OS available in a repository on their tree.

Another variant of installing Linux that has become popular is installing via a live environment. This environment can be a live USB or a live CD/DVD. This method provides several advantages: It allows the user to try (the) drive before actually installing anything onto it. It also allows the user to have a idea of how hardware and peripherals behave on the target system. Live drives are usually a stripped-down version of the full distribution and, as much, this is, with a little tweak here and there, you can get troublesome hardware working after the fact—your mileage will save you.

We will be performing a server class install in this using an operating system that was downloaded from the distribution website.

A side note regarding automated installations is that server-type installs have special considerations when it comes to automation, because each server usually has a unique task; each server will have a slightly different configuration. For example, a server dedicated to handling large partitions set up for the appropriate logging directories, is going to have especially de-optimized, compared to a file server that performs no logging of its own. (The obvious exception is for server farms with large numbers of replicated servers. But even those installations have nuances that require attention to detail specific to the installation.)

# # Installing Fedora

In this section, we will install a 64-bit version of a Fedora 23 distribution on a standalone-system. We will take a liberal approach to the process, installing some tools and subsystems relevant to serve operations. Later chapters build on the groundwork done in this chapter by exploring these subsystems as well as adding new subsystems.

> NOTE Don't worry if you choose a different version or architecture of Fedora—the installation steps involved between versions are similar. You'll also be fine if you choose to install a Linux distro other than Fedora: luckily, most of the concepts carry over among the various distributions. Some installers are just prettier than others.

# # Project Prerequisites

First, you need to download the ISO for Fedora that we will be installing. Fedora’s project web page has a listing of several mirrors located all over the world. You should,