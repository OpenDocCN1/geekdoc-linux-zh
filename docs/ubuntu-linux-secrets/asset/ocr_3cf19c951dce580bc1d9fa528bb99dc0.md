# Removing Packages

When you view the package list in Synaptic, installed packages have a green status box, indicating that all of the components for that package are installed. Right-clicking on the package produces a menu that gives you three options for managing the installed package:

+   - Mark for Reinstallation: Reinstall the package from the current version in the repository.
+   - Mark for Removal: Remove only the files installed by the package.
+   - Mark for Complete Removal: Remove the package files plus any additional configuration or data files associated with the application.

If you want to reinstall the package but have customized configuration files you'd like to use with the reinstallation, select Mark for Removal rather than Mark for Complete Removal. A complete removal will delete any custom configuration you've done to the package.

> If you request to remove a package that installed dependencies, Synaptic will ask whether you want to remove those packages as well. Ubuntu attempts to determine whether any installed packages use the dependent packages, but sometimes things get missed, especially if you have installed universe packages that aren't closely monitored by Ubuntu. Pay attention to the list of packages that Synaptic asks to remove. Be especially careful when removing library packages.

# Command-Line Package Management

If you're working on the Ubuntu server command line or just want to get to the command-line level on your workstation, you can't use the Synaptic graphical package management tools. Instead, you must use the command-line tool, apt-get. This section walks you through how to use the apt-get tool to update and install software on your Ubuntu system.

# Setting Repositories

Just as with the graphical package installers, you must configure the repositories the apt-get program contacts to update and install software packages. The list of repositories is stored in the /etc/apt/sources.list file.

The sources.list file contains multiple lines, one for each repository. The format of each file is

```
deb [address] [dist name] [package type list]
```

The [address] parameter specifies the web address of the repository. If Ubuntu detected your network connection during installation, it automatically provides the default Ubuntu repositories for your distribution version. If not, you'll need to go to the Ubuntu web site and find the current repository web addresses for your distribution.

The [dist name] parameter defines the name of the Ubuntu distribution version from which to retrieve package updates for installation (such as Gutsy, Hardy, or Intrepid).