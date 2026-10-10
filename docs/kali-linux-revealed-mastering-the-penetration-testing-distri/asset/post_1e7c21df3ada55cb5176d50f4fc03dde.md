
## Incompatibilities: the Breaks Field

The Breaks field has an effect similar to that of the Conflicts field, but with a special meaning. It signals that the installation of a package will break another package (or particular versions of it). In general, this incompatibility between two packages is transitory and the Breaks relationship specifically refers to the incompatible versions.

When a package breaks an already installed package, dpkg will refuse to install it, and apt will try to resolve the problem by updating the package that would be broken to a newer version (which is assumed to be fixed and, thus, compatible again).

This type of situation may occur in the case of updates without backwards compatibility: this is the case if the new version no longer functions with the older version and causes a malfunction in another program without making special provisions. The Breaks field helps prevent these types of problems.

## Provided Items: the Provides Field

This field introduces the very interesting concept of a virtual package. It has many roles, but two are of particular importance. The first role consists in using a virtual package to associate a generic service with it (the package provides the service). The second indicates that a package completely replaces another and that for this purpose, it can also satisfy the dependencies that the other would satisfy. It is thus possible to create a substitution package without having to use the same package name.

![](img/46e3313ea1bb2892f314630a4f0677b8_235_0.png)

### Providing a Service

Let’s discuss the first case in greater detail with an example: all mail servers, such as postfix or sendmail are said to provide the mail-transport-agent virtual package. Thus, any package that needs this service to be functional (e.g. a mailing list manager, such as smartlist or sympa) simply states it in its dependencies that it requires a mail-transport-agent instead of specifying a large yet incomplete list of possible solutions. Furthermore, it is useless to install two mail servers on the same machine, which is why each of these packages declares a conflict with the mail-transport-agent virtual package. A conflict between a package and itself is ignored by the system, but this technique will prohibit the installation of two mail servers side by side.

### Interchangeability with Another Package

The Provides field is also interesting when the content of a package is included in a larger package. For example, the libdigest-md5-perl Perl module was an optional module in Perl 5.6, and has been integrated as standard in Perl 5.8. As such, the package perl has since version 5.8 declared Provides: libdigest-md5-perl so that the dependencies on this package are met if the system has Perl 5.8 (or newer). The libdigest-md5-perl package itself was deleted, since it no longer had any purpose when old Perl versions were removed.

![](img/46e3313ea1bb2892f314630a4f0677b8_236_0.png)

This feature is very useful, since it is never possible to anticipate the vagaries of development and it is necessary to be able to adjust to renaming, and other automatic replacement, of obsolete software.

## Replacing Files: The Replaces Field

The Replaces field indicates that the package contains files that are also present in another package, but that the package is legitimately entitled to replace them. Without this specification, dpkg fails, stating that it cannot overwrite the files of another package (technically, it is possible to force it to do so with the --force-overwrite option, but that is not considered standard operation). This allows identification of potential problems and requires the maintainer to study the matter prior to choosing whether to add such a field.

The use of this field is justified when package names change or when a package is included in another. This also happens when the maintainer decides to distribute files differently among various binary packages produced from the same source package: a replaced file no longer belongs to the old package, but only to the new one.

If all of the files in an installed package have been replaced, the package is considered to be removed. Finally, this field also encourages dpkg to remove the replaced package where there is a conflict.

### 8.4.2. Configuration Scripts

In addition to the control file, the control.tar.gz archive for each Debian package may contain a number of scripts (postinst, postrm, preinst, prerm) called by dpkg at different stages in the processing of a package. We can use `dpkg -I` to show these files as they reside in a `.deb` package archive:

```
$ dpkg -I /var/cache/apt/archives/zsh_5.3-1_amd64.deb | head
new debian package, version 2.0.
size 814486 bytes: control archive=2557 bytes.
838 bytes, 20 lines control
3327 bytes, 43 lines md5sums
969 bytes, 41 lines * postinst #!/bin/sh
348 bytes, 20 lines * postrm #!/bin/sh
175 bytes, 5 lines * preinst #!/bin/sh
175 bytes, 5 lines * prerm #!/bin/sh
Package: zsh
Version: 5.3-1
$ dpkg -I zsh_5.3-1_amd64.deb preinst
#!/bin/sh
set -e
# Automatically added by dh_installdeb
dpkg-maintscript-helper symlink_to_dir /usr/share/doc/zsh zsh-common 5.0.7-3 -- "$@"
# End automatically added section
```

