
# 29

## FLOW CONTROL: LOOPING WITH WHILE AND UNTIL

In the previous chapter, we developed a menu-driven program to produce various kinds of system information. The program works, but it still has a significant usability problem. It executes only a single choice and then terminates. Even worse, if an invalid selection is made, the program terminates with an error, without giving the user an opportunity to try again. It would be better if we could somehow construct the program so that it could repeat the menu display and selection over and over, until the user chooses to exit the program.

In this chapter, we will look at a programming concept called looping, which can be used to make portions of programs repeat. The shell provides three compound commands for looping. We will look at two of them in this chapter and the third in Chapter 33.

## Looping

Daily life is full of repeated activities. Going to work each day, walking the dog, and slicing a carrot are all tasks that involve repeating a series of steps. Let’s consider slicing a carrot. If we express this activity in pseudocode, it might look something like this:

- 1. Get cutting board.
- 2. Get knife.
- 3. Place carrot on cutting board.
- 4. Lift knife.
- 5. Advance carrot.
- 6. Slice carrot.
- 7. If entire carrot sliced, then quit, else go to step 4.

Steps 4 through 7 form a loop. The actions within the loop are repeated until the condition, "entire carrot sliced," is reached.

### while

bash can express a similar idea. Let’s say we wanted to display five numbers in sequential order from 1 to 5. A bash script could be constructed as follows:

```
#!/bin/bash

# while-count: display a series of numbers

count=1

while [ $count -le 5 ]; do
    echo $count
    count=$(($count + 1))
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

By enclosing the menu in a while loop, we are able to have the program repeat the menu display after each selection. The loop continues as long as REPLY is not equal to 0 and the menu is displayed again, giving the user the opportunity to make another selection. At the end of each action, a sleep command is executed so the program will pause for a few seconds to allow the results of the selection to be seen before the screen is cleared and the menu is redisplayed. Once REPLY is equal to 0, indicating the "quit" selection, the loop terminates and execution continues with the line following done.

### Breaking out of a Loop

bash provides two built-in commands that can be used to control program flow inside loops. The break command immediately terminates a loop, and program control resumes with the next statement following the loop. The continue command causes the remainder of the loop to be skipped, and program control resumes with the next iteration of the loop. Here we see a version of the while-menu program incorporating both break and continue:

```
#!/bin/bash

# while-menu2: a menu driven system information program

DELAY=3 # Number of seconds to display results

while true; do
    clear
    cat <<_EOF_
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
            continue
        fi
        if [[ $REPLY == 2 ]]; then
            df -h
            sleep $DELAY
            continue
        fi
        if [[ $REPLY == 3 ]]; then
            if [[ $(id -u) -eq 0 ]]; then
                echo "Home Space Utilization (All Users)"
                du -sh /home/*
```
```
else
    echo "Home Space Utilization ($USER)"
    du -s $HOME
fi
sleep $DELAY
continue
fi
if [ $REPLY == 0 ]; then
    break
fi
else
    echo "Invalid entry."
    sleep $DELAY
fi
done
echo "Program terminated."
```

In this version of the script, we set up an endless loop (one that never terminates on its own) by using the true command to supply an exit status to while. Since true will always exit with an exit status of 0, the loop will never end. This is a surprisingly common scripting technique. Since the loop will never end on its own, it’s up to the programmer to provide some way to break out of the loop when the time is right. In this script, the break command is used to exit the loop when the 0 selection is chosen. The continue command has been included at the end of the other script choices to allow for more efficient execution. By using continue, the script will skip over code that is not needed when a selection is identified. For example, if the 1 selection is chosen and identified, there is no reason to test for the other selections.

### until

The until command is much like while, except instead of exiting a loop when a non-zero exit status is encountered, it does the opposite. An until loop continues until it receives a 0 exit status. In our while-count script, we continued the loop as long as the value of the count variable was less than or equal to 5. We could get the same result by coding the script with until:

```
#!/bin/bash

# until-count: display a series of numbers

count=1

until [ $count -gt 5 ]; do
    echo $count
    count=$(($count + 1))
done
echo "Finished."
```

By changing the test expression to $count -gt 5, until will terminate the loop at the correct time. Deciding whether to use the while or until loop is usually a matter of choosing the one that allows the clearest test to be written.
