# # Basic Filesystem Commands

There are some basic filesystem commands that will allow you to modify files and display information within the Linux filesystem.

| Command | Enables You To |
| :------- | :------------- |
| cd | Traverse the directory structure. There are several ways to specify the path name of the directory you need to switch to. The syntax of the cd command is cd *{Absolute or Relative path}*.<br><br> | 
| ls | List the files in the current working directory. This command displays only the file name when the command is run without any options. However, it can be used to list information such as size, file type, and permissions by running the command with the respective options. The syntax of this command is ls `[command options]` `{Absolute or Relative path of the directory}`.<br><br> | 
| mv | Move files and directories from one directory to another, or renames a file or directory. The syntax of this command is mv `{Absolute or Relative path}/`{file or directory name}` ({Absolute or Relative path}/`{new file or directory name} ).<br><br> | 
| cp | Copy a file. The syntax of this command is cp `[command options]` `{Absolute or Relative path of the file or directory to be copied}/` {file or directory name} `{Absolute or Relative path of the destination}`.<br><br> | 
| rm | Delete files or directories. The syntax of this command is rm `[command options]` `{Absolute or Relative path of file or directory}/` {file or directory name} ).<br><br> | 
| touch | Change the time of access or modification time of a file to the current time. In addition, the touch command creates an empty file if the file name specified as an argument does not exist. The syntax of this command is touch `{file name}`.<br><br> | 
| mkdir | Create a directory. The syntax of this command is mkdir `{directory name}`.<br><br> | 
| rmdir | Delete directories. The syntax of this command is rmdir `{directory name}`.<br><br> | 
| pushd | Add a directory at the top of a stack of directories or rotate a stack of directories. The syntax of this command is pushd `[option]` {directory name} ).<br><br> | 
| popd | Remove entries from a stack of directories. When no option is specified, it removes the top directory from the stack. The syntax of this command is pushd `[option]`.<br><br> |

# ## The -v Option

-v is a command option that can be used with the basic file management commands. This option explains the running of the command to produce the desired output, in a verbose manner.