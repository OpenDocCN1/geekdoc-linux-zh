```
monthly )
    sh /etc/monthly 2>&1 | tee /var/log/monthly.out | \
    mail -s "`hostname` monthly output" root
;;
* ) echo "Usage: `basename $0` [daily|weekly|monthly]"
esac

exit 0
```

This is a longer shell script, but if we look at it in sections, it's really no more complex than the earlier examples. In particular, notice that the case statement structure is

```
case $1 in
  daily ) statements
  ;;
  weekly ) statements
  ;;
  monthly ) statements
  ;;
  * ) statements
esac
```

This is more or less equivalent to

```
if [ $1 = daily ] ; then
  statements
elif [ $1 = weekly ] ; then
  statements
elif [ $1 = monthly ] ; then
  statements
else
  statements
fi
```

The only difference is that case statement clauses can do wildcard pattern matching, so whereas a conditional test with an if statement that matched dail* would be difficult to write, it's a breeze as part of a case statement: dail* )

Indeed, you'll often see complex regular expressions as part of case statements, and a set of choices to allow for, say, both single-character and longer flags is very common, and might look like this:

```
-a | --append ) statements
```

Also note that in the case statement that each block is ended with the all important double semicolon (;;), without which the script will drop through into the statements associated with the next condition. On the last case, of course, there is no "next" condition, so it can be omitted.