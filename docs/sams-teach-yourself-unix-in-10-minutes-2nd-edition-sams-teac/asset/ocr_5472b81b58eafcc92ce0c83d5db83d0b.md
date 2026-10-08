Notice that I didn't have to step back from the /rob directory to the /home directory and then from /priv switch and change directories to the root directory (/). I could simply specify /priv/home/rob when using the cd command.

> Unix Commands Are Similar to Windows Commands...Sometimes The cd command used with Unix is identical to the one used with Windows-based desktops when using the command or MS-DOS prompt. You can see this command and other Windows commands that are similar to Unix commands by going to start => run (or programs => run) and typing cad or command. Then, type the word help. The cd command (and many others) can be seen here. The cd command is common in use and structure in all systems.

# Changing Directories: pushd and popd

After you master the cd command, you need to learn to move around Unix using the pushd and popd commands. pushd <directory> will be entered if you want to specify the directory. With the popd command, however, you will not need to specify a directory name.

When changing between directories, these two commands allow you to make good use of the directory stack. The directory stack is a type of data storage that works as follows: Data is added to the top, creating the stack, and the most recently added “plate” of data is the first to be removed if requested, because it comes off the top of the stack. To describe this in terms of pushd and popd commands, data is pushed (pushd) onto the stack and popped (popd) off the stack when requested each command, making use of these commands quicker and more efficient than use of the cd command. The following examples will show you how to perform pushd and popd:

+   - pwd
- cd /priv/home/rob