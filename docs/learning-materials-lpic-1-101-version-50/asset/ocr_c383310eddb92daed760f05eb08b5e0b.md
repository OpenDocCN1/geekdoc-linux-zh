# ## Summary

In this lesson, you learned:

+   - How to use **dpkg** to install and remove packages.
+   - How to list installed packages and package contents.
+   - How to reconfigure an installed package.
+   - What is **apt**, and how to install, upgrade and remove packages using it.
+   - How to use **apt-cache** to search for packages.
+   - How the `/etc/apt/sources.list` file works.
+   - How to use **apt-file** to show the contents of a package, or how to find which package contains a specific file.

The following commands were discussed:

**dpkg -i**

Installs a single package, or a space-separated list of packages.

**dpkg -r**

Removes a package, or a space-separated list of packages.

**dpkg -I**

Inspects a package, providing details on the software it installs and any needed dependencies.

**dpkg --get-selections**

Lists out every package that dpkg has installed on the system.

**dpkg -L**

Prints out a list of every file that a particular package installs.

**dpkg-query**

With a specified file name, this command will print out the package that installed the file.

**dpkg-reconfigure**

This command will re-run a packages _post-install_ script so that an administrator can make configuration adjustments to the package’s installation.