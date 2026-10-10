```
result=`expr $result + $increment`
done
```

```
echo "result is $result"
```

The example here is identical to the example for the while statement, except that the condition being tested is just the opposite of the condition specified in the while statement.

# # The shift Statement

The shift statement is used to process the positional parameters, one at a time, from left to right. As you\ll remember, the positional parameters are identified as $1, $2, $3, and so on. The effect of the shift command is that each positional parameter is moved one position to the left and the current $1 parameter is lost.

The shift statement is useful when you are writing shell programs in which a user can pass various options. Depending on the specified option, the parameters that follow can mean different things or might not be there at all.

The format of the shift command is as follows:

```
shift *number*
```

The parameter *number* is the number of places to be shifted and is optional. If not specified, the default is 1; that is, the parameters are shifted one position to the left. If specified, the parameters are shifted *number* positions to the left.

# # The if Statement

The if statement evaluates a logical expression to make a decision. An if condition has the following format in bash:

```
if [ *expression* ]; then
    *Statements*

elif [ *expression* ]; then
    *Statements*

else
    *Statements*

fi
```

The if conditions can be nested. That is, an if condition can contain another if condition within it. It isn\t necessary for an if condition to have an elif or else part. The else part is executed if none of the expressions that are specified in the if statement and are optional in subsequent elif statements are true. The word fi is used to indicate the end of an if statement, which is very useful if you have nested if conditions. In such a case, you should be able to match fi to if to ensure that all if statements are properly coded.