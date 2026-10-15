
When the export_demo script is invoked, the name variable is set to John Doe and exported so that it becomes part of the environment of the commands that execute under export_demo as its children. The first echo command in the display_change_name script displays the value of the exported variable name. It then initializes a local variable called name to Plain Jane. The second echo command therefore echoes the current value of the local variable name and displays Plain Jane. When the display_change_name script finishes, the display_name script executes the echo command and displays the value of the exported name variable, thus displaying John Doe.

## 14.4.3 Resetting Variables

A variable retains its value for as long as the script in which it is initialized executes. You can remove a variable from the environment by using the unset and unsetenv commands. The following are brief descriptions of the commands.

### SYNTAX

```
unset variable-list
unsetenv variable
```

Purpose: Remove the specified variables from the environment. The variables in variable-list are separated by spaces. The unset command is used for the variables declared by the set or @ commands. The unsetenv command is used for variables declared by the setenv command.

Next we show a simple use of the unset command. The variables name and place are set to John and Corvallis, respectively, and the echo command displays the values of these variables. The unset command resets the name variable, defined with the set command, to null. Thus, the echo "$name" command should display a message saying that the name variable is undefined. However, the command shows John Doe as its output. If you go back and look at the shell session before the last one, you would see that name was initialized to John Doe using the setenv name "John Doe" command. The unset name command in the following session undefined the name variable defined by using this command, but the name variable defined using the setenv command remained defined with the value John Doe. When we run the unsetenv name command in the following session, the name variable defined with the setenv name "John Doe" command is undefined and the echo "$name" command shows the error message "name: Undefined variable.".

```
% set name=John place=Corvallis
% echo "$name $place"
John Corvallis
% unset name
% echo "$name"
John Doe
```

```
% echo "$place"
Corvallis
% unsetenv name
% echo "$name"
name: Undefined variable.
$
```

The following command removes the variables name and place, defined with the set command, from the environment:

```
% unset name place
%
```

To reset a variable, explicitly assign it a null value by using the set command with the variable name only. Or you can assign the variable no value and simply hit <Enter> after the = sign, as in.

```
% set country=
% echo "$country"

% set place
% echo $place
%
```

Here, the set command is used to reset the country and place variables to null.

## 14.4.4 Reading from Standard Input

So far, we have shown how you can assign values to shell variables statically at the command line or by using the assignment statement. If you want to write an interactive shell script that prompts the user for keyboard input, you need to use the set command in order to store the user input in a shell variable, according to the following syntax.

### SYNTAX
```
set variable = $<
set variable = `head -1`
```

Purpose: Read one line from stdin into variable; note the use of back quotes (grave accents) in 'head -1'

These commands allow you to read one line of keyboard input into variable. Some C shell implementations do not support the first set command, but the second set command works in all implementations. You can use the syntax for the second command to assign the first line of keyboard input to variable. Unlike that of the Bourne shell, the keyboard input feature of the C shell does not allow assignment of words in a line to multiple

variables. However, the words in a line are stored in the form of an array, and you can access them by using the name of the variable (we discuss arrays in Chapter 15).

We illustrate the semantics of the second set command with a script in the keyin_demo file, as follows:

```
% cat keyin_demo
#!/bin/csh
echo -n "Enter input: "
set line = `head -1`
echo "You entered: $line"
exit 0
%
```

In the following run, enter UNIX rules the network computing world!. The set command takes the whole input and puts it in the shell variable line without the newline character. The output of the echo command displays the contents of the shell variable line.

```
% ./keyin_demo
Enter input: UNIX rules the network computing world!
You entered: UNIX rules the network computing world!
%
```

The -n option is used with the echo command to keep the cursor on the same line. If you do not use this option, the cursor moves to the next line, which is what you want to see happen while displaying information and error messages. However, when you prompt the user for keyboard input, you should keep the cursor in front of the prompt for a more user-friendly interface. The C shell on most UNIX systems that are based on BSD UNIX, runs the BSD version of the echo command, which does not support the \c option and other options supported by the System V version of the echo command. The BSD version does support Standard ASCII control sequences that can be used to display other special characters, such as <Ctrl+H> for backspace and <Ctrl+G> for bell.

In the following in-chapter exercise, you will use the set command to practice reading from stdin in shell scripts.

## EXERCISE 14.5

Write commands for reading a value into the myname variable from the keyboard and exporting it so that the commands executed in any child shell have access to the variable.

## 14.5 PASSING ARGUMENTS TO SHELL SCRIPTS

In this section, we describe how command line arguments can be passed to shell scripts and manipulated by them. As we discussed in Section 14.3, you can pass command line arguments, also called positional parameters, to a shell script. The values of these
