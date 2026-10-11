
I will now enter the writing phase and show you how you can write a shell script. The language of the script is simple. See the script as under:

```bash
[gha@localhost ~]$ echo 'I am learning Linux'
I am learning Linux
```

This is shell scripting. Now I will add a comment to the same script.

```bash
[gha@localhost ~]$ echo 'I am learning Linux' # I have added a comment to the code.
I am learning Linux
```

Now you have to make the script executable. See the following:

```bash
[gha@localhost ~]$ ls -l Linux_learning
[gha@localhost ~]$ chmod 755 Linux_learning
```

The text Linux_learning is the name of the file in which I had saved the script. The chmod command is used to make the script executable in Linux.

## Displaying Text

Most of the shell commands tend to produce a specific output, which is displayed on your console monitor where you are running the script. You may need to add text messages to help out the script user know what is going to happen inside the script. You can do this by using the echo command I have talked about in the past section. The echo command displays simple text strings. There are different techniques to write a script with the echo command. I will explore all of them.

```bash
[gha@localhost ~]$ echo I am learning Linux shell scripting
I am learning Linux shell scripting
```

The most remarkable thing is that you do not have to use quotes to enclose the string text, as is the case with other programming languages. However, sometimes it becomes necessary to use quotes. Either you need single or double quotes to display the text strings.

```bash
[gha@localhost ~]$ echo 'I am learning Linux shell scripting.'
I am learning Linux shell scripting
```

In the next example, using quotes is going to be inevitable.

```bash
[gha@localhost ~]$ echo "Adam says, \"I am learning Linux shell scripting.\""
Adam says, "I am learning Linux shell scripting."
```

You can see that when you have to add a text that is in the form of direct speech, you will have to add quotation marks to the text.

## The if-then Statement

Many Linux shell scripting programs require some logic flow control between different commands inside the script, which means that the shell tends to execute different commands. In addition, it keeps the ability to execute different other commands that permit the script to loop through the commands based on the result of different other commands. We refer to them as structured commands. They are also known as conditionals.

Structured commands allow you to shift the flow of the operations of a program. Some commands are executed, while others are skipped when they are caught up in certain conditions. In other programming languages, the object after an if statement is the equation that the system evaluates for True or False grounds. The bash shell if statement does not work that way. Instead, it runs the command that is defined on the if line. If this command's exit status is considered zero, the commands that are listed under the then section tend to execute. If this command's exit status is something else, the then commands are put on hold, and the bash shell jumps over to the next command in the script.

```bash
$ cat testing5
#!/bin/bash
# I am now testing the if statement for bash shell
if date
then
    echo "The structured command has completely worked"
fi

$ bash -f main.sh
Tue Jan 26 05:02:54 UTC 2021
The structured command has completely worked
```

The script has used the date command on the if line. If this command is executed successfully, the echo statement must display the text string. When you are running the script from the command line, you will be getting the same results as above. The shell will execute the date command. Since the exit status was zero, it will also execute the echo statement that is listed in the then section. In the next example, I will test a bad command to see how it works.

```bash
$ cat testing2
#!/bin/bash
# It is time to run a test on a bad command
if hgjdksslh
then
    echo "it is not going to work"
fi
    echo "I cannot run the command because you're out of the if statement."

$ bash -f main.sh
    I cannot run the command because you're out of the if statement
```

Since the above command was a bad command, it produced an exit status that is at the moment a non-zero. The bash shell will skip the echo statement in the then section.

## The if-then-else Statement

The if-then statement provides one option to determine whether the command is successful. If a non-zero exit status code is returned, the bash shell goes to the next script command. In a situation like this, it would best if we had another set of commands we could execute, and that is where the if-then-else statement comes in.

If the if-statement command produces the exit status zero code, the commands in the then part of the statement are executed. If a non-zero exit status code is returned, the commands in the else part of the statement are executed.

```bash
$ cat testing4
#!/bin/bash
# I am now going to test the else section
testinguser=thisisabadtest
if grep $testinguser /etc/passwd
then
    echo "The files for user $testinguser are:"
    ls -a /home/$testinguser/b*
else
    echo "The user name $testinguser cannot be found on the system"
fi

$ ./test4
The user name thisisabadtest cannot be found on the system

$ bash -f main.sh
The user name thisisabadtest cannot be found on the system
```

On occasion, you may need to check things in the script code. Rather than separate if-then statements, a different version of the else statement can be used. This is called the elif, and this continues the else statement with a subsequent if-then statement. It provides a different evaluation command, which is much like the first if statement. If a zero exit status code is returned, the commands in the second then statement are executed by the bash shell.

## Advanced if-then Features

There is a double parentheses command in Linux that allows you to incorporate some advanced mathematical formulas when you are making comparisons. The test command permits simple operations in comparison. However, the double parentheses command offers more mathematical symbols that a number of programmers from different other languages are using.

The expression term may be any kind of mathematical assignment or expression. Besides the standard operators that the test command uses, additional operators are available for use in the double parentheses command.

You also can use the double bracket command for advanced features to do string comparisons. The double bracket command format uses the standard string comparison that we have used in the test command. Where it differs is by the option of pattern matching. You will be able to define a regular expression that you need to match against the string value.

```bash
$ cat testing2
#!/bin/bash
# I will now be using pattern matching
if [[ $MyUSER == r* ]]
then
    echo "Hello $MyUSER I know you from the days when you used to work in a restaurant in Europe."
else
    echo "Sorry, I have never seen you before. I don't know you."
fi

$ bash -f main.sh
Sorry, I have never seen you before. I don’t know you.
```

More often, you may find yourself attempting to evaluate the value of some variables in a bid to find out a specific value inside a set of possible values. In this typical scenario, you may end up writing a lengthy if-then-else statement such as the following:

```bash
$ cat testing555
#!/bin/bash
# I am now looking for some possible values
if [ $MyUSER = "rich" ]
then
    echo "Welcome $MyUSER to the heavens on the earth."
    echo "Please enjoy your visit in plush green fields and lush green mountains. I wonder if you want to take a bath in the river beneath the valley."
elif [ $MyUSER = Jason ]
then
    echo "Welcome $MyUSER to the lakes of Madora."
    echo "Please enjoy your stay in the shining waters of Madora lakes. I hope you enjoy the resorts, the sun, the breeze, the food, and the drinks."
elif [ $MyUSER = Simra ]
then
    echo "Welcome $MyUSER to the lakes of Madora."
    echo "Please enjoy your stay in the shining waters of Madora lakes. I hope you enjoy the resorts, the sun, the breeze, the food, and the drinks."
elif [ $MyUSER = Linda ]
then
    echo "Don't forget to logout when you're done"
else
    echo "Sorry, you're not allowed here"
fi
```

## The for Command

Iterations through a series of commands is normal practice when it comes to programming. Many a time, you may have to repeat different commands. Often you need to repeat a bunch of commands until the program meets a specified condition like processing files inside a directory or in all the lines inside a text file.

The bash shell offers the for command to develop a loop that iterates through a set of values. Each iteration tends to perform a set of commands by using a single value inside the series. One of the most basic uses of the for command is iteration through a list of values that are defined inside the for command itself.

```bash
$ cat testing111
#!/bin/bash
# This is the basic for command in Linux
for mytest in Alabama Texas Alaska Virginia Arizona Ohio Arkansas South Dakota California North Dakota Colorado New Jersey Florida Michigan
```
