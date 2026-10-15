# Using Completion in the zsh Shell

The zsh shell also offers completion but with added twists over the bash shell for the power user. Basically, though, you can type just part of a command, press Tab and have the Z-shell complete the command for you (Code Listing 3.10).

# To use completion in the zsh shell:

+   1. ls -l
+   Use ls -l to list the files in your current directory.
+   
+   2. cd pub Tab
+   Type in a partial command, and then press Tab to complete the command. In this example, we typed the cd command and part of the public_html directory (truncated to pub in the example), and then pressed the Tab key to complete it (see Code Listing 3.10).

# Tips

+   - In the Z-shell, command completion works even if multiple files might match the partial command that you type. For example, if you type cd pu (for public_html) and there's another subdirectory called puppy, then use Tab to complete the name, the shell will show you the options (public_html and puppy), then cycle through the options as you continue hitting Tab.
+   - You can use command completion to complete commands, directory names within commands, and nearly anything else you might enter.
+   - The Z-shell is smart enough to show you only the subdirectories you could change. bash, on the other hand, would show you files and directories, and beep at you—not as helpful, for sure.

```
$ ls
Complete    NewProject   bogus2
+ ftp        puppy
Completed   News         dead.letter
+ mail       temp
Mail        access       files
+ public_html           testme
$ cd public_html/
$
```

Code Listing 3.10 In this example, we typed only the ls command followed by cd pub and pressed the Tab key; zsh completed the command for us.