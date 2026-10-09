![](bbox=[0.28, 0.08, 0.86, 0.36])

**Figure 5-16 Starting vim**

# ## vim is not installed by default: use vim.tiny

The full version of the **vim** editor is not installed by default. Instead, a small version of **vim**, named **vim.tiny** is installed. You can either replace each **vim** command in this section with **vim.tiny**, or you can install the full **vim** editor by giving the command `sudo aptitude install vim` and then use the **vim** command as shown in this section.

# ## The vi command runs vim

On Ubuntu Linux systems the command `vi` runs `vim` in `vi`-compatible mode (page 193).

If you start `vim` with a terminal type that is not in the `terminfo` database, `vim` displays an error message and the terminal type defaults to `ansi`, which works on many terminals. In the following example, the user mistyped `vt100` and set the terminal type to `vg100`:

```
E558: Terminal entry not found in terminfo
'vg100' not known. Available builtin terminals are:
               builtin_ansi
               builtin_xterm
               builtin_iris-ansi
               builtin_dumb
    defaulting to 'ansi'
```

To reset the terminal type, press `ESCAPE` and then give the following command to exit from `vim` and display the shell prompt:

```
:q!
```

When you enter the colon (`:`), `vim` moves the cursor to the bottom line of the screen. The characters `q!` tell `vim` to quit without saving your work. (You will not ordinarily exit from `vim` this way because you typically want to save your work.) You must