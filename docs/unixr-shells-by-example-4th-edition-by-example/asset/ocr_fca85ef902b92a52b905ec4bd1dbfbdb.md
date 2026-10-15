# EXAMPLE 15.19

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

# EXAMPLE 15.20

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