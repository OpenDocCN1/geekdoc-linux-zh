# FINDING THE PACKAGE THAT HOLDS A FILE YOU NEED 521

Do you want to continue? [Y/n?] y
Writing extended state information... Done
(Reading database ... 123778 files and directories currently installed.)
Removing apache2.2-common ... ...
Purging configuration files for apache2.2-common ...

# Finding THE PACKAGE THAT HOLDS A FILE YOU NEED

Finding a package with a name that sounds like...

+   tip The aptitude search command looks for packages with names that match a pattern. For example, the command aptitude search vnc displays a list packages that have vnc in their names. See page 529 for more information.

You may know the name of a file or utility you need but not know the name of the package that holds the file. There are several ways you can locate a package that holds the file. The Ubuntu web page, packages.ubuntu.com, allows you to search for packages based on several criteria. Partway down the page is a section titled Search that gives you two ways to search for packages. Search the contents of packages, to search for a package that holds a specific file. Enter the name of the file in the text box labeled Keyword, click the radio button labeled packages that contain files named like this, select the distribution and architecture you are working with, and click Search. The browser displays a list of packages that hold the file you are looking for. For example, suppose you are compiling a program and get the following error message:

```
xv.h:174:22: error: X11/Xlib.h: No such file or directory
```

On an Intel x86-compatible system running Lucid and the file Xlib.h holds in the X11 directory. When you enter the X11/Xlib in the text box labeled Keyword (on packages.ubuntu.com), the browser displays the following list:

```
usr/include/X11/Xlib.h libx11-dev
usr/lib/Tenra/lib/include/x5/lib.api/X11.libh tender
```

Click the package name on the right to display more information about the package holding the file listed on the left. The most likely candidate is the first entry, which is supported by Ubuntu and is the most generic. You can install this package using the following command:

```
$ sudo apt install libx11-dev
```

apt-file You can also use the apt-file utility to search for a package containing a specified file. Before you can use this, you must install it and update the package list on the local system. Updating the package list takes a few minutes. Because apt-file displays