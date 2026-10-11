
## The getopt Command

Although the `getopts` command makes programming scripts somewhat easier, it doesn't adhere to the Linux switch standards. In particular, `getopts` doesn't allow double minus long switches.

To get around this limitation, Linux includes its own `getopt` (singular, *not* `getopts`) command. Similar to `getopts`, `getopt` allows long switches and has other features that `getopts` does not, and it is used in scripts in an entirely different way.

Because `getopt` is an external command, it can't save switches into variables the way `getopts` does. It has no way to export environment variables back to the script. Likewise, `getopt` doesn't know what switches the shell has unless they are copied to the `getopt` command using `$@`. As a result, instead of being run in a loop, `getopt` runs once to process all the parameters as a single group.

Like `getopts`, `getopt` uses a `OPTARG` list of options. The list can be preceded by `--options` (or `-o`) to make it clear that these are the list of switches. The items can be listed as in `getopts` or as a comma-separated list.

The list of options given to the script must be appended to the `getopt` command using a double minus and `$@`. The double minus indicates where the `getopt` switches end and where the script switches begin.

Listing 9.5 contains a script that duplicates the `getopts.sh` using `getopt`. Notice that the `--name` (or `-n`) switch is used to give `getopt` the name of the script to be used in any error messages.

### Listing 9.5: getopt.sh

```bash
#!/bin/bash
#
#getopt.sh - a demonstration of getopt
declare -rx SCRIPT=${0##*/}
declare RESULT
RESULT=$(getopt --name "$SCRIPT" --options "-h,-c" -- "$@")
printf "status code=$? result=\"$RESULT\"\n"
```

Here are the results:

```
$ bash getopt.sh -h
 status code=0 result=" -h --"
$ bash getopt.sh -c
 getopt.sh: option requires an argument -- c
 status code=1 result=" --"
$ bash getopt.sh -x
 getopt.sh: invalid option -- x
 status code=1 result=" --"
```

The status code indicates whether `getopt` was successful. Status code 1 indicates `getopt` printed error messages. Status code 2 indicates a problem with options given to the `getopt` command itself.

Long switches are supported using the `--longoptions` (or `-l`) switch. Include a comma-separated list of expected long options. For example, to allow a `--help` switch, do this:

```bash
RESULT=$(getopt --name "$SCRIPT" --options "-h, -c:" \
   --longoptions "help" -- "$@")
```

`getopt` has other enhancements. To specify an optional argument for a long option, add an equals sign and the name of the argument.

If a double colon follows a switch name, it indicates an optional argument to the switch instead of a required one. If the `POSIXLY_CORRECT` variable exists and the option list begins with a +, arguments are not allowed for switches and the first argument is treated as the end of the switches.

If the `GETOPT_COMPATIBLE` shell variable exists, `getopt` behaves more like the C language `getopt` standard library function. Some older versions of `getopt` have this behavior by default. If you need to check for this behavior, use the `-T` (or `--test`) switch to test for C compatibility mode: If it is not running in compatibility mode, the status code is 4.

What do you do with the switches after `getopt` examines them? They can replace the original parameters using the `set` command:

```bash
eval set -- "$RESULT"
```

Now the parameters can be examined using positional parameters or using the built-in `getopts`, as shown in Listing 9.6.

### Listing 9.6: getopt_demo.sh

