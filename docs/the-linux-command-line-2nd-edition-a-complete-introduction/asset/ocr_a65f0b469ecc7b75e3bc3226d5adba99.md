```
echo "Home Space Utilization ($USER)"
du -sh $HOME
fi
sleep $DELAY
continue
fi
if [[ $REPLY == 0 ]]; then
break
fi
else
echo "Invalid entry."
sleep $DELAY
fi
done
echo "Program terminated."
```

In this version of the script, we set up an endless loop (one that never terminates on its own) by using the true command to supply an exit status to while. Since true will always exit with an exit status of zero, the loop will never end. This is a surprisingly common scripting technique. Since the loop will never end on its own, it’s up to the programmer to provide some way to break out of the loop when the time is right. In this script, the break command is used to exit the loop when the “0” selection is chosen. The continue command has been included at the end of the other script choices to allow for more efficient execution. By using continue, the script will skip over code that is not needed when a selection is identified. For example, if the “1” selection is chosen and identified, there is no reason to test for the other selections.

# until

The until command is much like while, except instead of exiting a loop when a non-zero exit status is encountered, it does the opposite. An until loop continues until it receives a zero exit status. In our while-count script, we continued the loop as long as the value of the count variable was less than or equal to 5. We could get the same result by coding the script with until:

```
#!/bin/bash

# until-count: display a series of numbers

count=1

until [[ $count -gt 5 ]]; do
    echo $count
```