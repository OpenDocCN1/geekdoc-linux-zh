```
done
$ 
```

If you run the `test7.sh` shell script you see a listing of the files and directories in your home directory:

```
$ chmod u+x test7.sh
$ ./test7.sh
Desktop is a directory
Documents is a directory
Downloads is a directory
Music is a directory
Pictures is a directory
Public is a directory
Templates is a directory
test1.sh is a file
test2.sh is a file
test3.sh is a file
test4.sh is a file
test5.sh is a file
test6.sh is a file
test7.sh is a file
today.txt is a file
Videos is a directory
$ 
```

That saves a lot of coding from having to check each file manually in a bunch of `if-then` or `case` statements!

# ## The while loop

Another useful loop statement is the `while` command. This is its format:

```
while [ condition ] ; do
commands
done
```

The `while` loop keeps looping as long as the *condition* specified evaluates to a `True` logical value. When the condition evaluates to a `False` logical value the looping stops. The condition used in the `while` loop is the same as that for the `if-then` statement, so you can test numbers, strings, and files. Here’s an example that demonstrates using the `while` loop to calculate the factorial of a number. (The factorial of a number is the multiplication of all the preceding numbers, making this a perfect application for a loop.)