# Command Summary 341

export variable
if variable has been exported but does not yet have its value set.

# The false Command

General Format: false

The false command returns a nonzero exit status.

# The fc Command

General Format: fc -e editor -lnr first last [old=new]

The fc command is used to edit commands in the command history. A range of commands is specified from first to last, where first and last can be either numbers or strings; a negative number takes as an offset from the current command number, while a string specifies the most recently entered command beginning with that string. The commands are read into the editor and executed upon exit. If no editor is specified, the value of the shell variable FCEDIT is used; if FCEDIT is not set, ed is used.

The -l option lists the commands from first to last (that is, an editor is not invoked). If the -n option is not specified, these commands are not preceded by command numbers.

The -r option to fc reverses the order of the commands.

If last is not specified, it defaults to first. If first is also not specified, it defaults to the previous command for editing and to -16 for listing.

The -s option causes the selected command to be executed without editing it. The format

```
fc -s old=new first
```

causes the command first to be re-executed the old in the command is replaced with new. If first isn't specified, the previous command is used, and if old=new isn't specified, the command is not changed.

Examples

+   fc -l List the last 16 commands
fc -e vi sed Read the last sed command into vi
fc 100 110 Read commands 100 to 110 into $FCEDIT
fc -s Re-execute the previous command
fc -s abc=def 104 Re-execute command 104, replacing abc with def