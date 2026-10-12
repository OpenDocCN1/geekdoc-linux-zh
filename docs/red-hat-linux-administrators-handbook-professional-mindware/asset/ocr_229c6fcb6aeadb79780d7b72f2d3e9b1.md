server. Make a list of server software that you want to install. The Red Hat Linux installation program allows you to select individual packages before installation. Take the time to go through all the lists and select only the necessary packages. Sometimes, the installation program will install one or more packages that are prerequisites to the packages that you have selected. It will actually show you these prerequisite package names after you complete your package selection during the installation process. Write down the names of these packages.

After you install all the necessary packages and boot the system for the first time, you can either look at the installation log stored in /tmp or run the following rpm command to get the complete listing of all installed packages:

```
```bash
rpm -qa > /tmp/all.packages
```
```

Carefully go through the `/tmp/all.packages` file to detect any packages that you do not recall approving for installation. If the package does not show up in your prerequisite list, you may want to find out more about the package by using the following command:

```
```bash
rpm -qi package_name
```
```

If the package seems unnecessary, remove it by using the following command:

```
```bash
rpm -e package_name
```
```

The rpm command checks whether the package_name is required by some other package. If it is, you get a warning message and the package is not removed unless you use the -e -f option. Carefully read what the warning says and decide accordingly. If no other packages are dependent upon this package, it is cleanly removed from your system.

I recommend not installing the following types of packages on a computer that will be used as a server on the Internet:

+   * Anything related to X Window or X Window itself.
+   * Any multimedia applications (except the real-audio/video server package if you plan to provide real-audio/video services).
+   * Any interpreter other than what is required. I personally use only Perl for scripting and therefore do not install other scripting languages.
+   * Any unnecessary server software, such as NFS, NIS, INN, POP2 or 3, or Samba, that you do not need to have.