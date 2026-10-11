| Option | Purpose |
| --- | --- |
| overwrite | Overwrite a file from a new package, even if it belongs to another package. |
| depends-version | Normally an error is given if the correct version of a dependency is not installed. This option makes that a warning instead. |
| depends | Turn all dependency errors into warnings. |
| confnew | Always use the newly installed configuration file. |
| confold | Always use the old configuration file. |
| conflicts | Allow packages that conflict to be installed. |
| overwrite-dir | Overwrite another package's directory with a new one. |
| remove-essential | Remove essential system packages, dangerous. |

For example, if you had to install a package that conflicted with an existing package, you would use the following:

```
```
dpkg -install_new_package.deb --force-conflicts
```
```

# ## Removing packages

2.2 Installation and Package Management

+   * Use Debian package management. Be able to install, upgrade or uninstall packages.

To remove a package, use the following commands:

```
```
dpkg --remove package_name
```
```

or:

```
```
dpkg -r package_name
```
```

These commands remove all files of the package, except for configuration files that may be needed for a later reinstall. To remove all files including configuration files, use the following commands:

```
```
dpkg --purge package_name
```
```

or:

```
```
dpkg -P package_name
```
```

![](bbox=[0.14, 0.89, 0.2, 0.95])

Removing a package does not remove the configuration files. To remove all files, including the configuration files, use the purge option.