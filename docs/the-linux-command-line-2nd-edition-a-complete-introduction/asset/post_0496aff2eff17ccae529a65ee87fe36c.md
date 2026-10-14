
## Further Reading

- The *Bash Reference Manual* contains a chapter on builtins, which includes the `read` command:
  http://www.gnu.org/software/bash/manual/bashref.html#Bash-Builtins

## 29 – Flow Control: Looping With while / until

In the previous chapter, we developed a menu-driven program to produce various kinds of system information. The program works, but it still has a significant usability problem. It only executes a single choice and then terminates. Even worse, if an invalid selection is made, the program terminates with an error, without giving the user an opportunity to try again. It would be better if we could somehow construct the program so that it could repeat the menu display and selection over and over, until the user chooses to exit the program.

In this chapter, we will look at a programming concept called looping, which can be used to make portions of programs repeat. The shell provides three compound commands for looping. We will look at two of them in this chapter, and the third in a later one.

## Looping

Daily life is full of repeated activities. Going to work each day, walking the dog, slicing a carrot are all tasks that involve repeating a series of steps. Let's consider slicing a carrot. If we express this activity in pseudocode, it might look something like this:

- 1. get cutting board
- 2. get knife
- 3. place carrot on cutting board
- 4. lift knife
- 5. advance carrot
- 6. slice carrot
- 7. if entire carrot sliced, then quit, else go to step 4

Steps 4 through 7 form a loop. The actions within the loop are repeated until the condition, “entire carrot sliced,” is reached.

```
while
```

bash can express a similar idea. Let's say we wanted to display five numbers in sequential order from one to five. a bash script could be constructed as follows:

```
#!/bin/bash

# while-count: display a series of numbers

count=1

while [[ $count -le 5 ]]; do
    echo $count
    count=$((count + 1))
done
echo "Finished."
```

When executed, this script displays the following:

```
[me@linuxbox ~]$ while-count
1
2
3
4
5
Finished.
```

The syntax of the while command is:

```
while commands; do commands; done
```

Like if, while evaluates the exit status of a list of commands. As long as the exit status is zero, it performs the commands inside the loop. In the script above, the variable count is created and assigned an initial value of 1. The while command evaluates the exit status of the test command. As long as the test command returns an exit status of zero, the commands within the loop are executed. At the end of each cycle, the test command is repeated. After six iterations of the loop, the value of count has increased to 6, the test command no longer returns an exit status of zero and the loop terminates. The program continues with the next statement following the loop.

We can use a while loop to improve the read-menu program from the previous chapter:

```
#!/bin/bash

# while-menu: a menu driven system information program
```

```
DELAY=3 # Number of seconds to display results

while [[ $REPLY != 0 ]]; do
    clear
    cat << _EOF_
Please Select:

    1. Display System Information
    2. Display Disk Space
    3. Display Home Space Utilization
    0. Quit

_EOF_
    read -p "Enter selection [0-3] > "

    if [[ $REPLY =~ ^[0-3]$ ]]; then
        if [[ $REPLY == 1 ]]; then
            echo "Hostname: $HOSTNAME"
            uptime
            sleep $DELAY
        fi
        if [[ $REPLY == 2 ]]; then
            df -h
            sleep $DELAY
        fi
        if [[ $REPLY == 3 ]]; then
            if [[ $(id -u) -eq 0 ]]; then
                echo "Home Space Utilization (All Users)"
                du -sh /home/*
            else
                echo "Home Space Utilization ($USER)"
                du -sh $HOME
            fi
            sleep $DELAY
        fi
    else
        echo "Invalid entry."
        sleep $DELAY
    fi
done
echo "Program terminated."
```

By enclosing the menu in a while loop, we are able to have the program repeat the menu display after each selection. The loop continues as long as REPLY is not equal to "0" and the menu is displayed again, giving the user the opportunity to make another selection. At the end of each action, a sleep command is executed so the program will pause for a few seconds to allow the results of the selection to be seen before the screen is cleared and the menu is redisplayed. Once REPLY is equal to "0," indicating the "quit" selection,
