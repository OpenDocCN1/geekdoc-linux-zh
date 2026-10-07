
# Chapter 6: ADVANCED VARIABLE USAGE 321

site if you have trouble figuring out the arithmetic expression that will do this.) The following would be a possible interaction you could have with your functions:

```
[6128]: init_bd
[6129]: from.row=1 from.col=7 to.row=3 to.col=6
[6130]: move_pc from to
[6131]: show_bd
br bk bk bp bk bk bk br
bp bp bp bp bp bp bp bp
-- -- -- -- -- -- -- --
-- -- -- -- wk -
wp wp wp wp wp wp wp wp
wr wk wb wq wk wb -- wr
[6132]:
```

-   Write a function named reminder that takes two arguments. The first one is a string specifying a date or time, and the second one a string containing a message. Write a second function named todo that takes a date or time string as an argument and prints the date/time string and its associated message. The following would be a possible interaction you could have with your functions:

```
[6132]: reminder 4:15 "Get a snack."
[6133]: reminder 4:30 "Drink some coffee."
[6134]: todo 4:15
4:15: Get a snack.
[6135]: todo 5:30
5:30:
[6136]: todo 4:30
4:30: Drink some coffee.
[6137]:
```

# CHAPTER 7

# BASIC TESTS

There will be a test on this next Tuesday.

# CHAPTER OBJECTIVES

- In this chapter, you will learn about:
* The if Command Page 324
* The [[ Command ... ]] Operator Page 345

Scripts and functions would have pretty limited usefulness if they could only run a fixed list of commands each time they are run. In this chapter, you will learn the if built-in commands provided by the KornShell for controlling which commands get executed based on the outcomes of various tests. You also learn to use the double-bracket operator [[ ... ]] to make those tests. By the end of this chapter, you can start writing "real" programs that make decisions about commands to run as execute.

You use the commands in this chapter and the next to implement control structures, in which you group other commands in ways not covered in Chapter 2, "Command Line Syntax". Each type of control structure consists of two or more built-in commands (a compound command) that mark the parts of the control structure, as well as other commands (of any type) that make up the body of the control structure. For example, the first compound command you will look at has at least three parts: if, then, and fi. We will use the term statement to refer to entire control structure, including both the compound command that marks the parts of the structure and the other commands that are the subjects of the control structure.

# LAB 7.1

# THE if COMMAND

| LAB OBJECTIVES |
| :--- |
| After this lab, you will be able to: <br>- Write a Simple if, then, ... else Statement <br>- Use if to Test the Outcome of External Commands <br>- Use an Alternative Way to Test a Command |

This first control statement follows very closely the way we talk about decision making in everyday life. "If something is true, then I will do one thing, else I will do another thing." For the if command, something is true means execute some commands and test whether the exit code of the last one is true. I will do one thing and I will do another thing mean execute some commands. That is, with the if command, you test the result of executing one set of commands to decide which of two other sets of commands to execute.

# SYNTAX DIAGRAMS

The previous paragraph gives an informal sense of what an if command does, but it doesn't tell you all the details about how to write an if command, and it doesn't tell you about the variations that you can use when writing if commands. All that detailed information can be expressed very concisely using a table called a syntax diagram. Once you know how to read the syntax diagram for a command, you will have all the information you need to be able to use the command in any situation you desire.

# Chapter 7: Basic Tests 325

You already saw a form of syntax diagram in the "syntax synopsis" introduced in Lab 2.1, "Command Parts"; syntax diagrams are just another form for the same information.

LAB 7.1

# FOR EXAMPLE

To show you how syntax diagrams work, here is the one for the if command, followed by an explanation. This syntax diagram has line numbers in the left column to make it easier to talk about the diagram itself. We will not bother to number the lines in future syntax diagrams.

```
1. if Command ...
2. then Command ...
3. [ elif Command ...
4. then Command ... ]
5. ...
6. [ else Command ... ]
7. fi
```

- Line 1 shows that if an if command starts with the if keyword, followed by any number of commands. (ellipses (...) after Command means you can have any number of additional commands after the first.)
- The second line says that after the if command line, there must be a command that starts with the then keyword, followed by any number of commands.
- Lines 3 and 4 are inside square brackets, which means that they are optional. If you want to, you may put in a command starting with the elif keyword, followed by any number of commands. If you do use elif, it must be followed by a command that starts with the then keyword, followed by any number of commands.
- Line 5 uses ellipses to show what precedes it (i.e., lines 3 and 4) may be repeated any number of times. In this case, "any number of times" might be zero because of the square brackets around lines 3 and 4.

# LAB 7.1: THE if COMMAND

- Line 6 is also optional, as indicated by the square brackets around it. It shows that after the then part and any elif parts, you can start a command with else, followed by any number of commands.

- The last line shows that there has to be a fi (that's if spelled backward) to mark the end of an if command.

There are several points to make about this syntax diagram. The first point is that the phrase any means "one or more complete command lines." You can write anything that would be a valid command line, including command sequences, pipelines, and the other types of command lines introduced in Chapter 2, "Command Syntax".

The ability to put command sequences, command groups, and other structures inside the parts of a control structure is extremely powerful. However, this feature lets you write complex programs. Beginning programmers tend to produce more complex programs than advanced programmers, who learn how to write efficient programs. Strive to make your programs simple. If your code starts to get complex, think about how to write it more simply.

img/694fa9f0320e707804ac650b9609b4_345_0.png

The next point is that there must be an if, a then, and a fi—in that sequence.

If there is an else, it must be the last part of the if structure before the fi.

The elif keyword is a contraction for else if. I've included it in the syntax diagram for completeness, but if you need the logical feature it provides, you can often accomplish the same thing more clearly and at least as efficiently by using the case command introduced in Chapter 9, "The Case and Select Commands."

Avoid elif. It can lead to programs that are hard to understand, debug, and modify. If you can, use case statements instead.

img/694fa9f0320e707804ac650b9609b4_345_1.png

# LAB 7.1 EXERCISES

7.1.1 WRITE A SIMPLE IF then, ... else STATEMENT

This exercise uses the KornShell's built-in commands, print, true, and false. If you are not comfortable with these commands, you should review Chapter 2,“Command Syntax,” where they were introduced.

Look at the following commands and see if you can predict what will be printed:

```
if true
then print yes
else print no
fi
```

-   a) Type in these commands. What printed, and why?

Now, look at the following commands and see if you can predict what will be printed:

```
if true && false
then print ok 1
print ok 2
print ok 3
else print not ok 1
print not ok 2
fi
```

-   b) Type in these commands. What printed, and why?
