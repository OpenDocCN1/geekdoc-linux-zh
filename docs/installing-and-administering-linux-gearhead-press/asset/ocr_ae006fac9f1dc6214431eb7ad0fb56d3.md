from the current session are saved, and then proceeding into the hidden file called .bash_history in our $HOME directory. Using Up or Down allows us to recall and re-execute, then, commands that we have executed previously.

When you back up enough to enter the hidden .bash_history file, your initial position in that file is at the bottom, or the most recent command before your last logout. You can specify the number of old commands that will be placed in the .bash_history file, so you can travel back a fair distance in your command history (we will discuss how to do that in Chapter 11, “Shell Variables and the User Environment”). But pressing the Up key once you reach the top of .bash_history, however, results in a shell error beep.

To summarize, the benefit of using Up and Down is that you can repeat procedures by recalling commands and then pressing Enter to re-execute. That can save you a lot of typing, especially with respect to complicated syntax. You can also perform sensitivity analyses by re-executing commands while changing options or arguments with each execution.

# # Invoking Text Editor Features at the Command Line

Linux also enables you to invoke, at the command line, the editing features from its various text editors. For example, if you type the following at the command line, Linux enables you to use some vi commands and keystrokes:

```
$ set -o vi<Enter>
```

To turn the features off, type

```
$ set +o vi<Enter>
```

The “invoking other editor features” facility can be handy for UNIX-based operating system users and administrators when they find themselves at different locations (especially at different keyboards). The feature can bring some predictability to command-line activities.

For example, invoking vi features might let you use the h, j, k, and l keys to emulate the left, down, up, and right arrow keys, respectively, to navigate the command line or to recall previous commands by tapping into the buffer and your .bash_history file.