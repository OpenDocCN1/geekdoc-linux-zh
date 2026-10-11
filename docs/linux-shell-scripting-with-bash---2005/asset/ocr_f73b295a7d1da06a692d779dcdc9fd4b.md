Although positional parameters are a straightforward way to view switches and arguments, they do not “walk through” the list. There is a built-in `shift` command that discards the parameter in $1 and moves the remaining parameters down one number to take its place. Using `shift`, you can check each parameter in turn as if it were the first parameter.

Listing 9.2 shows a complete example, using `shift`.

# Listing 9.2 param2.sh

```
#!/bin/bash
#
# param2.sh
#
# This script expects the switch -c and a company name. --help (-h)
# is also allowed.

shopt -s -o nounset
declare -rx SCRIPT=$ {0##*/}

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
            printf "%s\n" "Usage: $SCRIPT [-h] [--help] -c company\r"
            exit 0
        -c) shift
            if [ $# -eq 0 ]; then
                printf "${SCRIPT}:${LINENO}: %s\n" "company for -c is missing" >&2
                exit 192
            fi
            COMPANY="$1"
        ;;
        *) printf "${SCRIPT}:${LINENO}: %s\n" "switch $1 not supported" >&2
        exit 192
```