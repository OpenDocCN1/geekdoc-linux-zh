
# Command Summary

do

```
nroff -Tlp $file | lp
done
```

## The getopts Command

General Format: getopts options var

This command processes command-line arguments. options is a list of valid single letter options. If any letter in options is followed by a :, that option requires an additional argument on the command line which must be separated from the option by at least one space.

Each time getopts is called, it processes the next command-line argument. If a valid option is found, getopts stores the matching option inside the specified variable var and returns a zero exit status.

If an invalid option is (not listed in options), getopts stores a ? inside var and returns with a zero exit status. It writes an error message to standard error.

If an option takes an argument, getopts stores the matching option inside var and stores the command-line argument inside the specified variable OPTARG. If no arguments are left on the command line, getopts sets var to ? and writes an error message to standard error.

If no more arguments remain on the command line (if the next command-line argument does not begin with a -), getopts returns a nonzero exit status.

The special variable OPTIND is also used by getopts. It is initially set to 1 and is adjusted each time getopts returns to indicate the number of the next command-line argument to be processed.

The argument -- can be placed on the command line to specify the end of the command-line arguments.

getopts supports stacked arguments, as in

```
repx - iau
```

which is equivalent to

```
repx -i -a -u
```

Options that have required arguments may not be stacked.

If the format

```
getopts options args var
```

is used, getopts parses the arguments specified by args rather than the command-line arguments.

Example

```
usage="Usage: foo [-r] [-0 outfile] infile"
```

```
while getopts ro: opt
```

## Appendix A Shell Summary

```
do
  case "$opt"
    in
      r) rflag=1;
      O) oflag=1
        file=$OPTARG;
      \?) echo "$usage"
    esac
    exit 1;
```

```
if [ $OPTIND -gt $# ]
then
  echo "Needs input file!"
  echo "$usage"
  exit 2
fi
```

```
shift $((OPTIND - 1))
if=$1
```

## The hash Command

**General Format:** hash `commands`

This command tells the shell to look for the specified commands and to remember what directories they are located in. If `commands` is not specified, a list of the hashed commands is displayed.

If the format

```
hash -r
```

used, the shell removes all commands from its hash list. Next time any command is executed, the shell uses its normal search methods to find the command.

*Examples*

```
hash rolo whoq
hash
hash -r
```

- Add rolo and whoq to hash list
- Print hash list
- Remove hash list

## The if if Command

**General Format:**

```
if command;
then
```

## Command Summary 345

```
command
command
...
fi
```

command, is executed and its exit status tested. If it is zero, the commands that follow up to the fi are executed. Otherwise, the commands that follow up to the fi are skipped.

## Example

```
if grep $sys sysnames > /dev/null
then
  echo "$sys is a valid system name"
fi
```

If the grep returns an exit status of zero (which it will if it finds $sys in the file sysnames), the echo command is executed; otherwise it is skipped.

The built-in command test is often used as the command following the if, either by explicitly calling test or using its mnemonic shortcut, [ the latter of which requires a matching ].

## Example

```
if [ $ -eq 0 ]; then
  echo "Usage: $0 [-1] file ..."
  exit 1
```

An else clause can be added to the if to be executed if the command returns a nonzero exit status. In this case, the general format of the if becomes

```
if command;
then
  command
  command
...
else
  command
  command
...
fi
```

If command, returns an exit status of zero, the commands that follow up to the else are executed, and the commands between the else and the fi are skipped. Otherwise, command, returns a nonzero exit status and the commands between the then and the else are skipped, and the commands between the else and the fi are executed.

```
if [ -z "$line" ]
then
  echo "I couldn't find $name"
```

else

```
echo "$line"
```

```
fi
```

In the preceding example, if line has zero length, the echo command that displays the message I couldn't find $name is executed; otherwise, the echo command that displays the value of line is executed.

A final format of the if command is useful when more than a two-way decision has to be made. Its general format is

```
if command,
```

```
then
```

```
command
  command
  ...
```

```
elif command_j
```

```
then
```

```
command
  command
  ...
```

```
elif command_n
```

```
then
```

```
command
  command
  ...
```

```
else
```

```
command
  command
  ...
```

```
fi
```

If command, returns an exit status of zero, the commands that follow up to the else are executed, and the commands between the else and the fi are skipped. Otherwise, command, returns a nonzero exit status and the commands between the then and the else are skipped, and the commands between the else and the fi are executed.

## Command Summary 346

## jobs Command

General Format: jobs

The list of active jobs is printed. If the -l option is specified, detailed information about each job is listed as well. If the -p option is specified, only process IDs are listed.

If an optional job_id is supplied to the jobs command, just information about job is listed.

Example

```
$ sleep 100 &
[1] Running      sleep 100 &
```

## The kill Command

General Format: kill -signal job

The kill command sends the signal to the specified process, where job is a process ID or job_id, and signal is a number or one of the signal names. The -l option lists the corresponding signal name.

The -s option can also be used when a signal name is supplied, in which case the dash before the name is not used (see the following example).

If signal isn't specified, SIGTERM (TERM) is used.

Examples

```
$ kill -9 1234
$ kill -HUP $2
kill -s TERM $2
kill $1
```

## The newgrp Command

General Format: newgrp group

This command changes your real group id (GID) to group. If no argument is specified, it changes you back to your default group.

## Shell Summary

Examples

```
newgrp shbook    Change to group shbook
newgrp             Change back to default
```

If a password is associated with the new group, and you are not listed as a member of the group, you will be prompted to enter it.

```
newgrp -l changes you back to your login group.
```

## The pwd Command

General Format: pwd

This command tells the shell to print your working directory, which is written to standard output.

Examples

```
$ pwd
/users/steve/documents/memos
$ cd
$ pwd
/users/steve
$
```

## The read Command

General Format: read vars

This command causes the shell to read a line from standard input and assign successive whitespace-delimited words to the variables vars. If fewer variables are listed than there are words on the line, the additional words are stored in the last variable.

Specifying just one variable has the effect of reading and assigning an entire line to the variable.

The exit status of read is zero unless an end-of-file condition is encountered.

Examples

```
$ read hours mins
10 19
$ echo "$hours:$mins"
10:19
$ read num rest
39 East 12th Street, New York City 10003
$ echo "$num\n$rest"
39
East 12th Street, New York City 10003
```
