Alternatively, you can use Pirut, which provides a GUI interface for Yum, letting you download software from any Yum-configured software repository.

# Pirut Package Manager: A Repository Model of Software Management

The Pirut Package Manager is a new package management tool that now replaces the older system-config-packages, which was used primarily for the disk-based packages. The Package Manager is Internet-based, installing from online repositories only, using Yum to download and install.

Pirut is the same tool used during the installation procedure to select packages, only now you can uninstall packages. Check fedoraproject.org/wiki/Tools/yum for tips on using Yum, including a script to let you perform partial installs. Yum by default stops the entire process if there is any configuration or dependency problem with any one repository or package.

As described in Chapter 3, to use Pirut you select the Add/Remove Software entry from the Applications menu. Pirut will start up by gathering information on all your packages. You then have three different ways to use Pirut: Search, Categories, and List. The Categories method accesses Fedora packages only, whereas the List and Search methods access all the software on all your enabled repositories (you can turn a repository off by setting its enabled bit to 0 in its repo configuration file, see Chapter 29). Due to the very large number of packages available, you may find yourself using the Search method frequently. Figure 4-8 shows Pirut used to list gconf (GNOME configuration tool) packages.

With Package Manager, Yum is now integrated as the primary install packages tool. When you install a package with Package Manager, Yum will be invoked and it will automatically select and download the package from the appropriate online repository. This is a major

![](bbox=[0.15, 0.54, 0.88, 0.9])

Figure 4-8 Pirut Package Manager