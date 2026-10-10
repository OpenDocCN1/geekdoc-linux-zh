# EXERCISE 19.1 (continued)

3. Open the Disks application from your graphical desktop menu.

4. Select the icon for the USB storage device from the left-side list of storage devices.

5. Click the minus button under the disk partition layout on the right side of the window. Click the Delete button in the dialog box that appears (if the partition is a Linux partition and is currently mounted, you will have to unmount it first).

6. When the partition is deleted, a plus button will appear under the partition. Click the plus sign button to create a new partition.

7. Click the Next button to partition the entire USB drive.

8. In the Volume Name text box, type Test Drive.

9. In the Test section, select the radio button "Internal disk for use with Linux systems only (ext4)."

10. Under that option, select the Password Protect Volume (LUKS) check box. Click Next.

11. Enter a password for the encrypted volume, and confirm it. Don’t forget the password you choose, as you’ll need it to mount the new drive.

12. Click Create to start building the encrypted drive.

13. When the process completes, view the drive from your File Manager program.

14. Remove the USB drive and plug it into a non-Linux workstation. If the workstation prompts you to reformat the drive, select Cancel.

15. Plug the drive back into your Linux workstation. At the password prompt, enter the password you assigned in step 11. Linux will mount the drive and allow you to read and write to the drive.

16. If you wish to convert the USB drive back for normal use, plug it into your workstation and follow the prompts to reformat the drive.

# Summary

There are many aspects to protecting a Linux system for use in today’s world. Most security practices break down into user security, system security, and network security. For user security, there are many different methods for authenticating users and authorizing them to access resources. The Kerberos package provides a centralized login system for multiple network servers. The LDAP package creates a distributed database for defining resources and users and granting users access to the network resources. The RADIUS package is a simpler authentication package that’s commonly used for network devices, such as switches and