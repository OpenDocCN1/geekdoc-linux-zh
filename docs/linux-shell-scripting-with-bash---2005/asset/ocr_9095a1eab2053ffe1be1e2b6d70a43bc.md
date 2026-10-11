This example counts customer orders stored as files in a directory. If there are not enough order files in the current directory, the script will run the statements between the `then` and `fi` keywords, printing a message and stopping the script.

The semicolon before the `then` is required. `then` is technically a separate command, although it works in conjunction with `if`. Because they are on one line, the semicolon is needed to separate the commands.

`if` commands can have an `else` part that is only executed when the condition fails.

```
NUM_ORDERS=`ls -1 | wc -1`
if [ "$NUM_ORDERS" -lt "$CUTOFF" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    printf "\n\n" "Starting to process the orders"
fi
```

`if` commands can be nested inside other `if` commands.

```
NUM_ORDERS=`ls -1 | wc -1`
if [ [ "$NUM_ORDERS" -lt $TOOFEW ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
else
    if [ [ "$NUM_ORDERS" -gt $TOOMANY ]; then
        printf "\n\n" "There are many orders.  Processing may take a long time"
    else
        printf "\n\n" "Starting to process the orders"
    fi
fi
```

The commands cannot be cross-nested; the inner `if` must always be completed before the outer `if`.

To choose between a series of alternatives, `if` commands can have an `elif` part. `elif` is a shortcut for `else if` and reduces unnecessary `if` nesting. The `elif` part can be followed by a final `else` part that, if it is present, is executed only when there are no alternatives. Combining these ideas, you can rewrite the previous example as follows.

```
NUM_ORDERS=`ls -1 | wc -1`
if [ "$NUM_ORDERS" -lt "$TOOFEW" ]; then
    printf "\n\n" "Too few orders...but will process them anyway"
elif [ "$NUM_ORDERS" -gt "$TOOMANY" ]; then
    printf "\n\n" "There are many orders.  Processing may take a long time"
else
    printf "\n\n" "Starting to process the orders"
fi
```

The `if` command doesn't have to be used with the `test` command. It can run and test the status code of any command.