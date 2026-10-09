+   3. Install MySQL packages.
a. Right-click any of the selected packages and choose the Open with "Software Installer" option.
b. In the **Installing packages** window, observe that four packages are listed.
c. Click **Apply**.
d. In the **Unable to verify perl-DBD-MySQL-3.0007-2.el5.i386** dialog box, click **Install anyway** to install the package.
e. Click **Install anyway** three times to install the remaining three packages.
f. In the **Software installed successfully** message box, click **OK**.

+   4. Start the MySQL daemon and verify that the installation was successful.
a. Choose **Applications→Accessories→Terminal** to display the terminal window.
b. Enter *service mysqld start* to start the MySQL daemon.
c. Observe that the **OK** status message is displayed after the "Starting MySQL" message, indicating that MySQL daemon was successfully started.
d. Enter *chkconfig mysqld on* to automatically start the MySQL daemon service.
e. Enter *mysql* to verify that you can connect to the MySQL server.
f. Observe that the *mysql* prompt is displayed indicating that MySQL is functional and you can use it to create databases.
g. Enter *quit* to exit the *mysql* prompt.
h. Enter *clear* to clear the terminal window.
i. Close the **Server - File Browser** window.