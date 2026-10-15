# EXPLANATION

+   1 The script name is runit; the command-line arguments are f1, f2, f3, dir2, and dir3.
+   2 The $* variable evaluates to a list of all the arguments (positional parameters) passed in at the command line. The foreach command processes, in turn, each of the words in the wordlist, f1, f2, f3, dir2, and dir3. Each time through the loop, the first word in the list is assigned to the variable arg. After a word is assigned, it is shifted off (to the left) and the next word is assigned to arg, until the list is empty.
+   3 The commands in this block are executed for each item in the list until the end statement is reached.
+   4 The end statement terminates the loop after the wordlist is empty.
+   5 After the loop ends, the program continues to run.

# 10.7.2 The while Loop

The while loop evaluates an expression, and as long as the expression is true (nonzero), the commands below the while command will be executed until the end statement is reached. Control will then return to the while expression, the expression will be evaluated, and if still true, the commands will be executed again, and so on. When the while expression is false, the loop ends and control starts after the end statement.

# EXAMPLE 10.40

```
(The Script)
#!/bin/csh -f
1 set num = 0
2 while ($num < 10)
3   echo $num
4   @ num++      # See arithmetic.
5 end
6 echo "Program continues here"
```

# EXPLANATION

+   1 The variable num is set to an initial value of 0.
+   2 The while loop is entered and the expression is tested. If the value of num is less than 10, the expression is true, and lines 3 and 4 are executed.
+   3 The value of num is displayed each time through the loop.
+   4 The value of the variable num is incremented. If this statement were omitted, the loop would continue forever.
+   5 The end statement terminates the block of executable statements. When this line is reached, control is returned to the top of the while loop and the expression is evaluated again. This continues until the while expression is false (i.e., when $num is 10).
+   6 Program execution continues here after the loop terminates.