```
cups-ipp-utils cups-pd c cups-server-common firefox-locale-ar (...)

74 upgraded, 0 newly installed, 0 to remove and 1 not upgraded.
Need to get 243 MB of archives.
After this operation, 30.7 kB of additional disk space will be used.
Do you want to continue? [Y/n]
```

The summary at the bottom of the output shows how many packages will be upgraded, how many will be installed, removed or kept back, the total download size and how much extra disk space will be needed to complete the operation. To complete the upgrade, just answer Y and wait for apt-get to finish the task.

To upgrade a single package, just run `apt-get upgrade` followed by the package name. As in dpkg, `apt-get` will first check if a previous version of a package is installed. If so, the package will be upgraded to the newest version available in the repository. If not, a fresh copy will be installed.

> TIP You can also use `apt upgrade` and `apt update`.

# The Local Cache

When you install or update a package, the corresponding `.deb` file is downloaded to a local cache directory before the package is installed. By default, this directory is `/var/cache/apt/archives`. Partially downloaded files are copied to `/var/cache/apt/archives/partial/`.

As you install and update packages, the cache directory can get quite large. To reclaim space, you can empty the cache by using the `apt-get clean` command. This will remove the contents of the `/var/cache/apt/archives` and `/var/cache/apt/archives/partial/` directories.

> TIP You can also use `apt clean`.

# Searching for Packages

The `apt-cache` utility can be used to perform operations on the package index, such as searching for a specific package or listing which packages contain a specific file.

To conduct a search, use `apt-cache search` followed by a search pattern. The output will be a list of every package that contains the pattern, either in its package name, description or files provided.

```
# apt-cache search p7zip
liblzma-dev - XZ-format compression library - development files
liblzma5 - XZ-format compression library
```