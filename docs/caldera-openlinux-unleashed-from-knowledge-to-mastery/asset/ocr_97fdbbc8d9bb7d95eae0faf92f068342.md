If you press Tab a second time, the shell lists the possibilities. You can complete the file-name yourself, or type enough characters to disambiguate the choice and then press Tab again.

**Tip**

The second Tab trick works for bash. If your shell is *tcsh*, you need to press **Ctrl+D** to get a listing of the possibilities. If your shell is *csh* or *sh*, you do not have completion at all. *tcsh* has a very elaborate completion mechanism and is described in Chapter 3.

If a completed filename is a directory, the shell is clever enough to add a trailing slash to it. You can even keep going, completing your way all the way down a long directory path. On my Caldera OpenLinux system, I can get to the 38-character file `/usr/share/sendmail/cf/ostype/linux.m4` with just 15 keystrokes:

```
`$ u Tab s Tab se Tab c Tab o Tab l Tab i Tab`
```

# # Command Editing

The shell lets you edit commands as you type them.

+   * Use the left and right arrow keys to move back and forth in the command line.
+   * Type characters to insert them where the cursor is.
+   * While you're editing a command, press **Ctrl+D** to delete the character under the cursor.

**Note**

Don't press **Ctrl+D** if you just have a shell prompt and no command yet. **Ctrl+D** is the terminal end-of-file character, and pressing it first thing after a shell prompt may log you out!

+   * Press up or down arrow to move to the previous or next command in the command history. Note that moving around in the command history discards any edits you may have made to the current command.
+   * Press **Ctrl+A** to move to the beginning of the command.
+   * Press **Ctrl+E** to move to the end of the command.