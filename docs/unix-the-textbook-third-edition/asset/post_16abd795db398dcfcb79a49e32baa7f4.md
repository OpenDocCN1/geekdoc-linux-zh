
![](img/02e070097d401d3bf7de4bf1c470b267_1160_0.png)

**FIGURE 23.18 Update Manager window.**

System > Administration > Update Manager. The Update Manager GUI appears on screen, as shown in Figure 23.18.

As seen in Figure 23.18, no updates are currently available for the system. If upgrades were available, a dialog would appear in the main pane of the Update Manager window showing you the availability of new system upgrades. You would then be allowed to accept or decline downloading and installation of the available software modules. Then, if you accept, their download status and installation status would be shown. They would automatically be installed, and you would have to reboot the system before they took effect.

The pkg command allows you to add, remove, and update existing software packages on the system, including upgrading the operating system itself. Section 23.7.2 will give a brief introduction to the pkg command and its options that allow you to update the user application package software.

You can type the following two lines as superuser on the command line in a terminal window to see the version numbers of available operating system upgrades, and the upgrade release you are currently working on:

```
root@solaris:~# pkg list -af entire
NAME (PUBLISHER)                          VERSION                    IFO
entire                                    0.5.11-0.175.1.0.0.24.2    i --
entire                                    0.5.11-0.175.0.10.1.0.0    ---
entire                                    0.5.11-0.175.0.0.0.2.0     ---
entire                                    0.5.11-0.151.0.0.1         ---
root@solaris:~# uname -v
11.1
```

The output of the first command shows that the latest upgrade release is 0.5.11-0.175.1.0.0.24.2, and the i in the IFO column means that you are on that release currently. The output of the second command shows that you are using major release 11.1 of Solaris.

Then, if a new major release is available to you without a Solaris service contract, you can type the following command to update to that new major release:

```
root@solaris:~# pkg update
```

If any major update is available at the default repository, the operating system will be updated automatically.

### 23.7.2 Updating the Installed Application Packages and Installing New Application Packages in Solaris

The easiest and most effective way to update or add new application packages to the system is with the Package Manager, which is launched by making the pull-down menu choice System > Administration > Package Manager. The Package Manager GUI appears on screen, as shown in Figure 23.19.

As seen in Figure 23.19, the repository (or publisher) that is being used is Solaris, the major package category selected is System, and the subcategory selected is Administration and Configuration. A total of 56 packages are in this category, none of which has been selected. To add a new package, choose one of the major categories, and then a subcategory, and examine the list of available packages. Under the Status column, you can see if a package has been installed already or has not.

In Figure 23.20, we show the choices you would make in order to install tkinter-27, the tkinter bindings to Tcl/Tk that were used in Chapter 16 to add GUI elements to Python programs. This package is found in the Solaris repository, in major package category Development, subcategory Python.

Before installing this package, you would have to install the python-27 package shown in the listing above tkinter-27 in the Development subcategory. Python 2.6 comes pre-installed with Solaris, so installing the python-27 package first to overwrite Python 2.6 is necessary. As seen in Chapter 16, the main Python program, via importing, uses the tkinter library modules in a subsidiary way.

Highlight and put a check in the box next to the package and then click on the Install/Update button at the top of the screen. That package will be installed. You will see the progress of downloading and installation in the main pane of the Package Manager window.

![](img/02e070097d401d3bf7de4bf1c470b267_1161_0.png)
