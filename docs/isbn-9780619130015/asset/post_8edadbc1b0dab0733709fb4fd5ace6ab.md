
3. Save the file and exit the editor.
4. Log out and log back on to load the functions.
5. Test the `sort_name`, `sort_dept`, and other functions.

Your last task is to display the phone listing in sorted order by employees' last names. You can do this by using your sort_name function, as stored in the .myfuncs file.

## Sorting the Phone List

To sort the phone list, make a minor revision to phlist1 to load the functions and then call sort_name to redirect the sorted output to a temporary file. The sorted temporary file serves as input to the Awk program that displays the records. The revised code will use the CLEAR variable also.

To sort the phone listing:

1. Make sure you are in the source directory. Use the vi or Emacs editor to add the code to the phlist1 script. The additions and revisions are in boldface.

```bash
#!/bin/bash
#==============================================================
# Script Name: phlist1
# By:      JQD
# Date:    March 1999
# Purpose:Use awk to format a colon-separated set of fields
#        in a flat file and display to the screen
# Command line:     bash phlist  <enter>
# ==============================================================
echo "$CLEAR"
cursor 2 20; echo "Corporate Phone List"
cursor 3 20; echo "==================="
cursor 5 0;
sort_name > sorted_phones
awk -F': ' '{ printf "%-12s %-12s %s\t%s%s$10.10s $s\n",
$2, $3, $4, $1, $5, $6, $7 }' sorted_phones

cursor 23 1; echo "Review"
cursor 23 8; read prompt
```

2. This code assumes you have modified your .bashrc file so it loads the functions in .myfuncs when you log on. Save the file and exit the editor.

3. Test the file by typing phlist1 and pressing Enter. Your screen looks similar to Figure 7-33. Press Enter when you finish observing the screen.

![](img/6d8286a85e2d8ad63e16f1801102da59_285_0.png)

**Figure 7-33:** Output of revised plist1 script

Adding code to call the other sort functions will be an exercise at the end of this chapter.

In this chapter you have learned to plan algorithms and programs using flowcharts and pseudocode. You have also learned to create complex decision expressions with the test command. You have furthered your use of the grep, tr, and sed commands to format output. In addition, you have learned advanced programming techniques, such as repositioning the cursor at a previous field in a data entry screen, and creating shell functions.

## SUMMARY

- To speed clearing the screen, assign the clear command sequence to the shell variable CLEAR that can be set inside your login script, .bashrc. This clears your screen faster because it does not require a look-up sequence in a file every time it executes.
- An algorithm is a sequence of instructions or commands that produce a desired result. Following the logic flow expressed in flowcharts and pseudocode develops algorithms.
- Shell functions can simplify the program code by isolating code that can be reused throughout that program as well as others.

## COMMAND SUMMARY

Options and arguments of test command

| Option | Meaning | Example Command |
| :--- | :--- | :--- |
| -eq | equal to | test a -eq b |
| -gt | greater than | test a -gt b |
| -lt | less than | test a -lt b |
| -ge | greater than or equal to | test a -ge b |
| -le | less than or equal to | test a -le b |
| -ne | not equal to | test a -ne b |
| -z | Tests for a zero-length string | test -z string |
| -n | Tests for a non-zero string length | test -n string |
| string1 = string2 | Tests two strings for equality | test string1 = string2 |
| string1 != string2 | Tests two strings for inequality | test string1 != string2 |
| string | Tests for a non-zero string length | test string |
| -e | True if a file exists | test -e file |
| -r | True if a file exists and is readable | test -r file |
| -w | True if a file exists and is writeable | test -w file |
| -x | True if a file exists and is executable | test -x file |
| -d | True if a file exists and is a directory | test -d file |
| -f | Tests if a file exists and is a regular file | test -f file |
| -s | True if a file exists and has a size greater than zero | test -s file |
| -c | Tests if a file exists and is a character special file (which is a character-oriented device, such as a terminal or printer) | test -c file |
| -b | Tests if a file exists and is a block special file (which is a block-oriented device, such as a disk or tape drive) | test -b file |
| -a | Logical AND | test expression1 -a expression2 |
| -o | Logical OR | test expression1 -o expression2 |
| ! | Logical negation | test !expression |

## REVIEW QUESTIONS

1. An algorithm is _________ .
    a. a name that replaces the standard UNIX command name
    b. an alternate name for a UNIX command
    c. always entered into the system-wide initialization file, /etc/profile
    d. a derived formula made up of a sequence of commands that produce a desired result

2. A shell function can be recognized because it has _______ after the function name.
    a. curly braces
    b. parentheses
    c. brackets
    d. quotation marks

3. A shell function's commands are enclosed inside _______ .
    a. curly braces
    b. parentheses
    c. brackets
    d. quotation marks

4. Shell functions are useful because _______ .
    a. you can reuse the code in other programs
    b. it cuts down on re-entry of duplicate code inside shell programs
    c. increases your productivity as a shell programmer
    d. all of the above

5. What is the proper sequence for developing an algorithm?
    a. flowchart—algorithm—pseudocode
    b. flowchart—pseudocode—algorithm.
    c. algorithm—flowchart—pseudocode
    d. there is no one correct sequence

6. How do you pass arguments to a shell function?
    a. Enclose them inside the parentheses that follow the function name.
    b. Use the positional variables, $1, $2, $3 ... $9.
    c. Use the $? shell variable.
    d. Use $# shell variable.

7. The output of a command can be stored in a shell variable by enclosing the command in _______ .
    a. parentheses
    b. double quotation marks
    c. single quotation marks
    d. back quote marks

8. Writing code to test and determine if user input is correct is known as _______.
    a. algorithm design
    b. data validation
    c. flowcharting
    d. pseudocode design

9. If `.numeric_functions` is a script file of shell functions, the _______ command is used to load it into memory.
    a. numeric_functions
    b. load numeric_functions
    c. .numeric_functions
    d. install numeric_functions

10. True or false: shell functions may be executed from the command line.

## EXERCISES

1. From the command line create the function dir to execute this: `ls -l | more`.

2. From the command line create the function simple_date to execute this: `date +%D`.

3. Create the executable script file `.mystuff` to contain the two functions created in Exercises 1 and 2, and to call each function from the command line.

4. In the Lesson A exercises, you created the file my_old_cars. Write a shell script that allows the user to enter a search string and displays all records in the file that contain a string matching the search string. For example, if the user enters "Ford", the script displays all records that contain the word "Ford."

5. Write a shell script that allows the user to enter a search string and deletes all records in the my_old_cars file that contain a string matching the search string. For example, if the user enters "1948," the script deletes all records containing "1948."

6. Create shell functions that sort the records in the file my_old_cars. Your functions should sort the records by year model (the first field), by make (the second field), and by car model (the third field). Write a menu program that calls each sort function.

7. Write a Main menu program for the my_old_cars file and all the script files you have created so far. Here is a list of the script files you should have:
    - Data entry screen
    - Script that displays all records in the file
    - Script that searches for and displays records containing a string
    - Script that deletes specified records from the file
    - Script that displays the records sorted in various ways
