course of the previous sessions. To refresh your memory about what a command does, follow the instructions shown in the Description column of Table 8-1 to try out that command. For your convenience, I organized the commands in categories.

Table 8-1
Linux Commands You've Learned in Previous Sessions

| Command Name | Description |
|---|---|
| Getting Online Help | |
| man | Displays online help information. Type man 1s for help with the 1s command. |
| Making Commands Easier | |
| alias | Defines an abbreviation (shortcut) for a long command. Type alias alone to view all currently defined aliases. Type alias topdir='cd /' and then type topdir to change the directory to the root directory (/). |
| unalias | Deletes an abbreviation defined using alias. Type unalias topdir to undefine the topdir abbreviation. |
| Managing Files and Directories | |
| cd | Changes the current directory. Type cd /usr to change to the /usr directory. |
| chmod | Changes file permissions. Type chmod +x filename to make that file executable (replace filename with the name of an existing file). |
| cp | Copies files. Type cd to change the directory to your home directory. Then type cp /etc/X11/XF86Config to copy a file to your home directory. |
| ls | Displays the contents of a directory. Type ls -F to see the contents of the current directory. |
| mkdir | Creates a directory. Type cd to change to your home directory and then type mkdir temp to create a directory named temp. |
| mv | Renames file as well as moves a file from one directory to another. Type mv filename1 filename2 to change a file’s name (use an existing file’s name for filename1). |