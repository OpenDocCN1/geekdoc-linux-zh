Dhcpd User's userid is dhcpd
Bind User's userid is named
NSCD Daemon's userid is nscd
X Font Server's userid is xfs
MySQL server's userid is mysql
Rich's userid is rich
test account's userid is testing
postfix's userid is postfix
$ 

The script2 program script uses the print command to print the comment data
field (field variable $5) of the /etc/passwd file, a short text message, then the userid
data field (field variable $1).

You can specify multiple commands in the program file. To do so, just place each command on
a separate line. There's no need to use semicolons:

```
$ cat script3
{
text="s userid is "
print $5 text $1
$ awk -F: - script3 /etc/passwd | more
root's userid is root
bin's userid is bin
PostgreSQL Server's userid is postgres
FTP User's userid is ftp
GDM User's userid is gdm
HTDIG User's userid is htdig
Dhcpd User's userid is dhcpd
Bind User's userid is named
NSCD Daemon's userid is nscd
X Font Server's userid is xfs
MySQL server's userid is mysql
Rich's userid is rich
test account's userid is testing
postfix's userid is postfix
$ 
```

The script3 program script defines a variable to hold a text string used in the print command.
You'll notice that gawk programs don't use a dollar sign when referencing a variable's value, as
thell script does.

# Running scripts before processing data

The gawk program also allows you to specify when the program is run. By default, gawk
reads a line of text from the input, then executes the program on the line of
text. Sometimes you may need to run a script before processing data, such as to create header