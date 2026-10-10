```
# yum update yum
```

Next, you can check for updates. Then you can choose to either update selected packages or all available packages. Here is how:

```
# yum check-update
```

The check-update option causes yum to check the software repositories for available updated versions of RPM packages you have installed. If you see a package you want to update, you can use the update option. For example, to update the nmap-frontend package, type the following:

```
# yum update nmap-frontend
```

To update all packages that have updates available, type the following:

```
# yum update
```

This command could take a while to complete, depending on how long it has been since the last time you installed updates and on how many total packages are installed on your computer. If, instead of trying to remember to do updates, you want them to happen automatically, the following section describes how to do that.

# # Managing RPM Packages

Both graphical and command-line tools are available for managing your systems. The Add/Remove Software window lets you display categories of software packages installed on and available for your system. The rpm command offers an extensive range of features for installing, uninstalling, listing, and verifying your RPM packages.

# ## Using the Add/Remove Window

Unless you installed every package that comes with CentOS, as you go through this book, you will probably find that you want to add some software packages after your initial installation. To do that, you can use the yum command as already described. You can also use rpm, a general-purpose command for installing any software packages in RPM format, described in the following section. However, the application with the most user-friendly interface is the Add/Remove Software window, which provides a graphical interface for installing packages.

The Add/Remove Software window provides a lot of flexibility to search, browse, list, and install software packages from yum repositories. To open the Add/Remove Software window, select Applications > Add/Remove Software from the menu on the top panel.

With the Add/Remove Software window displayed, you can find both available and installed packages as follows:

+   ■ Click on the Browse tab to browse software by categories. Select a main category from the left column, and then a group. With the group checked, click on the “Optional packages” button to see all packages and select other packages from that category’s group that would be installed.