The Debian Policy describes each of these files in detail, specifying the scripts called and the arguments they receive. These sequences may be complicated, since if one of the scripts fails, dpkg will try to return to a satisfactory state by canceling the installation or removal in progress (insofar as it is possible).

## The dpkg Database

You can traverse the dpkg database on the filesystem at `/var/lib/dpkg/`. This directory contains a running record of all the packages that have been installed on the system. All of the configuration scripts for installed packages are stored in the `/var/lib/dpkg/info/` directory, in the form of a file prefixed with the package's name:

```
$ ls /var/lib/dpkg/info/zsh.*
/var/lib/dpkg/info/zsh.list
/var/lib/dpkg/info/zsh.md5sums
/var/lib/dpkg/info/zsh.postinst
/var/lib/dpkg/info/zsh.postrm
/var/lib/dpkg/info/zsh.preinst
/var/lib/dpkg/info/zsh.prerm
```

This directory also includes a file with the `.list` extension for each package, containing the list of files that belong to that package:

```
$ head /var/lib/dpkg/info/zsh.list
/.
/bin
/bin/zsh
/bin/zsh5
/usr
/usr/lib
/usr/lib/x86_64-linux-gnu
/usr/lib/x86_64-linux-gnu/zsh
/usr/lib/x86_64-linux-gnu/zsh/5.2
/usr/lib/x86_64-linux-gnu/zsh/5.2/zsh
[...]
```

The `/var/lib/dpkg/status` file contains a series of data blocks (in the format of the famous mail headers request for comment, RFC 2822) describing the status of each package. The information from the control file of the installed packages is also replicated there.

```
$ more /var/lib/dpkg/status
Package: gnome-characters
Status: install ok installed
Priority: optional
Section: gnome
Installed-Size: 1785
Maintainer: Debian GNOME Maintainers <pkg-gnome-maintainers@lists.alioth.debian.org>
Architecture: amd64
Version: 3.20.1-1
[...]
```

Let's discuss the configuration files and see how they interact. In general, the preinst script is executed prior to installation of the package, while the postinst follows it. Likewise, preinst is invoked before removal of a package and postrm afterwards. An update of a package is equivalent to removal of the previous version and installation of the new one. It is not possible to describe in detail all the possible scenarios here but we will discuss the most common two: an installation/update and a removal.

These sequences can be quite confusing, but a visual representation may help. Manoj Srivastava made these diagrams explaining how the configuration scripts are called by dpkg. Similar diagrams have also been developed by the Debian Women project; they are a bit simpler to understand, but less complete.

- https://people.debian.org/~srivasta/MaintainerScripts.html
- https://wiki.debian.org/MaintainerScripts

> **CAUTION**
> The sequences described in this section call *configuration scripts* by specific names, such as *old-preinst* or *new-postinst*. They are, respectively, the *preinst* script contained in the old version of the package (installed before the update) and the *postinst* script contained in the new version (installed by the update).

**Symbolic Names of the Scripts**

### Installation and Upgrade Script Sequence

Here is what happens during an installation (or an update):

- For an update, dpkg calls the *old-preinst upgrade new-version*.
- Still for an update, dpkg then executes *new-preinst upgrade old-version*; for a first installation, it executes *new-preinst install*. It may add the old version in the last parameter if the package has already been installed and removed (but not purged, the configuration files having been retained).
- The new package files are then unpacked. If a file already exists, it is replaced, but a backup copy is made and temporarily stored.
- For an update, dpkg executes *old-postrm upgrade new-version*.
- dpkg updates all of the internal data (file list, configuration scripts, etc.) and removes the backups of the replaced files. This is the point of no return: dpkg no longer has access to all of the elements necessary to return to the previous state.
- *dpkg* will update the configuration files, prompting you to decide if it is unable to automatically manage this task. The details of this procedure are discussed in section 8.4.3, “Checksums, Confiles” [page 214].
- Finally, dpkg configures the package by executing *new-postinst configure last-version-configured*.
