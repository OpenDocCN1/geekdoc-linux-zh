This value for `$` is obviously out of whack (and on your system might differ from what’s shown here). The `$` notation is used by `g` to keep track of the values you’ve previously displayed, so you can easily reference them again later.

Take a look at what the index variable `i` is set to:

```
```
(  print i
$```

```

Oops! That’s not good. You have only five elements in the array and you tried to access the 233rd element when the error occurred. On your system, the error might occur earlier or later. But eventually, you should get an error.

Before you exit from `g`, look at another variable. See how nicely `g` deals with variables like arrays and structures:

Click here to view code image

```
```
(  print data
$  Show the contents of the data array
(  print data[0]
$  Show the value of the first element
$```

```

You’ll see an example of a structure a little later. To complete this first example with `g`, you need to learn how to get out. You can do that with the `q` command:

Click here to view code image

```
```
(  quit
T  y
$```

```

Even though the program had an error, technically speaking, it was still active inside `g`; the error merely caused your program’s execution to be suspended, but not terminated. That’s the reason `g` asked for confirmation about quitting.

# ## Working with Variables

`g` has two basic commands that allow you to work with variables in your program. One you’ve seen already is `p`. The other allows you to set the value of a variable. This is done with the `s` command. The `s` command actually takes a number of different options, but `v` is the one you want to use to assign a value to a variable:

Click here to view code image

```
```
(  set var i=5
(  print i
$  set var i=i*2
$  You can write any valid expression
(  print i
$  set var i=$1+20
$  You can use so-called "convenience variables"
(  print i
$```

```

A variable must be accessible by the current function, and the process must be *active*, that is, running. `g` maintains an idea of a current line (like an editor), a current file (the source file of the program), and a current function. When `g` starts up without a core file, the current function is `m`, the