# EXAMPLE 12.63

(The Script)

```
$ cat trap.err
#!/bin/ksh
# This trap checks for any command that exits with a nonzero
# status and then prints the message.
1 trap 'print "You gave me a non-integer. Try again."' ERR
2 typeset -i number   # Assignment to number must be integer
3 while true
do
4   print -n "Enter an integer. "
5   read -r number 2>/dev/null
6   if (( $? == 0 ))   # Was an integer read in?
                  # Was the exit status zero?
7   then
      break
   fi
done
8 trap - ERR          # Unset pseudo trap for ERR
n=$number
9 if grep ZOMBIE /etc/passwd > /dev/null 2>&1
then
:
else
10  print "\n is $n. So long"
fi
```

(The Output)

```
$ trap.err
4 Enter an integer. hello
1 You gave me a non-integer. Try again.
4 Enter an integer. good-bye
1 You gave me a non-integer. Try again.
4 Enter an integer. |||
1 You gave me a non-integer. Try again.
4 Enter an integer. 5
10 $n is 5. So long.
$ trap.err
4 Enter an integer. 4.5
10 $n is 4. So long.
```

# EXPLANATION

+   1. The ERR (fake or pseudo) signal will print the message in double quotes any time a command in the program returns a nonzero exit status, that is, fails.
+   2. The typeset command with the -i option creates an integer variable, number, which can only be assigned integers.