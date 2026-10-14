The second group consists of the following:

+   r  Read
+   w  Write
+   x  Execute

You might already be able to figure out how this is all going to work, but I'll spell it out just in case your intuition is worn out for the day. Let's say you want to change the permissions of a file (butterhaters.txt, for example) so that all users on your machine can read and write to it. After opening a Terminal window, you can make the change by typing chmod a+rw butterhaters.txt and pressing ENTER.

Oops! Just remembered that you don't want anyone changing the content of the file, eh? Well, to take back the write permissions for that file, you just need to type chmod a-w butterhaters.txt and then press ENTER. As you can see, the + gives permissions, while the - taketh away.

That's much simpler, you've got to admit.

# $ sudo

When you ran the Ubuntu Software Center in Chapter 6, you were first asked to input your password before you could run the program. The reason for this, as I mentioned is, that the Ubuntu Software Center installs the files it downloads in various folders throughout your system, almost all of which are write protected. By supplying your password, you are telling your system that you, as holder of the password, have the right to allow the Ubuntu Software Center to do that.

The command version of that same password-giving process is the sudo command. To perform an operation in a folder that is write protected, you would first type sudo and then the command you want to perform. For example, if you wanted to copy an icon image, let's call it myicon.png, to the globally located and write-protected pixmaps folder (/usr/share/pixmaps), you would type sudo cp myicon.png /usr/share/pixmaps.

After typing a command preceded by the sudo command and pressing ENTER, you will be prompted for your password. Once you type your password and press ENTER again, the command will be executed. I should mention that once you input your password, it will stay in memory for about five minutes. This means that you will not be prompted for your password when using the sudo command again within that time frame.

# $ locate

Now that you are familiar with the sudo command, let's take it out for a spin by working with the locate command. The locate command is essentially a command-line alternative to the graphical Search tool found in the Places menu. Using the command is quite easy: Simply type the command followed by a space and the name of the file you want to find.