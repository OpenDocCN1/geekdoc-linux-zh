
## EXAMPLE 14.4

(The Script)

```
#!/bin/bash
# Scriptname: nosy
echo -e "Are you happy? \c"
1  read answer
echo "$answer is the right response."
echo -e "What is your full name? \c"
2  read first middle last
echo "Hello $first"
echo -n "where do you work? "
3  read
4  echo I guess $REPLY keeps you busy!
5  read -p "Enter your job title: "
6  echo "I thought you might be an $REPLY."
echo -n "Who are your best friends? "
8  read -a friends
echo "Say hi to ${friends[2]}."
```

(The Output)

```
$ nosy
Are you happy? Yes
1  Yes is the right response.
2  What is your full name? Jon Jake Jones
Hello Jon
3  Where do you work? the Chico Nut Factory
4  I guess the Chico Nut Factory keeps you busy!
5  Enter your job title: Accountant
6  I thought you might be an Accountant.
7,8  Who are your best friends? Melvin Tim Ernesto
9  Say hi to Ernesto.
```

a. The commands listed below this line are not implemented on versions of bash prior to 2.x.

## EXPLANATION

- 1 The read command accepts a line of user input and assigns the input to the variable answer.
- 2 The read command accepts input from the user and assigns the first word of input to the variable first, the second word of input to the variable middle, and all the rest of the words up to the end of the line to the variable last.
- 3 A line is read from standard input and stored in the built-in REPLY variable.
- 4 The value of the REPLY variable is printed.

## EXPLANATION (CONTINUED)

- 5 With the -p option, the read command produces a prompt. Enter your job title: and stores the line of input in the special built-in REPLY variable.
- 6 The value of the REPLY variable is displayed in the string.
- 7 The user is asked to enter input.
- 8 With the -a option, the read command takes input as an array of words. The array is called friends. The elements read into the array are Melvin, Tim, and Ernesto.
- 9 The third element of the friends array, Ernesto, is printed. Array indices start at 0.

## EXAMPLE 14.3

(The Script)

```
#!/bin/bash
# Scriptname: printer_check
# Script to clear a hung-up printer
1 if [ $LOGNAME != root ]
then
echo "Must have root privileges to run this program"
exit 1
fi
2 cat << EOF
Warning: All jobs in the printer queue will be removed.
Please turn off the printer now. Press return when you
are ready to continue. Otherwise press Control C.
EOF
3 read JUNK    # Wait until the user turns off the printer
echo
4 /etc/rc.d/init.d/lpd stop      # Stop the printer
5 echo -e "\nPlease turn the printer on now."
6 echo "Press Enter to continue"
7 read JUNK            # Stall until the user turns the printer back on
echo                  # A blank line is printed
8 /etc/rc.d/init.d/lpd start   # Start the printer
```

## EXPLANATION

- 1 Checks to see if user is root. If not, sends an error and exits.
- 2 Creates a here document. Warning message is displayed on the screen.
- 3 The read command waits for user input. When the user presses Enter, the variable JUNK accepts whatever is typed. The variable is not used for anything. The read in this case is used to wait until the user turns off the printer, comes back, and presses Enter.
- 4 The lpd program stops the print daemon.
- 5 Now it's time to turn the printer back on!

## EXPLANATION (CONTINUED)

- 6 The user is asked to press Enter when ready.
- 7 Whatever the user types is read into the variable JUNK, and when Enter is pressed, the program will resume execution.
- 8 The lpd program starts the print daemon.

## 14.3 Arithmetic

### 14.3.1 Integers (declare and let Commands)

### The declare Command.

Variables can be declared as integers with the declare -i command. If you attempt to assign any string value, bash assigns 0 to the variable. Arithmetic can be performed on variables that have been declared as integers. (If the variable has not been declared as an integer, the built-in let command allows arithmetic operations. See "The let Command" on page 873.) If you attempt to assign a floating-point number, bash reports a syntax error. Numbers can also be represented in different bases such as binary, octal, and hex.

## EXAMPLE 14.6

```
1 $ declare -i num
2 $ num=hello
$ echo $num
0
3 $ num=5 + 5
bash: +: command not found
4 $ num=3+5
$ echo $num
10
5 $ num=4*6
$ echo $num
24
6 $ num="4 + 6"
$ echo $num
24
7 $ num=6.5
bash: num: 6:5: syntax error in expression (remainder of expression is ".5")
```

## EXPLANATION

- 1 The declare command with the -i option creates an integer variable num.
- 2 Trying to assign the string hello to the integer variable num causes the string to be stored as 0.
