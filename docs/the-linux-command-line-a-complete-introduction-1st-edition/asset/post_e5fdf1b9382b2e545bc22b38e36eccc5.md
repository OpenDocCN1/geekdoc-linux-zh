
Here we see our list of directories. If our script were located in any of the directories in the list, our problem would be solved. Notice the first directory in the list, /home/me/bin. Most Linux distributions configure the PATH variable to contain a bin directory in the user’s home directory to allow users to execute their own programs. So if we create the bin directory and place our script within it, it should start to work like other programs:

```
[me@linuxbox ~]$ mkdir bin
[me@linuxbox ~]$ mv hello_world bin
[me@linuxbox ~]$ hello_world
Hello World!
```

If the PATH variable does not contain the directory, we can easily add it by including this line in our .bashrc file:

```
export PATH=~/bin:$PATH
```

After this change is made, it will take effect in each new terminal session. To apply the change to the current terminal session, we must have the shell reread the .bashrc file. This can be done by “sourcing” it:

```
[me@linuxbox ~]$ . .bashrc
```

The dot (.) command is a synonym for the source command, a shell builtin that reads a specified file of shell commands and treats it like input from the keyboard.

> Note: Ubuntu automatically adds the ~/bin directory to the PATH variable if the ~/bin directory exists when the user’s .bashrc file is executed. So, on Ubuntu systems, if we create the ~/bin directory and then log out and log in again, everything works.

## Good Locations for Scripts

The ~/bin directory is a good place to put scripts intended for personal use. If we write a script that everyone on a system is allowed to use, the traditional location is /usr/local/bin. Scripts intended for use by the system administrator are often located in /usr/local/sbin. In most cases, locally supplied software, whether scripts or compiled programs, should be placed in the /usr/local hierarchy and not in /bin or /usr/bin. These directories are specified by the Linux Filesystem Hierarchy Standard to contain only files supplied and maintained by the Linux distributor.

## More Formatting Tricks

One of the key goals of serious script writing is ease of maintenance; that is, the ease with which a script may be modified by its author or others to be adapted to changing needs. Making a script easy to read and understand is one way to facilitate easy maintenance.

## CONFIGURING VIM FOR SCRIPT WRITING

The vim text editor has many, many configuration settings. Several common options can facilitate script writing.

`:syntax on` turns on syntax highlighting. With this setting, different elements of shell syntax will be displayed in different colors when viewing a script. This is helpful for identifying certain kinds of programming errors. It looks cool, too. Note that for this feature to work, you must have a complete version of vim installed, and the file you are editing must have a shebang indicating the file is a shell script. If you have difficulty with `:syntax on`, try `:set syntax=sh` instead.

`:set hlsearch` turns on the option to highlight search results. Say we search for the word *echo*. With this option on, each instance of the word will be highlighted.

`:set tabstop=4` sets the number of columns occupied by a tab character. The default is eight columns. Setting the value to 4 (which is a common practice) allows long lines to fit more easily on the screen.

`:set autoindent` turns on the auto indent feature. This causes vim to indent a new line the same amount as the line just typed. This speeds up typing on many kinds of programming constructs. To stop indentation, type `CTRL-D`.

These changes can be made permanent by adding these commands (without the leading colon characters) to your `~/.vimrc` file.

## Final Note

In this first chapter about scripting, we have looked at how scripts are written and made to easily execute on our system. We also saw how we can use various formatting techniques to improve the readability (and thus, the maintainability) of our scripts. In future chapters, ease of maintenance will come up again and again as a central principle in good script writing.
