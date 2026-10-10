
## TABLE 7.3 Common yum Commands (continued)

| Command | Description |
| :---- | :---- |
| `info` | Displays information about a package, similar to the `rpm -qi` command. |
| `clean` | Cleans up the Yum cache directory. Running this command from time to time is advisable, lest downloaded packages chew up too much disk space. |
| `shell` | Enters the Yum shell mode, in which you can enter multiple Yum commands one after another. |
| `resolvedep` | Displays packages matching the specified dependency. |
| `localinstall` | Installs the specified local RPM files, using your Yum repositories to resolve dependencies. |
| `localupdate` | Updates the system using the specified local RPM files, using your Yum repositories to resolve dependencies. Packages other than those updated by local files and their dependencies are *not* updated. |
| `deplist` | Displays dependencies of the specified package. |

In most cases, using Yum is easier than using RPM directly to manage packages, because Yum finds the latest available package, downloads it, and installs any required dependencies. Yum has its limits, though; it’s only as good as its repositories, so it can’t install software that’s not stored in those repositories.

> **WARNING**
> If you use Yum to automatically upgrade all packages on your system, you’re effectively giving control of your system to the distribution maintainer. Although Red Hat or other distribution maintainers are unlikely to try to break into your computer in this way, an automatic update with minimal supervision on your part could easily break something on your system, particularly if you’ve obtained packages from unusual sources in the past.

If you don’t want to install the package but merely want to obtain it, you can use `yumdownloader`. Type this command followed by the name of a package, and the latest version of the package will be downloaded to the current directory. This can be handy if you need to update a system that’s not connected to the Internet; you can use another system that runs the same distribution to obtain the packages and then transfer them to the target system.

If you prefer to use GUI tools rather than command-line tools, you should be aware that GUI front-ends to yum exist. Examples include Yum Extender (**yumex**) and kyum. You can use the text-mode yum to install these front-ends, as in **yum install yumex**. Figure 7.1 shows Yum Extender in action. To use it, click the **Updates**, **Available**, **Installed**, or **All** button to show the relevant types of packages. You can enter a search term in the line below these options (Figure 7.1 shows **samba** in this field) to restrict the package selection. You can then check or uncheck the tick boxes next to specific package names to mark them for installation or removal. When you’ve made your selections, click **Process Queue** to implement the changes.

### FIGURE 7.1 The Yum Extender (yumex) program provides a GUI front-end to Yum.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_345_0.png)

Yum is configured via the /etc/yum.conf file, with additional configuration files in the /etc/yum.repos.d/ directory. The yum.conf file holds basic options, such as the directory to which Yum downloads RPMs and where Yum logs its activities. Chances are you won’t need to modify this file. The /etc/yum.repos.d/ directory, on the other hand, potentially holds several files, each of which describes a Yum repository—that is, a site that holds RPMs that may be installed via Yum. You probably shouldn’t directly edit these files; instead, if you want to add a repository, manually download the RPM that includes the repository configuration and install it using rpm. The next time you use Yum, it will access your new repository along with the old ones. Several Yum repositories exist, mostly for Red Hat and Fedora, such as the following:

-   **Livna** This repository (http://rpm.livna.org/r1owiki/) hosts multimedia tools, such as additional codecs and video drivers.
-   **KDE Red Hat** Red Hat and Fedora favor the GNU Network Object Model Environment (GNOME) desktop environment, although they ship with the K Desktop Environment (KDE). The repository at http://kde-redhat.sourceforge.net provides improved KDE RPMs for those who favor KDE.
-   **Fresh RPMs** This repository (http://freshrpms.net) provides additional RPMs, mostly focusing on multimedia applications and drivers.

Many additional repositories exist. Try a Web search on terms such as *yum repository*, or check any Web site that hosts unusual software you want to run to see whether it provides a Yum repository. If so, it should provide an RPM or other instructions on adding its site to your Yum repository list.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_346_0.png)

The RPMfind Web site, http://rpmfind.net, is an extremely useful resource when you want to find an RPM of a specific program, but it's not accessible as a Yum repository. RPMFind includes links to RPMs built by programs' authors, specific distributions' RPMs, and those built by third parties.

## Handling Debian Packages

In their overall features, Debian packages are similar to RPMs, but the details of operation for each differ, and Debian packages are used on different distributions than are RPMs. Because each system uses its own database format, RPMs and Debian packages aren't interchangeable without converting formats.

### Debian Package Conventions

As the name implies, Debian packages originated with the Debian distribution. Since that time, the format has been adopted by several other distributions, including Ubuntu and Xandros. Such distributions are derived from the original Debian, which means that packages from the original Debian are likely to work well on other Debian-based systems. Although Debian doesn't emphasize flashy GUI installation or configuration tools, its derivatives add GUI configuration tools to the base Debian system, which makes these distributions more appealing to Linux novices. The original Debian favors a system that's as bug-free as possible, and it tries to adhere strictly to open source software principles rather than invest effort in GUI configuration tools.

Like RPM, the Debian package format is neutral with respect to both OS and CPU type. Debian packages are extremely rare outside Linux, though.

The original Debian distribution has been ported to many different CPUS, including x86, x86-64, IA-64, PowerPC, Alpha, 680x0, MIPS, and SPARC. The original architecture was x86, and subsequent ports exist at varying levels of maturity. Derivative distributions generally work only on x86 and x86-64 systems, but this could change in the future.

Debian packages follow a naming convention similar to those for RPMs, but Debian packages sometimes omit codes in the filename to specify a package's architecture, particularly on x86 packages. When these codes are present, they may differ from RPM conventions. For instance, a filename ending in 1386.deb indicates an x86 binary, amd64.deb is an x86-64 binary, and a11.deb indicates a CPU-independent package, such as documentation or scripts. As with RPM files, this file-naming convention is only that—a convention. You can rename a file as you see fit. There is no code for Debian source packages because Debian source packages actually consist of several separate files.

![](img/9903a4d3f7abd8dcbef1035fa04a3406_347_0.png)

> To install an x86 Debian package on an x86-64 (aka AMD64) system, you must use the --force-architecture option to dpkg. This contrasts with RPM-based distributions, which usually permit such installation by default.

## Using dpkg Commands

Debian packages are incompatible with RPM packages, but the basic principles of operation are the same across both package types. Like RPMs, Debian packages include dependency information, and the Debian package utilities maintain a database of installed packages, files, and so on. You use the **dpkg** command to install a Debian package. This command's syntax is similar to that of **rpm**:

```
dpkg [options] [action] [package-files|package-name]
```

*action* is the action to be taken; Table 7.4 summarizes common actions. The options (Table 7.5) modify the behavior of the action, much like the options to **rpm**.

### TABLE 7.4 dpkg Primary Actions

| Action | Description |
| :--- | :--- |
| -i or --install | Installs a package |
| --configure | Reconfigures an installed package—runs the post-installation script to set site-specific options |
| -r or --remove | Removes a package but leaves configuration files intact |
| -P or --purge | Removes a package, including configuration files |
| -p or --print-avail | Displays information about an installed package |
