FIGURE 15.4
RpmDrake lets you know which packages on the distribution CD-ROM have not been installed on the system.

![](bbox=[0.28, 0.24, 0.7, 0.56])

+   7. Install a package. Click the Install button. You will be told which Linux-Mandrake distribution CD-ROM to insert in the CD-ROM drive.
+   8. Place the CD-ROM in the CD-ROM drive and click OK. You might find that RpmDrake opens and closes the CD-ROM drive door for you.
+   9. Wait while the package installs on your system. You'll see a progress window while the package is added to the system. After the package is installed, it's ready for you and all the other users on your system to use.

# Managing Packages with the rpm Command

In the first half of this hour, you learned how easy it is to use a package management tool, such as RpmDrake or KPackage, to delete applications from your system and to add new ones. These tools are a front end to the rpm command. The rpm command uses a database (located in the /var/lib/rpm directory) to keep track of the software that is installed on the system and the files that are needed so that each installed package runs properly.

# Uninstalling Software

So, let's start from the beginning one more time. Locate the shell prompt, and find out which packages are installed on your Linux system. To view the list of installed