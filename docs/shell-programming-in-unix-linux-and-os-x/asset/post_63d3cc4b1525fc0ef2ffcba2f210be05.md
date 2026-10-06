
$ run new.hire Execute with new.hire as the argument
request id is laserl24 (standard input)
$

Each time you execute the program, whatever word follows on the command line will be stored inside the first positional parameter by the shell and handed to the program. In the first example, new.hire will be stored in this parameter.

Substitution of positional parameters is identical to substitution of other types of variables, so when the shell sees

$1 replaces the $1 with the first argument supplied to the program: new.hire.

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

## The $ Variable

In addition to the positional variables, the special shell variable $$ gets set to the number of arguments that were typed on the command line. As you will see in this chapter, variable is often tested by programs to determine whether the correct number of arguments was specified by the user.

The next program, called args, was written to get you more familiar with the way arguments are passed to shell programs. Study the output from each example and make sure you understand it:

```
$ args
echo $$ arguments passed
echo arg 1 = $1; arg 2 = $2; arg 3 = $3;
$ args a b c
3 arguments passed
arg 1 = :a; arg 2 = :b; arg 3 = :c;
$ args a b
```

> Look at the program
> Execute
> Try it with two arguments

## The $ Variable

2 arguments passed
arg 1 = :a arg 2 = :b arg 3 = 
Unassigned args are null

As you can see, the shell does its normal command-line processing when it executes your shell programs. This means that you can take advantage of the normal niceties, such as filename substitution and variable substitution, when specifying arguments to your programs.

## The $ Variable

The special variable references all the arguments passed to the program. This is often useful in programs that take an indeterminate or variable number of arguments. You'll see some more examples later. Here's a program that illustrates its use:

```
$ cat args2
echo $* arguments passed
echo they are $*
$ args2 a b c
3 arguments passed
they are :a b c:
$ args2 one two
2 arguments passed
they are :one two:
$ args2
0 arguments passed
they are ::
$ args2 * arguments passed
they are :args args2 names nu phonebook stat xact xtra
$
```

## A Program to Look Up Someone in the Phone Book

Here's the phonebook file from previous examples:

```
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
```

You know how to look up someone in the file using grep:

```
$ grep Cheb phonebook
Alice Chebbe 973-555-2015
$
```

And you know that if you want to look up someone by their full name, you need to put quotes around the words to keep the argument together:

```
$ grep "Susan T" phonebook
Susan Topple 212-555-4932
$
```

It would be nice to write a script that you could use to look up someone. Let's call the program lu and take it as its argument name of the person to seek:

```
$ cat lu
# Look someone up in the phone book
#
grep $1 phonebook
$
```

Here's a sample use of lu:

```
$ lu Alice
Alice Chebbe 973-555-2015
$ lu Susan
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
$ lu "Susan T"
grep: can't open T
phonebook:Susan Goldberg 201-555-7776
phonebook:Susan Topple 212-555-4932
$
```

In the preceding example, we were careful enough to enclose Susan T in double quotes; so what happened? Look again at the grep invocation in the lu program:

```
grep $1 phonebook
```

## A Program to Add Someone to the Phone Book

See the problem? Enclosing Susan inside double quotes results in its getting passed to lu as a single argument, when the shell substitutes this value for $1 on grep's command line within the program, it passes it as two arguments.

You can fix this problem by enclosing $1 inside double quotes in the lu program:

```
$ cat lu
# Look someone up in the phone book -- version 2
$ grep "$1" phonebook
$
```

Single quotes wouldn't work in this instance. Why? Now let's try that invocation again:

```
$ lu Tony Iannino 973-555-1295
$ lu "Susan T"
Susan Topple 212-555-4932
```

## A Program to Add Someone to the Phone Book

Let's continue with the development of programs that work with the phonebook file. You'll probably want to add someone to the file at some point, because our phonebook file is small, so let's write a program add that takes two arguments: the name of the person to be added and their number. The add program simply amends the name and number, separated by a tab character, onto the end of the phonebook file:

```
$ cat add
# Add someone to phone book
echo "$1"$2" >> phonebook
```

Although you can't tell, there's a tab character that separates the $1 from the $2 in the preceding echo command. This tab must be quoted to make it echo without getting gobbled by the shell. Let's try out our program:

```
$ add 'Stromboli Pizza' 973-555-978
$ lu
Stromboli Pizza 973-555-978
```

If we can find the new entry so far, so good.

## Chapter 6 Passing Arguments

```
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
Stromboli Pizza 973-555-978
$
```

What happened? Stromboli Pizza was quoted so the shell passed it to add as a single argument (what would have happened if it wasn't quoted?). After finishing execution, I ran to see if it could affect the new entry, and to edit. The command was executed to see what the modified phonebook file looked like. The new entry was added to the end, as intended. Unfortunately, the new file is no longer sorted. This will not affect the operation of the program but it's a nice feature nonetheless. Adding the program by the sort command:

```
$ cat add
# Add someone to phonebook file -- version 2
echo "$1"$2 >> phonebook
sort -o phonebook
$
```

Recall that the -o option to sort specifies what the sorted output is to be written, and this can be the same as the input file:

```
$ add 'Billy Bach' 201-555-718
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Billy Bach 201-555-718
Liz Stachiw 212-555-2298
Stromboli Pizza 973-555-978
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
```

Each time a new entry is added, the phonebook file will get re-sorted so that multi-line matches are always in alphabetical order.

## A Program to Remove Someone from the Phone Book

No set of programs that enable you to look up or add someone to the phone book would be complete without a program to remove someone from the phone book too. We'll call this program rem and let the user specify the name of the person to be removed as an argument.

What should the strategy for developing the program? Essentially, you want to remove the name from the file that contains the specified name, a reverse pattern match. The -v option to grep can be used here because it does exactly what we want, printing all lines from a file that doesn't match a pattern:

```
$ cat rem
# Remove someone from the phone book
grep -v "$1" phonebook > /tmp/phonebook
$
```

The grep construct writes all lines that do not match the file /tmp/phonebook. (Tip: /tmp is a directory in Unix systems for temporary files and is usually wiped clean every time the system restarts.) After the grep command is done, the phonebook file is replaced by the new one from /tmp.

```
$ rem 'Stromboli Pizza'
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Billy Bach 201-555-718
Liz Stachiw 212-555-2298
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
$
$ rem Susan
$ cat phonebook
Alice Chebbe 973-555-2015
Barbara Swizzle 201-555-9257
Billy Bach 201-555-718
Liz Stachiw 212-555-2298
Tony Iannino 973-555-1295
$
```

> Remove this entry

The first case, when Stromboli Pizza was removed, worked fine. In the second case, however, both Susan entries were removed because they matched the pattern. Not good! You can use the add program to add them back to the phone book:

```
$ add 'Susan Goldberg' 201-555-7776
$ add 'Susan Topple' 212-555-4932
$
```
