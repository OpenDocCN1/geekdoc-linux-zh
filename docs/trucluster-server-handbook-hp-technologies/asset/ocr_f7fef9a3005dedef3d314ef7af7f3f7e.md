```
# cat > tcrhb.evt
event {
    name        tcrhb.timeEvent.overDue
    format      "TCR HH: this book is overdue. $dueDate is the due date."
    priority    400
    var         {name dueDate type STRING value "Today"}
}
^D
```

Set the owner and permissions.

```
# chown root tcrhb.evt
# chmod 540 tcrhb.evt
```

Check the template file for syntax errors.

```
# evmrload -n
```

Tell EVM about the new template.

```
# evmreload
```

Post the new event.

```
# echo "event { name tcrhb.timeEvent.overDue }" | evmpost
```

Check to see if the event was posted.

```
# evmget -A -f "[name tcrhb]*"
TCR Handbook: this book is overdue. Today is the due date.
```

Post the event again. This time, pass a value to the "dueDate" variable.

```
# print "event
> { name tcrhb.timeEvent.overDue
>  var {name dueDate value "\${date}"} }" | evmpost
```

Retrieve the events. This time you should see two events since this is the second time we have posted an event.

```
# evmget -A -f "[name tcrhb]*"
TCR Handbook: this book is overdue. Today is the due date.
TCR Handbook: this book is overdue. Mon Mar 26 05:34:29 EST 2001 is the due date.
```