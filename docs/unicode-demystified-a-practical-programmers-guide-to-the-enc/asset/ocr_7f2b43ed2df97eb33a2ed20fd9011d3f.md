```
function func_name
{
  commands()
}
```

The first brace ({ can appear on the same line as the function name. If the function definition includes the names of aliases, they are expanded when the function is read, when it is executed. You can use the break builtin inside a function to terminate its execution. The functions builtin lists all the defined functions.

Shell functions are useful as a shorthand as well to define special commands. The following function starts a process named in the background, with the output normally displayed by process saved in .process.out:

```
start_process() {
  process > .process.out 2>&1 &
}
```

There is no setenv builtin in zsh. The following function mimics the behavior of this command, which is available in zsh:

```
zsh % setenv() {
if [ $ -eq 2 ]; then
  export $1=$2
else
  echo "Usage: setenv NAME VALUE" >&2
fi
```

If there are two arguments, the setenv function assigns the value of the second argument to the name of the first and exports the first. (The Shell export builtin is identical to bash's [page 571]). If there are not two arguments, the function displays a usage message.

The function builtin deletes a function definition:

```
unfunction func_name
```

The Shell stores functions in memory so that they run more efficiently than shell scripts. The source for the functions is loaded into memory each shell or subshell. If you define too many functions, the overhead of a shell (as when you run a script) becomes unacceptable.

You can also store functions in files so that they are read into memory the first time they are called. The autoload builtin notifies zsh that a function is stored in a file. When autoload is executed (normally when you start a new shell), the shell does not load the function into memory but keeps track of its name (it declares it as an undefined function). When a script calls an autoload function, zsh searches through the directories listed in FPATH for a file with the same name as the function. (The syntax of FPATH is identical to that of PATH [page 577]). When