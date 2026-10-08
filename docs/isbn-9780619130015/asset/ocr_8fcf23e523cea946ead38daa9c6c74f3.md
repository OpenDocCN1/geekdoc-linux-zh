In the following steps, you will add input validation code to the phoneadd script.

**To prevent phone number duplications:**

+   1  Make sure you are in the source directory. Load the phoneadd script into vi or Emacs.

+   2  Add the boldfaced section of code to complete the revised script.

```
```bash
#!/bin/bash
#==========================================
# Script Name:  phoneadd
# By:           JQD
# Date:         March 1999
# Purpose:      A shell script that sets up a loop to add
#               new employees to the phonelist file.
#
#               The code also prevents duplicate phone
#
#               numbers
#
#               from being assigned.
# Command Line:     phoneadd
# ===================================================
trap "rm -/tmp/* 2> /dev/null; exit" 0 1 2 3
phonefile=~/corp_phones
looptest=y
while test "$looptest" = "y"
do
	clear
	cursor 1 4 ; echo "Corporate Phone List Additions"
	cursor 2 4 ; echo "=============================="
	cursor 4 4 ; echo "Phone Number: "
	cursor 5 4 ; echo "Last Name    : "
	cursor 6 4 ; echo "First Name  : "
	cursor 7 4 ; echo "Middle Init : "
	cursor 8 4 ; echo "Dept #      : "
	cursor 9 4 ; echo "Job Title   : "
	cursor 10 4 ; echo "Date Hired  : "
	cursor 12 4 ; echo "Add another? (y)es or (q)uit "
	cursor 4 18; read phonenum
	if   test $phonenum = "q"
	then
		clear ; exit
	fi
```
```