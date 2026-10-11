
By finding the name of the script from $0, there is no danger that the wrong name will be printed after the script has been copied or renamed. SCRIPT is always the correct name of the script.

The variable $# contains the number of parameters to a script or a shell session. If there are no parameters, $# is zero. The number doesn't include the script name in $0.

```bash
$ printf "%d\n" $#
0
```

The first nine parameters are placed in the variables $1 through $9. (Parameters beyond nine can be accessed if curly braces surround the number.) When the nounset shell option is used, accessing an undefined parameter results in an error, just as if it were an undeclared variable name.

```bash
$ printf "%s\n" $9
bash: $9: unbound variable
```

The variable $* (or $@) returns a complete list of all the parameters as a single string.

When using positional parameters, Bash doesn't differentiate between switches and arguments. Each item on the command line is a separate parameter to the script. Consider the following script, shown in Listing 9.1.

### Listing 9.1 params.sh

```bash
#!/bin/bash
#
# params.sh: a positional parameter demonstration

printf "There are %d parameter(s)\n" "$#"
printf "The complete list is %s\n" "$@"
printf "The first parameter is %s\n" "$1"
printf "The second parameter is %s\n" "$2"
```

When the script runs using the parameters -c and t2341, $1 refers to -c and $2 refers to t2341.

```bash
$ bash params.sh -c t2341
There are 2 parameter(s)
The complete list is -c t2341
The first parameter is -c
The second parameter is t2341
```

Although both $@ and $* refer to all the parameters, they differ when they are enclosed in double quotes. $* parameters are separated by the first character of the IFS variable, or by spaces if IFS is empty, or without anything when IFS is unset. $* treats the set of parameters as a single group.

$@, on the other hand, always separates the parameters by spaces and treats the parameters as individual items, even when they are enclosed in double quotes. $@ is often used to transfer the entire set of switches to another command (for example, ls $@).

Although positional parameters are a straightforward way to view switches and arguments, they do not “walk through” the list. There is a built-in `shift` command that discards the parameter in $1 and moves the remaining parameters down one number to take its place. Using `shift`, you can check each parameter in turn as if it were the first parameter.

Listing 9.2 shows a complete example, using `shift`.

### Listing 9.2 param2.sh

```bash
#!/bin/bash
#
# param2.sh
#
# This script expects the switch -c and a company name. --help (-h)
# is also allowed.

shopt -s -o nounset
declare -rx SCRIPT=${0##*/}

# Make sure there is at least one parameter or accessing $1
# later will be an error.

if [ $# -eq 0 ]; then
    printf "%s\n" "Type --help for help."
    exit 192
fi

# Process the parameters

while [ $# -gt 0 ]; do
    case "$1" in
        -h | --help) # Show help
            printf "%s\n" "Usage: $SCRIPT [-h] [--help] -c company"
            exit 0
            ;;
        -c) shift
            if [ $# -eq 0 ]; then
                printf "${SCRIPT}:${LINENO}: %s\n" "company for -c is missing" >&2
                exit 192
            fi
            COMPANY="$1"
            ;;
        *) printf "${SCRIPT}:${LINENO}: %s\n" "switch $1 not supported" >&2
            exit 192
            ;;
    esac
    shift
done

if [ -z "$COMPANY" ]; then
    printf "$@\n" "company name missing" >&2
    exit 192
fi

# <-- begin work here
exit 0
```

A final parameter-related switch is $\_ (dollar underscore). This switch has two purposes. First, it represents the pathname to the shell or shell script when the shell (or shell script) is first started. Second, after each command is executed, the command is placed in the environment as a variable containing the pathname of the command.

```bash
$ /bin/date
Fri Jun 29 14:39:58 EDT 2001
$ printf "$_\n" "$_"
/bin/date
$ date
Fri Jun 29 14:40:04 EDT 2001
$ printf "$_\n" "$_"
date
```

You can use $\_ to repeat the last argument.

### The **getopts** Command

There are two limitations to the positional parameter approach. First, it requires the script writer to test for errors and create the corresponding messages. Second, the **shift** command destroys all the parameters. If you want to access them later, you can't.

To deal with these issues, Bash includes a built-in **getopts** (*get options*) command that extracts and checks switches without disturbing the positional parameter variables. Unexpected switches, or switches that are missing arguments, are recognized and reported as errors.

Using **getopts** requires some preparation by the script writer. First, you must define a string containing a list of expected switch letters. By convention, this variable is called **OPTSTRING**. If any switch requires an argument, add a colon after the switch character.

For example, if the param2.sh script expects -h (help) and -c (company ID) with a company ID argument, the OPTSTRING would be hc::.

There is a second required parameter after the list of options: The name of a shell variable into which to record each option encountered.

Each time the getopts command runs, the next switch on the command line is examined and the name of the switch is saved in the variable SWITCH. The position of the next parameter to be examined is in a variable called OPTIND. If it doesn't exist, OPTIND is automatically set to 1 before the first script parameter is checked. If there is any argument to the script, it is saved in a variable called OPTARG. Listing 9.3 shows a short script that tests the first parameter of the script.

### Listing 9.3 getopt.sh

```bash
#!/bin/bash
#
# getopt.sh

declare SWITCH
getopts "hc:" SWITCH
printf "The first switch is SWITCH=%s OPTARG=%s OPTIND=%s\n" \
    "$SWITCH" "$OPTARG" "$OPTIND"
```

In this short script, unknown switches assign a question mark (?) to the SWITCH variable; an error message is displayed.

```bash
$ bash getopt.sh -h
The first switch is SWITCH=h OPTARG= OPTIND=2
$ bash getopt.sh -c a4327
The first switch is SWITCH=c OPTARG=a4327 OPTIND=3
$ bash getopt.sh -a
t.sh: illegal option -- a
The first switch is SWITCH=? OPTARG= OPTIND=1
```

The error message can be hidden using a colon as the first character in the switch list. By using :hc:, the error on the bad switch -a disappears, but the bad option is saved in OPTARG to be used in a custom error message.

```bash
$ bash getopt.sh -a
The first switch is SWITCH=? OPTARG=a OPTIND=1
```

You can also hide errors by creating an OPTERR variable with the value of 0. This overrides the contents of the legal switches string.

Switches are usually checked with a while and case statement. See Listing 9.4.

### Listing 9.4 getopt_demo.sh

```bash
#!/bin/bash
#
# This script expects the switch -c and a company name. --help (-h)
# is also allowed.

shopt -s -o nounset

declare -rx SCRIPT=${0##*/}
declare -r OPTSTRING="hc:"
declare SWITCH
declare COMPANY

# Make sure there is at least one parameter

if [ $# -eq 0 ]; then
   printf "%s\n" "Type --help for help."
   exit 192
fi

# Examine individual options

while getopts "$OPTSTRING" SWITCH ; do
   case $SWITCH in
      h) printf "%s\n" "Usage: $SCRIPT [-h] -c companyid"
         exit 0
         ;;
      c) COMPANY="$OPTARG"
         ;;
      \?) exit 192
         ;;
      *) printf "$SCRIPT: $LINENO: %s\n" "script error: unhandled argument"
         exit 192
         ;;
   esac
done

printf "$SCRIPT: %s\n" "Processing files for $COMPANY..."
```

This script is shorter than the positional parameter version. The only error the script must look for is a legitimate switch listed in `OPTSTRING` that isn't handled by the `case` statement.

As a special case, `getopts` can process variables instead of script parameters if they are supplied with the `getopts` command as extra arguments. This can be used to test a switch using specific parameters.
