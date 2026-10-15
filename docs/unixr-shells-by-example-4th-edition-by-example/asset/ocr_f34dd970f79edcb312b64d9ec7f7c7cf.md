# EXAMPLE 2.6 (CONTINUED)

```
13    if (( ${#foods[*]} == $n ))
        then
            set -A foods cheese crackers shrimp drinks "hot dogs"
                         sandwiches
        fi
    fi
15 done
print "Bye..."
```

# EXPLANATION

1 This line lets the kernel know that you are running a Korn shell script.

2 This is a comment. It is ignored by the shell, but important for anyone trying to understand what the script is doing.

3 The variable guestfile is set to the full pathname of a file called guests.

4 This line reads: If the file guests does not exist, then print to the screen "guests non-existent" and exit from the script.

5 An environment variable is assigned a value and exported (made available to sub-shells).

6 The output of the UNIX/Linux command, the hour of the day, is assigned to the variable called Time. Variables are assigned the values for the place and time.

7 The list of foods to bring is assigned to an array called foods with the set -A command. Each item on the list can be accessed with an index starting at 0.

8 The typeset -i command is used to create an integer value.

9 For each person on the guest list a mail message will be created inviting the person to a party at a given place and time, and assigning a food from the list to bring.

10 The condition tests for the user root. If the user is root, control will go back to the top of the loop and assign the next user in the guest list to the variable, person.

11 The mail message is sent. The message body is contained in a here document.

12 The variable n is incremented by 1.

13 If the number of elements in the array is equal to the value of the variable, then the end of the array has been reached.

14 This marks the end of the looping statements.