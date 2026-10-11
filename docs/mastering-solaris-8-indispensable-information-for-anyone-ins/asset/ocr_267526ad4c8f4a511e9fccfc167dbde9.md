All functions are stored in memory so that the Korn shell can make the most efficient use of them. The source for the function is loaded into memory each time a shell or subshell is started. The downside to this is, if you define too many functions, the memory is sluggish when you run your scripts. It is wise to use functions sparingly or to use the auto_load built-in, which is available only in the Korn shell.

You can store functions in files and make them available to memory the first time they are called. The auto_load built-in notifies the shell that a function is stored in a file. The auto_load function executes usually at the beginning of a new shell. The shell does not load the function into memory but remembers the name. When a script calls for an auto_load function, the Korn shell searches through the directories listed in FPATH for a file with the same name. It then loads the function into memory and leaves it there. Here is the syntax for auto_load:

```
`auto_load <func_name>`
```

Make certain that the function definition and the file you store it in have the same name. Confusion will arise if you store it in a different file.

# ## Function Commands

The job control command under the Korn shell is similar to that of the C shell and Job shell. You can move commands between the foreground and background, suspend jobs temporarily, and produce a list of current jobs. The percent (`%`) sign references a job when followed by a job number or a string prefix.

The alias built-in in the Korn shell does not accept arguments as such. Use a shell function (as discussed earlier) with the alias command if you need to use an argument. This will disguise the argument. Here is the syntax for the alias built-in:

```
`alias [-tx] [<name>[=<command]]`
```

The <name> argument is the name of the alias and <command> is the command line the alias is replaced with when it is called. If you want to track an alias, use the -t option. The -x option will export the alias. If you establish aliases in your .profile file, they will be available every time you log in.

The Korn shell has some built-in aliases that can be unset or redefined:

```
``` 
 auto_load='type set -fu'
 functions='type set -f'
 history='fc -1'
 integer='type set -i'
 local=type set
 r='fc -e -'
 stop='kill -STOP'
 suspend='kill -STOP $$'
```
```