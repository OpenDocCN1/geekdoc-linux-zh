however, the program has a long way to go before it can offer similar functionality. Thus it is RedHat of all companies (inventor and developer of the RPM package format) which is still incapable of resolving all unsatisfied package dependencies during the installation of new packages.

At the start, gnome rpm displays all installed packages in a hierarchical order. (With RedHat 6.0 this hierarchy has been greatly simplified; it is now much clearer than.)

![](bbox=[0.218, 0.215, 0.781, 0.503])

Figure B.6 gnorpm groups the packages by categories.

If you cannot find a package but are sure that it is installed you can also determine its place in the hierarchy by means of rpm. rpm -qi perl, for example, yields the short description of the installed perl package. The group line gives information on where Perl is situated in the hierarchy (namely under Development/Languages). By the way, the hierarchy displayed in gnome has nothing to do with the components available during the first installation.

Individual packages can be selected with a click of the mouse. Ctrl or Shift plus mouse extends the selection as in Windows usage. You can even see several packages which are located in different hierarchies at the same time. This often happens involuntarily – therefore be careful with uninstallation! Use UNSELECT to completely undo the selection carried out to now.)

Three operations can be applied to selected packages: UNINSTALL, QUERY, and VERIFY.

UNINSTALL removes all files of the selected packages. (Files that are shared between separate packages are only removed with the uninstallation of the last package.)