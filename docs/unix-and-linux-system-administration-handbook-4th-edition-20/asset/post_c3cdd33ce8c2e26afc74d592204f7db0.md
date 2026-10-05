
# Managing packages

# Table 12.4 NIM command-line tools

| Tool | What it does |
| --- | --- |
| nim_master_setup | Installs and configures a NIM master server |
| nim_update_all | Updates installation resources and clients |
| nim_clients_setup | Defines new clients and initiates OS installation |
| nim_master_recover | Restores the NIM database to a new server |
| nim | Multiple: configures resources, defines clients, etc. |
| nimclient | Pulls resources (e.g., updates) from a server (run on clients) |

# 12.5 MANAGING PACKAGES

UNIX and Linux variants use some form of packaging system to facilitate the job of software management. Packages have traditionally been used to distribute software, but they can be used to wrap configuration files and administrative data as well. They have several advantages over the traditional unstructured .tar.gz archives. Perhaps most importantly, they try to make the installation process atomic as possible. If an error occurs, the package can be backed out or reapplied.

Package installers are typically aware of configuration files and will not overwrite local customizations performed by a system administrator. They will either back up the existing config files they change or provide example files under a different name (e.g., .pkg.conf.rpmew). If you find a newly installed package breaks something on your system, you can, least in theory, back out to restore your system to its original state. Of course, theory = practice, don't try this on a production system without testing it.

Packaging systems define a dependency model that allows package maintainers to ensure that the libraries and support infrastructure on which their applications depend are properly installed. Some packaging systems do a more complete job of dependency management than others.

Packages can also run scripts at various points during the installation, so they can do much more than just deploy files.

Packages are also a nice way to distribute your own localizations. You can create a package that, when installed, reads localization information about a machine (or gets it from central database) and uses that information to set up local configuration files. You can also bundle your local applications as packages, complete widely distributed in package format. You can customize your packages and dependencies for third-party applications that aren't normally distributed in package format. Use the dependency mechanism to upgrade machines automatically when a new version of your localization package is installed.

You can also use the dependency mechanism to create groups of packages. For example, it's possible to create a package that installs nothing of its own but depends on other patches. Installing the package with dependencies turned on results in all the patches being installed in a single step.

![](img/579efec8c67772f31ecf34844bbb71a2_429_0.png)

# 12.6 MANAGING LINUX PACKAGES

Two package formats are in common use on Linux systems. Red Hat, SUSE, and several other distributions use RPM, the Red Hat Package Manager. Ubuntu uses the separate but equally popular deb format (named after the Debian distribution on which Ubuntu was originally based). The two formats are functionally similar.

It’s easy to convert between the two package formats with a tool such as alien from kitenen.net/programs/alien. alien knows nothing about the software inside a package, so if the contents are not already compatible with your distribution, alien will not help. In general, it is best to stick with the native package mechanism used by your distribution.

On top of these commands are systems that know how to find packages on the Internet, analyze interchange dependencies, and upgrade all packages on a system. yum, the Yellowdog Updater, Modified, works with the RPM system. The Red Hat Network is specific to Red Hat Enterprise Linux and uses RPM. The Advanced Package Tool (APT) originated in the deb universe but works well with both .deb and RPM packages.

On the next couple of pages, we review the low-level commands rpm and dpkg. In the section Using high-level Linux package management systems starting on page 384, we discuss the comprehensive update systems (e.g., APT and yum) that build on these low-level facilities.

# rpm: manage RPM packages

The rpm command installs, verifies, and queries the status of packages. It formerly built them well, but this function has been broken out into a separate command rebuild. rpm options have complex interactions and can be used together only in certain combinations. It is most useful to use rpm if it were several different commands that happen to share the same name.

The mode you tell rpm to enter (such as -i or -q) specifies which of rpm’s personalities are hoping to access. rpm --help lists all the options down by most, but it’s your time to read the main page in detail if will be dealing with RPM packages.

The bread-and-butter options are -i (install), -U (upgrade), -e (erase), and -q (query). The q option is a bit tricky in that it serves only to enable other options: you must supply an additional command-line flag to pose a question. For example, the command -qa lists all the packages installed on the system. Let’s look at an example. Suppose you need to install a new version of OpenSSH because of a recent fix. Once you've downloaded the package, you could run rpm -U to replace the older version with the newer.

