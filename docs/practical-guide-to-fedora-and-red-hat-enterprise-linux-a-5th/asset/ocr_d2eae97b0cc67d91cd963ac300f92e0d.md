```
```
$ cat films/dar \u2192TAB (beep) cat films/dark_
```
```

In the `films` directory every file that starts with `dar` has `k_` as the next characters, so `bash` cannot extend the line further without making a choice among files. You are left with the cursor just past the `_` character. At this point you can continue typing the pathname or press `TAB` twice. In the latter case `bash` beeps, displays your choices, redisplay the command line, and again leaves the cursor just after the `_` character.

```
```
$ cat films/dark_ \u2192TAB (beep) \u2192TAB
dark_passage    dark_victory
$ cat films/dark_
```
```

When you add enough information to distinguish between the two possible files and press `TAB`, `bash` displays the unique pathname. If you enter `p` followed by `TAB` after the `_` character, the shell completes the command line:

```
```
$ cat films/dark_p \u2192TAB \u2192ssage
```
```

Because there is no further ambiguity, the shell appends a `SPACE` so you can finish typing the command line or just press `RETURN` to execute the command. If the complete pathname is that of a directory, `bash` appends a slash (`/`) in place of a `SPACE`.

# VARIABLE COMPLETION

When typing a variable name, pressing `TAB` results in *variable completion*, where `bash` tries to complete the name of the variable. In case of an ambiguity, pressing `TAB` twice displays a list of choices:

```
```
$ echo $HO \u2192TAB
HOME    HOSTNAME    SHOSTTYPE
$ echo $HOM \u2192TAB \u2192E
```
```

# Pressing RETURN executes the command

Pressing `RETURN` causes the shell to execute the command regardless of where the cursor is on the command line.

# ### .inputrc: CONFIGURING READLINE

The Bourne Again Shell and other programs that use the Readline Library read the file specified by the `INPUTRC` environment variable to obtain initialization information. If `INPUTRC` is not set, these programs read the `~/.inputrc` file. They ignore lines of `.inputrc` that are blank or that start with a pound sign (`#`).

# VARIABLES

You can set variables in `.inputrc` to control the behavior of the Readline Library using the following syntax:

```
`    set variable value`
```

Table 9-11 (next page) lists some variables and values you can use. See *Readline Variables* in the `bash` man or info page for a complete list.