```
46 history -a
47 history
$
$ cat .bash_history
ps -f
pwd
[...]
exit
history
ps --forest
ps --forest
pwd
ls .bash_history
history
cat .bash_history
history -a
$
```

Notice that contents from both the `history` command and the `.bash_history` file match, except for the very last command listed (the `history` command), because it came after the `history -a` command was issued.

# ## NOTE

> If you have multiple terminal sessions open, you can still append `.bash_history` in each open session using the `history -a` command. However, the histories are not automatically updated for your other open terminal sessions. This is because the `.bash_history` file is read-only when a terminal session is first started. To force the `.bash_history` file to be reread and a terminal session's history in memory to be updated, use the `history -n` command.

You can recall any command from the history list. Just enter an exclamation point and the command's number from the history list:

```
$ history
1 ps -f
```