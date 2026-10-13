
The exactarch boolean directive makes sure the architecture matches the actual processor type, as defined by the arch command.

```
exactarch=1
```

The obsoletes boolean directive can support the uninstallation of obsolete packages in conjunction with a yum update command.

```
obsoletes=1
```

The gpgcheck boolean directive makes sure the yum command actually checks the GPG signature of downloaded packages.

```
gpgcheck=1
```

The plugins boolean directive provides a necessary link to Python-based RHN plugins in the /usr/share/yum-plugins directory. It also refers indirectly to plugin configuration files in the /etc/yum/pluginconf.d directory.

```
plugins=1
```

The installonly_limit directive provides a safeguard of sorts, making sure that Linux kernel packages are always installed, and not upgraded, for reasons described earlier in this chapter:

```
installonly_limit=3
```

To make sure the header data downloaded from the RHN (and any other repositories) are up to date, the metadata_expire directive specifies a lifetime for headers. The default is shown in comments. In other words, if you haven't used the yum command in 90 minutes, the next use of the yum command downloads the latest header information.

```
#metadata_expire=90m
```

The final directive of interest, in comments, happens to be the default; it's a reference to the noted directory for actual configuration information for repositories:

```
# PUT YOUR REPOS HERE OR IN separate files named file.repo
# in /etc/yum.repos.d
```

## Configuration Files in the /etc/yum/pluginconf.d Directory

The default files in the /etc/yum/pluginconf.d directory configure a connection between yum and the Red Hat network. If you’re studying from a RHEL rebuild distribution such as Scientific Linux, you’ll see a different set of files in this directory. In Scientific Linux, the files in this directory are focused on connecting the local system to better repositories over the Internet. But as this is a Red Hat book, the focus will be on the two basic files in the RHEL 6 installation. If you’ve installed the Kickstart Configurator discussed in Chapter 2, there will be two additional files in this directory: blacklist.conf and whiteout.conf. They are not relevant to the Red Hat exams.

## Red Hat Network Plugins with rhnplugin.conf

If you have a subscription to the RHN, the rhnplugin.conf file in this directory is especially important. While the directives, as follows, may seem simple, they enable access and check GPG signatures:

```
[main]
enabled = 1
gpgcheck = 1
```

In comments, this file suggests that different settings can be configured for different repositories. The repositories entitled in brackets should match those associated with the actual RHN repositories (or the repositories of third-party rebuilds).

## Red Hat Network Plugins with refresh-packagekit.conf

The refresh-packagekit.conf file is designed to connect the yum system to the PackageKit. As discussed later in this chapter, PackageKit is a system designed to work with all types of update commands, including yum, apt, and others. It’s a simple file, with two directives, which enables a connection between yum and the GUI package management tools discussed later in this chapter.

```
[main]
enabled=1
```

## Configuration Files in the /etc/yum.repos.d Directory

The configuration files in the /etc/yum.repos.d directory are designed to connect systems to actual repositories. If you're running a rebuild distribution such as Scientific Linux, you'll see files that connect to public repositories on the Internet. If you're running RHEL 6, this directory may be empty, unless that system was installed locally from the RHEL 6 DVD. In that case, you'll see a packagekit-media.repo file in that directory, which is designed to get further updates from the DVD.

A couple of elements in common for configuration files in the /etc/yum.repos.d directory is the file extension (.repo) and the documentation, available with the man yum.conf command.

> exam watch
>
> - While not required, you should know how to create a working .repo file in the /etc/yum.repos.d directory during the RHCSA and RHCE exams. It can be a big time saver when you need to install additional packages.

A properly configured .repo file in the /etc/yum.repos.d directory can be a terrific convenience, to enable the installation of groups of packages with the yum command. As the /etc/yum.repos.d directory may be empty on a RHEL 6 system, you should know how to create that file from scratch, using data for the installation server and information available in the yum.conf man page.

## Deal with the packagekit-media.repo File

However, as the latest updates are available, it is often best to disable that file. In fact, you may not even have the RHEL 6 installation DVD available during an exam. While you could just delete that file, other software components regenerate that file when RHEL 6 is rebooted. So the best approach to the packagekit-media.repo file is to disable it by adding the following directive to the end of the file:

```
enabled=0
```

If you've experienced with various versions of Fedora Linux, this solution hasn't always worked. However, it works in current tests of RHEL 6 systems installed from DVD (as opposed to the RHCSA objective of installing RHEL 6 over a network).

## Understand /etc/yum.repos.d Configuration Files for Rebuild Distributions

If you're running a rebuild distribution, the files in the /etc/yum.repos.d directory may connect the local system to one or more remote repositories. One example
comes from Scientific Linux 6, as shown in Figure 7-7. While it includes a number of different repositories, you can learn from the pattern of directives configured for each repository.

There are four stanzas of data shown in Figure 7-7. Each stanza represents a connection to a Scientific Linux repository. For example, the first stanza includes the basic elements of a repository and more. The first line, in brackets, provides a name for the repository. In this case, the [sl] just happens to match the initials of Scientific Linux. It doesn't represent the directory where the associated packages are installed. That's a difference with the /etc/yum/pluginconf.d/rhnplugin.conf file described earlier.

[s1]

## FIGURE 7-7

Several repositories configured in one file

```
[sl]
name=Scientific Linux $releasever - $basearch
baseurl=http://ftp.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp1.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp2.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp.scientificlinux.org/linux/scientific/mirrorlist/$releasever/$basearch/os/
#mirrorlist=http://ftp.scientificlinux.org/linux/scientific/mirrorlist/sl-base-6.txt
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-testing]
name=Scientific Linux $releasever Testing - $basearch
baseurl=http://ftp.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp1.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp2.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp.scientificlinux.org/linux/scientific/rolling/testing/$basearch/

enabled=0
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-source]
name=Scientific Linux $releasever Alpha - Source
baseurl=http://ftp.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp1.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp2.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp.scientificlinux.org/linux/scientific/$releasever/SRPMS/

enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-testing-source]
name=Scientific Linux $releasever Testing - Source
baseurl=http://ftp.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp1.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp2.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/

enabled=0
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson
```
