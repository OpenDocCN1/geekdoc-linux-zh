| --e file | True if file exists. |
|---|---|
| -f file | True if file exists and is a regular file. |
| -g file | True if file exists and is set-group-id. |
| -h file | True if file exists and is a symbolic link. |
| -k file | True if file exists and its "sticky" bit is set. |
| -p file | True if file exists and is a named pipe (FIFO). |
| -r file | True if file exists and is readable. |
| -s file | True if file exists and has a size greater than zero. |
| -t fd | True if file descriptor fd is open and refers to a terminal. |
| -u file | True if file exists and its set-user-id bit is set. |
| -w file | True if file exists and is writable. |
| -x file | True if file exists and is executable. |
| -O file | True if file exists and is owned by the effective user ID. |
| -G file | True if file exists and is owned by the effective group ID. |
| -L file | True if file exists and is a symbolic link. |
| -S file | True if file exists and is a socket. |
| -N file | True if file exists and has been modified since it was last read. |
| file1 -nt file2 | True if file1 is newer by modification date than file2. |
| file1 -ot file2 | True if file1 is older by modification date than file2. |
| file1 -et file2 | True if file1 and file2 have the same device and inode numbers. |
| -o optname | True if shell option optname is enabled. |
| -z string | True if the length of string is zero. |
| -n string | True if the length of string is not zero. |
| string1 = string2 | True if the strings are equal. |
| string1 != string2 | True if the strings are not equal. |
| string1 < string2 | True if string1 sorts before string2 lexicographically. |
| string1 > string2 | True if string1 sorts after string2 lexicographically. |
| arg1 -eq arg2 | True if arg1 is equal to arg2. Both must be integers. |
| arg1 -ne arg2 | True if arg1 is not equal to arg2. |
| arg1 -lt arg2 | True if arg1 is less than arg2. |
| arg1 -le arg2 | True if arg1 is less than or equal to arg2. |
| arg1 -gt arg2 | True if arg1 is greater than arg2. |
| arg1 -ge arg2 | True if arg1 is greater than or equal to arg2. |

Conditional expressions are typically used in the formation of an *if*, *for*, or *while* loop. For example, consider the *-a* option, which simply tests whether a file exists. If you want to determine whether the user who is logged in has a *.bash_profile* and execute that profile if it exists, you can use the following *if* statement:

```
```
if [ -a /home/$USER/.bash_profile ]
then
    . /home/$USER/.bash_profile
fi
```
```