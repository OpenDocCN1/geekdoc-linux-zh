without a command line argument or with more than one argument. The second and third if statements, respectively, check if the file specified as command line argument exists and is not a directory. The fourth if statement is executed if you run the script with only one command line argument that exists in your directory hierarchy and is not a directory. It produces the desired results if the command line argument is an ordinary file. If the passed argument is not an ordinary file, the condition for the second if statement is false and the error message if_demo1: argument must be an ordinary file is displayed. Note that the exit status of the script is 1 when it exits because of an erroneous condition, and 0 when the script executes successfully and produces the desired results.

An important practice in script writing is to correctly indent the commands/statements in it. Proper indentation of programs enhances their readability, making them easier to understand, debug, and maintain (add or remove features). Note the indentation style used in the sample scripts presented in this textbook and follow it when you write scripts.

The second instance of the if statement syntax also allows two-way branching. The following is a brief description of the statement.

# SYNTAX

```
if (expression) then
then-commands
else
else-commands
endif
```

Purpose: To implement two-way branching

If expression is true, the commands in then-commands are executed; otherwise, the commands in else-commands are executed, followed by the execution of the first command after endif. The semantics of the statement are shown in Figure 14.2.

We rewrite the if_demo1 program by using the if-then-else-endif statement at the end. The resulting script is in the if_demo2 file, as shown in the following session. Notice that the program looks cleaner and more readable.

```
% cat if_demo2
#!/bin/csh
if ( ( $#argv == 0 ) || ( $#argv > 1 ) ) then
echo "Usage: $0 ordinary_file"
exit 1
endif
if ( ! -e $1 ) then
echo "$1 : non-existent file"
exit 1
```