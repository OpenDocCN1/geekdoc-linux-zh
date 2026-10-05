# 86 Part II: Installing SuSE Linux

YaST will alert you (at the moment that you select a package to be installed) of any package dependencies that may exist and offer to automatically select the necessary packages. If you are having problems with package dependencies, please read the section on package dependencies, that follows.

If you do not want to save your changes, press Esc to return to the Series selection window. We encourage you to view the contents of the different series to become familiar with some of the packages on the SuSE Linux For Dummies CD-ROM.

After you have finished selecting or viewing the packages, press F10 to get back to the main package management menu.

Although the Series window is helpful, you might want to view all the packages on the SuSE Linux For Dummies CD-ROM in alphabetical order, which you can do from the Series selection screen. From this screen, press the F4 key to re-sort the packages. The Selection of Packages For screen appears. First on the list is the Series option, followed by All Packages. Select All Packages and packages from the menu list; then press Enter. In the next screen, select All Packages (Excluding Sources) and then press Enter. A list of all packages in alphabetical order appears.

Following are more options to complete the installation of packages.

You use the Check Dependencies of Packages option to — check the dependencies of the various packages that you have selected to install on your system. If you have selected additional packages to be installed, we recommend that, as a precautionary measure, you verify that all dependencies are satisfied.

The three types of package dependency are as follows:

+   Package requires Package B. This type of package dependency can easily be resolved by YaST. If this package dependency is unresolved, YaST shows you the package that is selected to be installed and then the package that is required as well. The two packages are separated by the word [AND]. You can quickly add the necessary package(s) by selecting AUTO.

+   Package should not be installed with Package B. This type of package dependency issue requires your intervention. YaST shows you the two packages that have been selected to be installed. These two packages are separated by the word [EXCL], which stands for exclude. In this case, you need to select ABORT and go back to the package selection screen and deselect one of the two packages manually. An example of this package dependency issue is shown in 5-21.

![](bbox=[0.135, 0.395, 0.235, 0.565])