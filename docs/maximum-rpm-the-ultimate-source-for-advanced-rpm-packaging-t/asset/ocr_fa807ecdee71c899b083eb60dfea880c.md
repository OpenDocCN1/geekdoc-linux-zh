# 11:3.6. The Missing Spec File Sections

Our sample spec file is somewhat simplistic and it’s missing two sections that might be used in more complex situations. We’ll go over each one briefly here. More complete information on these sections will be given at various points in the book.

# 11.3.6.1. The Install/Uninstall Scripts

One missing section to our spec file is the section that would define one or more of four possible scripts. The scripts are executed at various times when a package is installed or erased.

The scripts can be executed at the following points:

+   - Before a package is installed
+   - After a package is installed
+   - Before a package is erased
+   - After a package is erased

We’ll see how these scripts are used in Chapter 20.

# 11.3.6.2. The %clean Section

The other missing section has the rather descriptive title %clean. This section can be used to clean up any files that are not part of the application’s normal build area. For example, if the application creates a directory structure in /tmp as part of its build, it will not be removed. By adding a sh script to the %clean section, such situations can be handled gracefully, right after the binary package is created.

# 11.4. Starting the Build

Now it’s time to begin the build. First, we change directory into the directory holding cdpayer’s spec file:

```
# cd /usr/src/redhat/SPECS
#
```

Next, we start the build with an rpm -b command:

```
# rpm -ba cdpayer-1.0.spec
```

The a following the -b option directs RPM to perform all phases of the build process. Sometimes it is necessary to stop at various phases during the initial build to resolve problems that crop up while writing the spec file. In these cases, other letters can be used after the -b in order to stop the build at the desired phase. For this example, however, we will continue through the entire build process.