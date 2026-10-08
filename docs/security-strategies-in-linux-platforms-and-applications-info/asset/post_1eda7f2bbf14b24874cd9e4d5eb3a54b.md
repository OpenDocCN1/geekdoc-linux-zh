
# 340 PART | Building a Layered Linux Security Strategy

```bash
// Automatic upgrade packages from these (origin, archive) pairs
Unattended-Upgrade::Allowed-Origins {
  // "Ubuntu hardy-security"
  // "Ubuntu hardy-updates"
};
```

```bash
// List of packages to not update
Unattended-Upgrade::Package-Blacklist {
  // "vim"
  // "libc6"
  // "libc6-dev"
  // "libc6-1686"
};
```

```bash
// Send email this address for problems or packages upgrades
// If empty or unset then no email is sent, make sure that you
// have a working mail setup on your system. The package 'mailx'
// must be installed or anything that provides /usr/bin/mail.
Unattended-Upgrade::Mail "root@localhost";
```

```
/etc/apt/conf.d/50unattended-upgrades [readonly] 19 lines, 595 characters
```

FIGURE 11 Ubuntu@unattended-upgrades configuration file.

The final directive, if the comment characters are removed, would send an e-mail to the root administrator on the local system when an unattended upgrade is run.
If an appropriate e-mail service is available, you could change that e-mail address to an actual e-mail address.

# Automatic Red Hat Updates

Automatic upgrades on Red Hat Enterprise Linux systems can be configured courtesy of the yum-updates.conf configuration file in the /etc/yum/ directory. By default, automatic upgrades are disabled with the following directives:

```ini
do_update = no
do_download = no
do_download_deps = no
```

To enable automatic updates, you'd change these directives to yes to perform updates and download updated packages.
Automatic upgrades on other Red Hat systems are possible with the help of the yum-cron package. While that package was created for Fedora systems, it is also available through the Extra Packages for Enterprise Linux (EPEL) project. Available packages for that project can be downloaded from https://fedaproject.org/wiki/EPEL. Packages associated with EPEL 5 are designed for Red Hat Enterprise Linux 5 as well as rebuild distributions such as CentOS 5.

# CHAPTER 11 | Managing Security Alerts and Updates

Once the yum-cron package is installed, it includes a daily cron job, yum.cron, in the /etc/cron.daily/ directory. That job uses parameters configured in the /etc/sysconfig/yum-cron file to determine whether to check for updates, downloadable packages, or proceed with installation-based parameters in the /etc/yum/yum-daily.yum. That file is fairly simple, based on a yum command shell.

You can start a yum on a system with the yum shell command. The directives shown in the yum-daily.yum file are run in that shell:

```bash
update
run
exit
```

The first directive, update, collects a list of updatable packages. Those packages are collected in a transaction set, ts for short. The ts directive takes that list of updatable packages, downloads, and installs them on the local system before exiting the yum command shell via the exit directive.

> TIP
> If you are running Red Hat Enterprise Linux and want some feature from the Fedora project, take a look at the EPEL project at https://fedoraproject.org/wiki/EPEL. Packages based on Fedora have been developed as part of the EPEL project for use on Red Hat Linux systems.

# Pushing or Pulling

Updates can be pushed or pulled. In other words, with help of administrative tools like the Red Hat Network, ZENworks, Landscape, or Spacewalk, administrators can push the installation of updates on remote systems. While that may not be costly on a network with one or two systems, it is a time saver when administering a few dozen systems. Properly configured, administrative-update tools can push the updates to dozens of systems simultaneously.

Of course, simultaneous updates only work if they've been tested and applied on systems with identical hardware and software configurations.

Some update tools also support remote administration. With the right centralized administrative tool, you may not even have to configure a remote login service as the Secure Shell (SSH).

# Local or Remote Repositories

To go step further, you could limit the number of packages available in local repositories. One way to do so is to limit those repositories available to local systems. On Ubuntu systems, you could configure clients and servers to avoid connections to the unsupported universe and multiverse repositories. On Red Hat systems, you could limit the channels. For example, RHEL 5 system may be subscribed to additional channels named Network Tools, Virtualization, Supplementary, and Optional Productivity Apps. On the Red Hat Network, you may disable subscriptions from a system to all of these channels.

On all systems, you can avoid connections to third-party repositories. While many third-party repositories are reputable, they are designed to include popular software not specifically supported by the developers of distributions as Red Hat and Ubuntu.

# 342 PART 3 | Building a Layered Linux Security Strategy

FYI

Third-party repositories designed for Ubuntu and even Red Hat Enterprise Linux are frequently located in countries where copyright laws hold less sway. For example, some third-party repositories include video players that may bypass legal requirements such as the Digital Millennium Copyright Act (DMCA).

While such packages are popular among Linux users, the presence of such packages that you administer may expose your organization to legal liability.

# Configure a Local Repository

It's easy to use the remote repositories already configured for most Linux distributions. The connections to such repositories have already been tested. If a problem arises with such systems, many administrators are likely to complain, and the problem is likely to be fixed.

However, there are advantages to maintaining a local repository. At minimum, a local repository reduces the load on the Internet. You can then point clients and servers to that local repository in their /etc/apt/sources.list.

To minimize that delay, you could set up a local mirror using a server such as Apache or vsFTP. Once a mirror is available, you'll still need to share the directory. You can use rsync to synchronize the data:

```bash
rsync -avz archive.ubuntu.com/
```

The switches for rsync are -a (archive mode), -v (verbose output), and -z (compression). This synchronizes the files in the /updates/.
