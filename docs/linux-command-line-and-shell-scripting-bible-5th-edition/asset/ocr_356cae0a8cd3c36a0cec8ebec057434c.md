Be careful with the backtick character—it is not the normal single quotation mark character you are used to using for strings. Because it is not used very often outside of shell scripts, you may not even know where to find it on your keyboard. You should become familiar with it, because it's a crucial component of many shell scripts. Hint: On a U.S. keyboard, it is usually on the same key as the tilde symbol (~).

Command substitution allows you to assign the output of a shell command to a variable. Though this doesn't seem like much, it is a major building block in script programming.

You must surround the entire command-line command with either the backtick characters:

```
`testing=`date``
```

or use the $( ) format:

```
`testing=$(date)`
```

The shell runs the command within the command substitution characters and assigns the output to the testing variable. Notice that there aren't any spaces between the assignment equals sign and the command substitution character. Here's an example of creating a variable using the output from a normal shell command:

```
$ cat test5
#!/bin/bash
testing=$(date)
echo "The date and time are: " $testing
$
```

The testing variable receives the output from the date command, and it is used in the echo statement to display it. Running the shell script produces the following output:

```
$ chmod u+x test5
$ ./test5
The date and time are: Sun Jun 01 15:45:25 EDT 2025
$
```

That's not all that exciting in this example (you could just as easily put the command in the echo statement), but once you capture the command output in a variable, you can do anything with it.

Here's a popular example of how command substitution is employed to capture the current date and use it to create a unique filename in a script:

```
#!/bin/bash
# copy the /usr/bin directory listing to a log file
today=$ (date +%Y%m%d)
ls /usr/bin -al > log.$today
```

The today variable is assigned the output of a formatted date command. This is a common technique used to extract date information for log filenames. The +%Y%m%d format instructs the date command to display the date as a two-digit year, month, and day:

```
$ date +%Y%m%d
250601
$
```