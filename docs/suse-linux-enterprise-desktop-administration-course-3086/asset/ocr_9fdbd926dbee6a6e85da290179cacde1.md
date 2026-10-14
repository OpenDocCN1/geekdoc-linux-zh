+   c. Show all the files installed by the wget package by entering:
+   
+      ```bash
+      rpm -ql wget
+      ```
+   
+      Where can you find information on the wget package? (Notice the location of the README files.)
+   
+   2. Log in as root and, using an editor of your choice, modify some comment in the `/etc/wgetrc` file. See what has changed in the files on your hard drive since the wget RPM was originally installed by entering:
+   
+      ```bash
+      rpm -V wget
+      ```
+   
+   3. View the documentation files for the wget command by entering:
+   
+      ```bash
+      rpm -qd wget
+      ```
+   
+      Notice that some of the files are still compressed (`*.gz`).

# Part II: Remove and Install Software with RPM

To remove and install software with RPM, do the following:

+   1. From a terminal window, switch to user root (`su -`, password `nov311`).
+   
+   2. Remove the gcalctool package by entering:
+   
+      ```bash
+      rpm -e gcalctool
+      ```
+   
+   3. Verify that the package is no longer installed by entering:
+   
+      ```bash
+      rpm -ql gcalctool
+      ```
+   
+   4. Insert *SUSE Linux Enterprise Desktop 10 SP1 Product DVD* into your CD-ROM drive.
+   
+   5. Enter the command `ls /media`. There will be a directory named according to the label of the DVD. Note the name of the directory.
+   
+   6. List all files included in the not installed gcalctool package by entering:
+   
+      ```bash
+      rpm -qpl /media/cdlabel/suse/i586/gcalctool*.i586.rpm
+      ```
+   
+   7. Install the gcalctool package by entering:
+   
+      ```bash
+      rpm -ihv /media/cdlabel/suse/i586/gcalc*.i586.rpm
+      ```
+   
+   8. Remove the DVD from your drive.
+   
+   9. (Conditional) If the CD drive does not open, enter the following:
+   
+      ```bash
+      eject
+      ```
+   
+      Then try again.
+   
+   10. Test the installation of the software package by entering:
+   
+       ```bash
+       gcalctool
+       ```