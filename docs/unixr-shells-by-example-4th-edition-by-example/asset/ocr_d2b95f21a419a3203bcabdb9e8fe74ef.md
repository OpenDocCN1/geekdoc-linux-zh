In the C and TC shells:

```
set x = 5
set name = John
set friend = "John Doe"
set empty = ""
```

The shell checks for undefined variables:

```
echo "Hi $firstname"
```

(Output)
firstname: Undefined variable

# EXAMPLE 15.7

```
#!/bin/tcsh
1 set friend1 = "George"
set friend2 = "Jake"
set friend4 = "Danny"
2 echo "Welcome $friend3 "
(Output)
3 friend3: Undefined variable.
```

# EXPLANATION

+   1 Three variables are set. When variables are so similar in thier names, it is easy to mistype one of them later in the program.
+   2 The variable friend3 was never defined.
+   3 The C and TC shells send an error to let you know that you have an undefined variable. The Bourne, Korn, and Bash shells leave a blank line.

# 15.4.2 Incomplete Programming Statements

Missing Keywords. When using a programming statement such as an if statement or while loop, you may accidentally omit part of the statement. For example, you may forget to complete your while loop with the done keyword. Whenever you see an error message concerning unexpected end of file, or if the message points to the line number one past the last (e.g., your script contains 10 lines and the error message refers to line 11), you should check for incomplete programming statements.

Indentation. An easy way to ensure that if/else, while/do/done, case statements, and other constructs are complete is to indent the block of statements under each test expression (at least one tab stop), and move the terminating keyword (done, end, endsW etc.) to line up with the conditional or looping command that it terminates. This is an extremely helpful technique when these constructs are nested.