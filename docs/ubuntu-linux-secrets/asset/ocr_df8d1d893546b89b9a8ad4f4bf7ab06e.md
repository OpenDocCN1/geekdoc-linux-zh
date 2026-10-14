# The Toolbar

The toolbar provides quick access to common functions in Synaptic:

+   - **Reload:** Refresh the package list from the configured repositories
+   - **Mark All Upgrades:** Mark all installed packages that have an upgrade available.
+   - **Apply:** Perform the operations as marked in the package list.
+   - **Properties:** Display the properties for the selected package.
+   - **Quick Search:** Enter text in the text box to perform a real-time search of the package based on package names and descriptions.
+   - **Search:** Search for packages using other attributes, such as version numbers, dependencies, and the maintainer.

Although there aren't many buttons in the Synaptic toolbar, the ones supplied should cover most of the features you need for normal operations.

# The Category List

The category list helps filter the packages that appear in the package list. There are five categories of filters you can select from:

+   - **Sections:** Contains individual section filters based on the package application type.
+   - **Status:** Displays the status of the package—installed or not installed.
+   - **Origin:** Filters packages based on which repository they were loaded from.
+   - **Custom Filters:** Lets you create your own definitions for filtering packages.
+   - **Search Results:** Filters the results based on the Search tool.

The Sections filter divides packages into sections based on the primary category they belong to. There are 32 different categories of packages, such as base packages loaded at installation time, GNOME packages, KDE packages, networking packages, and library packages.

Within each category there may be multiple entries, depending on the type of applications:

+   - **Main:** open-source packages supported by Ubuntu
+   - **Multiverse:** packages that may be covered by copyright or patent licensing but are not supported by Ubuntu and are not provided with automatic updates
+   - **Restricted:** packages that are supported by Ubuntu but are not open-source programs, such as proprietary hardware drivers
+   - **Universe:** packages that are open-source and supported by the open-source community but are not supported directly by Ubuntu (Ubuntu doesn't guarantee updates for these packages but may provide them if they are available)

> By default, Ubuntu allows you to install the highest-available version of a software package. Sometimes, though, this can cause problems when working with other packages in the distribution. If you need to synchronize all of the packages in your distribution to the same release levels, click the Distribution tab in the Preferences window and select the Always Prefer the Installed Version option.