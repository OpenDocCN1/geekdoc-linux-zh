# PACKAGE QUERYING

RPM has many powerful querying options so you can easily search to find out what software is installed on your system or what package a file belongs to or to get a list of files that belong to a certain package.

# SYSTEM VERIFICATION

If you think you may have accidentally deleted a file belonging to a certain package, you can use RPM to verify the package. If RPM finds anything amiss, you can reinstall the package without disturbing any configuration files that you have modified.

# WHY USE RPM?

Before RPM was developed, most Unix software packages were distributed as compressed tar files, and this arrangement is still fairly common. But if you install software that comes packaged this way, you run certain risks and lose some potential benefits:

+   - What if the new package overlays certain files that other packages depend upon, and the new version is not compatible with the old one? You could end up rendering one or more packages useless.
+   - What happens if you want to remove the package from your system? It can be a real nuisance to find all the files associated with a package and manually remove them without affecting other software that shares common files.
+   - What if the new version of PandaCalc replaces all your customization files with default versions? You’ll have to do all that work again.

RPM solves all these problems — by warning you when new packages may affect existing ones, by providing an intelligent uninstall feature, and by preserving your customization files during upgrades. If you’re thinking of downloading and installing some new software, always check to see if an RPM version is available first, and you’ll save yourself some trouble later on.

In this chapter, you’ll learn about the command-line interface to RPM and a graphical front-end called GnoRPM. They both get the job done, so it’s up to you to decide which one to use.