# # Upgrading Packages

RPM upgrade mode provides an easy way to upgrade existing software packages to
newer versions. upgrade mode is similar to install mode:

```
rpm -U [options] [packages]
```

options can be any of the install options or any of the general options.

One example of how to upgrade packages is if a system is currently running emacs version
19.31, there is a need upgrade to the newer emacs version 19.34. To upgrade, root willnuse the following command:

```
# rpm -Uvh emacs-19.34-4.1386.rpm
```

The upgrade mode is a combination of two operations, uninstall and install. First, rpm
uninstalls all older versions of the requested package, and then it installs the newer
version. If an older version of the package does not exist, rpm simply installs the requested
package.

An additional advantage of using upgrade over manually installing and uninstalling is that
upgrade automatically saves configuration files. For these reasons, some people prefer to
use upgrade rather than install for all package installations.

# # Uninstalling Packages

The rpm command:uninstall mode provides a clean method of removing files
belonging to a software package from many locations. Some software packages have files
scattered over the filesystem, such as in /etc, /usr, and /lib. Manually removing a
package's files can be confusing, but with rpm, an entire package can be removed as
follow:

```
rpm -e [options] [package]
```

options is one of the options listed in this section, and package is the name of the
package to be removed. For example, to remove the package for DOSEMU, use the following
command:

```
# rpm -e dosemu
```

The name specified here for the package is just the name of the package, not the name of
file that was used to install the package. If the following command had been entered:

```
# rpm -e dosemu.rpm
```

The following error would have been generated:

package dosemu.rpm is not installed