handle networking configuration tasks, Internet access tasks, personal productivity tasks, and others. The mix of applications ranges from the GUI desktop to server applications.

The packages you select to install should be chosen carefully, especially if you have limited resources. Every package you install uses disk space and, once installed and running, uses RAM and CPU processing time.

Unless you chose a custom installation, the installation program will automatically choose most packages for you. If you chose a Personal Desktop installation, the installation process will select the packages that would be most useful, based on that type of installation.

You can customize the packages you use by selecting the **Select Individual Packages** option, shown in Figure 3–24. This option will allow you to select or deselect packages within a group. For example, if Games were selected, you could choose only the games you want from a list of all games.

![](bbox=[0.32, 0.31, 0.87, 0.62])

# FIGURE 3-24
Red Hat package selection.

You can also select the **Everything** option to install all packages included with the Red Hat distribution.

Some packages have dependencies on other packages. In other words, in order to install some packages, you must have the dependent packages as well. Red Hat Linux installation will check dependencies and warn you before completing the installation process. If you have any unresolved dependencies, you select the **Install packages to satisfy dependencies** option. This will install the programs to resolve dependencies automatically by adding all required packages to the list of selected packages.

Packages that you do not install during installation can be added later by running the **redhat-config-packages** command. This command will launch the Package Management Tool. This tool and packages will be discussed in more detail in Chapter 5.

You begin installation by selecting **OK** on the *Installation to Begin* dialog box (see Figure 3-25). After the packages have been selected, they will be installed on the file system. Your installation will in all likelihood complete with no problems. However, if there is a problem the details will be stored in the installation log file. This file has a copy of all messages generated during installation and may prove invaluable if you have to re-install Linux. The log file can be found in the /root/install.log directory.

A progress indicator, shown in Figure 3-26, will be displayed indicating the percentage of completion. This gives you an indication that everything is progressing correctly and not “hanging” the system.