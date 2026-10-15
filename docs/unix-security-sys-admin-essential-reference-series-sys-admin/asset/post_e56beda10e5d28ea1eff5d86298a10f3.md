
# Listing 2.4 (continued)

```
weeknum ()
{
    echo $1 |
    awk '
    #
    for (i = 1; i <= length; i++) |
        i = length;
        do |
            sum += 64;
            sum += index(digits, substr($0, i, 1)) - 1;
        | while (--i);
    }
    END |
        print sum;
    |
    ' digits=$DIGITS
}
# Given a comma-separated number list (max,min,elapsed),
# output aging code
#
code_val ()
{
    echo $1 |
    awk -f '
    $1 < 0 || $1 >= length(digits) {
        print "Max out of range! 0 <= Max < ", length(digits);
        exit;
    }
    $2 < 0 || $2 >= length(digits) {
        print "Min out of range! 0 <= Min < ", length(digits);
        exit;
    }
    |
```

The code_val function also required changing to handle the reverse place-value problem. Values are passed to this function as a comma-separated list. Because /etc/passwd requires the maximum and minimum values to be single-character values, though a user could pass test values of any amount, the awk program range-checks them. Encoded values show as a set of characters, such as 00AH where the o is the MAX, the 0 is the MIN, and the AH is the weeks ELAPSED. The code produced can simply receive these characters concatenated. Because the MAX and MIN are single characters, awk's substr() function is sufficient.

The elapsed value requires base-64 decomposition. awk doesn't have Boolean AND or bit-shifting operators, so division and remainder operators are needed. These operations don't change with the reverse place-value order, but the concatenation sequence does. The original version showing the mathematically correct digit construction, appending the base-64 number to the latest digit's value, remains as a comment for interested readers. To get reverse place-order sequence, append the latest digit to the base-64 number constructed instead. The final base-64 number, whatever the place-value order, is concatenated to the MAX and MIN codes and omitted from the code_val function.

aging_val converts an encoded aging value into its decimal form. aging_val uses expr()'s colon operator to extract the MAX, MIN, and ELAPSED substring codes, and the weeknum function to show their decimal equivalents. One key issue is that HP-UX's /etc/passwd specifies that a missing elapsed code is equivalent to a 0 value. To make the code regular, aging_val appends the ..0 value to the code. Finally, in displaying the time elapsed since the last change, I chose to show how long ago the password was changed. This number is dynamic. As time passes from week to week, running the chkaging program will show different values for the same account.

show_aging is the default operating function for the chkaging program. It extracts the user names and their encrypted password fields from the /etc/passwd file. chkaging assumes that administrative accounts will have their logins explicitly disabled and will show an * instead of a password. It ignores such accounts. Otherwise, each name is echoed with its aging information. The shell's set command parsing mechanism separates the aging information from the encrypted password. There is no comma in the 4-digit encryption character list.

Originally, the script simply output the warning that aging was inactive next to each login name. Soon, though, I ran into a system where almost every account had no aging. To simplify identifying such accounts for repair, I decided to accumulate the names into a NOAGING variable. After showing the active user list, I display the NOAGING names all at once in a columnar list. Once the NOAGING variable's handling and printing were in place, I commented out the two original lines.

The main processing routine decides whether to call show_aging to review the /etc/passwd file, to analyze the encrypted aging values (the -a option), or to analyze the decimal week code values (the -d option).

# Listing 2.4 (continued)

```
code = substr(digits, $1 + 1, 1);
code = code substr(digits, $2 + 1, 1);

elapsed = $3;
do
  quot = int(elapsed / 64);
  remn = elapsed % 64;
  base64 = substr(digits, remn + 1, 1) base64;
  base64 = base64 substr(digits, remn + 1, 1);
  elapsed = quot; while (elapsed >= 64);
  base64 = substr(digits, quot + 1, 1) base64;
  base64 = base64 substr(digits, quot + 1, 1);
  code = code base64;
  print code;
}

' digits=$DIGITS
|
#
# Given a full aging value (no comma), display its numeric values
#
aging_val ()
{
  code = $1
  if [ `expr length $code` -eq 2 ]
  then
    code=$[code]..
  else if [ `expr length $code` -lt 3 ]
  then
    echo Invalid aging code "$code"
    return
  fi
  fi

  MAX=`expr $code : '\(..)'`      # Grab max weeks
  MIN=`expr $code : ':\(..)'`    # Grab min weeks
  ELAPSED=`expr $code : ':\..\(*' ` # Grab weeks since epoch

echo "aging set to `weeknum $MAX` weeks max, \c"
echo "`weeknum $MIN` weeks min, \c"
echo "last changed `expr $NOW_WEEKS - \`weeknum $ELAPSED\`` weeks ago."
}
```
