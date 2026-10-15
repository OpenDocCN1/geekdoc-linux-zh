If any major update is available at the default repository, the operating system will be updated automatically.

# 23.7.2 Updating the Installed Application Packages and Installing New Application Packages in Solaris

The easiest and most effective way to update or add new application packages to the system is with the Package Manager, which is launched by making the pull-down menu choice System>Administration>Package Manager. The Package Manager GUI appears on screen, as shown in Figure 23.19.

As seen in Figure 23.19, the repository (or publisher) that is being used is Solaris, the major package category selected is System, and the subcategory selected is Administration and Configuration. A total of 56 packages are in this category, none of which has been selected. To add a new package, choose one of the major categories, and then a subcategory, and examine the list of available packages. Under the Status column, you can see if a package has been installed already or has not.

In Figure 23.20, we show the choices you would make in order to install tkinter-27, the tkinter bindings to tcl/tk that were used in Chapter 16 to add GUI elements to Python programs. This package is found in the Solaris repository, in major package category Development, subcategory Python.

Before installing this package, you would have to install the python-27 package shown in the listing above tkinter-27 in the Development subcategory. Python 2.6 comes pre-installed with Solaris, so installing the python-27 package first to overwrite Python 2.6 is necessary. As seen in Chapter 16, the main Python program, via importing, uses the tkinter library modules in a subsidiary way.

Highlight and put a check in the box next to the package and then click on the Install/Update button at the top of the screen. That package will be installed. You will see the progress of downloading and installation in the main pane of the Package Manager window.

![](bbox=[0.28, 0.86, 0.72, 0.97])