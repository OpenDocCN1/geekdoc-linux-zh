# $ sudo

When you tried to install software from the Ubuntu Software Center in chapter 6, you were asked to input your password. The reason for this, as mentioned, is that the Ubuntu Software Center installs the files it downloads in various folders throughout your system, almost all of which are protected. By supplying your password, you are telling the system that you, as holder of the password, you have the right to allow the Ubuntu Software Center to do that.

The command-line version of that same process is the sudo command. To perform an operation in a folder that is write protected, you would first type sudo and then the command you want to perform. For example, if you wanted to copy an icon image—let it be myicon.png—to the globally-located and write-protected pixmaps folder (/usr/share/pixmaps), you would type cp myicon.png /usr/share/pixmaps.

After typing a command preceded by the sudo and pressing ENTER, you will be prompted for your password and press ENTER again, the command will be executed. I should mention that once you input your password, it will stay in memory for about five minutes, so you won't be prompted for your password when using the sudo command.

# $ locate

Now that you are familiar with the sudo command, let's take it out for a spin by working with the locate command. The locate command is essentially a command-line alternative to the graphical Search tool found in the Places menu. Using the command is quite easy: Simply type the command followed by a space and the name of the file you want to find.

Before you can use this command, though, you should update the database of filenames that locate uses. This is where the sudo command, along with another command, updated, comes into play. Just type sudo updated and press ENTER. Type your password when asked to do so—and then it will seem as though nothing is happening. But don't worry. As long as the cursor in your Terminal is blinking, the process is being made, and when your user prompt returns, you will have successfully created the database file. After that, you can use the locate command.

Oh, and in the future if you think that the process seems to be taking longer and longer, don't worry—it is. The more files and applications you add to your system, the longer it will take to catalog them all.

To make this new command for a test drive, let's look for the LibreOffice Writer icon, libreoffice-writer.png. Just type the following and press ENTER:

```
locate libreoffice-writer.png
```

Your results should look like those in Figure 8-6.