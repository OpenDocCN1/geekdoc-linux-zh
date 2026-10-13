The two-digit hour obtained from `date` is assigned to the shell variable `hour`, then the `case` statement is executed. The value of `hour` is compared against the first pattern:

```
0? | 1[01]
```

which matches any value that starts with a zero followed by any character (midnight through 9 am), or any value that starts with a one and is followed by a zero or one (10 or 11 am).

The second pattern

```
1[2-7]
```

matches a value that starts with a one and is followed by any one of the digits two through seven (noon through 5 pm).

The last case, the catch-all, matches anything else (6 pm through 11 pm).

```
$ date
Wed Aug 28 15:45:12 EDT 2002
$ greetings
Good afternoon
$
```

# The Null Command :

Every matching case statement needs a resulting command, and every `if-then` conditional needs a resultant command too—but sometimes you don't want to execute anything, just “eat” the result. How do you do that? With the shell’s built-in *null* command. The format of this command is simply

```
:
```

and the purpose of it is—you guessed it—to do nothing.

In most cases it’s used to satisfy the requirement that a command appear, particularly in `if` statements. Suppose that you want to make sure that the value stored in the variable `system` exists in the file `/user/steve/mail/systems`, and if it doesn’t, you want to issue an error message and exit from the program. So you start by writing something like

```
if grep "^$system" /users/steve/mail/systems > /dev/null
then
```

but you don’t know what to write after the `then` because you want to test for the nonexistence of the system in the file and don’t want to do anything special if the grep succeeds. The shell requires that you write a command after the `then`, so here’s where the null command comes to the rescue:

```
if grep "^$system" /users/steve/mail/systems > /dev/null
then
        :
else
        echo "$system is not a valid system"
        exit 1
fi
```