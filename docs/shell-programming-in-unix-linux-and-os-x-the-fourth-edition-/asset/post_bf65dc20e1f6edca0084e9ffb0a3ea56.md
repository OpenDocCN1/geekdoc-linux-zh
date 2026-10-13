
## Decisions, Decisions

This chapter introduces the conditional statement, a construct that is present in almost every programming language: `if`. It enables you to test a condition and then change the flow of program execution based on the result of the test.

The general format of the `if` command is

```text
if command
then
        command
        command
        ...
fi
```

where `command` is executed and its exit status is tested. If the exit status is zero, the commands that follow between `then` and `fi` are executed; otherwise, they’re skipped.

### Exit Status

To understand how conditional tests work, it’s important to know about how Unix works with what’s called the exit status. Whenever any program completes execution, it returns an exit status code to the shell. This status is a numeric value that indicates whether the program ran successfully or failed. By convention, an exit status of zero indicates that a program succeeded, and non-zero indicates that it failed, with different values indicating different kinds of failures.

Failures can be caused by invalid arguments passed to the program, or by an error condition detected by the program. For example, the `cp` command returns a non-zero (fail) exit status if the copy fails (for example, if it can’t find the source file or create the destination file), or if the arguments aren’t correctly specified (for example, the wrong number of arguments, or more than two arguments and the last one isn’t a directory).

What do we mean by non-zero? Simply, any integer value that isn’t 0. Most command man pages list possible exit status values too, so possible error conditions for a file copy command could be 1 for file not found, 2 for file not readable, 3 for destination folder not found, 4 for destination folder not writable, 5 for general error copying the file and, of course, 0 for success.

In the case of grep, an exit status of zero (success) is returned if it finds the specified pattern in at least one of the files specified; a non-zero value is returned if it can’t find the pattern or if a different error occurs, like failure to open a specified source file.

In a pipeline, the exit status reflects the last command in the pipe. So in

```text
who | grep fred
```

the grep exit status is used by the shell as the exit status for the whole pipeline. In this case, an exit status of zero (success) means that fred was found in who’s output (that is, fred was logged on at the time that this command was executed).

### The `$?` Variable

The shell variable `$?` is automatically set by the shell to the exit status of the last command executed. Naturally, you can use echo to display its value at the terminal.

```text
$ cp phonebook phone2
$ echo $?
0                         Copy “succeeded”
$ cp nosuch backup
cp: cannot access nosuch
$ echo $?
2                         Copy “failed”
$ who                     See who’s logged on
root     console Jul 8 10:06
wilma    tty03   Jul 8 12:36
barney   tty04   Jul 8 14:57
betty    tty15   Jul 8 15:03
$ who | grep barney
barney   tty04   Jul 8 14:57
$ echo $?                 Print exit status of last command (grep)
0                         grep “succeeded”
$ who | grep fred
$ echo $?
1                         grep “failed”
$ echo $?
0                         Exit status of last echo
$
```

Note that the numeric result of a “failure” for some commands can vary from one version of Unix to the next, but success is always signified by a zero exit status.

Let’s write a shell program called `on` that tells us whether a specified user is logged on to the system. The name of the user to check will be passed to the program on the command line. If the user is logged on, we’ll print a message to that effect; otherwise we’ll say nothing. Here is the program:

```text
$ cat on
#
# determine if someone is logged on
#
user="$1"

if who | grep "$user"
then
    echo "$user is logged on"
fi
$
```

This first argument typed on the command line is stored in the shell variable `user`. Then the `if` command executes the pipeline

```text
who | grep "$user"
```

and tests the exit status returned by `grep`. If the exit status is zero (success), `grep` found `user` in `who`’s output. In that case, the `echo` command that follows is executed. If the exit status is non-zero (failure), the specified user is not logged on, and the `echo` command is skipped.

The `echo` command is indented from the left margin for aesthetic reasons only. In this case, just a single command is enclosed between the `then` and `fi`. When more commands are included, and when the nesting gets deeper, indentation can have a significant impact on the program’s readability. Later examples will help illustrate this point.

Here are some sample uses of `on`:

