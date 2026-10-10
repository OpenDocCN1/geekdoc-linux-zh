These aliases give you good results in a Shell buffer. In a normal terminal session (console or xterm), you can use the standard `ls` and `ls -l` commands, and the output will be colored as before.

When Emacs starts up your default shell in a Shell buffer it will use an Emacs-specific initialization file rather than the default `~/.bashrc` if one exists. You can put the above aliases in a file named `~/.emacs_bash` and they will only be effective in Emacs. This works with any shell, not just Bash; as an example Zsh users can name the file `~/.emacs_zsh`.

Another alternative is to use Eshell rather than standard shell mode.

# ## Eshell

Eshell is a new package written by John Wiegley. It is still under active development, but in its current state, it is a viable replacement for standard shell mode.

Rather than using your normal command shell, Eshell provides a new shell written completely in Emacs Lisp. Many of the standard shell commands are emulated in Lisp to such an extent that for casual use you won’t be able to tell the difference. The emulated `ls` command’s output is very similar to the colored `ls -l` output seen in an xterm.

Command completion, aliases, zsh-like globbing, and many other features of the standard Linux shells are all provided by Eshell.

Eshell comes with its own scripting language, but the documentation hasn’t been written yet.

Eshell will be included with Emacs 21. It is currently available as an XEmacs package. Emacs 20-and-earlier users can install Eshell from the tar archive, available on this book’s CD-ROM in the directory `/cdrom/packages`.

You might want to check out the following Web site, because a newer version might be available by the time you read this: `http://www.gci-net.com/users/j/johnw/`.

Installation for pre-21 versions of Emacs isn’t too involved. Just copy the `*.el` files to the site-lisp directory and byte-compile the files. Then insert this line into your `~/.emacs` file:

```
(load "eshell-auto")
```

After you have it installed, start an Eshell session by pressing `M-x` and typing

```
eshell
```

John Wiegley has ambitious plans for Eshell. It might eventually become the default Emacs shell.