# dpkg: manage.deb packages in Ubuntu

```
redhat$ sudo rpm -U openssh-2
error: failed dependencies:
openssh = 2.9-7 is needed by openssh-askpass-7
openssh = 2.9-7 is needed by openssh-gnome-7
openssh = 2.9-7 is needed by openssh-clients-7
openssh = 2.9-7 is needed by openssh-server-7
```

Doh! It's not so simple after all. Here we see that the currently installed version of OpenSSH, 2.9-2, is required by a number of other packages. rpm won't upgrade OpenSSH because the change might affect the order of these packages. This type of conflict happens all the time, and it's motivation for the development of systems like APT and yum. In real life we wouldn't attempt to untangle the dependencies by hand, but let's continue with rpm alone for the purpose of this example. We could force the upgrade with the --force option, but would have a bad idea. The dependency information is there to save you time and trouble, not just to get in your way. There's nothing like a broken SSH on remote system to ruin it.

Instead, we will grab updated versions of dependent packages. If we were smart, could have determined that other packages depended on OpenSSH before we attempted the upgrade:

```
redhat$ rpm -q --requires openssh
openssh-askpass-7
openssh-gnome-7
openssh-clients-7
openssh-server-7
```

Suppose that we've obtained updated copies of all the packages. We could install them one at a time, but rpm is smart enough to handle them at once. If you list multiple RPMs on the command line, rpm sorts them by dependency before installation.

```
redhat$ sudo rpm -U openssh*
```

Cool! Looks like it succeeded, so:

```
redhat$ rpm -q openssh
openssh-2.9-7
```

Note that rpm understands which package we are talking about even though we didn't specify the package's full name or version.

# dpkg: manage.deb packages in Ubuntu

Just as RPM packages have the all-in-one rpm command, Debian packages have the dpkg command. Useful options include --install, --remove, and -l to list the packages that have been installed on the system. A dpkg --install of a package thats already on the system removes the previous version before installing.

# Chapter 12 Software Installation and Management

Running dpkg -l | grep package is a convenient way to determine if a particular package is installed. For example, to search for an HTTP server, try:

```
ubuntu$ dpkg -l | grep -i http
ii lighttpd 1.4.13-9ubuntu4
```

A fast webserver with minimal memory footprint

This search found the lighttpd software, an excellent open source, lightweight web server. The leading ii indicates that the software is installed.

Suppose that the Ubuntu team recently released a fix to nvi to patch a potential security problem. After grabbing the patch, we run dpkg to install it. As you can see, it is much chatter than rpm and tells us exactly what its doing:

```
ubuntu$ dpkg --install /nvi_1.79-16a_1.i386.deb
(Reading database ... 24368 files and directories currently installed)
Preparing to replace nvi 1.79-14 (using /nvi_1.79-16a_1.i386.deb)
Unpacking replacement nvi ...
Setting up nvi (1.79-16a.1) ...
```

Checking available versions of ex, updating links in /etc/alternatives ...
You may modify the symlinks yourself if desired - see 'man ln'.
Leaving ex (/usr/bin/ex) pointing to /usr/bin/nvi.
Leaving ex.1.gz (/usr/share/man/man1/ex.1.gz) pointing to /usr/share/man/man1/nvi.1.gz.

We can now dpkg -l to verify that the installation worked. The -l flag allows an optional pattern to match, so we can just search for nvi:

```
ubuntu$ dpkg -l nvi
Desired=Unknown/Install/Config-files/Unpacked/Failed-config/Half-installed
| Err=(none)/Hold/Reinst-required=X-both-problems (Status,Err: uppercase=bad)
| Name            Version Description
++ ---------------------------------------
ii nvi             1.79-16a.1       4.4BSD re-implementation of vi.
```

Our installation seems to have gone smoothly.

# 12.7 USING HIGH-LEVEL LINUX PACKAGE MANAGEMENT SYSTEMS

Metapackage management systems such as APT, yum, and the Red Hat Network share several goals:

+   - To simplify the task of locating and downloading packages
-   To automate the process of updating or upgrading systems
-   To facilitate the management of interpackage dependencies

Clearly, there is more to these systems than just client-side commands. They all require that distribution maintainers organize their offerings in an agreed-upon way that the software can be accessed and reasoned about by clients.
