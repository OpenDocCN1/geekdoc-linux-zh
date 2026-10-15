# In Search of Ancient Accounts

Using finger to find idle accounts immediately suggests using finger to identify ancient accounts. Sometimes accounts just drop off, and, in a busy job shop with lots of special access and consultant accounts, it is very easy to leave old, unused accounts on the system. Such an account represents a security issue because anyone who once had access to that account could still get in. idleuser used finger's summary output to find information about idle time in days. The oldacct script (Listing 2.3) also uses finger but requests more verbose information about each user.

When you give finger a user's name, even several users' names, it delivers lines for each user, identifying various facts about that user. finger takes most of those facts from the /etc/passwd file, along with the /etc/utmp(4) and /etc/wtmp files, where who(1) and login(1) keep their latest data.

Because finger gives verbose information only when given each user's name individually, oldacct must look through the passwd file to learn the users' names. Every possible account name is in the passwd file, including administrative user accounts and pseudo-user accounts, which may not get used for a very long time.

# Listing 2.3 The oldacct script reports users idle for over 90 days.

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