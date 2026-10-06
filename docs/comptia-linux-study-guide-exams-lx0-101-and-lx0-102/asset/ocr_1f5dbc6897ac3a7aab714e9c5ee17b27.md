# Using Debian Packages

-P or --purge    Removes a package, including configuration files

--get-selections    Displays currently installed packages

-p or --print-avail    Displays information about an installed package

-I or --info    Displays information about an uninstalled package

-l pattern or --list pattern Lists all installed packages whose names match pattern

-L or --listfiles    Lists the installed files associated with a package

-S pattern or --search pattern Locates the package(s) that own file(s) specified by pattern

-C or --audit    Searches for partially installed packages and suggests what to do with them

# TABLE 2.5 Options for fine-tuning dpkg actions

| Option | Used with actions | Description |
|---|---|---|
| --root=dir | All | modifies the Linux system using a root directory located at dir. Can be used to maintain one Linux installation discrete from another one, say during OS installation or emergency maintenance. |
| -B or --auto-deconfigure | -r | disables packages that rely on one that is being removed. |
| --force-things | Assorted | overrides defaults that would ordinarily cause dpkg to abort. Consult the dpkg manager page for details of things this option does. |
| --ignore-depends=package | -i, -r | ignores dependency information for the specified package. |
| --no-act | -i,-r | checks for dependencies, conflicts, and other problems without actually installing or removing the package. |
| --recursive | -i | installs all packages that match the package-name wildcard in the specified directory and all subdirectories. |
| -G | -i | doesn't install the package if a newer version of the package is already installed. |
| -E or --skip-same-version | -i | doesn't install the package if the same version of the package is already installed. |