
In the output above, the repository id is shown on the first column (repo id) of each line. Use only the part before the first /, so the id for the CentOS-7 - Updates repo is updates, and not updates/7/x86_64.

```
# yum-config-manager --disable updates
```

The command above will disable the updates repo. To re-enable it use:

```
# yum-config-manager --enable updates
```

> NOTE Yum stores downloaded packages and associated metadata in a cache directory (usually /var/cache/yum). As the system gets upgraded and new packages are installed, this cache can get quite large. To clean the cache and reclaim disk space you can use the yum clean command, followed by what to clean. The most useful parameters are packages (yum clean packages) to delete downloaded packages and metadata (yum clean metadata) to delete associated metadata. See the manual page for yum (type man yum) for more information.

## DNF

dnf is the package management tool used on Fedora, and is a fork of yum. As such, many of the commands and parameters are similar. This section will give you just a quick overview of dnf.

### Searching for packages

- `dnf search PATTERN`, where `PATTERN` is what you are searching for. For example, `dnf search unzip` will show all packages that contain the word `unzip` in the name or description.

### Getting information about a package

- `dnf info PACKAGENAME`

### Installing packages

- `dnf install PACKAGENAME`, where `PACKAGENAME` is the name of the package you wish to install. You can find the name by performing a search.

### Removing packages

- `dnf remove PACKAGENAME`

### Upgrading packages

- `dnf upgrade PACKAGENAME` to update only one package. Omit the package name to upgrade all the packages in the system.

### Finding out which package provides a specific file

```
dnf provides FILENAME
```

### Getting a list of all the packages installed in the system

```
dnf list --installed
```

### Listing the contents of a package

```
dnf repoquery -l PACKAGENAME
```

> **NOTE** `dnf` has a built-in help system, which shows more information (such as extra parameters) for each command. To use it, type `dnf help` followed by the command, like `dnf help install`.

## Managing Software Repositories

Just as with `yum` and `zypper`, `dnf` works with software repositories (repos). Each distribution has a list of default repositories, and administrators can add or remove repos as needed.

To get a list of all available repositories, use `dnf repolist`. To list only enabled repositories, add the `--enabled` option, and to list only disabled repositories, add the `--disabled` option.

```
# dnf repolist
Last metadata expiration check: 0:20:09 ago on Sat 21 Sep 2019 02:39:43 PM -03.
repo id                       repo_name                              status
*fedora                       Fedora 30 - x86_64                     56,582
*fedora-modular               Fedora Modular 30 - x86_64                 135
*updates                      Fedora 30 - x86_64 - Updates           12,774
*updates-modular              Fedora Modular 30 - x86_64 - Updates     145
```

To add a repository, use `dnf config-manager --add-repo URL`, where `URL` is the full URL to the repository. To enable a repository, use `dnf config-manager --set-enabled REPO_ID`.

Likewise, to disable a repository use `dnf config-manager --set-disabled REPO_ID`. In both cases `REPO_ID` is the unique ID for the repository, which you can get using `dnf repolist`. Added repositories are enabled by default.

Repositories are stored in `.repo` files in the directory `/etc/yum.repos.d/`, with exactly the same syntax used for `yum`.

## Zypper

zypper is the package management tool used on SUSE Linux and openSUSE. Feature-wise it is similar to apt and yum, being able to install, update and remove packages from a system, with automated dependency resolution.

### Updating the Package Index

Like other package management tools, zypper works with repositories containing packages and metadata. This metadata needs to be refreshed from time to time, so that the utility will know about the latest packages available. To do a refresh, simply type:

```
# zypper refresh
Repository 'Non-OSS Repository' is up to date.
Repository 'Main Repository' is up to date.
Repository 'Main Update Repository' is up to date.
Repository 'Update Repository (Non-Oss)' is up to date.
All repositories have been refreshed.
```

zypper has an auto-refresh feature that can be enabled on a per-repository basis, meaning that some repos may be refreshed automatically before a query or package installation, and others may need to be refreshed manually. You will learn how to control this feature shortly.

### Searching for Packages

To search for a package, use the `search` (or `se`) operator, followed by the package name:

```
# zypper se gnumeric
Loading repository data...
Reading installed packages...

S | Name            | Summary                                  | Type
--+------------------+------------------------------------------+--------
| gnumeric          | Spreadsheet Application              | package
| gnumeric-devel    | Spreadsheet Application              | package
| gnumeric-doc      | Documentation files for Gnumeric     | package
| gnumeric-lang     | Translations for package gnumeric    | package
```

The search operator can also be used to obtain a list of all the installed packages in the system. To do so, use the `-i` parameter without a package name, as in `zypper se -i`.

To see if a specific package is installed, add the package name to the command above. For example, the following command will search among the installed packages for any containing “firefox” in the name:

```
# zypper se -i firefox
Loading repository data...
Reading installed packages...

S | Name                            | Summary                       | Type
--+-----------------------------------+-----------------------------+------
i | MozillaFirefox                  | Mozilla Firefox Web B-> | package
i | MozillaFirefox-branding-openSUSE | openSUSE branding of -> | package
i | MozillaFirefox-translations-common | Common translations f-> | package
```

To search only among non-installed packages, add the `-u` parameter to the `se` operator.

### Installing, Upgrading and Removing Packages

To install a software package, use the `install` (or `in`) operator, followed by the package name. Like so:

```
# zypper in unrar
zypper in unrar
Loading repository data...
Reading installed packages...
Resolving package dependencies...

The following NEW package is going to be installed:
 unrar

1 new package to install.
Overall download size: 141.2 KiB. Already cached: 0 B. After the operation, additional 301.6 KiB will be used.
Continue? [y/n/v/...? shows all options] (y): y
Retrieving package unrar-5.7.5-lp151.1.1.x86_64
(1/1), 141.2 KiB (301.6 KiB unpacked)
Retrieving: unrar-5.7.5-lp151.1.1.x86_64.rpm .............[done]
Checking for file conflicts: ..........................[done]
(1/1) Installing: unrar-5.7.5-lp151.1.1.x86_64 .............[done]
```

zypper can also be used to install an RPM package on disk, while trying to satisfy its dependencies using packages from the repositories. To do so, just provide the full path to the package instead of a package name, like `zypper in /home/john/newpackage.rpm`.

To update packages installed on the system, use `zypper update`. As in the installation process, this will show a list of packages to be installed/upgraded before asking if you want to proceed.

If you wish to only list the available updates, without installing anything, you can use `zypper list-updates`.

To remove a package, use the `remove` (or `rm`) operator, followed by the package name:

```
# zypper rm unrar
Loading repository data...
Reading installed packages...
Resolving package dependencies...

The following package is going to be REMOVED:
unrar

1 package to remove.
After the operation, 301.6 KiB will be freed.
Continue? [y/n/v/...? shows all options] (y): y
(1/1) Removing unrar-5.7.5-1p151.1.1.x86_64 ...................[done]
```

Keep in mind that removing a package also removes any other packages that depend on it. For example:

```
# zypper rm libgimp-2_0-0
Loading repository data...
Warning: No repositories defined. Operating only with the installed resolvables. Nothing can be installed.
Reading installed packages...
Resolving package dependencies...

The following 6 packages are going to be REMOVED:
gimp gimp-help gimp-lang gimp-plugins-python libgimp-2_0-0 libgimpui-2_0-0

6 packages to remove.
After the operation, 98.0 MiB will be freed.
Continue? [y/n/v/...? shows all options] (y):
```
