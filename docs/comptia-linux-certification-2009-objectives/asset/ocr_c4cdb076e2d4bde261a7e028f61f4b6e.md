+   2. List the files in the AdobeReader package.

    a. Enter `rpm -ql AdobeReader_en` to view the list of files in the package.
    b. Observe that the application files are installed in the /opt/Adobe/Reader8/bin directory.
    c. Enter `clear` to clear the terminal window.

+   3. Check the status of the files in the AdobeReader package.

    a. Enter `rpm -qs AdobeReader_en` to view the status of all files in the package.
    b. Observe that the first column displays `normal` as the status for all files, indicating that the files are correctly installed.
    c. Minimize the `root@srvA:/rpms` window.
    d. On the desktop, double-click the **Adobe Reader 8** icon.
    e. In the **Adobe Reader - License Agreement** dialog box, click **Accept** to accept the terms of the agreement.
    f. Observe that the **Adobe Reader** window is displayed, indicating that the application was successfully installed.
    g. Close the **Adobe Reader** window.
    h. Restore the `root@srvA:/rpms` window.
    i. In the `root@srvA:/rpms` window, enter `clear` to clear the screen.