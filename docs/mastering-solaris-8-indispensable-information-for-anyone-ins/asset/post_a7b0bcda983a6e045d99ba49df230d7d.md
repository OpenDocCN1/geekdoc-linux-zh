
files, and those files are read anytime the shell initializes. In multiuser environments, a system will store specific startup files for each username that logs in to the system. Solaris shells use a template system for creating startup resource files. There is usually a systemwide shell resource file for each of the shells that are copied into the home directory. An administrator can modify the template resource file as well as any user's resource file. A user can modify the resource files in their own home directories by adding shell commands to the files. Thus, a user has control over the nature of their environment. The standard Solaris distribution comes with three shells—Bourne, Korn, and C shells—although you can add other shells to the system if you like. By default, the standard shell is the Bourne shell. The Bourne and Korn shells use the `/etc/profile` file as a startup file, and the C shell uses the `.cshrc` and `.login` files. The first time you log in to the C shell, it reads the `.login` file, and any subsequent times you start up a new C shell, it reads the `.cshrc` file.

> **NOTE** The Bourne shell is described in Chapter 18, the Korn shell in Chapter 19, and the C shell in Chapter 20.

The graphical user interfaces such as the Common Desktop Environment (CDE) and OpenWindows are full-featured window managers that offer desktop features. Those environments run on top of X Window sessions. There are many configuration and startup files that set up your environment for these different systems, and those files are described at the beginning of Chapter 7, "The Solaris Desktop." Typically, you use desktop controls in the form of icons that call configuration programs or utilities to change the resource file settings in a window manager. It is possible to modify X Window resource file settings directly, as is described in "Customizing the Desktop" and the sections on the X Window System toward the end of Chapter 7.

## Creating Directories and Files

You can create a directory from the command line using the `mkdir` (make directory) command or in the File Manager by using the New Folder command on the File menu. The command-line option is somewhat more powerful, allowing you to create a directory anywhere in the file system with options that even help create a path or set the access privileges for that directory.

The syntax for the `mkdir` command is as follows:

```
mkdir options <pathname>/<directoryname list>
```

There are really only two significant options that you might want to use with the `mkdir` command:

- The `-m`, or mode, option sets the access privileges of the directory using either symbolic or octal nomenclature (these two systems are described in the section “Modifying Access Rights” earlier in this chapter).
- The `-p`, or parent, option will create any directory name in the path you specified if it doesn’t already exist.

For example, if you specify a list of directory names without paths, then `mkdir` creates those directories in your current directory. If you give the command `mkdir -p /usr/docs/letters/l2001letters` from within the docs directory and the docs directory doesn’t already have a `/usr/docs/letters` subdirectory, then this command creates the `/usr/docs/letters` subdirectory and places the `l2001letters` directory into that new subdirectory. This is a pretty convenient option to use if you can remember it.

The second option (-m) that allows you to set the access privileges of a new directory is illustrated by the command `mkdir -m ugo=rwx-w 12001letters`, which creates the new directory and gives the user, group, and others access rights to read and execute but not to write. In octal format, a similar command, `mkdir -m 600 12001letters`, creates the directory and sets the user’s access permissions to read (4) plus write (2).

In the CDE, to use the File Manager window to create a new folder, follow these steps:

1. Select the New Folder command from the File menu. The New Folder dialog box, shown in the following graphic, appears.

![](img/256e02a6afce528d264a8d911fa0ff20_173_0.png)

2. To have Solaris create the new folder at the location you specify, enter the path name and folder name (in the format `<pathname>/<foldername>`) into the New Folder Name text box.
3. Click the Apply button to create the folder or the OK button to create the folder and close the dialog box.

The New Folder dialog box is not a command-line processor; it doesn’t support the `-p` or `-m` options, nor will it accept a folder name list.

The File Manager window offers you an opportunity to create new data files by selecting the New File command from the File menu. The following graphic shows you the New File dialog box. If you enter a name without a suffix in the New File Name text box, you create a data file. If you add a suffix, like .tif, to the filename, Solaris creates a file of that type.

![](img/256e02a6afce528d264a8d911fa0ff20_174_0.png)

The copy command (see “Copying and Moving Directories and Files”) is yet another way of creating new directories (as duplicates) from old ones. Solaris supports both the `cp` (copy) command-line expression and a Copy command in the CDE File Manager. The `cp` command creates a duplicate of any directory that you have write privileges to and copies all of the contents of that directory as well. The `cp` command works with both files and directories (or folders).

Here is the syntax for the `cp` (copy) command appropriate to creating directories:

```
cp <options> <source_directoryname list> <pathname>/<target_directoryname>
```

It can take a list of directories and copy them and their contents to another location. Use the `-r` flag for a recursive copy or the `cp` command will respond "cp: xx is a directory" and will not perform the copy.

From a File Manager window, you can copy selected folders using the Copy To command (Ctrl+C) on the Selected menu. In the resulting Copy To dialog box, enter the name of the copied folder into the Name for Copy text box and the path into the Destination text box. The Copy To dialog box creates a folder in the location you specify. Chapter 7 describes using the File Manager to copy, move, and rename files and folders in more detail.

## Navigating Directories

You often need to move the focus of your actions to a directory to act on it and the files it contains. The command that changes your focus to a new working directory without modifying the directory is the `cd` (change directory) command. The `cd` command is a Solaris utility, but it is also one of the built-in shell commands for each of the three main Solaris shells (Korn, Bourne, and C shells). The syntax for this very simple but important command is as follows:

```
cd <pathname>/<directoryname>
```

Once you use this command, your actions affect files and subdirectories in your new working directory. If you have forgotten or don’t know where in the file system you are, then use the `pwd` (print working directory) command to have Solaris return the path name and directory name `<pathname>/<directoryname>` of the current directory.

You can use the parent pointer to move up one directory in the file system, as follows:

```
# pwd
/usr/docs/letters/12/letters
# cd ..
# pwd
/usr/docs/letters
```

The following command moves you to the root folder:

```
# cd /
# pwd
/
```

If you are familiar with MS-DOS, then you know that it sets as a default a prompt that shows the path of the current working directory. If you want to see this kind of prompt in any of the Solaris shells, you can modify your shell prompt by including the following `set` command (shown for the Korn shell, the first is for root and the second is for users):

```
PS1='# 'pwd'
PS1='$ 'pwd'
```

For the C shell, that `set` command would be as follows:

```
set prompt=`pwd' %'
```

Now if you log in to the `/usr/home/barries` directory at startup, as you might if your username were barriers, then what you see for a prompt is the following:

```
/usr/home/barries #
```

For the Korn shell, the environmental variables are set in the `/etc/profile` or the `~/.profile` files, and the C shell uses the `~/.cshrc` and `~/.login` files. You can also use the `home` environmental variable command in those files to set the location of the home directory.
