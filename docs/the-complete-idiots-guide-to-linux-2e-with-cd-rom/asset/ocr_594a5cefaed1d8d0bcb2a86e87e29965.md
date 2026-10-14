regular user access to these devices, you’ll need to tell your system that it is OK for a user to mount the device. You’ll learn how to do this next.

# Configuring the System to Allow Users to Access the CD-ROM and the Floppy

The system keeps a configuration file for disks and where they are mounted in /etc/fstab. This configuration file is just a regular text file that you can edit using any text editor, including KEdit. However, permissions to modify this file are restricted to root, the superuser; to change and modify this file, you need to have this privilege.

You can obtain this privilege in two ways:

+   - You can exit the system, log in as root, and reenter the system
+   - You can start up a File Manager with superuser (root) privileges

For the sake of learning a new trick, let’s walk through the second option.

# Starting a Superuser KFM Session

To launch a KFM window as the superuser, you can go to the Application Starter|System and pick the File manager (Superuser Mode) command (see the following figure).

![](bbox=[0.2, 0.84, 0.3, 0.92])

Launch a KFM window with superuser powers from the System submenu.

This will display a window asking you for the root password. After you enter it, a KFM window similar to the ones you’ve used before will be displayed.

Superuser KFM windows are distinguished from normal KFM windows by a red tab that tells you to exercise care when manipulating files and directories (see the next figure). One wrong manipulation can trash your system.

![](bbox=[0.22, 0.00122, 0.32, 0.00132])

A superuser KFM window has a red tab on the menu bar pane.

Type /etc/fstab and hit Enter in the location field on the root KFM window. A new KEdit will launch. This instance of KEdit inherits the superuser permissions, allowing you to modify the file.

After you finish editing the file, as explained in the section “Creating kdelnk Files for the Floppy and CD,” close the KEdit window and the KFM root window to ensure that you don’t use these empowered applications by mistake.