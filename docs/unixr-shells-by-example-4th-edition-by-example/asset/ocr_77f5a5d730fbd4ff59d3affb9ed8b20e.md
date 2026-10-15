# The .cshrc and .tcshrc Files.

The .cshrc file contains C shell variable settings and is executed when you log in and every time a csh subshell is started. Likewise, the .tcshrc file contains TC shell variable settings and is executed when you log in and every time a tcsh subshell is started. These files share similar settings. For example, aliases and history are normally set here.

# EXAMPLE 9.1

```
(The .cshrc File)
1  if ($?prompt) then
2     set prompt = "\! stardust >"
3     set history = 32
4     set savehist = 5
5     set noclobber
6     set filec ignore = (.o)
7     set cdpath = (/home/jody/ellie/bin /usr/local/bin /usr/bin)
8     set ignoreeof
9     alias m more
     alias cd 'cd \!*;set prompt = "!\! <cwd> "'
endif
```

# EXPLANATION

+   1 If the prompt has been set ($?prompt), the shell is running interactively; that is, it is not running in a script.
+   2 The primary prompt is set to the number of the current history event, the name stardust, and a > character. This will change the % prompt, the default.
+   3 The history variable is set to 32. This controls the number of history events that will appear on the screen. The last 32 commands you entered will be displayed when you type history (see "Command-Line History" on page 413).
+   4 Normally, when you log out, the history list is cleared. The savehist variable allows you to save a specified number of commands from the end of the history list. In this example, the last 5 commands will be saved in a file in your home directory, the .history file, so that when you log in again, the shell can check to see if that file exists and put the history lines saved at the top of the new history list.
+   5 The noclobber variable is set to protect the user from inadvertently removing files when using redirection. For example, sort myfile > myfile will destroy myfile. With noclobber set, the message file exists will appear on the screen.
+   6 The filec variable is used for filename completion so that you only need to type the first number of significant characters in a filename, press the Esc key, and the shell will complete the rest of the filename. By pressing ^D (Ctrl-D) when typing in the filename, the C shell will display a list of files that match that string. The fignore variable allows you to exclude files that you do not want affected by filename completion. In this case, all the .o filenames (object files) will not be affected by filec, even though filec is set (see "Filename Completion: The filec Variable" on page 431).