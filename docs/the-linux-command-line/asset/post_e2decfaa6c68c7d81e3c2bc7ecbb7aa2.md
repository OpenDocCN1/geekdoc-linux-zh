
```
count=$(($count + 1))
done
echo "Finished."
```

By changing the test expression to $count -gt 5, until will terminate the loop at the correct time. The decision of whether to use the while or until loop is usually a matter of choosing the one that allows the clearest test to be written.

## Reading Files With Loops

while and until can process standard input. This allows files to be processed with while and until loops. In the following example, we will display the contents of the distros.txt file used in earlier chapters:

```
#!/bin/bash

# while-read: read lines from a file
while read distro version release; do
    printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
        $distro \
        $version \
        $release
done < distros.txt
```

To redirect a file to the loop, we place the redirection operator after the done statement. The loop will use read to input the fields from the redirected file. The read command will exit after each line is read, with a zero exit status until the end-of-file is reached. At that point, it will exit with a non-zero exit status, thereby terminating the loop. It is also possible to pipe standard input into a loop:

```
#!/bin/bash

# while-read2: read lines from a file
sort -k 1,1 -k 2n distros.txt | while read distro version release; do
    printf "Distro: %s\tVersion: %s\tReleased: %s\n" \
        $distro \
        $version \
        $release
done
```

Here we take the output of the sort command and display the stream of text. However, it is important to remember that since a pipe will execute the loop in a subshell, any variables created or assigned within the loop will be lost when the loop terminates.

## Summing Up

With the introduction of loops, and our previous encounters with branching, subroutines and sequences, we have covered the major types of flow control used in programs. bash has some more tricks up its sleeve, but they are refinements on these basic concepts.

## Further Reading

- The Bash Guide for Beginners from the Linux Documentation Project has some more examples of while loops:
  http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_09_02.html
- The Wikipedia has an article on loops, which is part of a larger article on flow control:
  http://en.wikipedia.org/wiki/Control_flow#Loops

## 31 – Troubleshooting

As our scripts become more complex, it’s time to take a look at what happens when things go wrong and they don’t do what what we want. In this chapter, we’ll look at some of the common kinds of errors that occur in scripts, and describe a few useful techniques that can be used to track down and eradicate problems.

## Syntactic Errors

One general class of errors is syntactic. Syntactic errors involve mis-typing some element of shell syntax. In most cases, these kinds of errors will lead to the shell refusing to execute the script.

In the following the discussions, we will use this script to demonstrate common types of errors:

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=1

if [ $number = 1 ]; then
    echo "Number is equal to 1."
else
    echo "Number is not equal to 1."
fi
```

As written, this script runs successfully:

```
[me@linuxbox ~]$ trouble
Number is equal to 1.
```

## Missing Quotes

If we edit our script and remove the trailing quote from the argument following the first echo command:

```
#!/bin/bash

# trouble: script to demonstrate common errors

number=1

if [ $number = 1 ]; then
    echo "Number is equal to 1.
else
    echo "Number is not equal to 1."
fi
```

watch what happens:

```
[me@linuxbox ~]$ trouble
/home/me/bin/trouble: line 10: unexpected EOF while looking for matching "'
/home/me/bin/trouble: line 13: syntax error: unexpected end of file
```

It generates two errors. Interestingly, the line numbers reported are not where the missing quote was removed, but rather much later in the program. We can see why, if we follow the program after the missing quote. bash will continue looking for the closing quote until it finds one, which it does immediately after the second echo command. bash becomes very confused after that, and the syntax of the if command is broken because the fi statement is now inside a quoted (but open) string.

In long scripts, this kind of error can be quite hard to find. Using an editor with syntax highlighting will help. If a complete version of vim is installed, syntax highlighting can be enabled by entering the command:

```
:syntax on
```

## Missing Or Unexpected Tokens

Another common mistake is forgetting to complete a compound command, such as if or
