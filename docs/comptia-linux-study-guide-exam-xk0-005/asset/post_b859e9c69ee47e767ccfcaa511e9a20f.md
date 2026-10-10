
## Looking at Red Hat Enterprise Linux

The original Red Hat Linux started life in 1995 as an open source project. It gained in popularity to the point where it was at one time the most popular Linux distribution, used in educational environments, in corporate environments, and even by casual Linux hobbyists. However, in 2003 Red Hat discontinued the Red Hat Linux project in favor of the Red Hat Enterprise Linux (RHEL) project. The RHEL project is primarily focused on business Linux environments. RHEL is a commercial package; thus under most situations you must purchase a license to use it. In return, Red Hat provides full customer support to help with setting up and troubleshooting the Linux system, unlike most other Linux distributions.

Fortunately for Linux hobbyists, there is an alternative way to run RHEL. Since Linux is an open source software package, Red Hat is required to release the source code for RHEL. A few other Linux distributions have popped up using the RHEL source code. The most popular had been the Community Enterprise Operating System (CentOS). It was nearly an exact duplicate of RHEL, and a great free study resource for the CompTIA Linux+ certification exam.

However, as is often the case in the fast-moving Linux world, things have changed. In 2014 CentOS joined Red Hat’s Open Source and Standards team, and in 2020 Red Hat replaced the original CentOS project with a new development version called CentOS Stream. Although you can still freely obtain CentOS Stream, it’s no longer an exact duplicate of the current RHEL version, but rather a testing ground for new concepts, making it less beneficial as a study resource.

But have no fear, the original developers of CentOS have started yet another distribution, named Rocky Linux. Rocky Linux has gone back to the origins of CentOS—it’s an exact duplicate of the latest RHEL version. You can obtain a Rocky Linux distribution ISO from the Rocky website at www.rockylinux.org. Be aware that this distribution, like many others, comes in multiple flavors. We recommend you obtain the Rocky BaseOS download package, in the 8.x version series (at the time of this writing, at version 8.5).

![](img/c0a399aca0d18f8822d714ad0a173123_74_0.png)

> As time goes on, new Rocky distribution versions will be available. Although it is always tempting to get the latest and greatest version, it is not beneficial to use it in your learning space. Remember that the CompTIA Linux+ objectives are static until the next time the certification exam is updated. Therefore, it is wise to use the distribution versions that *were available at* the certification exam’s creation time.

As you install Rocky Linux, you’ll be prompted for the environment you want to install. For learning Linux, it’s usually best to install a graphical desktop environment, because that provides the easiest way to access all of the Linux features you’ll need to learn about.

After you install your Rocky Linux version 8.x BaseOS distribution, you should update the software packages. Do this by logging into the root account using the password you set up during installation and issuing the commands shown in Listing 1.1.

### Listing 1.1: Updating software on Rocky Linux

```bash
# sudo dnf update
Loaded plugins: fastestmirror
[...]
Upgrade  3 Packages

Total download size: 1.3 M
Is this ok [y/d/N]: y
[...]
Complete!
# 
```

While RHEL (and its derivatives) is a popular distro, you also need a distribution in the Debian camp. Next, we'll explore the Ubuntu distribution.

## Looking at Ubuntu

The Ubuntu Linux distribution is managed by Canonical LTD and has been around since 2004. This free and popular Linux distro is based on the Debian distribution and is a must-have in your personal Linux learning space.

You can obtain the Ubuntu distro ISO from www.ubuntu.com. There are several flavors of Ubuntu, and if you'd like to ensure that you can follow the examples in this book, we recommend you download the Ubuntu Desktop version 20.04 LTS.

![](img/c0a399aca0d18f8822d714ad0a173123_75_0.png)

> The LTS in the Ubuntu version name stands for Long-Term Support. This is an indicator Canonical uses to show that it will provide maintenance and security updates for an extended time period. In the case of 20.04 LTS, you can count on these updates through April 2025.

