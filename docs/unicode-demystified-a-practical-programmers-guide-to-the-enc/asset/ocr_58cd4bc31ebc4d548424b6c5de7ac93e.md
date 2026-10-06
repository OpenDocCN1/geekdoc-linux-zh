```
if test-command
then
    commands
else
    commands
fi
```

![](bbox=[0.395, 0.203, 0.755, 0.51])

Because a semicolon ( ends a command just as a NEWLINE on the same line as if by preceding it with a semicolon. (Because if and then are separate builtins, they require a command separator between them; a semicolon and NEWLINE work equally well.) Some people prefer this notation for aesthetic reasons; others, because it saves space:

```
if test-command; then
    commands
else
    commands
fi
```

If the test-command returns a true status, the if structure executes the commands between the then and else statements and then diverts control to the statement following fi. If the test-command returns a false status, the if structure executes the commands following the else statement.