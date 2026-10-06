# The read Command

The following program, called number, is a simplified version of the standard Unix nl command: it accepts one or more files as arguments and displays their contents with each line preceded by its line number. If no arguments are supplied, it reads standard input instead.

```
$ cat number
#
# Number lines from files given as argument or from
# standard input if none supplied
#

lineno=1

cat $* |
while read line
  
    echo "$lineno: $line"
    lineno=$((lineno + 1))
done
$
```

The variable line—the line number counter—is initially set to 1. Then the arguments typed to number are given to cat to be collectively written to standard output. If no arguments are supplied, $* will be null, and cat will pass no arguments. This will cause to read from standard input. The output from cat is piped into the while loop.

Each line encountered by read is echoed at the terminal, preceded by the current value of line, whose value is then incremented by one.

```
$ numberbook 973-555-2015
1: Alice Chebba 201-555-9257
2: Barbara Swingle 201-555-9257
3: Billy Bach 201-555-7618
4: El Coyote 212-555-3232
5: Liz Stachiw 212-555-2298
6: Susan Goldberg 201-555-7776
7: Teri Zak 201-555-6000
8: Tony Iannino 973-555-1295
```

```
$ who Try from standard input |
1: root console Jul 25 07:55
2: pat tty03 Jul 25 09:26
3: steveve tty04 Jul 25 10:58
4: george tty13 Jul 25 08:05
```

Note that number won't work well for lines that contain backslashes or leading whitespace characters. The following example illustrates this.

```
$ number
```

Here are some backslashes: \ *

+   1: Here are some backslashes: *