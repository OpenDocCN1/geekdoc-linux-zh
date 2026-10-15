
## EXAMPLE 12.63

(The Script)

```
$ cat trap.err
#!/bin/ksh
# This trap checks for any command that exits with a nonzero
# status and then prints the message.
1 trap 'print "You gave me a non-integer. Try again."' ERR
2 typeset -i number   # Assignment to number must be integer
3 while true
do
4   print -n "Enter an integer. "
5   read -r number 2>/dev/null
6   if (( $? == 0 ))   # Was an integer read in?
                  # Was the exit status zero?
7   then
      break
   fi
done
8 trap - ERR          # Unset pseudo trap for ERR
n=$number
9 if grep ZOMBIE /etc/passwd > /dev/null 2>&1
then
:
else
10  print "\n is $n. So long"
fi
```

(The Output)

```
$ trap.err
4 Enter an integer. hello
1 You gave me a non-integer. Try again.
4 Enter an integer. good-bye
1 You gave me a non-integer. Try again.
4 Enter an integer. |||
1 You gave me a non-integer. Try again.
4 Enter an integer. 5
10 $n is 5. So long.
$ trap.err
4 Enter an integer. 4.5
10 $n is 4. So long.
```

## EXPLANATION

+   1. The ERR (fake or pseudo) signal will print the message in double quotes any time a command in the program returns a nonzero exit status, that is, fails.
+   2. The typeset command with the -i option creates an integer variable, number, which can only be assigned integers.

## EXPLANATION (CONTINUED)

3 The exit status of the true command is always 0; the body of the while loop is entered.

4 The user is asked to type in an integer.

5 The read command reads user input and assigns it to the number variable. The number must be an integer; if not, an error message will be sent to /dev/null. The -r option to the read command allows you to enter a negative number (starting with the minus sign).

6 If the exit status from the read command is 0, a number was entered, and the if statements will be executed.

7 The break command is executed and the loop exits.

8 The trap for the fake Korn shell signal ERR is unset.

9 When grep fails, it returns a nonzero exit status; if we had not unset the ERR trap, the script would have printed You gave me a non-integer. Try again. So long if the grep failed to find ZOMBIE in the /etc/passwd file.

10 This line is printed if the grep failed. Note that if a floating-point number such as 4.5 is entered, the number is truncated to an integer.

## 12.9.5 Traps and Functions

If trap is used in a function, the trap and its commands are local to the function.

## EXAMPLE 12.64

```
(The Script)
#!/bin/ksh
1 function trapper {
    print "In trapper"
2   trap 'print "Caught in a trap!"' INT
    print "Got here."
    sleep 2S
}
3 while :
do
    print "In the main script"
4   trapper  # Call the function
5   print "Still in main"
    sleep 5
    print "Bye"
done
```

## EXAMPLE 12.64 (CONTINUED)

```
(The Output)
$ functrap
In the main script
In trapper
Got here.
^C Caught in a trap!
$
```

## EXPLANATION

+   1 The function trapper is defined. It contains the trap command.

+   2 The trap command will be executed if Ctrl-C is entered. The print command within the trap is executed and the program continues execution. Ctrl-C is entered while the sleep command is running. Normally, the program will continue to run just after the command where it was interrupted (with the exception of the sleep command, which causes the program to abort). The trap has no effect on lines starting after 4.

+   3 In the main part of the script, a while loop is started. The colon is a do-nothing command that always returns a zero exit status. The loop will go forever.

+   4 Once in the loop, the function trapper is called.

+   5 The trap command within the trapper function will have no effect in this part of the program because the trap is local to the function. If the function exits normally (i.e., ^C is not pressed), execution will continue here. The default behavior for ^C will cause the script to abort if the signal is sent here or to any of the lines that follow.

## 12.10 Coprocesses

A coprocess is a special two-way pipeline that allows shell scripts to write to the standard input of another command and to read from its standard output. This provides a way to create a new interface for an existing program. The append operator, |&, is placed at the end of the command to initiate the command as a coprocess. Normal redirection and background processing should not be used on coprocesses. The print and read commands require a -p switch to read from and write to a coprocess. The output must be sent to standard output and have a newline at the end of each message of output. The standard output must be flushed after each message is sent to standard output. You can run multiple coprocesses by using the exec command with the >&p or <&p operator. To open file descriptor 4 as a coprocess, you would enter exec 4>&p.
