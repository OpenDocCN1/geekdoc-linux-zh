# strings

The *strings* command outputs all text strings found inside binary programs. This can be useful to view the contents of files when you do not have a viewer program for a file’s format or for looking at the contents of a binary program (such as to search for help text). For example, try this to look at all strings inside the *pico* editor:

```
# strings /usr/bin/pico | less
```

# su

su enables a user to temporarily become another user. If a user ID is not given, the computer thinks you want to be either the *superuser* or *root*. In either case, a shell is spawned that makes you the new user, complete with that user ID, group ID, and any supplemental groups of that new user. If you are not root and the user has a password (and the user should!), *su* prompts for a password. *root* can become any user at any time without knowing passwords. Technically, the user just needs to have a user ID of *0* (which makes a user a *superuser*) to log on as anyone else without a password.

# swapon

swapon sets the swap area to the file or block device by path. *swapon* stops swapping to the file and is normally done during system boot.

# swapoff

swapoff is the command that stops swapping to a file or block device.

# tail

*tail* prints to standard output the last 10 lines of a given file. If no file is given, it reads from standard input. If more than one file is given, it prints a header consisting of the file’s name enclosed in left and right arrows (*==>* & *<=*) before the output of each file. The default value of 10 lines can be changed by placing a *-n#* in the command. The syntax for the command follows:

```
tail [-# of lines to see] [filename(s)]
```

# talk

The *talk* command is used to have a “visual” discussion with someone else over a terminal. The basic idea behind this visual discussion is that your input is copied to the other person’s terminal, and the other person’s input is copied to your terminal. Thus, both people involved in the discussion see the input from both themselves and the other person.