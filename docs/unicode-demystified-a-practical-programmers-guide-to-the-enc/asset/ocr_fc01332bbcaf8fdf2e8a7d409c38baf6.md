called keymaps. By altering the keymaps, you can change the gathering
rules or which procedure is associated with which sequence. If you
used to use vi's CONTROL-W to back up over the word you are entering,
y may want to change emacs CONTROL-W binding from its standard
ill-region to delete-word-backward.

+   * The command behavior is often conditioned by one or more global vari-
ables options. It may be possible to get the behavior you want by setting
some of these variables.

+   * The command itself is usually a Lisp program that can be reprogrammed
to make it behave as desired. Although this is not for beginners, the Lisp
source to nearly all commands is available, and the internal Lisp system is
fully documented. As mentioned before, it is common to load customized
lisp code at startup time, even if you did not write it.

Most emacs documentation glosses translation, gathering, and pro-
jecture selection and talks about keystrokes as though they were the commands.
However, it is still important to know that the underlying machinery exists and to
understand that its behavior can be changed.

# The .emacs Startup File

Each time you start emacs, it loads the file of Lisp code named ~/.emacs. Using this
file is the most common way to customize emacs for yourself. Two command line
options control the use of the ~/.emacs file. The -q option ignores the .emacs file so
that emacs starts up without it; the only way to get a bad parse. The -u
user option uses the user/.emacs file (the .emacs file from the home directory of
user).

The .emacs startup file is generally concerned only with key bindings and option
settings; it is possible to write the Lisp statements for this file in a straightforward
style. Inside the parenthen-ses first symbol is the Lisp function name, and the rest of the SPACE-separated tokens
arguments are to that function. The most common function in the .emacs file, setq,
is a simple assignment to a global variable. The first argument is the name of a vari-
abled named c-indent and the second argument is its value. The following example sets the
cindent-level to 8:

```
(setq c-indent-level 8)
```

Set the default value for a variable that is buffer-private, using the function
name setq-default. To set a specific element of a vector, use the function name outset.
The first argument is the name of the vector, the second is the target offset, and