Listing 24-3B
The del script

```
```
#!/bin/sh
# Delete a file interactively
filename=$1
if test ! -f $filename
then
    echo "There is no file \"$filename\"."
else
    echo "Do you want to delete \"$filename\"?"
    read choice
    if test $choice = y
    then
        rm $filename
        echo "\"$filename\" deleted."
    else
        echo "\"$filename\" not deleted."
    fi
fi
```
```

# 24.4 A Daily Reminder System: tickle

We have already seen how you can use the ca lendar utility to remind yourself of important events. One limitation of ca lendar is that you have to enter each event individually, along with its date. This can be a problem for routine events that happen every day or every week. For reminding yourself of such events, the fol lowing ti ckle script can be very useful. It uses the date command to check the day of the week, then prints out an appropriate message.

Listing 24-4A
Summary of the tickle script.

> NAME
> tickle--a daily reminder service
> SYNOPSIS
> tickle
> DESCRIPTION
> Here is the outline for tickle:
> Select sh
> Use set to capture the output from date
> Print a message
> Check day ($1) and print an appropriate message