```text
$ who
root     console  Jul 8 10:37
barney   tty03    Jul 8 12:38
fred     tty04    Jul 8 13:40
joanne   tty07    Jul 8 09:35
tony     tty19    Jul 8 08:30
lulu     tty23    Jul 8 09:55
$ on tony
tony     tty19    Jul 8 08:30
tony is logged on
$ on
$ on ann
joanne   tty07    Jul 8 09:35
ann is logged on
$
```

> *We know he’s on*  
> *Where did this come from?*

> *We know he’s not on*  
> *Try this one*

There are a couple of problems with the program as written, however. When the specified user is logged on, the corresponding line from `who`’s output is also displayed, courtesy of the call to `grep`. This may not be such a bad thing, but the program requirements called for only the informational “logged on” message to be displayed and nothing else.

This extra line is displayed because of the conditional test: not only does `grep` return an exit status in the pipeline

```text
who | grep "$user"
```

but it also goes about its normal function of writing any matching lines to standard output, even though we’re really not interested in that.

Since we’re not interested in seeing the result of the command, just testing the exit code, we can dispose of `grep`’s output by redirecting it to the system’s “garbage can,” `/dev/null`. This is a special file on the system that anyone can read from (and get an immediate end of file) or write to. When you write to it, the bits vanish, as if it were a massive black hole!

```text
who | grep "$user" > /dev/null
```

That’ll solve the superfluous output problem.

The second problem with `on` appears when the program is executed with the argument `ann`. Even though `ann` is not logged on, `grep` matches the characters `ann` for the user `joanne`. What we need is a more restrictive pattern, which you learned how to do in Chapter 3 where we talked about regular expressions. Because `who` lists each username in column one of the output, we can anchor the pattern to match the beginning of the line by preceding the pattern with the character `^`:

```text
who | grep "^$user" > /dev/null
```

But that’s still not enough. Search for a pattern like `bob` and `grep` still matches a line like

```text
bobby   tty07  Jul 8 09:35
```

What you need to do is also anchor the pattern on the right too. Realizing that `who` ends each username with one or more spaces, the further modified pattern

```text
"^$user "
```

now only matches lines for the specified user. Problem two fixed!

Let’s try the new and improved version of `on`:

```text
$ cat on
#
# determine if someone is logged on -- version 2
#
user="$1"

if who | grep "^$user " > /dev/null
then
        echo "$user is logged on"
fi
$ who                    Who's on now?
root       console Jul 8 10:37
barney     tty03   Jul 8 12:38
fred       tty04   Jul 8 13:40
joanne  tty07  Jul 8 09:35
tony    tty19  Jul 8 08:30
lulu    tty23  Jul 8 09:55
$ on lulu
lulu is logged on
$ on ann
$ on
$
```

> *Try this again*  
> *What happens if we don't give any arguments?*

If no arguments are specified, `user` will be null. `grep` will then look through `who`’s output for lines that start with a blank (why?). It won’t find any, and so just a command prompt will be returned. In the next section, you’ll see how to test whether the correct number of arguments has been supplied to a program and, if not, take some action.

### The test Command

Though the previous example program used a pipeline to test for the `if` statement, a built-in shell command called `test` is much more commonly used for testing one or more conditions. Its general format is

```text
test expression
```

where *expression* represents the condition you’re testing. `test` evaluates *expression*, and if the result is *true*, it returns an exit status of zero, otherwise the result is *false*, and it returns a nonzero exit status.

### String Operators

As an example, the following command returns a zero exit status if the shell variable `name` contains the characters `julio`:

```text
test "$name" = julio
```

The `=` operator is used to test whether two values are identical. In this case, we’re testing to see whether the *contents* of the shell variable `name` are identical to the characters `julio`. If it is, `test` returns an exit status of zero; nonzero otherwise.

Note that `test` must see all operands (`$name` and `julio`) and operators (`=`) as separate arguments, meaning that they must be delimited by one or more whitespace characters.

Getting back to the `if` command, to echo the message “Would you like to play a game?” if `name` contains the characters `julio`, you would write your `if` command like this:

```text
if test "$name" = julio
then
        echo "Would you like to play a game?"
fi
```

When the `if` command gets executed, the command that follows the `if` is executed, and its exit status is evaluated. The `test` command is passed the three arguments `$name` (with its
