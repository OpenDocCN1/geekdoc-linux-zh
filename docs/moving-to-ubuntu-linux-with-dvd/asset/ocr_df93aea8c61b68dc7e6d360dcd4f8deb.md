Those other nine characters (characters 2 through 10) indicate permissions for the user or owner of the file (first three), the group (second group of three), and others or everyone else (last three). If you look at an image and see `-rw-rw-r--`, you’ll see that the user and group have read and write permissions. All others have read-only permission, the same permission everyone else has. The $r$ stands for read, the $w$ for write, and the $x$ (not seen above) for executable.

> **Shell Out** Want to see the permissions at the shell prompt? Simply add -1 to the ls command, like this:
> `ls -1 directory_name`

From time to time during your Linux experience, you have to change permissions, sometimes to give someone else access to your directories or files or to make a script or program executable. By using the Permissions tab, you can select read, write, or execute permissions for the owner (yourself), the group you belong to, and everyone else by checking off the permissions in the appropriate check boxes.

# ## Deleting Files and Folders

Every once in a while, a file or directory has outlived its usefulness. It is time to be ruthless and do a little cleaning of the old file system.
As you’ve no doubt come to expect, there are several ways to get rid of an offending file or directory. The friendliest and safest method is to drag the file from Nautilus to the *wastebasket icon* over on the right side of your lower panel. For the novice, this is a safer method because items sent to the trash can be recovered—until you take out the trash, that is. Until that time, you can click the trash can icon and (you guessed it) a Nautilus window appears, showing you the items you have sent to the trash. These items can then be moved (or copied) back to wherever you need them. To remove files from the trash permanently, right-click the trash can icon and click Empty the Wastebasket.

> **Note** After you empty the wastebasket, those files are gone forever.