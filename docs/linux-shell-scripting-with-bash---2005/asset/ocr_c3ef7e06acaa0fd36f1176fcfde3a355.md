signal generated when a window changes its size. By installing a trap, a message can be displayed each time the window is resized.

$ trap "printf "There are %s lines\n" "${LINES}" SIGWINCH

Altering the window size results in:

$ There are 32 lines
$ There are 43 lines
$ There are 37 lines

You can view the current trap with the -p (print) switch.

$ trap -p SIGWINCH
trap -- "printf "There are %s lines\n" "${LINES}" SIGWINCH

To restore the default handler, don’t supply a trap.

$ trap SIGWINCH
$ trap -p SIGWINCH

SIGUSR1 and SIGUSR2 are user-defined signals that have no pre-defined meaning. They can be freely used in scripts. When the following script receives a SIGUSR1 signal, it waits for the current command to complete, prints the message SIGUSR1, and resumes the script, as shown in Listing 10.2.

# Listing 10.2 trap_demo.sh

```
#!/bin/bash
#
# trap_demo.sh
#
# Wait indefinitely for SIGUSR1, print a message when one arrives.

shopt -s -o nounset
trap 'printf "SIGUSR1\n"' SIGUSR1

# Infinite loop!
while true ; do
    sleep 1
done

printf "%s\n" "Should never get here!" >&2
exit 192
```

The script continues until killed.

$ bash trap_demo.sh &
[1] 544