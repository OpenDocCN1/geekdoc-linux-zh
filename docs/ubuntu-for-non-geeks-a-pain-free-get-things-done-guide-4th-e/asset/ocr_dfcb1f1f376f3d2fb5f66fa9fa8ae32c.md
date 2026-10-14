# Empty the package cache

When the Ubuntu Software Center installs a program, it keeps the package used to install it for a little while in case it’s needed again. These cached files can take up quite a bit of disk space, but it’s fine to delete them (the program won’t be uninstalled or anything like that). Open a Terminal, and type `sudo apt-get clean`, followed by ENTER. Type your password if prompted, and then press ENTER to empty the cache.

# My Disk Is Completely Full

If your hard disk is completely full, you may not be able to start Ubuntu at all, and all you’ll get is a blank screen. If this happens, press CTRL-ALT-F2 to change to a Terminal login prompt. Type your username, followed by ENTER, followed by your password, followed by ENTER again, to access a command line. Once there, try clearing some disk space by typing some of the commands recommended in "My Disk Is Almost Full" on page 397. You can also use the `rm` command to remove some files in your home folder, but be careful: There’s no undo when using `rm`.

Once you’ve cleared a little disk space, type `sudo reboot` to restart the computer. With any luck, there will be enough disk space for you to be able to log in now.

# I Can’t Delete a File

The usual reason for not being able to delete a file is because you don’t have the right permissions to delete it (see Chapter 7 for an explanation of file permissions). Right-click a blank area of the folder that the file is stored in, choose Properties, and select the Permissions tab. If you are listed as the owner, make sure that your Folder Access permissions are set to Create and delete files. Click Close, and then try to delete the file again.

If you are not the owner of the folder, you’ll have to gain ownership of it before you can delete the file. This is where you need to ask yourself, "Should I really be deleting someone else’s file?" Sometimes file permissions get messed up and so the file might be yours—in that case, it’s OK to delete it. If it’s someone else’s file, though, ask for their permission first. If you’re convinced that deleting the file is a good idea, open a Terminal, and use the `chown` command to change the owner of the folder. Here’s how it works: If I wanted to delete a file called `cats.jpg` from the Pets folder in my Pictures folder, I would type `sudo chown phil ~/Pictures/Pets`, followed by the ENTER key (remember, ~ means "my home folder"). After typing my password and pressing ENTER again, I would become the owner of the Pets folder and could delete `cats.jpg` as normal. Of course, you should substitute the name of the folder and your username in place of mine to work for you.

> **NOTE**
> *Don’t use this method to delete system files (in other words, files that aren’t stored in the /home folder) unless you’re sure you know what you’re doing. You don’t have permission to delete system files for a reason; you could really screw up your system if you remove something vital.*