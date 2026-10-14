**TIP** When trying to comprehend how Linux handles files, it helps if you remember it's a clone of Unix, an operating system designed to have hundreds or even thousands of different users. One of the fun facts about Linux is that, although you might use it on your humble desktop computer, it really is capable of running on a mainframe computer without any adaptation.

You can view and edit file permissions for any file or folder by right-clicking it and selecting Properties from the menu. In the dialog box that appears, click the Permissions tab. You can then change permissions for a file or folder that you own.

Let’s take a look at permissions in action. The user called frank creates a spreadsheet. He’s a member of the accounts group, along with the user called jane, his colleague in the Accounts department. frank wants jane to be able to edit the spreadsheet, so he sets the group permissions for the file so that anybody in the accounts group can both read and write the spreadsheet. frank wants other people in the company to be able to view the spreadsheet, including users in other departments who aren’t in the accounts group. Yet he doesn’t want them to be able to edit it. So, he sets read-only permission for others.

In the case of operating system files, owned by the root user, permissions are normally set so that other users on the system can view (read) files, but not modify them (write). Important system folders are also protected in this way, so that new files can’t be created there. The root user also owns the root of the filesystem (known as C:\ in Windows). This particular permission is “hard-wired,” so that only the root user can create new files or folders there. Again, this is for security reasons.

**NOTE** Under Ubuntu, group file permissions are unimportant when it comes to files owned by root, because the root user is in a private group of its own, also called root.

We’ll come back to file permissions in Chapter 5, which looks at the Linux command-line. It’s at the command-line that file permissions become much more important, particularly when administering the system.

# Nautilus: An overview

The file browsing program provided with Ubuntu is called Nautilus. It’s a staple of the Gnome desktop environment and is extremely powerful, yet also user-friendly.

You can start Nautilus by clicking Places ➔ Home Folder. This will let you view the contents of your personal folder within the /home folder.