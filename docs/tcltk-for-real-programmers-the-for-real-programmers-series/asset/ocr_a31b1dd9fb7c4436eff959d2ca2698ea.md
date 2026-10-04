# Chapter 2. The Mechanics of Using the Tcl and Tk Interpreters

Under Unix the command interpreters also evaluate shell programs. This is the equivalent of having the MS-DOS .bat file interpreter and command.com functionality available at the command line. Experienced users use this feature to write small programs from the command line to accomplish simple tasks.

For instance, suppose you've been busy developing code for a while and you've forgotten which files you changed. If you've got (or retrieve from an archive) the original code, you can compare all the files in one directory with files with the same name in another directory and put the results in a file with a DIF suffix. The commands at the Bourne, Korn, or Bash prompt are:

```
$ for i in *.c
do
  diff i ../otherDir/$i >$i.DIF
```

You can use tclsh to gain this functionality in the Windows world. To accomplish the same task under a tclsh shell, type:

```
% foreach i [glob *.c] {
  diff $i ../otherDir/$i >$i.DIF
}
```

# 2.2.2 TkConsole—An Alternative Interactive tclsh/wish Shell

Jeffrey Hobbs has written a useful console program, TkConsole, which provides a nicer interface than the simple % prompt.

TkConsole provides:

+   - A menu-driven history mechanism, to make it easy to find and repeat previous commands.

+   - An Emacs-like editor interface to the command line, to make it easy to fix typos or modify commands slightly.

+   - Brace and parenthesis matching, to help you keep your code ordered.

+   - Color coding Tcl command names, to differentiate commands and data.