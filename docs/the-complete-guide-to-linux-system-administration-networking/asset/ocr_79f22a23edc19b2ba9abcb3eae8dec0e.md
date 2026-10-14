The hundreds of options supported by the rpm command fall into several categories:

+   - Use the -q option to query the database and learn about packages (either installed packages or those not yet installed).
+   - Use the -i or -U option to install or upgrade a package when you have a new rpm file you want to add to your system.
+   - Use the -e option to erase (uninstall) an rpm package from your system.

These options can be used in combination. For example, to query the rpm database for a list of all files included in a package, you combine the -q option with the -l option:

```
$ rpm -ql setup
```

To see a list of all the packages installed on your system, use the -q and -a options:

```
$ rpm -qa
```

The -q and -a options are often used together with the grep command to search for a package when you are unsure of the exact name or whether the package is installed. For example, if you wanted to see what Web server-related packages were installed, and you knew that the Web server program was httpd, you might use a command such as this one to see a list of all package names that include the string "http":

```
$ rpm -qa | grep http
```

If you see a file on your system and need to know of which package it is a part, use the -q option with the -f option (you must use the complete path of the file you want to learn about).

```
$ rpm -qf /etc/services
```

You can install new rpm files either from your Linux CD-ROM or you can download them from the Internet. Suppose that you have downloaded an updated rpm file for the Z shell from rpmfind.net. The file you have downloaded to the /tmp directory is called zsh-4.2.0-1.i386.rpm. You want to install it on your system. This command would do that:

```
# rpm -Uvh /tmp/zsh-4.2.0-1.i386.rpm
```

![](bbox=[0.14, 0.9, 0.22, 0.98])

> You can use rpm to query information about packages when logged in as any user, but only root can install, upgrade, or delete packages.

If you have downloaded a collection of packages that need to be installed together, you can use a regular expression to specify the package names. The rpm utility examines each matching package name and determines the correct order in which the packages need to be installed. For example, suppose you had not installed the gimp image manipulation program