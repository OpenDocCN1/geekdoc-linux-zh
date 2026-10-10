The *root* user is the *superuser* in Linux — the one with permissions to do anything in the system. You're better off reserving that account for your own exclusive use. You need to assign a password that you can remember but that others cannot guess easily. Make the password at least eight characters long, include a mix of letters and numbers, and (for good measure) throw in some special characters, such as `+` or `*`.

Type the password on the first line, and re-enter the password on the next line. Each character in the password appears as an asterisk (`*`) on-screen. Both entries must match before the installation program accepts your pass-word. This feature ensures that a mistyped (or guessed) password doesn't work.

You must enter the *root* password before you can proceed with the rest of the installation. After you have done so, click the Next button to continue with the installation.

# ## Selecting and installing the package groups

After you set up the key system parameters, the installer displays a screen from which you can select Fedora Core package groups to install. After you select the package groups, you can take a coffee break and let the Fedora Core installation program get busy formatting the disk partitions and copy-ing all your selected files to those partitions.

A *package group* is made up of several Fedora Core packages. Each Fedora Core package, in turn, includes many files that make up specific software.

![](bbox=[0.13, 0.52, 0.22, 0.58])

Figure 2-9 shows the screen with the list of package groups (in effect, the software components) that you can choose to install. The left side of the screen displays the categories of package groups and the right side displays the package groups for the currently selected category. An icon, a descrip-tive label, and a check box identify each package group.

Some package groups are already selected, as indicated by the check marks in the check boxes. Think of the selected package groups as the minimal set of packages recommended for installation. You can, however, choose to install any or all of the components. Use the mouse to move up and down in the scrolling list and click a check box to select or deselect that package group.

![](bbox=[0.15, 0.81, 0.24, 0.87])

In an actual production installation of Fedora Core, you install exactly the package groups you need. However, when you're trying to learn everything about Fedora Core, you need many different packages. If you have enough hard drive space (at least 6GB) for the Linux partition, select the Everything package group to install all the package groups so that you can try all that Fedora Core has to offer.