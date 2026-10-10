
## Note

Currently, package sets are supported only by Progeny Debian CDs or download sites. You cannot use gnome-apt-pkgset with an ordinary Debian source.

-   1. Log in as the root user.
-   2. Start gnome-apt-pkgset. Either:
    -   Select **Programs > System > Add/Remove Software** from the main menu.
    -   Or type `gnome-apt-pkgset` at the command line.

In either case, the Add/Remove Package Set window opens.

![](img/e36b94f8548b09d00212238f073b11d9_271_0.png)

The window consists of four sections:

-   **Available Software**: A list of package sets. A package set with a check in the box is installed. A package set with a box that is unselected is not installed.
-   **Description**: A summary of what is in the package set.
-   **Buttons**: The possible functions.
-   **Details**: The current status of the package set and the amount of hard drive space it occupies once installed.

-   3. Select the packages to work with. A package set is highlighted when selected.

![](img/e36b94f8548b09d00212238f073b11d9_272_0.png)

**Note**

A package set may be selected regardless of whether it is installed or not. However, all you would want to do with an uninstalled package set is install it.

-   4. Select a function from the buttons on the right of the window:
    -   **Apply**: Install the selected package.
    -   **Revert**: Undo the previous action and restore the package set to its original status.
    -   **Update**: Update the list of package sets available from the sources.
    -   **Upgrade**: Upgrade the selected package set if a newer version is available.
-   5. When you are finished, select the Close button to close the Add/Remove Software window.

# Installing and Removing Packages With the apt-pkgset Command

Progeny Debian simplifies package selection by grouping related packages into sets. If a program requires more than one package, you can install all the packages at the same time using Progeny's apt-pkgset utility.

As the name implies, apt-pkgset is the command line version of GNOME apt-pkgset, Progeny’s desktop tool.

Both are based on the apt utility. Both include much of the functionality of apt, and works in much the same way. For example, like apt, both depend on a sources list.

However, experienced users may find apt-pkgset limiting and prefer to use apt. See “Installing and Removing Packages With the apt-get Command,” page 273.

Type: `apt-pkgset COMMAND PACKAGESSET`.

No hyphen is placed in front of a command.

![](img/e36b94f8548b09d00212238f073b11d9_274_0.png)

## Note

For a list of package sets, see `/usr/share/package-sets`. Each package set includes a file with an extension of `.contents`, which lists the packages in the set, and a file with an extension of `.description`, which displays in gnome-apt-pkgset.

### The apt-pkgset Command

| Command | Action |
| :--- | :--- |
| install | Adds the package set to your system. |
| remove | Removes the package set from your system. |
| status | Reports on the package set's status. |
| purge | Removes the package set from your system and all files associated with it. |

# Installing and Removing Packages With the apt-get Command

The apt-get (A Package Tool or Advanced Package Tool) utility is widely considered one of the most sophisticated package tools available. Although still in development, apt-get can reliably upgrade your system over the internet or upgrade all packages on your system in a single operation.

The apt-get command can run from the command line, or be selected as a source in dselect, the old text-based package management tool in Debian.

The apt-get utility is not so much a command, but a collection of commands. This fact is reflected in its format, which can include not only options, but a specific command as well.

> Type: `apt-get OPTIONS COMMAND PACKAGE_NAME`.

Note that:

-   You may be asked questions during the install. Many can be answered with a y (“yes”) or n (“no”).
-   Some commands can be entered without specifying package names. If no packages are mentioned, commands like *upgrade* affect the entire system. Other commands, such as *install*, require that a package is specified.
-   Options can be entered as part of the command or set in `/etc/apt/apt.conf`. Options set in the configuration file can be overridden from the command line by using the option `OPTION_NAME=no`.

### The apt-get Command (Manage Packages): Options

| Option | Action | Comment |
| :--- | :--- | :--- |
| -b<br>--compile<br>--build | Compiles source packages after they are downloaded. | |
| -d<br>--download-only | Downloads packages, but does not unpack them. | The option for the configuration file is: `apt::Get::Download-only` |
| -f<br>--fix-broken | Adds missing dependencies. | The option for the configuration file is: `apt::Get::Fix-Broken` |
| --force-yes | Forces an action. | No prompts for actions are given.<br>In some cases, this option could make your system unusable.<br>The option for the configuration file is: `apt::Get::force-yes`. |
| --ignore-hold | Ignores hold flags on a package. | Use with the dist-upgrade command for efficiency.<br>The option for the configuration file is: `apt::Get::ignore-hold`. |
| -m<br>--ignore-missing<br>--fix-missing | Ignores missing or corrupted packages. | Do not use with -f or --fix-broken. |
| --no-download | Prevents downloading. | Only packages already downloaded are affected by other commands or options. |
| --no-upgrade | To prevent the upgrading of packages | The option for the configuration file is: `apt::Get::--no-upgrade`. |
| -u<br>--show-upgraded | Displays a list of all packages to be upgraded. | The option for the configuration file is: `apt::Get::Show-Upgraded`. |
| -y<br>--yes<br>--assume-yes | Automatically replies “yes” to all prompts. | The option for the configuration file is: `apt::Get::Assume-yes`. If an error occurs, then apt-get stops. |

### The apt-get Command (Manage Packages): Commands

| Option | Action | Comment |
| :--- | :--- | :--- |
| autoclean | Removes package files that can no longer be downloaded from the sources. | |
| check | Updates listings of packages and check for broken packages | |
| clean | Clear the local listings of retrieved package files. | |
| dist-upgrade | Installs the latest versions of all packages currently installed, as well as any necessary dependencies. | |
| install PACKAGE | Installs packages | Enter only the package name, not the full file name. |
| remove PACKAGE | Removes packages. | Enter only the package name, not the full file name. |
| source PACKAGE | Finds and downloads source packages | Use the `--compile` option to convert the source packages to binary packages. Use the `--download-only` option to download, but not unpack. |
| update | Updates package overview files with information from the source. | Run the update command first. |
| upgrade | Installs the latest versions of all packages currently installed. | Run the update command first. |

# Editing Source Lists

Source lists are essential to the use of apt-get. Without at least one valid source, apt-get is not usable.

Sources for packages are listed in two files:

-   `/etc/apt/sources.list`: Any source.
-   `/var/state/apt/cdroms.list`: CD sources.

![](img/e36b94f8548b09d00212238f073b11d9_279_0.png)

All source lists can be opened in a text editor. However, you can also use tools to automate editing.

# Adding a New Source

-   1. Type `apt-setup`. The Apt Configuration window opens.

![](img/e36b94f8548b09d00212238f073b11d9_280_0.png)

**Note**

apt-setup removes all comments from `/etc/apt/sources.list`.

-   2. Select the type of source from the list. Then select the OK button.
-   3. Follow the on-line instructions. Depending on the type of source you select, you may be asked:
    -   Whether you want to use a site that includes software restricted in the United States.
    -   Whether you want to use non-free software.

Before you continue, you are given the choices of whether to use each of these categories of software. If you are an American citizen or prefer to use only free software, consider your choices carefully before continuing.

If you choose to edit a source file directly, then the file opens in the vim editor.
