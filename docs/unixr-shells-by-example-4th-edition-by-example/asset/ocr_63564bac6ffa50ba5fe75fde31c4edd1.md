assigned to the variable, and so on. The body of the loop starts at the do keyword and ends at the done keyword. When all of the words in the list have been shifted off, the loop ends and program control continues after the done keyword.

# FORMAT

```
for variable in wordlist
do
    command(s)
done
```

# EXAMPLE 12.29

(The Script)

```
1  for pal in Tom Dick Harry Joe
2  do
3      print "Hi $pal"
4  done
5  print "Out of loop"
```

(The Output)

```
Hi Tom
Hi Dick
Hi Harry
Hi Joe
Out of loop
```

# EXPLANATION

+   1 This for loop will iterate through the list of names, Tom, Dick, Harry, and Joe, shifting each one off (to the left) after it is assigned to the variable pal. As soon as all of the words are shifted and the wordlist is empty, the loop ends and execution starts after the done keyword. The word following the for command, pal, is a variable that will be assigned the value after the in keyword, one at a time, for each iteration of the loop. The first time in the loop, the variable pal will be assigned the word Tom. The second time through the loop, pal will be assigned Dick, the next time pal will be assigned Harry, and the last time, pal will be assigned Joe.
+   2 The do keyword is required after the wordlist. If it is used on the same line, the list must be terminated with a semicolon. For example:
+   for pal in Tom Dick Harry Joe; do
+   3 This is the body of the loop. After Tom is assigned to the variable pal, the commands in the body of the loop, that is, all commands between the do and the done keywords, are executed.
+   4 The done keyword ends the loop. If there are no words left to be processed in the wordlist on line 1, the loop exits, and execution starts at line 5.
+   5 This line is executed when the loop terminates.