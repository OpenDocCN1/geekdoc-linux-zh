
Finally, how many days into the current year are we? That's easily done at 9.

```
dayofyear=$( $date +%j )
```

Then it's just a matter of summing up the days to get the result!

## Running the Script

Let's look at those historical dates again in Listing 15-4.

```
$ daysago 7 20 1969
17106 days have elapsed between 7/20/1969 and today, day 141 of 2016.
```

```
$ daysago 6 6 1944
26281 days have elapsed between 6/6/1944 and today, day 141 of 2016.
```

```
$ daysago 1 1 2010
2331 days have elapsed between 1/1/2010 and today, day 141 of 2016.
```

Listing 15-4: Running the daysago script with various dates

These were all run on . . . Well, let's let date tell us:

```
$ date
Fri May 20 13:30:49 UTC 2016
```

## Hacking the Script

There are additional error conditions that the script isn't catching, notably the edge cases when the date in the past is just a few days ago or even a few days in the future. What happens, and how can you fix it? (Tip: look at Script #101 to see additional tests you can apply to this script.)

## #101 Calculating Days Until a Specified Date

The logical partner of Script #100, daysago, is another script, daysuntil. This script essentially performs the same calculation but modifies the logic to count days left in the current year, days in intervening years, and days before the specified date in the target year, as shown in Listing 15-5.

### The Code

```
#!/bin/bash
# daysuntil--Basically, this is the daysago script backward, where the
#   desired date is set as the current date and the current date is used
#   as the basis of the daysago calculation.
# As in the previous script, use 'which gdate' if you are on OS X.
# If you are on Linux, use 'which date'.
date="$(which gdate)"

function daysInMonth
{
case $1 in
1|3|5|7|8|10|12 ) dim=31 ;;  # Most common value
4|6|9|11          ) dim=30 ;;
2                ) dim=29 ;;  # Depending on whether it's a leap year
*                ) dim=-1 ;;  # Unknown month
esac
}

function isleap
{
# If specified year is a leap year, returns nonzero value for $leapyear

leapyear=$( $date -d 12/31/$1 +%j | grep 366 )
}

####################
### MAIN BLOCK
####################

if [ $# -ne 3 ] ; then
echo "Usage: $(basename $0) mon day year"
echo "  with just numerical values (ex: 1 1 2020)"
exit 1
fi

$date --version > /dev/null 2>&1      # Discard error, if any.

if [ $? -ne 0 ] ; then
echo "Sorry, but $(basename $0) can't run without GNU date." >&2
exit 1
fi

eval $( $date +"thismon=%m;thisday=%d;thisyear=%Y;dayofyear=%j" )

endmon=$1; endday=$2; endyear=$3

# Lots of parameter checks needed...

daysInMonth $endmon  # Sets $dim variable
if [ $endday -lt 0 -o $endday -gt $dim ] ; then
echo "Invalid: Month #$endmon only has $dim days." >&2
exit 1
fi

if [ $endmon -eq 2 -a $endday -eq 29 ] ; then
isleap $endyear
if [ -z ${leapyear} ] ; then
  echo "Invalid: $endyear wasn't a leapyear; February had 28 days." >&2
  exit 1
fi
fi

if [ $endyear -lt $thisyear ] ; then
  echo "Invalid: $endmon/$endday/$endyear is prior to the current year." >&2
  exit 1
fi

if [ $endyear -eq $thisyear -a $endmon -lt $thismon ] ; then
  echo "Invalid: $endmon/$endday/$endyear is prior to the current month." >&2
  exit 1
fi

if [ $endyear -eq $thisyear -a $endmon -eq $thismon -a $endday -lt $thisday ]
then
  echo "Invalid: $endmon/$endday/$endyear is prior to the current date." >&2
  exit 1
fi

if [ $endyear -eq $thisyear -a $endmon -eq $thismon -a $endday -eq $thisday ]
then
  echo "There are zero days between $endmon/$endday/$endyear and today." >&2
  exit 0
fi

#### If we're working with the same year, the calculation is a bit different.

if [ $endyear -eq $thisyear ] ; then
  totaldays=$(($(date -d "$endmon/$endday/$endyear" +%j) - $(date +%j)))
else

#### Calculate this in chunks, starting with days left in this year.

#### DAYS LEFT IN START YEAR

# Calculate the date string format for the specified starting date.

thisdatefmt="$thismon/$thisday/$thisyear"

calculate="$(date -d \"12/31/$thisyear\" +%j) - $(date -d $thisdatefmt +%j)"

daysleftinyear=$(($calculate))

#### DAYS IN INTERVENING YEARS

daysbetweenyears=0
tempyear=$(($thisyear + 1))
```
