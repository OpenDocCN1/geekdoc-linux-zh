# DEBIAN GNU/LINUX 2.1

```
dpkg --install package_file
```

This installs the specified package. If an older version is already installed, it is replaced with the new version. The following example shows the installation of the graphics xv, which is included as a non-free package on the contrib CD.

```
# dpkg --install /cdrom/debian/non-free/binary-i386/graphics/xv_3.10a-20.deb
```

Selecting previously deselected xv.
(Reading database 45374 files and directories currently installed)
Unpacking xv (from .../graphics/xv_3.10a-20.deb )
Setting up xv (3.10a-20)...

```
Update-menus: waiting for dpkg to finish (forking for background)
Update-menus: checking /var/lib/dpkg/lock
```

```
dpkg --configure package_name
```

This reconfigures an installed package. Please note that you not need to specify the full file name (with the extension *.deb), but only the package name without path and extension.

```
dpkg --remove package_name
dpkg --purge package_name
```

These two commands remove the specified packages. In the second variation, the configuration files are deleted as well.

```
dpkg --list
dpkg --list 'pattern'
```

In the first syntax variation, dpkg displays all effectively installed packages. The second variation also considers all non-installed packages that had been registered as available during the last select in the menu item UPDATE.

```
dpkg --listfiles package_name
```

This command shows all files of a package. The command works only with installed packages. The contents of non-installed packages can be displayed by means of dpkg-deb --contents file_name.

```
dpkg --search file_name
```

In this syntax variation, dpkg searches for the package which contains the specified file. For example, dpkg --search /etc/aliases yields the package name sendmail (provided that sendmail is installed and the file /etc/aliases exists).