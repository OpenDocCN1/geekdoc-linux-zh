+   ► Distribute NNLS components among several different servers.
+   
+   As stated earlier, this is strongly recommended for large organizations. The horsepower required from your server to run all the NNLS components on the same system is considerable.
+   
+   If you have thousands of users requesting services at the same time, the system could slow to-a crawl. The custom option allows you to specify which server each component is to be placed on. By dividing the load among servers, NNLS can provide stellar high-load performance.
+   
+   A nice feature of NNLS is the fact that it will check each server you select for the appropriate dependencies and install missing packages for you (if it has them).

+   ► Install into an existing eDirectory tree or create a new one.

+   ► Customize where various objects used by NNLS components are stored in the tree.

Because of the sheer amount of data you must provide, it's a good idea to fill out Table 5.1 from earlier in this section.

As with the express option, you can automate the installation process using a response file. Because the custom installation requires a lot more information from the administrator, you must use a different response file. The file for a custom installation is available for download from http://www.novell.com/documentation/lg/nnls/answers/custom.txt.

As with the express response file, you must edit the file with a Linux text editor to provide the requested information. Then you must save the file as /etc/opt/novell/enterprise_linux_services_install.conf and run the install script with the -s option.

Once you have selected the type of install you want to use, you're ready to begin! In the next lab exercise, we will perform a complete custom installation using detailed steps. At a high-level, the steps you need to follow to install NNLS are as follows:

+   1. Mount your NNLS 1.0 CD or ISO image on your Linux server.
+   2. Mount the floppy disk containing your NICI file on your Linux server.
+   3. Open a terminal session and change to the root user account by entering su - and supplying your root user password.
+   4. Change to the directory where the NNLS 1.0 CD or ISO image is mounted.