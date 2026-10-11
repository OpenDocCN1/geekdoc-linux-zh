The interpreter who reads the commands from the user is called shell; the most popular and default in many distributions is called bash. Running a command in a Linux system has five important elements to have into consideration:

+   **The command to be executed**: This can be a system command (for example, mkdir to create a directory), an internal function from the Linux terminal (for example, alias to create command shortcut) or can be a user application (such as firefox). The command can be specified in three different options:

+   Using the name of the command without indicating where it is located. The system has configured some directories where to find the command specified, and introducing the command will go in order through the commands to check if the command is available.

+   Using the full path where the command is situated, no matter the directory where currently the user is located, for example: /usr/bin/mkdir.

+   Using a relative path from the directory where the user is located, for example: ../bin/firefox. In this example, the command firefox is located in a subdirectory called bin in the top-level directory where the user is located:

+   If the user is located in /home/agonzalez/Documents/ running the command previously indicated, it will execute /home/agonzalez/bin/firefox. The two dots “..” indicates the top-level directory.

+   The special character “~” indicates the home directory for the user. If the home directory is, for example, /home/agonzalez/, then indicating ~/bin/firefox will be expanded to /home/agonzalez/bin/firefox.

+   **The options for the command**: This can be one or more options if it is needed to change the command behavior. Some options can be required. The command ls to list the content of the current directory will show the name of files and directories, using the option -l (ls -l)