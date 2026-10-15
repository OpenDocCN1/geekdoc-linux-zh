For redhat-config-packages, you can use your file manager to locate the RPM file and double-click the RPM package file. You can also, on GNOME, right-click it, and select Open With → Install Packages, or on KDE, select Install Package. redhat-config-packages starts up and checks for any dependent packages you may need. It then installs the RPM package for you.

If you are using the rpm command, you use the -U option to upgrade packages. In the following example, the rpm command with the -Uvh option installs an upgrade for Emacs:

```
# rpm -Uvh emacs-21.2-18.i386.rpm
```

# Command Line Installation: rpm

If you do not have access to the desktop, or you prefer to work from the command line interface, you can use the rpm command to manage and install software packages. rpm is the command that actually performs installation, removal, and queries of software packages. In fact, redhat-config-packages uses the rpm command to install and remove packages. An RPM package is an archive of software files that include information about how to install those files. The filenames for RPM packages end with .rpm, indicating software packages that can be installed by the Red Hat Package Manager.

# The rpm Command

With the rpm command, you can maintain packages, query them, build your own, and verify the ones you have. Maintaining packages involves installing new ones, upgrading to new versions, and uninstalling packages. The rpm command uses a set of options to determine what action to take. In addition, certain tasks, such as installing or querying packages, have their own options that further qualify the kind of action they take. For example, the -q option queries a package, but when combined with the -l option, it lists all the files in that package. Table 29-3 lists the set of rpm options. The syntax for the rpm command is as follows (rpm-package-name is the name of the software package you want to install):

```
rpm options rpm-package-name
```

A complete description of rpm and its capabilities is provided in the online manual:

```
# man rpm
```

| Mode of Operation | Effect |
|---|---|
| rpm -i options package-file | Installs a package; the complete name of the package file is required. |
| rpm -e options package-name | Uninstalls (erases) a package; you only need the name of the package, often one word. |
| rpm -q options package-name | Queries a package. An option can be a package name, a further option and package name, or an option applied to all packages. |