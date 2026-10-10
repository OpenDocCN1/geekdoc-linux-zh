
```bash
[student@desktop ~]$ sudo usermod -L username
[sudo] password for student: studentpassword
```

Another benefit of using the sudo access is that all commands that any user runs using sudo are logged to /var/log/secure.

## CHAPTER 11. Commands and Functions for the Beginner

Here we present two guides for the Linux newbie. The first will be a handy cheat sheet so to speak. If you have to memorize anything for the desktop or server, this is the way to go. The second list is more comprehensive, but again, it is not the end of the Commands needed to truly advance to novice levels with Linux.

### List of Top 29 Commands for Beginners- If you have to memorize them

1. apt-get Search for software packages and install
2. bzip2 Compress/decompress a file
3. cd Change Directory
4. chmod Change access permissions for a file
5. cp Copy one or more files or directories location
6. date Display or set the date & time
7. df Display free and used disk space
8. emacs Text editor
9. exit Exit shell
10. find Search for files that meet a certain pattern
11. hostname Print or change system name
12. install Copy files, set/change attributes
13. locate Search and find files
14. ls List information about directory contents
15. man Display help information for a certain command
16. mkdir Create new folder/directory
17. mv Move or rename directories and files
18. nano Text editor with shortcuts to menus
19. open Open a file in original application
20. ps Display of current process status
21. pwd Display/Print working directory
22. quota Display disk use, limits
23. reboot Reboot system
24. rm Remove, delete directories or files
25. rmdir Remove, delete, empty directories or folders
26. shutdown Shutdown or restart
27. sftp Secure File Transfer Program
28. sudo Execute command as certain user with all permissions
29. tar Store, list or extract files from a tarfile or tarball/archive

## CHAPTER 12. Using Linux Text Editors

Even though you are capable of using a desktop that has a functional graphic interface, you will find the desire to interact with the Linux environment by editing and creating files using editors that belong outside the GUI. Learning how to use text editors will allow you to make your own shell scripts and communicate with the programs that you want to run in your operating system. At the same time, you will also be able to fix possible problems in your configuration files, especially when the X Window System fails to load.

In this chapter, you will learn how to use GUI and text mode editors, which will both allow you to configure and create text files.

### How to Use GUI Text Editors

The GUI desktops KDE and GNOME come with built-in text editors that have their own graphical user interfaces. You can load these editors from the main menu. For example, if you want to open the GUI text editor for GNOME, navigate to Applications->Text Editor and then select the file gedit. Once the editor loads, you can select the Open option found on the toolbar and then pull up a file that you want to edit or change directories that contain the file that you want in the dialog box labeled Open File.

GNOME's text editor is also capable of loading multiple files at a time and even switch in between windows to work with them. A typical editing session will look like this:

Image from: Linux All-in-One for Dummies

Looking at this image, you will notice that there are two files loaded in the editor – one appears to be a new file, and the other is named motd. You can find the names of the files that are being edited in the tabs, which you can also click to switch windows.

If you open a file that is only available to be read, you will see a text that displays “Read Only” added to the filename displayed in the window title. If you have access to superuser privileges, you can of course change the ownership of the file in order for you to make edits.

If you have a KDE desktop, you can pull up the KWrite text editor by navigating to Applications -> Accessories -> Text Editor.

Just like in the GNOME text editor, you can click on the Open icon or navigate to File -> Open in order to load the file that you want to edit. This is how the KWrite editor looks like:

Image from: Linux All-in-One for Dummies

### Using ed and vi as Text Editors

As you may have noticed, text editors that have GUIs allow you to edit files using your mouse and keyboard similar to how you would type a document in a word processor. However, text mode editors are more complex than that — you only have your keyboard as your input device and you will have to type in commands in order to perform tasks such as copying, pasting, or cutting texts.

Text editors that come native with Linux are called ed and vi.

#### ed

This line oriented editor is going to be extremely useful when you loaded a minimal version of the OS and you do not have the support that you need yet for a full-screen editor yet. You may encounter this situation when you load up Linux from a boot disk.

Using ed allows you to work in these modes:

-   Command mode – this is the default mode, in which everything that you type is being interpreted by Linux as a command. In this mode, ed has a rather simple set of commands, wherein each command is made up of one or multiple characters.
-   Text input mode – this mode is for typing longer texts. You can enter this mode when you enter the commands a (meaning append), c (meaning change), or i (meaning insert). When you are done entering several lines of text, you can leave this mode by putting only a period on an empty line.

To practice using ed as an editor, perform the following commands:

This will copy the file `/etc/fstab` in your home directory. To start editing this file, key in this command;

The editor will then respond to display this output:

From this example, the -p option allowed you to set the colon (the symbol : ) as your prompt and also opened the fstab file copy that you have in your home directory. Each time the ed editor pulls up a file for editing, it displays the number of characters that are within the editable file and then displays the colon prompt that signals you can enter your commands through the editor.

Tip: when you want to edit using ed, see to it that you have turned on the prompt using the -p option. This will help you distinguish that you are in the text input mode and not in the command mode.

Once ed has opened up a file that you want to edit, you will immediately be in the last line of the file. To see what the current line number is, or the line where the command that you are going to input is going to be placed, you can use the . = command, which will appear like this:

From this result, you know now that the file fstab contains 9 lines. Now, if you want to see all the lines that are contained in the file, you can use the following command:

This will return with an output that appears like this:

If you want to go to a line number that you want to edit (line 2, for example), simply type in the line number on the prompt. The editor will then respond by displaying that particular line:

If, for example, you want to delete a line that contains the word cdrom, all you need to do is to search for that particular string. You can do this by typing the / sign, then the string that you need to find:

This will return with the line that contains the line that you want to edit, which becomes the current line. To delete it, simply enter d on the prompt.

To replace a specific string with a different one, the s command will be handy to use. For example, if you want to replace the string “cdrom” with “cd”, enter this command:

To input a line in front of the line that you are currently editing, use the following command:

From this point, you can enter as many lines that you want. If you are done typing, enter the period sign on an empty line to indicate that you are ending the text input mode. After doing so, you will see that ed switches back to the command mode.

If you want to save the changes that you have made to the file, enter the w command on the prompt. If you want to save the changes and exit the editor, key in wq on the prompt to perform both actions. The output will appear like this:

The editor will then save all changes that you have performed and then display the number of characters that were saved. Afterward, Linux will exit the editor. However, if you want to exit without saving any changes that you have made to the file, key in the q command to exit without writing to the file.

Of course, there are different other commands that you can use in ed. Here is a summary of the most common commands used in the ed editor:

Image from: Linux All-in-One for Dummies

#### vi

The editor vi is definitely easier to use compared to ed, although it is still considered as a command line editor. The vi allows you to use a text editor in a full screen mode, which means that you can view multiple lines at the same time. It also helps to know that most of the Unix systems (this includes Linux) come with this text editor; which means that once you understand how this editor works, you will be able to modify text files in any system that is based in Unix.

Note: When you edit a text file using vi, the editor reads it into a buffer memory. This means that you can change the file in the buffer. At the same time, this editor also makes use of temporary files during an edit session, which means that no changes are made in the original file unless you save any changes that you made.

To start editing with vi, key in vi followed by the filename:
