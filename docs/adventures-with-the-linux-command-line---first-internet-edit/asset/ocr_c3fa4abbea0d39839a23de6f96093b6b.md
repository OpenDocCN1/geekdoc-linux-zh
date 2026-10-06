```
error_exit() {
    local error_message="$1"
    printf("%s: %s\n" "$PROGNAME" "${error_message:-Unknown Error}" >&2
    clean_up
    exit 1
}
```

```
graceful_exit() {
    clean_up
    exit
}
```

```
signal_exit() { # Handle trapped signals
    local signal="$1"
    case "$signal" in
        INT)
            error_exit "Program interrupted by user"; ;
        TERM)
            error_exit "Terminating on unknown signal"; ;
    esac
}
```

The first group of functions handles parameter parsing. The clean_up function should include the code for any housekeeping tasks needed before the script exits. This function is called by all the other exit functions to ensure an orderly termination.

```
load_libraries() { # Load external shell libraries
    local i
    for i in $LIBS; do
        if [ ! -r "$i" ]; then
            source "%s" || error_exit "Library '$i' contains errors.";
        else
            error_exit "Required library '$i' not found.";
        fi
    done
}
```

The load_libraries function loops through the contents of the LIBS constant and sources each file. If any file is missing or contains errors, this function will terminate the script with an error.

```
usage() {
    printf "%s\n" "Usage: ${PROGNAME} [-h|--help]"
    printf "%s\n" "  ${PROGNAME} [-a|--option_a] [-b|--option_b b_argument]"
}
```

```
help_message() {
    cat <<EOF
$PROGNAME ver. $VERSION
Demonstrate the new_script template
EOF
```

Coding Standards Part 2: new_script 215