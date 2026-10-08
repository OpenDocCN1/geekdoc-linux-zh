# # Advanced Bash-Scripting Guide

```
month_length () # Takes month number as an argument.
{
  # Returns number of days in month.
  monthD="31 28 31 30 31 30 31 30" # Declare as local?
  echo "$monthD" | awk '{print \$1}' # Tricky.
  #...
}
# Parameter passed to function ($1 -- month number), then to awk.
# Awk sees this as "print $1" . print "$2" (depending on month number)
# Template for passing a parameter to embedded awk script:
  $=$=$(script_parameter)
```

Here's a slightly simpler awk construct:
echo $monthD | awk -v month=$1 '{print $(month)}'
Uses the -v option, which assigns a variable value
prior to execution of the awk program.
Thank you, Rick.

# Needs error checking for correct parameter range (1-12)
# and for February in leap year.

```
# Usage example:
month=4 # April, for example (4th month).
days_in=$($month_length $month)
echo $days_in # 30
```

See also Example A-7 and Example A-37.

**Exercise:** Using what we have just learned, extend the previous **Roman numerals** to accept arbitrarily large input.

# Redirection

Redirecting the stdin of a function
A function is essential to a code block, which means its stdin can be redirected (as in Example 3-1).

# Example 24-11. Real name from username

```
#!/bin/bash
# realname.sh
#n# From username, gets "real name" from /etc/passwd.
```

```
ARGCOUNT=1 # Expect one arg.
E_WRONGARGS=85

file=/etc/passwd
pattern=$1

if [ $# -ne "$ARGCOUNT" ];
then
  echo "Usage: `basename $0` USERNAME"
  exit $E_WRONGARGS
fi
```

```
file_excerpt () # Scan file for pattern,
{
+# then print relevant portion of line.
```

Chapter 24. Functions