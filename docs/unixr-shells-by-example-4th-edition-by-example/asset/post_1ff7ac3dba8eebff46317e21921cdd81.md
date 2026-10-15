
## 12.6.2 The $* and $@ Variables in Wordlists

When expanded, the $* and $@ are the same unless enclosed in double quotes. "$*" evaluates to one string, whereas "$@" evaluates to a list of separate words.

### EXAMPLE 12.32

```
(The Script)
#!/bin/ksh
1 for name in $*   # or for name in $@
2 do
3   echo Hi $name
done

(The Command Line)
$ greet Dee Bert Lizzy Tommy
Hi Dee
Hi Bert
Hi Lizzy
Hi Tommy
```

### EXPLANATION

- 1 $* and $@ expand to a list of all the positional parameters; in this case, the arguments passed in from the command line: Dee, Bert, Lizzy, and Tommy. Each name in the list will be assigned, in turn, to the name variable in the for loop.
- 2 The commands in the body of the loop are executed until the list is empty.
- 3 The done keyword marks the end of the loop body.

## 12.6.3 The while Command

The while evaluates the command immediately following it, and if its exit status is 0, the commands in the body of the loop (commands between do and done) are executed. When the done keyword is reached, control is returned to the top of the loop and the while command checks the exit status of the command again. Until the exit status of the command being evaluated by the while becomes nonzero, the loop continues. When the exit status reaches nonzero, program execution starts after the done keyword. If the exit status never becomes nonzero, the loop goes around and around infinitely. (Of course, pressing Ctrl-C or Ctrl-\ will stop the looping.)

### FORMAT

```
while command
do
    command(s)
done
```

### EXAMPLE 12.33

(The Script)

```
1 num=0        # Initialize num
2 while (( num < 10 ))  # Test num with the let
do
    print -n $num
3    (( num=num + 1 ))  # Increment num
done
print "\nAfter loop exits, continue running here"
```

(The Output)

```
0123456789
After loop exits, continue running here
```

### EXPLANATION

- 1. This is the initialization step. The variable num is assigned 0.
- 2. The while command is followed by the let command. If the value of num is less than 10, the body of the loop is entered.
- 3. In the body of the loop, the value of num is incremented by one. If the value of num was never changed, the loop would iterate infinitely or until the process was killed.

### EXAMPLE 12.34

(The Script)

```
#!/bin/ksh
# Scriptname: quiz
1 read answer?"Who was the U.S. President in 1992? "
2 while [[ $answer != "Bush" ]]
do
4   print "Wrong try again!"
5   read answer
done
6 print Good guess!
```

(The Output)

```
$ quiz
Who was the U.S. President in 1992? George
Wrong try again!
Who was the U.S. President in 1992? I give up
Wrong try again!
Who was the U.S. President in 1992? Bush
Good guess!
```

### EXPLANATION

1 The read command prints the string after the question mark (?), who was the U.S. President in 1992?, and waits for input from the user. The input will be stored in the variable answer.

2 The while loop is entered and the test command, [[, evaluates the expression. If the variable answer does not equal the string Bush, the body of the loop is entered and commands between the do and done are executed.

3 The do keyword is the start of the loop body.

4 The user is asked to re-enter input.

5 The done keyword marks the end of the loop body. Control is returned to the top of the while loop, and the expression is tested again. As long as $answer does not evaluate to Bush, the loop will continue to iterate. When the user's input is Bush, the loop ends. Program control goes to line 6.

### EXAMPLE 12.35

(The Script)

```
1 go=1
print Type q to quit.
2 while let go or (( go ))
do
    print I love you.
    read word
3 if [[ $word = [qQ] ]]
then
    print "I'll always love you"
    go=0
4
5 fi
done
```

(The Output)

```
$ sayit
Type q to quit.
I love you.
I love you.
I love you.
I love you.
I love you.
q
I'll always love you
$
```

### EXPLANATION

- 1 The variable go is assigned 1.
- 2 The loop is entered. The let command tests the expression. The expression evaluates to one. The program goes into the body of the while loop and executes commands from the do keyword to the done keyword.
- 3 If the user enters a q or Q as input to the variable word, the commands between then and fi are executed. Anything else will cause I love you. to be displayed.
- 4 The variable go is assigned 0. When program control starts at the top of the while loop, the expression will be tested. Because the expression evaluates to false, the loop exits and the script starts execution after the done keyword on line 5.
- 5 The done marks the end of the body of the loop.

## 12.6.4 The until Command

The until command is used like the while command, but evaluates the exit status in the opposite way. The until evaluates the command immediately following it, and if its exit status is not 0, the commands in the body of the loop (commands between do and done) are executed. When the done keyword is reached, control is returned to the top of the loop and the until command checks the exit status of the command again. Until the exit status of the command being evaluated by until becomes 0, the loop continues. When the exit status reaches 0, program execution starts after the done keyword.

### FORMAT

```
until command
 do
   command(s)
 done
```

### EXAMPLE 12.36

```
#!/bin/ksh
until who | grep linda
do
  sleep 5
done
talk linda@dragonwings
```

### EXPLANATION

- 1 The until loop tests the exit status of the last command in the pipeline, grep. The who command lists who is logged on this machine and pipes its output to grep. The grep command will return 0 exit status (success) only when it finds user linda.
- 2 If user linda has not logged in, the body of the loop is entered and the program sleeps for 5 seconds.
- 3 When linda logs on, the exit status of the grep command will be 0 and control will go to the statements following the done keyword.
