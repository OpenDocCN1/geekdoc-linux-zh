
## The Linux Directory Structure

| Directory | What's In It |
| :--- | :--- |
| `/etc` | Most of the system's configuration files. Including `/etc/X11` for the X Window system and `/etc/opt` for third party applications. |
| `/floppy` | The usual mount point for the first floppy drive. If the system has a second floppy drive, its mount point is usually `/floppy2`. |
| `/home` | Home directories for all regular users. The root user's home directory is `/root`. |
| | Subdirectories of `/home` are named for the user name of each account. Personal configuration files that start with a `.` (a period) are in each home directory. |
| `/initrd` | Files for Linux's RAM disk. |
| `/lib` | Programming libraries needed to start the system and run basic commands. |
| | Look for other lib directories scattered throughout the system. |
| `/lost+found` | Files recovered when a check is run on a damaged file system. |
| `/mnt` | A folder for other mount points, usually other partitions not used directly by Linux, including those for other operating systems. |
| `/proc` | Process and system information. Be extremely careful of changes to /proc while you are logged in as the root user, because they can easily bring the system down. |
| `/root` | The home directory for the root user. |
| | Home directories for other users are generally sub-directories of /home. |
| `/sbin` | System binary files. Some of these are usable-only by the root user. |
| | Other executables are in /bin. |
| `/usr` | Programs and system files that are shared by all users. A common location for free software or for third-party software. Important sub-directories include /usr/local and /usr/share. |
| `/var` | Data files whose content changes frequently, such as caches, spools, log files and user mailbox files. |
| `/var/lock` | Lock files that prevent another user from opening or saving particular files. |
| `/var/log` | Log files for different programs. These logs are invaluable for solving problems. |

## Understanding Absolute and Relative File Paths

A file path is a list of the directories above the file, ending with the file name.

Linux uses two types of paths: absolute and relative paths:

- An absolute path always starts with the root directory.
    - For example, the absolute path to a file in a sub-directory in a user's home directory might be `/home/khcong/10100/january.txt`.
    - This path can take a long time to type, but is completely clear.
- A relative path starts in your present working directory.
    - For example, if you were in the `/home/khcong` directory, the relative path to a file in a sub-directory might be `10100/january.txt`.
    - You can find your present working directory by using the `pwd` ("present working directory") command.

In addition, `/` indicates the present working directory when you are using the command line.

## Searching from the Desktop

You can search for files or text from the desktop using:

- The GNOME search tool (gsearchtool): A graphical interface for the find and locate commands that includes the most common options for the commands.
- The GNOME Midnight Commander: Useful for simple searches.
- If you want a more elaborate search, see “Searching From the Command Line,” page 182.

### Using the find Command From the Desktop

The find command is a tool for locating files. It can also do basic searches using strings and regular expressions.

1. At a command line, type: gsearchtool. The GNOME search tool opens, with the Full find (find) tab selected.

![](img/e36b94f8548b09d00212238f073b11d9_177_0.png)

2. Enter the directory in which to start the search.
    - You can type the directory, choose it from the drop-down list of recent choices, or use the browse button to make a selection.

3. Choose the options to use from the drop-down list beside the Add button. These options correspond to the most common ones in the find command.

![](img/e36b94f8548b09d00212238f073b11d9_178_0.png)

The default choice is the File name.

Select the option. When it displays, select the Add button to make it part of your search.

You can disable an option temporarily by de-selecting the Enable button beside it or remove it from the display by selecting the Remove button.

4. When you have chosen the options to use, enter any information needed to use each option.

5. If you want, select the Show Command button to see what the command would look like at the command line.

6. Select the Start button to search. Search results display in a separate window. This window stays open so that the results of other searches can be added to it.

![](img/e36b94f8548b09d00212238f073b11d9_179_0.png)

7. From the Search Results window, you can:
    - Select a result to open the file in gedit.
    - Clear the window of results.
    - Save the results to a file.

### Using the locate Command From the Desktop

The locate command searches a database of file names and prints results that match the string that is entered for a command.

1. At a command line, type: locate. The GNOME search tool opens, with the Full find (find) tab selected.

2. Select the Quick Find (locate) tab.

![](img/e36b94f8548b09d00212238f073b11d9_180_0.png)

3. Enter a string, with or without metacharacters.

4. Select the Start button to search. Search results display in a separate window. This window stays open so that the results of other searches can be added to it.

![](img/e36b94f8548b09d00212238f073b11d9_180_1.png)

5. From the Search Results window, you can:
    - Select a result to open the file in gedit.
    - Clear the window of results.
    - Save the results to a file.

### Searching From the GNOME Midnight Commander

1. Open the GNOME Midnight Commander. Do one of the following:
    - From the workspace, select the Home directory launcher.
    - From the menu, select Programs > File Manager.

In both cases, the GNOME Midnight Commander opens, displaying your home directory.

![](img/e36b94f8548b09d00212238f073b11d9_181_0.png)

2. From the GNOME Midnight Commander menu, select Commands > Find File. The Find File window displays.

![](img/e36b94f8548b09d00212238f073b11d9_181_1.png)

3. In the Start at field, type the directory from which to start the search. The default is the current directory.

4. In the Filename field, type the file name to search for. You can use wildcards.

5. In the Content field, type a text string to search for. This field is optional.

6. Start the search. Select the OK button.

The search results display in a separate window: They may take some time to display.

![](img/e36b94f8548b09d00212238f073b11d9_182_0.png)

### Note

You can only search for results in directories in which you have read permission.

Using the buttons in the results window, you can:

- Select a result and change to its directory.
- Start a new search.
- Close the search tool.

## Searching From the Command Line

The Linux command line includes many tools for locating files or information in them. These tools can be divided into two main categories:

- File-Locating Tool: `find`, `locate`.
- Text-Locating Tools: `grep`, `egrep`, and `fgrep`.

Some of these commands, including `grep`, `egrep` and `find` can use variable text patterns (metacharacters or regular expressions) to extend their search abilities. See "Using Metacharacters or Wild Cards," page 118.

## Searching for Files: Using the find Command

The basic tool for finding files is `find`. The `find` command is useful for locating files by their attributes or by their position in the directory tree.

You can search by a wide variety of criteria, including:

- When the file was last accessed.
- When the file was last changed.
- The file's owner or the owner's group.
- A text string, including one that uses metacharacters. see "Using Metacharacters or Wild Cards," page 118.
- The type of file.
- The file's age relative to another file.
- The file's permissions.

Usually, `find` starts with the current directory, then searches its sub-directories. However, you can specify the starting directory.

You can also specify how many levels of sub-directories down to search.
