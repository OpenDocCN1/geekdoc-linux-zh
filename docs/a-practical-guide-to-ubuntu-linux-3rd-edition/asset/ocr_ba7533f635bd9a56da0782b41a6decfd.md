```
```
$ sudo aptitude install xxx
...
Couldn't find package "xxx".  However, the following
packages contain "xxx" in their name:
    mixxx mixxx-data
No packages will be installed, upgraded, or removed.
... ```
```

This message means that the package you requested does not exist in the repositories that APT is searching (as specified in `sources.list`). It may also mean that the package does not exist; check the spelling. If you are not running the latest version of Ubuntu, it may be available on a later version; try enabling the backports repository in `sources.list` (discussed next).

# ## sources.list: Specific Repositories for APT to Search

The `/etc/apt/sources.list` file specifies the repositories APT searches when you ask it to find or install a package. You must modify the `sources.list` file to enable APT to download software from nondefault repositories. You can use `software-properties-gtk` to display the Software Sources window to modify `sources.list` (as explained on page 131) or you can use an editor to modify it (as explained in this section).

Each line in `sources.list` describes one repository and has the following format:

```
```
type URL repository category-list ```
```

where type is `deb` (page 533) for packages of executable files and `deb-src` for packages of source files; URL is the location of the repository, usually cdrom or an Internet address that starts with http://; repository is the name of the repository that APT is to search; and category-list is a space-separated list of categories (see “Software package categories” in the preceding section) that APT selects packages from. When a line specifies a non-Ubuntu repository, the repository and category-list may have other values. Comments begin with a hashmark (#) anywhere on a line and end at the end of the line. The comment # Added by software-properties indicates that software-properties-gtk added the line to sources.list.

The following line from sources.list causes APT to search the Lucid archive located at us.archive.ubuntu.com/lucid for deb packages that contain executable files. It accepts packages that are categorized as main or restricted:

```
```
deb http://us.archive.ubuntu.com/ubuntu/ lucid main restricted ```
```

Replacing `deb` with `deb-src` causes APT to search in the same manner for packages of source files. Use the `apt-get source` command to download source packages (page 532).

The default `sources.list` file includes repositories such as lucid (Lucid as originally released), lucid-updates (major bug fixes after the release of Intrepid), lucid-security (critical security-related updates), and lucid-backports (newer, less-tested software that is not reviewed by the Ubuntu security team). Separating security updates from