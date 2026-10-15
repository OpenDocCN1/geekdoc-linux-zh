Such accounts shouldn't figure into oldacct's checking. Typically, administrative accounts have low UID numbers. These numbers reside in field three of the /etc/passwd file. On the system for which I originally wrote the oldacct script, the threshold UID was 200. Administrative accounts had UIDs less than 200; regular user accounts used 200 or greater. You'll need to tune the oldacct script to reflect the lowest regular UID your system uses.

# Listing 2.3 (continued)

```
if [ "$5" = "Idle" ]      # Still logged in
then
    continue                 # Keep going
fi

OLDMONTH=$4
OLDDay=$5
OLDYEAR=$6

# If last login was within 6 months, year will be an hh:mm time
if [ $OLDYEAR -gt 999 ]      # It must be >= 6 months old
then
    echo "$u\t$OLDMONTH $OLDDay $OLDYEAR"
    continue
fi

if [ `monthnum $OLDMONTH` -lt $EXPMONTH -o \
`monthnum $OLDMONTH` -gt $CURRMONTH ]
then
    echo "$u\t$OLDMONTH $OLDDay $OLDYEAR"
    continue
fi

if [ `monthnum $OLDMONTH` -eq $EXPMONTH -a $OLDDay -lt $EXPDAY ]
then
    echo "$u\t$OLDMONTH $OLDDay $OLDYEAR"
    continue
fi

done

if [ -n "$NOLOGIN" ]
then
    echo "Never logged in:"
    echo $NOLOGIN | tr ' ' '\012' | pr -t -6
```