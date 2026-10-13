As you can see, indentation goes a long way toward making the program easy to read and understand. Get into the habit of setting and following indentation rules in your own programs and you’ll definitely thank us later on as your programs become increasingly complicated.

The sophistication of the user experience is clearly improved over previous versions of the program:

```
```text
$ on                         No arguments
Incorrect number of arguments
Usage:  on user
$ on priscilla               One argument
priscilla is not logged on
$ on jo anne                 Two arguments
Incorrect number of arguments
Usage:  on user
$
```
```

# The exit Command

A built-in shell command called `exit` enables you’ to immediately terminate execution of your shell program. The general format of this command is

`exit n`

where *n* is the exit status that you want returned. If none is specified, the exit status used is that of the last command executed prior to the exit (that is, it’s effectively `exit $?`).

Be advised that executing the exit command directly from your terminal will log you off the system because it will have the effect of terminating execution of your login shell.

# A Second Look at the `rem` Program

`exit` is frequently used as a convenient way to terminate execution of a shell program. For example; let’s take another look at the `rem` program, which removes an entry from the phonebook file:

```
```sh
$ cat rem
#
# Remove someone from the phone book
#

grep -v "$1" phonebook > /tmp/phonebook
mv /tmp/phonebook phonebook
$
```
```

As written, this program has the potential to create problems if unexpected situations arise, potentially even corrupting or wiping out the entire phonebook file.