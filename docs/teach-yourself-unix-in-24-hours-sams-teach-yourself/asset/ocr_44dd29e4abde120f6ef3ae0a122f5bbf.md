# Hour 16

Because shells are really just interpreted languages, any sequence of commands you wish to be placed in a file and run regularly. This is a shell program. Most UNIX experts write their shell programs for the Bourne shell (/bin/sh) because that is standard on every UNIX platform. Earlier in this book, I illustrated examples by using the C shell, because I feel this is a better interface for the user. Because I'm programming the Bourne shell, the command prompt is slightly different; it's rather than %.

![](bbox=[0.166, 0.273, 0.233, 0.335])

JUST A MINUTE

| I strongly urge you to look at the shells you have available. The best shell is to use the one that makes you the most productive |

# Task 16.1: Shell Variables

![](bbox=[0.166, 0.398, 0.243, 0.426])

Programming languages usually include variables, and the shell naturally does, too. Variables are tags to identify values that may change as a program is used. In the shell, these variables can take a single value and are always interpreted as strings. Even numeric values are strings to the shell.

![](bbox=[0.166, 0.497, 0.233, 0.559])

JUST A MINUTE

| The C shell and Korn shell both support arrays and have means of representing numeric values. |

You can use any string-manipulation command, such as sed or cut, to change a shell variable.

![](bbox=[0.166, 0.626, 0.243, 0.654])

Here is an example of setting the value of a shell variable:

```
$ color-blue
```

This sets the variable color to the string blue. One can output the value of any variable with the echo command:

```
$ echo $colorlue
```

This also indicates how to reference a shell variable: It must be preceded by the dollar sign ($). This can cause some problems. If you are using a shell variable as a prefix and want to immediately append text, you might think this would work:

```
$ leaning="anti-*"
$ echo Joe is basically $leaningtaxes
```

![](bbox=[0.066, 0.893, 0.143, 0.966])