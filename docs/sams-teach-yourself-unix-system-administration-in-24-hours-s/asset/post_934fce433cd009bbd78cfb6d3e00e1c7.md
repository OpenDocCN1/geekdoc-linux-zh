
In this hour you will learn about

- Working with RPM on Linux
- Adding RPM packages from the Internet
- Working with fink on Darwin
- Working with pkg on Solaris

## Red Hat Package Manager and Linux

The Red Hat Package Manager (RPM) system is one of the most sophisticated available in the Unix marketplace, and is the result of years of development by contract programmers (and eventually employees) of Red Hat Linux Corporation. Indeed, some sysadmins stick with Red Hat because RPM is so easy to work with.

The concept behind RPM is the same as with all package managers: They encapsulate all the files and configuration details needed to install and enable the specified package, including tracking version numbers of libraries, installing relevant documentation, and even checking automatically to ensure that the installation won’t step on files needed by a different package.

The interface to RPM is a bit baffling, however, so let’s jump right in and see how it works.

> If you are using a GUI, the good news is that there’s an RPM front end for both of the popular window managers in Linux—GnoRPM for GNOME, and Kpackage for KDE.

### Task 8.1: Working with RPM

There are basic tasks that you’ll want to know how to do in your package manager: query what packages are installed, install (or update) a specific package, list what files are included with a given package, and delete a package from the system.

1. The most basic RPM command is to query all packages. This is done with -qa, and you’ll probably have 400-600 packages installed on your system. When we first installed Red Hat Linux (see Hour 1, "Installing Unix"), recall that we opted for the "workstation" configuration, and that it took forever because it was installing package after package. RPM is how you can go back and query exactly what it did.

```
$ rpm -qa | head
redhat-logos-1.1.3-1
glibc-2.2.4-13
cracklib-2.7-12
dosfstools-2.7-1
gdbm-1.8.0-10
ksymoops-2.4.1-1
mktemp-1.5-11
perl-5.6.0-17
setserial-2.17-4
netconfig-0.8.11-7
$ rpm -aq | wc -l
638
```

There are more than 600 packages installed, so typing rpm -qa without feeding it to a pager or something similar would result in a phenomenal wave of information!

Each package is identified by its name, version number, and the package version number. For example, the Perl package is identified as perl-5.6.0-17, which means that it's the perl package for version 5.6.0 of Perl, and that this is the 17th version of the RPM package for this particular distribution of Perl.

![](img/5ced0c78d748bd190e9027e5549a3622_179_0.png)

> Why is this the seventeenth version of this package? Because when packages are large, include lots of files, and have lots of dependencies, it can often take package developers quite a few tries to get things just right for all platforms and possible configurations. Nothing to worry about!

2. To learn more about a specific package, use rpm -qi, either by specifying the full package name, or just the base name instead:

```
$ rpm -qi setserial
Name : setserial              Relocations: /usr
Version : 2.17                Vendor: Red Hat, Inc.
Release : 4                   Build Date: Sun 24 Jun 2001
Install date: Wed 21 Nov 2001 02:34:04 PM PST   Build Host: elliot.
Group : Applications/System   Source RPM: setserial-2.17-4.
Size : 31113                  License: GPL
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary : A utility for configuring serial ports.
Description :
Setserial is a basic system utility for displaying or setting serial
port information. Setserial can reveal and allow you to alter the I/O
port and IRQ that a particular serial device is using, and more.
```

3. One of the features I really like about other package systems that isn't a part of RPM is the capability to provide a summary listing of packages and their descriptions.

And yet, if you look at the output, there's a Summary line. So a little bit of judicious shell script coding produces showrpms:

```sh
$ cat showrpms.sh
#!/bin/sh

# SHOWRPMS - List all the RPM packages on the system in a friendly manner
count=0

for package in `rpm -qa`
do
  summary=`rpm -qi $package | grep '^Summary' | cut -d: -f2-`
  echo "$package: $summary"
  count=`expr $count + 1`
done

echo ""
echo "Listed $count RPM packages"
exit 0
```

In a nutshell, this loops through all packages reported by rpm -qa, querying each for its information, then extracts the summary line and outputs the package name and summary on the same line:

```sh
$ showrpms.sh | head
redhat-logos-1.1.3-1: Red Hat-related icons and pictures.
glibc-2.2.4-13: The GNU libc libraries.
cracklib-2.7-12: A password-checking library.
dosfstools-2.7-1: Utilities for making and checking MS-DOS FAT filesystems on Linux.
gdbm-1.8.0-10: A GNU set of database routines which use extensible hashing.
ksymoops-2.4.1-1: Kernel oops and error message decoder
mktemp-1.5-11: A small utility for safely making /tmp files.
perl-5.6.0-17: The Perl programming language.
setserial-2.17-4: A utility for configuring serial ports.
netconfig-0.8.11-7: A text-based tool for simple configuration of ethernet devices.
```

