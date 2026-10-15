
awk does the rest of the work with the pared list. awk parses the login name field from the idle time field. Remember that awk sees everything as strings unless you explicitly use a value in a numeric expression. When a value contains anything other than a digit, you must tell awk to convert it to a number. The d at the end of each idle days number prevents awk from seeing the value as numeric. String comparison is inappropriate for comparing the days number with the idle days threshold coming from idleuser’s command line. As a string, 1d would come before 2d, but 9d would come after 10d because the 9 digit comes after the 1 digit. Adding 0 to the value causes awk to take the numeric value of the string, throwing out all nondigit characters after the last digit, and use the result as a number. awk will compare the numbers correctly.

The program shows the names and idle days of only those users idle for more than the command line’s threshold number. If you think that 7 days, 14 days, or even 30 days of idle time is fair, you could use idleuser 30 as your command line or in your cron job. idleuser assumes that you’re not interested in any user idle for fewer than those days. The script reports anyone idle for that number of days or more so that you can decide whether it’s a problem.

## Listing 2.2 The idleuser script reports overly idle users.

```
#!/bin/sh
#
# idleuser
#
# Show users idle longer than specified days.
#
# Copyright 1994, Lawrence S Reznick

if [ $# -ne 1 ]
then
echo "Usage: $0 days\n"
echo "Show users logged in & idle for longer than the specified days."
exit 1
fi

finger |
cut -c9,35-40 |
egrep "[0-9]d" |
awk '
if ( $2 + 0 >= days ) {
print $1, "(" $2 ")";
}
' days=$1
```

## In Search of Ancient Accounts

Using finger to find idle accounts immediately suggests using finger to identify ancient accounts. Sometimes accounts just drop off, and, in a busy job shop with lots of special access and consultant accounts, it is very easy to leave old, unused accounts on the system. Such an account represents a security issue because anyone who once had access to that account could still get in. idleuser used finger's summary output to find information about idle time in days. The oldacct script (Listing 2.3) also uses finger but requests more verbose information about each user.

When you give finger a user's name, even several users' names, it delivers lines for each user, identifying various facts about that user. finger takes most of those facts from the /etc/passwd file, along with the /etc/utmp(4) and /etc/wtmp files, where who(1) and login(1) keep their latest data.

Because finger gives verbose information only when given each user's name individually, oldacct must look through the passwd file to learn the users' names. Every possible account name is in the passwd file, including administrative user accounts and pseudo-user accounts, which may not get used for a very long time.

## Listing 2.3 The oldacct script reports users idle for over 90 days.

```
#!/bin/sh
#
# oldacct
#
# Identify accounts not used for over 90 days.
#
# Copyright 1994, Lawrence S Reznick
#
# 94Apr19 LSR
# Finger doesn't always show "On since" when the user is still logged in.
# If the user has been idle, finger shows the minutes & seconds idle.
# Added a test for "Idle" to catch that. Also found one acct that had a
# home phone field. Finger outputs that on a separate line, pushing the
# "Last logged in" line to the 5th line. The word "Directory:" appears on
# the 4th line when that happens. Added a test to handle that. Finally,
# changed the "Never logged in" code to collect the names. After the loop
# finishes, the names are output in a columnar list. Looks cleaner that way.
PW_FILE=/etc/passwd        # Point to passwd file
LOWUID=200                 # Lowest non-admin UID
```

```
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
