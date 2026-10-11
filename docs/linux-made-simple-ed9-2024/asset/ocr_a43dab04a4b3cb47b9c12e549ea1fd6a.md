# # Terminal: Work with files

Time to turn our attention to navigating your file system and manipulating files and folders from the beloved Terminal.

Previously we introduced you to the basics of using the Terminal. We opened by revealing it works in the same way as your Linux shell; how commands are structured (utility command -option); plus gave you the tools to manage software packages and get further help. This time, we’re going to look at how you can navigate your file system, work with files and folders and learn some more time-saving shortcuts in the bargaain.

![](bbox=[0.56, 0.34, 0.88, 0.48])

> > Make good use of `/` and `\` characters when folder paths contain spaces and other special characters.

When you open a new Terminal window, the command prompt automatically places you in your own personal **home** folder. You can verify this using the `ls` command, which lists the contents of the current folder. The default Terminal application displays folder names in blue, and filenames in white, helping you differentiate between them. The `ls` command can be used in other ways too. Start by typing `ls/a` to display all files, including those that begin with a period mark (.), which are normally hidden from view. Then try `ls/a -recursive`, the `-recursive` option basically means that the contents of sub-folders are also displayed. If you want more detail about the folder’s contents – permissions settings, user and group owners, plus file size (in bytes) and date last modified, use `ls/l/`. If you’d prefer to list file sizes in kilobytes, megabytes or even gigabytes depending on their size, add the `ls/h` option – so use `ls/ah` instead. There are many more options for `ls/` and you can use the `ls/-help` option to list them all.

The folder begins with a capittal letter – as your personal **Documents** folder does, eg – you’ll get an error about the folder not existing if you type it all in lower case, eg, `cd/documents`. You can also move down several levels at once using the following syntax: `cd/subfolder/subfolder2/`. To move back up to the previous level, use `cd/..`, you can also use the `cd/../` character to move up multiple levels at once, eg, `cd/../../` moves up two levels.

So that if you want to go somewhere completely different? Use `cd//` to place yourself in the root directory, or navigate anywhere on your system by entering the exact path, including that preceding `/` character to indicate you’re navigating from the top level, eg `cd/media/username`.

The `~` character works in a similar way to `/`, except this places you in your home directory. So typing `cd/~/Documents` is the same as typing `cd/home/username/`

Navigating your file system is done using the `cd` command – to move down one level to a sub-folder that’s inside the current directory use `cd/<subfolder>`, replacing `<subfolder>` with the name of the folder you wish to access. Remember that folder and filenames are case sensitive, so if

# ## Speedier navigation

In last part we revealed some handy keyboard shortcuts to help you enter commands more quickly, but the following keys will help you navigate the Terminal itself more efficiently.

+   - `Home`/`End` Press these to jump to the beginning or end of the current line.
+   - `Ctrl`+left/right cursor Move quickly

between arguments.

+   - `Ctrl`+`k` Clear the entire line to start again.
+   - `Ctrl`+`l` Delete everything from the cursor’s position onwards.
+   - `Ctrl`+`w` Delete the word before the cursor.

Accidentally omitted `sudo` from your command? Just type `sudo !!` and hit Enter to repeat the last command with `sudo` applied to it. And if you make a typo when entering a command, instead of retyping the entire command again, just use the following syntax to correct the mistyped word (in the following example, `plogi` was originally mistyped as `dkpg`):

```
```bash
$dkpg/!dpkg
```
```