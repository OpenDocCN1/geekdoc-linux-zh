$ run new.hire Execute with new.hire as the argument
request id is laserl24 (standard input)
$

Each time you execute the program, whatever word follows on the command line will be stored inside the first positional parameter by the shell and handed to the program. In the first example, new.hire will be stored in this parameter.

Substitution of positional parameters is identical to substitution of other types of variables, so when the shell sees

tbl $1 replaces the $1 with the first argument supplied to the program: new.hire.

As another example, the following program, called ison, lets you know if a specified user is logged on:

```
$ ison
who | grep $1
$ who
root console t 7 Jul 8 12:37
barney tty03 Jul 8 12:28
fred tty04 Jul 8 13:24
joanne tty07 Jul 8 09:35
tony tty19 Jul 8 08:30
lulu tty23 Jul 8 09:55
$ ison
tony tty19 Jul 8 08:30
$ ison pat
```

> See who's on

> Not logged on

# # $ Variable

In addition to the positional variables, the special shell variable $$ gets set to the number of arguments that were typed on the command line. As you will see in this chapter, variable is often tested by programs to determine whether the correct number of arguments was specified by the user.

The next program, called args, was written to get you more familiar with the way arguments are passed to shell programs. Study the output from each example and make sure you understand it:

```
$ args
echo $$ arguments passed
echo arg 1 = ::1; arg 2 =::$2; arg 3 = :3:
$ args a b c
3 arguments passed
arg 1 = :a; arg 2 = :b; arg 3 = :c;
$ args a b
```

> Look at the program

> Execute

> Try it with two arguments