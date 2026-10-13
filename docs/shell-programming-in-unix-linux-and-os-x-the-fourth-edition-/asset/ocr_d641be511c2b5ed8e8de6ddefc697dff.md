```
```sh
command
command
...
else
    if command₂
    then
        command
        command
        ...
    else
        ...
        if commandₙ
        then
            command
            command
            ...
        else
            command
            command
            ...
        fi
        ...
    fi
fi
```
```

This type of command sequence can be useful when you need to make more than just a two-choice decision. In this case, a multiway decision is made, with the last else clause executed if none of the preceding conditions is satisfied.

As a relatively simple example, let’s write a program called `greetings` that prints a friendly Good morning, Good afternoon, or Good evening based on time of day. For purposes of the example, consider any time from midnight to noon to be the morning, noon to 6 pm the afternoon, and 6 pm to midnight the evening.

To write this program, you have to find out what time it is. `date` serves just fine for this purpose. Take another look at the output from this command:

```
```sh
$ date
Wed Aug 29 10:42:01 EDT 2002
$
```
```

The format of `date`’s output is fixed, a fact that you can use to your advantage because the time will always appear in character positions 12 through 19. In fact, you really only need the hour value in positions 12 and 13:

```
```sh
$ date | cut -c12-13
10
$
```
```