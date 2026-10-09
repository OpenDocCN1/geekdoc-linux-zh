If you want to delete the entire command line, type the line kill character (page 151). You can type this character while the cursor is anywhere in the command line. If you want to delete from the cursor to the end of the line, press `CONTROL-k`.

# ## READLINE COMPLETION COMMANDS

You can use the `TAB` key to complete words you are entering on the command line. This facility, called _completion_, works in both `vi` and `emacs` editing modes. Several types of completion are possible, and which one you use depends on which part of a command line you are typing when you press `TAB`.

# ## COMMAND COMPLETION

If you are typing the name of a command (usually the first word on the command line), pressing `TAB` initiates _command completion_, in which **bash** looks for a command whose name starts with the part of the word you have typed. If no command starts with the characters you entered, **bash** beeps. If there is one such command, **bash** completes the command name. If there is more than one choice, **bash** does nothing in `vi` mode and beeps in `emacs` mode. Pressing `TAB` a second time causes **bash** to display a list of commands whose names start with the prefix you typed and allows you to continue typing the command name.

In the following example, the user types **bz** and presses `TAB`. The shell beeps (the user is in `emacs` mode) to indicate that several commands start with the letters **bz**. The user enters another `TAB` to cause the shell to display a list of commands that start with **bz** followed by the command line as the user had entered it so far:

```
```
$ bz --TAB-- (beep) --TAB--
   bzcata   bzciff   bzips2   b2less
   bzcmp    bzgrep   bzips2recover  b2more
$ bz
```
```

Next the user types **c** and presses `TAB` twice. The shell displays the two commands that start with **bzc**. The user types a followed by `TAB`. At this point the shell completes the command because only one command starts with **bzca**.

```
```
$ bzca --TAB-- (beep) --TAB--
   bzcat  bzcmp
$ bzca --TAB-- -- t
```
```

# ## PATHNAME COMPLETION

_Pathname completion_, which also uses `TAB`s, allows you to type a portion of a pathname and have **bash** supply the rest. If the portion of the pathname you have typed is sufficient to determine a unique pathname, **bash** displays that pathname. If more than one pathname would match it, **bash** completes the pathname up to the point where there are choices so that you can type more.

When you are entering a pathname, including a simple filename, and press `TAB`, the shell beeps (if the shell is in `emacs` mode---in `vi` mode there is no beep). It then extends the command line as far as it can.