```bash
#!/bin/bash

# getopt_demo.sh
# This script expects the switch -c and a company name. --help (-h) is also allowed.

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r OPTSTRING="-h, -c:"
declare COMPANY
declare RESULT

# Check getopt mode

getopt -T
if [ $? -ne 4 ] ; then
    printf "%s: %s\n" "$SCRIPT" "getopt is in compatibility mode" >&2
    exit 1
fi

# Test parameters

RESULT=$(getopt --name "$SCRIPT" --options "$OPTSTRING" \
  --longoptions "help" -- "$@")
if [ $? -gt 0 ] ; then
    exit 1
fi

# Replace the parameters with the results of getopt

eval set -- "$RESULT"

# Process the parameters

while [ $# -gt 0 ] ; do
  case "$1" in
    -h | --help) # Show help
      printf "Usage: %s [-h][--help] -c companyid\n" "$SCRIPT"
      exit 0
      ;;
    -c )
      shift
      if [ $# -eq 0 ] ; then
        printf "%s:%s: %s\n" "$SCRIPT" "$LINENO" "company for -c is missing" >&2
        exit 1
      fi
      COMPANY="$1"
      ;;
  esac
  shift
done

if [ -z "$COMPANY" ] ; then
  printf "company name missing\n" >&2
  exit 1
fi

printf "%s: %s\n" "$SCRIPT" "Processing files for $COMPANY..."

# <-- begin work here

exit 0
```

This might seem like a lot of work, but for scripts with many complex switches, `getopt` makes the job of handling them much easier.

There are also a number of special switches. The `--alternative` (or `-a`) switch allows long options with only a single leading minus sign. Using this switch violates Linux convention. `--quiet-output` (or `-q`) can be used to check the switches without returning the processed list to standard output. `--quiet` (or `-q`) indicates any errors by the status code but hides the error messages so that you can create your own custom messages. The `--shell` (or `-u`) switch uses quotation marks to protect special characters like spaces that might be treated in a special way by a shell. (This is necessary only in C compatibility mode.)

## Subshells

Chapter 7, “Compound Commands,” mentioned that a set of commands can be grouped together using curly braces. These commands act as a group and return a single status code.

```
$ ( sleep 5 ; printf "%s\n" "Sleep for 5 seconds" ; )
Sleep for 5 seconds
```

A subshell is a set of commands grouped using round parentheses instead of curly braces. Unlike a command group, if a subshell appears on a single line, a semicolon is not required after the last command.

```
$ ( sleep 5 ; printf "%s\n" "Sleep for 5 seconds" )
Sleep for 5 seconds
```

Subshells act like a hybrid of a curly braces command set and a separate script. Like a statement group, a subshell is a set of statements that returns a single status code. Like a separate shell script, a subshell has its own environment variables.

```
$ declare -ix COUNT=15
$ ( COUNT=10 ; printf "%d\n" "$COUNT" ; )
10

$ printf "%d\n" "$COUNT"
15

$ ( COUNT=20 ; printf "%d\n" "$COUNT" )
20

$ printf "%d\n" "$COUNT"
15
```

In this example, a command group can change the value of the variable `COUNT` in the shell session because the group runs as part of the session. The subshell cannot change the value of `COUNT` in the main program because it runs as if it were a separate shell script. `COUNT` is a copy of the variable from the session and the subshell can only change its private copy of `COUNT`.

Subshells are often used in conjunction with pipes. Using a pipe (or file redirection), the results of a command can be redirected to the subshell for processing. The data appears on the standard input of the subshell, as shown in Listing 9.7.

### Listing 9.7: subshell.sh

```bash
#!/bin/bash
#
# subshell.sh
#
# Perform some operation to all the files in a directory

shopt -s -o nounset
declare -rx SCRIPT=${0##*/}
declare -rx INCOMING_DIRECTORY="incoming"

ls -1 "$INCOMING_DIRECTORY" |
(
    while read FILE ; do
        printf "%s: Processing %s...\n" "$SCRIPT" "$FILE"
        # <-- do something here
    done
)
printf "Done\n"
exit 0
```

The read command in the subshell reads one line at a time from standard input. In this case, it is reading the list of files created by the ls command.

```
$ bash subshell.sh
subshell.sh: Processing alabama_orders.txt...
subshell.sh: Processing new_york_orders.txt...
subshell.sh: Processing ohio_orders.txt...
Done
```

Subshells inherit more than just environment variables. This topic is discussed in detail in Chapter 14, “Functions and Script Execution.”

Argument handling greatly increases the flexibility of scripts, and subshells are an indispensable tool. But there is still more fundamental material to master before a script can be truly called professional. A script without job control and signal handling is still incomplete.
