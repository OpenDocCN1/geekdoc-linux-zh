# EXAMPLE 7.16 (CONTINUED)

```
(Output)
10 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 9 bottles of beer on the shelf!
9 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 8 bottles of beer on the shelf!
8 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 7 bottles of beer on the shelf!
< continues >
2 bottles of beer on the shelf on the shelf. Take one down and pass it all around.
Now 1 bottle of beer on the shelf!
1 bottle of beer on the shelf on the shelf. Take one down and pass it all around.
Now 0 bottles of beer on the shelf!
Party's over.
```

# EXPLANATION

+   1. The initialization of all scalars is done in the first expression of the *for* loop. Each initialization is separated by a comma, or the expression is terminated with a semicolon. The first expression is executed only once, when the loop starts. The second expression is the test. If it evaluates to true, the statements in the block are executed. After the last statement in the block is executed, the third expression is evaluated. The control is then passed to the second expression in the *for* loop, and so on.
+   2. The block is executed if the second expression in the *for* loop is evaluated as true.
+   3. This statement will be tested and, if the condition is true, the statement will be executed and control will go to the third expression within the *for* loop, incrementing *$count* for the last time.

# 7.3.5 The *foreach* (*for*) Loop

If you need to iterate through an array or hash such as a list of files, IP or email addresses, keys, values from a hash, and so forth, then the *foreach* loop, as its name implies, is a control structure designed just for you.

The *foreach* loop (a synonym for *for*) iterates over each element in the parenthesized list or an array, aliasing each element of the list to a scalar variable, one after the other, until the end of the list.

The *VARIABLE* is local to the *foreach* block. It will regain its former value when the loop is exited. Any changes made when assigning values to *VARIABLE* will, in turn, affect the individual elements of the array. If *VARIABLE* is not present, the *$_* special scalar variable is implicitly used.