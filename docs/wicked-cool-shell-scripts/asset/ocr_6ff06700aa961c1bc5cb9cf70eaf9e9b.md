```
if [ ! isMonthName $word2 ] ; then
    echo "Bad date format: unknown month name specified." >&2
    exit 1
fi

word2="$(normalize $word2)"

if [ -z "$word3" ] ; then
    date="$word1$word2"
else
    if [ ! -z "$(echo $word3|sed 's/[[ :digit:]]//g')" ] ; then
        echo "Bad date format: third field should be year." >&2
        exit 1
    elif [ $word3 -lt 2000 -o $word3 -gt 2500 ] ; then
        echo "Bad date format: year value should be 2000-2500" >&2
        exit 1
    fi
    date="$word1$word2$word3"
fi

/bin/echo -n "One-line description: "
read description

# Ready to write to data file

echo "$(echo $date|sed 's/ / /g')$description" >> $agendafile

exit 0
```

# Listing 3-12: The addagenda shell script

The second script, in Listing 3-13, is shorter but is used more often.

```
#!/bin/sh

# agenda--Scans through the user's .agenda file to see if there
#  are matches for the current or next day

agendafile="$HOME/.agenda"

checkDate()
{
    # Create the possible default values that will match today.
    weekday=$1  day=$2  month=$3  year=$4
    format1="$weekday"  format2="$day$month"  format3="$day$month$year"

    # And step through the file comparing dates...

    IFS="|"    # The reads will naturally split at the IFS.

echo "On the agenda for today:"
```