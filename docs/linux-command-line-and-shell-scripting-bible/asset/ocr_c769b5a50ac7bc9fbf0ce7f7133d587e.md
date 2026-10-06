# The tcsh Shell 21

The output from the alloc command is somewhat cryptic. The two sets of numbers show the list of memory blocks in increasing block sizes, starting at an 8-byte block, a 16-byte block, and so on up to a 2 MB block of memory. Thus, in this example, there are eighty-three 16-byte blocks free, 93 32-byte blocks free, five 64-byte blocks free, and so on up to one 16 KB block free. The process is used to display the used memory blocks. The result totals are shown at the end of the listing.

The bindkey command is another interesting built-in command in the tcsh shell. It allows you to bind a key combination to any sequence, or shell command. By default, the tcsh shell binds lots of key combinations to editor commands, allowing you to easily edit your command lines using simple editor key combinations.

You can list all of the current key bindings just by entering the bindkey command by itself on the command line:

```
$ bindkey
Standard key bindings set-mark-command
"* beginning-of-line
^A backward-char
^C tty-sigintr
^D delete-char-list-or-eof
^E end-of-line
```

This is just a partial list of the current key binding in my tcsh shell. The list is quite lengthy.

To define a new key binding, list the desired key combination and the command or string you want to assign:

```
$ bindkey -c G ls-F
test1-* test2* tmp/
logout.txt test2-* test.txt
```

Now every time I hit the Ctrl-G key binding I get the ls -F listing!

# Scripting in tcsh

Writing shell scripts in the tcsh shell isn't any more difficult than in the bash shell, just different. You'll need to get used to a slightly different method for performing many of the standard statements you're used in bash.

577