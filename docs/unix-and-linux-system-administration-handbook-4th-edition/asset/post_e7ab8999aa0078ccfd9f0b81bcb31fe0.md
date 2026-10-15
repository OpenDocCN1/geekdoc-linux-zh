
**Table 1.5  Sysadmin resources on the web**

| Web site | Description |
|---|---|
| blogs.sun.com | Great collection of technical articles, many Solaris-related |
| cpan.org | Authoritative collection of Perl modules |
| freshmeat.net | Large index of Linux and UNIX software |
| kernel.org | Official Linux kernel site |
| linux.com | Linux forum, good for new usersᵃ |
| linux.org | General Linux information clearing house |
| linux.slashdot.org | Linux-specific arm of tech news giant Slashdot |
| linuxhq.com | Compilation of kernel-related info and patches |
| lwn.net | Linux and open source news service |
| lxer.com | Linux news aggregator |
| rootvg.net | AIX-oriented site with lots of links and good forums |
| securityfocus.com | General computer security info |
| serverfault.com | Collaboratively edited database of sysadmin questions |
| ServerFiles.com | Directory of network admin software and hardware |
| slashdot.org | Tech news in a variety of categories |
| solariscentral.org | Open blog with Solaris-related news and articles |
| sun.com/bigadmin | Sun-specific aggregation site for admin info |
| sunhelp.org | Very nice collection of Sun-related material |
| ugu.com | UNIX Guru Universe — all things sysadmin |

ᵃ This site is now run by the Linux Foundation.

## 1.12  WAYS TO FIND AND INSTALL SOFTWARE

Chapter 12, *Software Installation and Management*, addresses software provisioning in detail. But for the impatient, here's a quick primer on how to find out what's installed on your system and how to obtain and install new software.

Modern operating systems divide their contents into packages that can be installed independently of one another. The default installation includes a range of starter packages that you can expand according to your needs.

Add-on software is often provided in the form of precompiled packages as well, although the degree to which this is a mainstream approach varies widely among systems. Most software is developed by independent groups that release the software in the form of source code. Package repositories then pick up the source code, compile it appropriately for the conventions in use on the systems they serve, and package the resulting binaries. It's usually easier to install a system-specific binary package than to fetch and compile the original source code. However, packages are sometimes a release or two behind the current version.

The fact that two systems use the same package format doesn’t necessarily mean that packages for the two systems are interchangeable. Red Hat and SUSE both use RPM, for example, but their filesystems and software are somewhat different. It’s best to use packages designed for your particular system if they are available.

Major Linux distributions provide excellent package management systems that include tools for accessing and searching Internet software repositories. Distributors aggressively maintain these repositories on behalf of the community, so there is rarely a need for Linux administrators to step outside the bounds of their systems’ default package manager. Life is good.

UNIX systems show more ambivalence about package management. Solaris, HP-UX, and AIX all provide packaging software that works at the level of individual machines. However, the vendors of these systems don’t maintain repositories of open source software, so the user communities are mostly left to fend for themselves.9 Unfortunately, one of the main pieces of glue that holds a packaging universe together is a way for packages to reliably refer to other packages in order to express dependency or compatibility information. Without some central coordination, the whole ecosystem can quickly fall apart.

In the real world, results have varied. Solaris has an add-on system (pkgutil from blastwave.org) that provides for easy software installation from an Internet repository, much like the native systems found on Linux distributions. HP-UX has a nice Internet repository in the form of the HP-UX Porting and Archiving Centre at hpux.connect.org.uk, but packages must be manually and individually downloaded. At the more dismal end of the spectrum, the availability of prepackaged software for AIX is somewhat scattershot.

Administrators without access to prepackaged binaries must install software the old-fashioned way: by downloading a tar archive of the source code and manually configuring, compiling, and installing it. Depending on the software and the operating system, this process can range from trivial to nightmarish.

In this book, we generally assume that optional software is already installed rather than torturing you with boilerplate instructions for installing every package. If there’s a potential for confusion, we sometimes mention the exact names of the packages needed to complete a particular project. For the most part, however, we don’t repeat installation instructions since they tend to be similar from one package to the next.

### Determining whether software has already been installed

For a variety of reasons, it can be a bit tricky to determine which software package contains the component you actually need. Rather than starting at the package level, it’s easier to use the shell’s which command to find out if a relevant binary is already in your search path. For example, the following command reveals that the GNU C compiler has already been installed on this machine:

```
aix$ which gcc
/opt/pware/bin/gcc
```

9. OpenSolaris does offer a Linux-quality package management system and Internet repository. This feature does not exist in Solaris 10, but it’s likely to be featured in Solaris 11.
