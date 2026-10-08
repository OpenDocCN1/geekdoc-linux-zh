to restrict the search to only the beginning of the line, as shown in the following example:

```
# grep ^bin passwd.test
bin:*:1:1:bin:/bin:
```

![](bbox=[0.88, 0.12, 0.98, 0.2])

This search results in exactly the information in which we are interested, that is, a line beginning with *bin*. When using special characters, such as the caret(`^`) in this example, you should enclose the special characters in single quotes (`'`). Special characters may be interpreted by the shell and cause problems with the arguments we're trying to send to **grep**. Enclosing the search pattern in single quotes will ensures that the search pattern, in this case `^bin`, is passed directly to **grep**. The search pattern in single quotes looks like the following:

```
# grep '^bin' passwd.test
bin:*:1:1:bin:/bin:
```

Because we are going to have to search for this line in the **passwd.test** file after we find it, we may as well print out the line number as well as the line itself by using the *-n* option, as shown in the following example:

```
# grep -n '^bin' passwd.test
2:bin:*:1:1:bin:/bin:
```

The following is a summary of the **grep** command: