
## The diff3 Command (Comparing and Merging)

| Option | Topic | Comments |
| :--- | :--- | :--- |
| -a | Compares binary files | Binary files are treated as text files. |
| -m | Displays merged differences on the screen. | Output can also be redirected to a file. |
| --merge | | |

# 9 Working with Directories, Files, and Links

In general, all information on your Linux system is stored in files. Although you often use separate commands to manipulate directories and links, both are basically specialized types of files.

This chapter covers the basic tasks, such as creating, selecting, copying and deleting directories and files. It also explains how to view and create links, and how to change file attributes.

> **Note**
>
> You cannot manipulate files unless you have permission to do so. This limitation is one of the major differences between Linux and many popular operating systems. See “Changing Permissions,” page 227.

On the desktop, you can use the GNOME Midnight Commander for the most common file functions.

However, for a complete set of options, you must use the command line. In fact, a few tasks, such as merging or splitting files can only be done from the command line.

### Creating New Files From the Desktop

1. Open a program, such as a text editor.
2. From the menu, select File > Save. The Save dialogue window opens.
3. Use the directory tree to select a directory.
4. Enter the file name. Then select the Save button.

### Creating New Files From the Command Line

Type: `touch FILES`.
If no path is entered, then the files are created in the present directory.

### Creating New Directories From the Desktop

1. Open the GNOME Midnight Commander. Do one of the following:
   - From the workspace, select the Home directory launcher.
   - From the menu, select Programs > File Manager.
2. Right-click on the directory pane. A pop-up menu displays.
3. From the menu, select New Directory. The Create a new directory window opens.

![](img/e36b94f8548b09d00212238f073b11d9_205_0.png)

4. Enter a name for the new directory. Select the **OK** button when you are finished.

> **Note**
> You may need to select **Edit > Rescan directory** before the new directory displays in the **GNOME Midnight Commander**.

### Creating New Directories From the Command Line

Type: `mkdir OPTIONS DIRECTORY`.

#### The `mkdir` Command (Make Directory)

| Option | Action | Comment |
| :--- | :--- | :--- |
| -m MODE | Sets permissions for new directory in absolute mode. | See “Changing Permissions in Absolute Mode,” page 234. |
| -p | Creates any parent directories if they do not already exist. | |
| --parents | | |

### Selecting Files From the Desktop

1. Open the **GNOME Midnight Commander**. Do one of the following:
   - From the workspace, select the **Home directory** launcher.
   - From the menu, select **Programs > File Manager**.

In both cases, the GNOME Midnight Commander opens, displaying your home directory.

![](img/e36b94f8548b09d00212238f073b11d9_207_0.png)

2. Select a file. Do one of the following:
   - Left-click on an icon with the mouse. If you want to select another file, left-click on its icon while pressing the Ctrl key.
   - Hold down the left mouse button, and drag the cursor across the files you want to select. A box displays around the files as they are selected.

![](img/e36b94f8548b09d00212238f073b11d9_207_1.png)

   - Select an item from the menu:
     - Edit → Select All: Selects all files in the current window.
     - Edit > Select Files: Selects files that match the regular expression that you enter in a dialogue.
     - Edit > Invert Selection: Deselects files that are currently selected and selects files that are currently deselected.

No matter how you choose files, their icon text is highlighted when selected.

### Selecting Multiple Files From the Command Line

Either:
- Enter file names after a command. Put a space between them.
- Or use metacharacters in regular expressions. For example, "*.jpg" selects all files in the directory with a .jpg extension.

See “Using Metacharacters or Wild Cards,” page 118.

### Copying Files From the Desktop

1. Open the GNOME Midnight Commander. Do one of the following:
   - From the workspace, select the Home directory launcher.
   - From the menu, select Programs > File Manager.

2. Select the files to copy. See “Selecting Files From the Desktop,” page 205.

3. Right-click on one of the selected files. A pop-up menu displays.

4. Select Copy from the pop-up menu. The Copy window displays.

![](img/e36b94f8548b09d00212238f073b11d9_209_0.png)

5. Enter the folder to copy the files to. You can type the folder's path or select it using the Browse button.

6. If you wish, select Copy options from the Advanced tab.

The Advanced options are:
- Preserve Symlinks: If a link is copied, it points to the original file.
- Follow links: The original file is copied, instead of the link. The original file is probably larger than the link.
- Preserve file attributes: Information from the original is transferred to the copy. Permissions are transferred even if this option is not selected.
- Recursively copy subdirectories: If a directory is being copied, then all sub-directories in it are also copied.

By default, only Preserve file attributes is selected.

7. Select the OK button to copy the file.

> **Note**
>
> If you cannot copy, then you do not have write permission. See “Changing Permissions,” page 227.

You can also drag selected files with the left mouse button to any folder in any open Midnight Commander window.

### Copying From the Command Line

Type: `cp OPTIONS SOURCE TARGET`.

#### The `cp` Command (Copy)

| Option | Action | Comments |
| :--- | :--- | :--- |
| -a, --archive | Gives target files the same attributes as the source files. | |
| -b, --backup | Backs up files that will be overwritten. | |
| -f, --force | Overwrites any existing files with the copy. | No confirmation is asked. Consider using with -i or -b to avoid overwriting files by accident. |
| -i, --interactive | Asks for confirmation before overwriting any files. | |
| -p | Includes the original file's attributes. | Attributes include the owner, group, permissions and dates. |
| --preserve | | |
| -P | Copies parent directories to sub-directories of the target directory. | |
| --parents | | |
| -r, -R | Copies sub-directories and their contents. | |
| --recursive | | |
| -s | Makes the target a symbolic link to the source file, instead of a copy. | See “Working With Symbolic Links,” page 218. |
| --symbolic-link | | |
| -u | Copies only files whose date are the same or newer than similarly named ones in the target directory. | |
| --update | | |
| -v | Displays file names as they are copied. | |
| --verbose | | |

### Moving Files From the Desktop

1. Open the GNOME Midnight Commander. Do one of the following:
   - From the workspace, select the Home directory launcher.
   - From the menu, select Programs > File Manager.

2. Select the files to move. See “Selecting Files From the Desktop,” page 205.

> **Warning**
> Paths, aliases and other features may be affected by moving a file.

3. Right-click on one of the selected files. A pop-up menu displays.

4. Select Move from the pop-up menu. The Move window opens.

![](img/e36b94f8548b09d00212238f073b11d9_212_0.png)

5. Select the folder to move the files to. You can enter the folder or select it using the Browse button.

6. If you wish, select Preserve symlinks from the Advanced tab. With this option, symbolic links are automatically updated.

7. Select the OK button to move the file.

> **Note**
> If you cannot move a file, then you do not have write permission in the target directory. See “Changing Permissions,” page 227.
