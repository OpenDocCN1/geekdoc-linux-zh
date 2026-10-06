# 'Round and 'Round She Goes

In this chapter you'll learn how to set up program loops. These loops will enable you to execute a set of commands either a specified number of times or until a specific end condition is met.

The three built-in looping commands for shell programming are

+   - for
- while
- until

You'll learn about each one of these loops in separate sections of this chapter.

# The for Command

The for command is used to execute one or more commands a specified number of times. Its basic format is as shown:

```
for var in word_1, word_2, ... word_n
do
  command
  command
  ...
done
```

The commands enclosed between the do and the done are what's known as the body of the loop and are executed for as many items as listed after the in. When the loop is executed, the first word, word_i, is assigned to the variable var, and the body of the loop is then executed. Next, the second word in the list, word_j, is assigned to var, and the body of the loop is executed again.