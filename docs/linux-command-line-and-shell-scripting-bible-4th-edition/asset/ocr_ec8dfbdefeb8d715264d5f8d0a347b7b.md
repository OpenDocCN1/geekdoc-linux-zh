# CHAPTER 12

# Using Structured Commands

# IN THIS CHAPTER

+   * Working with the if-then statement
+   * Nesting ifs
+   * Understanding the test command
+   * Testing compound conditions
+   * Using double brackets and parentheses
+   * Looking at case

In Chapter 11, “Basic Script Building,” the shell processed each individual command in the order in which it appeared within a shell script. Although this works out fine for sequential operations, many programs require some sort of logic flow control between the commands in the script.

There is a whole command class that allows the shell to skip over script sections based on tested conditions and alter the operation flow. These commands are generally referred to as structured commands.

Quite a few structured commands are available in the Bash shell, so we’ll break them up into different chapters. In this chapter, we look at if-then and case statements.

# Working with the if-then Statement

The most basic type of structured command is the if-then statement. The if-then statement has the following format:

```
if command
then commands
fi
```