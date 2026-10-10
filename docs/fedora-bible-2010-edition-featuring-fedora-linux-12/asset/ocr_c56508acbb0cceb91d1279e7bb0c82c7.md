# # Using the PackageKit Add/Remove window

Unless you installed every package that comes with Fedora, as you go through this book you will probably find that you want to add some Fedora software packages after the initial installation. To do that, you can use the `yum` command (as already described). You can also use `rpm`, a general-purpose command for installing any software packages in RPM format, described in the following section. However, the application with the most user-friendly interface is the PackageKit Add/Remove Software window, which provides a graphical interface for installing packages.

The PackageKit Add/Remove Software window replaces the older Package Manager window in Fedora. This window provides a lot of flexibility to search, browse, list, and install software packages from yum repositories. To open the Add/Remove Software window in Fedora, select System → Administration → Add/Remove Software from the menu on the top panel.

With the Add/Remove Software window displayed, you can find both available and installed packages as follows:

+   - Select a category from the left column to see all packages from that category in the right column.
+   - Enter all or part of a package name into the search box and select Find, to have all packages that include that term appear in the right column.

Packages appear with open box icons if they are installed or closed box icons if they are not. Select a package to see information about the contents of that package. With a package selected, you can choose to either install or remove it (depending on its current state).

> **NOTE:** Note that not all packages in a repository will necessarily show up in the groups shown on the left window pane. So, if you believe a package you want is in an enabled repository, but you can't browse for it, use the Find box to search for it by name.

The Add/Remove Software window appears as shown in Figure 5-2. In this example, after searching for `xfce` and displaying all packages with that term in the right column, I selected one of the packages. In the bottom of the window, I can then see a description of the package. From the Selection menu, I can choose to see a complete list of files the package contains and any packages it depends on or that depend on it. From the Selection menu, I can also go to the project’s home page or select to install the package.

# # Using the rpm command

The original command used to work with RPM package files is `rpm`. Unlike `yum`, the `rpm` command is not designed to work with repositories. Instead, `rpm` is best used to install individual packages, verify the contents of packages (before or after you install them) and query information about packages you have installed or are about to install.