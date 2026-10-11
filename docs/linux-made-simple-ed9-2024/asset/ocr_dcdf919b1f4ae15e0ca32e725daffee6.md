# Files: File permissions uncovered

Take a deep breath and launch into the murky world of users, groups and files in Ubuntu.

+   - **Quick tip** If you share your PC with others, open System Settings and select User Accounts to give everyone their own, private user account and home folder. Share files with others using your Public folder.

If you've migrated to Ubuntu from Windows, you'll already have an inking about file permissions and users, plus the effect one has on the other, but it can still be a confusing subject to grasp, particularly where Linux is concerned. Before you dive into the confusing world of who's got what access to which file, acquaint yourself with the essentials of file permissions.

# Grasp the fundamentals

Despite appearances to the contrary, every single thing in Linux is a file, including folders and hardware devices. On top of this, the Linux file system – ext2, ext3 or ext4 – applies special permissions to files that ultimately determine how they're accessed, and by whom.

There are three levels of access to files in Linux, and while they differ slightly between files and folders, they follow the same broad principle: read, write and execute. Access to any or all of these permissions can be granted or blocked. Read access typically means viewing a file or looking at the contents of a folder, while write allows you to edit a file, or – in the case of folders – create or delete files that are inside that folder. Execute allows users to run files that are programs, or actually enter the folder in question.

These three levels are expressed as **r** (read), **w** (write) and **x** (execute). For example, a file with full access is expressed as **rwx**, while one that's read-only is **r–**, and another that has read and execute access is **rx**. These terms – **rw** and **x –** are important because they're displayed when you view extended

# Exploring Nautilus's file permissions interface

+   - **Owner** Any other restriction when managing permissions through Nautilus is that you can only view a file or folder's owner through the Permissions tab.
+   - **Change group** Click the 'Group:' drop-down menu to view a list of available user groups on your system – most refer to hidden system users, so avoid these.
+   - **Access rights** If you're not the owner of a file or folder you can view permissions, but you can't change them – in Nautilus or via the Terminal.

+   - **Execute** This box only requires ticking if it has a .run or .bin file extension, or you want to run a file as a script. Note it affects the permissions for all users.
+   - **Change access** Click here to change the access level – you have fewer options in Nautilus. The three options shown for folders translate to --, r-x and rwx respectively.
+   - **Enclosed files** This button will apply the same permissions you've set for the folder to all files inside it, ensuring they stay consistent.

![](bbox=[0.36, 0.64, 0.9, 0.84])