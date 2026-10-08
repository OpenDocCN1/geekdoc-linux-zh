+   - A path, as defined in UNIX, serves as a map to access any file on the system. An absolute path is one that always starts at the root level. A relative path is one that starts at your current location.

+   - You may customize your command prompt to display the current working directory name, the date, time, and several other items.

+   - The ls command displays the names of files and directories contained in a directory. The ls -l command and its options display all file information on the screen. This display is often called a long listing. The ls -a command shows hidden files.

+   - Wildcard characters can be used in a command, such as ls, and take the place of other characters in a file name. The * wildcard can take the place of any string of characters, and the ? wildcard can take the place of any single character.

+   - You can use the mkdir command to create a new directory as long as you own the parent directory. A file’s owner is the person who creates it and becomes the only one who controls access to it.

+   - You can use the chmod command to set permissions for files that you own. The permissions settings are rwx, which mean read, write, and execute, respectively. File permissions are set to control file access by three types of users: the owner, the group, and others. You must remember to change permission settings on any directories you own if you want others to access information in those directories. You use the execute permission (x) command to grant access to directories.

+   - You can use the cp command to copy a source file to a destination file. UNIX overwrites the destination file without warning unless you use the -i option. The dot notation (current directory) is a shorthand way to specify the destination in a cp command.

# COMMAND SUMMARY

| | Command | Purpose | Options covered in this chapter | | | | | cd | Change directories | | | | | chmod | Set file permissions for specified users | | | | | cp | Copy files from one directory to another | -i prevents overwriting of the destination file without warning | | | | | ls | Display directory's contents, including its files and subdirectories | -a lists the hidden files -l generates a long listing of the directory | | | | |