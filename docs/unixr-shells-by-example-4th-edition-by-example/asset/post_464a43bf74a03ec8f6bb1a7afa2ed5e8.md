
# Exit Status with an if Conditional.

When the if command is evaluating the success or failure of a command, it checks the exit status of that command. If the exit status is 0, the command was successful and if nonzero the command failed in some way. If you are not sure of what exit status a command returns, you should check before using it, or your program may not perform as expected. Consider the following example. The awk, sed, and grep commands are all able to use regular expressions for searches in a pattern, but grep is the only one of the three commands that reports a nonzero exit status if it cannot find the search pattern. The sed and awk programs will return 0, whether the pattern is found or not. Therefore, neither of these programs would be of any use after an if condition, because the condition would always be true.

## EXAMPLE 13.16

```
#!/bin/sh
name="Fred Fardbuckle"
if grep "$name" db > /dev/null 2>&1
then
echo Found $name
else
echo "Didn't find $name"     # Fred is not in the db file
fi
if awk "/$name/" db > /dev/null 2>&1
then
echo Found $name
else
echo "Didn't find $name"
fi
if sed -n "/$name/p" db > /dev/null 2>&1
then
echo Found $name
else
echo "Didn't find $name"
fi
```

(Output)
4 grep: Didn't find Fred Fardbuckle
6 awk: Found Fred Fardbuckle
8 sed: Found Fred Fardbuckle

Possible Fix

Check the exit status of the command before using it.

```
awk "/$name/" db
echo $? (bash, sh, ksh)
echo $status (tcsh, csh, bash)
```

## EXPLANATION

Here we see that awk, nawk, and gawk always return an exit status of 0, unless the command statements are incorrect. grep returns an exit status of 0 if its search is successful, and a nonzero integer if it cannot find the pattern in the file or if the file does not exist.

# Lacking Robustness.

A program is robust if it can handle illegal input and other unexpected situations in a reasonable way. For example, if a program is expecting numeric data, then it must be able to check to see if that's what it got, and print an error message and ignore the bad input. Another example of robustness would be if the script is going to extract data from an external file, but the external file doesn't exist or does not have read permissions. The robust program would use file testing to check for the existence of the file before trying to read from it.

Example 15.17 shows how to check for null input.

## EXAMPLE 15.17

```
#!/bin/csh
# Program should check for null input -- T and TC shells

1 echo -n "Enter your name: "
set name = $<
    # if user enters nothing, program will hang
2 if ( `grep "$name" db >& /dev/null` ) then
    echo Found name
endif

(Output)
Enter your name: Ellie
Found name

Enter your name:
<program prints every line in the file Found name>

--------------------------------Possible Fix--------------------------------

echo -n "Enter your name: "
set name = $<
    # if user enters nothing, program will hang
3 while ( $name == "" )
    echo "Error: you did not enter anything."
    echo -n "Please enter your name"
    set name = $<
end
<program continues here>
```

## EXPLANATION

1 The user is asked for input. If he or she presses the Enter key, the variable, name, will be set to null.

## EXAMPLE 15.19

```
#!/bin/csh
# Script: renames a file -- C/TC shells

1 if ( $#argv < 2 ) then      # Argument checking
2   echo "Usage: $0 file1 file2"
3   exit 1
endif
if ( -e $1 ) then            # Check for file existence
  mv $1 $2                   # Rename file1
  echo "$1 has been renamed to $2"
else
  echo "$1 doesn't exist"
  exit 2
endif

(Output)
% ./rename file1
Usage: mytest file1 file2
```

Examples 15.20 and 15.21 show how to check for numeric input.

## EXAMPLE 15.20

```
(The Script)
$ cat trap.err
#!/bin/ksh
# This trap checks for any command that exits with a nonzero
# status and then prints the message -- Korn shell

1 trap 'print "You gave me a non-integer. Try again."' ERR
2 typeset -i number          # Assignment to number must be integer
3 while true
do
4   print -n "Enter an integer. "
5   read -r number 2> /dev/null
6   if ( ( $? == 0 ) )        # Was an integer read in?
   then                       # Was the exit status zero?
7     break
   fi
done
8 trap -- ERR                # Unset pseudo trap for ERR
n=$number
```
