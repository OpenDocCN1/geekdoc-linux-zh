# More on Subshells

You know that a subshell can’t change the value of a variable in a parent shell, nor can it change its current directory. Suppose that you want to write a program to set values for some variables that you like to use whenever you log on. For example, assume that you have the following file called vars:

```
```sh
$ cat vars
BOOK=/users/steve/book
VUPUB=/user/spot1/uucppublic
DOCS=/usr/steve/docs/memos
DB=/usr2/data
$
```
```

If you invoke vars, the values assigned to these variables will essentially vanish after the program has finished executing because vars is run in a subshell:

```
```sh
$ vars
$ echo $BOOK

$
```
```

No surprise there.

# The . Command

To address this dilemma, there’s a built-in shell command called . (pronounced “dot”) whose general format is

```
```sh
. file
```
```

and whose purpose is to execute the contents of file in the current shell. That is, commands from file are executed by the current shell just as if they were typed, not within a subshell. The shell uses your PATH variable to find file, just like it does when executing other programs.

```
```sh
$ . vars        # Execute vars in the current shell
$ echo $BOOK    # Hoorah!
/users/steve/book
$
```
```

Because a subshell isn’t spawned to execute the program, any variable that gets assigned a value is retained even after the program completes.

If you have a program called db that has the following commands:

```
```sh
$ cat db
DATA=/usr2/data
RPTS=$DATA/rpts
BIN=$DATA/bin

cd $DATA
$
```
```