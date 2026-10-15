# EXPLANATION

1 The read command prints the string after the question mark (?), who was the U.S. President in 1992?, and waits for input from the user. The input will be stored in the variable answer.

2 The while loop is entered and the test command, [[, evaluates the expression. If the variable answer does not equal the string Bush, the body of the loop is entered and commands between the do and done are executed.

3 The do keyword is the start of the loop body.

4 The user is asked to re-enter input.

5 The done keyword marks the end of the loop body. Control is returned to the top of the while loop, and the expression is tested again. As long as $answer does not evaluate to Bush, the loop will continue to iterate. When the user's input is Bush, the loop ends. Program control goes to line 6.

# EXAMPLE 12.35

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