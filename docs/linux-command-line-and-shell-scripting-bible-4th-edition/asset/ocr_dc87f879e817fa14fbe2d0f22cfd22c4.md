**are only a few years older may have the earlier version of the xargs command, so we kept the absolute directory references.**

All three commands are hooked together via a pipe. The ps command produces a list of the user's running processes, which include the PID of each process. The ps command passes its standard output (STDOUT) as STDIN to the gawk command. The gawk command, in turn, strips off only the PIDs from the ps command's STDOUT (Chapter 15). The xargs command takes each PID the gawk command produces as STDIN. It creates and executes the kill command for each PID to kill all the user's running processes. The entire command pipe looks like this:

```
$command_1 | gawk '{print $1}' | $command_3
```

Thus, the complete case statement for killing off any of the user account's running processes is as follows:

```
case $answer in
y|Y)    # If user answers "yes",
        # kill User Account processes.
        #
        echo
        echo "Killing off process(es)...
        #
        # List user process running code in command_1
        command_1="ps -u $user_account --no-heading"
        #
        # Create command_3 to kill processes in variable
        command_3="xargs -d \\n /usr/bin/sudo /bin/kill -9"
        #
        # Kill processes via piping commands together
        $command_1 | gawk '{print $1}' | $command_3
        #
        echo
        echo "Process(es) killed."
        ;;
*)      #If user answers anything but "yes", do not kill.
        echo
        echo "Will not kill process(es)."
        ;;
esac
```

By far, this is the most complicated piece of the script! However, now