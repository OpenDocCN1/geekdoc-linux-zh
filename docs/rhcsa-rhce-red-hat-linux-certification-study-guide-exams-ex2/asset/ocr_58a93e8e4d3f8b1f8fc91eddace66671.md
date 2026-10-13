the repository where a package is available or note that the package is already installed.

+   2. Enter the gpk-application command in a GUI command line. This should open the Add/Remove Software tool.
+   
+   3. In a second command line console, type in the yum grouplist command. In the Add/Remove Software tool, select Package Collections. Compare the list of package groups in each output.
+   
+   4. Review available package groups in the Add/Remove Software tool. For example, click the arrow next to Servers. Under the options that appear, click CIFS Server. (CIFS stands for the Common Internet File System.) There's only one official package in the RHEL 6 configuration of this group. If you see more than one package, they are different versions of the same package. Select the latest available version of the package, which will be installed when you click Apply.
+   
+   5. Click the All Packages option. Review the list of available packages. Packages that are already selected (or don't even have a check box) are currently installed. If you select or deselect a package, it will be installed or removed (with dependencies) when you click Apply.
+   
+   6. Locate the text box in the upper-left corner of the Add/Remove Software tool. Type in a common search term such as gnome and watch as a long list of packages are shown. Compare the result to the output of the yum search gnome command.
+   
+   7. Use a less common search term such as iptables. Highlight the iptables package and review it in the lower-right part of the screen. Compare the result to the output of the yum info iptables command.
+   
+   8. Once you've selected some packages, click Apply. If there are dependencies, you'll see a window with a list of packages that you've selected for installation and removal. Depending on whether the packages are to be installed or removed, you'll see an Install or Remove button and a Cancel button.
+   
+   9. Wait as downloads packages are installed. When finished, click System | Quit to exit from the Add/Remove Software tool.