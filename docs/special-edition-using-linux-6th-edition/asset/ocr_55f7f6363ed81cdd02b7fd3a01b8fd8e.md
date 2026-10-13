The commands are categorized into one of the following four areas:

+   - Working with directories
+   - Working with files
+   - Networking utilities
+   - System utilities

# WORKING WITH DIRECTORIES

| Command | Syntax (Example) | Description |
|---|---|---|
| cd | `cd [path]` | Changes directory to the specified path. |
|  | `cd ..` | Changes to the parent directory of the current directory. |
|  | `cd -` | Changes to the previous working directory, prior to the last `cd` command. |
|  | `cd` | Changes to the home directory of the current login ID. |
|  | `cd ~` | Changes to the home directory of the current login ID. |
| dir |  | See the `ls` command. |
| ls | `ls [path]` | Lists the contents of a directory. |
|  | `ls -l (11)` | Lists the files in long format, displaying all file attributes. |
|  | `ls -a` | Lists all files (including hidden files, sometimes referred to as dot files). |
| mkdir | `mkdir <directory>` | Makes a new directory. |
| pwd |  | Displays present working directory. |
| rmdir | `rmdir <directory>` | Removes a directory. |

# WORKING WITH FILES

| Command | Syntax (Example) | Description |
|---|---|---|
| cat | `cat <file>` | Most commonly used to display the contents of a file. Derived from the word “concatenate,” which it also does. |
| chattr | `chattr <option> file` | Changes the ext2 attribute of a file. Some options available only to UID 0. |
| cp | `cp <source> <dest>` | Copies a file. |
| dd | `dd if=input of=output` | Most commonly used to convert a file. Can be used to copy image files from one device to another device or file. |
| file | `file <file>` | Determines the type of a given file. |
| grep | `grep <pattern> <file>` | Searches a file or files for a specified pattern. |