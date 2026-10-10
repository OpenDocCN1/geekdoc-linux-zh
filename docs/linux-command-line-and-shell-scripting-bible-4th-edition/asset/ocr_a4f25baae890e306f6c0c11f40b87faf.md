> **Obviously, running apt 's upgrade option is something you should do on a regular basis to keep your system up to date. However, it is especially important to run it after a fresh distribution installation. Usually there are lots of security patches and updates that have been released since the last full release of a distribution.**

# ## Uninstalling software with apt

Getting rid of software packages with apt is as easy as installing and upgrading them. The only real choice you have to make is whether or not to keep the software's data and configuration files around afterward.

To remove a software package, but not the data and configuration files, use apt 's remove command. To remove a software package and the related data and configuration files, use the purge option:

```
```
$ sudo apt purge zsh
Reading package lists... Done
Building dependency tree
Reading state information... Done
The following package was automatically installed and is no
longer required:
  zsh-common
Use 'sudo apt autoremove' to remove it.
The following packages will be REMOVED:
  zsh*
0 upgraded, 0 newly installed, 1 to remove and 56 not
upgraded.
After this operation, 2,390 kB disk space will be freed.
Do you want to continue? [Y/n] y
(Reading database ... 180985 files and directories currently
installed.)
Removing zsh (5.8-3ubutntu1) ...
Processing triggers for man-db (2.9.1-1) ...
(Reading database ... 180928 files and directories currently
installed.)
Purging configuration files for zsh (5.8-3ubutntu1) ...
$
```
```