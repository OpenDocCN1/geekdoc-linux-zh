
## Objective 1—Install and Uninstall Software Packages

After performing a standard SUSE Linux Enterprise Desktop 10 installation, you will often need to install additional software. To do this, start the YaST module Software > Software Management.

The installed packages and the packages that are available on the installation media are analyzed, and dependencies between packages are checked.

After the packages are checked, the dialog shown in Figure 6-1 appears to search for packages.

![](img/9129877170834ca9d5fdac5319bf5f12_179_0.png)

Figure 6-1

To find the software you want to install or uninstall, you can choose from different filters listed in the drop-down list in the upper-left corner of the window labeled **Filter**. The following filters are available:

- *Patterns*—Displays available software grouped in predefined sets of packages that logically belong together.
- *Package Groups*—Displays available software grouped by category.
- *Languages*—Displays all language-related files (for instance spell checker, help).
- *Installation Sources*—Lists all registered installation sources and displays the packages available from the respective source.
- *Search*—Lets you enter a search term and where you want YaST to search for the software package.
- *Installation Summary*—Displays all the packages with a marked status.

To find a package, select the Search filter and enter the package name or parts of the package name or some keywords in the Search field; then select Search.

The matched packages are listed in the area to the right. The installation state is shown by a small symbol in front of the package name. Figure 6-2 shows the most commonly displayed symbols.

| Symbol | Status | Description |
|---|---|---|
| ☐ | Do not install | This package is not installed and it will not be installed. |
| ☑ | Install | This package will be installed. It is not installed yet. |
| ☑ | Keep | This package is already installed. Leave it untouched. |
| ↻ | Update | This package is already installed. Update it or reinstall it (if the versions are the same). |
| 🗑 | Delete | This package is already installed. Delete it. |
| ⊘ | Taboo | This package is not installed and should not be installed under any circumstances, especially because of unresolved dependencies that other packages might have or get. Packages set to “taboo” are treated as if they did not exist on any installation media. |
| ▣ | Protected | This package is installed and should not be modified, especially because of unresolved dependencies that other packages might have or get. Use this status for third-party packages that should not be overwritten by newer versions that may come with the distribution. |
| ☑ | Autoinstall | This package will be installed automatically because some other package needs it. Hint: You may have to use “taboo” to get rid of such a package. |

**Figure 6-2**

To view a list of all possible symbols, select **Help > Symbols**.

Select the symbol of the package you want to install several times until the Install symbol appears; then select **Accept**.

You might see a dialog indicating that dependencies between packages cannot be solved and that some other packages need to be installed, too. In most cases, you can simply confirm this dialog.

If the wrong CD or DVD is in your drive, a warning appears.

To uninstall a package, select the symbol of the package until the Delete symbol appears; then select Accept. If the package you want to uninstall is needed by some other package due to dependency requirements, a message similar to the one shown in Figure 6-3 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_181_0.png)

Figure 6-3

Select the appropriate buttons to resolve the issue; then select OK – Try Again. When there are no dependency issues left, the software will be uninstalled.

![](img/9129877170834ca9d5fdac5319bf5f12_181_1.png)

## Exercise 6-1: Install and Uninstall Software

In this exercise, you install a software package (locate) that is available on the SUSE Linux Enterprise Desktop 10 installation media, and you uninstall a software package that you do not need during the course (isdn support, i4l-base).

### Detailed Steps to Complete This Exercise

- Part I: Install a Software Package
- Part II: Uninstall a Software Package

### Part I: Install a Software Package

To install a software package, do the following:

- 1. From the GNOME desktop, open the main menu.
- 2. Select More Applications.
- 3. Type ya into the Filter text box.
- 4. Select the YaST icon to start YaST.
- 5. Type the root password n0v311 in the Password Needed dialog; then select Continue or press Enter. The YaST Control Center appears.
- 6. From the YaST Control Center, select Software > Software Management.
- 7. From the Filter drop-down list, select Search.
- 8. In the Search text box, type locate; then select Search.
- 9. From the right side of the window, select the package findutils-locate.
- 10. Select Accept.
- 11. (Conditional) If requested by YaST, insert the SUSE Linux Enterprise Desktop 10 SP1 Product DVD; then select OK.
- 12. (Conditional) If you want to see what the tool locate does, open a terminal window and as root (su – with password n0v311) run the command updatedb to build the database locate needs (this step will take some time). Then enter locate fstab to find out where the file fstab or files containing the string fstab are located.

![](img/9129877170834ca9d5fdac5319bf5f12_182_0.png)

### Part II: Uninstall a Software Package

To uninstall a software package, do the following:

- 1. After you have installed the software package as described above, you are asked to install or remove more packages. Select Yes.
- 2. From the Filter drop-down list, select Package Groups.
- 3. From the left side of the window, select Hardware > ISDN.
- 4. From the right side of the window, select the check box of the i4l-base package until the Delete symbol appears; then select Accept.
- 5. A message appears to inform you about dependencies to other packages. Select Delete package (for instance Delete i4lfrm) for each package where there is a dependency; then select OK – Try Again.
- 6. You are now asked to install or remove more packages. Select No.
- 7. Close the YaST Control Center by selecting Close.
- 8. (Conditional) If you installed from DVD, remove the DVD from your drive.

## Objective 2—Manage Installation Sources

The Software Installation dialog lists only the packages that are on the current installation media.

To add more installation sources, select **Software > Installation Source** from the YaST Control Center. The dialog shown in Figure 6-4 appears.

![](img/9129877170834ca9d5fdac5319bf5f12_183_0.png)

**Figure 6-4**

To add a new source, select Add; then select the type of installation source. Depending on the type of source, you might have to provide additional information (such as the IP address of an installation server).

To edit the configuration of an existing installation source, select the source in the list; then select Edit.

If you want to disable an installation source temporarily, select the source in the list; then select Source Settings > Enable or Disable. Repeat these steps to enable it again.

To remove an installation source permanently, select the source from the list; then select Delete.

![](img/9129877170834ca9d5fdac5319bf5f12_184_0.png)

## Exercise 6-2: Add an Installation Source

In this exercise, you add installation sources for the graphics drivers from ATI and Nvidia.

### Detailed Steps to Complete This Exercise

To add the ATI and Nvidia software repositories, do the following:

- 1. From the GNOME desktop, open the main menu and select More Applications > System > YAST. Enter the root password (`novell`) in the Password Needed dialog.
- 2. Select **Software > Installation Source**.
- 3. In the Configure Software Catalogs dialog, select Add.
- 4. In the Media Type dialog, select **HTTP**; then select Next.
- 5. In the Server and Directory dialog, type:
  
  Server Name: www2.ati.com  
  Directory on Server: suse  
  Authentication: Anonymous
  
  Select Next.
- 6. In the **Signed with Untrusted Public Key** warning dialog, select **Trust the key**.
- 7. In the **Import Untrusted GnuPG Key** dialog, read the explanation. Select **Import**. In a production environment, your decision to import or not import the key might depend on the security policies in place.
- 8. Repeat Steps 3 to 7 for the following server:
  
  Server Name: download.nvidia.com  
  Directory on Server: novell  
  Authentication: Anonymous
- 9. In the Configure Software Catalogs dialog, select Finish.

## Objective 3—Configure Novell Customer Center and Online Update

Computer installations are rarely, if ever, static. Software gets added and removed, updates are installed to add new functionality or to correct bugs, and so on.

This objective covers software updates on the SUSE Linux Enterprise Desktop 10. You need to understand the following:

- Novell Customer Center Configuration
- Online Update
