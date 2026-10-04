If the directory /usr/bin exists, the message Directory Found is displayed.

The opposite of && is the double bar (||). When two commands are separated by ||, the second command executes only if the first command returns a non-zero exit status (indicating failure).

Example:

```
ls -d /usr/foo || echo "No directory found"
```

If the directory does not exist, the following message is displayed:

```
/usr/foo: No such file or directory
No directory found
```

The Bourne shell contains the special programs true and false. The only function of the true program is to return a true (zero) exit status. Similarly, the function of the false program is to return a false (non-zero) exit status.

Example:

```
True && echo True
```

The system responds with True

```
False || echo False
```

The system responds with False

True and false tests will be discussed later when we discuss if and while conditionals.

The && and || are useful conditionals for creating very simple scripts, but additional functionality is sometimes required. The Bourne shell offers two more conditional commands, if and case.

# if

One of the more important built-ins of the Bourne shell is the if conditional. The syntax of the if conditional is

```
if condition-list
    then list
    elif condition-list
        then list
    else list
fi
```

The list following if is executed; if it returns a zero exit status, the list following the first then is executed. Otherwise the list following elif is executed; if its value is zero, the list following the next then is executed. Failing that, the else list is executed. If no list is