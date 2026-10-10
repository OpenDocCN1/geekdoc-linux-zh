comes with this book (and it was mounted on `/media/disk/`), you could type the following to install the gftp package:

```
```
# yum localinstall /media/disk/Fedora/Packages/gftp-*
yum localinstall /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
.
.
.
Resolving Dependencies
---> Running transaction check
---> Package gftp.i386 1:2.0.18-7.fc8 set to be updated
Dependencies Resolved
================================================================================
Package    Arch     Version                  Repository        Size
================================================================================
Installing:
gftp       i386     1:2.0.18-7.fc8           /media/disk/Fedora/Packages/gftp-2.0.18-7.fc8.rpm
  946 k

Transaction Summary
================================================================================
Install    1 Package(s)
Update     0 Package(s)
Remove     0 Package(s)

Total download size: 946 k
Is this ok [y/N]: y
```
```

A good reason for using `yum localinstall` instead of the `rpm` command to install RPM packages is that `yum` will check whether the package you are installing is dependent on any other packages being installed. If `yum` finds that it needs other packages, it will search any `yum` repositories you have configured (at least the main Fedora repository) to download and install what you need.

In this example, you found that gftp didn't require any additional packages be installed. So, typing `y` at the prompt caused only the one package to be installed.

# ## Using yum for listing packages

Besides downloading and installing new RPM packages, yum can also be used to list available packages as well as those that are already installed. The following examples illustrate some uses of yum.

If you want to see a list of all packages that are available for download from the repositories you have configured, type the following:

```
```
# yum list | less
```
```

Adding the `less` command to the end lets you scroll through the list of software (it could be long, depending on which repositories you point to). If you try to install a package and it fails