Piping the Output of a Loop to a UNIX Command. Output can be either piped to another command(s) or redirected to a file.

# EXAMPLE 8.43

(The Script)

```
#!/bin/sh
1 for i in 7 9 2 3 4 5
2 do
    echo $i
3 done | sort -n
```

(The Output)

```
2
3
4
5
7
9
```

# EXPLANATION

+   1 The for loop iterates through a list of unsorted numbers.
+   2 In the body of the loop, the numbers are printed. This output will be piped into the UNIX sort command, a numerical sort.
+   3 The pipe is created after the done keyword. The loop is run in a subshell.

# 8.6.8 Running Loops in the Background

Loops can be executed to run in the background. The program can continue without waiting for the loop to finish processing.

# EXAMPLE 8.44

(The Script)

```
#!/bin/sh
1 for person in bob jim joe sam
2 do
    mail $person < memo
3 done &
```

# EXPLANATION

+   1 The for loop shifts through each of the names in the wordlist: bob, jim, joe, and sam. Each of the names is assigned to the variable person, in turn.
+   2 In the body of the loop, each person is sent the contents of the memo file.
+   3 The ampersand at the end of the done keyword causes the loop to be executed in the background. The program will continue to run while the loop is executing.