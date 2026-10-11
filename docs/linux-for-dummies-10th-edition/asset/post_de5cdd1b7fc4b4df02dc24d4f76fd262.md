
3. Save the file, and then use the `chmod` command to change the execute permissions:

```
chmod u+x test2.sh
```

4. Run the file:

```
$ ./test2.sh
User info for userid: rich
UID: 1000
HOME: /home/rich
$
```

The `$USER`, `$UID`, and `$HOME` environment variables are commonly used to display information about the logged-in user. The values you see are related to your user account. This allows you to dynamically retrieve information about the user account running your shell script to customize the output.

# User variables

User variables allow you to store your own data within your shell scripts. You assign values to user variables using the equal sign. Spaces must not appear between the variable name, the equal sign, and the value. Here are a few examples:

```
var1=10
var2=23,45
var3=testing
var4="Still more testing"
```

The shell script stores all values as text, but the individual commands interpret the text as numbers or string data. Variables that you define within the shell script are called *local variables*, and are only accessible from within the shell script. Global variables are defined outside of the shell script at the main shell level, and are inherited by the script shell environment.

![](img/577d3bff979ee86b07f9836e0df274ce_383_0.png)

The `set` command displays all the global variables set. If you need to see the local variables set for your session, use the `printenv` command.

Just like with environment variables, you can reference user variables using the dollar sign. Here's an example of writing a shell script that uses user variables:

```
$ cat test3.sh
#!/bin/bash
# testing variables
days=10
guest=Katie
echo $guest checked in $days days ago
$
```

Running the test3.sh script produces the following output:

```
$ chmod u+x test3.sh
$ ./test3.sh
Katie checked in 10 days ago
$
```

Once you store the data in a user variable you can reference it anywhere in your shell script!

![](img/577d3bff979ee86b07f9836e0df274ce_384_0.png)

Be careful when using variables within the echo statement. Because variable names are just text values, if you try to append text to a variable name the shell considers the text as part of the variable name and you won't get the results you thought. If you need to do that, you can enclose the variable name in braces, such as ${guest}. This ensures any text appended to the end of the variable is separate from the variable name.

# Command line arguments

One of the most versatile features of shell scripts is the ability to pass data into the script when you run it. This allows you to customize the script with new data each time you run it.

One method of passing data into a shell script is to use command line arguments. Command line arguments are data you include on the command line when you run the command. Just start listing them after the command, separating each data value with a space, in this format:

```
command argument1 argument2 ...
```

You retrieve the values in your shell script code using special numeric positional variables. Use the variable $1 to retrieve the first command line argument, $2 the second argument, and so on. Here’s an example that shows how to use positional variables in your shell script:

```
$ cat test4.sh
#!/bin/bash
# Testing command line arguments
echo $1 checked in $2 days ago
$ chmod u+x test4.sh
$ ./test4.sh Barbara 4
Barbara checked in 4 days ago
$ ./test4.sh Jessica 5
Jessica checked in 5 days ago
$
```

The test4.sh shell script uses two command line arguments. The $1 variable holds the name of the person, and the $2 variable holds the number of days ago they checked in. When you run the test4.sh shell script be sure to include both data values in the command line. The shell won’t produce an error message if a positional variable doesn’t exist; you just won’t get the results you expected:

```
$ ./test4.sh rich
rich checked in days ago
$
```

It’s up to you to check whether the positional variable exists within your program code. I explore how to do that later in the “Logic statements” section.

# The exit status

When a shell script ends it returns an *exit status* back to the parent shell that launched it. The exit status tells you whether the shell script completed successfully.

Linux provides you with the special `$?` variable, which holds the exit status value from the last command that executed. To check the exit status of a command, you must view the `$?` variable immediately after the command ends. It changes values according to the exit status of the last command executed by the shell:

```
$ who
rich     :0      2020-06-16 23:16 (:0)
$ echo $?
0
$
```

By convention, the exit status of a command that successfully completes is 0. If a command completes with an error, then a positive integer value appears as the exit status.

You can change the exit status of your shell scripts by using the `exit` command. Just specify the `exit` status value you want in the `exit` command:

```
$ /bin/bash
$ exit 120
exit
$ echo $?
120
$
```

This example starts a new child shell with the `/bin/bash` command, and then uses the `exit` command to exit the child shell with an exit status code of 120. The parent shell then displays the `$?` variable value to see whether it matched the value set in the `exit` command.

![](img/577d3bff979ee86b07f9836e0df274ce_386_0.png)

As you write more complicated scripts you can indicate errors by changing the exit status value. That way, by checking the exit status, you can easily debug your shell scripts.

# Writing Script Programs

So far you’ve explored how to combine regular command line commands within a shell script to automate common tasks that you may perform as the system administrator. But shell scripts allow you to do much more than just that. The `bash` shell provides more programming-like commands that allow you to write full-fledged programs within your shell scripts, such as capturing command output, performing mathematical operations, checking variable and file conditions, and looping through commands. This section walks through some of the advanced programming features available from the `bash` shell.

## Command substitution

Quite possibly one of the most useful features of shell scripts is the ability to store and process data. So far I’ve discussed how to use output redirection to store output from a command to a file, and piping to redirect the output of a command to another command. Another technique, however, can give you more flexibility in storing and using data in your scripts.

*Command substitution* allows you to assign the output of a command to a user variable in the shell script. After the output is stored in a variable, you can use standard Linux string manipulation commands (such as `sort`) to manipulate the data before displaying it.

To redirect the output of a command to a variable, you need to use one of two command substitution formats:

- Placing backticks (`` ` ``) around the command
- Using the command within the `$( )` function

Both methods produce the same result — redirecting the output from the command into a user variable. Here’s an example that demonstrates using both methods:

```
$ var1=`date`
$ echo $var1
Tue Jun 16 18:05:38 EST 2020
$ var2=$(who)
$ echo $var2
rich :0 2020-06-16 17:56 (:0)
$ 
```

The output from the command substitutions is stored in the appropriate variables. You can then use those variables anywhere in your script program as a standard string value.

> **WARNING**: The backtick character is not the same as a single quote. It’s the character usually found on the same key as the tilde character (~) on U.S. keyboards. Because of the confusion between backticks and single quotes, it’s become more popular in the Linux world to use the `$( )` function format.

## Performing math

Eventually you’ll want to do more than just manipulate text strings in your shell scripts. The world revolves around numbers, and at some point you’ll probably need to do some mathematical operations with your data. Unfortunately, this is one place where the bash shell shows its age. The mathematical features in the bash shell aren’t quite as fancy as the features found in newer shells, such as the Z shell. However, you can use simple mathematical functions in bash shell scripts in a couple ways.

To include mathematical expressions in your shell scripts you use a special format. This format places the equation within the `$[ ]` characters:

```
result=$(( 25 * 5 ))
```
