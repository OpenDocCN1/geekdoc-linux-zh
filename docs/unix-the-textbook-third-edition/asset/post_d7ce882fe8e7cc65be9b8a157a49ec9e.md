
## 12.3.6 Reading from Standard Input

So far, we have shown how you can assign values to shell variables statically at the command line level or by using the assignment statement in your programs. If you want to write an interactive shell script that prompts the user for keyboard input, you need to use the read command to store the user input in a shell variable. This command allows you to read one line of standard input. The following is a brief description of the command.

```
SYNTAX
read variable-list

Purpose: Read one line from standard input and assign words in the line to variables in variable-list
```

A line is read in the form of words separated by white spaces (<Space> or <Tab> characters, depending on the value of the shell environment variable IFS). The words are assigned to the variables in the order of their occurrence, from left to right. If the number of words in the line is greater than the number of variables in variable-list, the last variable is assigned the extra words. If the number of words in a line is less than the number of variables, the remaining variables are reset to null.

We illustrate the semantics of the read command by way of the following script in the read_demo file.

```
$ cat read_demo
#!/bin/sh
echo -n "Enter input: "
read line
echo "You entered: $line"
echo -n "Enter another line: "
read word1 word2 word3
echo "The first word is: $word1"
echo "The second word is: $word2"
echo "The rest of the line is: $word3"
exit 0
$
```

We now show how the input that you enter from the keyboard is read by the read command in that script. In the following run, you enter the same input: UNIX rules the network computing world!. The first read command takes the whole input and puts it in the shell variable line without the newline character. In the second read command, the first word of your input is assigned to the variable word1, the second word is assigned to the variable word2, and the rest of the line (without the newline character) is assigned to the variable word3. The outputs of the echo commands for displaying the values of these variables confirm this point.

```
$ ./read_demo
Enter input: UNIX rules the network computing world!
You entered: UNIX rules the network computing world!
Enter another line: UNIX rules the network computing world!
The first word is: UNIX The second word is: rules
The rest of the line is: the network computing world!
$
```

The -n option used in the two echo commands is used to force the cursor to stay at the same line after the echo command has displayed the quoted text. If you do not use this character, the cursor moves to the next line, which is what you like to see happen while displaying information and error messages. However, when you prompt the user for keyboard input, you should keep the cursor in front of the prompt for a user-friendlier interface.

On BSD and System V compatible UNIX systems, including PC-PSD, several special characters can be used in the Bourne shell echo -e command as control characters. These characters start with a backslash (\). Thus, for example, the echo -n "Enter input: " command in the read_demo script may be replaced with echo -e "Enter input: \c". Some of the control characters, along with their meanings, are listed in Table 12.3. Note that on some UNIX systems, you may have to use double backslash (\\ ) instead of single backslash for the special characters to work. For example, use \\c instead of \c to keep the cursor on the same line.

In the following in-chapter exercises, you will use the read and export commands to practice reading from stdin in shell scripts and exporting variables to child processes.

## EXERCISE 12.5

Give commands for reading a value into the myname variable from the keyboard and exporting it so that commands executed in any child shell have access to the variable.

### TABLE 12.3 Special Characters for the echo -e Command

| Character | Meaning |
|---|---|
| \b | Backspace |
| \c | Prints line without moving cursor to next line |
| \f | Form feed |
| \n | Newline (move cursor to next line) |
| \r | Carriage return |
| \t | Horizontal tab |
| \v | Vertical tab |
| \\ | Backslash (escape special meaning of backslash) |
| \0N | Character whose ASCII number is octal N (it is 0 and not o) |

Note: You might have to use \\ instead of \ on some UNIX systems.
