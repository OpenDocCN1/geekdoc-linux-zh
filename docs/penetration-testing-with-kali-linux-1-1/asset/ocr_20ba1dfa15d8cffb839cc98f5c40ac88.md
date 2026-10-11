In Listing 143, we created a simple Bash script, set executable permissions on it, and then ran it with two arguments. The $1 and $2 variables represent the first and second arguments passed to the script. Let’s explore a few special Bash variables:

| Variable Name | Description |
|---|---|
| $0 | The name of the Bash script |
| $1 - $9 | The first 9 arguments to the Bash script |
| $# | Number of arguments passed to the Bash script |
| $@ | All arguments passed to the Bash script |
| $? | The exit status of the most recently run process |
| $$ | The process ID of the current script |
| $USER | The username of the user running the script |
| $HOSTNAME | The hostname of the machine |
| $RANDOM | A random number |
| $LINENO | The current line number in the script |

Some of these special variables can be very useful when debugging a script. For example, we might be able to obtain the exit status of a command to determine whether it was successfully executed or not.

# 5.2.2 Reading User Input

Command-line arguments are a form of user input, but we can also capture interactive user input while a script is running with the **read** command. In this example, we will use **read** to capture user input and assign it to a variable:

```
```bash
kali@kali:~$ cat ./input.sh
#!/bin/bash

echo "Hello there, would you like to learn how to hack: Y/N?"

read answer

echo "Your answer was $answer"

kali@kali:~$ chmod +x ./input.sh

kali@kali:~$ ./input.sh
Hello there, would you like to learn how to hack: Y/N?
Y
Your answer was Y
```
```

We can alter the behavior of the **read** command with various command line options. Two of the most commonly used options include **-p**, which allows us to specify a prompt, and **-s**, which makes the user input silent. The latter is ideal for capturing user credentials:

```
```bash
kali@kali:~$ cat ./input2.sh
#!/bin/bash
# Prompt the user for credentials
```
```