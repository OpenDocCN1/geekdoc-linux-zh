```
$ ./askname.sh
Enter your name: Richard Blum
Hello Richard Blum, welcome to my script.
$
```

That's pretty simple. Notice that the echo command that produced the prompt uses the -n option. This suppresses the newline character at the end of the string, allowing the script user to enter data immediately after the string, instead of on the next line. This gives your scripts a more form-like appearance.

In fact, the read command includes the -p option, which allows you to specify a prompt directly in the read command line:

```
$ cat askage.sh
#!/bin/bash
# Using the read command with the -p option
#
read -p "Please enter your age: " age
days=$( $age \* 365 )
echo "That means you are over $days days old!"
exit
$
```

```
$ ./askage.sh
Please enter your age: 30
That means you are over 10950 days old!
$
```

You'll notice in the first example that when a name was entered, the read command assigned both the first name and last name to the same variable. The read command assigns all data entered at the prompt to a single variable, or you can specify multiple variables. Each data value entered is assigned to the next variable in the list. If the list of variables runs out before the data does, the remaining data is assigned to the last variable:

```
$ cat askfirstlastname.sh
#!/bin/bash
# Using the read command for multiple variables
#
read -p "Enter your first and last name: " first last
echo "Checking data for $last, $first..."
exit
$
```

```
$ ./askfirstlastname.sh
Enter your first and last name: Richard Blum
Checking data for Blum, Richard...
$
```

You can also specify no variables on the read command line. If you do that, the read command places any data it receives in the special environment variable called REPLY:

```
$ cat asknamereply.sh
#!/bin/bash
# Using the read command with REPLY variable
```