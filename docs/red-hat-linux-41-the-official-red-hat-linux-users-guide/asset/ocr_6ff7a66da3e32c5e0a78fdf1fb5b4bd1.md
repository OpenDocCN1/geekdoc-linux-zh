packages. When it’s finished, the installed packages will appear in the the main glint windows and any old versions of the packages will be removed.

It is much better to use the upgrade option than to uninstall the old versions of a package and then install the new one. Using upgrade ensures that any changes you made to package configuration files get preserved properly, while doing it manually could cause those changes to be lost.

If you run out of disk space during an installation, the install will fail. However, the package which was being installed when the error occurred may leave some files around. To clean this up, reinstall the package after you’ve made more disk space available.

# 9.4.4 Uninstalling Packages

Uninstalling a package is not the same as upgrading one. When a package is uninstalled, any files it uses that are not needed by other packages on your system are removed. Changed configuration files are copied to `<filename>.rpmsave` so you can reuse them later.

Like verifying and querying packages, you can remove a package through the buttons on the right of the glint window or through a context sensitive menu. Remember that when you make a choice from a group’s menu, the operation is performed on all of the packages in that group, so be careful!

Once you’ve begun the uninstall, glint asks for confirmation, showing a window like the one in figure 9.12. All of the packages that are about to be uninstalled are listed. You should look at them all to ensure you’re not about to remove something you want to keep. Clicking the Yes button will start the uninstallation process. After it completes, the packages and groups that have been removed will disappear from any windows they were in.