If you are unfamiliar with Ubuntu, you need to be aware of a few important items. By default, you cannot log into the root account. Instead, when you need to use super user privileges, log into the account you set up at installation and put the command `sudo` in front of your command-line commands. An example is shown in Listing 1.2.

### Listing 1.2: Using sudo on Ubuntu

```bash
$ sudo grep root /etc/shadow
root:::17737:0:99999:7:::
$
```

![](img/c0a399aca0d18f8822d714ad0a173123_75_1.png)

> If you have never issued command-line commands in a terminal, it is recommended you read this entire chapter prior to attempting to do so. You will read more about terminals later in this chapter.

Another important item concerns installing Ubuntu. If you are connected to a network, you can automatically update the distribution's software when you install the distribution. You will see this option listed in the installation process as **Download updates** during the installation with a check box next to it. If you choose to not install updates during the installation, you can update the software via the command line later on by manually issuing the commands shown in Listing 1.3 in a terminal, using super user privileges.

### Listing 1.3: Updating software on Ubuntu

```bash
$ sudo apt-get update
[sudo] password for Christine:
Hit:1 http://us.archive.ubuntu.com/ubuntu bionic InRelease
Get:2 http://us.archive.ubuntu.com/ubuntu bionic-updates InRelease
[88.7 kB]
[...]
Fetched 1,053 kB in 2s (631 kB/s)
Reading package lists... Done
$
$ sudo apt-get dist-upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
The following packages will be upgraded:
[...]
Do you want to continue? [Y/n] Y
[...]
$
```

If you have room for only two Linux distros, Rocky Linux and Ubuntu make fine choices. If you have additional resources, it would be worthwhile to add another distribution, openSUSE.

## Looking at openSUSE

The openSUSE distro had its first release in 1994, under a different name, SUSE Linux. There have been many companies involved in supporting it, with the Germany-based company SUSE being the original.

This distro has a very loyal and solid following. Not only is the openSUSE distribution strongly supported by community developers, the openSUSE users love it as well. One of its unique and popular utilities is the Yet another Setup Tool (YaST). YaST, which can be thought of as a command center utility, allows you to control many system services from one interface.

You can obtain the openSUSE distribution ISO from `https://software.opensuse.org`. This distro comes in two primary flavors, Leap and Tumbleweed. We recommend you select openSUSE Leap in the version 15.x series.

![](img/c0a399aca0d18f8822d714ad0a173123_77_0.png)

The openSUSE community changed its distribution’s version numbering scheme in 2017. The version before 15.0 was 42.3. Be aware of this dramatic change when you go to obtain openSUSE Leap.

Once you have successfully installed openSUSE, it is a good idea to update all the software prior to exploring this distro. To update the software via the command line, manually issue the commands shown in Listing 1.4 in a terminal, using super user privileges.

### Listing 1.4: Updating software on openSUSE

```bash
$ sudo zypper patch
[sudo] password for root:
Loading repository data...
Reading installed packages...
Resolving package dependencies...
[...]

Note: System reboot required.
Continue? [y/n/.../? shows all options] (y): y
[...]
Warning: One of the installed patches requires a
reboot of your machine. Reboot as soon as possible.
There are some running programs that might use files
deleted by recent upgrade. You may wish to check and
restart some of them. Run 'zypper ps -s' to list these programs.
$
```

You may have noticed that the last three distros use different commands for updating software. This is another reason you need to have access to multiple distributions in your learning space. We’ll look at one more important distro next.

## Looking at Fedora

Fedora is maintained by the Fedora Project, which is sponsored by Red Hat. Innovative and sometimes bleeding-edge software is one of this distribution’s great features. If you want to try something new, Fedora is for you. This distro, like the others, comes in multiple flavors, which are called *editions* by the Fedora Project. We recommend Fedora 34 Workstation edition. You can get a copy of this Fedora ISO at `https://getfedora.org`.
