The two move (mv) commands, the first moves the file abc to the same directory (essentially renaming it), the second moves the file abc to your home directory (-). The first copy (cp) copies abc to the file def, whereas the second copies abc to your home directory (-). The first remove (rm) deletes the abc file; the second removes all the files in the current directory (except those that start with a dot).

> CAUTION: Be sure to use the * and other characters wisely, because you might match (and therefore remove) files you don't match. There is no undelete on Linux.

> NOTE: For the root user, mv, cp, and rm commands are aliased to run with the -i option. This causes a prompt to appear asking you to confirm copy and remove, one file at a time. For moves, -i option will prompt you if the move would overwrite a file, but you still unintentionally move a file, be careful. This is done to prevent the root user from messing up a large group of files by mistake. To get around an alias, use the full path to the command (for example, `/bin/rm -rf /tmp/jmp/`).

# # Using the Vi Editor

It's almost impossible to use Linux for any period of time and not need to use a text editor. If you are using a GUI, you can run edit, which is fairly intuitive for editing text. Most Linux users will use either the vi or emacs commands to edit text files. The advantage of vi or emacs over a graphical editor is that you can use it from any shell, a character-based connection over a network (using telnet or ssh, for example). No GUI is required.

This section provides a brief tutorial of the vi editor. The tutorial was done using the vi or vim (Improved) editors provided with the min-minimal and vim-advanced packages in Fedora.

Any time in this book that I suggest you manually edit a configuration file, you can use vi to do that (from any shell). If vi doesn't suit you, see the sidebar "Exploring Text Editors" (for other options).

The editor is difficult to learn at first. But when you know it, you will be able to edit and move around quickly and efficiently within files. Your fingers never leave the keyboard to pick up a mouse or press a function key.

# # Starting with vi

Most often, you start vi to open a particular file. For example, to open a file called /tmp/test, type the following command:

```
$ vi /tmp/test
```

If this is a new file, you should see something similar to the following: