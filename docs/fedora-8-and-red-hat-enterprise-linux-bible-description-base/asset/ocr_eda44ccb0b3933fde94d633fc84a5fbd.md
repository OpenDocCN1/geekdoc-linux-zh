At any time you can check whether updates are available for RPM packages installed on your Fedora or RHEL system. Before doing updates with yum, however, you should always update yum itself first:

```
# yum update yum
```

Next, you can check for updates. Then you can choose to either update selected packages or all available packages. Here is how:

```
# yum check-update
```

The check-update option causes yum to check the software repositories for available updated versions of RPM packages you have installed. If you see a package you want to update, you can use the update option. For example, to update the npm-frontend package, type the following:

```
# yum update npm-frontend
```

To update all packages that have updates available, type the following:

```
# yum update
```

This command could take a while to complete, depending on how long it has been since the last time you installed updates and on how many total packages are installed on your computer. If, instead of trying to remember to do updates, you want them to happen automatically, the following section describes how to do that.

# Getting updates with Package Updater

A tool with a graphical means of doing what yum does from the command line is called the Package Updater (also referred to as Pup). Because Pup is based on yum it offers the same advantages of being able to gather updates for every repository you have enabled.

Start Pup by selecting Applications → System Tools → Software Updater. Pup checks for available updates from your repositories and displays available updates, as shown in Figure 5-1.

Scroll through the available updates (all will be selected by default) and unselect any update you don’t want to install. Click the arrow next to Update Details to see details about a package, such as which dependent packages are required and which packages will be replaced by the selected update. Click Apply updates to apply the selected updates. The selected packages are then downloaded and installed.