# ## Part IV: Working with Alternative Shells

The tesh shell is no slouch in providing built-in commands! I'm sure that you recognize many of these commands from their Bash counterparts. There are a few commands that the tesh shell provides that aren't available in the Bash shell.

The alloc command is an easy way to check on the memory status on your Linux system:

```
ubuntu2404:-> alloc
tesh current memory allocation:
Total space allocated from system: 573440
Number of non-inuse chunks: 2
Number of mmaped regions: 0
Total space in mmaped regions: 0
Total allocated space: 462640
Total non-inuse space: 110800
Top-most, releasable space: 108336
ubuntu2404:->
```

The ls-F command is another command unique to the tesh shell. It produces the same output as if you use the ls command along with the -F parameter (which displays an indicator next to each entry showing executable files, linked files, and directories). Since it's a built-in command, it can produce the output much faster than the standard ls command.

The bindkey command is another interesting built-in command in the tesh shell. It allows you to bind a key combination to any key sequence, or shell command. By default, the tesh shell binds lots of key combinations to editor commands, allowing you to easily edit your command line entries using simple editor key combinations.

You can list all of the current key bindings by entering the bindkey command by itself on the command line:

```
$ bindkey
Standard key bindings
"^A" -> set-mark-command
"^A" -> beginning-of-line
"^B" -> backward-char
"^C" -> tty-sigr
"^D" -> delete-char-or-list-or-eof
"^E" -> end-of-line
...
$
```

This is just a partial list of the current key binding in my tesh shell. The list is quite lengthy.

To define a new key binding, just list the desired key combination and the command or string you want to assign:

```
$ bindkey -C ^G ls-F
$
test1-* test2* tmp/
logout.txt test2-* test.txt
$
```

Now every time I press the Ctrl-G key combination I get the ls-F listing!