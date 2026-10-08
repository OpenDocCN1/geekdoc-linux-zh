# Creating the Phoneadd Shell Program

The Phmenu program offers the option to add a phone record to the corp_phones file; that is, the user interacts with the program to enter a new employee's phone record. To do this, you can use a cursor program, similar to the one you wrote earlier, to design your data entry screen, display it, and place the cursor in the first data-entry field. You can subsequently position it for all the other entries.

# To create the phoneadd program to allow additions:

1  Use the editor of your choice to create the script phoneadd. Enter this code:

```
# ==========================================================
# Script Name: phoneadd
# By: JQD
# Date: March 1999
# Purpose: A shell script that sets up a loop to add new employees to the Corp_phones file.
# Command Syntax: phoneadd
#
# ==========================================================
trap "rm ~/tmp/* 2> /dev/null; exit" 0 1 2 3
phonefile=~/source/corp_phones
looptest=y
while [ $looptest = y ]
do
    clear
    cursor 1 4; echo "Corporate Phone List Additions"
    cursor 2 4; echo "============================="
    cursor 5 4; echo "Last Name : "
    cursor 6 4; echo "First Name : "
    cursor 7 4; echo "Middle Init : "
    cursor 8 4; echo "Dept # : "
    cursor 9 4; echo "Job Title : "
    cursor 10 4; echo "Date Hired : "
    cursor 12 4; echo "Add Another? (Y)es or (Q)uit "
    cursor 4 18; read phonenum
    if [ "$phonenum" = 'q' ]
    then
        { clear; exit }
    fi
    cursor 5 18; read lname
    cursor 6 18; read fname
    cursor 7 18; read midget
    cursor 8 18; read deptno
    cursor 9 18; read jobtitle
    cursor 10 18; read datehired
    # Check to see if last name is not a blank before you
    # write to disk
    if [ "$lname" > "    "]
    then
        echo "$phonenum:$lname:$fname:$midget:$deptno:$jobtitle:$datehired" >> $phonefile
```