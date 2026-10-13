```
```sh
$ fc -s B=C
cat docs/planC
...
$
```
```

# # Functions

Bash and the Korn shell both have function features not available in the POSIX standard shell. Let's have a look.

# ## Local Variables

Both Bash and Korn shell functions can have local variables, making recursive functions possible. These variables are defined with the typeset command, as in

typeset i j

If a variable of the same name already exists, it is saved when the typeset is executed and restored when the function exits.

After using the shell for a while, you may develop a set of functions that you like to use during your interactive work sessions. A good place to define such functions is inside your ENV file so that they will be defined whenever you start up a new shell.

# ## Automatically Loaded Functions

The Korn shell allows you to set up a special variable called FPATH that is similar to your PATH variable. If you try to execute a function that is not yet defined, the Korn shell searches the colon-delimited list of directories in FPATH for a file that matches the function name. If it finds such a file, it executes it in the current shell with the expectation that somewhere in the file is a definition for the specified function.

# # Integer Arithmetic

Both Bash and the Korn shell support evaluating arithmetic expressions without arithmetic expansion. The syntax is similar to $((...)) but without the dollar sign. Because expansion is not performed, the construct can therefore be used by itself as a command:

```
```sh
$ x=10
$ ((x = x * 12))
$ echo $x
120
$
```
```