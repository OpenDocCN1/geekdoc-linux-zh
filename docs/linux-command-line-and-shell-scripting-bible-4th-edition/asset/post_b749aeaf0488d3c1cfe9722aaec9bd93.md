
than symbol, followed by the name of the file to capture the output. You can append output data to an existing file by using two greater-than symbols. The less-than symbol is used to redirect input to a command. You can redirect input from a file to a command.

The Linux pipe command (the broken bar symbol) allows you to redirect the output of a command directly to the input of another command. The Linux system runs both commands at the same time, sending the output of the first command to the input of the second command without using any redirect files.

The Bash shell provides a couple of ways for you to perform mathematical operations in your shell scripts. The expr command is a simple way to perform integer math. In the Bash shell, you can also perform basic math calculations by enclosing equations in square brackets, preceded by a dollar sign. To perform floating-point arithmetic, you need to use the bc calculator command, redirecting input from inline data and storing the output in a user variable.

Finally, we discussed how to use the exit status in your shell script. Every command that runs in the shell produces an exit status. The exit status is an integer value between 0 and 255 that indicates whether or not the command completed successfully, and if not, what the reason may have been. An exit status of 0 indicates that the command completed successfully. You can use the exit command in your shell script to declare a specific exit status upon the completion of your script.

So far in your shell scripts, things have proceeded in an orderly fashion from one command to the next. In the next chapter, you'll see how you can use some logic flow control to alter which commands are executed within the script.

# CHAPTER 12

# Using Structured Commands

## IN THIS CHAPTER

- Working with the if-then statement
- Nesting ifs
- Understanding the test command
- Testing compound conditions
- Using double brackets and parentheses
- Looking at case

In Chapter 11, “Basic Script Building,” the shell processed each individual command in the order in which it appeared within a shell script. Although this works out fine for sequential operations, many programs require some sort of logic flow control between the commands in the script.

There is a whole command class that allows the shell to skip over script sections based on tested conditions and alter the operation flow. These commands are generally referred to as structured commands.

Quite a few structured commands are available in the Bash shell, so we’ll break them up into different chapters. In this chapter, we look at if-then and case statements.

## Working with the if-then Statement

The most basic type of structured command is the if-then statement. The if-then statement has the following format:

```bash
if command
then commands
fi
```

If you're using `if`-`then` statements in other programming languages, this format may be somewhat confusing. In other programming languages, the object after the `if` statement is an equation that is evaluated for a `true` or `false` value. That's not how the Bash shell `if` statement works.

The Bash shell `if` statement runs the command defined on the `if` line. If the exit status of the command (see [Chapter 11](Chapter11)) is zero (the command completed successfully), the commands listed under the `then` section are executed. If the exit status of the command is anything else, the `then` commands aren't executed, and the Bash shell moves on to the next command in the script. The `fi` statement sets the `if`-`then` statement's end.

Here's a simple example to demonstrate this concept:

```bash
$ cat test1.sh
#!/bin/bash
# testing the if statement
if pwd
then
  echo "It worked"
fi
$
```

This script uses the `pwd` command on the `if` line. If the command completes successfully, the `echo` statement should display the text string. When we run this script from the command line, we get these results:

```bash
$ ./test1.sh
/home/christine/scripts
It worked
$
```

The shell executed the `pwd` command listed on the `if` line. Because the exit status was zero, it also executed the `echo` statement listed in the `then` section.

Here's another example:

```bash
$ cat test2.sh
#!/bin/bash
# testing an incorrect command
if IamNotaCommand
then    echo "It worked"
fi
echo "We are outside the if statement"
$
./test2.sh
./test2.sh: line 3: IamNotaCommand: command not found
We are outside the if statement
$
```

In this example, we deliberately used a nonexistent command, IamNotaCommand, in the `if` statement line. Because this is an incorrect command, it produces an exit status that's non-zero. Thus, the Bash shell skips the `echo` statement in the `then` section. Also notice that the error message generated from running the command in the `if` statement still appears in the script's output. There may be times when you don't want an error statement to appear. Chapter 15, “Presenting Data,” discusses how this can be avoided.

> ### NOTE
>
> You might see an alternative form of the `if-then` statement used in some scripts:
>
> ```
> if command; then
>    commands
> fi
> ```
>
> By putting a semicolon (`;`) at the end of the command to evaluate, you can include the `then` statement on the same line, which looks closer to how `if-then` statements are handled in some other programming languages.

You are not limited to just one command in the `then` section. You can list commands just as you do in the rest of the shell script. The Bash shell treats the commands as a block, executing all of them when the command in the `if` statement line returns a zero exit status or skipping all of them when the command returns a non-zero exit status:

```bash
$ cat test3.sh
#!/bin/bash
# testing multiple commands in the then block
#
testuser=christine
#
if grep $testuser /etc/passwd
then
    echo "This is my first command in the then block."
    echo "This is my second command in the then block."
    echo "I can even put in other commands besides echo:"
    ls /home/$testuser/*.sh
fi
echo "We are outside the if statement"
```

The if statement line uses the grep command to search the /etc/passwd file to see if a specific username is currently used on the system. If there’s a user with that logon name, the script displays some text and then lists the Bash scripts in the user’s $HOME directory:

```bash
$ ./test3.sh
christine:x:1001:1001::/home/christine:/bin/bash
This is my first command in the then block.
This is my second command in the then block.
I can even put in other commands besides echo:
/home/christine/factorial.sh
We are outside the if statement
$
```

However, if you set the testuser variable to a user that doesn’t exist on the system, nothing within the then code block executes:

```bash
$ cat test3.sh
#!/bin/bash
# testing multiple commands in the then block
#
testuser=NoSuchUser
#
if grep $testuser /etc/passwd
then
    echo "This is my first command in the then block."
    echo "This is my second command in the then block."
    echo "I can even put in other commands besides echo:"
    ls /home/$testuser/*.sh
fi
echo "We are outside the if statement"
$ ./test3.sh
We are outside the if statement
$
```

It's not all that exciting. It would be nice if we could display a little message saying that the username wasn't found on the system. Well, we can, using another feature of the if-then statement.

## Exploring the if-then-else Statement

In the if-then statement, you have only one option for whether a command is successful. If the command returns a non-zero exit status code, the Bash shell just moves on to the next command in the script. In this situation, it would be nice to be able to execute an alternate set of commands. That's exactly what the if-then-else statement is for.

The if-then-else statement provides another group of commands in the statement:

```bash
if command
then
commands
else
commands
fi
```

When the command in the if statement line returns with a zero exit status code, the commands listed in the then section are executed, just as in a normal if-then statement. When the command in the if statement line returns a non-zero exit status code, the Bash shell executes the commands in the else section.

Now you can copy and modify the test script to include an else section:

```bash
$ cp test3.sh test4.sh
$
$ nano test4.sh
$
$ cat test4.sh
#!/bin/bash
# testing the else section
#
testuser=NoSuchUser
```
