In the last chapter, you saw the Bourne Again Shell (bash) in some detail. Not everyone wants to use the bash shell, so several other shells are included with most Linux systems. One of them is **pdksh**, a variation on the Korn shell. We'll also look at how you can customize your copy of **pdksh**, as well as several of the important commands and variables used by the shell.

# # The Public Domain Korn Shell (pdksh)

The Korn shell, written by David Korn, was the third mainstream shell written for UNIX (after the Bourne shell and the C shell). Because of this, it incorporates many of the features of the Bourne and C shells together. The Korn shell is not usually distributed with all UNIX versions, so many users don't get to work with it. The Korn shell is important to UNIX users, though, because it builds a lot of the important new features of the C shell into the much older Bourne shell, while remaining completely compatible with sh. Because of the Korn shell's popularity among UNIX users, a version was developed for Linux called the Public Domain Korn Shell, or **pdksh**.

The current version of the Public Domain Korn Shell does not support all of the features that exist in the commercial version of the Korn shell. It does support most of the main features, however, and adds a few new features of its own.

# ## Command-Line Completion

Often, when you are entering commands at the command line, the complete text of the command is not necessary in order for **pdksh** to be able to determine what you want to do. Command-line completion enables you to type in a partial command, and then by entering a key sequence, tell **pdksh** to try to finish the command for you.

**pdksh** does not default to allow the user to perform command-line completion. You must enter a command to tell **pdksh** that you want to be able to use command-line completion. In order to enable command-line completion, enter one of the following commands:

```
```
set  -O emacs
set  -O vi
```
```

This causes **pdksh** to accept command editing that is similar to *emacs* or *vi*. Choose the editor that you are most familiar with, and use the basic editor commands for command-line editing.