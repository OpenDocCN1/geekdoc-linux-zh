there, try clearing some disk space by typing some of the commands recommended in the previous section, “My Disk Is Almost Full.” You can also use the rm command to remove files in your Home folder, but be careful: There’s no undo when using rm.

Once you've cleared a little disk space, type `sudo` to restart the computer. With any luck, there will be enough disk space for you to be able to log in.

If this all seems a bit tedious and technical to you, you could always try booting from the Ubuntu Live CD included with this book. Once you have using Nautilus to mount your hard disk, allowing you to find and delete files using a more friendly graphical interface. (This goes without saying, but do be careful what you delete!) Chapter 2 for more on starting from the live CD and Chapter 19 for tips on how to mount hard-disk partitions.

# Can’t Delete a File

The usual reason for not being able delete a file is that you don't have the permissions to delete it (see Chapter 7 for an explanation of file permissions). Right-click a blank area of the folder where the file is stored, choose `Properties`, and select the `Permissions` tab. If you are listed as the owner, make sure that your Folder Access permissions are set to Create and delete files. Click `Close` and then try to delete the file again.

If you are not the owner of the folder, you’ll have to gain ownership of it before you delete the file. This is where to ask yourself, “Should I really deleting someone else’s file?” Sometimes file permissions get messed up, and so the file is yours—in that case, it’s okay to delete it. If it’s someone’s file, though, ask for his permission.

If you’re convinced that the file is a good idea, open a Terminal and use the `chown` command to change the owner of the folder. Here’s how it works: I wanted to delete a file called `cats.jpg` from the Pets in the Shared folder, I would type `sudo chown phil ~/Shared/Pets`, where `~` means “my Home folder”. After typing my password and pressing ENTER again, I would become the owner of the Pets folder and delete `cats.jpg`. Normal of course, you should substitute the name of the folder and your username in mine for this to work for you.

> Don’t use this method to delete system files (in other words, files that aren’t stored in the /home folder) unless you are sure what you’re doing. There’s a good reason why you don’t have permission to delete system files by default; you could really screw up your system if you remove something vital.

# Software Installation Problems

Ubuntu’s software management tools tend to operate pretty smoothly these days. Nevertheless, I’ve included some troubleshooting tips for two or three problems that tend to be common (but to be getting rarer with each release). If you’re having a problem with installing, removing, or updating packages, this section is for you.