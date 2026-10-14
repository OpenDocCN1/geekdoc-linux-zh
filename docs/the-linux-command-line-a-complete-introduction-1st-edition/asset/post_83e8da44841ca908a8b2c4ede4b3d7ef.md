
where variable is the name of a variable that will increment during the execution of the loop, words is an optional list of items that will be sequentially assigned to variable, and commands are the commands that are to be executed on each iteration of the loop.

The for command is useful on the command line. We can easily demonstrate how it works:

```
[me@linuxbox ~]$ for i in A B C D; do echo $i; done
A
B
C
D
```

In this example, for is given a list of four words: A, B, C, and D. With a list of four words, the loop is executed four times. Each time the loop is executed, a word is assigned to the variable i. Inside the loop, we have an echo command that displays the value of i to show the assignment. As with the while and until loops, the done keyword closes the loop.

The really powerful feature of for is the number of interesting ways we can create the list of words. For example, we can use brace expansion:

```
[me@linuxbox ~]$ for i in {A..D}; do echo $i; done
A
B
C
D
```

or pathname expansion:

```
[me@linuxbox ~]$ for i in distros*.txt; do echo $i; done
distros-by-date.txt
distros-dates.txt
distros-key-names.txt
distros-key-vernums.txt
distros-names.txt
distros.txt
distros-vernums.txt
distros-versions.txt
```

or command substitution:

```bash
#!/bin/bash

# longest-word : find longest string in a file

while [ -n "$1" ]; do
    if [ -r "$1" ]; then
        max_word=
        max_len=0
        for i in $(strings "$1"); do
            len=$(echo "$i" | wc -c)
            if (( len > max_len )); then
                max_len=$len
                max_word=$i
            fi
        done
        echo "$1: '$max_word' ($max_len characters)"
    fi
    shift
done
```

In this example, we look for the longest string found within a file. When given one or more filenames on the command line, this program uses the strings program (which is included in the GNU binutils package) to generate a list of readable text "words" in each file. The for loop processes each word in turn and determines if the current word is the longest found so far. When the loop concludes, the longest word is displayed.

If the optional in words portion of the for command is omitted, for defaults to processing the positional parameters. We will modify our longest-word script to use this method:

```bash
#!/bin/bash

# longest-word2 : find longest string in a file

for i; do
    if [[ -r $i ]]; then
        max_word=
        max_len=0
        for j in $(strings "$i"); do
            len=$(echo "$j" | wc -c)
            if (( len > max_len )); then
                max_len=$len
                max_word=$j
            fi
        done
        echo "$i: '$max_word' ($max_len characters)"
    fi
done
```

As we can see, we have changed the outermost loop to use for in place of while. Because we omitted the list of words in the for command, the positional parameters are used instead. Inside the loop, previous instances of the variable i have been changed to the variable j. The use of shift has also been eliminated.

## WHY I?

You may have noticed that the variable i was chosen for each of the for loop examples above. Why? No specific reason actually, besides tradition. The variable used with for can be any valid variable, but i is the most common, followed by j and k.

The basis of this tradition comes from the Fortran programming language. In Fortran, undeclared variables starting with the letters I, J, K, L, and M are automatically typed as integers, while variables beginning with any other letter are typed as real (numbers with decimal fractions). This behavior led programmers to use the variables i, j, and k for loop variables, since it was less work to use them when a temporary variable (as a loop variable often was) was needed. It also led to the following Fortran-based witticism: "GOD is real, unless declared integer."

## for: C Language Form

Recent versions of bash have added a second form of for-command syntax, one that resembles the form found in the C programming language. Many other languages support this form, as well.

```
for (( expression1; expression2; expression3 )); do
    commands
done
```

where expression1, expression2, and expression3 are arithmetic expressions and commands are the commands to be performed during each iteration of the loop.

In terms of behavior, this form is equivalent to the following construct:

```
(( expression1 ))
while (( expression2 )); do
    commands
    (( expression3 ))
done
```

expression1 is used to initialize conditions for the loop, expression2 is used to determine when the loop is finished, and expression3 is carried out at the end of each iteration of the loop.

Here is a typical application:

```bash
#!/bin/bash

# simple_counter: demo of C style for command

for (( i=0; i<5; i=i+1 )); do
    echo $i
done
```

When executed, it produces the following output:

```
[me@linuxbox ~]$ simple_counter
0
1
2
3
4
```

In this example, expression1 initializes the variable i with the value of 0, expression2 allows the loop to continue as long as the value of i remains less than 5, and expression3 increments the value of i by 1 each time the loop repeats.
