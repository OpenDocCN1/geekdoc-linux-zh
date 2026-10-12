This command pipes the scripts into a file, where you can examine it with a text editor. You could also pipe it to the `less` pagination command to view the scripts on your display:

```
# rpm -q --scripts **filename** | less
```

# Graphical Package Management

The Fedora graphical package management tool identified in the menu as Add/Remove Software is actually an application named system-config-packages. This application replaces kpackage, gnorpm, and xrpm—all of which are no longer provided. Add/Remove Software allows you to select packages arranged in categories and install or remove them.

With the addition of Yum to Fedora Core, you may now add your own packages to the Fedora Core graphical tools' database, improving its usefulness over earlier versions.

Launch the Fedora GUI package manager by clicking the Start button on your desktop, and then choose System Settings, Add/Remove Applications. The package management tool launches with the Add and Remove Software screen, shown in Figure 7.2.

![](bbox=[0.14, 0.44, 0.81, 0.81])

**FIGURE 7.2** The initial screen of the package management tool will look familiar if you installed Fedora Core; it's the package selection screen used by the installation program.

The packages listed in the screen are organized into the Desktops, Applications, Servers, Development, and Systems groups. To choose individual package groups for installation or removal click details next to the subgroup. The numbers to the right of the package group name indicate the number of packages installed on your system and the total