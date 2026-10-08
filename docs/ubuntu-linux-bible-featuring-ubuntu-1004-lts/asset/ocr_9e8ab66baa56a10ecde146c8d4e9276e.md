# Part II: Ubuntu for Desktop Users

+   - DSC: A description file for the Ubuntu package that identifies the contents of the package, associated binary packages, any package dependencies for that package, and so on
- tar.gz: A compressed archive file containing the source code for the official version of this package

After retrieving these files, the apt-get source command unpacks the compressed source, creating a working directory for your development efforts, and automatically applies any patches that are available in the (optional) compressed patch file.

Chapter 23, "Software Development on Ubuntu," discusses how to install the basic packages required for software development on an Ubuntu system. If you are writing your own code or simply compiling existing applications on an Ubuntu system, that may be sufficient—except when you are building complex graphical software or when you are building your own DEB packages from the downloaded source for an Ubuntu package. In these cases, you will quickly encounter frustration from facts such as today's graphical software has dependencies on libraries, files, and utilities that you may not be familiar with or even heard of. Similarly, building DEB packages requires the use of billions and billions of utilities that may be new to you. To not worry—you're not the first person to have encountered these issues, and the apt-get command provides a handy solution, as explained in the next section.

# Satisfying Building Dependencies using apt-get

Many of the software packages available for Linux have dependencies on other packages, which makes perfect sense—why reinvent the wheel when you can link your code to it? However, if you decide to work on an existing Linux package, build-time dependencies can be frustrating. They're rarely documented, so you tend to encounter them as an iterative set of errors when you try to compile and link the application you're trying to build. This is also true when you begin to work with software packages in the formats used by different package management systems. The DEB packages used on Ubuntu and Debian systems (and derivatives) eliminate the dependency mumble-jumbo that you encounter with other package formats (such as RPM), but require the presence of entirely related utilities in order to build and package them successfully. Starting with these can be tricky—you don't know what you're missing until your process goes up flames.

The apt-get tool provides a great, automated solution for these sorts of problems through its build-dep command-line option. Using this command-option, followed by the name of the package you want to build, automatically identifies, retrieves, and installs all of the files, libraries, and tools required to build the specified package. The following is an example of the output when retrieving dependencies for the MythTV package used as an example in the previous section:

```
$ sudo apt-get build-dep mythtv
Reading package lists...
Building dependency tree... Done
The following NEW packages will be installed
```

694