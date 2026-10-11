This is the best possible solution to a tricky problem. The package is installed with a config file that is known to work. After all, the original file may be for an older, incompatible version of the software. However, the original file is saved so that it can be studied by the system administrator, who can decide whether the original file should be put back into service.

# 2.3. Two Handy Options

There are two options to `rpm -i` that work so well and are so useful that you might think they should be RPM's default behavior. They aren't, but using them requires only that you type an extra two characters, which are described in the following sections.

# 2.3.1. Getting a Bit More Feedback with -v

Even though `rpm -i` is doing many things, it's not very exciting, is it? When performing installs, RPM is pretty quiet unless something goes wrong. However, we can ask for a bit more output by adding -v to the command:

```
# rpm -iv eject-1.2-2.i386.rpm
Installing eject-1.2-2.i386.rpm
#
```

By adding -v, RPM displayed a simple status line. Using -v is a good idea, particularly if you're going to use a single command to install more than one package:

```
# rpm -iv *.rpm
Installing eject-1.2-2.i386.rpm
Installing libcs-1.2-3.i386.rpm
Installing logrotate-1.0-1.i386.rpm
#
```

In this case, there were three `.rpm` files in the directory. By using a simple wildcard, it's as easy to install a package as it is to install 100!

# 2.3.2. -h: Perfect for the Impatient

Sometimes a package can be quite large. Other than watching the disk activity light flash, there's no assurance that RPM is working, and if it is, how far along it is. If you add -h, RPM will print 50 hash marks (#) as the install proceeds:

```
# rpm -ih eject-1.2-2.i386.rpm
##################################################
#
```

When all 50 hash marks are printed, the package is completely installed. Using -v with -h results in a very nice display, particularly when you're installing more than one package:

```
# rpm -ivh *.rpm
eject     ##################################################
libcs     ##################################################
logrotate ##################################################
#
```