When the rpm command removes a package, it checks whether the package provides capabilities needed by other packages. If so, it suppresses execution and warns you. If necessary, you can override this check by specifying the --nodeps flag.
When the rpm command removes a package, it also saves any modified configuration files. Thus, when you need a little extra disk space to cope with any emergency, you can easily remove and later reinstall some packages. Now, complete Exercise 12.2, which requires you to remove a package.

# EXERCISE 12.2

Removing a Package
Often, a system administrator must free disk space on a system. A convenient way to do so is to delete a package, which can be reinstalled when more disk space is available. To verify your ability to remove a package, use the rpm command to remove the package you added in the previous exercise. As usual, you can consult this chapter for help; before taking the RHCE exam, though, be sure you remove a package without the assistance of a book or notes.

# Performing Updates and Fixes

From time to time, new versions of packages are published. Often, these contain bug fixes or new features that are important. RPM makes it easy to install new versions of packages. To do so, use a command of the form

```
rpm -Uvh package_file_name
```

where package_file_name is the name of the file containing the new version of the package. You can omit the -v and -h flags, if you prefer. The -U flag causes the rpm command to remove the existing package (as though you performed an rpm -e) and then install the new package (as though you performed an rpm -i). When the rpm command removes the old, it saves any modified configuration files, renaming them by appending. .rpms to their names. If the specified file is not currently installed, the rpm command installs it. Therefore, many system administrators use the -U in place of the -i flag; rpm -U will install the package if it is absent or update it if it is present.