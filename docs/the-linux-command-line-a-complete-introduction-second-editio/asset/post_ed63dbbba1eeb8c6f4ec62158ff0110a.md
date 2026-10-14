
| Option | Description |
|---|---|
| -a array | Assign the input to array, starting with index zero. We will cover arrays in Chapter 35. |
| -d | The first character in the string delimiter is used to indicate delimiter the end of input, rather than a newline character. |
| -e | Use Readline to handle input. This permits input editing in the same manner as the command line. |
| -i string | Use string as a default reply if the user simply presses ENTER. Requires the -e option. |
| -n num | Read num characters of input, rather than an entire line. |
| -p prompt | Display a prompt for input using the string prompt. |
| -r | Raw mode. Do not interpret backslash characters as escapes. |
| -s | Silent mode. Do not echo characters to the display as they are typed. This is useful when inputting passwords and other confidential information. |
| -t seconds | Timeout. Terminate input after seconds. read returns a non-zero exit status if an input times out. |
| -u fd | Use input from file descriptor fd, rather than standard input. |

Using the various options, we can do interesting things with read. For example, with the -p option, we can provide a prompt string.

```
#!/bin/bash

# read-single: read multiple values into default variable

read -p "Enter one or more values > "

echo "REPLY = '$REPLY'"
```

With the -t and -s options, we can write a script that reads “secret” input and times out if the input is not completed in a specified time.

```
#!/bin/bash

# read-secret: input a secret passphrase

if read -t 10 -sp "Enter secret passphrase > " secret_pass; then
    echo -e "\nSecret passphrase = '$secret_pass'"
else
    echo -e "\nInput timed out" >&2
    exit 1
fi
```

The script prompts the user for a secret passphrase and waits ten seconds for input. If the entry is not completed within the specified time, the script exits with an error. Because the -s option is included, the characters of the passphrase are not echoed to the display as they are typed.

It's possible to supply the user with a default response using the -e and -i options together.

```
#!/bin/bash

# read-default: supply a default value if user presses Enter key.

read -e -p "What is your user name? " -i $USER
echo "You answered: '$REPLY'"
```

In this script, we prompt the user to enter a username and use the environment variable USER to provide a default value. When the script is run, it displays the default string, and if the user simply presses ENTER, read will assign the default string to the REPLY variable.

```
[me@linuxbox ~]$ read-default
What is your user name? me
You answered: 'me'
```

## IFS

Normally, the shell performs word-splitting on the input provided to read. As we have seen, this means that multiple words separated by one or more spaces become separate items on the input line and are assigned to separate variables by read. This behavior is configured by a shell

variable named IFS (for Internal Field Separator). The default value of IFS contains a space, a tab, and a newline character, each of which will separate items from one another.

We can adjust the value of IFS to control the separation of fields input to read. For example, the /etc/passwd file contains lines of data that use the colon character as a field separator. By changing the value of IFS to a single colon, we can use read to input the contents of /etc/passwd and successfully separate fields into different variables. Here we have a script that does just that:

```
#!/bin/bash

# read-ifs: read fields from a file

FILE=/etc/passwd

read -p "Enter a username > " user_name

file_info=$(grep "^$user_name:" $FILE)

if [ -n "$file_info" ]; then
IFS=":" read user pw uid gid name home shell <<< "$file_info"
echo "User =      '$user'"
echo "UID =       '$uid'"
echo "GID =       '$gid'"
echo "Full Name = '$name'"
echo "Home Dir. = '$home'"
echo "Shell =     '$shell'"
else
echo "No such user '$user_name'" >&2
exit 1
fi
```

This script prompts the user to enter the username of an account on the system and then displays the different fields found in the user's record in the /etc/passwd file. The script contains two interesting lines. The first is as follows:

```
file_info=$(grep "^$user_name:" $FILE)
```

This line assigns the results of a grep command to the variable file_info. The regular expression used by grep assures that the username
