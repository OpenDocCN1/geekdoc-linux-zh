for each of the two commands. Note that the `which` command shows only the external command file.

> **TIP**
> 
> **To use the external command for a command that has multiple flavors, directly reference the file. For example, to use the `pwd` external command, type `/usr/bin/pwd`.**

# Using the *history* command

The Bash shell keeps track of the most recent commands you have used. You can recall these commands and even reuse them. A helpful built-in command that lets you explore and manage these previously issued commands is the `history` command.

To see a list of recently used commands, type the `history` command with no options:

```
```
$ history
  1  ps -f
  2  pwd
  3  ls
  4  coproc ( sleep 10; sleep 2 )
  5  jobs
  6  ps --forest
  7  ls
  8  ps -f
  9  pwd
 10  ls -l /usr/bin/ps
 11  history
 12  cd /etc
 13  pwd
 14  ls
 15  cd
 16  type -a pwd
 17  which pwd
 18  type -a echo
 19  which echo
 20  ls
[...]
$ ```
```