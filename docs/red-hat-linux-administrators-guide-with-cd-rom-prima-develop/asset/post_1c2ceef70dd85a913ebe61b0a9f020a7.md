
For example, rather than retyping the entire command to move to a new directory or the entire absolute path, you can simply press the up-arrow key until you find that same command entered earlier under that same shell. Once the correct command is displayed at the prompt, you press Enter to execute it again. This feature can save you much typing and guesswork.

The bash shell also remembers past keystrokes in between shell sessions. This means all commands I execute during one bash session are stored and then retrievable when I next log in at a bash shell. All commands under bash are stored in the user's home directory under the filename .bash_history. If you forget where a certain file is located, but remember having been there before or having previously issued the correct command, you can use any text editor and view the contents of the file. Any search command should quickly locate the line in question. Using Ctrl+R will also help find earlier commands. This makes switching between directories with long pathnames easy.

> **TIP**
> The cat command works also very well. This command prints out the contents of a file without invoking a text editor. Paging the cat command through the more and less commands will also help to navigate through a file's contents. Entering `cat <filename> less <filename>` is quicker and easier than using a text editor. You can also simply type `less <filename>` and scroll through the contents as well. The more option also works well. Less is more, as Linux users say.

## Completing Filenames

The bash shell also helps reduce repetitive typing in other ways. It has an option that allows you to complete file or directory names by simply pressing the Tab key. Rather than typing every filename to its completion, you need only type the first few letters of the file and then press Tab. The bash shell then attempts to complete the file or directory's name. If there is more than one file that has the same initial letters as you entered, bash signals an error with an audible beep and will attempt to complete the word. Two Tab strokes will display all the potential files that share those same beginning letters.

While in the `/usr/X11R6/lib/X11/fvwm2`, an obscure directory whose location I frequently forget, I wish to edit the file `FvwmConsole.pl`. Because this directory has over 30 files that all begin with Fvwm, I need to be specific as to which file I want to edit. The bash shell reduces the amount of typing that I need to do. I can then enter the name of the text editor in which I wish to open the file, type Fvw, then press the Tab key. The bash shell finishes the filename that begins with Fvwm, then signals that there are more choices. Pressing the Tab key again displays all the other possible files with the same initial letters. I continue typing FvwmCo and again press the Tab key. The bash shell again gives an audible alert that there are more choices available. Type in the next few characters and allow bash to complete the end of the file, press Enter, then open the file.

## Paths

Paths help list directories to which you have immediate access from the command line. When executing a file, you can either type its absolute path or the relative directory in which it is located. Verify first that the file's directory is accessible in your path and then simply enter the executable's name. The latter option is by far the better choice.

If `/usr/local/bin` is not in my path, I would have to enter `/usr/local/bin/runme` to start the program runme. However, if that pathname is in your path, from anywhere on the system you would need only enter runme to execute that program.

> **CAUTION**
> Make sure that the filename you are looking for is unique. As your shell's path goes through the directories, it will stop at the first match it encounters. Be sure to check the listing of your paths by typing `echo $PATH`.

Understanding how paths work and making them accessible is crucial to simplifying your own duties as a Linux administrator. Keep in mind the order your system uses to search the available paths. By placing often-used executables or scripts in a common and early path, you can access them more readily.

## Exporting Paths

Knowing the path to a file can be extremely useful, but when you cannot find a file, there remains a lot of hard drive to search. Linux needs to know where to look first when searching for a particular file. By setting up the correct paths at the beginning, you tell Linux where to look initially and thus save the system time and effort by enabling it to avoid futile searches in remote, obscure directories.

Like most other operating systems, Linux sets up some standard default search paths. These paths are defined in a couple of areas, either for global users or for individual users. When setting up global paths or when making a directory path that all users can quickly reference, you add the path to `/etc/profile`. When you are editing an individual user's path, the standard file to change under Red Hat is `.bash_profile` or the file specific to the default shell.

The standard practice for most administrators when installing a program such as Netscape on the system is to place the file somewhere accessible to all users. You will want to provide all users with fast and easy access. You can do so by placing the default install directory within their path.

For a program such as Netscape, you would add `/opt/netscape` to the path or create a link from the executable to the `/usr/local/bin` directory. Either way, users on the system can now find the Netscape executable. Now when the system searches for a particular file, it will look in this directory as well for any executables. Any user on the system could quickly find and execute the program Netscape, which would be located in this directory as well.

Here is an example `/etc/profile` file with additional entries to the default path, allowing all users to access both the Netscape and Star Office directories:

```
PATH="${PATH}:/usr/X11R6/bin:/opt/netscape:/usr/local/Office51/bin"
export PATH PS1 HOSTNAME HISTSIZE HISTFILESIZE USER LOGNAME MAIL INPUTRC
```

Here I have added the absolute paths to the directories containing the Netscape and Star Office executables, or `/opt/netscape` and `/usr/local/Office51/bin`. I also need to verify that I am exporting the variable names, such as PATH and PS1. After I add the new path, the shell needs to reread `/etc/profile` and update its path. You accomplish this by entering the following command:

```
source /etc/profile
```

The system then reads through the `/etc/profile` file once more and adds the additional directories to its default list of files to which it has immediate access.

## Locating Additional Files

The which command helps to locate files within the available paths. However, this command is only good for locating files found in exported paths. If the directory is not in your path, the system will be unable to find the file in question. Once your shell has reread the contents of `/etc/profile`, you should be able to see the newly exported files. Had I executed a which command on Netscape before adding it to `/etc/profile`, it would not have been able to inform me that the executable is located in `/opt/netscape/netscape`.

To see all the directories currently read by bash and that are in the current path, enter `echo $PATH`. Do not forget the dollar sign before PATH or forget to type the command in all capital letters. PATH is a variable and as such has several unique features. If you type it without the dollar sign, then the word PATH will be printed to the screen.

## Temporarily Changing Your $PATH

To add more directories to your path, at least temporarily, you would issue the following command:

```
export PATH="$PATH:/usr/local/bin:/sbin"
```

For the duration of the session that you are logged in, you will be able to see not only the executable files found in your previously defined $PATH, but also the binaries located in `/usr/local/bin` and `/sbin`. If you are trying to keep the system secure and limit access to certain files, this feature can be useful for those instances where typing the entire pathname is long and tedious. By combining the export feature with bash's history file, you can potentially cut the amount of required typing in half.

If you want to make these paths a permanent feature for your own use and not allow others access to the same directories, customizing the `.bash_profile` file will produce the same results, except only on a user-specific basis.

This local file sets the paths only for needed files, however. To start up files automatically upon login or to execute them without manually calling them, you would need to add their paths, or just their binary name if their path is already listed, to the `.bashrc` file. It is here that files start up automatically. It can also be