An attractive and much more sysadmin-friendly output!

![](img/5ced0c78d748bd190e9027e5549a3622_180_0.png)

> There is actually a way to convince RPM to output information in this format, if you really dig into it. There's a command option --queryformat that lets you specify exactly what information you want presented, and in what form. If you use
> 
> ```bash
> rpm -qa --queryformat '%{NAME}: %{SUMMARY}\n'
> ```
> your output will be the same as the showrpms script.

4. Now we can more effectively search to see, for example, what command line shells are installed:

```
$ showrpms.sh | grep -i shell
sharutils-4.2.1-8: The GNU shar utilities for packaging and unpackaging shell archives.
mc-4.5.51-80: A user-friendly file manager and visual shell.
docbook-utils-0.6.9-2: Shell scripts for managing DocBook documents.
bash-2.05-8: The GNU Bourne Again shell (bash) version 2.05.
ash-0.3.7-2: A smaller version of the Bourne shell (sh).
tcsh-6.10-6: An enhanced version of csh, the C shell.
sh-utils-2.0.11-5: A set of GNU utilities commonly used in shell scripts.
```

The RPM package is a powerful way to manage packages on your system, but where it really gets exciting is when you can grab different packages from the Internet and extend the capabilities of your system with ease!

## Adding New RPM Packages from the Internet

There’s no capability within the rpm command to reach out to a Net archive and search for available packages, so you’ll need to pop into your graphical Web browser (perhaps Konqueror, a popular Linux browser) and poke around a bit.

### Task 8.2: Installing New Web-Based RPM Packages

To install new packages on your system, you need to explore the Web and identify the specific package desired.

> A great place to start your RPM package search is the Pbone Web site at http://rpm.pbone.net/. You can also make sure you have the latest version of RPM by checking http://www.rpm.org/.

1. Because the network isn’t always available, I like to have copies of relevant documentation on my own system for backup purposes. I popped over to Pbone and learned that the great Linux FAQ set is available as an RPM package called faq-7.2.1.noarch.rpm. On the site, it also lists the full URL of the specific package at a variety of servers around the world.

I’ll pick a link from the University of Oklahoma and feed it to the RPM package with the -i to install, -v for more verbose output, and -h to show a sequence of hash marks as the file downloads:

```bash
# rpm -ivh ftp://ftp.ou.edu/mirrors/linux/redhat/redhat-7.2-en/doc/RedHat/RPMS/faq-7.2.1.noarch.rpm
Retrieving ftp://ftp.ou.edu/mirrors/linux/redhat/redhat-7.2-en/doc/RedHat/RPMS/faq-7.2.1.noarch.rpm
Preparing...
######################################## [100%]
1:faq ######################################## [100%]
```

2. Looks like it installed just fine. Let's double-check with the -qi flag:

```bash
# rpm -qi faq
Name        : faq                     Relocations: (not relocatable)
Version     : 7.2                     Vendor: Red Hat, Inc.
Release     : 1                       Build Date: Thu 30 Aug 2001
Install Date: Sat 26 Jan 2002 11:31:11 AM PST   Build Host: strippies.devel.redhat.com
Group       : Documentation           Source RPM: faq-7.2.1.src.rpm
Size        : 1596478                 License: distributable
Packager    : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary     : Frequently Asked Questions (FAQ) about Linux.
Description :
The faq package includes the text of the Frequently Asked
Questions (FAQ) about Linux from
http://metalab.unc.edu/pub/Linux/docs/faqs/. These FAQs are a great source
of information (sometimes historical) about Linux.
```

Install the faq package if you'd like to read the Linux FAQ off your own machine.

There's another useful flag to RPM that will show you the exact names of all the files installed with a package—the -l flag:

```bash
# rpm -ql faq | wc -l
121
```

You can see that more than 120 files were installed with this simple rpm install. To have a peek, let's use head:

```bash
# rpm -ql faq | head -20
/etc/X11/applnk/Documentation
/etc/X11/applnk/Documentation/Linux Community
/etc/X11/applnk/Documentation/Linux Community/faq.desktop
/usr/share/doc/FAQ
/usr/share/doc/FAQ/html
/usr/share/doc/FAQ/html/AfterStep-FAQ
/usr/share/doc/FAQ/html/AfterStep-FAQ/AfterStep-FAQ-1.html
```
