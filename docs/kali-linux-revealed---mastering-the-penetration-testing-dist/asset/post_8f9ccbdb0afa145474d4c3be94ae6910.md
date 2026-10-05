
as firewalls and packet filtering. Finally, we reviewed monitoring tools and strategies and showed how to implement them to detect potential threats to your system.

Summary Tips:

- Take time to define a comprehensive security policy.
- If you are running Kali on a publicly accessible server, change any default passwords for services that may be configured (see section 7.3, [Securing Network Services](page 153)) and restrict their access with a firewall (see section 7.4, [Firewall or Packet Filtering](page 153)) prior to launching them.
- Use *fail2ban* to detect and block password-guessing attacks and remote brute force attacks.
- If you run web services, host them over HTTPS to prevent network intermediaries from sniffing your traffic (which might include authentication cookies).
- Real risk arises when you travel from one customer to the next. For example, your laptop could be stolen while traveling or seized by customs. Prepare for these unfortunate possibilities by using full disk encryption (see section 4.2.2, "Installation on a Fully Encrypted File System"[page 85]) and consider the n feature ("Adding a Nuke Password for Extra Safety"[page 246]) to protect your clients data.
- Implement firewall rules (see section 7.4, "Firewall or Packet Filtering"[page 153]) to forbid all outbound traffic except that your VPN access. This is meant as a safety net, so that when the VPN is down you immediately notice (instead of falling back to the local network access).
- Disable services that you do not use. Kali makes it easy to do this since all external services are disabled by default.
- The Linux kernel embeds the *netfilter* firewall. There is no turn-key for configuring any firewall, since network and user requirements differ. However, you can control *netfilter* from user space with the *iptables* and *iptables* commands.
- The logcheck program logs every file by default and sends unusual messages in emails to the administrator for further analysis.
- top is an interactive tool that displays list of currently running processes.
- *dpkg --verify* (or *dpkg -V*) displays the system files that have been modified (potentially by an attacker), but relies on checksums, which may be subverted by a clever attacker.
- The Advanced Intrusion Detection Environment (AIDE) tool checks integrity and detects any changes against a previously-recorded image of the valid system.
- Tripwire is very similar to AIDE but uses a mechanism to sign the configuration file, so that an attacker cannot make it point a different version of the reference database.
- Consider the use of rkhunter, checksecurity, and chkhrootkit to help detect rootkits on your system.

In the next chapter, we are going to dig into Debian fundamentals and package management. You will quickly understand the power behind Kali's Debian roots and learn how the developers have harnessed that power. Be warned, the next chapter is fairly dense, but it is critical that you understand Debian basics and package management if you are going to be a Kali power user.

![](img/4d5d0d3397277b3d6e29d1328d013586_192_0.png)

# Keywords

- dpkg
- apt
- sources.list
- Upgrades
- Package repositories

![](img/4d5d0d3397277b3d6e29d1328d013586_193_0.png)

# KALI LINUX
REVEALED

# Chapter 8
Debian Package Management

- Introduction to APT 170
- Basic Package Interaction 175
- Advanced APT Configuration and Usage 194
- Package Reference: Digging Deeper into the Debian Package System 204
- Summary 216

After the basics of Linux, it is time to learn the package management system of a Debian-based distribution. In such distributions, including Kali, the Debian package is the canonical way to make software available to end-users. Understanding the package management system will give you a deal of insight into how Kali is structured, enabling you to more effectively troubleshoot issues, and help you quickly locate help and documentation for the wide array of tools and utilities included in Kali Linux.

In this chapter, we will introduce the Debian package management system and introduce dpkg and the APT suite of tools. One of the primary strengths of Kali Linux lies in the flexibility of its package management system, which leverages these tools to provide near-seamless installation, upgrades, removal, and manipulation of application software, even when the base operating system itself. It is critical that you understand how this system works to get the most out of Kali and streamline your efforts. The days of painful compilations, disastrous upgrades, debugging gcc, and configure problems are long gone, the number of available applications has exploded and you need to understand the tools designed to take advantage of them. This is also a critical skill because there are a number of security tools that, due to licensing or other issues, cannot be included in Kali but have Debian packages available for download. It is important that you know how to process and install these packages and how they impact the system, especially when things do not go as expected.

We will begin with some basic overviews of APT, describe the structure and contents of binary source packages, take a look at some basic tools and scenarios, and then dig deeper to help you wring every ounce of utility from this spectacular package system and suite of tools.

# 8.1. Introduction to APT

Let's begin with some basic definitions, an overview, and some history about Debian packages, starting with dpkg and APT.

# 8.1.1. Relationship between APT and dpkg

A Debian package is a compressed archive of a software application. A binary .deb file contains files that can be directly used (such as programs or documentation), while a source package contains the source code for the software and the instructions required for building a binary package. A Debian package contains the application's files as well as other metadata including the names of the dependencies the application needs, as well as scripts that enable the execution of commands at different stages in the package's lifecycle (installation, removal, and upgrades).

The dpkg tool was designed to process and install .deb packages, but if it encountered an unsatisfied dependency (like a missing library) that would prevent the package from installing, dpkg would simply list the missing dependency, because it had no awareness or built-in logic to find or process the packages that might satisfy those dependencies. The Advanced Package Tool (APT), including apt and apt-get, were designed to address these shorthcomings and automatically resolve these issues. We will talk about both dpkg and the APT tools in this chapter.

The base command for handling Debian packages on the system is dpkg, which performs installation or analysis of .deb packages and their contents. However, dpkg has only a partial view of the Debian universe: it knows what is installed on the system and whatever you provide on the command line, but knows nothing of the other available packages. As such, it will fail if a dependency is not met. 

APT is a set of tools that help manage Debian packages, applications on your Debian system. You can use APT to install and remove packages, update packages, and upgrade your entire system. The magic of APT lies in the fact that it is a complete package management system that will not only install or remove a package, but will consider the requirements and dependencies of the packaged application (and even their requirements and dependencies) and attempt to satisfy them automatically. APT relies on dpkg but APT differs from dpkg, the former installs the latest package from an online source and works to resolve dependencies while dpkg installs a package located on your local system and does not automatically resolve dependencies.

If you have been around long enough to remember compiling programs with gcc when you likely remember that it was a painful process, especially if the application had several dependencies. By deciphering the various warnings and error messages, you may be able to determine which part of the code was failing and most often that failure was due to a missing library or dependency. You would then track down that missing library or dependency, correct it, and try again. If you were lucky, the compile would work, but often the build would fail again, complaining about another broken dependency.

APT was designed to alleviate that problem, collate program requirements and dependencies, and resolve them. This functionality works out-of-box on Kali Linux, but it isn't foolproof. It is important that you understand Debian and Kali's packaging system because you will need to install packages, update software, or troubleshoot problems with packages. You will use APT in your day-to-day work with Kali Linux in this chapter, we will introduce you to APT and show how to install, remove, upgrade, and manage packages, and even show how to move packages between different Linux distributions. We will also talk about graphical tools that leverage APT, how you validate the authenticity of packages, and delve into the concept of a rolling distribution, a technique that brings daily updates to your Kali system.

Before we dig in and show you how to use dpkg and APT to install and manage packages, it is important that we delve into some of the inner workings of APT and discuss some terminology surrounding it.

| Package Source and Source Package |
| :--- | :--- |
| The word source can be ambiguous. A source package—a containing the source code of a program—should not be confused with a source—a repository (website, FTP server, CD-ROM, local directory, etc.) that contains packages. |
