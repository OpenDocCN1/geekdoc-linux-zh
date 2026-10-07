# ## Key Bindings

Like the pdks, tcsh provides the ability to change and add key bindings. The tcsh implementation of key bindings is more powerful than the way key bindings are done in pdks.

With tcsh you can bind to things other than the built-in editor commands. This means that you can bind a key to a UNIX command, for example. tcsh also enables you to bind vi editing commands, whereas pdks only allows the binding of emacs editing commands.

Key bindings can be very useful, especially if you're using a favorite editor other than emacs or vi. The basic syntax for defining key bindings is

```
bindkey [option] <instring or keyname> <outstring or command>
```

The options that bindkey supports are not discussed in this book. If you want to learn about the bindkey options, refer to the tcsh man page. The basic function of the bindkey command is to bind the key sequence contained in the first argument to the command contained in the second argument.

The following list gives some of the most useful editing commands that you can bind key sequences to, along with the default key binding for that command. You can list all the bindings that are defined in tcsh by typing the bindkey command without any arguments.

+   - beginning-of-line (^A): Moves the cursor to the beginning of the command line.
- backward-char (^B): Moves the cursor back one character.
- end-of-line (^E): Moves the cursor to the end of the command line.
- forward-char (^F): Moves the cursor forward one character.
- backward-delete-char (^H): Deletes the character to the left of the cursor.
- kill-line (^K): Deletes all of the characters to the right of the cursor.
- clear-screen (^L): Removes all of the text from the shell window.
- down-history (^N): Moves down one command in the history list.
- up-history (^P): Moves up one command in the history list.
- kill-whole-line (^U): Deletes all of the characters on the current line.

All of these commands are the same whether you're in emacs or vi insert mode. tcsh supports many more editing commands than are listed here. To see what these commands are, refer to the tcsh man page.