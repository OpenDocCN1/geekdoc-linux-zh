
but not least, we will discuss the cryptographic protocols and utilities in place that will let you validate each package's authenticity.

## 8.3.1. Configuring APT

Before we dive into the configuration of APT, let's take a moment to discuss the configuration mechanism of the Debian system. Historically, configuration was handled by dedicated configuration files. However, in modern Linux systems like Debian and Kali, configuration directories with the `.d` suffix are becoming more commonly used. Each directory represents a configuration file that is split into multiple files. In this sense, all of the files in `/etc/apt/apt.conf.d/` are instructions for the configuration of APT. APT processes the files in alphabetical order, so that the later files can modify configuration elements defined in the earlier files.

This structure brings some flexibility to administrators and package maintainers, allowing them to make software configuration changes through file additions without having to change an existing file. This is especially helpful for package maintainers because they can use this approach to adapt the configuration of other software to ensure that it perfectly co-exists with theirs, without breaking the Debian policy that explicitly forbids modifying configuration files of other packages. Because of the `.d` configuration mechanism, you don't have to manually follow multiple package configuration instructions typically found in the package's `/usr/share/doc/package/README-Debian` file, since the installer can drop in configuration files.

> While APT has native support of its `/etc/apt/apt.conf.d/` directory, this is not always the case. For some applications (like exim, for example), the `.d` directory is a Debian-specific addition used as input to dynamically generate the canonical configuration file used by the application. In those cases, the packages provide an "update-" command (for example: `update-exim4.conf`) that will concatenate the files from the `.d` directory and overwrite the main configuration file.
>
> In those cases, you must not manually edit the main configuration file or your changes will be lost on the next execution of the update- command, and you must also not forget to run the former command after having edited a file out of the `.d` directory (or your changes will not be used).

Armed with an understanding of the `.d` configuration mechanism, let's talk about how you can leverage it to configure APT. As we have discussed, you can alter APT's behavior through command-line arguments to dpkg like this example, which performs a forced overwrite install of zsh:

```bash
# apt -o Dpkg::Options::="--force-overwrite" install zsh
```

Obviously this is very cumbersome, especially if you use options frequently, but you can also use the `.d` directory configuration structure to configure certain aspects of APT by adding directives to a file in the `/etc/apt/apt.conf.d/` directory. For example, this (and any other) directive can easily be added to a file in /etc/apt/apt.conf.d/. The name of this file is somewhat arbitrary, but a common convention is to use either local or 99local:

```bash
$ cat /etc/apt/apt.conf.d/99local
Dpkg::Options {
	"--force-overwrite";
}
```

There are many other helpful configuration options and we certainly can’t cover them all, but one we will touch on involves network connectivity. For example, if you can only access the web through a proxy, add a line like `Acquire::http::proxy "http://yourproxy:3128"`. For an FTP proxy, use `Acquire::ftp::proxy "ftp://yourproxy"`.

To discover more configuration options, read the apt.conf(5) manual page with the man apt.conf command (for details on manual pages, see section 6.1.1, “Manual Pages” [page 124]).

## 8.3.2. Managing Package Priorities

One of the most important aspects in the configuration of APT is the management of the priorities associated with each package source. For instance, you might want to extend your Kali Rolling system with one or two newer packages from Debian Unstable or Debian Experimental. It is possible to assign a priority to each available package (the same package can have several priorities depending on its version or the distribution providing it). These priorities will influence APT’s behavior: for each package, it will always select the version with the highest priority (except if this version is older than the installed one and its priority is less than 1000).

APT defines several default priorities. Each installed package version has a priority of 100. A non-installed version has a priority of 500 by default but it can jump to 990 if it is part of the target release (defined with the -t command-line option or the APT::Default-Release configuration directive).

You can modify the priorities by adding entries in the /etc/apt/preferences file with the names of the affected packages, their version, their origin and their new priority.

APT will never install an older version of a package (that is, a package whose version number is lower than the one of the currently installed package) except when its priority is higher than 1000. APT will always install the highest priority package that follows this constraint. If two packages have the same priority, APT installs the newest one (whose version number is the highest). If two packages of same version have the same priority but differ in their content, APT installs the version that is not installed (this rule has been created to cover the case of a package update without the increment of the revision number, which is usually required).

In more concrete terms, a package whose priority is less than 0 will never be installed. A package with a priority ranging between 0 and 100 will only be installed if no other version of the package is already installed. With a priority between 100 and 500, the package will only be installed if there is no other newer version installed or available in another distribution. A package of priority between 501 and 990 will only be installed if there is no newer version installed or available in the target distribution. With a priority between 990 and 1000, the package will be installed except if the installed version is newer. A priority greater than 1000 will always lead to the installation of the package even if it forces APT to downgrade to an older version.

When APT checks /etc/apt/preferences, it first takes into account the most specific entries (often those specifying the concerned package), then the more generic ones (including for example all the packages of a distribution). If several generic entries exist, the first match is used. The available selection criteria include the package’s name and the source providing it. Every package source is identified by the information contained in a Release file that APT downloads together with the Packages files. These files specify the origin, usually “Kali” for the packages from Kali’s official mirrors and “Debian” for the packages from Debian’s official mirrors, but the origin can also be a person’s or an organization’s name for third-party repositories. The Release file also provides the name of the distribution together with its version. Let’s have a look at its syntax through some realistic case studies of this mechanism.

### Priority of Kali-Bleeding-Edge and Debian Experimental

If you listed kali-bleeding-edge or Debian experimental in your sources List file, the corresponding packages will almost never be installed because their default APT priority is 1. This is of course a specific case, designed to keep users from installing bleeding edge packages by mistake. The packages can only be installed by typing `apt install *package/kali-bleeding-edge*`, assuming of course that you are aware of the risks and potential headaches of life on the edge. It is still possible (though *not recommended*) to treat packages of kali-bleeding-edge/experimental like those of other distributions by giving them a priority of 500. This is done with a specific entry in /etc/apt/preferences:

```
Package: *
Pin: release a=kali-bleeding-edge
Pin-Priority: 500
```

Let’s suppose that you only want to use packages from Kali and that you only want Debian packages installed when explicitly requested. You could write the following entries in the /etc/apt/preferences file (or in any file in /etc/apt/preferences.d/):

```
Package: *
Pin: release o=Kali
Pin-Priority: 900

Package: *
Pin: release o=Debian
Pin-Priority: -10
```
