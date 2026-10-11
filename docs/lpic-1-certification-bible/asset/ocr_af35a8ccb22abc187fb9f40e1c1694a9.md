Debian packages, or debs, usually contain the binary files to be installed along with other information known as metadata. This metadata holds information on the package, scripts that will be executed, and a list of any dependencies, conflicts, or suggestions. Some Debian packages contain the source code and can be compiled manually. The Debian package naming scheme is as follows:

```
package_version-build_architecture.deb
```

where:

+   * `package` is the name of the application being installed.
+   * `version` is the version number of the application.
+   * `build` is the build number of this package. Each time the package is redone this number is incremented, usually when it is tweaked in some way.
+   * `architecture` is the platform the package was compiled for.

A special type of package is available, known as a *task package*. These packages are actually empty packages with no software, but have a large number of dependencies. They are used to install a large “task” on the system, such as X Window workstation, GNOME desktop, or KDE. They are installed the same way as normal packages and have names such as `helix-gnome-task`.

# ## Using dpkg

The core package tool in Debian is `dpkg`. Most of the other tools are just overlays that make `dpkg` easier to use. But, some functions can be performed only with `dpkg`, and it is sometimes faster to use `dpkg` directly than going through another interface.

# ### Installing packages

**2.2 Installation and Package Management**

![](bbox=[0.18, 0.7, 0.24, 0.77])

+   * Use Debian package management. Be able to install, upgrade or uninstall packages.

Once you have obtained a package you want to install, you use the following command:

```
dpkg --install package_file.deb
```

or:

```
dpkg -i package_file.deb
```