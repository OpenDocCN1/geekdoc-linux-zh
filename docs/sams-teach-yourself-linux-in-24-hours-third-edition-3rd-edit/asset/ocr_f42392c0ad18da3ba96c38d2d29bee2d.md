# 3. What are the three types of access that can be granted to each of the three types of users?

Read access on a file allows users to view the contents of a file. Read access on a directory allows users to list the contents of the directory. Write access gives users the ability to make changes to a file or to delete a file. Write access for a directory allows users to add files to a directory and to delete files in a directory. Execute access for a file means that the file can be run as a command or program. Execute access for a directory allows the user and groups to access the directory and list information about the files contained in the directory.

# 4. How do you change the password for your user account and when should you change the password?

Use the passwd command while logged in to your user account. You will be asked for your current password and then you will need to supply the new password. You should change your password on a regular basis to make it harder for others to figure out your password. You'll also want to change the password if someone learns your password. This is especially important for the superuser (or root) account because that account has access to every file and directory on the system.

# 5. Why would you want to organize users into groups and how do you create group accounts?

If several users have a need to share certain files, organize those users into a group. You can have as many group accounts on the system as you like and users can belong to more than one group. The easiest way to create a group account is to edit the /etc/group file with your favorite text editor. You'll need to give the group a name and identification number, and list the users who will be part of that group.

# 6. How can you quickly find out the groups to which you belong?

You can use either the groups command or the id command. Both will list your assigned groups, and the id command also lists the identification numbers for your user account and the group accounts to which you belong.

# Activities

+   1. Set up a directory structure in which the users on your system can store files for workgroup purposes. Then create groups depending on who needs to share files with whom and place the proper access rights to the individual directories. You'll then need to educate your users on the proper way to store files and how to set permissions so that only those people with a need to know or a need to use have access to the files.