# Part III Advanced Shell Scripting

This short program displays the first data field in the password file on the system. Because the /etc/passwd file uses a colon to separate the data fields, if you want to separate out each data element you must specify it as the field separation character in the awk options.

# Using multiple commands in the program script

A programming language would not be very useful if you could only execute one command. The awk programming language allows you to combine commands into a normal program. To use multiple commands in the program script specified on the command line, just place a semicolon between each command:

```
$ echo "My name is Rich" | awk '{$4="Dave"; print $0}'
My name is Dave
$
```

The first command assigns a value to the $4 variable. The second command then prints the entire field. Notice from the output that the awk program replaced the fourth data field in the original text with the new value.

You can also use the secondary prompt to enter your script commands one line at a time:

```
$ awk '$(
> $4="testing"
> print $0'
This is not a good test.
This is not testing good test.
$
```

After you open the single quotation mark, the bash shell provides the secondary prompt for more data. You can add commands one at a time on each line until you are entering the single quotation mark. To exit the program, just press the Ctrl-D key combination to signal the end of the data.

# Reading the program from a file

Just as the sed editor, the awk editor allows you to store your programs in a file and refer to them in the command line:

```
$ cat script2
( print $5 "userid is $1"
$ awk -f script2 /etc/passwd
root's userid is root
bin's userid is bin
PostgreSQL Server's userid is postgres
FTP User's userid is ftp
GDM User's userid is gdm
HTDIG User's userid is htdig
```

426