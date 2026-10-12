3. Click the Details button to find out the details of the package you're installing.

For example, select the Graphical Internet group and the Graphical Internet Package Details window opens. You see that the Mozilla mail client is included.

4. Select the check box next to the menu option.

5. Click the Close button to return to the Package Management window.

6. Click the Update button and the Preparing Systems Update window opens.

The Package Manager determines which additional packages are needed by the package you're installing. After the dependencies are determined, the Completed System Preparation window displays the number of packages to be installed and how much disk space they require.

7. Click the Continue button.

The Information window opens and you're prompted to insert the DVD.

8. Insert the CD and click OK.

The System Update Progress Installing window shows a progress meter.

9. Insert additional CDs, if you're prompted, and click the OK button in the Information window.

After the installation process is finished, the System Update Process window shows the Update Complete message.

10. Click the OK button to return to the Add and Remove Software window.

Until the advent of the RPM (and the Debian Package Manager on Debian Linux systems), Linux software was distributed only by tar archives, which are sometimes referred to as tarballs (or more descriptively, hairballs). The tar file storage mechanism stores one or more files in a single file in a tar format. A tar file has the .tar file suffix; if the tar file is compressed, it has a suffix like .tqz or .tar.gz. Using the tar-based distribution system is sufficient if your software doesn't change often and you're young. But when you need to upgrade or change software or work with complex software systems, tar becomes quite difficult to work with. Rather than spend your life spitting up hairballs, use systems such as RPM to greatly simplify your life.

# Removing an RPM package

You can remove Red Hat packages as easily as you install them. Use the RPM erase (-e) function, which is the opposite of the install (-i) function. The