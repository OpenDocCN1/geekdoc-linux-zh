```
```sh
monthnum ()
{
    Jan=1 Feb=2 Mar=3 Apr=4 May=5 Jun=6
    Jul=7 Aug=8 Sep=9 Oct=10 Nov=11 Dec=12
    echo `eval echo \$"$1"`             # Show month's number
}

EXPMONTH=`date "+%m"`                    # Get current date
EXPDAY=`date "+%d"`
EXPYEAR=`date "+%Y"`

CURMONTH=$EXPMONTH
CURYEAR=$EXPYEAR

if [ $EXPMONTH -le 3 ]
then
    EXPMONTH=`expr $EXPMONTH + 9`          # Wrap around year
    EXPMONTH=`expr $EXPYEAR - 1`
else
    EXPMONTH=`expr $EXPMONTH - 3`
fi

if [ $EXPMONTH -eq 2 -a $EXPDAY > 28 ]
then
    EXPDAY=28                              # Force Feb 28
fi

#
# Turn month number into that month's name
#

#Months="Jan Feb Mar Apr May Jun Jul Aug Sep Oct Nov Dec"

#set $MONTHS                              # Create associative array
#EXPMONTH=`eval echo $"$EXPMONTH"`        # Select month's name

#
# Collect all non-administrative users' names
#

USERS=""
awk
    BEGIN { FS = ":" }
    $3 >= LOWUID { print $1 }
' LOWUID=$LOWUID $PW_FILE |
sort
```
```